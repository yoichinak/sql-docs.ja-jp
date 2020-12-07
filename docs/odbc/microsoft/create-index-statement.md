---
description: CREATE INDEX ステートメント
title: CREATE INDEX ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a3f5a13624cdb137e8c86cf2c27044c6705298f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483635"
---
# <a name="create-index-statement"></a>CREATE INDEX ステートメント
CREATE INDEX ステートメントの構文は次のとおりです。  
  
 CREATE [UNIQUE] インデックス *インデックス-名前* に *テーブル名* (*列識別子* [asc] [desc] [, *列識別子* [asc] [desc]...])で \<*index option list*>  
  
 には次の値 \<*index option list*> を指定できます。 PRIMARY &#124; null を許可しない &#124; null を無視する  
  
 [NULL を許可しない] および [NULL インデックスを無視する] オプションは、Microsoft Access ドライバーでのみ使用されます。 DBASE および Paradox ドライバーは構文を受け入れますが、どちらのオプションも存在しません。  
  
 Paradox ドライバーを使用すると、CREATE INDEX ステートメントによって、Paradox のプライマリキーファイルとセカンダリファイルが作成されます。  
  
 このステートメントは、Microsoft Excel またはテキストドライバーではサポートされていません。
