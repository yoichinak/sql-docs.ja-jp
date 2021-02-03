---
description: MSSQLSERVER_21862
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9e722121773db00eb1411b42a0206d83a22484c4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196394"
---
# <a name="mssqlserver_21862"></a>MSSQLSERVER_21862
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|MSSQLSERVER|  
|イベント ID|21862|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21862|  
|メッセージ テキスト|FILESTREAM 列は、同期方法 'database snapshot' または 'database snapshot character' を使用して、パブリケーションでパブリッシュすることはできません。|  
  
## <a name="explanation"></a>説明  
データベース スナップショットから FILESTREAM データにアクセスできないため、パブリケーションの同期方法に *database snapshot* パラメーターまたは *database_snapshot_character* パラメーターが指定されている場合、スナップショット エージェントは FILESTREAM データを読み取ることができません。  
  
## <a name="user-action"></a>ユーザーの操作  
パブリケーションの同期方法を *database snapshot* または *database_snapshot_character* 以外の方法に変更するか、パブリケーションから FILESTREAM 列を除外します。  
  
