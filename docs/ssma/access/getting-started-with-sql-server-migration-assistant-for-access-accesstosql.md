---
title: Access の SQL Server Migration Assistant を使ってみる |Microsoft Docs
description: SSMA を使用して Access データベースオブジェクトを SQL Server または Azure SQL Database オブジェクトに変換し、結果のオブジェクトをアップロードして、データを移行する方法については、「」をご覧ください。
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: e05bc860ec1cc9f3703a1d1c17441c4e1ad3de15
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100044622"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>アクセスのための SQL Server Migration Assistant の概要 (アクセス用 SQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access の Migration Assistant (SSMA) を使用すると、Access データベースオブジェクトを Azure SQL Database またはオブジェクトに簡単に変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、結果のオブジェクトをまたは Azure SQL Database にアップロードしたり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスからまたは Azure SQL Database にデータを移行したりすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 必要に応じて、または Azure SQL Database テーブルにアクセステーブルをリンクして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 既存のアクセスフロントエンドアプリケーションをまたは Azure SQL Database で引き続き使用できるようにすることもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
このトピックでは、インストールプロセスについて説明します。 SSMA ユーザーインターフェイスについて理解するのに役立ちます。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA を使用するに Azure SQL Database は、まず、移行するデータベースとのターゲットインスタンスの両方にアクセスできるコンピューターに SSMA クライアントプログラムをインストールする必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 インストール手順については、「 [&#41;&#40;Access の SQL Server Migration Assistant をインストールする ](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)」を参照してください。  
  
SSMA を開始するには、[ **スタート**] をクリックし、[ **すべてのプログラム**] をポイントします。次に、[ **アクセス SQL Server Migration Assistant**] をポイントし、[ **アクセス SQL Server Migration Assistant**] を選択します。  
  
## <a name="using-ssma"></a>SSMA の使用  
SSMA をインストールした後、このツールを使用して Access データベースをまたは Azure SQL Database に移行する前に、SSMA ユーザーインターフェイスに慣れることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA ユーザーインターフェイスは、次の図に示すように、メタデータエクスプローラー、メタデータ、ツールバー、出力ウィンドウ、および [エラー一覧] ウィンドウを含みます。  
  
![SSMA for Access のグラフィカル ユーザー インターフェイス](../../ssma/access/media/ssmaforaccessgui.gif "SSMA for Access のグラフィカル ユーザー インターフェイス")  
  
移行を開始するには、新しいプロジェクトを作成し、access データベースを追加して、メタデータエクスプローラーにアクセスします。 その後、Access Metadata Explorer で [オブジェクト] を右クリックして、次のようなタスクを実行できます。
- Access データベースオブジェクトのインベントリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database にエクスポートする。
- または Azure SQL Database への変換を評価するレポートを作成する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
- スキーマへのアクセススキーマの変換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と Azure SQL Database

また、ツールバーとメニューを使用して、これらのタスクを実行することもできます。  
  
また、のインスタンスに接続する必要もあり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 接続に成功すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メタデータエクスプローラーにデータベースの階層が表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 アクセススキーマをスキーマに変換した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、メタデータエクスプローラーで変換されたスキーマを選択し、スキーマをに読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[新しいプロジェクト] ダイアログボックスの [移行先] ドロップダウンから Azure SQL Database を選択した場合は、Azure SQL Database に接続する必要があります。 接続に成功すると、Azure SQL Database データベースの階層が Azure SQL Database メタデータエクスプローラーに表示されます。 アクセススキーマを Azure SQL Database スキーマに変換した後 Azure SQL Database メタデータエクスプローラーで変換されたスキーマを選択し、スキーマをに読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
変換されたスキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に読み込むと、メタデータエクスプローラーにアクセスして、access データベースからまたは Azure SQL Database データベースにデータを移行することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたは Azure SQL Database テーブルにアクセステーブルをリンクすることもできます。  
  
これらのタスクとその実行方法の詳細については、次のトピックを参照してください。  
  
-   [Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [Access アプリケーションの SQL Server へのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
次のセクションでは、SSMA ユーザーインターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータエクスプローラー  
SSMA には2つのメタデータエクスプローラーが含まれており、アクセスしたり Azure SQL Database データベースに対して操作を実行したりするために使用でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
#### <a name="access-metadata-explorer"></a>メタデータ エクスプローラーにアクセスする  
Access メタデータエクスプローラーには、プロジェクトに追加された Access データベースに関する情報が表示されます。 Access データベースを追加すると、SSMA によってそのデータベースに関するメタデータが取得されます。これは Access メタデータエクスプローラーで使用できるメタデータです。  
  
Access Metadata Explorer を使用して、次のタスクを実行できます。  
  
-   各 Access データベースのテーブルを参照します。  
  
-   変換するオブジェクトを選択し、オブジェクトを構文に変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [Access データベースオブジェクトの変換](converting-access-database-objects-accesstosql.md)」を参照してください。  
  
-   データ移行用のオブジェクトを選択し、それらのオブジェクトからにデータを移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「SQL Server への [アクセスデータの移行](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)」を参照してください。  
  
-   アクセスとテーブルのリンクとリンク解除を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 行います。  
  
#### <a name="sql-server-or-azure-sql-database-metadata-explorer"></a>SQL Server または Azure SQL Database メタデータエクスプローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database メタデータエクスプローラーでは、または Azure SQL Database のインスタンスに関する情報が表示さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れます。 または Azure SQL Database のインスタンスに接続すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA はそのインスタンスに関するメタデータを取得し、プロジェクトファイルに格納します。  
  
SQL Server または Azure SQL Database メタデータエクスプローラーを使用して、変換された Access データベースオブジェクトを選択し、それらのオブジェクトをのインスタンスまたは Azure SQL Database に読み込んで (同期する) ことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
詳細については、「変換された [データベースオブジェクトの SQL Server への読み込み](loading-converted-database-objects-into-sql-server-accesstosql.md)」を参照してください。  
  
### <a name="metadata"></a>Metadata  
各メタデータエクスプローラーの右側には、選択したオブジェクトを説明するタブがあります。 たとえば、Access Metadata Explorer でテーブルを選択すると、 **テーブル**、 **型マッピング**、 **プロパティ**、 **データ** の4つのタブが表示されます。 メタデータエクスプローラーでテーブルを選択すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **テーブル**、 **SQL**、 **データ** の3つのタブが表示されます。  
  
ほとんどのメタデータ設定は読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   Access Metadata Explorer では、型マッピングを変更できます。 レポートを作成したりスキーマを変換したりする前に、必ずこれらの変更を行ってください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータエクスプローラーでは、[**テーブル**] タブでテーブルおよびインデックスのプロパティを変更できます。スキーマをに読み込む前に、これらの変更を行っ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] てください。 詳細については、「 [Access データベースオブジェクトの変換](converting-access-database-objects-accesstosql.md)」を参照してください。  
  
### <a name="toolbars"></a>ツールバー  
SSMA には、[プロジェクト] ツールバーと [移行] ツールバーの2つのツールバーがあります。  
  
#### <a name="the-project-toolbar"></a>[プロジェクト] ツールバー  
プロジェクトツールバーには、プロジェクトを操作したり、Access データベースファイルを追加したり、または Azure SQL Database に接続したりするためのボタンが含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのボタンは、[ **ファイル** ] メニューのコマンドに似ています。  
  
#### <a name="the-migration-toolbar"></a>[移行] ツールバー  
[移行] ツールバーには、次のコマンドがあります。  
  
|ボタン|Function|  
|----------|------------|  
|**変換、読み込み、および移行**|Access データベースを変換し、変換されたオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に読み込み、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に移行します。すべて1回の手順で行うことができます。|  
|**レポートの作成**|選択したアクセススキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database 構文に変換し、変換が成功したかどうかを示すレポートを作成します。<br /><br />このコマンドは、Access メタデータエクスプローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**スキーマの変換**|選択したアクセススキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database スキーマに変換します。<br /><br />このコマンドは、Access メタデータエクスプローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**データの移行**|Access データベースからまたは Azure SQL Database にデータを移行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このコマンドを実行する前に、アクセススキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database スキーマに変換し、オブジェクトをまたは Azure SQL Database に読み込む必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br />このコマンドは、Access メタデータエクスプローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**Stop**|オブジェクトをまたは Azure SQL Database 構文に変換するなど、現在のプロセスを停止し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
  
### <a name="menus"></a>メニュー  
SSMA には、次のメニューが含まれています。  
  
|メニュー|説明|  
|--------|---------------|  
|**[最近使ったファイル]**|移行ウィザードのコマンド、プロジェクトの操作、Access データベースファイルの追加と削除、およびへの接続と Azure SQL Database への接続が含まれ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**編集**|[ [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL の詳細] ペインからコピーするなど、詳細ページ内のテキストを検索して操作するためのコマンドが含まれています。 [ブックマークの **管理** ] ダイアログを開くには、[編集] メニューの [ブックマークの管理] をクリックします。 ダイアログには、既存のブックマークの一覧が表示されます。 ダイアログの右側にあるボタンを使用して、ブックマークを管理できます。|  
|**表示**|**メタデータエクスプローラーの同期** コマンドを含みます。 これにより、Access メタデータエクスプローラーと Azure SQL Database メタデータエクスプローラーの間でオブジェクトが同期され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 には、 **出力** ペインおよび **エラー一覧** ウィンドウの表示と非表示を切り替えるコマンドと、レイアウトで管理するオプション **レイアウト** も含まれています。|  
|**ツール**|レポートの作成、データのエクスポート、オブジェクトとデータの移行、テーブルのリンク、および [グローバルおよびプロジェクトの設定] ダイアログボックスへのアクセスを行うためのコマンドが含まれています。|  
|**ヘルプ**|SSMA ヘルプおよび [ **バージョン情報** ] ダイアログボックスへのアクセスを提供します。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウとエラー一覧ペイン  
[ **表示** ] メニューには、[出力] ウィンドウと [エラー一覧] ウィンドウの表示を切り替えるためのコマンドが用意されています。  
  
-   [出力] ウィンドウには、オブジェクトの変換、オブジェクトの同期、およびデータ移行中に SSMA からのステータスメッセージが表示されます。  
  
-   エラー一覧ペインには、エラー、警告、および情報の各メッセージが一覧に表示され、並べ替えることができます。  
  
## <a name="see-also"></a>関連項目  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
