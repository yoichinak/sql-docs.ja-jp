---
title: Reporting Services のリリース ノート (2017 以降) | Microsoft Docs
description: バージョン 2017 以降の SQL Server Reporting Services (SSRS) での変更点の詳細について説明します。
ms.date: 10/11/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maggies
author: casualoak
ms.author: rhys
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: a20939e77c29566c890450d828cff441366c6f00
ms.sourcegitcommit: dc3ea1696b8a4332934568439aed6cce4e9737eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244664"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 以降のリリース ノート

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

この記事では、[!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) のバージョン 2017 以降の変更点について説明します。

レポート ビューアー コントロールのリリース ノートについては、「[SSRS のWebForms および WinForms のレポート ビューアー コントロールのリリースノート](application-integration/release-notes-ssrs-application-integration.md)」を参照してください。

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->
## <a name="sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services

## <a name="15075454810-20200831"></a>15.0.7545.4810、2020 年 8 月 31 日 
" *(製品バージョン: 15.0.1102.861)* "

| 修正された問題 | 詳細 |
| :---------- | :------ |
| セキュリティ更新プログラム  | &nbsp; |
| PDF ドキュメントを許可しないようにコメントの添付ファイルのサポートを制限  | &nbsp; |
| 名前にピリオドを含むレポートをエクスポートするときのファイル名の切り捨てを修正  | &nbsp; |
| 無効な日付形式のエラーが発生するサブスクリプションと zh-TW カルチャに関連する問題を修正  | &nbsp; |
| 特定のレポートでパラメーター オプションにアクセスすると値が不定になるという問題を修正  | &nbsp; |
| レポート名の一重引用符に関連する問題を修正  | &nbsp; |
| URL アクセスの FindString で一致が見つからないという問題を修正  | &nbsp; |
| PDF エクスポートの代替テキストがマルチバイト文字に対して正しくエンコードされないという問題を修正  | &nbsp; |
| 線形要素の下にある空の画像が不必要に表示される問題を修正  | &nbsp; |
| Web Edition でカスタム認証に対して誤って表示される未サポート エラーを修正  | &nbsp; |
| スクリーン リーダーが Tablix 内の余分な行と余分な列を読み取っていた問題を修正  | &nbsp; |
| ページ全体にズームしたときにサイズに合わせて画像が切り捨てられていた問題を修正  | &nbsp; |
| コマンド ラインのアップグレードで EULA フラグが不要になった  | &nbsp; |

## <a name="150724337714-20191101"></a>15.0.7243.37714、2019/11/01
" *(製品バージョン: 15.0.1102.675)* "

最初のリリース。


## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services

## <a name="1406001669-20200831"></a>14.0.600.1669、2020 年 8 月 31 日 

| 修正された問題 | 詳細 |
| :---------- | :------ |
| セキュリティ更新プログラム  | &nbsp; |
| PDF ドキュメントを許可しないようにコメントの添付ファイルのサポートを制限  | &nbsp; |
| 名前にピリオドを含むレポートをエクスポートするときのファイル名の切り捨てを修正  | &nbsp; |
| 無効な日付形式のエラーが発生するサブスクリプションと zh-TW カルチャに関連する問題を修正  | &nbsp; |

## <a name="1406001572-20200406"></a>14.0.600.1572、2020/04/06 

| 修正された問題 | 詳細 |
| :---------- | :------ |
| JQuery UI を 1.12 に更新  | &nbsp; |
| URL の大文字と小文字の区別を修正  | &nbsp; |
| パラメーターが多数ある場合のパラメーターの配置を修正  | &nbsp; |
| HTML5 レンダリングで機能しない FindString を修正  | &nbsp; |
| Analysis Services クライアント ライブラリを TLS 1.0/1.1 の非推奨に対応するように更新 | &nbsp; |

## <a name="1406001451-20191113"></a>14.0.600.1451、2019/11/13 

| 修正された問題 | 詳細 |
| :---------- | :------ |
| セキュリティ更新プログラム | &nbsp; |
| スナップショットが有効になっていると、ページ分割されたレポートがフィルター パラメーターで正しく機能しない  | &nbsp; |
| 閲覧者ロールと既定の設定を持つユーザーに、Excel ファイルをダウンロードするためのアクセス許可がない  | &nbsp; |
| SQL Server 2016 Reporting Services から Power BI Report Server へのアップグレードが、アップグレード中に失敗する | &nbsp; |
| SQL Server 2012 Reporting Services からアップグレードすると、"メール ヘッダーに無効な文字が見つかりました: ', '" というメッセージが表示され、サブスクリプションが失敗する | &nbsp; |
| 構成ツールの [データベース] セクションでモーダル ウィンドウをキャンセルすると、Reporting Services サービスが再起動される | &nbsp; |
| テキスト ボックス コントロールの BorderStyle プロパティ式が Excel 形式にレンダリングされない  | &nbsp; |
| 特定のレポートが途中で停止し、同じページが表示されたままレポートの最後のページまで到達しなくなることがある改ページの問題 | &nbsp; |

## <a name="1406001274-20190701"></a>14.0.600.1274、2019/07/01

