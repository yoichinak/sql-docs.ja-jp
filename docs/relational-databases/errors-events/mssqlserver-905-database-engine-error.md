---
description: MSSQLSERVER_905
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 01b230fedd998bc3affc3826163a3c51dcede123
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88410609"
---
# <a name="mssqlserver_905"></a>MSSQLSERVER_905
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|905|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBSTARTUP_EE_PARTITIONING|  
|メッセージ テキスト|データベース '%.*ls' は、このエディションの SQL Server では起動できません。このデータベースには、パーティション関数 '%.\*ls' が含まれています。 パーティション分割は SQL Server Enterprise Edition でしかサポートされません。|  
  
## <a name="explanation"></a>説明  
データベースに 1 つ以上のパーティション テーブルまたはパーティション インデックスが含まれています。 このエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではパーティション分割を使用できません。 したがって、データベースを正常に起動できません。 パーティション テーブルとパーティション インデックスは、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
sp_detach_db ストアド プロシージャを使用してデータベースをデタッチします。 必要であればファイルを移動してから、CREATE DATABASE で FOR ATTACH オプションまたは FOR ATTACH_REBUILD_LOG オプションを使用し、サポートされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エディションのインスタンスにデータベースをアタッチします。 すべてのテーブルのパーティションを無効にし、パーティション関数を削除します。 もう一度、データベースをデタッチしてから、現在のサーバーにデータベースを再アタッチします。  
  
