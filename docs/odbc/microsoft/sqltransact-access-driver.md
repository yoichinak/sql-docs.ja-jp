---
description: SQLTransact (Access ドライバー)
title: SQLTransact (Access Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9b00f8f5a12af2d3823171d22ad53106569352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339691"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access ドライバー)
> [!NOTE]  
>  このトピックでは、ドライバー固有の情報にアクセスします。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 Microsoft Access ドライバーが使用されている場合、 **Sqltransact**を呼び出すと、SQL_COMMIT と SQL_ROLLBACK が*fType*引数に対してサポートされます。  
  
 コミット処理中にエラーが発生した場合は、Microsoft Access driver セットアップの [データベースの修復] オプションを使用するか、 **Sqlconfigdatasource** 関数の REPAIR_DB キーワードを使用して、影響を受けるデータベースを修復できます。
