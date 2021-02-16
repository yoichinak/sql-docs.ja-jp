---
title: 仮想デバイス インターフェイス リファレンス
titlesuffix: SQL Server VDI reference
description: この記事では、SQL Server バックアップの仮想デバイス インターフェイス リファレンスの概要について説明します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 9e4e415ec768344208f7f9c2573ce0ad9a910135
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341750"
---
# <a name="virtual-device-interface-vdi-reference"></a>仮想デバイス インターフェイス (VDI) リファレンス

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

このセクションには、サードパーティのバックアップ ソフトウェア ベンダーが使用するための SQL Server アプリケーション プログラミング インターフェイスの仕様が含まれています。

## <a name="overview"></a>概要

仮想デバイス インターフェイス (VDI) は、パフォーマンスの低下を最小限に抑えて、トランザクション ワークロードに最高のオンライン バックアップ スループットを提供するだけでなく、可能な限り最速の復元時間を実現します。 これによりサードパーティ ベンダーは、SQL Server ネイティブのバックアップ/復元と同じパフォーマンス特性を実現し、すべてのバックアップ/復元機能を使用できるようになります。 VDI は SQL Server 7.0 で導入され、以降のバージョンでサポートおよび拡張されています。

VDI では、主に次の 2 種類のバックアップ テクノロジがサポートされています。

- バックアップ セットのコンテンツ全体が読み取られ、バックアップ メディアに転送される、従来のオンライン バックアップ。

- 基になる分割ミラーまたは書き込み時コピー テクノロジを使用したスナップショット バックアップ。

VDI によって実行される従来のオンライン バックアップでは、SQL Server でのバックアップと復元のあらゆる機能を利用できます。 スナップショット バックアップは、完全なデータベースとファイル/ファイルグループのバックアップのみに制限されます。 ただし、スナップショット バックアップでは、従来のデータベース差分バックアップ、ファイル差分バックアップ、およびトランザクション ログ バックアップを使用してロール フォワードすることができる場合があります。

## <a name="next-steps"></a>次のステップ

このセクションの VDI リファレンス ドキュメントを確認します。

完全な仕様とサポート ソース ファイルをダウンロードします。

[SQL Server 2005 Virtual Backup Device Interface (VDI) の仕様](https://www.microsoft.com/download/details.aspx?id=17282)