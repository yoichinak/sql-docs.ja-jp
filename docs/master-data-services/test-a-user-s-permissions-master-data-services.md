---
description: ユーザーのアクセス許可のテスト (マスター データ サービス)
title: ユーザー&#39;のアクセス許可のテスト
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 90299ab429b38e3c851b51273742c5fef28fec40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471905"
---
# <a name="test-a-user39s-permissions-master-data-services"></a>ユーザーのアクセス許可のテスト (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、テスト ユーザーを作成し、Web アプリケーションにログインして権限をテストできます。ユーザーが [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] の URL にアクセスを試みると、ユーザーの資格情報が認証されます。 Internet Explorer のセキュリティ設定によって、自動認証を行うかユーザー名とパスワードの入力を求めるかが制御されます。 これらの設定を変更するには、次の手順を実行します。  
  
### <a name="to-test-a-users-security"></a>ユーザーのセキュリティをテストするには  
  
1.  Internet Explorer 7 以降で、 **[ツール]**、 **[インターネット オプション]** の順にクリックして、 **[セキュリティ]** タブをクリックします。  
  
2.  **[ローカル イントラネット]** をクリックして、 **[レベルのカスタマイズ]** ボタンをクリックします。  
  
3.  **[ユーザー認証]** セクションで **[ユーザー名とパスワードを入力してログオンする]** をクリックします。  
  
4.  次にブラウザー ウィンドウを開くときに、ユーザー名とパスワードの入力を求められます。  
  
## <a name="see-also"></a>参照  
 [セキュリティ (マスター データ サービス)](../master-data-services/security-master-data-services.md)  
  
  
