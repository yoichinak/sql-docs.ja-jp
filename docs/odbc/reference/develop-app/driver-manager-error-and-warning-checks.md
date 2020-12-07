---
description: ドライバー マネージャーのエラーと警告の確認
title: ドライバーマネージャーのエラーと警告の確認 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99a99e1dfeb6cb6993a6967d5d93748afbd44b83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483055"
---
# <a name="driver-manager-error-and-warning-checks"></a>ドライバー マネージャーのエラーと警告の確認
ドライバーマネージャーは、多数の関数を完全または部分的に実装しているため、これらの関数のすべてまたは一部のエラーと警告を確認します。  
  
-   ドライバーマネージャーは、 **Sqldatasources ソース** と **sqldatasources** を実装し、これらの関数のすべてのエラーと警告を確認します。  
  
-   ドライバーマネージャーは、ドライバーが **Sqlgetfunctions**を実装しているかどうかを確認します。 ドライバーが **Sqlgetfunctions**を実装していない場合、ドライバーマネージャーはを実装し、その中のすべてのエラーと警告を確認します。  
  
-   ドライバーマネージャーは、 **SQLAllocHandle**、 **SQLConnect**、 **SQLDriverConnect**、 **SQLBrowseConnect**、 **sqlfreehandle**、 **SQLGetDiagRec**、および **SQLGetDiagField** を部分的に実装し、これらの関数でいくつかのエラーをチェックします。 これらの関数の一部では、同じエラーが返される場合があります。これは、これらの関数の両方で同様の操作が実行されるためです。 たとえば、 **SQLDriverConnect**のログインダイアログボックスを表示できない場合、ドライバーマネージャーまたはドライバーが SQLSTATE IM008 (Dialog failed) を返すことがあります。
