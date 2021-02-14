---
title: レポート ビューアー コントロール バージョンのサポート
description: Microsoft Report Viewer コントロールは、最新のサポート ライフサイクル ポリシーに従う、SQL Server Reporting Services と Power BI Report Server に対応しています。
author: maggiesMSFT
ms.custom: seo-lt-2019
ms.author: maggies
ms.reviewer: jonhp
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 12/01/2020
ms.openlocfilehash: fac7ebfc88432ef3bd8abde6c0e4e62115311520
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100015642"
---
# <a name="support-for-report-viewer-current-branch-versions"></a>レポート ビューアー Current Branch のサポート

**_適用対象: Microsoft Report Viewer バージョン 150.900.148 以降_**

**Microsoft Report Viewer コントロール** は、Microsoft の最新 [サポート ライフサイクル ポリシー](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)に従う、SQL Server Reporting Services と Power BI Report Server に対応しています。 この情報は、[NuGet](https://www.nuget.org/) 経由で配布される **ASP.NET** バージョンと **WinForms** バージョンの両方に該当します。 リリース済みのバージョンはすべて [NuGet](https://www.nuget.org/) で入手できます。 パッチ、機能、その他の更新プログラムは最新版にロールフォワードされます。 最高を受け取るには最新版を適用する必要があります。 レポート ビューアーは **セキュリティ更新プログラムと重要な更新プログラム** を引き続き受信します。サポート ポリシーに変更がある場合、少なくとも 1 年前に通知されます。

レポート ビューアー コントロールのバージョン履歴は次のリンク先でご確認いただけます。

- [Windows フォーム](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/)
- [ASP.NET Web フォーム](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/)

## <a name="application-server-and-report-server-combinations"></a>アプリケーション サーバーとレポート サーバーの組み合わせ

レポート ビューアー コントロールの一部の機能は、オペレーティング システムの既定の動作に依存しています。 そのため、クライアント (レポート ビューアー コントロールを実行しているアプリケーション サーバー) とサーバー (Reporting Services を実行している) の両方で同じバージョンを実行することが必要になる場合があります。 次のアプリケーション サーバーとレポート サーバーの組み合わせがサポートされています。

| アプリケーション サーバー | レポート サーバー |
| :----------------- | :------ |
| Windows Server 2012 | Windows Server 2012 |
| Windows Server 2012 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 |
| Windows Server 2016 以降 | Windows Server 2016 以降 |

## <a name="next-steps"></a>次の手順

レポート ビューアー コントロールの詳細については、[レポート ビューアー コントロールを使用して Reporting Services を統合する方法の概要](integrating-reporting-services-using-reportviewer-controls-get-started.md)に関する記事を参照してください。
