---
title: SQLDriverConnect | を使用した接続Microsoft Docs
description: SQLDriverConnect は、SQLConnect に対する追加の接続機能を提供します。詳細については、ユーザーにプロンプトを表示するオプションも含まれています。
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746172"
---
# <a name="connecting-with-sqldriverconnect"></a>SQLDriverConnect による接続

**SQLDriverConnect** は、接続文字列を使用してデータソースに接続するために使用されます。 次のシナリオでは、 **SQLConnect**の代わりに**SQLDriverConnect**が使用されます。  
  
- データソース名、1つ以上のユーザー Id、1つ以上のパスワード、およびデータソースに必要なその他の情報を含む接続文字列を使用して接続を確立します。  
  
- 部分的な接続文字列を使用して接続を確立するか、追加情報を使用しません。この場合、ドライバーマネージャーとドライバーは、ユーザーに接続情報の入力を求めることができます。  
  
- システム情報で定義されていないデータソースへの接続を確立します。 アプリケーションが部分的な接続文字列を提供する場合、ドライバーはユーザーに接続情報の入力を求めることができます。  
  
- Dsn ファイル内の情報から構築された接続文字列を使用して、データソースへの接続を確立します。  
  
接続が確立されると、 **SQLDriverConnect** は完了した接続文字列を返します。 アプリケーションは、後続の接続要求にこの文字列を使用できます。

このセクションでは、次のトピックを扱います。  
  
- [ドライバー固有の接続情報](driver-specific-connection-information.md)  
  
- [接続情報をユーザーに確認する](prompting-the-user-for-connection-information.md)  
  
- [ファイル データ ソースを使用した接続](connecting-using-file-data-sources.md)  
  
- [ドライバーに直接接続する](connecting-directly-to-drivers.md)
