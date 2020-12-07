---
description: '[フルテキスト インデックス] ダイアログ ボックス (Visual Database Tools)'
title: '[フルテキスト インデックス] ダイアログ ボックス'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 68b0546f18d5026caf7e0a141eb58bd62efa2188
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034878"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>[フルテキスト インデックス] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
このダイアログ ボックスを使用すると、データベース テーブルのテキスト ベースの列に対するフルテキスト検索用にフルテキスト インデックスを作成できます。 フルテキスト インデックスは、通常のインデックスに基づくため、最初に通常のインデックスを作成する必要があります。 通常のインデックスは、単一の非 null 列に作成する必要があります。大きな値を格納している列ではなく、小さな値を格納している列を選択するのが最も適切です。  
  
> [!NOTE]
> フルテキスト インデックスを作成する場合、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、Enterprise Manager などの外部ツールを使用して、あらかじめデータベースのフルテキスト カタログを作成しておく必要があります。  
> 
> [!NOTE]
> フルテキスト インデックスの機能は、 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで利用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2012 の各エディションがサポートする機能](../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
## <a name="options"></a>Options  
**[選択されたフルテキスト インデックス]**  
既存のフルテキスト インデックスを一覧表示します。 インデックスを選択すると、右のグリッドにそのインデックスのプロパティが表示されます。 一覧が空の場合、テーブルにフルテキスト インデックスは定義されていません。  
  
**追加**  
新しいフルテキスト インデックスを作成します。  
  
**削除**  
**[選択されたフルテキスト インデックス]** ボックスの一覧で選択したフルテキスト インデックスを削除します。  
  
**[全般] カテゴリ**  
展開して **[列]** および **[フルテキスト カタログ名]** を表示します。  
  
**[列]**  
フルテキスト検索ができる列の名前を、コンマ区切りの一覧として表示します。 完全な一覧を表示するには、プロパティ フィールドの左側にある省略記号ボタン ( **[...]** ) をクリックします。  
  
**Full-Text Catalog Name**  
フルテキスト インデックスが格納されているフルテキスト カタログの名前を表示します。 インデックスを別のカタログに格納するには、カタログ名をクリックし、ドロップダウン リストから別のカタログを選択します。  
  
> [!NOTE]  
> カタログは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Enterprise Manager などの外部ツールで、あらかじめ作成しておく必要があります。  
  
**[IDENTITY] カテゴリ**  
展開してインデックスの名前フィールドを表示します。  
  
**名前**  
システムが指定したフルテキスト インデックスの名前を表示します。  
  
**[テーブル デザイナー] カテゴリ**  
展開してインデックスの実行方法を指定するプロパティを表示します。  
  
**アクティブ**  
該当するフルテキスト インデックスを使用して、フルテキスト検索を現在実行できるかどうかを示します。  
  
**[トラッキング設定の変更]**  
該当するインデックスの変更履歴の状態を示します。[手動]、[自動]、または [オフ]。  
  
**[クロールの完了]**  
最近のクロールが完了したかどうかを示します。 このプロパティ値が [いいえ] の場合、クロールは現在進行中です。  
  
**[現在または最近のクロールの終了日時]**  
最近のクロールが終了した日時を表示します。  
  
**[現在または最近のクロール内のエラー]**  
現在のクロールまたは最近のクロールで発生したエラーの数を表示します。  
  
**[インデックス バージョン]**  
クロールが開始した時点での、テーブルのスキーマ バージョンを表示します。  
  
**[現在または最近のクロール内の行]**  
現在のクロールまたは最近のクロールで更新された行の数を表示します。  
  
**[現在または最近のクロールの開始日時]**  
現在のクロールまたは最近のクロールが開始した日時を表示します。  
  
**[次のクロールのタイムスタンプ]**  
次のクロールが開始する日時を表示します。  
  
**[現在または最近のクロールの種類]**  
現在のクロールまたは最近のクロールの型を表示します。[空き領域なし]、[インクリメンタル]、[更新]、または [自動伝達]。  
  
**[一意のインデックス名]**  
一意の単一列インデックスを持つ、データベース内のすべての列の名前を一覧表示します。 これらの列は、フルテキスト インデックスの作成に使用できます。  
  
## <a name="see-also"></a>関連項目  
[フルテキスト インデックス作成ウィザードの使用](../../relational-databases/search/use-the-full-text-indexing-wizard.md)  
[CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
