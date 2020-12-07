---
description: '[ファイル データ ソース]'
title: ファイルデータソース |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d02c767adab90ee4a7b6ff93a34886c03b87780c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429044"
---
# <a name="file-data-sources"></a>[ファイル データ ソース]
*ファイルデータソース* はファイルに格納され、接続情報が1人のユーザーによって繰り返し使用されるか、複数のユーザー間で共有されます。 ファイルデータソースを使用すると、ドライバーマネージャーは、dsn ファイルの情報を使用してデータソースへの接続を行います。 このファイルは、他のファイルと同様に操作できます。 ファイルデータソースには、マシンデータソースと同じようにデータソース名がなく、1つのユーザーまたはコンピューターに登録されていません。  
  
 ファイルデータソースは接続プロセスを合理化します。これは、 **SQLDriverConnect** 関数を呼び出すために作成する必要のある接続文字列が dsn ファイルに含まれているためです。 Dsn ファイルのもう1つの利点は、任意のコンピューターにコピーできることです。そのため、適切なドライバーがインストールされていれば、同一のデータソースを多くのコンピューターで使用できます。 ファイルデータソースは、アプリケーションで共有することもできます。 共有可能なファイルデータソースは、ネットワーク上に配置して、複数のアプリケーションで同時に使用することができます。  
  
 また、dsn ファイルを unshareable することもできます。 Unshareable ファイルは、1台のコンピューター上に存在し、コンピューターのデータソースを指します。 Unshareable file データソースは、主に、コンピューターのデータソースをファイルデータソースに簡単に変換できるようにするために存在します。これにより、ファイルデータソースだけで動作するようにアプリケーションを設計できます。 ドライバーマネージャーは、unshareable file データソース内の情報を送信するときに、必要に応じて、dsn ファイルが指すマシンデータソースに接続します。  
  
 ファイルデータソースの詳細については、「 [ファイルデータソースを使用した接続](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)」または「 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 関数の説明」を参照してください。
