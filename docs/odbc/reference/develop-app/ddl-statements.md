---
description: DDL ステートメント
title: DDL ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 395abe3eed64f37c000ecff6f0b68a6e0cb1d076
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424734"
---
# <a name="ddl-statements"></a>DDL ステートメント
データ定義言語 (DDL) ステートメントは、Dbms によって大きく異なります。 ODBC SQL では、最も一般的なデータ定義操作 (テーブル、インデックス、およびビューの作成と削除) のステートメントを定義します。テーブルの変更権限の付与と取り消しを行います。 その他のすべての DDL ステートメントは、データソース固有です。 そのため、相互運用可能なアプリケーションで一部のデータ定義操作を実行することはできません。 通常、これは問題ではありません。そのような操作は DBMS 固有のものであり、ほとんどの Dbms またはドライバーに付属するセットアッププログラムに付属している専用のデータベース管理ソフトウェアに残されている傾向があるためです。  
  
 データ定義のもう1つの問題は、データ型名が Dbms 間で大きく異なることです。 標準のデータ型名を定義し、それらを DBMS 固有の名前に変換するようにドライバーを強制するのではなく、 **SQLGetTypeInfo** を使用すると、アプリケーションで dbms 固有のデータ型名を検出できます。 相互運用可能なアプリケーションでは、これらの名前を SQL ステートメントで使用してテーブルを作成および変更する必要があります。 [「付録 C: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)」と [「付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」に記載されている名前は、例にすぎません。
