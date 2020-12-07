---
title: ODBC Driver for SQL Server on Windows のリリース ノート
description: このリリース ノート記事では、Windows 上の SQL Server 用 Microsoft ODBC ドライバーの各リリースにおける変更点について説明します。
ms.custom: ''
ms.date: 10/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-chojas
author: v-makouz
ms.author: v-chojas
manager: kenvh
ms.openlocfilehash: 6c19be21aebb6a8480fb51f396530e6843ac2861
ms.sourcegitcommit: 9e2c682929ee64c051dc62f8917d147861f7c635
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93043807"
---
# <a name="release-notes-for-microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows のリリース ノート

このリリース ノート記事では、Windows 上の SQL Server 用 Microsoft ODBC ドライバーの新機能について説明します。

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="176"></a>17.6

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2137027)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2137028)  

バージョン番号: 17.6.1.1  
リリース日:2020 年 7 月 31 日

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x40a)

| 追加された機能 | 詳細 |
| :------- | :------ |
| 準備されたステートメントのメタデータ キャッシュ | [Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページを参照してください。 |
| 自動 BEGIN TRANSACTION が ROLLBACK または COMMIT の後に行われるかどうかを制御する SQL_COPT_SS_AUTOBEGINTXN 接続属性 | [DSN および接続文字列の属性とキーワード](../dsn-connection-string-attribute.md)に関する記事を参照してください。 |
| バグが修正されました。 | [バグの修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>以前のリリース

## <a name="1752"></a>17.5.2

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120137)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120140)  

バージョン番号: 17.5.2.1  
リリース日:2020 年 3 月 6 日

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40a)  

### <a name="features-added-in-1752"></a>17.5.2 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Managed Identity for Azure Key Vault を使用した認証のサポート | [ODBC ドライバーでの Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページをご覧ください。 |
| その他の Azure Key Vault エンドポイントのサポート | [ODBC ドライバーでの Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページをご覧ください。 |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

以前のバージョンの ODBC ドライバーをダウンロードするには、次のセクションのダウンロード リンクをクリックします。

## <a name="175"></a>17.5

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120248)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120353)  

バージョン番号: 17.5.1.1  
リリース日:2020 年 1 月 31 日

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x40a)  

### <a name="features-added-in-175"></a>17.5 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| サーバーへのラウンド トリップなしで SPID を取得する SQL_COPT_SS_SPID 接続属性 | [DSN および接続文字列の属性とキーワード](../dsn-connection-string-attribute.md)に関する記事を参照してください。 |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="1742"></a>17.4.2

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120354)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120249)  

バージョン番号: 17.4.2.1  
リリース日:2019 年 10 月

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x40a)  

### <a name="features-added-in-1742"></a>17.4.2 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| その他の Azure Key Vault エンドポイントのサポート | [ODBC ドライバーでの Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページをご覧ください。 |
| データ分類バージョンの設定のサポート | 「[データ分類](../data-classification.md#bkmk-version)」を参照してください。 |
| Azure Active Directory 認証ライブラリ (adal.dll) をインストーラーに含める | 基本ドライバーのインストールに含まれるようになりました。これにより、ODBC インストーラーを使用すると、SQL Server 用の Microsoft Active Directory 認証ライブラリの既存のインストールがアップグレードされ、Windows のインストール済みアプリケーションの一覧からこれが削除されます。 |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="174"></a>17.4

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120149)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120150)  

バージョン番号: 17.4.1.1  
リリース日:2019 年 7 月

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x40a)  

### <a name="features-added-in-174"></a>17.4 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| セキュリティで保護されたエンクレーブが設定された Always Encrypted。 | [ODBC ドライバーでの Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページをご覧ください。 |
| 構成可能な TCP キープアライブ設定。 | 「[SQL Server への接続](../linux-mac/connection-string-keywords-and-data-source-names-dsns.md)」をご覧ください。 |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="173"></a>17.3

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120355)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120356)  

バージョン番号: 17.3.1.1  
リリース日:2019 年 2 月

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x40a)  

### <a name="features-added-in-173"></a>17.3 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Azure Active Directory マネージド ID (システムおよびユーザー割り当て) 認証モード。 | 「[ODBC ドライバーでの Azure Active Directory の使用](../using-azure-active-directory.md)」を参照してください。 |
| Always Encrypted 列に対して入力パラメーターをストリーム配信する機能。 | 「[Limitations of the ODBC driver when using Always Encrypted (Always Encrypted を使用するときの ODBC ドライバーの制限事項)](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)」をご覧ください。 |
| XA 分散トランザクション。 | 「[Using XA Transactions (XA トランザクションの使用)](../use-xa-with-dtc.md)」をご覧ください。 |
| 更新された Visual C++ 再頒布可能パッケージ | ランタイム依存関係を Visual C++ 2017 再頒布可能パッケージ ([x64 のダウンロード](https://aka.ms/vs/15/release/vc_redist.x64.exe)、[x86 のダウンロード](https://aka.ms/vs/15/release/vc_redist.x86.exe)) にアップグレードしました |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="172"></a>17.2

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120250)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120357)  

バージョン番号: 17.2.0.1  
リリース日:2018 年 7 月

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x40a)  

