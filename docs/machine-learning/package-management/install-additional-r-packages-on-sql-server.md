---
title: 새 R 패키지 설치
description: sqlmlutils를 사용하여 SQL Server Machine Learning Services 인스턴스에 새 R 패키지를 설치하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/04/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d3f7c61420dc1b85f7f40854dce9931d25aef895
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870496"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>sqlmlutils를 사용하여 새 R 패키지 설치

[!INCLUDE [SQL Server 2019 SQL MI](../../includes/applies-to-version/sqlserver2019-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
이 문서에서는 [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) 패키지의 함수를 사용하여 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 및 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md) 인스턴스에 새 R 패키지를 설치하는 방법을 설명합니다. 설치하는 패키지는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) T-SQL 문을 사용하여 데이터베이스 내에서 실행되는 R 스크립트에서 사용할 수 있습니다.

> [!NOTE]
> 이 문서에서 설명하는 **sqlmlutils** 패키지는 SQL Server 2019 이상에 R 패키지를 추가하는 데 사용됩니다. SQL Server 2017 이전 버전의 경우 [R 도구를 사용하여 패키지 설치](./install-r-packages-standard-tools.md?view=sql-server-2017)를 참조하세요.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
이 문서에서는 [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) 패키지의 함수를 사용하여 [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 인스턴스에 새 R 패키지를 설치하는 방법을 설명합니다. 설치하는 패키지는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) T-SQL 문을 사용하여 데이터베이스 내에서 실행되는 R 스크립트에서 사용할 수 있습니다.
::: moniker-end

## <a name="prerequisites"></a>사전 요구 사항

- SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에 [R](https://www.r-project.org) 및 [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)을 설치합니다. 스크립트 실행에 아무 R IDE를 사용해도 되지만, 이 문서에서는 RStudio를 사용하는 것으로 가정합니다.

- SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에 [Azure Data Studio](../../azure-data-studio/what-is.md)를 설치합니다. 다른 데이터베이스 관리 또는 쿼리 도구를 사용할 수 있지만, 이 문서에서는 Azure Data Studio를 사용한다고 가정합니다.

### <a name="other-considerations"></a>기타 고려 사항

- 패키지 설치는 **sqlmlutils** 에 제공하는 연결 정보를 통해 지정한 SQL 인스턴스, 데이터베이스 및 사용자에게 적용됩니다. 패키지를 여러 SQL 인스턴스 또는 데이터베이스에서 사용하거나 여러 사용자가 사용하도록 하려면 각각에 대해 패키지를 설치해야 합니다. 단, 패키지를 `dbo`의 멤버가 설치하는 경우 패키지는 공용이며 모든 사용자와 공유됩니다. 사용자가 새 버전의 공용 패키지를 설치하는 경우 공용 패키지는 영향을 받지 않지만 해당 사용자는 새 버전에 액세스할 수 있습니다.

- SQL Server에서 실행되는 R 스크립트는 기본 인스턴스 라이브러리에 설치된 패키지만 사용할 수 있습니다. SQL Server는 외부 라이브러리의 패키지를 로드할 수 없으며, 라이브러리가 동일한 컴퓨터에 있더라도 마찬가지입니다. 여기에는 다른 Microsoft 제품과 함께 설치된 R 라이브러리가 포함됩니다.

- 강화된 SQL Server 환경에서는 다음을 방지해야 할 수 있습니다.
  - 네트워크 액세스가 필요한 패키지
  - 상승된 파일 시스템 액세스 권한이 필요한 패키지
  - 웹 개발 또는 SQL Server 내에서 실행해도 장점이 없는 기타 태스크에 사용되는 패키지

## <a name="install-sqlmlutils-on-the-client-computer"></a>클라이언트 컴퓨터에 sqlmlutils 설치

**sqlmlutils** 를 사용하려면 먼저 SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에 sqlmlutils를 설치해야 합니다.

**sqlmlutils** 패키지는 **RODBCext** 패키지에 종속되며, **RODBCext** 는 다른 여러 패키지에 종속됩니다. 다음은 이러한 패키지를 올바른 순서로 설치하는 절차입니다.

### <a name="install-sqlmlutils-online"></a>온라인으로 sqlmlutils 설치

클라이언트 컴퓨터에서 인터넷에 액세스할 수 있는 경우 **sqlmlutils** 및 해당 종속 패키지를 온라인으로 다운로드하여 설치할 수 있습니다.

1. 최신 **sqlmlutils** 파일(Windows의 경우 `.zip`, Linux의 경우 `.tar.gz`)을 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 에서 클라이언트 컴퓨터로 다운로드합니다. 파일을 확장하지 않습니다.

1. **명령 프롬프트** 를 열고 다음 명령을 실행하여 **RODBCext** 및 **sqlmlutils** 를 설치합니다. 다운로드한 **sqlmlutils** 파일의 경로를 대체합니다. **RODBCext** 패키지는 온라인으로 찾아서 설치합니다.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='https://mran.microsoft.com/snapshot/2019-02-01/')"
   R CMD INSTALL sqlmlutils_0.7.1.zip
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='https://mran.microsoft.com/snapshot/2019-02-01/')"
   R CMD INSTALL sqlmlutils_0.7.1.tar.gz
   ```
   ::: moniker-end

### <a name="install-sqlmlutils-offline"></a>오프라인으로 sqlmlutils 설치

클라이언트 컴퓨터가 인터넷에 연결되어 있지 않은 경우에는 인터넷에 액세스할 수 있는 컴퓨터를 사용하여 **RODBCext** 및 **sqlmlutils** 패키지를 미리 다운로드해야 합니다. 그런 다음, 클라이언트 컴퓨터의 폴더에 파일을 복사하고 오프라인으로 패키지를 설치할 수 있습니다.

**RODBCext** 패키지에는 여러 종속 패키지가 포함되어 있으므로 패키지의 모든 종속 요소를 식별하기가 어렵습니다. 따라서 [**miniCRAN**](https://andrie.github.io/miniCRAN/)을 사용하여 모든 종속 패키지가 포함된 패키지의 로컬 리포지토리 폴더를 만드는 것이 좋습니다.
자세한 내용은 [miniCRAN을 사용하여 로컬 R 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)를 참조하세요.

**sqlmlutils** 패키지는 클라이언트 컴퓨터에 복사하여 설치할 수 있는 단일 파일로 구성되어 있습니다.

인터넷에 액세스할 수 있는 컴퓨터의 경우:

1. **miniCRAN** 을 설치합니다. 자세한 내용은 [miniCRAN 설치](create-a-local-package-repository-using-minicran.md#install-minicran)를 참조하세요.

1. RStudio에서 다음 R 스크립트를 실행하여 **RODBCext** 패키지의 로컬 리포지토리를 만듭니다. 이 예에서는 `rodbcext` 폴더에 리포지토리가 생성된 것으로 가정합니다.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2019-02-01/")
   local_repo <- "rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2019-02-01/")
   local_repo <- "rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```
   ::: moniker-end

   `Rversion` 값으로는 SQL Server에 설치된 R 버전을 사용합니다. 설치된 버전을 확인하려면 다음 T-SQL 명령을 사용합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. [https://github.com/Microsoft/sqlmlutils/tree/master/R/dist](https://github.com/Microsoft/sqlmlutils/tree/master/R/dist)에서 최신 **sqlmlutils** 파일(Windows의 경우 `.zip` , Linux의 경우 `.tar.gz` )을 다운로드합니다. 파일을 확장하지 않습니다.

1. 전체 **RODBCext** 리포지토리 폴더와 **sqlmlutils** 파일을 클라이언트 컴퓨터로 복사합니다.

SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에서 다음을 수행합니다.

1. 명령 프롬프트를 엽니다.

1. 다음 명령을 실행하여 **RODBCext** 와 **sqlmlutils** 를 차례로 설치합니다. 이 컴퓨터에 복사한 **RODBCext** 리포지토리 폴더와 **sqlmlutils** 파일의 전체 경로를 대체합니다.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='rodbcext')"
   R CMD INSTALL sqlmlutils_0.7.1.zip
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='rodbcext')"
   R CMD INSTALL sqlmlutils_0.7.1.tar.gz
   ```
   ::: moniker-end

## <a name="add-an-r-package-on-sql-server"></a>SQL Server에서 R 패키지 추가

다음 예제에서는 SQL Server에 [**glue**](https://cran.r-project.org/web/packages/glue/) 패키지를 추가합니다.

### <a name="add-the-package-online"></a>온라인으로 패키지 추가

SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터가 인터넷에 연결되어 있는 경우 **sqlmlutils** 를 사용하여 인터넷을 통해 **glue** 패키지와 종속성을 찾은 다음, 원격으로 SQL Server 인스턴스에 패키지를 설치할 수 있습니다.

1. 클라이언트 컴퓨터에서 RStudio를 열고 새 **R 스크립트** 파일을 만듭니다.

1. 다음 R 스크립트를 사용하여 **sqlmlutils** 를 통해 **glue** 패키지를 설치합니다. 사용자의 SQL Server 데이터베이스 연결 정보를 대체합니다.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server   = "server",
     database = "database",
     uid      = "username",
     pwd      = "password")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > **범위** 는 **공용** 또는 **전용** 일 수 있습니다. 공용 범위는 모든 사용자가 사용할 수 있는 패키지를 설치하려는 데이터베이스 관리자에게 유용 합니다. 프라이빗 범위는 패키지를 설치하는 사용자만 패키지를 사용할 수 있습니다. 범위를 지정하지 않으면 기본 범위인 **프라이빗** 이 사용됩니다.

### <a name="add-the-package-offline"></a>오프라인으로 패키지 추가

클라이언트 컴퓨터가 인터넷에 연결되어 있지 않은 경우에는 인터넷에 액세스할 수 있는 컴퓨터에서 **miniCRAN** 을 사용하여 **glue** 패키지를 다운로드할 수 있습니다. 그런 다음, 패키지를 오프라인으로 설치할 수 있는 클라이언트 컴퓨터에 이 패키지를 복사합니다.
**miniCRAN** 설치에 대한 자세한 내용은 [miniCRAN 설치](create-a-local-package-repository-using-minicran.md#install-minicran)를 참조하세요.

인터넷에 액세스할 수 있는 컴퓨터의 경우:

1. 다음 R 스크립트를 실행하여 **glue** 에 대한 로컬 리포지토리를 만듭니다. 다음 예제는 `c:\downloads\glue`에 리포지토리 폴더를 만듭니다.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```
   ::: moniker-end

   `Rversion` 값으로는 SQL Server에 설치된 R 버전을 사용합니다. 설치된 버전을 확인하려면 다음 T-SQL 명령을 사용합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 전체 **glue** 리포지토리 폴더(`c:\downloads\glue`)를 클라이언트 컴퓨터에 복사합니다. 예를 들어 `c:\temp\packages\glue` 폴더에 복사합니다.

