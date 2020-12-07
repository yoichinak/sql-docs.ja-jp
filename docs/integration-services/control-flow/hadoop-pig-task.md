---
description: Hadoop Pig Task
title: Hadoop Pig Task | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8bb1c648647ea2341e899989f6199cbacd583b1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88393358"
---
# <a name="hadoop-pig-task"></a>Hadoop Pig Task

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Hadoop Pig Task は、Hadoop クラスターで Pig スクリプトを実行するために使用します。  
  
 Hadoop Pig Task を追加するには、デザイナーにドラッグ アンド ドロップします。 その後タスクをダブルクリックするか、右クリックして **[編集]** をクリックし、 **[Hadoop Pig タスク エディター]** ダイアログ ボックスを表示します。  
  
 ![Hadoop Pig タスク エディター](../../integration-services/control-flow/media/hadoop-pig-task.png "[Hadoop Pig Task Editor]")  
  
## <a name="options"></a>オプション  
 **[Hadoop Pig Task Editor]** (Hadoop Pig Task エディター) ダイアログ ボックスで、次のオプションを構成します。  
  
|フィールド|説明|  
|-----------|-----------------|  
|**Hadoop 接続**|既存の Hadoop 接続マネージャーを指定するか、新しい Hadoop 接続マネージャーを作成します。 この接続マネージャーは、WebHCat サービスがホストされる場所を示します。|  
|**[SourceType]**|クエリのソースの種類を指定します。 使用できる値は、 **ScriptFile** と **DirectInput**です。|  
|**InlineScript**|**[SourceType]** の値が **DirectInput**の場合は、Pig スクリプトを指定します。|  
|**[HadoopScriptFilePath]**|**[SourceType]** の値が **ScriptFile**の場合は、Hadoop 上のスクリプト ファイルのパスを指定します。|  
|**[TimeoutInMinutes]**|タイムアウト値を分単位で指定します。 タイムアウトが経過するまでに完了していない場合、Hadoop ジョブが停止します。 Hadoop ジョブを非同期的に実行するようにスケジュールを設定するには、0 を指定します。|  
  
## <a name="see-also"></a>関連項目  
 [Hadoop 接続マネージャー](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
