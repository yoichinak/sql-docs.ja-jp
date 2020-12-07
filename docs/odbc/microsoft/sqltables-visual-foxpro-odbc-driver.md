---
description: SQLTables (Visual FoxPro ODBC ドライバー)
title: SQLTables (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 089208ab612984283e3f87c4ad03aca0ccfa2b38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471554"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル1  
  
 **Sqltables**ステートメント内のパラメーターによって指定されたテーブル名の一覧を返します。 パラメーターが指定されていない場合は、現在のデータソースに格納されているテーブル名を返します。 ドライバーは、結果セットとして情報を返します。  
  
 列挙型の呼び出しは、リモートビューまたはローカルのパラメーター化されたビューに対して結果セットのエントリを受け取りません。 ただし、一意のテーブル名指定子を使用して **Sqltables** を呼び出すと、そのビューに一致するものが見つかります。これにより、API を使用して、新しいテーブルを作成する前に名前の競合を確認できます。  
  
> [!NOTE]  
>  Visual FoxPro ODBC ドライバーは、両方の種類のテーブルがシステムの同じディレクトリに格納されている場合でも、 [データベーステーブル](../../odbc/microsoft/visual-foxpro-terminology.md) と [フリーテーブル](../../odbc/microsoft/visual-foxpro-terminology.md)を区別します。 データソースがフリーテーブルのディレクトリの場合、Visual FoxPro ODBC ドライバーは、データベースに関連付けられているテーブルの名前をカタログ化または返しません。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [sqltables](../../odbc/reference/syntax/sqltables-function.md) 」を参照してください。
