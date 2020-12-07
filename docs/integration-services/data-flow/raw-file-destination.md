---
description: RAW ファイル変換先 (Raw File destination)
title: RAW ファイル変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 27b28672540d25fe84573c37004161992d3d3827
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194203"
---
# <a name="raw-file-destination"></a>RAW ファイル変換先 (Raw File destination)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  RAW ファイル変換先は、生データをファイルに書き込みます。 データは変換先に固有の形式であるため、データは変換の必要がなく、解析もほとんど必要ありません。 したがって、RAW ファイル変換先は、フラット ファイルや OLE DB 変換先などの他の変換先よりも、高速にデータを書き込むことができます。  
  
 RAW ファイル変換先を使用すると、RAW データをファイルに書き込むことに加え、パッケージを実行せずに、列のみを含む空の RAW ファイル (メタデータのみのファイル) を生成することができます。 以前に変換先によって書き込まれた RAW データを取得するには、RAW ファイル ソースを使用します。 RAW ファイル ソースの参照先を、メタデータのみのファイルにすることもできます。  
  
 RAW ファイルの形式には、並べ替えの情報が含まれています。 RAW ファイル変換先には、文字列の列の比較フラグを含む並べ替えの情報がすべて保存されます。 RAW ファイル ソースは、並べ替えの情報を読み取って受け入れます。 詳細エディターを使用して、ファイル内の並べ替えのフラグを無視するように RAW ファイル ソースを構成するためのオプションが用意されています。 比較フラグの詳細については、「 [文字列データの比較](../../integration-services/data-flow/comparing-string-data.md)」を参照してください。  
  
 RAW ファイル変換先は、次の方法で構成できます。  
  
-   RAW ファイル変換先がデータを書き込むファイルの名前、またはその名前が含まれている変数のどちらかのアクセス モードを指定します。  
  
-   RAW ファイル変換先によって、同じ名前の既存のファイルにデータを追加するか、新しいファイルを作成するかを指定します。  
  
 RAW ファイル変換先は、パッケージの実行間で、部分的に処理されたデータの中間結果を書き込むために使用される場合がよくあります。 生データを格納すると、RAW ファイル ソースによって迅速に読み取られたデータを、最終的な変換先に読み込む前に、さらに変換できます。 たとえば、パッケージを複数回実行し、そのたびに生データをファイルに書き込むことができます。 後で、別のパッケージが RAW ファイル ソースを使用して各ファイルからデータを読み取り、全体結合変換を使用してデータを 1 つのデータセットにマージし、次に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルなどの最後の変換先に読み込まれる前に、追加の変換を適用してデータを集約することができます。  
  
> [!NOTE]  
>  RAW ファイル変換先では、NULL データはサポートされていますが、バイナリ ラージ オブジェクト (BLOB) データはサポートされていません。  
  
> [!NOTE]  
>  RAW ファイル変換先は、接続マネージャーを使用しません。  
  
 この変換先は 1 つの標準入力をとります。 エラー出力はサポートされていません。  
  
## <a name="append-and-new-file-options"></a>データの追加および新しいファイルの作成オプション  
 WriteOption プロパティには、データを既存のファイルに追加する、または新しいファイルを作成するオプションが含まれています。  
  
 次の表では、WriteOption プロパティで使用できるオプションについて説明します。  
  
|オプション|説明|  
|------------|-----------------|  
|追加する|既存のファイルにデータを追加します。 追加するデータのメタデータは、ファイル形式と一致している必要があります。|  
|常に作成する|常に新しいファイルを作成します。|  
|1 回だけ作成する|新しいファイルを 1 つ作成します。 ファイルが存在する場合、コンポーネントは失敗します。|  
|切り捨てと追加|既存のファイルを切り捨て、データをそのファイルに書き込みます。 追加するデータのメタデータは、ファイル形式と一致している必要があります。|  
  
 データの追加に関する重要事項を次に示します。  
  
-   既存の RAW ファイルにデータを追加しても、データが再度並べ替えられることはありません。  
  
     並べ替えられるキーの順序が正しいことを確認する必要があります。  
  
-   既存の RAW ファイルにデータを追加しても、ファイルのメタデータ (並べ替えの情報) が変更されることはありません。  
  
 たとえば、パッケージは ProductKey (PK) を基準に並べ替えられたデータを読み取ります。 パッケージのデータ フローでは、既存の RAW ファイルにデータを追加します。 パッケージの初回実行時には、3 つの行 (PK 1000、1100、1200) を受け取ります。 RAW ファイルには次のデータが含まれています。  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 パッケージの 2 回目の実行時には、2 つの新しい行 (PK 1001、1300) を受け取ります。 RAW ファイルには次のデータが含まれています。  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 新しいデータは RAW ファイルの末尾に追加されるため、並べ替えられるキー (PK) の順序が正しくありません。 また、追加操作ではファイルのメタデータ (並べ替えの情報) が変更されませんでした。 RAW ファイル ソースを使用してファイルを読み取る場合、このコンポーネントは、ファイル内のデータの順序が正しくなくても PK を基準にファイルが並べ替えられることを示します。  
  
 データの追加中でも並べ替えられるキーの順序を正しく保つために、パッケージのデータ フローを次の手順で作成できます。  
  
1.  ソース A を使用して新しい行を取得します。  
  
2.  ソース B を使用して、RawFile1 から既存の行を取得します。  
  
3.  全体結合変換を使用して、ソース A とソース B からの入力を結合します。  
  
4.  PK を基準に並べ替えを行います。  
  
5.  RAW ファイル変換先を使用して RawFile2 に書き込みます。  
  
     データ フローにおいて、RawFile1 は読み取り元となるためロックされます。  
  
