---
title: MSSQLSERVER_233 | Microsoft Docs
description: SQL Server クライアントがサーバーに接続できません。 エラー 233 の説明と、考えられる解決策をご確認ください。
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bf1a3e2f94c221caa4b70105aaccc331c6082b97
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521073"
---
# <a name="mssqlserver_233"></a>MSSQLSERVER_233
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|233|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|サーバーとの接続は正常に確立されましたが、ログイン プロセスでエラーが発生しました。 (プロバイダー:共有メモリ プロバイダー、エラー:0 - パイプの他端にプロセスがありません。) (Microsoft SQL Server、エラー:233)|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントがサーバーに接続できません。 このエラーは、サーバーがリモート接続を許可するように構成されていないことが原因で発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー ツールを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリモート接続を許可できるようにします。  
  
## <a name="see-also"></a>参照  
[ネットワーク プロトコルとネットワーク ライブラリ](~/sql-server/install/network-protocols-and-network-libraries.md)  
[クライアント ネットワーク構成](~/database-engine/configure-windows/client-network-configuration.md)  
[クライアント プロトコルの構成](~/database-engine/configure-windows/configure-client-protocols.md)  
[サーバー ネットワーク プロトコルの有効化または無効化](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
