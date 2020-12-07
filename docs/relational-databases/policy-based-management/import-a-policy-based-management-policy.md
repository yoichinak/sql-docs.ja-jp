---
description: ポリシー ベースの管理ポリシーのインポート
title: ポリシー ベースの管理ポリシーのインポート | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1ea5d3c83667dbd194e9fb82ae7bce2e815d479b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "91412769"
---
# <a name="import-a-policy-based-management-policy"></a>ポリシー ベースの管理ポリシーのインポート
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ポリシー インスタンスをインポートする方法について説明します。  
  
## <a name="permissions"></a>アクセス許可
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。

  
##  <a name="using-sql-server-management-studio"></a>SQL Server Management Studio を使用する  
  
### <a name="to-import-a-policy-instance"></a>ポリシー インスタンスをインポートするには  
  
1.  **オブジェクト エクスプローラー** で、プラス記号をクリックして、新しくインポートするポリシー インスタンスを配置するサーバーを展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  **[ポリシー]** フォルダーを右クリックし、 **[ポリシーのインポート]** をクリックします。  
  
5.  **[インポート]** ダイアログ ボックスで、ファイルのパスと名前を入力します。または、参照ボタン (**[...]**) を使用してポリシーを含んでいる XML ファイルを特定し、ファイルを選択します。 **[インポート]** ダイアログ ボックスで利用可能なオプションの詳細については、「 [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md)」を参照してください。  
  
6.  完了したら、 **[OK]** をクリックします。  


## <a name="example-policies"></a>ポリシーの例
 ポリシーの例は、[SQL Server のサンプル コード リポジトリ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/epm-framework/sample-policies)にあります。 これらのポリシーは、ご自分のポリシー ベースの管理ポリシーの基礎としてインポートおよび使用できます。
