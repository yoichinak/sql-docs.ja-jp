---
description: MSSQLSERVER_17130
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c60cada5e0f1172c927fdb4ef5ebd8c89e719a33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499553"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|17130|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|INIT_NOLOCKSPACE|  
|メッセージ テキスト|構成されたロック数に対するメモリが不足しています。 より小さいロックのハッシュ テーブルで開始しますが、パフォーマンスに影響する場合があります。 データベース管理者に連絡して、データベース エンジンのこのインスタンスに割り当てるメモリを増やすように構成してください。|  
  
## <a name="explanation"></a>説明  
ロック マネージャーのハッシュ テーブルの必要なサイズに対してメモリが不足しています。  より小さいハッシュ テーブルの割り当てが試行されます。  
  
## <a name="user-action"></a>ユーザーの操作  
サーバーのメモリ構成パラメーター (min/max server memory) を確認し、メモリ負荷を確認します。 SQL Server へのメモリの割り当てを増やします。  
  
