---
title: Power Pivot の接続の種類 | Microsoft Docs
description: データ ソースを構築する方法については、この記事の Power Pivot の接続の種類に関する情報を参照してください。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c83a33e56bca1cba9fab1c5e3ef873e9aa312f8a
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891732"
---
# <a name="power-pivot-connection-type-ssrs"></a>Power Pivot の接続の種類 (SSRS)
  SQL Server Analysis Services データ処理拡張機能を使用すると、SharePoint の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリーにパブリッシュされた [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックからデータを取得することができます。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、「 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ ソースは、SharePoint サイトの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリーにパブリッシュされている必要があります。  
  
 レポート ビルダーから [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックへの接続をサポートするには、ワークステーション コンピューターに SQL Server 2008 R2 ADOMD.NET が必要です。 このクライアント ライブラリは [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel と共にインストールされますが、このアプリケーションがインストールされていないコンピューターを使用する場合は、 [SQL Server 2008 R2 用 Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272)に関するページから ADOMD.NET をダウンロードしてインストールする必要があります。  
  
## <a name="data-source-type"></a>データ ソースの種類  
 使用するレポート データ ソースの種類は **Microsoft SQL Server Analysis Services**です。  
  
## <a name="connection-string"></a>接続文字列  
 接続文字列は、SharePoint の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリーまたはその他のライブラリにパブリッシュされた [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックの URL です (例: `https://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx`)。  
  
## <a name="credentials"></a>資格情報  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックおよび SharePoint サイトへのアクセスに必要な資格情報を指定します (Windows 認証 (統合セキュリティ) など)。 詳細については、「[データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」または「[レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
## <a name="queries"></a>クエリ  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ ソースに接続した後、MDX グラフィカル クエリを使用して、基となるデータ構造を参照および選択してクエリを作成します。 クエリを作成したら、それを実行して結果ペインにサンプル データを表示します。  
  
 クエリ デザイナーにより、クエリを分析してデータセット フィールドが決定されます。 また、 **レポート データ** ペインでデータセット フィールド コレクションを手動で編集することもできます。 詳細については、「[レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="filters"></a>フィルター  
 フィルター ペインで、クエリ結果から除外するか、クエリ結果に追加するディメンションおよびメンバーを指定します。  
  
## <a name="parameters"></a>パラメーター  
 フィルター ペインで、フィルターの **[パラメーター]** オプションを選択して、フィルターの選択に対応する使用可能な値を持つレポート パラメーターが自動的に作成されるようにします。  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリーの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックからレポート ビルダーを開いた場合、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックのピボットテーブル、ピボットグラフ、スライサー、およびその他のレイアウト機能や分析機能は、レポートで再作成されません。 代わりに、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブック内のデータを参照する、あらかじめ構成されたデータ ソースが空のレポートに含まれます。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックに基づくレポートをデザインする場合、レポートで再作成するスライサー、フィルター、およびテーブルやグラフの数によっては、手間と時間がかかることがあります。 そのため、レポートでのデータの表示方法については、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のデザインとは切り離して考えることをお勧めします。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブック内のデータは大幅に圧縮されていますが、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックから取得されたレポートのデータは圧縮されません。 クエリ デザイナーを使用してフィルターとパラメーターを指定し、レポートに必要なデータだけに制限します。  
  
 Analysis Services キューブへの接続とは異なり、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] モデルには階層はありません。 ブック内の関連するスライサーに同様の機能を提供するには、レポートでカスケード型パラメーターを作成する必要があります。 詳細については、「 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)で作成するモバイル レポートで使用できます。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] モデルの基になるデータ値に対応するように、式を調整しなければならない場合があります。 式を変更してデータを適切なデータ型に変換したり、集計関数を追加または削除したりすることが必要になります。 たとえば、データ型を文字列型から整数型に変換するには、 `=CInt`を使用します。 レポートをパブリッシュする前に、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] モデルのデータから意図した値が表示されることを必ず確認してください。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリーのレポートのプレビュー イメージは、以下の条件を満たしている場合にのみ生成されます。  
  
-   データを提供するレポートおよび [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックは、同じ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリーに一緒に保存する必要があります。  
  
-   レポートには、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ ソースからの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データのみが格納されます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services の MDX クエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](/previous-versions/sql/)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
