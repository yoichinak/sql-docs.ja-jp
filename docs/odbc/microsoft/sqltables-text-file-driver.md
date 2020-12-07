---
description: SQLTables (テキスト ファイル ドライバー)
title: SQLTables (テキストファイルドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6c6f65603cee70811d7c9894ba9d840d28ad4f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339693"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (テキスト ファイル ドライバー)
> [!NOTE]  
>  このトピックでは、テキストファイルドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
|引数|コメント|  
|--------------|--------------|  
|*szTableOwner*|すべてのドライバーで所有者名がサポートされていないため、 *Sztableowner* の有効な引数は NULL だけです。 *Sztableowner*を NULL に設定すると、すべてのテーブルが返されます。 TABLE_OWNER 列に NULL が返されます。|  
|*szTableQualifier*|TABLE_QUALIFIER 列では、 **Sqltables** はディレクトリへのパスを返します。|  
|*SzTableType*|サポートされているテーブル型は、"TABLE" だけです。<br /><br /> テキストドライバーを使用する場合、 **Sqltables**によって返されるファイルの一覧は、[ **ODBC テキストの設定**] ダイアログボックスの [**拡張機能]** ボックスの一覧に表示されるファイル拡張子によって決まります。|
