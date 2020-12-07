---
description: MSSQLSERVER_854
title: MSSQLSERVER_854
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 854 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f0bf9061b452329280f0625bcc1339469372f4df
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418872"
---
# <a name="mssqlserver_854"></a>MSSQLSERVER_854
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|854|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|HARDWARE_MEMORY_SCRUBBER|
|メッセージ テキスト|マシンでメモリ エラーの回復がサポートされています。 メモリ破損から回復するために、SQL メモリ保護が有効になっています|
||

## <a name="explanation"></a>説明

このメッセージは、オペレーティング システムのハードウェアによって、メモリ エラーから回復する機能がサポートされていることを示します。 新しいハードウェアが備わっており、Windows Server 2012 以降のバージョンを実行しているコンピューター上では、ハードウェアにより、オペレーティング システムとアプリケーションに対して、メモリ ページ (オペレーティング システム ページ) が不良または破損とマークされていることを通知できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのアプリケーションで、次の API セットを使用して、これらの不良メモリ ページ通知を登録することができます。

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 以降のバージョンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、これらの通知のサポートが追加されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ハードウェアでこの新機能がサポートされているかどうかが確認されます。 また、エラー ログに次のメッセージが表示されます。

> \<Datetime> サーバー マシンでメモリ エラーの回復がサポートされています。 メモリ破損から回復するために、SQL メモリ保護が有効になっています。

## <a name="user-action"></a>ユーザー アクション

855 や 856 などの他のエラーが発生しているかどうかを確認し、適切な修正措置を行います。

## <a name="more-information"></a>詳細情報

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トレース フラグ 849 を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメモリ エラー通知用にオペレーティング システムに登録されないようにすることができます。 しかし、トレース フラグ 849 を有効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でオペレーティング システムから不良メモリ通知を受信できなくなることにご注意ください。 そのため、一般的な状況ではこのトレース フラグを使用しないことをお勧めします。
