---
description: サポートされている機能を特定する
title: サポートされている内容の確認 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: rothja
ms.author: jroth
ms.openlocfilehash: c2caaf9e708b9a9fccd728472c7b13857978fdbe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991383"
---
# <a name="determining-what-is-supported"></a>サポートされている機能を特定する
**サポート**メソッドは、指定された**レコードセット**オブジェクトが特定の種類の機能をサポートするかどうかを判断するために使用されます。 次の構文があります。  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>解説  
 **サポート**メソッドは、プロバイダーがカーソルオプション引数によって識別されるすべての機能をサポートしているかどうかを示すブール値を返します。 **サポート**メソッドを使用して、**レコードセット**オブジェクトがサポートする機能の種類を決定できます。 対応する定数が*カーソルオプション*に含まれる機能を**レコードセット**オブジェクトがサポートしている場合、 **supports**メソッドは**True**を返します。 それ以外の場合は **False**を返します。  
  
 **Supports**メソッドを使用して、**レコードセット**オブジェクトが新しいレコードの追加、ブックマークの使用、**検索**メソッドの使用、スクロールの使用、**インデックス**プロパティの使用、およびバッチ更新の実行を行うことができるかどうかを確認できます。 定数とその意味の完全な一覧については、「 [カーソルオプション列挙型](../../reference/ado-api/cursoroptionenum.md)」を参照してください。  
  
 **サポート**メソッドは特定の機能に対して**True**を返す場合がありますが、プロバイダーがすべての状況でこの機能を使用できるようにすることは保証されません。 **サポート**メソッドは、特定の条件が満たされていることを前提として、プロバイダーが指定された機能をサポートできるかどうかを単純に返します。 たとえば、 **サポート** されているメソッドは、 **レコードセット** オブジェクトが更新をサポートしていることを示している場合があります。これは、カーソルが複数のテーブルの結合に基づいている場合でも、更新できない列もあります。