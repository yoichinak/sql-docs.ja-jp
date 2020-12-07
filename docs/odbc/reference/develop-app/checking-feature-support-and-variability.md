---
description: 機能のサポートと可変性の確認
title: 機能のサポートと可変性のチェックMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60fb6b39d7b2326a925aea40303ce52165cca8a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465914"
---
# <a name="checking-feature-support-and-variability"></a>機能のサポートと可変性の確認
機能のサポートと可変性を確認するために、アプリケーションは通常、 **SQLGetInfo**、 **sqlgetfunctions**、および **SQLGetTypeInfo**を呼び出します。 適切な開始位置は、ドライバーの API と SQL 文法の準拠レベルです。 これらの機能は、さまざまなレベルの機能サポートについて説明しています。 アプリケーションは、他のオプションを指定して **SQLGetInfo** を呼び出して、必要な機能のサポートまたは可変性を判断します。 **sqlgetfunctions** は、返された準拠レベルを超えて必要な関数をサポートするかどうかを判断し、 **SQLGetTypeInfo** はサポートされている SQL データ型を判別します。  
  
 アプリケーションでは、その属性を使用して **SQLSetStmtAttr** または **SQLSetConnectAttr** を呼び出すことによって、ステートメントまたは接続属性がサポートされているかどうかを判断できます。 関数が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返す場合、属性はサポートされています。SQL_ERROR と SQLSTATE HYC00 (省略可能な機能が実装されていない) が返された場合、属性はサポートされません。  
  
 アプリケーションでは、 **Sqldrivers**を呼び出してドライバーに接続する前に、限られた量の情報を確認することもできます。
