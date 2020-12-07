---
description: トランザクションのサポート
title: トランザクションのサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0218941606752ccd93c7bc9bdfe31096682c6d87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476331"
---
# <a name="transaction-support"></a>トランザクションのサポート
トランザクションのサポートの次数はドライバーで定義されています。 ODBC は、データの複数の更新を管理する必要がないシングルユーザーまたはデスクトップデータベースに実装するように設計されています。 さらに、トランザクションをサポートする一部のデータベースは、SQL のデータ操作言語 (DML) ステートメントでのみ使用できます。トランザクションがアクティブな場合のデータ定義言語 (DDL) の使用に関する制限や特別なトランザクションセマンティクスがあります。 つまり、テーブルに対する複数の同時更新のトランザクションがサポートされている場合がありますが、トランザクション中にテーブルの数と定義を変更することはできません。  
  
 アプリケーションは、SQL_TXN_CAPABLE オプションを指定して **SQLGetInfo** を呼び出すことにより、トランザクションがサポートされているかどうか、トランザクションに ddl を含めることができるかどうか、および ddl をトランザクションに含める場合の特殊な効果を決定します。 詳細については、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明を参照してください。  
  
 ドライバーがトランザクションをサポートしていないものの、アプリケーションが (ODBC 以外の API を使用して) データをロックおよびロック解除できる場合、アプリケーションは必要に応じてレコードとテーブルのロックおよびロック解除を行うことでトランザクションサポートを実現できます。 アカウント転送の例を実装するために、アプリケーションは、両方のアカウントのレコードをロックし、現在の値をコピーし、最初のアカウントをデビットにして、2番目のアカウントをクレジットし、レコードのロックを解除します。 いずれかの手順が失敗した場合、アプリケーションはコピーを使用してアカウントをリセットします。  
  
 トランザクションをサポートするデータソースであっても、特定の環境内で同時に複数のトランザクションをサポートできない場合があります。 アプリケーションでは、SQL_MULTIPLE_ACTIVE_TXN オプションを使用して **SQLGetInfo** を呼び出し、データソースが同じ環境内の複数の接続で同時にアクティブなトランザクションをサポートできるかどうかを判断します。 接続ごとに1つのトランザクションがあるため、これは同じデータソースへの複数の接続を持つアプリケーションにのみ適用されます。
