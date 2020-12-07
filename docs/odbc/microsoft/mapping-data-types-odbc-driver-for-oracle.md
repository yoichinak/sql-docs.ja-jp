---
description: データ型のマッピング (ODBC Driver for Oracle)
title: データ型のマッピング (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ea39a8277508422028d5794ccbcb7a62dacdb08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483515"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>データ型のマッピング (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 Oracle サーバーは、一連のデータ型をサポートしています。 ODBC Driver for Oracle は、これらのデータ型を適切な ODBC SQL データ型にマップします。 次の表に、Oracle 7.3 Server のデータ型とそれに対応する ODBC SQL データ型を示します。  
  
 ODBC Driver for Oracle は、Oracle 7.3 およびいくつかの Oracle8 データ型をサポートしています。 サポートされている Oracle8 データ型の詳細については、「 [サポートされるデータ型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)」を参照してください。  
  
|Oracle Server データ型|ODBC SQL データ型|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  許容される VARCHAR 列のサイズの詳細については、このガイドの「 [Varchar 列のサイズ](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) 」を参照してください。
