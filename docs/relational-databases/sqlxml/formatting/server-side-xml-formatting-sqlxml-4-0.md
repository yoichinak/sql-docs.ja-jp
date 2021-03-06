---
title: サーバー側の XML 書式設定 (SQLXML)
description: Microsoft SQL Server データベースに対して実行される SQLXML 4.0 クエリによって生成されるドキュメントのサーバー側 XML 書式設定について説明します。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 629221cc127011e63e58c5044ef9375001b68df3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429969"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>サーバー側の XML 書式設定 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  ここでは、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータベースに対するクエリを実行して生成される行セットを基に、サーバー側で XML ドキュメントを書式設定する場合の情報をまとめます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、データベース テーブルに XML ドキュメントを格納したり、データベース テーブルから XML ドキュメントを取得することができます。 XML ドキュメントを取得するには、SELECT クエリで FOR XML クエリ拡張を使用します。  
  
 たとえば、クライアントアプリケーションが、次のクエリで構成されるに対してコマンドを実行するとし [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] ます。  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 サーバーでは、クエリが 2 段階で実行されます。 最初に、サーバーでは次の SELECT ステートメントが実行されます。  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 次に、サーバーでは生成された行セットに対して FOR XML 変換が適用され、 結果の XML が 1 列の行セットとしてクライアントに送られます。 このドキュメントでは、この処理をサーバー側の XML 書式設定と呼びます。  
  
 サーバー側では、FOR XML 句で次のモードを指定できます。  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 FOR XML 句の詳細については、「 [for Xml を使用した xml の構築](../../../relational-databases/xml/for-xml-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [クライアント側およびサーバー側の XML 書式設定のアーキテクチャ &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [クライアント側の XML 書式設定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