클라이언트 컴퓨터의 경우:

1. RStudio를 열고 새 **R 스크립트** 파일을 만듭니다.

1. 다음 R 스크립트를 사용하여 **sqlmlutils** 를 통해 **glue** 패키지를 설치합니다. SQL Server 데이터베이스 연결 정보를 바꿉니다(Windows 인증을 사용하지 않는 경우 `uid` 및 `pwd` 매개 변수 추가).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > **범위** 는 **공용** 또는 **전용** 일 수 있습니다. 공용 범위는 모든 사용자가 사용할 수 있는 패키지를 설치하려는 데이터베이스 관리자에게 유용 합니다. 프라이빗 범위는 패키지를 설치하는 사용자만 패키지를 사용할 수 있습니다. 범위를 지정하지 않으면 기본 범위인 **프라이빗** 이 사용됩니다.

## <a name="use-the-package"></a>패키지 사용

**glue** 패키지가 설치되었으면 T-SQL **sp_execute_external_script** 명령을 사용하여 SQL Server의 R 스크립트에서 glue 패키지를 사용할 수 있습니다.

1. Azure Data Studio를 열고 SQL Server 데이터베이스에 연결합니다.

1. 다음 명령 실행:

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **결과**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>패키지 제거

**glue** 패키지를 제거하려면 다음 R 스크립트를 실행합니다. 앞에서 정의한 **연결** 변수를 사용합니다.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>다음 단계

- 설치된 R 패키지에 대한 자세한 내용은 [R 패키지 정보 가져오기](r-package-information.md)를 참조하세요.
- R 패키지 사용에 대한 도움말은 [R 패키지 사용 팁](tips-for-using-r-packages.md)을 참조하세요.
- Python 패키지 설치에 대한 자세한 내용은 [pip를 사용하여 Python 패키지 설치](install-additional-python-packages-on-sql-server.md)를 참조하세요.
- SQL Server Machine Learning Services에 대한 자세한 내용은 [SQL Server Machine Learning Services(Python 및 R)란?](../sql-server-machine-learning-services.md)을 참조하세요.