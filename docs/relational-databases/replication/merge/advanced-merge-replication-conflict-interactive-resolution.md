---
description: マージ レプリケーションの競合の詳細 - インタラクティブな解決
title: インタラクティブな競合解決 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 07b8552da25b0ba9d79320c09d3fb4eb8f346532
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867908"
---
# <a name="advanced-merge-replication-conflict---interactive-resolution"></a>マージ レプリケーションの競合の詳細 - インタラクティブな解決
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションには、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同期マネージャーでの要求時同期中に、手動で競合を解決できるインタラクティブ競合回避モジュールが用意されています。 インタラクティブ競合回避モジュールを実行時に有効化すると、グラフィカル インターフェイスに競合する各行のデータが表示されます。ここから、競合するデータを表示および編集し、個々の競合を解決できます。  
  
 インタラクティブ競合回避モジュールは競合表示モジュールに似ています。 ただし、競合表示モジュールではマージ同期後に解決済みの競合の結果が表示されるのに対して、インタラクティブ競合回避モジュールでは解決の前に各競合が表示されるため、マージ同期時に取り込むデータを指定できます。 いずれかのユーザーが、競合発生時にインタラクティブ競合回避モジュールを監視できるようになっている必要があります。  
  
> [!NOTE]  
>  インタラクティブな競合回避には Windows 同期マネージャーが必要です。 同期が Windows 同期マネージャーの外部で (スケジュールされた同期、または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] かレプリケーション モニターでの要求時同期として) 実行される場合、競合は、アーティクルに指定された競合回避モジュールに従って、ユーザーの介入なしに自動的に解決されます。 論理レコードに関連する競合は、インタラクティブ競合回避モジュールには表示されません。 これらの競合に関する情報を表示するには、レプリケーション ストアド プロシージャを使用します。 詳細については、「[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](../view-and-resolve-data-conflicts-for-merge-publications.md)」を参照してください。  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>アーティクル競合回避モジュールおよびインタラクティブ競合回避モジュール  
 競合回避モジュール (既定の競合回避モジュール、ビジネス ロジック ハンドラー、カスタム競合回避モジュールのいずれか) は、パブリケーションの作成時に特定のアーティクルに割り当てられます。そこでルールのセットによって、競合している行データを入力したときにどのデータセットを使用するかが決まります。 インタラクティブ競合回避モジュールは、競合でどのデータを優先するかを指定するルールを持つ独立した競合回避モジュールではなく、既定またはカスタムの競合回避モジュールと組み合わせて使用するツールです。 アーティクル競合回避モジュールでは、どの行を競合で優先し、どの行を優先しないかが指定されますが、インタラクティブ競合回避モジュールでは、その結果にユーザーが介入し、データを受け入れたり、拒否したり、変更したりすることができます。  
  
 インタラクティブ競合回避モジュールを使用するには、競合回避を必要とする各アーティクルまたはサブスクリプションに対して、インタラクティブな競合回避を有効にしておく必要があります。 1 つ以上のアーティクルまたはサブスクリプションで有効にしておくと、マージ同期中に競合が検出された場合、インタラクティブ競合回避モジュールを使用できます。  
  
 インタラクティブ競合回避モジュールを使用するには、[マージ レプリケーションのオプションの指定](../../../relational-databases/replication/merge/specify-merge-replication-properties.md)に関するページと、[Windows 同期マネージャーを使用したサブスクリプションの同期 (Windows 同期マネージャー)](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md) に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーションの競合検出および解決の詳細](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
