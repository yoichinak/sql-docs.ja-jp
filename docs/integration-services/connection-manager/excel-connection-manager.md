---
description: Excel 接続マネージャー
title: Excel 接続マネージャー | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa3a520812d2b28e67b5b863d4480d7d01afaa57
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130094"
---
# <a name="excel-connection-manager"></a>Excel 接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Excel 接続マネージャーを使用すると、パッケージは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ブック ファイルに接続できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる Excel ソースと Excel 変換先は、Excel 接続マネージャーを使用します。  
 
> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

 Excel 接続マネージャーをパッケージに追加するときに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、実行時に Excel 接続として解決される接続マネージャーを作成し、接続マネージャーのプロパティを設定して、接続マネージャーをパッケージの **Connections** コレクションに追加します。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **EXCEL** に設定されます。  
  
## <a name="configure-the-excel-connection-manager"></a>Excel 接続マネージャーの構成  
 Excel 接続マネージャーは、次の方法で構成できます。  
  
-   Excel ブック ファイルのパスを指定します。  
  
-   ファイルの作成に使用した Excel のバージョンを指定します。  
  
-   選択したワークシート内または範囲内の最初の行に、列名が格納されているかどうかを示します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「 [Excel 接続マネージャー]()」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="excel-connection-manager-editor"></a>Excel 接続マネージャー
  **[Excel 接続マネージャー]** ダイアログ ボックスを使用すると、既存または新規の [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ブック ファイルへの接続を追加できます。  
  
### <a name="options"></a>オプション  
 **[Excel ファイル パス]**  
 既存または新規の Excel ブック ファイルのパスおよびファイル名を入力します。  
   
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、Excel ファイルが存在するフォルダー、または新しいファイルを作成するフォルダーを指定します。  
  
 **[Excel バージョン]**  
 ファイルを作成するために使用した Microsoft Excel のバージョンを指定します。  
  
 **[先頭行に列名を含める]**  
 選択されているワークシートのデータの 1 行目に列名が含まれているかどうかを指定します。 このオプションの既定値は **[true]** です。  

## <a name="solution-to-import-data-with-mixed-data-types-from-excel"></a>データ型が混在しているデータを Excel からインポートするためのソリューション

既定でデータ型が混在するデータを使用する場合、Excel ドライバーでは最初の 8 行が読み取られます (**TypeGuessRows** レジスタ キーで設定される)。 Excel ドライバーでは、データの最初の 8 行に基づき、各列のデータ型が推測されます。 たとえば、Excel のデータ ソースで 1 列に数字とテキストが入っているとき、最初の 8 行が数字であれば、その最初の 8 行に基づき、その列のデータが整数型であるとドライバーでは判断される可能性があります。 その場合、SSIS では、テキスト値がスキップされ、NULL としてインポート先にインポートされます。

この問題を解決するには、次の解決策のいずれかをお試しいただけます。

* Excel ファイルで Excel 列の種類を **[テキスト]** に変更します。
* IMEX 拡張プロパティを接続文字列に追加し、ドライバーの既定動作をオーバーライドします。 ";IMEX=1" という拡張プロパティを接続文字列の終わりに追加すると、Excel ではデータがすべてテキストとして扱われます。 次の例を参照してください。
    
  ```ACE OLEDB connection string:
  Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\ExcelFileName.xlsx;Extended Properties="EXCEL 12.0 XML;HDR=YES;IMEX=1";
  ```

   この解決策で解決するには、場合によってはレジストリ設定も変更する必要があります。 main.cmd ファイルは次のようになります。
  
   ```cmd
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   ```

* ファイルを CSV 形式で保存し、CSV インポートをサポートするように SSIS パッケージを変更します。

## <a name="related-tasks"></a>Related Tasks  
[SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)  
[Excel ソース](../data-flow/excel-source.md)  
[Excel 変換先](../data-flow/excel-destination.md)