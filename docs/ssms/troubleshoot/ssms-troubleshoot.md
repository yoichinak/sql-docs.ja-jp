---
description: SQL Server Management Studio (SSMS) がクラッシュした後に診断データを取得する
title: SSMS でのシステムの応答停止またはクラッシュのトラブルシューティング
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.reviewer: drskwier, sstein
ms.custom: seo-lt-2019
ms.date: 09/18/2019
ms.openlocfilehash: 97200a4dfdaebeb77703fe420267557a3d5ad9d7
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035908"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>SQL Server Management Studio (SSMS) がクラッシュした後に診断データを取得する

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

## <a name="get-full-memory-dump-after-an-unresponsive-system-or-crash"></a>システムの応答停止またはクラッシュが発生した後に完全メモリ ダンプを取得する

SQL Server Management Studio (SSMS) が応答停止またはクラッシュした場合に、その完全メモリ ダンプを取得します。

診断情報を取得して SSMS のクラッシュまたは応答停止のトラブルシューティングを行うには、以下の手順を行います。

1. [ProcDump](/sysinternals/downloads/procdump) をダウンロードします。

2. ダウンロードしたものをフォルダーに解凍します。

3. コマンド プロンプトを開き、次のコマンドを実行します。

    ```console
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    使用許諾契約書に同意するように求められた場合は、 *[同意する]* を選択します。

4. SSMS をまだ起動していない場合は起動します。

5. 問題を再現します。

6. ダンプ ファイルの書き込みに関する cmd プロンプトにテキストが表示されるはずです。書き込みが完了するまで待ちます。

7. 新しいフォルダーを作成し、そのフォルダーに書き込む *.dmp ファイルをコピーします。

8. 次のファイルを同じフォルダーにコピーします。

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. フォルダーを圧縮する

## <a name="get-full-memory-dump-for-an-outofmemoryexception"></a>OutOfMemoryException の完全メモリ ダンプを取得する

OutOfMemoryException がスローされるとき、SSMS の完全メモリ ダンプを取得する

あらゆる管理対象の例外について、完全メモリ ダンプを取得できます。

SSMS から OutOfMemoryException の問題を解決するための診断情報を取得するには、以下の手順を行います。

1. [ProcDump](/sysinternals/downloads/procdump) をダウンロードします。

2. ダウンロードしたものをフォルダーに解凍します。

3. コマンド プロンプトを開き、次のコマンドを実行します。

    ```console
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    使用許諾契約書に同意するように求められた場合は、 *[同意する]* を選択します。

4. SQL Server Management Studio をまだ起動していない場合は起動します。

5. 問題を再現します。

6. ダンプ ファイルの書き込みに関する cmd プロンプトにテキストが表示されるはずです。書き込みが完了するまで待ちます。

7. 新しいフォルダーを作成し、そのフォルダーに書き込む *.dmp ファイルをコピーします。

8. 次のファイルを同じフォルダーにコピーします。

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. フォルダーを圧縮します。