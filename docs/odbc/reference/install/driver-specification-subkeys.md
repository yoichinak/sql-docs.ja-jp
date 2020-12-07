---
description: ドライバーの仕様のサブキー
title: ドライバーの仕様のサブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a363335931723e33a6461b86395494153491d328
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499785"
---
# <a name="driver-specification-subkeys"></a>ドライバーの仕様のサブキー
ODBC ドライバーのサブキーに記載されている各ドライバーには、独自のサブキーがあります。 このサブキーには、ODBC ドライバーのサブキーの下にある対応する値と同じ名前が付けられています。 このサブキーの下の値には、ドライバーとドライバーのセットアップ Dll の完全なパス、 **Sqldrivers**によって返されるドライバーのキーワードの値、および使用状況の数が一覧表示されます。 値の形式を次の表に示します。  
  
|名前|データ型|データ|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**n**} {**y**&#124;**n**} {**y**&#124;**n**}|  
|CreateDSN|REG_SZ|*ドライバー-説明*|  
|ドライバー|REG_SZ|*ドライバー-DLL パス*|  
|DriverODBCVer|REG_SZ|*nn. nn*|  
|FileExtns|REG_SZ|**\*.** *extension1*[**, \* 。** *ファイル-extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|設定|REG_SZ|*setup.exe-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 次の表は、各キーワードの使用方法を示しています。  
  
|Keyword|使用法|  
|-------------|-----------|  
|**APILevel**|ドライバーでサポートされている ODBC インターフェイスの準拠レベルを示す数値:<br /><br /> 0 = なし<br /><br /> 1 = レベル1がサポートされています<br /><br /> 2 = サポートされているレベル2<br /><br /> これは、 **SQLGetInfo**の SQL_ODBC_INTERFACE_CONFORMANCE オプションに対して返される値と同じである必要があります。|  
|**CreateDSN**|ドライバーのインストール時に作成される1つまたは複数のデータソースの名前。 システム情報には、 **Createdsn** キーワードを使用して一覧表示されたデータソースごとに1つのデータソース仕様セクションが含まれている必要があります。 これらのセクションには driver **キーワードを** 含めないでください。ドライバーの仕様セクションで指定されていますが、ダイアログボックスを表示せずにデータソースの仕様を作成するには、ドライバーセットアップ DLL の **configdsn** 関数に十分な情報を含める必要があります。 データソース仕様セクションの形式については、「 [データソースの指定サブキー](../../../odbc/reference/install/data-source-specification-subkeys.md)」を参照してください。|  
|**ConnectFunctions**|ドライバーが **SQLConnect**、 **SQLDriverConnect**、および **SQLBrowseConnect**をサポートしているかどうかを示す3文字の文字列。 ドライバーが **SQLConnect**をサポートしている場合、最初の文字は "Y" です。それ以外の場合は、"N" になります。 ドライバーが **SQLDriverConnect**をサポートしている場合、2番目の文字は "Y" です。それ以外の場合は、"N" になります。 ドライバーが **SQLBrowseConnect**をサポートしている場合、3番目の文字は "Y" です。それ以外の場合は、"N" になります。 たとえば、ドライバーが **SQLConnect** と **SQLDriverConnect** をサポートしていても、 **SQLBrowseConnect**をサポートしていない場合、3文字の文字列は "yyn" になります。|  
|**DriverODBCVer**|ドライバーがサポートしている ODBC のバージョンを含む文字列。 バージョンは *nn. nn*という形式です。最初の2桁はメジャーバージョンで、次の2桁はマイナーバージョンです。 このマニュアルで説明されている ODBC のバージョンでは、ドライバーは "03.00" を返す必要があります。<br /><br /> これは、 **SQLGetInfo**の SQL_DRIVER_ODBC_VER オプションに対して返される値と同じである必要があります。|  
|**FileExtns**|ファイルベースのドライバーの場合、ドライバーが使用できるファイルの拡張子のコンマ区切りの一覧。 たとえば、dBASE ドライバーでは、.dbf を指定し、フォーマットされ \* たテキストファイルドライバーで \* .txt、.csv を指定することができます。 \* アプリケーションがこの情報を使用する方法の例については、「 **Fileusage** キーワード」を参照してください。|  
|**FileUsage**|ファイルベースのドライバーがデータソース内のファイルを直接どのように扱うかを示す数値。<br /><br /> 0 = ドライバーはファイルベースのドライバーではありません。 たとえば、ORACLE ドライバーは DBMS ベースのドライバーです。<br /><br /> 1 = ファイルベースのドライバーは、データソース内のファイルをテーブルとして扱います。 たとえば、Xbase ドライバーでは、各 Xbase ファイルがテーブルとして扱われます。<br /><br /> 2 = ファイルベースのドライバーは、データソース内のファイルをカタログとして扱います。 たとえば、Microsoft® Access ドライバーは、各 Microsoft Access ファイルを完全なデータベースとして扱います。<br /><br /> アプリケーションでこれを使用して、ユーザーがデータを選択する方法を決定する場合があります。 たとえば、Xbase や Paradox のユーザーは、多くの場合、データをファイルに格納していると考えていますが、ORACLE と Microsoft Access のユーザーは、データをテーブルに格納していると考えています。<br /><br /> ユーザーが [**ファイル**] メニューから **[データファイルを開く**] を選択すると、[ **Windows ファイルオープン**コモン] ダイアログボックスが表示されることがあります。 ファイルの種類の一覧では、 **Fileextns** キーワードで指定されたファイル拡張子を使用します。このドライバーでは、 **fileusage** 値が1で、"Y" が **connectfunctions** キーワードの値の2番目の文字として指定されています。 ユーザーがファイルを選択すると、アプリケーションは**DRIVER**キーワードを使用して**SQLDriverConnect**を呼び出し、 **SELECT \* FROM *table name* **ステートメントを実行します。<br /><br /> ユーザーが [**ファイル**] メニューから [**データのインポート**] を選択すると、 **fileusage**値が0または2で、"Y" が**connectfunctions**キーワードの値の2番目の文字として指定されているドライバーの説明の一覧がアプリケーションで表示される場合があります。 ユーザーがドライバーを選択すると、アプリケーションは**driver**キーワードを使用して**SQLDriverConnect**を呼び出し、カスタムの **[テーブルの選択**] ダイアログボックスを表示します。|  
|**SQLLevel**|ドライバーでサポートされている SQL 92 文法を示す数値:<br /><br /> 0 = SQL-92 エントリ<br /><br /> 1 = FIPS127-2 移行<br /><br /> 2 = SQL-92 中間<br /><br /> 3 = SQL-92 完全<br /><br /> これは、 **SQLGetInfo**の SQL_SQL_CONFORMANCE オプションに対して返される値と同じである必要があります。|  
  
 使用量の詳細については、このセクションで前述した [使用量のカウント](../../../odbc/reference/install/usage-counting.md) に関するセクションを参照してください。  
  
 アプリケーションで使用状況カウントを設定しないでください。 ODBC ではこのカウントが維持されます。  
  
 たとえば、フォーマットされたテキストファイルのドライバーに Text.dll という名前のドライバー DLL があり、Txtsetup.dll という名前の別のドライバーセットアップ DLL がインストールされているとします。 ドライバーがレベル1の API 準拠レベルをサポートしている場合、最小 SQL 文法準拠レベルをサポートし、ファイルをテーブルとして扱い、.txt および .csv 拡張子を持つファイルを使用できます。 Text サブキーの下の値は次のようになります。  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
