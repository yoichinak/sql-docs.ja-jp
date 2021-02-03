---
description: MSSQLSERVER_10520
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0f2187ccd80b90c0375ae960bd4e27806640e74b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197445"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|10520|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_PARAM_NOT_ALLOWED|  
|メッセージ テキスト|プラン ガイド '%.*ls' を作成できません。'%ls' として指定した @type のパラメーター '%ls' に NULL 以外の値を指定しています。 この型のパラメーターには、NULL 値を指定する必要があります。 パラメーターに NULL を指定するか、パラメーターに NULL 以外の値を指定可能な型に変更します。|  
  
## <a name="explanation"></a>説明  
@type で指定した型のパラメーターには、NULL 値を指定する必要がありますが、NULL 以外の値を指定しました。  
  
## <a name="user-action"></a>ユーザーの操作  
パラメーターに NULL を指定するか、パラメーターに NULL 以外の値を指定可能な型に変更します。  
  
## <a name="see-also"></a>参照  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
  
