---
title: SQL_NUMERIC_STRUCT를 사용 하 여 숫자 데이터 검색 | Microsoft Docs
description: ODBC를 사용 하는 c/c + +는 SQL_C_NUMERIC와 관련 된 SQL_NUMERIC_STRUCT를 사용 하 여 SQL Server numeric 데이터 형식을 검색 합니다.
editor: ''
ms.prod: sql
ms.technology: connectivity
ms.devlang: cpp
ms.topic: conceptual
ms.custom: ''
ms.date: 07/14/2017
ms.author: v-daenge
author: David-Engel
ms.openlocfilehash: 63575c952feb8fc21d56f48540a7cd4e54d5e11f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305124"
---
# <a name="retrieve-numeric-data-with-sql_numeric_struct"></a>SQL\_숫자\_구조체로 숫자 데이터 검색

이 문서에서는 SQL Server ODBC 드라이버에서 숫자 데이터를 검색 하는 방법을 설명 합니다. 또한 특정 전체 자릿수 및 소수 자릿수 값을 사용 하 여 올바른 값을 가져오는 방법을 설명 합니다.

이 데이터 형식을 사용 하면 응용 프로그램에서 숫자 데이터를 직접 처리할 수 있습니다. 2003 년에 odbc 3.0에는 **\_SQL c\_숫자로**식별 되는 새로운 odbc C 데이터 형식이 도입 되었습니다. 이 데이터 형식은 여전히 2017와 관련이 있습니다.

사용 되는 C 버퍼에는 **\_SQL 숫자\_구조체**의 형식 정의가 있습니다. 이 구조에는 숫자 데이터의 전체 자릿수, 소수 자릿수, 부호 및 값을 저장 하는 필드가 있습니다. 값 자체는 가장 왼쪽 위치에서 시작 하 여 최하위 바이트로 크기가 조정 된 정수로 저장 됩니다. 

[C 데이터 형식](c-data-types.md) 문서에서는 SQL\_숫자\_구조체의 형식 및 사용에 대 한 자세한 정보를 제공 합니다. 일반적으로 ODBC 3.0 프로그래머 참조의 [부록 D](appendix-d-data-types.md) 는 데이터 형식에 대해 설명 합니다.


## <a name="sql_numeric_struct-overview"></a>SQL\_숫자\_구조체 개요


SQL\_숫자\_구조체는 sqltypes 헤더 파일에서 다음과 같이 정의 됩니다.


```c
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
숫자 구조의 전체 자릿수 및 소수 자릿수 필드는 응용 프로그램의 입력에는 사용 되지 않으며, 응용 프로그램에 대 한 드라이버의 출력에만 사용 됩니다.

드라이버는 응용 프로그램에 데이터를 반환할 때마다 기본 전체 자릿수 (드라이버 정의) 및 기본 소수 자릿수 (0)를 사용 합니다. 응용 프로그램에서 전체 자릿수 및 소수 자릿수에 대 한 값을 지정 하지 않는 한 드라이버는 기본값을 가정 하 고 숫자 데이터의 소수 부분을 자릅니다.

## <a name="sql_numeric_struct-code-sample"></a>SQL\_숫자\_구조체 코드 샘플

이 코드 샘플에서는 다음 작업을 수행 하는 방법을 보여 줍니다.

- 전체 자릿수를 설정 합니다.
- 크기를 설정 합니다.
- 올바른 값을 검색 합니다. 

> [!Note]
> 이 문서에서 제공 하는 코드를 사용 하는 것은 사용자의 책임입니다. 
>
> Microsoft는 상품성 및/또는 특정 목적에의 적합성에 대 한 묵시적 보증을 포함 하 되이에 제한 되지 않는 모든 종류의 보증 없이 "있는 그대로" 이러한 코드 샘플을 제공 합니다.

```c
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>중간 결과:


```console
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


숫자 구조에서 val 필드는 16 개 요소의 문자 배열입니다. 예를 들어 25.212는 25212으로 크기가 조정 되 고 배율은 3입니다. 16 진수 형식으로,이 수는 27C입니다.

드라이버는 다음 항목을 반환 합니다.

- ' | ' 인 7C의 상응 하는 문자 (파이프)를 문자 배열의 첫 번째 요소에 있습니다.
- 두 번째 요소에서 ' b ' 인 62에 해당 하는 값입니다.
- 배열 요소의 나머지에 0을 포함 하므로 버퍼에 ' | b\0 \ '가 포함 됩니다.

이제이 문자열 배열에서 크기 조정 된 정수를 구성 하는 것이 쉽지 않습니다. 문자열의 각 문자는 두 개의 16 진수 숫자 (LSD)와 가장 중요 한 숫자 (MSD)에 해당 합니다. 크기 조정 된 정수 값은 1부터 시작 하 여 각 숫자 (LSD & MSD)를 16의 배수로 곱하여 생성할 수 있습니다.

Little endian 모드에서 크기 조정 된 정수로의 변환을 구현 하는 코드입니다. 응용 프로그램 개발자는이 기능을 구현 해야 합니다. 다음 코드 예제는 가능한 여러 가지 방법 중 하나일 뿐입니다.


```c
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>버전에 적용


SQL\_숫자\_구조체에 대 한 이전 정보는 다음 제품 버전에 적용 됩니다.

- Microsoft SQL Server 3.7 용 Microsoft ODBC 드라이버
- Microsoft 데이터 액세스 구성 요소 2.1
- Microsoft 데이터 액세스 구성 요소 2.5
- Microsoft 데이터 액세스 구성 요소 2.6
- Microsoft 데이터 액세스 구성 요소 2.7


## <a name="sql_c_numeric-overview"></a>SQL\_C\_숫자 개요


다음 샘플 프로그램은 테이블에 123.45을 삽입\_하\_여 SQL C 숫자를 사용 하는 방법을 보여 줍니다. 테이블에서 열은 전체 자릿수 5와 소수 자릿수 2를 사용 하 여 숫자 또는 10 진수로 정의 됩니다.

이 프로그램을 실행 하는 데 사용 하는 ODBC 드라이버는 ODBC 3.0 기능을 지원 해야 합니다.


```c
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

https://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/help/222831

https://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

https://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/sql/odbc/reference/appendixes/c-data-types
-->

