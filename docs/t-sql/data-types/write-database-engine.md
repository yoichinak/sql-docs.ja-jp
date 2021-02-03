---
description: Write (データベース エンジン)
title: Write (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: aba1271dd68224d237595a81d61b23d8db38b7c7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211488"
---
# <a name="write-database-engine"></a>Write (データベース エンジン)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

書き込み のバイナリ表現を書き込みます **SqlHierarchyId** を渡されたに **BinaryWriter** です。 書き込み [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して呼び出すことができない です。 代わりに、CAST または CONVERT を使用してください。
  
## <a name="syntax"></a>構文  
  
```csharp
void Write( BinaryWriter w )
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*w*  
**BinaryWriter** オブジェクトをこのバイナリ表現 **hierarchyid** ノードが書き出されます。
  
## <a name="return-types"></a>戻り値の型  
**CLR の戻り値の型: void**
  
## <a name="remarks"></a>解説  
書き込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部で使用される 必要な場合など **からデータを読み込むときに、 hierarchyid** 列です。 Write は、**hierarchyid** と **varbinary** 間で変換が行われる場合も呼び出されます。
  
## <a name="examples"></a>例  
  
```csharp
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
```  
  
## <a name="see-also"></a>関連項目
[Read &#40;データベース エンジン&#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40;データベース エンジン&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid データ型メソッド リファレンス](./hierarchyid-data-type-method-reference.md)
  
