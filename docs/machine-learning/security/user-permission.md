---
title: Python スクリプトと R スクリプトを実行する権限を許可する
description: SQL Server Machine Learning Services で外部の Python スクリプトおよび R スクリプトを実行する権限をユーザーに許可する方法とデータベースに対する読み取り、書き込み、またはデータ定義言語 (DDL) の権限を許可する方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019, contperfq4
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 7c7fa9d7702fb93fd4fe8334f873eb1b66c0f61d
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115277"
---
# <a name="grant-users-permission-to-execute-python-and-r-scripts-with-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services で Python スクリプトと R スクリプトを実行する権限をユーザーに許可する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で外部の Python スクリプトおよび R スクリプトを実行する権限をユーザーに許可する方法とデータベースに対する読み取り、書き込み、またはデータ定義言語 (DDL) の権限を許可する方法について説明します。

詳細については、「[機能拡張フレームワークのセキュリティ概要](../../machine-learning/concepts/security.md#permissions)」の「権限」セクションを参照してください。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>スクリプトを実行する権限

SQL Server Machine Learning Services で Python スクリプトまたは R スクリプトを実行する、管理者ではない各ユーザーに対して、その言語が使用されている各データベースで外部スクリプトを実行する権限を許可する必要があります。

外部スクリプトを実行する権限を許可するには、次のようにします。

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> サポートされているスクリプト言語には、権限が固有ではありません。 言い換えると、R スクリプトと Python スクリプトには個別の権限レベルがありません。

<a name="permissions-db"></a>

## <a name="grant-databases-permissions"></a>データベースの権限の許可

ユーザーがスクリプトを実行している間、ユーザーは他のデータベースからデータを読み取ることが必要になる場合があります。 ユーザーは、結果を格納したり、テーブルにデータを書き込んだりするために、新しいテーブルを作成することが必要になる場合もあります。

R スクリプトまたは Python スクリプトを実行している Windows ユーザー アカウントまたは SQL ログインがそれぞれ、特定のデータベースに対して適切なアクセス許可を持っていることを確認します。 

+ データを読み取るための `db_datareader`。
+ オブジェクトをデータベースに保存するための `db_datawriter`。
+ トレーニングおよびシリアル化されたデータを含むストアド プロシージャまたはテーブルなどのオブジェクトを作成する `db_ddladmin`。

たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、SQL ログインである *MySQLLogin* に、*ML_Samples* データベースで T-SQL クエリを実行する権限を与えています。 このステートメントを実行するには、SQL ログインがサーバーのセキュリティ コンテキストに既に存在している必要があります。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>次のステップ

各ロールに含まれる権限の詳細については、「[データベース レベルのロール](../../relational-databases/security/authentication-access/database-level-roles.md)」をご覧ください。
