---
description: ファイル ベースのドライバー
title: ファイルベースのドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 770e8560c540e8423aebf0a79c0e8ee5c124c8e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429084"
---
# <a name="file-based-drivers"></a>ファイル ベースのドライバー
ファイルベースのドライバーは、ドライバーが使用するスタンドアロンデータベースエンジンを提供しない dBASE などのデータソースと共に使用されます。 これらのドライバーは物理データに直接アクセスし、SQL ステートメントを処理するためにデータベースエンジンを実装する必要があります。 標準的な方法として、ファイルベースのドライバーのデータベースエンジンは、SQL の最小一致レベルで定義されている ODBC SQL のサブセットを実装します。この準拠レベルの SQL ステートメントの一覧については、「 [付録 C: Sql 文法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)」を参照してください。  
  
 ファイルベースのドライバーと DBMS ベースのドライバーを比較する場合、ファイルベースのドライバーは、データベースエンジンのコンポーネントによって記述するのは困難です。また、データベースエンジンをデータベースエンジンに作成する時間は、データベース企業によって作成されたものと同じほど強力ではないため、あまり複雑ではありません。  
  
 次の図は、ファイルベースのドライバーの2つの異なる構成を示しています。1つはデータがローカルにあり、もう1つはネットワークファイルサーバー上に存在します。  
  
 ![ファイル&#45;ベースのドライバーの2つの構成](../../odbc/reference/media/pr06.gif "pr06")
