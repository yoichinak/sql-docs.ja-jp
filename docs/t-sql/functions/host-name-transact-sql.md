---
description: HOST_NAME (Transact-SQL)
title: HOST_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HOST_NAME_TSQL
- HOST_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- HOST_NAME function
- workstation names [SQL Server]
ms.assetid: 4b8b0705-c083-4b07-b954-c83ee73b2ebb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3dbd0179163a13989308f1c01ba350b37bf959ea
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116679"
---
# <a name="host_name-transact-sql"></a>HOST_NAME (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  ワークステーション名を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
HOST_NAME ()  
```  

## <a name="return-types"></a>戻り値の型
 **nvarchar(128)**  
  
## <a name="remarks"></a>注釈  
 システム関数へのパラメーターが省略可能の場合は、現在のデータベース、ホスト コンピューター、サーバー ユーザー、またはデータベース ユーザーが推測されます。 組み込み関数の後には常にかっこが必要です。  
  
 システム関数は、選択リストの中、WHERE 句の中、また、式を使える所ならどこにでも使用できます。  
  
> [!IMPORTANT]  
>  クライアント アプリケーションによりワークステーション名が提供されます。また、不正確なデータが提供されることもあります。 HOST_NAME はセキュリティ機能としては期待しないでください。  
  
## <a name="examples"></a>例  
 次の例では、受注を記録するテーブルに行を挿入するコンピューターのワークステーション名を記録するために、`HOST_NAME()` 定義内で `DEFAULT` を使用するテーブルを作成します。  
  
```sql  
CREATE TABLE Orders  
   (OrderID     INT        PRIMARY KEY,  
    CustomerID  NCHAR(5)   REFERENCES Customers(CustomerID),  
    Workstation NCHAR(30)  NOT NULL DEFAULT HOST_NAME(),  
    OrderDate   DATETIME   NOT NULL,  
    ShipDate    DATETIME   NULL,  
    ShipperID   INT        NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
