---
description: xp_logevent (Transact-sql)
title: xp_logevent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7001b9d29a96dd192e044ddfe779b8f39a581a94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419276"
---
# <a name="xp_logevent-transact-sql"></a>xp_logevent (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログファイルと Windows イベントビューアーにユーザー定義メッセージを記録し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 xp_logevent を使用すると、クライアントにメッセージを送信せずにアラートを送信できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>引数  
 *error_number*  
 50,000 より大きい、ユーザー定義のエラー番号を指定します。 最大値は 2147483647 (2 ^ 31-1) です。  
  
 **'** *message* **'**  
 最大 2048 バイトまでの文字列を指定します。  
  
 **'** *severity* **'**  
 は、3つの文字列 (情報、警告、またはエラー) のいずれかです。 *重大度* は省略可能で、既定値は情報です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 xp_logevent ではコード例に対し、次のエラー メッセージが返されます。  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>解説  
 プロシージャ、トリガー、バッチなどからメッセージを送信する場合は [!INCLUDE[tsql](../../includes/tsql-md.md)] 、xp_logevent ではなく RAISERROR ステートメントを使用します。 xp_logevent は、クライアントのメッセージハンドラーを呼び出さず、@ を設定 @ERROR します。 のインスタンス内の Windows イベントビューアーおよびエラーログファイルにメッセージを書き込むには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、RAISERROR ステートメントを実行します。  
  
## <a name="permissions"></a>アクセス許可  
 Master データベースの db_owner 固定データベースロールのメンバーシップ、または sysadmin 固定サーバーロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、Windows イベントビューアーのメッセージに渡された変数を使用して、メッセージをログに記録します。  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>参照  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;の一般的な拡張ストアドプロシージャ ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
