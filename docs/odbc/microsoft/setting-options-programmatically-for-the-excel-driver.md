---
description: Excel ドライバーのプログラムでオプションの設定
title: Excel Driver のプログラムによるオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97a17a0967581f4097b5030adb803a69c6a82f80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449254"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Excel ドライバーのプログラムでオプションの設定

|オプション|説明|認証方法|  
|------------|-----------------|------------|  
|データ ソース名|給与や職員など、データソースを識別する名前。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**DSN**キーワードを使用します。|  
|データベース|Microsoft Access データソースは、データベースを選択または作成せずに設定できます。 セットアップ時にデータベースが指定されていない場合、データソースへの接続時にデータベースファイルを選択するように求めるメッセージがユーザーに表示されます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**dbq**キーワードを使用します。|  
|説明|データソース内のデータの説明 (省略可能)。たとえば、"入社日、給与履歴、およびすべての従業員の現在のレビュー" などです。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**DESCRIPTION**キーワードを使用します。|  
|ディレクトリ|現在選択されているディレクトリが表示されます。<br /><br /> Microsoft Excel 3.0/4.0 ファイルの場合、パスの表示には "Directory" というラベルが付きますが、Microsoft Excel 5.0、7.0、または97ファイルの場合は、パスの表示に "Workbook" というラベルが付きます。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|  
|[読み取り専用]|データベースを読み取り専用として指定します。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**READONLY**キーワードを使用します。|  
|スキャンする行|各列のデータ型を決定するためにスキャンする行の数。 データ型は、見つかったデータの種類の最大数に基づいて決定されます。 列に対して推測されるデータ型と一致しないデータが検出されると、データ型は NULL 値として返されます。<br /><br /> Microsoft Excel ドライバーでは、スキャンする行の数を 1 ~ 16 の数値で入力できます。 既定値は8です。0に設定されている場合は、すべての行がスキャンされます。 (制限外の数値はエラーを返します)。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**MAXSCANROWS**キーワードを使用します。|  
|ディレクトリの選択|アクセスするファイルが格納されているディレクトリを選択できるダイアログボックスを表示します。<br /><br /> データソースディレクトリを定義する場合 (Microsoft Access を除くすべてのドライバー用)、最も一般的に使用されるファイルが置かれているディレクトリを指定します。 ODBC ドライバーでは、このディレクトリが既定のディレクトリとして使用されます。 頻繁に使用する場合は、他のファイルをこのディレクトリにコピーします。 または、次のようにディレクトリ名を指定して、SELECT ステートメント内のファイル名を修飾することもできます。<br /><br /> \*C:\MYDIR\EMP から選択<br /><br /> または、 **SQLSetConnectOption** 関数を SQL_CURRENT_QUALIFIER オプションと共に使用して、新しい既定のディレクトリを指定することもできます。<br /><br /> Microsoft Excel 3.0 または4.0 ファイルの場合、パスの表示には "ディレクトリ" と表示され、パスの選択ボタンは "ディレクトリを選択する" というラベルが付いています。 Microsoft Excel 5.0、7.0、または97ファイルの場合、パスの表示には "ブック" と表示され、パスの選択ボタンは "Select Workbook" というラベルが付いています。 データソースディレクトリを定義するときは、microsoft excel 3.0/4.0 の microsoft Excel ファイルが最もよく使用されているディレクトリを指定します。または、Microsoft Excel 5.0、7.0、または97のブックファイルが置かれているディレクトリを指定します。 Microsoft Excel 5.0、7.0、および97で**現在のディレクトリを使用する**ことはできません。|このオプションを動的に設定するには、 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)への呼び出しで**DEFAULTDIR**キーワードを使用します。|
