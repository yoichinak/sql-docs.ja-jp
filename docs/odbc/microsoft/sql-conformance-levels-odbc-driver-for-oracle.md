---
description: SQL への準拠レベル (ODBC Driver for Oracle)
title: SQL 準拠レベル (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78e98aed952ef8b15a4654be9f82e355d1b4177b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483425"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL への準拠レベル (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 ODBC Driver for Oracle では、sql の構文とコアの SQL 文法がサポートされています。また、次の ODBC 拡張機能もサポートされています。  
  
-   日付、時刻、およびタイムスタンプデータ  
  
-   左外部結合と右外部結合  
  
-   数値関数:  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            床  
        :::column-end:::
        :::column:::
            ログ  
            Log10  
            Mod  
            Pi  
            電力  
        :::column-end:::
        :::column:::
            round  
            second  
            署名  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   日付関数:   

    :::row:::
        :::column:::
            Curdate  
            Curtime  
            Dayname  
            Dayofmonth  
        :::column-end:::
        :::column:::
            Dayofweek  
            Dayofyear  
            時間  
            Month  
        :::column-end:::
        :::column:::
            monthname  
            minute  
            now  
            quarter  
        :::column-end:::
        :::column:::
            second  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   文字列関数:   

    :::row:::
        :::column:::
            Ascii  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            Left  
            長さ  
            Ltrim  
            Replace  
        :::column-end:::
        :::column:::
            right  
            rtrim  
            soundex  
            substring  
        :::column-end:::
        :::column:::
            ucase  
        :::column-end:::
    :::row-end:::

-   型変換関数:  

    Convert  

-   システム関数:  
  
    Ifnull  
    ユーザー
