---
title: sqlagent90 アプリケーション
description: sqlagent90 アプリケーションは、コマンド プロンプトから SQL Server エージェントを起動します。 SQL Server エージェントを診断する場合、またはサポート プロバイダーから指示された場合にそれを使用してください。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1930add6748d979c0a00455529ca932e8d0b43c8
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714080"
---
# <a name="sqlagent90-application"></a>sqlagent90 アプリケーション
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  **sqlagent90** アプリケーションは、コマンド プロンプトから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントを起動します。 通常、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントは [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] から実行するか、またはアプリケーションで SQL-SMO メソッドを使って実行します。 ただし、 **エージェントを診断する場合や、プライマリ サポート プロバイダーから指示された場合は、コマンド プロンプトから** sqlagent90 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を実行してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlagent90  
-c [-v] [-i instance_name]  
```  
  
## <a name="arguments"></a>引数  
 **-c**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントをコマンド プロンプトから実行し、Microsoft Windows サービス コントロール マネージャーの制御下にないことを指定します。 **-c** を使用する場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントを、管理ツールのサービス アプリケーションまたは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーから制御することはできません。 この引数は必須です。  
  
 **-v**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントを冗長モードで実行し、診断情報をコマンド プロンプト ウィンドウに書き込みます。 診断情報は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントのエラー ログに書き込まれる情報と同じです。  
  
 **-i** *instance_name*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance_name *によって指定された名前付き*インスタンスに接続します。  
  
## <a name="remarks"></a>解説  
 **sqlagent90** は、 **-v** スイッチが指定された場合にのみ、著作権に関するメッセージを表示した後にコマンド プロンプト ウィンドウに出力を表示します。 **sqlagent90**を停止するには、コマンド プロンプトで Ctrl キーを押しながら C キーを押します。 **sqlagent90**を停止する前に、コマンド プロンプト ウィンドウを閉じないでください。  
  
## <a name="see-also"></a>参照  
 [管理タスクの自動化 &#40;SQL Server エージェント&#41;](../ssms/agent/automated-administration-tasks-sql-server-agent.md?view=sql-server-ver15)  
  
