---
description: catalog.remove_data_tap
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca55276a6108cd53ffae82fd4c40089023da20fb
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243616"
---
# <a name="catalogremove_data_tap"></a>catalog.remove_data_tap 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  実行内のコンポーネント出力からデータ タップを削除します。 データ タップの一意な識別子が実行のインスタンスに関連付けられています。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>引数  
 [ @data_tap_id = ] *data_tap_id*  
 catalog.add_data_tap ストアド プロシージャを使用して作成されるデータ タップの一意識別子。 *data_tap_id* は **bigint** です。  
  
## <a name="remarks"></a>注釈  

- パッケージに同じ名前の複数のデータ フロー タスクが含まれる場合、データ タップは指定された名前で最初に見つかったデータ フロー タスクに追加されます。  
  
- データ タップを削除するには、実行のインスタンスが作成済みの状態 ( [catalog.operations &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) ビューの **status** 列の値が 1) である必要があります。  
  
## <a name="return-codes"></a>リターン コード  
 成功した場合は 0 を返します。  
  
 ストアド プロシージャが失敗した場合は、エラーをスローします。  
  
## <a name="result-set"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 ストアド プロシージャが失敗する原因となる条件を以下に示します。  
  
-   ユーザーに MODIFY 権限がない。  
  
## <a name="see-also"></a>関連項目  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
