---
title: sp_rda_test_connection (Transact-sql) |Microsoft Docs
description: Sp_rda_test_connection を使用して SQL Server からリモート Azure サーバーへの接続をテストし、データ移行を妨げる可能性のある問題を報告する方法について説明します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 031e3abe622a4a15fa9656e65bce80b5eaf27365
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540406"
---
# <a name="syssp_rda_test_connection-transact-sql"></a>sp_rda_test_connection (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  SQL Server からリモート Azure サーバーへの接続をテストし、データ移行を妨げる可能性のある問題を報告します。  
  
## <a name="syntax"></a>構文  
  
```  
  
EXECUTE sys.sp_rda_test_connection  
   @database_name = N'db_name',   
   @server_address = N'azure_server_fully_qualified_address',  
   @azure_username = N'azure_username',   
   @azure_password = N'azure_password',  
   @credential_name = N'credential_name'  
  
```  
  
## <a name="arguments"></a>引数  
 @database_name = N '*db_name*'  
 Stretch が有効な SQL Server データベースの名前。 このパラメーターは省略可能です。  
  
 @server_address = N '*azure_server_fully_qualified_address*'  
 Azure サーバーの完全修飾アドレス。  
  
-   ** \@ Database_name**に値を指定しても、指定したデータベースで Stretch が有効になっていない場合は、 ** \@ server_address**の値を指定する必要があります。  
  
-   ** \@ Database_name**の値を指定し、指定されたデータベースで Stretch が有効になっている場合、 ** \@ server_address**の値を指定する必要はありません。 ** \@ Server_address**に値を指定した場合、ストアドプロシージャはそれを無視し、既に Stretch が有効なデータベースに関連付けられている既存の Azure サーバーを使用します。  
  
 @azure_username = N '*azure_username*  
 リモート Azure サーバーのユーザー名。  
  
 @azure_password = N '*azure_password*'  
 リモート Azure サーバーのパスワード。  
  
 @credential_name = N '*credential_name*'  
 ユーザー名とパスワードを指定する代わりに、Stretch が有効なデータベースに格納されている資格情報の名前を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **成功**した場合、sp_rda_test_connection によってエラー 14855 (STRETCH_MAJOR、STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) と重大度 EX_INFO および成功したリターンコードが返されます。  
  
 エラーが **発生**した場合、sp_rda_test_connection によってエラー 14856 (STRETCH_MAJOR、STRETCH_CONNECTION_TEST_PROC_FAILED) と重大度 EX_USER およびエラーリターンコードが返されます。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|link_state|INT|次のいずれかの値。 **link_state_desc**の値に対応します。<br /><br /> -0<br />-1<br />-2<br />-3<br />-4|  
|link_state_desc|varchar(32)|次のいずれかの値。 **link_state**の前の値に対応します。<br /><br /> -正常<br />     SQL Server とリモート Azure サーバーの間のが正常な状態です。<br />-ERROR_AZURE_FIREWALL<br />     Azure ファイアウォールによって、SQL Server とリモート Azure サーバー間のリンクが妨げられています。<br />-ERROR_NO_CONNECTION<br />     SQL Server は、リモートの Azure サーバーに接続することはできません。<br />-ERROR_AUTH_FAILURE<br />     認証エラーにより、SQL Server とリモート Azure サーバーの間のリンクが妨げられています。<br />-エラー<br />     認証の問題、接続の問題、またはファイアウォールの問題ではないエラーにより、SQL Server とリモート Azure サーバーの間のリンクが妨げられています。|  
|error_number|INT|エラーの番号。 エラーがない場合、このフィールドは NULL になります。|  
|error_message|nvarchar(1024)|エラー メッセージ。 エラーがない場合、このフィールドは NULL になります。|  
  
## <a name="permissions"></a>アクセス許可  
 Db_owner のアクセス許可が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>SQL Server からリモート Azure サーバーへの接続を確認する  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 結果は、SQL Server がリモートの Azure サーバーに接続できないことを示しています。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<connection-related error number>*|*\<connection-related error message>*|  
  
### <a name="check-the-azure-firewall"></a>Azure ファイアウォールを確認する  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果は、Azure ファイアウォールが SQL Server とリモート Azure サーバー間のリンクを妨げていることを示しています。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<firewall-related error number>*|*\<firewall-related error message>*|  
  
### <a name="check-authentication-credentials"></a>認証資格情報の確認  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果には、認証エラーが原因で、SQL Server とリモート Azure サーバーの間のリンクが妨げられていることがわかります。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<authentication-related error number>*|*\<authentication-related error message>*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>リモート Azure サーバーの状態を確認する  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 結果は、接続が正常であることと、指定されたデータベースの Stretch Database を有効にできることを示しています。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|戻ら|NULL|NULL|  
  
  
