---
description: '[サブスクリプションの再初期化] - 1 つのサブスクリプション'
title: '[サブスクリプションの再初期化] - 1 つのサブスクリプション | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 84aeb92a82869376385f716c224b0cd0d02cf6b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88405548"
---
# <a name="reinitialize-subscriptions---one-subscription"></a>[サブスクリプションの再初期化] - 1 つのサブスクリプション
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **[サブスクリプションの再初期化]** ダイアログ ボックスを使用すると、サブスクリプションに再初期化を設定できます。 再初期化には、サブスクライバーへのスナップショットの適用が含まれています。トランザクション パブリケーションに対するサブスクリプションの場合はディストリビューション エージェントによって実行され、マージ パブリケーションに対するサブスクリプションの場合はマージ エージェントによって実行されます。  
  
## <a name="options"></a>オプション  
 **[現在のスナップショットを使用する]**  
 このオプションを選択すると、次にディストリビューション エージェントまたはマージ エージェントが実行されたときに、現在のスナップショットがサブスクライバーに適用されます。 有効なスナップショットが使用できない場合、このオプションは選択できません。  
  
 **[新しいスナップショットを使用する]**  
 このオプションを選択すると、新しいスナップショットによってサブスクリプションが再初期化されます。 スナップショットは、スナップショット エージェントによって生成された後にだけ、サブスクライバーに適用できます。 スナップショット エージェントの実行がスケジュールに設定されている場合、次にスケジュールされたスナップショット エージェントの実行が終了するまで、サブスクリプションは再初期化されません。  
  
 スナップショット エージェントをすぐに開始するには、 **[今すぐ新しいスナップショットを生成する]** を選択します。  
  
 **[再初期化する前に、同期されていない変更をアップロード]**  
 マージ レプリケーションのみです。 このオプションを選択すると、サブスクライバーのデータがスナップショットで上書きされる前に、保留中の変更がサブスクリプション データベースからアップロードされます。  
  
 パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
 **[再初期化するように設定]**  
 クリックすると、サブスクリプションに再初期化が設定されます。 有効なスナップショットが使用できるようになった後、サブスクリプションに対してディストリビューション エージェントまたはマージ エージェントを次回実行するとき、スナップショットはサブスクライバーに適用されます。  
  
## <a name="see-also"></a>関連項目  
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
