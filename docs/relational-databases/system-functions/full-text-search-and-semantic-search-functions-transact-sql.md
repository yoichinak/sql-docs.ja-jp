---
description: フルテキスト検索およびセマンティック検索関数 (Transact-sql)
title: フルテキスト検索およびセマンティック検索関数 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: deb790da4e4e263318717c3ee81cc8ee8d467ae6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474649"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>フルテキスト検索およびセマンティック検索関数 (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このセクションでは、フルテキスト検索とセマンティック検索に関係するシステム関数について説明します。  
  
## <a name="full-text-search-functions"></a>フルテキスト検索関数  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 1つの単語と語句の完全一致またはあいまい一致を含む列、特定の範囲内での近接語句、または重み付け一致を含む列について、0行、1行、または複数の行から成るテーブルを返します。  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 指定された *freetext_string*内のテキストの正確な表現だけでなく、意味に一致する値を含む列について、0行、1行、または複数の行から成るテーブルを返します。  
  
## <a name="semantic-search-functions"></a>セマンティック検索関数  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 指定されたテーブル内の列に関連付けられているキーフレーズに対して、0行、1行、または複数の行を含むテーブルを返します。  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 2つのドキュメント (ソースドキュメントと一致するドキュメント) に共通し、意味が似ているキーフレーズの0行、1行、または複数の行から成るテーブルを返します。  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 指定されたドキュメントに意味が似ているコンテンツを持つこれらの列に対し、0 行、1 行、または複数の行から成るテーブルを返します。  
  
  
