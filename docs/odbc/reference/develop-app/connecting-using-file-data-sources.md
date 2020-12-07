---
description: ファイル データ ソースを使用した接続
title: ファイルデータソースを使用した接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ab210a77d1d6516b6b54ba25767d859ff9102fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476764"
---
# <a name="connecting-using-file-data-sources"></a>ファイル データ ソースを使用した接続
ファイルデータソースの接続情報は、dsn ファイルに格納されます。 このため、接続文字列は、1人のユーザーが繰り返し使用することも、適切なドライバーがインストールされていれば複数のユーザー間で共有することもできます。 このファイルには、ドライバー名 (または unshareable file データソースの場合は別のデータソース名) と、必要に応じて **SQLDriverConnect**で使用できる接続文字列が含まれています。 ドライバーマネージャーは、 **SQLDriverConnect** への呼び出し用の接続文字列を、dsn ファイル内のキーワードから作成します。  
  
 ファイルデータソースを使用すると、アプリケーションで接続オプションを指定できます。 **SQLDriverConnect**で使用する接続文字列を作成する必要はありません。 通常、ファイルデータソースは **SAVEFILE** キーワードを指定することによって作成されます。これにより、ドライバーマネージャーは **SQLDriverConnect** の呼び出しによって作成された出力接続文字列を、dsn ファイルに保存します。 この接続文字列は、 **FILEDSN**キーワードを使用して**SQLDriverConnect**を呼び出すことによって、繰り返し使用できます。 これにより、接続プロセスが効率化され、接続文字列の永続的なソースが提供されます。  
  
 ファイルデータソースは、インストーラー DLL で **Sqlcreatedatasource** を呼び出すことによっても作成できます。 **SQLWriteFileDSN**を呼び出すことによって、dsn ファイルに情報を書き込むことができます。また、 **SQLReadFileDSN**を呼び出して、dsn ファイルから読み取ることもできます。これらの関数はどちらも、インストーラー DLL に含まれています。 インストーラー DLL の詳細については、「 [データソースの構成](../../../odbc/reference/install/configuring-data-sources.md)」を参照してください。  
  
 接続情報に使用されるキーワードは、dsn ファイルの [ODBC] セクションにあります。 [ODBC] セクションで共有可能な dsn ファイルの最小情報は、DRIVER キーワードです。  
  
```  
DRIVER = SQL Server  
```  
  
 共有可能な dsn ファイルには、通常、次のような接続文字列が含まれています。  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 ファイルデータソースが unshareable の場合、dsn ファイルには **dsn** キーワードだけが含まれます。 ドライバーマネージャーは、unshareable file データソース内の情報を送信すると、 **DSN** キーワードによって示されるデータソースに必要に応じて接続します。 Unshareable ファイルには、次のキーワードが含まれています。  
  
```  
DSN = MyDataSource  
```  
  
 ファイルデータソースに使用される接続文字列は、dsn ファイルで指定されたキーワードと、 **SQLDriverConnect**の呼び出しで接続文字列で指定されたキーワードの和集合です。 Dsn ファイル内のいずれかのキーワードが接続文字列のキーワードと競合する場合は、使用するキーワード値がドライバーマネージャーによって決定されます。 詳細については、「 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
