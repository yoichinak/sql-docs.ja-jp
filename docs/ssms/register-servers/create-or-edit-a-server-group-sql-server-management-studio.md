---
description: サーバー グループの作成または編集 (SQL Server Management Studio)
title: サーバー グループの作成または編集
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.editgroup.f1
- sql13.swb.newgroup.f1
helpviewer_keywords:
- Registered Servers [SQL Server], server groups
- server groups [SQL Server]
- groups [SQL Server], server
ms.assetid: d4a942bd-2dd1-42db-ad0e-e9a9ae5b856d
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 00caef8ecdd73814d60ce2c98c65ba0fc4083379
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037605"
---
# <a name="create-or-edit-a-server-group-sql-server-management-studio"></a>サーバー グループの作成または編集 (SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

このトピックでは、サーバー グループを作成し、サーバーをそのサーバー グループに配置して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で、登録済みサーバー内のサーバーを整理する方法について説明します。 登録済みサーバーにはサーバー グループをいつでも作成できます。また、サーバーの登録時にサーバー グループを作成することもできます。  

## <a name="SSMSProcedure"></a>

### <a name="to-create-a-server-group-in-registered-servers"></a>登録済みサーバーにサーバー グループを作成するには  

1. [登録済みサーバー] で、[登録済みサーバー] ツール バーのサーバーの種類をクリックします。 [登録済みサーバー] が表示されていない場合は、 **[表示]** メニューの **[登録済みサーバー]** をクリックします。  

2. サーバーまたはサーバー グループを右クリックし、 **[新規作成]** をポイントし、 **[サーバー グループ]** をクリックします。  

3. **[新しいサーバー グループ]** ダイアログ ボックスの **[グループ名]** ボックスに、一意のサーバー グループ名を入力します。 このサーバー グループ名は、登録済みサーバーのツリーの現在の場所に対して一意である必要があります。

4. 必要に応じて、 **[グループの説明]** ボックスに、サーバー グループを説明する表示名 (「ラテン アメリカ地区の財務サーバー」など) を入力します。  

5. **[新しいサーバー グループの場所を選択する]** ボックスで、グループの場所をクリックし、 **[保存]** をクリックします。  

   > [!NOTE]
   >  また、サーバーの登録時でも、 **[新しいグループ]** をクリックし、 **[新しいサーバー グループ]** ダイアログ ボックスでの操作を完了すれば、新しいサーバー グループを作成できます。  

## <a name="see-also"></a>関連項目

[サーバーの登録](./register-servers.md)