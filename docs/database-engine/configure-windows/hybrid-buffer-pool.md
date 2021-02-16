---
title: ハイブリッド バッファー プール | Microsoft Docs
description: ハイブリッド バッファー プールによりメモリ バスを介して永続メモリ デバイスにアクセスできるようにする方法について確認します。 この SQL Server 2019 機能を有効または無効にして、ベスト プラクティスを確認します。
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: 70754d80b8faba251683c1cec1db808e91d8d6e1
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100350369"
---
# <a name="hybrid-buffer-pool"></a>ハイブリッド バッファー プール
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

ハイブリッド バッファー プールを使用すると、バッファー プール オブジェクトで、揮発性 DRAM にキャッシュされたデータのコピーではなく、永続メモリ (PMEM) 上にあるデータベース ファイル内のデータ ページを参照できます。 この機能は [!INCLUDE[sqlv15](../../includes/sssql19-md.md)] で導入されています。

![ハイブリッド バッファー プール](./media/hybrid-buffer-pool.png)

永続メモリ (PMEM) デバイスはバイトアドレス指定可能で、直接アクセス (DAX) の永続メモリ対応ファイル システム (XFS、EXT4、NTFS など) を使用する場合、OS の通常のファイル システム API を使用してファイル システム上のファイルにアクセスできます。 または、デバイス上のファイルのメモリ マップに対するロード操作およびストア操作と呼ばれる操作を実行できます。 これにより、SQL Server などの PMEM 対応アプリケーションは、従来の記憶域スタックを経由せずにデバイス上のファイルにアクセスできます。

ハイブリッド バッファー プールは、この機能を使用して、マップ済みファイルに対するロード操作およびストア操作を実行し、PMEM デバイスをバッファー プールのキャッシュとして利用するだけでなく、データベース ファイルの格納にも利用します。 これにより、論理的な読み込みと物理的な読み込みの両方が基本的には同じ操作であるという特殊な状況が生じます。 永続メモリ デバイスは、通常の揮発性 DRAM と同様、メモリ バスを介してアクセスできます。

クリーンなデータ ページのみがハイブリッド バッファー プールのデバイス上にキャッシュされます。 ページがダーティとしてマークされている場合、そのページは DRAM バッファー プールにコピーされてから、最終的に PMEM デバイスに書き戻されて再びクリーンとしてマークされます。 これは、通常のチェックポイント操作中に、標準のブロック デバイスに対して実行される場合と同様の方法で発生します。

ハイブリッド バッファー プール機能は、Windows と Linux の両方で使用できます。 PMEM デバイスは、DAX (DirectAccess) をサポートするファイル システムでフォーマットする必要があります。 DAX は、XFS、EXT4、NTFS のすべてのファイル システムでサポートされます。 SQL Server は、適切にフォーマットされた PMEM デバイス上にデータ ファイルが存在するかどうかを自動的に検出し、新しいデータベースがアタッチ、復元、または作成されると、起動時にデータベース ファイルのメモリ マッピングを実行します。

詳細については、次を参照してください。

* [永続メモリの理解と配置 (Windows)](/windows-server/storage/storage-spaces/deploy-pmem/)
* [SQL Server on Linux 用に永続メモリ (PMEM) を構成する](../../linux/sql-server-linux-configure-pmem.md)


## <a name="enable-hybrid-buffer-pool"></a>ハイブリッド バッファー プールを有効にする

[!INCLUDE[sqlv15](../../includes/sssql19-md.md)] では、ハイブリッド バッファー プールを管理するための動的データ言語 (DDL) が導入されています。

次の例では、SQL Server のインスタンス用にハイブリッド バッファー プールを有効にします。

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

既定では、ハイブリッド バッファー プールはインスタンスのスコープで無効にされます。 設定の変更を有効にするためには、SQL Server インスタンスを再起動する必要があることに注意してください。 サーバー上の合計 PMEM 容量を考慮するために十分なハッシュ ページの割り当てを容易にするためには、再起動が必要です。

次の例では、特定のデータベース用にハイブリッド バッファー プールを有効にします。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

既定では、ハイブリッド バッファー プールはデータベースのスコープで有効にされます。

## <a name="disable-hybrid-buffer-pool"></a>ハイブリッド バッファー プールを無効にする

次の例では、ハイブリッド バッファー プールをインスタンス レベルで無効にします。

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

既定では、ハイブリッド バッファー プールはインスタンス レベルで無効にされます。 この変更を有効にするには、インスタンスを再起動する必要があります。 これにより、サーバー上の PMEM の容量を考慮する必要があるため、バッファー プールに十分なハッシュ ページが割り当てられます。

次の例では、特定のデータベース用にハイブリッド バッファー プールを無効にします。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

既定では、ハイブリッド バッファー プールはデータベースのスコープで有効にされます。

## <a name="view-hybrid-buffer-pool-configuration"></a>ハイブリッド バッファー プールの構成を表示する

次の例では、インスタンスの現在のハイブリッド バッファー プール構成の状態を戻します。

```sql
SELECT * FROM
sys.server_memory_optimized_hybrid_buffer_pool_configuration;
```

次の例では、データベースと、ハイブリッド バッファー プールのデータベース レベルの設定 (`is_memory_optimized_enabled`) をリストします。

```sql
SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>ハイブリッド バッファー プールのベスト プラクティス

 - Windows 上でご利用の PMEM デバイスをフォーマットする場合、NTFS に利用できる最大のアロケーション ユニット サイズ (Windows Server 2019 では 2 MB) を使用して、デバイスが DAX (Direct Access) 用に確実にフォーマットされているようにします。

 - Windows で [[メモリ内のページのロック]](./enable-the-lock-pages-in-memory-option-windows.md) を使用します。

 - ファイル サイズは 2 MB の倍数である必要があります (剰余 2 MB はゼロと等しい)。

 - ハイブリッド バッファー プールのサーバー スコープ設定が無効に設定されている場合、この機能はどのユーザー データベースでも使用されません。

 - ハイブリッド バッファー プールのサーバー スコープ設定が有効に設定されている場合、データベース スコープ設定を使用して、個々のユーザー データベースに対してこの機能を無効にすることができます。
