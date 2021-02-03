---
description: MSSQLSERVER_611
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7a9776bca7b50043f4e61034476e140f68e804fa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211382"
---
# <a name="mssqlserver_611"></a>MSSQLSERVER_611
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|611|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|VAR_SIZE_TOO_BIG|  
|メッセージ テキスト|行を挿入または更新できません。オーバーヘッドを含む、変数列の合計サイズが、制限を超える %d バイトです。|  
  
## <a name="explanation"></a>説明  
最大の可変長の列サイズがスキーマで許可されている値を超えています。 vardecimal ストレージ形式を設定したときに可変長の列が固定値の制限を超えているか、可変長の列サイズが圧縮データ レコードの [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] で許可されている制限を超えていた場合に、エラー 611 が返されます。  
  
## <a name="user-action"></a>ユーザーの操作  
レコードのサイズを縮小します。  
  
