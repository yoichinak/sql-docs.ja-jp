---
description: SQL_NO_DATA
title: SQL_NO_DATA |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb81d6f1fce50a27aba203eec4b78648754010e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424574"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
ODBC 3 の場合。*x* アプリケーションは、ODBC 2 で **SQLExecDirect**、 **Sqlexecute**、または **sqlparamdata** を呼び出します。*x* ドライバーデータソースの行に影響を与えない、検索された update ステートメントまたは delete ステートメントを実行するには、ドライバーが SQL_NO_DATA ではなく SQL_SUCCESS を返す必要があります。 ODBC 2 の場合。*x* または ODBC 3。*x* アプリケーションが ODBC 3 を使用して動作している。*x* ドライバーは、同じ結果 (ODBC 3) を使用して **SQLExecDirect**、 **Sqlexecute**、または **sqlparamdata** を呼び出します。*x* ドライバーは SQL_NO_DATA を返す必要があります。
