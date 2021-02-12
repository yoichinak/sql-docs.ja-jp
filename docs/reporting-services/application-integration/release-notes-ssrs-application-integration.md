---
title: レポート ビューアー コントロールのリリース ノート
description: Reporting Services に関連する WebForms および WinForms のレポート ビューアー コントロールのリリース ノート。
ms.date: 11/30/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: b6d1c768bb933036d3b23d37be20974515896a3b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100068157"
---
# <a name="release-notes-for-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS の WebForms および WinForms のレポート ビューアー コントロールのリリース ノート

これらは、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) に関連する WebForms および WinForms のレポート ビューアー コントロールのリリース ノートです。

SSRS のリリース ノートについては、「[SQL Server Reporting Services (SSRS) 2017 以降のリリース ノート](../release-notes-reporting-services.md)」を参照してください。

## <a name="15014270"></a>150.1427.0
| 変更の説明 | 詳細 |
| :----------------- | :------ |
| バグの修正 | クリック後にリンクが表示済みとして表示されない問題を修正しました。 |
|           | 特定のロケールに影響する datetime 解析に関する問題を修正しました。 |
| &nbsp; | &nbsp; |

## <a name="15014040"></a>150.1404.0
| 変更の説明 | 詳細 |
| :----------------- | :------ |
| バグの修正 | WebForms のツール バーのタブ オーダーに関する問題を修正しました。 |
|           | テーブルの HTML 表示のアクセシビリティが向上しました。 |
| &nbsp; | &nbsp; |

## <a name="15014000"></a>150.1400.0
| 変更の説明 | 詳細 |
| :----------------- | :------ |
| バグの修正 | ビューアー コントロールがデザイン モードで読み込まれない問題を修正しました。 |
| &nbsp; | &nbsp; |

## <a name="15013580"></a>150.1358.0
| 変更の説明 | 詳細 |
| :----------------- | :------ |
| バグの修正 | プロジェクト参照から Microsoft.ReportViewer.Design アセンブリを削除した変更を元に戻しました。 |
|           | その他の変更の一環で 2 つのアセンブリはバージョン 15.0 から 15.3 に変更されていました。 これは元に戻されました。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 変更の説明 | 詳細 |
| :----------------- | :------ |
| バグの修正  | 高 DPI モニターの適切な印刷プレビュー |
|            | [印刷] ダイアログが表示領域の外側に表示されていました |
|            | パラメーターが多数あると、パラメーター スクロール バーとドロップダウン リストが正常に動作しなくなりました |
|            | Null と日時のパラメーターに関する問題を修正しました |
|            | JQuery をバージョン 3.3.1 に更新しました |
|            | HTML レンダリングで tablix セルとの重なりを修正しました |
|            | 不適切な VS アセンブリがプロジェクトに追加されないように、設計時のプロジェクト参照を削除しました |
|            | アクティブなアイテムに対してのみナレーションを行うようにツール バーのアクセシビリティを修正しました |
| &nbsp; | &nbsp; |

## <a name="150900148"></a>150.900.148

| 変更の説明 | 詳細 |
| :----------------- | :------ |
| パラメーターのないレポートが **Server.LoadReportDefinition** によって読み込まれないバグが修正されています。 | &nbsp; |
| WebForms レポート ビューアー コントロール。 | RTL ページ (*direction: rtl;* css を使用してテキスト フローをを変更するページ) への埋め込みがサポートされました。<br/><br/>*IReportViewerMessages5* ローカリゼーション インターフェイスを使用した、印刷ダイアログ テキストのカスタマイズがサポートされました。<br/><br/>ユーザー補助のサポートが改善されました。<br/><br/>&bull; &nbsp; &nbsp; [WebForms のレポート ビューアー コントロール用の NuGet パッケージ](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms レポート ビューアー コントロール。 | アプリが高 DPI モードで実行されている場合の印刷機能が修正されました。<br/><br/>&bull; &nbsp; &nbsp; [WinForms のレポート ビューアー コントロール用の NuGet パッケージ](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>次のステップ

レポート ビューアー コントロールの[概要](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

その他の質問 [Reporting Services のフォーラムをお試しください](https://go.microsoft.com/fwlink/?LinkId=620231)。
