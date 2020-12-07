---
description: ドライバー マネージャーのロール
title: ドライバーマネージャーの役割 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f974fe6436173b55f39aced45cc38312221cffaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465659"
---
# <a name="role-of-the-driver-manager"></a>ドライバー マネージャーのロール
ドライバーマネージャーは、生成された状態レコードを返す最終的な順序を決定します。 特に、順位が最も高いレコードを決定し、最初に返されるレコードを決定します。 ドライバーは、生成された状態レコードの順序付けを行います。 状態レコードがドライバーマネージャーとドライバーの両方によって投稿されている場合は、ドライバーマネージャーによってそれらの順序が決定されます。 詳細については、「 [一連の状態レコード](../../../odbc/reference/develop-app/sequence-of-status-records.md)」を参照してください。  
  
 ドライバーマネージャーは、可能な限り多くのエラーチェックを行います。 これにより、すべてのドライバーが同じエラーをチェックすることができません。 たとえば、関数の引数が**SQLSetPos**の*操作*などの個別の値の数を受け入れる場合、ドライバーマネージャーは、指定された値が有効であることを確認します。  
  
 次のセクションでは、ドライバーマネージャーによってチェックされる条件の種類について説明します。 これらは包括的なものではありません。ドライバーマネージャーが返す SQLSTATEs の完全な一覧については、各関数の「診断」セクションを参照してください。ドライバーマネージャーによって行われた各チェックの説明は、"(DM)" という文字で始まります。 「 [付録 B: ODBC 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」の状態遷移テーブルも参照してください。かっこで囲まれたエラーは、ドライバーマネージャーによって検出されます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [引数の値のチェック](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [状態遷移の確認](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [一般的なエラー チェック](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [ドライバー マネージャーのエラーと警告の確認](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
