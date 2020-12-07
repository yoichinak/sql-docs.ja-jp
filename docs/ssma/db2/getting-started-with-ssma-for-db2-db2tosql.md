---
description: SSMA for DB2 (DB2ToSQL) を使用したはじめに
title: SSMA for DB2 (DB2ToSQL) でのはじめに |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7cb317fc73f32a8795fe5ce4e5be9af776edf938
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454264"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>SSMA for DB2 (DB2ToSQL) を使用したはじめに
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for DB2 を使用すると、DB2 データベーススキーマをスキーマに簡単に変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、結果のスキーマをにアップロード [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] して、db2 からにデータを移行することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
このトピックでは、インストールプロセスについて説明した後、SSMA ユーザーインターフェイスについて理解することができます。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA を使用するには、最初に、ソースの DB2 データベースとのターゲットインスタンスの両方にアクセスできるコンピューターに SSMA クライアントプログラムをインストールする必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 を実行しているコンピューター上の DB2 OLEDB プロバイダー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 これらのコンポーネントは、DB2 システム関数のデータ移行とエミュレーションをサポートしています。 インストール手順については、「 [SSMA FOR DB2 &#40;DB2ToSQL&#41;のインストール ](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)」を参照してください。  
  
SSMA を開始するには、[**スタート**] をクリックし、[**すべてのプログラム**] をポイントします。次に、[db2] をポイントし、[ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for db2**] ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant**をクリックします。  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA for DB2 ユーザーインターフェイス  
SSMA のインストール後、SSMA を使用して DB2 データベースをに移行することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これは、開始する前に SSMA ユーザーインターフェイスを理解するのに役立ちます。 次の図は、メタデータエクスプローラー、メタデータ、ツールバー、出力ウィンドウ、および [エラー一覧] ウィンドウを含む SSMA のユーザーインターフェイスを示しています。  
  
![SSMA ユーザー インターフェイス](../../ssma/db2/media/ssma_db2_ui.png "SSMA ユーザー インターフェイス")  
  
移行を開始するには、最初に新しいプロジェクトを作成する必要があります。 次に、DB2 データベースに接続します。 接続に成功すると、db2 スキーマが DB2 メタデータエクスプローラーに表示されます。 次に、DB2 メタデータエクスプローラーでオブジェクトを右クリックして、への変換を評価するレポートの作成などのタスクを実行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 また、ツールバーとメニューを使用して、これらのタスクを実行することもできます。  
  
また、のインスタンスに接続する必要もあり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 接続が成功すると、データベースの階層 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメタデータエクスプローラーに表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 DB2 スキーマをスキーマに変換したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、それらの変換されたスキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メタデータエクスプローラーで選択し、スキーマをと同期し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
変換されたスキーマをと同期した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Db2 メタデータエクスプローラーに戻り、db2 スキーマのデータをデータベースに移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
これらのタスクとその実行方法の詳細については、「 [DB2 データベースの SQL Server &#40;DB2ToSQL&#41;への移行 ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)」を参照してください。  
  
次のセクションでは、SSMA ユーザーインターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータエクスプローラー  
SSMA には、DB2 とデータベースに対する操作を参照して実行するための2つのメタデータエクスプローラーが含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
#### <a name="db2-metadata-explorer"></a>DB2 メタデータエクスプローラー  
Db2 メタデータエクスプローラーには、DB2 スキーマに関する情報が表示されます。 DB2 メタデータエクスプローラーを使用すると、次のタスクを実行できます。  
  
-   各スキーマ内のオブジェクトを参照します。  
  
-   変換するオブジェクトを選択し、オブジェクトを構文に変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [DB2 スキーマ &#40;DB2ToSQL&#41;の変換 ](../../ssma/db2/converting-db2-schemas-db2tosql.md)」を参照してください。  
  
-   データ移行用のテーブルを選択し、それらのテーブルのデータをに移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [DB2 データベースの SQL Server &#40;DB2ToSQL&#41;への移行 ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)」を参照してください。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server メタデータエクスプローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メタデータエクスプローラーには、のインスタンスに関する情報が表示さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れます。 のインスタンスに接続すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ssma はそのインスタンスに関するメタデータを取得し、プロジェクトファイルに格納します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータエクスプローラーを使用して、変換された DB2 データベースオブジェクトを選択し、そのオブジェクトをのインスタンスと同期させることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
### <a name="metadata"></a>メタデータ  
各メタデータエクスプローラーの右側には、選択したオブジェクトを説明するタブがあります。 たとえば、DB2 メタデータエクスプローラーでテーブルを選択すると、 **テーブル**、 **SQL**、 **型マッピング、レポート**、 **プロパティ**、 **データ**の6つのタブが表示されます。 [ **レポート** ] タブには、選択したオブジェクトを含むレポートを作成した後にのみ情報が表示されます。 メタデータエクスプローラーでテーブルを選択すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **テーブル**、 **SQL**、 **データ**の3つのタブが表示されます。  
  
ほとんどのメタデータ設定は読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   DB2 メタデータエクスプローラーでは、プロシージャと型マッピングを変更できます。 変更されたプロシージャと型マッピングを変換するには、スキーマを変換する前に変更を加えます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータエクスプローラーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアドプロシージャのを変更できます。 でこれらの変更を確認するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、スキーマをに読み込む前に、これらの変更を行い [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
メタデータエクスプローラーで行った変更は、ソースまたはターゲットのデータベースではなく、プロジェクトのメタデータに反映されます。  
  
### <a name="toolbars"></a>ツールバー  
SSMA には、[プロジェクト] ツールバーと [移行] ツールバーの2つのツールバーがあります。  
  
#### <a name="the-project-toolbar"></a>[プロジェクト] ツールバー  
[プロジェクト] ツールバーには、プロジェクトを操作したり、DB2 に接続したり、に接続したりするためのボタンが含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのボタンは、[ **ファイル** ] メニューのコマンドに似ています。  
  
#### <a name="migration-toolbar"></a>移行ツールバー  
次の表は、移行ツールバーのコマンドを示しています。  
  
|Button|機能|  
|------|--------|  
|**レポートの作成**|選択した DB2 オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構文に変換し、変換が成功したかどうかを示すレポートを作成します。<br /><br />このコマンドは、DB2 メタデータエクスプローラーでオブジェクトが選択されていない限り、無効になっています。|  
|**スキーマの変換**|選択した DB2 オブジェクトをオブジェクトに変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br />このコマンドは、DB2 メタデータエクスプローラーでオブジェクトが選択されていない限り、無効になっています。|  
|**データの移行**|DB2 データベースからにデータを移行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このコマンドを実行する前に、DB2 スキーマをスキーマに変換し、オブジェクトをに読み込む必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br />このコマンドは、DB2 メタデータエクスプローラーでオブジェクトが選択されていない限り、無効になっています。|  
|**Stop**|現在のプロセスを停止します。|  
  
### <a name="menus"></a>メニュー  
SSMA メニューを次の表に示します。  
  
|メニュー|説明|  
|----|-----------|  
|**[最近使ったファイル]**|プロジェクトを操作したり、DB2 に接続したり、に接続したりするためのコマンドが含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**[編集]**|[ [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL の詳細] ペインからコピーするなど、詳細ページ内のテキストを検索して操作するためのコマンドが含まれています。 には、[ **ブックマークの管理** ] オプションも含まれています。このオプションを使用すると、既存のブックマークの一覧を表示できます。 ダイアログの右側にあるボタンを使用して、ブックマークを管理できます。|  
|**表示**|**メタデータエクスプローラーの同期**コマンドを含みます。 これにより、DB2 メタデータエクスプローラーとメタデータエクスプローラーの間でオブジェクトが同期され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 には、 **出力** ペインおよび **エラー一覧** ウィンドウの表示と非表示を切り替えるコマンドと、レイアウトを管理するためのオプション **レイアウト** も含まれています。|  
|**ツール**|レポートを作成し、オブジェクトとデータを移行するためのコマンドが含まれています。 [ **グローバル設定** ] および [プロジェクトの **設定** ] ダイアログボックスへのアクセスも提供します。|  
|**Help (ヘルプ)**|SSMA ヘルプおよび [ **バージョン情報** ] ダイアログボックスへのアクセスを提供します。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウとエラー一覧ペイン  
[ **表示** ] メニューには、[出力] ウィンドウと [エラー一覧] ウィンドウの表示を切り替えるためのコマンドが用意されています。  
  
-   [出力] ウィンドウには、オブジェクトの変換、オブジェクトの同期、およびデータ移行中に SSMA からのステータスメッセージが表示されます。  
  
-   エラー一覧ペインには、並べ替え可能な一覧にエラーメッセージ、警告メッセージ、および情報メッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[DB2 データの SQL Server &#40;DB2ToSQL&#41;への移行 ](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[ユーザーインターフェイスリファレンス &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
