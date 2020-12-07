---
title: JDBC ドライバーによるパフォーマンスと信頼性の強化
description: Microsoft JDBC driver for SQL Server を使用する際の、アプリケーションのパフォーマンスと信頼性を強化するさまざまな方法について説明します。
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc04a90569974acbc99dcb66680d66289db1c0d1
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565380"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>JDBC ドライバーによるパフォーマンスと信頼性の強化

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

アプリケーション開発において、パフォーマンスと信頼性の強化は常に求められるものです。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、このような要求を実現させる技術を豊富に備えています。  
  
このセクションのトピックでは、JDBC ドライバーを使用する際の、アプリケーションのパフォーマンスと信頼性を強化するさまざまな方法について説明します。  

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|  
|-----------|-----------------|  
|[使用されていないオブジェクトを閉じる](../../connect/jdbc/closing-objects-when-not-in-use.md)|必要なくなった JDBC ドライバー オブジェクトを閉じることの重要性について説明します。|  
|[トランザクション サイズの管理](../../connect/jdbc/managing-transaction-size.md)|トランザクションのパフォーマンスを向上させる方法について説明します。|  
|[ステートメントおよび結果セットの操作](../../connect/jdbc/working-with-statements-and-result-sets.md)|ステートメントまたは ResultSet オブジェクトを使用するときにパフォーマンスを向上させる方法について説明します。|  
|[アダプティブ バッファリングの使用](../../connect/jdbc/using-adaptive-buffering.md)|サーバー カーソルのオーバーヘッドを発生させることなく、あらゆる種類の大きな値のデータを取得できるように設計されている、アダプティブ バッファリング機能について説明します。|  
|[スパース列](../../connect/jdbc/sparse-columns.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスパース列に対する JDBC ドライバーのサポートについて説明します。|  
|[JDBC ドライバーの準備されたステートメント メタデータ キャッシュ](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|準備されたステートメント クエリを使用してパフォーマンスを向上させる方法について説明します。|
|[バッチ挿入操作に一括コピー API を使用する](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|バッチ挿入操作に対して一括コピー API を有効にする方法とその利点について説明します。|
|[String パラメーターが Unicode として送信されない](../../connect/jdbc/setting-the-connection-properties.md)|**CHAR**、**VARCHAR**、**LONGVARCHAR** データを使用するとき、ユーザーはパフォーマンスを最適化する目的で、接続プロパティ **sendStringParametersAsUnicode** を `false` に設定できます。|

## <a name="see-also"></a>関連項目

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
