---
title: Microsoft SQL Server 用 Drivers for PHP をダウンロードする
description: SQL Server や Azure SQL Database に接続する PHP アプリケーションを開発するには、Microsoft Drivers for PHP for SQL Server をダウンロードします。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24dfef1b33b2a61c0d82c07ce6306e0b0449b8f3
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680767"
---
# <a name="download-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft SQL Server 用 Drivers for PHP をダウンロードする

Microsoft Drivers for PHP for SQL Server を使用すると、PHP アプリケーション用に SQL Server を統合することができます。 このドライバーは、PHP スクリプト内から SQL Server データの読み取りと書き込みを可能にする PHP 拡張機能であり、 Azure SQL Database 内のデータおよび SQL Server 2005 以降のすべてのエディション (Express Edition を含む) 内のデータにアクセスするためのインターフェイスを備えています。 このドライバーは、PHP ストリームなどの PHP 機能を使用して、ラージ オブジェクトの読み取りと書き込みを行います。

Linux と macOS では、PECL を使用して PHP 用のドライバーを簡単にダウンロードしてインストールできます。 詳細については、[Linux および macOS のインストール チュートリアル](installation-tutorial-linux-mac.md)に関する記事を参照してください。 Linux および macOS で PHP 用のドライバーを手動でダウンロードしてインストールする必要がある場合は、GitHub リリース タグにこれらのプラットフォーム用のパッケージがあります。

## <a name="download"></a>ダウンロード

Microsoft Drivers 5.8 for PHP for SQL Server は、最新の一般提供 (GA) バージョンです。

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft Drivers for PHP for SQL Server (Windows) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2120362)**  
[GitHub リリース タグ v5.8.0 (こちらから Linux と macOS のパッケージが入手できます)](https://github.com/Microsoft/msphpsql/releases/tag/v5.8.0)

### <a name="version-information"></a>バージョン情報

- リリース番号:5.8.0
- リリース日:2019 年 1 月 31 日

フィードバックがある場合、Microsoft Drivers for PHP for SQL Server チームに連絡する最善の方法は、[GitHub リポジトリ](https://github.com/Microsoft/msphpsql/issues)で問題を報告することです。

## <a name="release-notes"></a>リリース ノート

このリリースの変更点の詳細については、[リリース ノート](release-notes-php-sql-driver.md)を参照してください。

## <a name="previous-releases"></a>以前のリリース

このページは、Microsoft Drivers for PHP の最新バージョンのみを対象としています。 以前のバージョンをダウンロードするには、[Microsoft Drivers for PHP for SQL Server の以前のリリース](release-notes-php-sql-driver.md#previous-releases)を参照してください。

## <a name="see-also"></a>関連項目

[Microsoft Drivers for PHP for SQL Server の概要](getting-started-with-the-php-sql-driver.md)  
[Microsoft SQL Server 用 Drivers for PHP のシステム要件](system-requirements-for-the-php-sql-driver.md)  
[SQL Server 用 Microsoft PHP Drivers のサポート マトリックス](microsoft-php-drivers-for-sql-server-support-matrix.md)  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](programming-guide-for-php-sql-driver.md)  
[SQLSRV ドライバー API リファレンス](sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV ドライバー API リファレンス](pdo-sqlsrv-driver-reference.md)  
