---
description: MSSQLSERVER_8525
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eb5b5812aac0cf4e6a15d45806b84c68294398dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482706"
---
# <a name="mssqlserver_8525"></a>MSSQLSERVER_8525
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|8525|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|分散トランザクションが完了しました。 このセッションを新規トランザクションまたは NULL トランザクションのいずれかに参加させます。|  
  
## <a name="explanation"></a>説明  
分散トランザクション コーディネーターを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用するプログラミング モデルでは、分散トランザクションに対してアプリケーションを明示的に参加させたり参加を解除したりする必要があります。  
  
このエラーは、次の 4 つの条件が揃った場合に発生します。  
  
-   アプリケーションが分散トランザクションに参加している。  
  
-   トランザクションが、何かの理由でコミットまたはロールバックされた状態で終了した。  
  
-   ユーザー アプリケーションが、分散トランザクションへの参加を明示的に解除されていないか、新しい分散トランザクションに明示的に参加していない。  
  
-   既存の分散トランザクションへの参加の解除でも新しい分散トランザクションへの参加でもないトランザクション操作、たとえば、クエリの実行やローカル トランザクションの開始を、アプリケーションで試行している。  
  
ローカル トランザクションを作成する操作をアプリケーションで実行している場合はエラー状態 1 が使用され、バインドされたセッションへの参加をアプリケーションで試みている場合はエラー状態 2 が使用されます。  
  
## <a name="user-action"></a>ユーザーの操作  
アプリケーションは、分散トランザクションに参加した後、その分散トランザクションへの参加を明示的に解除するか、別の分散トランザクションに参加する必要があります。 これにより、前のトランザクションへの参加が暗黙的に解除されます。 分散トランザクションへの参加やその解除を行うための正確な構文については、アプリケーションのプログラミング インターフェイス マニュアルを参照してください。  
  
