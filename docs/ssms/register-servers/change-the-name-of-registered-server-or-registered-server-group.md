---
description: 登録済みサーバーまたは登録済みサーバー グループの名前の変更
title: 登録済みサーバーまたはサーバー グループの名前の変更
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/02/2016
ms.openlocfilehash: c5c8566a40d3993c6e273de3e3b6137d35e969c1
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250982"
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>登録済みサーバーまたは登録済みサーバー グループの名前の変更

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

このトピックでは、 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、登録済みサーバーまたは登録済みサーバー グループの名前を変更する方法について説明します。 この名前はいつでも変更できます。 [登録済みサーバー] でサーバーの名前を変更すると、名前の表示のみが変更されます。 別のサーバーに接続するには、登録済みサーバーの接続プロパティを編集する必要があります。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用

メニューから **[表示]\\[登録済みサーバー]** を選択し、**[登録済みサーバー]** ペインを開きます。

### <a name="to-change-the-name-of-a-server"></a>サーバーの名前を変更するには

1. **[登録済みサーバー]** の **[データベース エンジン]** 、 **[ローカル サーバー グループ]** の順に展開します。  

2. サーバーを右クリックして **[プロパティ]** を選択し、 **[サーバー登録プロパティの編集]** ダイアログ ボックスを開きます。

3. **[登録済みサーバーの名前]** テキスト ボックスにサーバーの新しい登録名を入力し、 **[保存]** をクリックします。  

### <a name="to-change-the-name-of-a-server-group"></a>サーバー グループの名前を変更するには  

1. **[登録済みサーバー]** の **[データベース エンジン]** 、 **[ローカル サーバー グループ]** の順に展開します。  

2. サーバー グループを右クリックし、 **[プロパティ]** を選択して **[サーバー グループ プロパティの編集]** ダイアログ ボックスを開きます。 

3. **[グループ名]** テキスト ボックスにサーバー グループの新しい名前を入力し、 **[保存]** をクリックします。  

## <a name="see-also"></a>参照

[サーバーの登録の変更 &#40;SQL Server Management Studio&#41;](./change-a-server-s-registration-sql-server-management-studio.md)