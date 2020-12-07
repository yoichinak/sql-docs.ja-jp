---
description: データ ソースの管理
title: データソースの管理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 506a7b6fbbf93b8fb4b28f66824778b2266f6cbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412864"
---
# <a name="managing-data-sources"></a>データ ソースの管理
ドライバーのセットアッププログラムから ODBC ドライバーをインストールした後、1つまたは複数のデータソースを定義できます。 データソース名 (DSN) は、データの一意の説明を提供する必要があります。たとえば、" *支払い* " や " *買掛金勘定*" などです。 現在インストールされているすべてのドライバーに対して定義されているユーザーおよびシステムデータソースは、[ **ODBC データソースアドミニストレーター** ] ダイアログボックスの [**ユーザー dsn** ] タブまたは [**システム dsn** ] タブに表示されます。 指定されたディレクトリ内のファイルデータソースは、[**ファイル DSN** ] タブに表示されます。表示されるディレクトリは、[**ファイル DSN** ] タブの [**検索対象**] ボックスに入力します。  
  
> [!NOTE]  
>  64ビットプラットフォームで32ビットドライバーに接続するデータソースを管理するには、c:\windows\sysWOW64\odbcad32.exe を使用します。 64ビットドライバーに接続するデータソースを管理するには、c:\windows\system32\odbcad32.exe を使用します。 64ビット Windows 8 オペレーティングシステムの **管理ツール** では、[32 ビットおよび64ビットの **ODBC データソースアドミニストレーター** ] ダイアログボックスの両方にアイコンがあります。  
  
 64ビット odbcad32.exe を使用して32ビットドライバーに接続する DSN を構成または削除する場合 (たとえば、ドライバーの **Microsoft access ( \* .mdb))**、次のエラーメッセージが表示されます。  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 このエラーを解決するには、32ビットの odbcad32.exe を使用して、DSN を構成または削除します。  
  
 データソースによって、特定の ODBC ドライバーが、そのドライバーを介してアクセスするデータに関連付けられます。 たとえば、ODBC dBASE ドライバーを使用して、ハードディスク上の特定のディレクトリまたはネットワークドライブにある1つ以上の dBASE ファイルにアクセスするデータソースを作成することができます。 次の表に示すように、ODBC データソースアドミニストレーターを使用して、データソースを追加、変更、および削除できます。  
  
|アクション|説明|  
|------------|-----------------|  
|データ ソースの追加|複数のデータソースを追加することができます。各データソースには、ドライバーを使用してアクセスするデータを関連付けるものがあります。 各データソースに、そのデータソースを一意に識別する名前を付けます。 たとえば、顧客情報を含む dBASE ファイルのセットのデータソースを作成する場合、データソースに "Customers" という名前を指定できます。 通常、アプリケーションには、ユーザーが選択できるデータソース名が表示されます。<br /><br /> ファイルデータソースの追加は、ユーザーデータソースまたはシステムデータソースの追加とは少し異なります。 詳細については、ODBC データソースアドミニストレーターのヘルプファイルを参照してください。|  
|データソースの変更|要件によっては、データソースの再構成が必要になる場合があります。 オプションをリセットするには、[ドライバーの設定] ダイアログボックスで [ **構成** ] をクリックします。|  
|データソースの削除|データソースを選択した後、[ **削除** ] をクリックします。|  
  
 ファイルデータソースの詳細については、「ファイルデータソースまたは[SQLDriverConnect 関数](../../odbc/reference/syntax/sqldriverconnect-function.md)[を使用した接続](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ODBC データ ソース アドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md)
