---
description: Odbc テストは odbc 対応のアプリケーションであり、odbc ドライバーおよび ODBC ドライバーマネージャーのテストに使用できます。
title: ODBC のテスト
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288247"
---
# <a name="odbc-test"></a>ODBC のテスト

## <a name="about"></a>詳細

Microsoft® ODBC Test は odbc 対応のアプリケーションであり、odbc ドライバーおよび ODBC ドライバーマネージャーのテストに使用できます。 ODBC テストは、 [Microsoft Data Access Components (MDAC) 2.8 ソフトウェア開発キット](https://www.microsoft.com/download/details.aspx?id=21995)の一部として含まれています。

ODBC 3.51 には、ANSI と Unicode 対応の両方のバージョンの ODBC テストが含まれています。 対応するファイルは次のとおりです。

- `Odbcte32.exe` および `Gtrtst32.dll` (ANSI バージョンの場合)。

- `Odbct32w.exe` および `Gtrts32w.dll` (Unicode バージョンの場合)。

ODBC テストを使用するには、ODBC API、C 言語、および SQL を理解している必要があります。 ODBC API の詳細については、 [Odbc プログラマーズリファレンス](../odbc/reference/odbc-programmer-s-reference.md)を参照してください。

ドキュメントのこのセクションに以前含まれていたヘルプトピックが、ODBC テストプログラムに含まれるようになりました。 `Odbcte32.exe`またはを開き、[ `Odbct32w.exe` **ヘルプ**] メニューを開き、[**ヘルプトピック**] をクリックします。

64ビットの Microsoft Windows オペレーティングシステムを対象とするこれらのアプリケーションの64ビットバージョンは、個別のファイルであっても、32ビットバージョンと同じ名前になっていることに注意してください。 つまり、64ビットバージョンの ODBC テストの Unicode バージョンの `odbct32w.exe` 名前はです。

## <a name="open-source"></a>オープン ソース

ODBC テストはオープンソースです。 コードを表示し、最新バージョンの ODBC テストを自分でビルドするには、 [Odbc テスト用の GitHub リポジトリ](https://github.com/microsoft/ODBCTest)にアクセスしてください。
