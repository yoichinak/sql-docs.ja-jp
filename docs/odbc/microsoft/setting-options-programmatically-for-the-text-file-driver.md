---
description: テキスト ファイル ドライバーのプログラムでオプションの設定
title: テキストファイル Driver | のプログラムでオプションを設定するMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdc130904266dcdaedf84e826d4812aa6cfbb607
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483455"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>テキスト ファイル ドライバーのプログラムでオプションの設定

|オプション|説明|認証方法|  
|------------|-----------------|------------|  
|データ ソース名|給与や職員など、データソースを識別する名前。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**DSN**キーワードを使用します。|  
|形式の定義|[ **テキスト形式の定義** ] ダイアログボックスを表示し、データソースディレクトリ内の個々のテーブルのスキーマを指定できます。|このオプションは、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しによって動的に設定することはできません。|  
|説明|データソース内のデータの説明 (省略可能)。たとえば、"入社日、給与履歴、およびすべての従業員の現在のレビュー" などです。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**DESCRIPTION**キーワードを使用します。|  
|ディレクトリ|ターゲットディレクトリを選択します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|  
|拡張機能の一覧|データソース上のテキストファイルのファイル名拡張子を一覧表示します。 テキストドライバーが使用されている場合は、拡張子を持たない名前を指定して CREATE TABLE ステートメントを実行すると、拡張子のないファイルが作成されます。 他のドライバーは、拡張子が指定されていないときに、既定の拡張子を持つファイルを作成します。 拡張子 .txt を持つファイルを作成するには、拡張子を名前に含める必要があります。 拡張子のないファイルを [ **テキスト形式の定義** ] ダイアログボックスに表示するには、"*" を使用します。 拡張機能の一覧に追加する必要があります。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**EXTENSIONS**キーワードを使用します。|  
|[読み取り専用]|データベースを読み取り専用として指定します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**READONLY**キーワードを使用します。|  
|スキャンする行|各列のデータ型を決定するためにスキャンする行の数。 データ型は、見つかったデータの種類の最大数に基づいて決定されます。 列に対して推測されるデータ型と一致しないデータが検出されると、データ型は NULL 値として返されます。<br /><br /> テキストドライバーについては、スキャンする行の数として 1 ~ 32767 の数値を入力できます。ただし、この値は常に既定で25に設定されます。 (制限外の数値はエラーを返します)。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**MAXSCANROWS**キーワードを使用します。|  
|ディレクトリの選択|アクセスするファイルが格納されているディレクトリを選択できるダイアログボックスを表示します。<br /><br /> データソースディレクトリを定義するときは、最もよく使用されるファイルが置かれているディレクトリを指定します。 ODBC ドライバーでは、このディレクトリが既定のディレクトリとして使用されます。 頻繁に使用する場合は、他のファイルをこのディレクトリにコピーします。 または、次のようにディレクトリ名を指定して、SELECT ステートメント内のファイル名を修飾することもできます。 `SELECT * FROM C:\MYDIR\EMP`<br /><br /> または、 **SQLSetConnectOption** 関数を SQL_CURRENT_QUALIFIER オプションと共に使用して、新しい既定のディレクトリを指定することもできます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|
