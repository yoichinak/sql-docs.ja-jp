---
title: SqlTriggerContext オブジェクト |Microsoft Docs
description: SQL Server CLR 統合では、SqlTriggerContext クラスによって、アクションの種類や操作中に変更された列などのトリガーのコンテキスト情報が提供されます。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
ms.openlocfilehash: c6f11eda2ef791eb8c987af8d82149507770d47a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809163"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext オブジェクト
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **Sqltriggercontext**クラスは、トリガーに関するコンテキスト情報を提供します。 このコンテキスト情報には、トリガーを起動する原因となったアクションの種類、更新操作で変更された列、データ定義言語 (DDL) トリガーの場合は、トリガー操作を記述する XML **EventData** 構造が含まれます。 **Sqltriggercontext**クラスの使用方法の詳細と例については、「 [CLR Triggers](/dotnet/framework/data/adonet/sql/clr-triggers)」を参照してください。  
  
 詳細については、.NET Framework SDK ドキュメントの「 **Microsoft Sql server のコンテキスト** クラスのリファレンスドキュメント」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CLR トリガー](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
