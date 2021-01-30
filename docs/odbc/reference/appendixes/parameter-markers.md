---
description: パラメーター マーカー
title: パラメーターマーカー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 7ab9b0cd8682ecc722f97b563285bdd31665c1fd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99205333"
---
# <a name="parameter-markers"></a>パラメーター マーカー
SQL-92 仕様に従って、アプリケーションは次の場所にパラメーターマーカーを配置することはできません。 より包括的な一覧については、「SQL-92 の仕様」を参照してください。  
  
-   **選択** リスト内  
  
-   *比較述語* で両方の *式* として  
  
-   二項演算子の両方のオペランドとして  
  
-   **BETWEEN** 演算の1番目と2番目のオペランドの両方として  
  
-   **BETWEEN** 演算の1番目と3番目のオペランドの両方として  
  
-   **IN** 演算の式と最初の値の両方として  
  
-   単項演算のオペランドとしての。  
  
-   *セット関数参照* の引数として  
  
 パラメーターマーカーの詳細については、「SQL-92 の仕様」を参照してください。 パラメーターの詳細については、「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。