### <a name="features-added-in-172"></a>17.2 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Azure SQL Database と SQL Server のデータ分類。 | 「[データ分類](../data-classification.md)」を参照してください。 |
| UTF-8 サーバー エンコードのサポート。 | &nbsp; |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="171"></a>17.1

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120151)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120443)  

バージョン番号: 17.1.0.1  
リリース日:2018 年 3 月

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x40a)  

### <a name="features-added-in-171"></a>17.1 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| `SQL_COPT_SS_CEKCACHETTL` および `SQL_COPT_SS_TRUSTEDCMKPATHS` 接続属性のサポート。 | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>列暗号化キーのローカル キャッシュが存在する時間を制御したり、それをフラッシュしたりできます。<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>アプリケーションで、AE 操作が指定したリストの列マスター キーのみを使用するように制限できます。<br/><br/> 詳しくは、「[SQL Server 用 ODBC ドライバーと共に Always Encrypted を使用する](../using-always-encrypted-with-the-odbc-driver.md)」をご覧ください。 |
| Azure Active Directory 対話型認証のサポート | &nbsp; |
| バグが修正されました。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="170"></a>17.0

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120444)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120152)  

バージョン番号: 17.0.1.1  
リリース日:2018 年 2 月

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x40a)  

### <a name="features-added-in-170"></a>17.0 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| BCP API の Always Encrypted サポート。 | &nbsp; |
| 新しい接続文字列属性 `UseFMTOnly`。 | ドライバーは一時テーブルを必要とする特殊なケースで以前のメタデータを使用します。 |
| Azure SQL Managed Instance のサポート。 | 後の「[Managed Instance (ODBC バージョン 17) を使用するときの相違点](#diffs-managed-instance-17)」の一覧をご覧ください。 |
| &nbsp; | &nbsp; |

| 依存関係の変更 | 詳細 |
| :------------ | :------ |
| 削除された Microsoft オンライン サービス サインイン アシスタント | 依存関係が削除されました。 |
| &nbsp; | &nbsp; |

### <a name="differences-when-using-managed-instance-odbc-version-17"></a><a name="diffs-managed-instance-17"></a> Managed Instance (ODBC バージョン 17) を使用するときの相違点

このバージョンの ODBC には、Azure SQL Managed Instance のサポートが含まれています。 Managed Instance を使用するときは、以下で示す相違点の一覧をご覧ください。

> [!NOTE]
> Managed Instance を使用するときはいくつかの相違点があります。
>
> - FILESTREAM はサポートされていません。
> - ローカル ファイル システムのアクセスはサポートされていませんが、トレース ファイルなどの場合は必要です。
> - ローカル パスからの UDT の作成はサポートされていません。
> - Windows 統合認証はサポートされていません。
> - DTC はサポートされていません。
> - `sa` アカウントは存在しません (既定のアカウントは `cloudSA` と呼ばれます)。
> - TDS トークン エラー (0xAA) では、正しくないサーバー名が返されます。
> - データベース名の特殊文字はサポートされていません。
> - ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] はサポートされていません。
> - 言語設定に関係なく、エラー メッセージは常に英語で表示されます (Azure と同じ)。

## <a name="131"></a>13.1

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2121020)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120923)  

バージョン番号: 13.1  

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x40a)  

[Microsoft Command Line Utilities 13.1 for SQL Server をダウンロードする](https://www.microsoft.com/download/details.aspx?id=53591)

### <a name="features-added-in-131"></a>13.1 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、[Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md) および [Azure Active Directory](../using-azure-active-directory.md) のサポートが追加されています。 | これらの追加されたサポートは、Microsoft SQL Server 2016 以降のバージョンに接続するときに使用できます。 |
| Always Encrypted および Azure Active Directory のサポートに対応する接続プールのキーワードと属性があります。 | これらのキーワードと属性については、「[ODBC Driver for SQL Server のドライバー対応接続プール](driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)」で説明されています。 |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2121118)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2120924)  

バージョン番号: 13  

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x40a)  

[Microsoft Command Line Utilities 13 for SQL Server をダウンロードする](https://www.microsoft.com/download/details.aspx?id=52680)

### <a name="features-added-in-13"></a>13 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Microsoft SQL Server 2016 のサポートが追加されます。 | ODBC ドライバー バージョン 11 の機能が保持されます。 |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

![ダウンロード](../../../ssms/media/download-icon.png) [x64 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2121206)  
![ダウンロード](../../../ssms/media/download-icon.png) [x86 インストーラーのダウンロード](https://go.microsoft.com/fwlink/?linkid=2121021)  

バージョン番号: 11  

自動的に検出されたもの以外の言語でインストーラーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
X64 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x40a)  
X86 ドライバーの場合: [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x40a)  

[Microsoft Command Line Utilities 11 for SQL Server をダウンロードする](https://www.microsoft.com/download/details.aspx?id=36433)  

### <a name="features-added-in-11"></a>11 で追加された機能

| 追加された機能 | 詳細 |
| :------------ | :------ |
| 新しい機能が含まれます。 | 「[Microsoft ODBC Driver for SQL Server on Windows の機能](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)」をご覧ください。 |
| SQL Server 2012 Native Client の ODBC に付属するすべての機能が含まれています。 | &nbsp; |
| &nbsp; | &nbsp; |
