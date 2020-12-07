---
description: FOR JSON が SQL Server データ型を JSON データ型に変換する方法 (SQL Server)
title: FOR JSON が SQL Server データ型を JSON データ型に変換する方法
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d010978b7c660b43a5fe6487ac57e0d6143b282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499302"
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON が SQL Server データ型を JSON データ型に変換する方法 (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **FOR JSON** 句は、次の規則に従って、JSON 出力で SQL Server データ型を JSON 型に変換します。  
  
|カテゴリ|SQL Server のデータ型|JSON データ型|  
|--------------|--------------|---------------|  
|文字型と文字列型|char、nchar、varchar、nvarchar|string|  
|数値型|int、bigint、float、decimal、numeric|number|  
|ビット型|bit|Boolean (true または false)|  
|日付型と時刻型|date、datetime、datetime2、time、datetimeoffset|string|  
|バイナリ型|varbinary、binary、image、timestamp、rowversion|BASE64 エンコード文字列|  
|CLR 型|geometry、geography、他の CLR 型|サポートされていません。 これらの型はエラーを返します。<br /><br /> SELECT ステートメントで CAST または CONVERT を使用するか、CLR プロパティまたはメソッドを使用して、JSON 型に正常に変換できる SQL Server データ型にソース データを変換します。 たとえば、geometry 型には **STAsText()** を使い、CLR 型には **ToString()** を使います。 JSON 出力値の型は、その後 SELECT ステートメントで適用している変換の戻り値の型から派生します。|  
|その他の型|uniqueidentifier、money|string|  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [FOR JSON を使用してクエリ結果を JSON として書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
