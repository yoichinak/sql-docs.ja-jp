---
description: MSSQLSERVER_847
title: MSSQLSERVER_847 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 847 (Database Engine error)
ms.assetid: 67208b7c-bd8d-48a1-9f70-a6488e0f5f9b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ece596b38638f4e043fac150e683682a551592de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420946"
---
# <a name="mssqlserver_847"></a>MSSQLSERVER_847
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|847|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|該当なし|  
|メッセージ テキスト|ラッチを待機中にタイムアウトが発生しました。クラス '%ls'、ID %p、型 %d、タスク 0x%p : %d、待機時間 %d、フラグ 0x%I64x、所有しているタスク 0x%p。 待機を続行します。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってバッファー ラッチ エラーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに書き込まれるのと同時に、コンピューターが応答を停止するか、タイムアウトなどにより通常の操作が中断される場合があります。  
  
メッセージの状態フィールドの値 0x04 がオンの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は I/O 操作を待機しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログにメッセージ [MSSQLSERVER_833](~/relational-databases/errors-events/mssqlserver-833-database-engine-error.md) を受信する場合もあります。  
  
メッセージの状態フィールドの値 0x04 がオフの場合、ページに対して多数の競合が存在します。 オブジェクトがデータ ページの場合、非効率なコード デザインに起因している可能性があります。 データ以外のページの場合、ハードウェア リソースの不足など、サーバーのボトルネックによってエラーが発生した可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
この問題を回避するには、環境に応じて次の 1 つ以上の手順を実行します。これにより、エラー メッセージの発生を回避または減らすことができる可能性があります。  
  
-   ハードウェアにボトルネックがあるかどうかを判断します。 必要な場合、使用している環境の構成、クエリ、および負荷要件がサポートされるように、ハードウェアをアップグレードします。 ボトルネックの詳細については、「[Identify Bottlenecks](~/relational-databases/performance/identify-bottlenecks.md)」 (ボトルネックの特定) を参照してください。  
  
-   記録されたエラーを確認し、ハードウェア ベンダーの提供する診断を実行します。  
  
-   ディスク ドライブが圧縮されていないことを確認してください。 データ ファイルやログ ファイルを圧縮ドライブに格納することはできません。 物理的ファイルの詳細については、「[Database Files and Filegroups](~/relational-databases/databases/database-files-and-filegroups.md)」 (データベース ファイルとファイル グループ) をご覧ください。  
  
-   次のオプションをオフに設定して、エラー メッセージが消えるかどうかを確認します。  
  
    -   SQL Server の priority boost 構成オプション  
  
    -   簡易プーリング (ファイバー モード) オプション  
  
    -   set working set size オプション  
  
    > [!NOTE]  
    > これらの設定を既定のオフから変更すると、多くの場合、効率が悪化します。 詳細については、「[Server Configuration Options &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)」 (サーバー構成オプション (SQL Server)) を参照してください。  
  
-   クエリをチューニングして、システムで使用するリソースを削減します。 パフォーマンス チューニングは、システム負荷の削減と、個々のクエリの応答時間改善に役立ちます。  
  
-   AUTO_SHRINK オプションをオフにして、データベース サイズに対する変更のオーバーヘッドを軽減します。  
  
-   FILEGROWTH オプションに、頻繁になりすぎないように十分な大きさを持った増分値を設定するようにします。 データベース内で使用可能な領域を確認するジョブをスケジュールし、ピーク時以外にデータベース サイズを大きくします。  
  
