---
description: MSSQLSERVER_125
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a4f0e32c318134778544315240e0af229c9f8d1c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197052"
---
# <a name="mssqlserver_125"></a>MSSQLSERVER_125
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|125|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|Case 式は、%d レベルまでしか入れ子にできません。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Case 式に入れ子にできるのは 10 レベルまでです。  
  
## <a name="user-action"></a>ユーザーの操作  
Case ステートメントのレベルを 10 以下にします。  
  
## <a name="see-also"></a>参照  
[CASE &#40;Transact-SQL&#41;](~/t-sql/language-elements/case-transact-sql.md)  
  
