---
title: 永続的なメモリ (PMEM) の構成
description: SQL Server on Linux 用に永続メモリ (PMEM) を構成する方法、および PMEM デバイス用の名前空間を作成する方法について説明します。
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.date: 10/31/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: c6f791cf96520f46c37bb061f30ac7df962695e5
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115690"
---
# <a name="configure-persistent-memory-pmem-for-sql-server-on-linux"></a>SQL Server on Linux 用に永続メモリ (PMEM) を構成する

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] on Linux 用に永続メモリ (PMEM) を構成する方法について説明します。

## <a name="overview"></a>概要

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] には、永続メモリを使用するインメモリ機能が多数あります。 このドキュメントでは、SQL Server on Linux 用に永続メモリを構成するために必要な手順について説明します。

> [!NOTE]
> 用語_エンライトメント_は、永続メモリ対応ファイル システムの操作の概念を伝えるために導入されました。 ユーザー スペース アプリケーションからファイル システムへの直接アクセスは、メモリ マッピング (`mmap()`) を使用することで容易になります。 ファイルのメモリ マッピングを作成すると、アプリケーションは、I/O スタックを完全にバイパスするロード命令またはストア命令を発行できます。 これは、ホスト拡張アプリケーション (SQLPAL と Windows OS または Linux OS がやり取りできるようにするブラック ボックス コード) の観点からは、「エンライトメントされた」ファイル システムと見なされます。

## <a name="create-namespaces-for-pmem-devices"></a>PMEM デバイスの名前空間を作成する

### <a name="configure-the-devices"></a>デバイスを構成する

Linux では `ndctl` ユーティリティを使用します。

- `ndctl` をインストールして、PMEM デバイスを構成します。 詳しくは[こちら](https://docs.pmem.io/getting-started-guide/installing-ndctl)をご覧ください。
- `ndctl` を使用して名前空間を作成します。 名前空間は、PMEM NVDIMM 間でインターリーブされ、デバイス上のメモリ領域へのさまざまな種類のユーザースペース アクセスを提供できます。 `fsdax` は、SQL Server の既定のモードであり、望ましいモードです。

```bash 
ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=dev
```

`fsdax` モードを選択しており、システム メモリを使用してページごとのメタデータを格納していることに注意してください。 `--map=dev`を使用することをお勧めします。 これは、メタデータを名前空間に直接格納します。 現時点では、`--map=mem` を使用してメタデータをメモリに格納するのは試験的であると見なされます。

`ndctl` を使用して名前空間を確認します。 
  
サンプル出力を次に示します。

```bash
# ndctl list -N
{
  "dev":"namespace0.0",
  "mode":"fsdax",
  "map":"dev",
  "size":4294967296,
  "sector_size":512,
  "blockdev":"pmem0",
  "numa_node":0
}
```

### <a name="create-and-mount-pmem-device"></a>PMEM デバイスの作成とマウント

例: XFS

```bash
mkfs.xfs -f /dev/pmem0
mount -o dax,noatime /dev/pmem0 /mnt/dax
xfs_io -c "extsize 2m" /mnt/dax
```

例: EXT4

```bash
mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
mount -o dax,noatime /dev/pmem0 /mnt/dax
```

## <a name="technical-considerations"></a>技術的な考慮事項

- 前述のとおり、XFS または EXT4 のいずれかに 2MB のブロック割り当て
- ブロック割り当てと `mmap` の不整合により、4KB へのサイレント フォールバックが発生
- ファイル サイズを 2MB の倍数 (剰余 2MB) である必要がある
- Transparent Huge Pages (THP) を無効にしない (ほとんどのディストリビューションでは既定で有効化)

デバイスを `ndctl` を使用して構成し、作成とマウントを行ったら、そこにデータベース ファイルを配置するか、新しいデータベースを作成できます。

PMEM デバイスは、O_DIRECT (ダイレクト I/O) セーフであるため、トレース フラグ 3979 を有効にして強制フラッシュ メカニズムを無効にすることを検討してください。 詳細については、[FUA のサポート](https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux) に関するページをご覧ください。 強制ユニット アクセスの内部については、[FUA の内部](/archive/blogs/bobsql/sql-server-on-linux-forced-unit-access-fua-internals)に関するページをご覧ください。

## <a name="next-steps"></a>次のステップ

SQL Server on Linux について詳しくは、「[SQL Server on Linux](sql-server-linux-overview.md)」をご覧ください。
SQL Server on Linux のパフォーマンスに関するベスト プラクティスについては、[パフォーマンスのベスト プラクティス](sql-server-linux-performance-best-practices.md)に関するページをご覧ください。