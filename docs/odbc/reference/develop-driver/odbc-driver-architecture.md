---
description: ODBC ドライバーのアーキテクチャ
title: ODBC ドライバーのアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1789d5799ed9eb15ace7ea263d1a5804c8e86e74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476248"
---
# <a name="odbc-driver-architecture"></a>ODBC ドライバーのアーキテクチャ
ドライバーの作成者は、アプリケーションで DBMS 固有の SQL を使用できるかどうかについて、ドライバーのアーキテクチャが影響を受ける可能性があることに注意する必要があります。  
  
 ![ODBC ドライバーのアーキテクチャ](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "Odbcdriverのすべてのアーキテクチャ")  
  
 [ファイルベースのドライバー](../../../odbc/reference/file-based-drivers.md)  
  
 ドライバーが物理データに直接アクセスすると、ドライバーはドライバーとデータソースの両方として機能します。 ドライバーは、ODBC 呼び出しと SQL ステートメントの両方を処理する必要があります。 ファイルベースのドライバーの開発者は、独自のデータベースエンジンを作成する必要があります。  
  
 [DBMS ベースのドライバー](../../../odbc/reference/dbms-based-drivers.md)  
  
 別のデータベースエンジンを使用して物理データにアクセスする場合、ドライバーは ODBC 呼び出しのみを処理します。 処理のために SQL ステートメントをデータベースエンジンに渡します。  
  
 [ネットワークアーキテクチャ](../../../odbc/reference/network-example.md)  
  
 ファイルと DBMS の ODBC 構成は、1つのネットワーク上に存在できます。  
  
 [その他のドライバーのアーキテクチャ](../../../odbc/reference/other-driver-architectures.md)  
  
 ドライバーがさまざまなデータソースを操作する必要がある場合は、ミドルウェアとして使用できます。 異種結合エンジンのアーキテクチャにより、ドライバーがドライバーマネージャーとして表示されるようになります。 また、ドライバーをサーバーにインストールして、一連のクライアントで共有できるようにすることもできます。  
  
 ドライバーのアーキテクチャの詳細については、「 [ODBC アーキテクチャ](../../../odbc/reference/odbc-architecture.md)」の「[ドライバーマネージャー](../../../odbc/reference/the-driver-manager.md)と[ドライバーのアーキテクチャ](../../../odbc/reference/driver-architecture.md)」を参照してください。  
  
 ドライバーの問題の詳細については、次の表に記載されている場所を参照してください。  
  
|問題|トピック|場所|  
|-----------|-----------|--------------|  
|アプリケーションとドライバーの互換性の問題|[アプリケーション/ドライバーの互換性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[プログラミングに関する考慮事項](../../../odbc/reference/develop-app/programming-considerations.md)(ODBC プログラマーリファレンス)|  
|ODBC ドライバーの記述|[ODBC 3.x ドライバーの作成](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[プログラミングに関する考慮事項](../../../odbc/reference/develop-app/programming-considerations.md)(ODBC プログラマーリファレンス)|  
|旧バージョンとの互換性のためのドライバーのガイドライン|[ドライバーの下位互換性のガイドライン](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|付録 G: ODBC プログラマーリファレンスにおける[旧バージョンとの互換性のためのドライバーガイドライン](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|  
|ドライバーへの接続|[データ ソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|ODBC プログラマーリファレンスの[データソースまたはドライバーに接続する](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|ドライバーの識別|[ドライバーの表示](../../../odbc/admin/viewing-drivers.md)|Microsoft ODBC データソースアドミニストレーターのオンラインヘルプの「[ドライバーの表示](../../../odbc/admin/viewing-drivers.md)」|  
|接続プールの有効化|[ODBC 接続プール](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|ODBC プログラマーリファレンスの[データソースまたはドライバーに接続する](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|Unicode/ANSI ドライバーと接続の問題|[Unicode ドライバー](../../../odbc/reference/develop-app/unicode-drivers.md)|[プログラミングに関する考慮事項](../../../odbc/reference/develop-app/programming-considerations.md)(ODBC プログラマーリファレンス)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
