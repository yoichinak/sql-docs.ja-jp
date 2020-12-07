---
description: カタログとスキーマの使用状況
title: カタログとスキーマの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2506810c477e9d75e1d3b38f38185d22edf9d010
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494692"
---
# <a name="catalog-and-schema-usage"></a>カタログとスキーマの使用状況
データソースは、すべての SQL ステートメントで、カタログ名とスキーマ名をオブジェクト名の識別子としてサポートするとは限りません。 データソースでは、データ操作言語 (DML) ステートメント、プロシージャ呼び出し、テーブル定義ステートメント、インデックス定義ステートメント、特権定義ステートメントなど、SQL ステートメントの1つ以上のクラスで、カタログ名とスキーマ名がサポートされている場合があります。 アプリケーションでは、カタログ名とスキーマ名を使用できる SQL ステートメントのクラスを特定するために、SQL_CATALOG_USAGE オプションと SQL_SCHEMA_USAGE オプションを使用して **SQLGetInfo** を呼び出します。
