---
title: MSSQLSERVER エラー 823  | mssqlserver_823
description: Microsoft SQL Server エラー 823 (mssqlserver_823) の説明といくつかの一般的な解決策。これはシステムレベルの重大なエラー状態であり、データベースの整合性を損なう可能性があり、すぐに対処する必要があります。
ms.custom: ''
ms.date: 01/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ed748bdf748aa51813d11348859bc769525ed35
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197901"
---
# <a name="mssqlserver-error-823"></a>MSSQLSERVER エラー 823
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|823|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|B_HARDERR|  
|メッセージ テキスト|オペレーティング システムにより、ファイル '%ls' のオフセット %#016I64x で %S_MSG 中の SQL Server にエラー %ls が返されました。 SQL Server エラー ログとシステム イベント ログ内の別のメッセージで詳細情報が報告されることもあります。 このシステムレベルのエラー状態は深刻で、データベースの一貫性を損なう可能性があるので、すぐに解決する必要があります。 完全なデータベース整合性確認 (DBCC CHECKDB) を完了させてください。 このエラーには多くの要因があります。詳細については、SQL Server オンライン ブックを参照してください。|  
  
## <a name="explanation"></a>説明  
SQL Server では、Windows API (たとえば [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)、[WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile)、[ReadFileScatter](/windows/win32/api/fileapi/nf-fileapi-readfilescatter)、[WriteFileGather](/windows/win32/api/fileapi/nf-fileapi-writefilegather)) を使用してファイル I/O 操作を実行します。 これらの I/O 操作の実行後、SQL Server によって、これらの API 呼び出しに関連付けられたエラー条件が確認されます。 オペレーティング システム エラーが発生して API 呼び出しが失敗した場合、SQL Server によってエラー 823 が報告されます。

 823 エラー メッセージには次の情報が含まれています。
 - I/O 操作が実行された対象のデータベース ファイル
 - I/O 操作が試行されたファイル内の位置のオフセット。 これはファイルの先頭からの物理バイト オフセットです。 この数値を 8192 で割ると、エラーの影響を受けた論理ページ番号が得られます。
 - I/O 操作が読み取り要求か書き込み要求か
 - オペレーティング システム エラー コードと、かっこで囲まれたエラーの説明
 

**オペレーティング システム エラー:** 読み取りまたは書き込みの Windows API 呼び出しが失敗し、SQL Server で Windows API 呼び出しに関連するオペレーティング システム エラーが発生します。 次のメッセージは、823 エラーの例です。

```
Error: 823, Severity: 24, State: 2.
2010-03-06 22:41:19.55 spid58 The operating system returned error 1117 (The request could not be performed because of an I/O device error.) to SQL Server during a read at offset 0x0000002d460000 in file 'e:\program files\Microsoft SQL Server\mssql\data\mydb.MDF'. Additional messages in the SQL Server error log and system event log may provide more detail. This is a severe, system-level error condition that threatens database integrity and must be corrected immediately. It is recommended to complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```

エラー メッセージ内のファイルに関連付けられたデータベースでの DBCC CHECKDB ステートメントからエラーが表示される場合もあれば、表示されない場合もあります。 823 エラーが発生した場合は、DBCC CHECKDB ステートメントを実行できます。 DBCC CHECKDB ステートメントでエラーが報告されない場合は、システムの問題が断続的に発生するか、ディスクの問題が発生している可能性があります。

トレース フラグ 818 を使用すると、823 エラーの追加の診断情報が SQL Server のエラー ログ ファイルに書き込まれる場合があります。
詳細については、「[KB 826433: 報告されない I/O の問題を検出するために追加された SQL Server 診断](https://support.microsoft.com/help/826433/sql-server-diagnostics-added-to-detect-unreported-i-o-problems-due-to)」を参照してください。


## <a name="cause"></a>原因
823 エラー メッセージは、通常、基になるストレージ システムやハードウェア、または I/O 要求のパスにあるドライバーに問題があることを示しています。 ファイル システムに不整合がある場合、またはデータベース ファイルが破損している場合に、このエラーが発生することがあります。 ファイル読み取りの場合、SQL Server で 823 が返される前に、読み取り要求が既に 4 回再試行されています。 再試行操作が成功した場合、クエリは失敗しませんが、メッセージ [825](mssqlserver-825-database-engine-error.md) がエラー ログとイベント ログに書き込まれます。

## <a name="user-action"></a>ユーザーの操作  
 - この問題が発生している他のページ (同じデータベースまたは別のデータベース内) について、MSDB の [suspect_pages](../system-tables/suspect-pages-transact-sql.md) テーブルを確認します。
 - DBCC CHECKDB コマンドを使用して、(823 メッセージで報告されているものと) 同じボリュームにあるデータベースの整合性を確認します。 DBCC CHECKDB コマンドで不整合が見つかった場合は、「[DBCC CHECKB によって報告された、データベースの整合性エラーのトラブルシューティング方法](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check)」のガイダンスを使用してください。 
 - Windows イベント ログで、オペレーティング システム、記憶装置、デバイス ドライバーのいずれかから報告されたエラーまたはメッセージがないか確認します。 それらがこのエラーと何らかの関連がある場合は、まずそれらのエラーに対処します。 たとえば、823 メッセージとは別に、ディスク ソースによって報告された "ドライバーは \Device\Harddisk4\DR4 でコントローラー エラーを検出しました" のようなイベントがイベント ログ内に見つかることがあります。 その場合は、このファイルがこのデバイスに存在するかどうかを評価してから、最初にそれらのディスク エラーを修正する必要があります。
 - [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) ユーティリティを使用して、このような 823 エラーが通常の SQL Server I/O 要求の外部で再現されるかどうかを確認します。 SQLIOSim ユーティリティには SQL Server 2008 以降のバージョンが付属しているため、別個にダウンロードする必要はありません。 これは通常、`C:\Program Files\Microsoft SQL Server\MSSQLxx.MSSQLSERVER\MSSQL\Binn` フォルダーにあります。
 - ハードウェア ベンダーまたはデバイスの製造元と協力して確認します。
   - ハードウェア デバイスと構成が SQL Server の I/O 要件に準拠していること
   - I/O パス内のすべてのデバイスのデバイス ドライバーおよびその他のサポート ソフトウェア コンポーネントが最新であること
 - ハードウェア ベンダーまたはデバイスの製造元から診断ユーティリティが提供されている場合は、それらを使用して I/O システムの正常性を評価します。
 - 問題が発生した I/O 要求のパスに存在する[フィルター ドライバー](https://support.microsoft.com/help/2454053/use-of-system-filter-drivers-can-lead-to-sql-server-database-engine-pe)があるかどうかを評価します。
   - これらのフィルター ドライバーに更新プログラムがあるかどうかを確認します
   - これらのフィルター ドライバーを削除するか無効にして、823 エラーを発生させる問題が解決するかどうかを確認できます  
