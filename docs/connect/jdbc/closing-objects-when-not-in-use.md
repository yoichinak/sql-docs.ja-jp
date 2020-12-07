---
description: 使用されていないオブジェクトを閉じる
title: 使用されていないオブジェクトを閉じる | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c8e1242f5090e347dd3dd61d42fedd3698613cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438454"
---
# <a name="closing-objects-when-not-in-use"></a>使用されていないオブジェクトを閉じる
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] のオブジェクト、特に [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)、または Statement オブジェクト ([SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) など) の 1 つを使用する場合、必要でなくなったときは close メソッドを使用して明示的に閉じる必要があります。 これにより、Java 仮想マシンのガベージ コレクターによる処理を待たずに、迅速にドライバーとサーバーのリソースを解放できるため、パフォーマンスが向上します。  
  
 スクロール ロックを使用しているときに、サーバー上で適切なコンカレンシーを維持するためには、オブジェクトを閉じることが特に重要となります。 最後にアクセスしたフェッチ バッファーのスクロール ロックは、結果セットが閉じられるまで保持されます。 同様に、ステートメントの準備されたハンドルは、ステートメントが閉じられるまで保持されます。 複数のステートメントで接続を再利用する場合は、スコープから出る前にステートメントを閉じることで、サーバーが準備されたハンドルを早期にクリーンアップできるようになります。  
  
## <a name="see-also"></a>関連項目  
 [JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
