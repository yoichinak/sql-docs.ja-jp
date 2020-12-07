---
description: 新しいパブリケーションのスナップショットを使用したサブスクリプションの初期化
title: スナップショットを使用したサブスクリプションの初期化
ms.custom: ''
ms.date: 03/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 526be3921fa6b842415f0fbd2c78e2fd66981253
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475544"
---
# <a name="initialize-a-subscription-with-a-snapshot-for-a-new-publication"></a>新しいパブリケーションのスナップショットを使用したサブスクリプションの初期化

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

この記事では、レプリケーション パブリケーションが初期化されるときに発生する処理について説明します。 初期スナップショットは、サブスクライバーに適用されます。

## <a name="snapshot-for-a-new-publication"></a>新しいパブリケーションのスナップショット

既定では、パブリケーションの作成後にスナップショットがキャプチャされます。
スナップショットはスナップショット フォルダーにコピーされます。 この既定の動作は、パブリケーションの新規作成ウィザードを使用して作成されたマージ パブリケーションに対して発生します。

### <a name="snapshot-is-applied-to-subscriber"></a>スナップショットがサブスクライバーに適用される

新しいスナップショットは、サブスクライバーに適用されます。 適用は、サブスクリプションの初期同期中に行われます。 適用するエージェントは、パブリケーションの種類によって異なります。

- "_トランザクション_" パブリケーションと "_スナップショット_" パブリケーションの場合:
  - ディストリビューション エージェント。

- "_マージ_" パブリケーションの場合:
  - マージ エージェント。

### <a name="type-of-publication"></a>パブリケーションの種類

次の表は、パブリケーションの種類ごとのスナップショットの内容を示しています。

&nbsp;

| スナップショットの対象となるパブリケーションの種類 | スナップショットの内容 |
| :---------------------------------------- | :----------------------- |
| <ul> <li>スナップショット パブリケーション</li> <li>トランザクション パブリケーション</li> <li>パラメーター化されたフィルターを使用しないマージ パブリケーション</li> </ul> | <ul> <li>スキーマ</li> <li>一括コピー プログラム (BCP) のファイル内のデータ</li> <li>制約</li> <li>拡張プロパティ</li> <li>インデックス</li> <li>トリガー</li> <li>レプリケーションに必要なシステム テーブル</li> </ul> <br/>[スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)を参照。 |
| <ul> <li>パラメーター化されたフィルターを使用するマージ パブリケーション</li> </ul> | <ul> <li>スキーマ スナップショット (レプリケーション スクリプト、パブリッシュされたがデータがないオブジェクト)</li> <li>サブスクリプションのパーティションに属するデータ</li> </ul> <br/>[パラメーター化されたフィルターを使用したマージ パブリケーションのスナップショット](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)を参照。 |
| | |

#### <a name="two-part-process-with-merge-publication-that-uses-parameterized-filters"></a>パラメーター化されたフィルターを使用するマージ パブリケーションを使用した 2 部構成のプロセス

パラメーター化されたフィルターを使用するマージ パブリケーションの場合、スナップショットは、2 部構成のプロセスを使用して作成されます。

1. スキーマ スナップショットが作成されます。これには次の項目が含まれています。
   - レプリケーション スクリプト。
   - パブリッシュされたオブジェクトのスキーマ。
   - _(ただし、データはありません)。_

2. 各サブスクリプションはその後、スナップショットを使用して初期化されます。 スナップショットには、次の項目が含まれます。
   - スキーマ スナップショットからコピーされたスクリプトとスキーマ。
   - サブスクリプションのパーティションに属するデータ。

## <a name="type-of-replication"></a>レプリケーションの種類

スナップショットに含まれるファイルの種類は、レプリケーションの種類やパブリケーションのアーティクルによって異なります。

&nbsp;

| レプリケーションの種類 | 通常のスナップショット ファイル |
| :------------------ | :-------------------- |
| スナップショット レプリケーション、または<br/>トランザクション レプリケーション | &bullet; スキーマ (.sch) <br/>&bullet; データ (.bcp) <br/>&bullet; 制約とインデックス (.dri) <br/>&bullet; 圧縮スナップショット ファイル (.cab) <br/>&bullet; トリガー (. タグ)、サブスクライバーの更新のみ <br/><br/>&bullet; 制約 (idx) |
| マージ レプリケーション                                      | &bullet; スキーマ (.sch) <br/>&bullet; データ (.bcp) <br/>&bullet; 制約とインデックス (.dri) <br/>&bullet; 圧縮スナップショット ファイル (.cab) <br/>&bullet; トリガー (.trg) <br/><br/>&bullet; システム テーブル データ (.sys) <br/>&bullet; 競合テーブル (cft) |
| | |

### <a name="snapshot-folder"></a>[スナップショット フォルダー]

ファイルは、既定の "_スナップショット フォルダー_"、またはスナップショットの "_代替フォルダー_" にコピーされて転送されます。

スナップショット フォルダーは、ディストリビューターの構成時に指定されます。 代替フォルダーは、パブリケーションの作成時に指定されます。

### <a name="resume-transfer-after-interruption"></a>中断後に転送を再開する

信頼性の低い接続によって転送が中断された場合、スナップショット フォルダーへのファイルの転送は自動的に再開されます。

効率性のため、中断の前に完全に転送されたファイルは再送信されません。

## <a name="snapshot-options"></a>スナップショット オプション

スナップショットを使用してサブスクリプションを初期化するときに使用できるオプションがいくつかあります。 次のようにすることができます。

- 既定のスナップショット フォルダーを代替または追加する場所として、代替スナップショット フォルダーの場所を指定できます。 詳細については、[スナップショット オプションの変更](../../relational-databases/replication/snapshot-options.md)に関する記事を参照してください。

- リムーバブル メディア上に格納するためや低速なネットワーク上で転送するための圧縮スナップショットを使用できます。 詳細については、「 [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots)」を参照してください。

- スナップショットを適用する前または後に Transact-SQL スクリプトを実行できます。 詳細については、「[スナップショットが適用される前および後のスクリプトの実行](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。

- ファイル転送プロトコル (FTP) を使用してスナップショット ファイルを転送できます。 詳細については、「[FTP によるスナップショットの転送](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)」を参照してください。

## <a name="see-also"></a>参照

[サブスクリプションを初期化する](../../relational-databases/replication/initialize-a-subscription.md)

[スナップショット フォルダーのセキュリティ保護](../../relational-databases/replication/security/secure-the-snapshot-folder.md)
