---
description: MSSQLSERVER_10534
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f53c5a8ce3a2965cda3f9fa1028189e2fbc8c266
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197395"
---
# <a name="mssqlserver_10534"></a>MSSQLSERVER_10534
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|10534|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_INVALID_PARAMS|  
|メッセージ テキスト|プラン ガイド '%.\*ls' を作成できません。 **\@params** に指定された値が無効です。 *parameter_name parameter_type* 形式の値を指定するか、NULL を指定してください。|  
  
## <a name="explanation"></a>説明  
**\@params** に指定した値が無効です。  
  
## <a name="user-action"></a>ユーザーの操作  
*parameter_name parameter_type* 形式の値を指定するか、NULL を指定してください。  
  
## <a name="see-also"></a>参照  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
