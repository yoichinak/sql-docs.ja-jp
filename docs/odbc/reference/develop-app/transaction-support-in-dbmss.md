---
description: DBMS でのトランザクションのサポート
title: Dbms | でのトランザクションのサポートMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487455"
---
# <a name="transaction-support-in-dbmss"></a>DBMS でのトランザクションのサポート
一部のデータベース (特に、dBASE、Paradox、および Btrieve などのデスクトップデータベース) では、トランザクションはサポートされていません。 トランザクションをサポートするデータベース間でも、トランザクション内で使用できる SQL ステートメントの種類には違いがあります。 詳細については、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明の SQL_TXN_CAPABLE オプションを参照してください。
