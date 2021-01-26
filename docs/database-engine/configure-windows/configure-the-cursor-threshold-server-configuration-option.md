---
title: cursor threshold サーバー構成オプションの構成 | Microsoft Docs
description: cursor threshold オプションについて説明します。 SQL Server によってカーソル キーセットが非同期に生成されるかどうかにこの値がどのように影響するかを説明し、その設定方法について説明します。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
author: markingmyname
ms.author: maghan
ms.openlocfilehash: de30cb4bcf672fdf47ab926a28680baa1d9b1067
ms.sourcegitcommit: 2f3f5920e0b7a84135c6553db6388faf8e0abe67
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98783287"
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>cursor threshold サーバー構成オプションの構成
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 **で** または [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cursor threshold [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **cursor threshold** オプションは、カーソル キーセットが非同期に生成されるカーソル セット内の行数を指定します。 カーソルが結果セットのキーセットを生成するとき、その結果セットに返される行数をクエリ オプティマイザーが予測します。 返される行数がこのしきい値を超えていると予測された場合、カーソルは非同期に生成されます。これにより、ユーザーはカーソルの作成が続行されている間に行を取り出すことができます。 返される行数がこのしきい値以下と予測された場合、カーソルは同期をとって生成され、すべての行が返されるまでクエリが待機します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して cursor threshold オプションを構成するには**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [cursor threshold オプションを構成した後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、キーセット ドリブン カーソルまたは静的 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルの非同期な作成はサポートされません。 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソル操作はバッチで行われます。したがって、 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルを非同期に生成する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各カーソル操作におけるクライアントのラウンド トリップのため、待機時間が少ない OPEN が問題になるような非同期キーセット ドリブン カーソルまたは静的 API (アプリケーション プログラミング インターフェイス) サーバー カーソルは、 で引き続きサポートされます。  
  
-   キーセットの行数を予測するクエリ オプティマイザーの精度は、カーソル内の各テーブルの統計の新しさによって左右されます。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロフェッショナルだけが変更するようにしてください。  
  
-   **cursor threshold** を -1 に設定すると、すべてのキーセットが同期して生成されます。これはカーソル セットが小さい場合に役立ちます。 **cursor threshold** を 0 に設定すると、すべてのカーソル キーセットが非同期に生成されます。 それ以外の値を設定した場合、クエリ オプティマイザーによってカーソル セットの予測行数が比較され、 **cursor threshold** に設定した値を超えていれば、キーセットが非同期に生成されます。 小さな結果セットは同期をとって作成する方がよいので、 **cursor threshold** の値は小さくしすぎないでください。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>cursor threshold オプションを設定するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ノードをクリックします。  
  
3.  **[その他]** の **[カーソルのしきい値]** オプションを目的の値に変更します。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>cursor threshold オプションを設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して `cursor threshold` オプションを `0` に設定して、カーソル キーセットを非同期に生成する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="follow-up-after-you-configure-the-cursor-threshold-option"></a><a name="FollowUp"></a>補足情報: cursor threshold オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
