---
description: SET PATH コマンド
title: パスの設定コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36131e53d1a10d8af3e7ca226768a9c08a14ba77
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421836"
---
# <a name="set-path-command"></a>SET PATH コマンド
ファイル検索のパスを指定します。 ドライバー固有の情報については、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引数  
 [ *パス*]  
 Visual FoxPro で検索するディレクトリを指定します。 ディレクトリを区切るには、コンマまたはセミコロンを使用します。  
  
## <a name="remarks"></a>解説  
 SET PATH を使用すると、ストアドプロシージャ内で呼び出すことができる他の Visual FoxPro プログラムの検索パスを指定できます。 SET PATH は、接続に指定したデータソースのパスを変更しません。  
  
 既定のディレクトリまたはフォルダーへのパスを復元するには *、パスを指定せ* ずにパスを設定します。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 ストアドプロシージャで SET PATH を実行すると、次の関数とコマンドによって無視されます。  
  
-   [Sqltables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)や[sqltables](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)などのカタログ関数は、新しいパスを無視し、 [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)または[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)のデータソースによって指定されたパスを引き続き参照します。  
  
-   SELECT、INSERT、UPDATE、DELETE、CREATE TABLE などのコマンドは、新しいパスを無視し、 **SQLPrepare** または **SQLExecDirect**のデータソースによって指定されたパスを引き続き参照します。  
  
 ストアドプロシージャで SET パスを発行した後で、そのパスを元の状態に戻すことができない場合、データベースへの他の接続では、新しいパスが使用されます (SET PATH のスコープがデータセッションに設定されていないため)。  
  
 データソースで指定されたディレクトリ以外のディレクトリでテーブルを作成、選択、または更新する場合は、コマンドを使用してファイルの完全パスを指定します。  
  
## <a name="see-also"></a>参照  
 [[ODBC Visual FoxPro セットアップ] ダイアログボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