6.  RawFile1 を RawFile2 に置き換えます。  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>ループでの RAW ファイル変換先の使用  
 RAW ファイル変換先を使用するデータ フローがループ内にある場合、ファイルを 1 回だけ作成し、ループが繰り返されるたびにデータをそのファイルに追加することができます。 ファイルにデータを追加するには、追加するデータが既存のファイルの形式に一致している必要があります。  
  
 ループの最初の繰り返しでファイルを作成し、ループの以降の繰り返しで行を追加するには、デザイン時に次のことを行う必要があります。  
  
1.  WriteOption プロパティを **CreateOnce** または **CreateAlways** に設定し、ループの繰り返しを 1 回実行します。 ファイルが作成されます。 これにより、追加するデータのメタデータとファイルが必ず一致するようになります。  
  
2.  WriteOption プロパティを **Append** にリセットし、ValidateExternalMetadata プロパティを **False** に設定します。  
  
 **Append** オプションの代わりに **TruncateAppend** オプションを使用すると、以前の実行で追加された行が切り捨てられ、新しい行が追加されます。 また **TruncateAppend** オプションを使用するには、データがファイル形式に一致している必要があります。  
  
## <a name="configuration-of-the-raw-file-destination"></a>RAW ファイル変換先の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
-   [RAW ファイルのカスタム プロパティ](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 sqlservercentral.com のブログ「 [RAW ファイルは最高](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)」  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>[RAW ファイル変換先エディター] ([接続マネージャー] ページ)
  ファイルに RAW データを書き込むための RAW ファイル変換先を構成するには、RAW ファイル変換先エディターを使用します。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [RAW ファイル変換先エディターを開く](#open)  
  
-   [[接続マネージャー] タブのオプションの設定](#connection)  
  
-   [[列] タブのオプションの設定](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> RAW ファイル変換先エディターを開く  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]パッケージに RAW ファイル変換先を追加します。  
  
2.  コンポーネントを右クリックし、 **[編集]** をクリックします。  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> [接続マネージャー] タブのオプションの設定  
 **アクセス モード**  
 ファイル名の指定方法を選択します。 ファイル名とパスを直接入力するには **[ファイル名]** を選択します。ファイル名を含んでいる変数を指定するには、 **[変数からのファイル名]** を選択します。  
  
 **[ファイル名]** または **[変数名]**  
 RAW ファイルの名前とパスを入力するか、またはファイル名を含んでいる変数を選択します。  
  
 **[書き込みオプション]**  
 ファイルの作成およびファイルへの書き込みに使用するメソッドを選択します。  
  
 **[初期 RAW ファイルの生成]**  
 パッケージを実行せずに、列のみを含む空の RAW ファイル (メタデータのみのファイル) を生成するには、このボタンをクリックします。 ファイルには、 **[RAW ファイル変換先エディター]** の **[列]** ページで選択した列が含まれています。 RAW ファイル ソースの参照先を、このメタデータのみのファイルにすることができます。  
  
 **[初期 RAW ファイルの生成]** をクリックすると、メッセージ ボックスが表示されます。 ファイルの作成を続行するには、 **[OK]** をクリックします。 **[列]** ページで別の列の一覧を選択するには、 **[キャンセル]** をクリックします。  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> [列] タブのオプションの設定  
 **使用できる入力列**  
 RAW ファイルに書き込む 1 つ以上の入力列を選択します。  
  
 **入力列**  
 **[使用できる入力列]** から選択した場合、このテーブルに入力列が自動的に追加されます。入力列をこのテーブルで直接選択することもできます。  
  
 **[出力の別名]**  
 出力列に使用する代替名を指定します。  
  
## <a name="raw-file-destination-editor-columns-page"></a>[Raw ファイル変換先エディター] ([列] ページ)
  ファイルに RAW データを書き込むための RAW ファイル変換先を構成するには、RAW ファイル変換先エディターを使用します。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [RAW ファイル変換先エディターを開く](#open)  
  
-   [[接続マネージャー] タブのオプションの設定](#connection)  
  
-   [[列] タブのオプションの設定](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> RAW ファイル変換先エディターを開く  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]パッケージに RAW ファイル変換先を追加します。  
  
2.  コンポーネントを右クリックし、 **[編集]** をクリックします。  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> [接続マネージャー] タブのオプションの設定  
 **アクセス モード**  
 ファイル名の指定方法を選択します。 ファイル名とパスを直接入力するには **[ファイル名]** を選択します。ファイル名を含んでいる変数を指定するには、 **[変数からのファイル名]** を選択します。  
  
 **[ファイル名]** または **[変数名]**  
 RAW ファイルの名前とパスを入力するか、またはファイル名を含んでいる変数を選択します。  
  
 **[書き込みオプション]**  
 ファイルの作成およびファイルへの書き込みに使用するメソッドを選択します。  
  
 **[初期 RAW ファイルの生成]**  
 パッケージを実行せずに、列のみを含む空の RAW ファイル (メタデータのみのファイル) を生成するには、このボタンをクリックします。 RAW ファイル ソースの参照先を、メタデータのみのファイルにすることができます。  
  
 このボタンをクリックすると、列の一覧が表示されます。 [キャンセル] をクリックして列を変更するか、[OK] をクリックしてファイルの作成を続行することができます。  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> [列] タブのオプションの設定  
 **使用できる入力列**  
 RAW ファイルに書き込む 1 つ以上の入力列を選択します。  
  
 **入力列**  
 **[使用できる入力列]** から選択した場合、このテーブルに入力列が自動的に追加されます。入力列をこのテーブルで直接選択することもできます。  
  
 **[出力の別名]**  
 出力列に使用する代替名を指定します。  
  
## <a name="see-also"></a>参照  
 [RAW ファイル ソース](../../integration-services/data-flow/raw-file-source.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
