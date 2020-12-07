---
description: SQL Server Compact Edition 接続マネージャー
title: SQL Server Compact Edition 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlmobileconnection.connection.f1
- sql13.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae61fcfcec740ee26a7fc2a57c0e03b0141e6e10
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88425944"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーを使用すると、パッケージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先では、この接続マネージャーの使用により、データが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベース内のテーブルに読み込まれます。  
  
> [!NOTE]  
>  64 ビット コンピューターでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データ ソースに接続するパッケージを 32 ビット モードで実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact データ ソースへの接続に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Provider は、32 ビット版でのみ使用できます。  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 接続マネージャーの構成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーをパッケージに追加すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定して、接続マネージャーをパッケージの **接続** コレクションに追加します。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **SQLMOBILE** に設定されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーは、次の方法で構成できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースの場所を指定する接続文字列を指定します。  
  
-   パスワードで保護されているデータベースのパスワードを指定します。  
  
-   データベースが格納されるサーバーを指定します。  
  
-   接続マネージャーから作成される接続を、実行時に保持するかどうかを指定します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="sql-server-compact-edition-connection-manager-editor-connection-page"></a>[SQL Server Compact Edition 接続マネージャー エディター] ([接続] ページ)
  **[SQL Server Compact Edition 接続マネージャー エディター]** ダイアログ ボックスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続するためのプロパティを指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 接続マネージャーについて詳しくは、「 [SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)」をご覧ください。  
  
### <a name="options"></a>オプション  
 **[データベースのファイル名とパスを入力]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースのパスとファイル名を入力します。  
  
 **[参照]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server Compact Edition データベースの選択] **ダイアログ ボックスを使用して、目的の** Compact データベース ファイルを探します。  
  
 **[データベースのパスワードを入力]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースのパスワードを入力します。  
  
## <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>[SQL Server Compact Edition 接続マネージャー エディター] ([すべて] ページ)
  **[SQL Server Compact Edition 接続マネージャー エディター]** ダイアログ ボックスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続するためのプロパティを指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 接続マネージャーについて詳しくは、「 [SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)」をご覧ください。  
  
### <a name="options"></a>オプション  
 **[AutoShrink Threshold]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベース ファイルの空き容量 (%) がどの程度になったら自動圧縮プロセスを実行するかを指定します。  
  
 **[Default Lock Escalation]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースが、ロックのエスカレートを試行する前に取得するデータベース ロックの数を指定します。  
  
 **[Default Lock Timeout]**  
 トランザクションがロックを待機する既定の間隔を、ミリ秒単位で指定します。  
  
 **[Flush Interval]**  
 トランザクションがコミットされてから、ディスクにフラッシュされるまでの間隔を秒単位で指定します。  
  
 **[Locale Identifier]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースのロケール ID (LCID) を指定します。  
  
 **[Max Buffer Size]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact が、データをディスクにフラッシュするまでに使用する最大メモリ容量を KB 単位で指定します。  
  
 **[Max Database Size]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースの最大サイズを MB 単位で指定します。  
  
 **モード**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースを開くファイル モードを指定します。 このプロパティの既定値は **[Read Write]** です。  
  
 [Mode] オプションには、次の表に示すように 4 つの値が用意されています。  
  
|値|説明|  
|-----------|-----------------|  
|**読み取り専用**|データベースに対する読み取り専用アクセスを指定します。|  
|**[Read Write]**|データベースに対する読み取り/書き込み権限を指定します。|  
|**[排他]**|データベースに対する排他アクセスを指定します。|  
|**[Shared Read]**|他のユーザーがデータベースからの読み取りを同時に行うことができることを指定します。|  
  
 **Persist Security Info**  
 セキュリティ情報を接続文字列の一部として返すかどうかを指定します。 このオプションの既定値は **[False]** です。  
  
 **[Temp File Directory]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 一時データベース ファイルの場所を指定します。  
  
 **データ ソース**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースの名前を指定します。  
  
 **パスワード**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースのパスワードを入力します。  
  