| 修正された問題 | 詳細 |
| :---------- | :------ |
| セキュリティ更新プログラム | &nbsp; |
| 毎週の共有スケジュールを作成するときに平日を選択できない | &nbsp; |
| 復帰が Word 形式で正しくレポートに表示されない | &nbsp; |
| System Center Operations Manager (SCOM) 2019 が、最新の SSRS 2017 アップグレードで動作しない | &nbsp; |
| 共有データセットに対する承認拡張機能の呼び出し中にエラーが発生する | &nbsp; |
| SSRS 2017 および PBIRS でストアド プロシージャ GetAllProperties のロジックが変更されたことが原因で、Web サービス エンドポイントの ReportingService2010.GetProperties メソッドでリンク レポートのデータを取得できない | &nbsp; |
| グリッド内の項目をクリックすると、モバイル レポートの単純なグリッド行ヘッダーが表示されなくなる | &nbsp; |
| データ ドリブン サブスクリプション パラメーターで日付フィールドを使用できない | &nbsp; |
| SSRS 2016 以降の入れ子になった Tablix で、フォントが小さく表示されたり部分的に表示されたりする | &nbsp; |
| 異なるロケールを持つユーザーがサブスクリプションを編集すると、DateTime パラメーターが指定されたサブスクリプションがエラーになる | &nbsp; |
| Null 配信拡張機能を使用してデータ ドリブン サブスクリプションを作成すると、"配信エラーが発生しました" というメッセージが表示されて失敗する | &nbsp; |
| Excel および Word 形式で値を設定した場合、URL エンコードが正しくない | &nbsp; |

## <a name="1406001109-20190212"></a>14.0.600.1109、2019/02/12

| 修正された問題 | 詳細 |
| :---------- | :------ |
| キャッシュ レポート スナップショット スケジュールが、サブスクリプションの変更後に "レポート固有のスケジュール" に変更される。 | &nbsp; |
| Express エディションで rc:Toolbar=false が機能しない。 | &nbsp; |
| ページ分割されたレポートを PDF にエクスポートすると、タイ語の特定の文字が正しく表示されない。 | &nbsp; |
| 完成したデータ ドリブン サブスクリプションの通知中にデッドロックが発生する。 | &nbsp; |
| rc:Toolbar=False パラメーターを使用すると、特定の状況で埋め込み画像が表示されなくなる。 | &nbsp; |
| カスケード型パラメーターを使用するレポートに対して、データ ドリブン サブスクリプションを作成できない。 | &nbsp; |
| 無効な間隔で構成されているサブスクリプションを編集できない。 | &nbsp; |
| セキュリティ更新プログラム。 | &nbsp; |
| リンク レポートの UI が表示されない。 | &nbsp; |
| 入れ子になった tablix コントロールがあるページ分割されたレポートで、間違ったフォントが使用される。 | &nbsp; |
| tablix データ領域を含む、ページ分割された一部のレポートに、ホワイトスペースが間違って追加される。 | &nbsp; |
| モバイル レポートのシンプル データ グリッドを拡張すると、ヘッダー行が消える。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906、2018/09/12

次の問題が修正されています。

| 修正された問題 | 詳細 |
| :---------- | :------ |
| カスタム認証が正しい Cookie 情報を返さない。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892、2018/08/31

| 修正された問題 | 詳細 |
| :---------- | :------ |
| rc:Toolbar=False で、テキストが長い場合、四角形の内部にあるテキスト ボックスのために四角形が垂直方向に拡大しない。 | &nbsp; |
| pageHeight が 0.5 インチ未満の場合、テキストのサイズが拡大縮小しない。 | &nbsp; |
| SSRS カタログ データベースを CRM で使用すると、デッドロックが発生する。 | &nbsp; |
| レポートを下にスクロールするとき、垂直方向に整列された列見出しが正しく表示されない。 | &nbsp; |
| System Center Operations Manager レポート作成ロールに追加されたユーザーが、SSRS Web ポータルへのアクセスをブロックされる。 | &nbsp; |
| タイ語の文字が PDF に正しくエクスポートされない。 | &nbsp; |
| ブラウザーの役割の動作の変更。 | &nbsp; |
| Express エディションで rc:Toolbar=false が機能しない。 | &nbsp; |
| パラメーター プロンプト領域に垂直スクロール バーが表示されない。 | &nbsp; |
| 更新されたモバイル レポート ランタイム。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744、2018/04/25

| 修正された問題 | 詳細 |
| :---------- | :------ |
| 配信オプションを作成しても [データ ドリブン サブスクリプション] ページに表示されない。 | &nbsp; |
| SSRS 2012 を SSRS 2017 にアップグレードすると、RSManagement で数秒ごとに例外がスローされる。 | &nbsp; |
| IE11 で複数値のパラメーターの既定値を変更できない。 | &nbsp; |
| 共有スケジュールが実行されるたびにスケジュールが空になる。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689、2018/02/28

| 修正された問題 | 詳細 |
| :---------- | :------ |
| リンク レポートのレポート パラメーターの表示が、そのプロパティを編集すると元に戻る。 | &nbsp; |
| Express エディションで URL パラメーター rc:Toolbar=false が機能しない。 | &nbsp; |
| CanGrow プロパティが false に設定されたテキスト ボックスに式があると、値が表示されない。 | &nbsp; |
| セットアップ時のプロダクト キーに " _詳細情報_ " リンクが追加される。 | &nbsp; |
| カスタムのフォーム認証を使用した Web ポータルで、スライド式有効期限の Cookie が無視される。 | &nbsp; |
| 行のコンテンツが空の場合、Word にエクスポートすると行の高さが等しくならない。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594、2018/01/09

一部のセキュリティ更新プログラムが実装されました。

### <a name="140600490-20171101"></a>14.0.600.490、2017/11/01

SKU アップグレードに関する問題を解決しました。

## <a name="140600451-20170930"></a>14.0.600.451、2017/09/30

最初のリリース。

## <a name="next-steps"></a>次のステップ

[Reporting Services (SSRS) の新機能](what-s-new-in-sql-server-reporting-services-ssrs.md)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)。
