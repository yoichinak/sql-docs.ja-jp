---
description: MSSQLSERVER_41301
title: MSSQLSERVER_41301 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c47d56a61bd2c33955109677249d3532e3022865
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88410808"
---
# <a name="mssqlserver_41301"></a>MSSQLSERVER_41301
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41301|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|COMMIT_DEPENDENCY_FAILURE|  
|メッセージ テキスト|現在のトランザクションが依存している前のトランザクションが中止されたため、現在のトランザクションはコミットできません。|  
  
## <a name="explanation"></a>説明  
依存エラーが発生したため、トランザクションに失敗しました。  
  
このエラーは、従属トランザクションが多すぎるために発生することもあります。 どの書き込みトランザクションでも、従属トランザクションの数には制限があります。 たとえば、このエラーは、ある更新トランザクションに依存関係を適用しようと試みる読み取りトランザクションの数が多すぎる場合に発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
そのトランザクションは操作しないでください。 ROLLBACK TRAN を呼び出し、トランザクションをロールバックします。 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
