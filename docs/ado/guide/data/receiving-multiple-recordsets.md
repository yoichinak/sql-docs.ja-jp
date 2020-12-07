---
description: 複数のレコードセットの受信
title: 複数のレコードセットを受け取る |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: rothja
ms.author: jroth
ms.openlocfilehash: abac183f348553f30bf0cf5ed91725ef421afb3e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979973"
---
# <a name="receiving-multiple-recordsets"></a>複数のレコードセットの受信
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)では、複数の sql ステートメント (sql ステートメントごとに1つの**レコードセット**) を含む1つのコマンドに対して複数の**レコードセット**オブジェクトを返すことができます。 **レコードセット**が返される順序は、SQL ステートメントがコマンドテキストに配置される順序に従います。  
  
 Microsoft OLE DB Provider for SQL Server も、コマンドに COMPUTE 句が含まれている場合に複数の結果セットを ADO に返します。 たとえば、次の SQL ステートメントを含むコマンドは、2つの **レコードセット** オブジェクト (*ProductID*、 *ProductName*、 *UnitPrice*) の結果と、テーブル内のすべての製品の平均価格の結果を返します。  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 **NextRecordset**メソッドを使用して、2つのオブジェクトを列挙できます。  
  
 詳細については、「 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)」を参照してください。
