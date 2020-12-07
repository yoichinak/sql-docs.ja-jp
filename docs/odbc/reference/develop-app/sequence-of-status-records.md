---
description: 状態レコードのシーケンス
title: 状態レコードのシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2cb519cab987a1abd924f1b779a7f07c3201475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476454"
---
# <a name="sequence-of-status-records"></a>状態レコードのシーケンス
2つ以上の状態レコードが返された場合、ドライバーマネージャーとドライバーは、次の規則に従ってそれらを順位付けします。 ランクが最も高いレコードが最初のレコードになります。 レコードの順位付け時には、レコードのソース (ドライバーマネージャー、ドライバー、ゲートウェイなど) は考慮されません。  
  
-   **エラー** エラーを説明する状態レコードのランクが最も高くなります。 エラーレコードの中には、トランザクションエラーまたは可能性のあるトランザクションエラーを示すレコードが、他のすべてのレコードを処理しています。 2つ以上のレコードで同じエラー条件が記述されている場合、Open Group CLI 仕様 (クラス 03 ~ HZ) によって定義された SQLSTATEs は、ODBC 定義の SQLSTATEs とドライバーで定義された SQLSTATEs を使用します。  
  
-   **実装で定義されたデータ値がありません** ドライバーで定義されたデータ値がないことを示す状態レコード (クラス 02) には、2番目に高いランクが付けられます。  
  
-   **警告** 警告 (クラス 01) を説明する状態レコードのランクは最も低くなります。 2つ以上のレコードが同じ警告条件を記述している場合、Open Group CLI 仕様で定義されている警告 SQLSTATEs は、ODBC 定義の sqlstates とドライバーで定義された SQLSTATEs を指定します。  
  
 ランクが最も高いレコードが2つ以上ある場合、どのレコードが最初のレコードであるかが定義されていません。 他のすべてのレコードの順序は定義されていません。 特に、エラーの前に警告が表示されることがあるため、SQL_SUCCESS 以外の値が返された場合、アプリケーションはすべての状態レコードを確認する必要があります。
