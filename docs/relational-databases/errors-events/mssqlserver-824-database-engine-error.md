---
description: MSSQLSERVER_824
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0e2242b539f5fadb18beb54115e2cbad95336497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499527"
---
# <a name="mssqlserver_824"></a>MSSQLSERVER_824
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|824|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|B_HARDSSERR|  
|メッセージ テキスト|SQL Server で、一貫性に基づいた論理 I/O エラーが検出されました: %ls。 このエラーは、ファイル '%ls' のオフセット %#016I64x にあるデータベース ID が %d のページ %S_PGID の %S_MSG 中に発生しました。  SQL Server エラー ログまたはシステム イベント ログ内の別のメッセージで詳細情報が報告されることもあります。|  
  
## <a name="symptom"></a>症状  


データベース ページの読み取りまたは書き込みを行った後で論理的な整合性チェックが失敗した場合は、SQL Server エラー ログまたは Windows アプリケーション イベント ログに次のエラー メッセージが表示されることがあります。
 
``` 
2009-11-02 15:46:42.90 spid51      Error: 824, Severity: 24, State: 2.
2009-11-02 15:46:42.90 spid51      SQL Server detected a logical consistency-based I/O error: incorrect pageid (expected 1:43686; actual 0:0). It occurred during a read of page (1:43686) in database ID 23 at offset 0x0000001554c000 in file 'H:\MSSQL.SQL2008\MSSQL\DATA\my_db.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```
 
データのクエリまたは変更中にアプリケーションでこのメッセージが表示された場合は、エラー メッセージがアプリケーションに返され、データベース接続が終了します。 
  
## <a name="cause"></a>原因
このエラーは、ディスクからページが正常に読み取られたことが Windows によって報告されたが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってそのページに異常が検出されたことを示しています。 このエラーは、Windows によってエラーが検出されなかった点を除けば、エラー 823 と似ています。通常は、ディスク ドライブの欠陥、ディスク ファームウェアの問題、デバイス ドライバーの障害など、I/O サブシステムでの問題を示しています。 I/O エラーの詳細については、「[Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))」 (Microsoft SQL Server I/O の基礎 (第 2 章)) を参照してください。  

SQL Server では Windows API (たとえば、ReadFile、WriteFile、ReadFileScatter、WriteFileGather) を使用して、I/O 操作を実行します。 これらの I/O 操作の実行後、SQL Server によって、これらの API 呼び出しに関連付けられたエラー条件が確認されます。 オペレーティング システム エラーが発生して、これらの API 呼び出しが失敗した場合、SQL Server によってエラー 823 が報告されます。 Windows API 呼び出しが実際には成功していても、I/O 操作によって転送されたデータで論理的な整合性の問題が発生している場合があります。 これらの論理的な整合性の問題は、エラー 824 で報告されます。
 
824 エラーには、次の情報が含まれています。

- I/O 操作が実行されるデータベース ファイル
- I/O 操作が試行されたファイルでのオフセット
- このファイルが属しているデータベース
- I/O 操作に関係したページ番号
- 操作が読み取りまたは書き込み操作だった
- 失敗した論理的な整合性チェックの詳細 (チェックの種類、実際の値、およびこのチェックに使用された予測値)
 
これらの論理的な整合性チェックは、データ転送に関係したデータの特定の重要な側面が I/O 操作全体で維持されていたことを確認するために、SQL Server によって実行される追加の整合性チェックです。 チェックには、チェックサム、正しくないページ、短い転送、不適切なページ ID、古い読み取り、ページ監査エラーが含まれます。 実行されるチェックの性質は、データベースおよびサーバー レベルのさまざまな構成オプションによって異なります。 
 
824 エラー メッセージは、通常、基になるストレージ システムやハードウェア、または I/O 要求のパスにあるドライバーに問題があることを示しています。 ファイル システムに不整合がある場合、またはデータベース ファイルが破損している場合に、このエラーが発生することがあります。

## <a name="resolution"></a>解決方法  

エラー 824 が発生した場合は、次の解決策を試すことができます。 

- msdb の [suspect_pages](../backup-restore/manage-the-suspect-pages-table-sql-server.md) テーブルを調べ、(同じデータベースまたは別のデータベース内の) 他のページでこの問題が発生しているかどうかを確認します。
- DBCC CHECKDB コマンドを使用して、(824 メッセージで報告されているものと) 同じボリュームにあるデータベースの整合性を確認します。 DBCC CHECKDB コマンドで不整合が見つかった場合は、サポート技術情報の記事の「[DBCC CHECKB によって報告された、データベースの整合性エラーのトラブルシューティング方法](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check)」のガイダンスを使用してください。
- これらの 824 エラーが発生したデータベースで、PAGE_VERIFY CHECKSUM データベース オプションがオンになっていない場合は、すぐにそのようにします。 824 エラーはチェックサム エラー以外の理由で発生することがありますが、CHECKSUM では、ディスクに書き込まれた後のページの整合性を確認するための最適なオプションが提供されます。
- Windows イベント ログで、オペレーティング システム、記憶装置、デバイス ドライバーのいずれかから報告されたエラーまたはメッセージがないか確認します。 それらがこのエラーと何らかの関連がある場合は、まず、それらのエラーに対処してください。 たとえば、824 メッセージとは別に、ディスク ソースによって報告された "ドライバーは \Device\Harddisk4\DR4 でコントローラー エラーを検出しました" のようなイベントがイベント ログ内で見つかることもあります。 その場合は、このファイルがこのデバイスに存在するかどうかを評価してから、最初にそれらのディスク エラーを修正する必要があります。
- [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) ユーティリティを使用して、このような 824 エラーが通常の SQL Server I/O 要求の外部で再現されるかどうかを確認します。 SQLIOSim には SQL Server 2008 が付属しているため、このバージョン以降で別個にダウンロードする必要はありません。
- ハードウェア ベンダーまたはデバイス製造元と協力して、次のことを確認します。
   - ハードウェア デバイスと構成が [SQL Server の I/O 要件](https://support.microsoft.com/help/967576/microsoft-sql-server-database-engine-input-output-requirements)に準拠している。
   - I/O パス内のすべてのデバイスのデバイス ドライバーおよびその他のサポート ソフトウェア コンポーネントが更新されている。
- ハードウェア ベンダーまたはデバイス製造元から診断ユーティリティが提供されている場合は、それらを使用して I/O システムの正常性を評価します。
- 問題が発生したこれらの I/O 要求のパスに存在するフィルター ドライバーがあるかどうかを評価します。
   - これらのフィルター ドライバーに更新プログラムがあるかどうかを確認します
   - これらのフィルター ドライバーを削除するか無効にして、824 エラーを発生させる問題が解決するかどうかを確認できます
- 問題がハードウェアに関するものではなく、また既知のクリーン バックアップがある場合は、そのバックアップを使用してデータベースを復元します。  

## <a name="see-also"></a>参照  
[suspect_pages テーブルの管理 &#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
