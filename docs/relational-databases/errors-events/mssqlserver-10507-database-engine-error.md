---
description: MSSQLSERVER_10507
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 804a09bd518b5dd15d9abbd1944cf4cbb1aa00d6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197483"
---
# <a name="mssqlserver_10507"></a>MSSQLSERVER_10507
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|10507|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_STMT_DOES_NOT_MATCH|  
|メッセージ テキスト|プラン ガイド '%.\*ls を作成できません。 **\@stmt** と **\@module_or_batch** または **\@plan_handle** と **\@statement_start_offset** で指定されたステートメントが、指定されたモジュールまたはバッチのどのステートメントとも一致しません。 モジュールまたはバッチのステートメントと一致するように値を変更してください。|  
  
## <a name="explanation"></a>説明  
指定したモジュールまたはバッチのステートメントが、指定したステートメントまたはステートメントのオフセット値と一致しませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
モジュールまたはバッチのステートメントと一致するように指定のパラメーター値を変更します。  
  
## <a name="see-also"></a>参照  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
