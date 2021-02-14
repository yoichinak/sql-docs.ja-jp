---
title: SSMA for SAP ASE でのはじめに (SybaseToSQL) |Microsoft Docs
description: SAP ASE のインストールプロセスの SQL Server Migration Assistant (SSMA) について説明し、SSMA ユーザーインターフェイスについて理解を深めます。
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2ed1698af612a3bd960b7c16011dc4f95e33f61a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100078863"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>SSMA for SAP ASE でのはじめに (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SAP ASE 用の Migration Assistant (SSMA) を使用すると、SAP Adaptive Server Enterprise (ASE) データベーススキーマを簡単にまたは Azure SQL Database スキーマに変換したり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結果のスキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database にアップロードしたり、sap ase からまたは Azure SQL Database にデータを移行したりでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
このトピックでは、インストールプロセスについて説明した後、SSMA ユーザーインターフェイスについて理解することができます。  
  
## <a name="installing-and-licensing-ssma"></a>SSMA のインストールとライセンス  
SSMA を使用するに Azure SQL Database は、まず、SAP ASE のソースインスタンスとのターゲットインスタンスの両方にアクセスできるコンピューターに SSMA クライアントプログラムをインストールする必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 サーバー側のデータ移行を使用するには、を実行しているコンピューターに拡張パックと、少なくとも1つの SAP ASE プロバイダー (OLE DB または ADO.NET) をインストールする必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのコンポーネントは、SAP ASE システム関数のデータ移行とエミュレーションをサポートしています。 インストール手順については、「 [SSMA FOR SAP ASE &#40;SybaseToSQL&#41;のインストール ](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)」を参照してください。  
  
Ssma を開始するには、[**スタート**] をクリックし、[**すべてのプログラム**] をポイントします。次に、[sybase] **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [Migration Assistant**] をポイントし、[ **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sybase の Migration Assistant**] を選択します。 SSMA を初めて起動したときに、[ライセンス] ダイアログボックスが表示されます。 SSMA を使用するには、Windows Live ID を使用して SSMA のライセンスを付与する必要があります。 ライセンスの手順については、「 [SSMA For Sybase クライアントのインストール &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) 」のインストール手順を参照してください。  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA for SAP ASE のユーザーインターフェイス  
SSMA のインストールとライセンス供与が完了したら、SSMA を使用して、SAP ASE データベースをまたは Azure SQL Database に移行することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これは、開始する前に SSMA ユーザーインターフェイスを理解するのに役立ちます。 次の図は、メタデータエクスプローラー、メタデータ、ツールバー、出力ウィンドウ、および [エラー一覧] ウィンドウを含む SSMA のユーザーインターフェイスを示しています。  
  
![SSMA for SAP ASE のユーザーインターフェイス](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA for SAP ASE のユーザーインターフェイス")  
  
移行を開始するには、最初に新しいプロジェクトを作成する必要があります。 次に、SAP ASE に接続します。 接続が成功すると、SAP ASE データベースの階層が Sybase メタデータエクスプローラーに表示されます。 Sybase メタデータエクスプローラーでオブジェクトを右クリックして、または Azure SQL Database への変換を評価するレポートの作成などのタスクを実行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 また、ツールバーやメニューを使用して、これらのタスクを実行することもできます。  
  
また、のインスタンスまたは Azure SQL Database に接続する必要もあり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 接続が成功すると、また [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は SQL Azure メタデータエクスプローラーにまたは Azure SQL データベースの階層が表示されます。 SAP ASE スキーマをまたは Azure SQL Database スキーマに変換した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、または SQL Azure メタデータエクスプローラーで変換されたスキーマを選択 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] してから、または Azure SQL Database にスキーマを読み込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
変換されたスキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に読み込むと、Sybase メタデータエクスプローラーに戻り、SAP ASE データベースから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL データベースにデータを移行することができます。  
  
これらのタスクとその実行方法の詳細については、「SAP ASE データベースの SQL Server への移行」を参照してください。 [Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)。  
  
次のセクションでは、SSMA ユーザーインターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータエクスプローラー  
SSMA には、SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または AZURE SQL データベースに対する操作を参照して実行するための2つのメタデータエクスプローラーが含まれています。  
  
#### <a name="sybase-metadata-explorer"></a>Sybase メタデータエクスプローラー  
Sybase メタデータエクスプローラーには、SAP ASE のソースインスタンス上のデータベースに関する情報が表示されます。  
  
Sybase メタデータエクスプローラーを使用すると、次のタスクを実行できます。  
  
-   各データベース内のテーブルを参照します。  
  
-   変換するオブジェクトを選択し、オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database 構文に変換します。 詳細については、「 [sql&#41;&#40;の SAP ASE データベースオブジェクトの変換 ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)」を参照してください。  
  
-   データ移行用のオブジェクトを選択し、それらのオブジェクトからまたは Azure SQL Database にデータを移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [SQL Server Azure SQL Database &#40;SybaseToSQL&#41;への SAP ASE データの移行 ](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)」を参照してください。  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server または SQL Azure メタデータエクスプローラー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure メタデータエクスプローラーでは、または Azure SQL Database のインスタンスに関する情報が表示さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れます。 または Azure SQL Database のインスタンスに接続すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA はそのインスタンスに関するメタデータを取得し、プロジェクトファイルに格納します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーを使用して、変換された SAP ASE データベースオブジェクトを選択し、それらのオブジェクトをまたは Azure SQL Database のインスタンスに読み込んで (同期) でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
詳細については、「変換された [データベースオブジェクトを SQL Server &#40;SybaseToSQL&#41;に読み込む ](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md)」を参照してください。  
  
### <a name="metadata"></a>Metadata  
各メタデータエクスプローラーの右側には、選択したオブジェクトを説明するタブがあります。 たとえば、Sybase メタデータエクスプローラーでテーブルを選択すると、 **テーブル**、 **SQL**、 **型マッピング**、 **データ**、 **プロパティ**、および **レポート** の6つのタブが表示されます。 [ **レポート** ] タブには、選択したオブジェクトを含むレポートを作成した後にのみ情報が表示されます。 または SQL Azure メタデータエクスプローラーでテーブルを選択すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **テーブル**、 **SQL**、 **データ** の3つのタブが表示されます。  
  
ほとんどのメタデータ設定は読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   Sybase Metadata Explorer では、プロシージャと型マッピングを変更できます。 スキーマを変換する前に、これらの変更を行います。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアドプロシージャのを変更できます。 スキーマをに読み込む前に、これらの変更を行い [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
メタデータエクスプローラーで行った変更は、ソースまたはターゲットのデータベースではなく、プロジェクトのメタデータに反映されます。  
  
### <a name="toolbars"></a>ツールバー  
SSMA には、[プロジェクト] ツールバーと [移行] ツールバーの2つのツールバーがあります。  
  
#### <a name="the-project-toolbar"></a>[プロジェクト] ツールバー  
プロジェクトツールバーには、プロジェクトを操作したり、SAP ASE に接続したり、または Azure SQL Database に接続したりするためのボタンが含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのボタンは、[ **ファイル** ] メニューのコマンドに似ています。  
  
#### <a name="the-migration-toolbar"></a>[移行] ツールバー  
[移行] ツールバーには、次のコマンドがあります。  
  
|ボタン|Function|  
|----------|------------|  
|**レポートの作成**|選択した SAP ASE オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構文に変換し、変換が成功したかどうかを示すレポートを作成します。<br /><br />このコマンドは、Sybase メタデータエクスプローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**スキーマの変換**|選択した SAP ASE オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database オブジェクトに変換します。<br /><br />このコマンドは、Sybase メタデータエクスプローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**データの移行**|SAP ASE データベースからまたは Azure SQL Database にデータを移行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このコマンドを実行する前に、SAP ASE スキーマを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database スキーマに変換し、オブジェクトをまたは Azure SQL Database に読み込む必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br />このコマンドは、Sybase メタデータエクスプローラーでオブジェクトが選択されている場合にのみ使用できます。|  
|**Stop**|オブジェクトをまたは Azure SQL Database 構文に変換するなど、現在のプロセスを停止し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
  
### <a name="menus"></a>メニュー  
SSMA には、次のメニューが含まれています。  
  
|メニュー|説明|  
|--------|---------------|  
|**[最近使ったファイル]**|プロジェクトを操作したり、SAP ASE に接続したり、または Azure SQL Database に接続したりするためのコマンドが含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**編集**|[ [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL の詳細] ペインからコピーするなど、詳細ページ内のテキストを検索して操作するためのコマンドが含まれています。 には、[ **ブックマークの管理** ] オプションもあります。このオプションでは、既存のブックマークの一覧が表示されます。 ダイアログの右側にあるボタンを使用して、ブックマークを管理できます。|  
|**表示**|**メタデータエクスプローラーの同期** コマンドを含みます。 これにより、Sybase メタデータエクスプローラーと SQL Azure メタデータエクスプローラー間でオブジェクトが同期され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 には、 **出力** ペインおよび **エラー一覧** ウィンドウの表示と非表示を切り替えるコマンドと、レイアウトを管理するためのオプション **レイアウト** も含まれています。|  
|**ツール**|レポートの作成、データのエクスポート、およびオブジェクトとデータの移行を行うためのコマンドが含まれています。 [ **グローバル設定** ] および [プロジェクトの **設定** ] ダイアログボックスへのアクセスも提供します。|  
|**テスト担当者**|テストケースを作成したり、テスト結果を表示したり、データベースバックアップ管理のコマンドを表示したりするためのコマンドが含まれています。|  
|**ヘルプ**|SSMA ヘルプおよび [ **バージョン情報** ] ダイアログボックスへのアクセスを提供します。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウとエラー一覧ペイン  
[ **表示** ] メニューには、[出力] ウィンドウと [エラー一覧] ウィンドウの表示を切り替えるためのコマンドが用意されています。  
  
-   [出力] ウィンドウには、オブジェクトの変換、オブジェクトの同期、およびデータ移行中に SSMA からのステータスメッセージが表示されます。  
  
-   エラー一覧ペインには、エラー、警告、および情報の各メッセージが一覧に表示され、並べ替えることができます。  
  
## <a name="see-also"></a>関連項目  
[SAP ASE データベースの SQL Server Azure SQL Database &#40;SybaseToSQL&#41;への移行 ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[ユーザーインターフェイスリファレンス &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
