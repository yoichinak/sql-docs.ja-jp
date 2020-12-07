---
description: MSSQLSERVER_856
title: MSSQLSERVER_856
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 856 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f94f6f4e8f8eebee48bbb0c2a6d0faefa4218c25
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418862"
---
# <a name="mssqlserver_856"></a>MSSQLSERVER_856
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|856|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|BAD_MEMORY_CLEAN_DATABASE_PAGE|
|メッセージ テキスト|SQL Server により、データベース '% ls'、ファイル ID: %u、ページ ID; %u、メモリ アドレス: 0x% I64x でハードウェアのメモリ破損が検出され、ページが正常に回復されました|
||

## <a name="explanation"></a>説明

このメッセージは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、バッファー プールの外部にあるキャッシュされたオブジェクトで不良メモリ ページが検出されたことを示します。 このメッセージは、メモリ エラーから回復する機能をサポートするシステムで表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、変更されていない破損したメモリ ページが破棄され、これらのエラー メッセージが修正され、このエラー メッセージがログに記録されます。 破損したメモリ ページが変更されている (ダーティ) 場合は、エラー 824 が発生します ([MSSQLSERVER_824](mssqlserver-824-database-engine-error.md))

## <a name="user-action"></a>ユーザー アクション

ハードウェアまたはシステム チェックを実行して、メモリまたは CPU の問題があるかどうかを確認する必要があります。 すべてのシステム ドライバー、オペレーティング システムの更新プログラム、およびハードウェアの更新プログラムが確実にシステムに適用されていることを確かめます。 メモリ関連のテストを含む、ハードウェアの製造元の診断を実行することを検討します。 このエラーが発生した場合は常に、このインスタンス内のすべてのデータベースに対して `DBCC CHECKDB` を実行することを検討してください。

## <a name="more-information"></a>詳細情報

新しいハードウェアが備わっており、Windows Server 2012 以降のバージョンを実行しているコンピューター上では、ハードウェアにより、オペレーティング システムとアプリケーションに対して、メモリ ページ (オペレーティング システム ページ) が不良または破損とマークされていることを通知できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのアプリケーションで、次の API セットを使用して、これらの不良メモリ ページ通知を登録することができます。

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンについては、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、これらの通知のサポートが追加されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ハードウェアでこの新機能がサポートされているかどうかが確認されます。 また、エラー ログに次のメッセージが表示されます。

> \<Datetime> サーバー マシンでメモリ エラーの回復がサポートされています。 メモリ破損から回復するために、SQL メモリ保護が有効になっています。

現在、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でこれらの通知を受信したときにアクションを実行できるのはバッファー プールのみです。 通知の受信時に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でバッファー プール全体を反復処理し、割り当てられた各バッファーのアドレスを検出する必要があります。 その後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で `QueryWorkingSetEX` API が使用され、データ ページの基になるメモリ ページのいずれかが不良とマークされているかどうかを確認します。 このメモリ ページに対応する `PSAPI_WORKING_SET_EX_BLOCK` 出力構造体のそのメンバーは、何らかの破損が報告された場合に 1 に設定され、不良と見なされるようになります。

そのバッファー プールまたはデータ ページが現在変更されていないか、そこで I/O が処理されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータ ページを破棄してコミットを解除することができます。 その後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって次のメッセージがログに記録されます。

> SQL Server により、データベース '% ls'、ファイル ID: %u、ページ ID; %u、メモリ アドレス: 0x% I64x でハードウェアの破損が検出され、ページが正常に回復されました。

クエリでデータ ページが再び必要になったときに、バッファー プールでディスクからデータ ページを読み取り、その内容をバッファー プールに戻すことができます。 ディスク上のバージョンのページが破損状態になるおそれもあります。 その場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、エラー824 などの追加のエラーがログに記録されることがあります。

不良ページがバッファー プールではなく、他のキャッシュされたオブジェクトまたは構造体によって使用されている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、次のメッセージがログに記録されます。

> 修正できないハードウェア メモリの破損が検出されました。 システムが不安定になるおそれがあります。 詳細については、Windows イベント ログを確認してください。

サーバーによってメモリ エラーが報告されている場合は、コンピューターのハードウェア ベンダーに問い合わせて、メモリ診断の実行、BIOS とファームウェアの更新、不良メモリ モジュールの交換など、適切なアクションを行う必要があります。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トレース フラグ 849 を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメモリ エラー通知用にオペレーティング システムに登録されないようにすることができます。 しかし、トレース フラグ 849 を有効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でオペレーティング システムから不良メモリ通知を受信できなくなることにご注意ください。 そのため、一般的な状況ではこのトレース フラグを使用しないことをお勧めします。

また、既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、サポートされているハードウェアでこれらの通知が受信されることにご注意ください。

これらのメモリ エラー通知用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を登録すると、レイジー ライター システム プロセスで一定のページ チェックが実行されないことにもご注意ください。 一定のページ チェックの詳細については、「[SQL Server でのメッセージ 832 (変更不可のページが変更されました) のトラブルシューティングの方法](https://support.microsoft.com/help/2015759)」を参照してください。
