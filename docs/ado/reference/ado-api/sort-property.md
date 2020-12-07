---
description: Sort プロパティ
title: Sort プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
author: rothja
ms.author: jroth
ms.openlocfilehash: 9397d99d2d020fcf2c703bd96420ee4af4b1a610
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988993"
---
# <a name="sort-property"></a>Sort プロパティ
[レコードセット](./recordset-object-ado.md)が並べ替えられる1つ以上のフィールド名と、各フィールドを昇順と降順のどちらで並べ替えるかを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 並べ替えの対象となる**レコードセット**内のフィールド名を示す**文字列**値を設定または返します。 各名前はコンマで区切られます。オプションで、空白とキーワード **ASC**を使用します。この場合、フィールドは昇順に並べ替えられ、 **DESC**はフィールドが降順に並べ替えられます。 既定では、キーワードが指定されていない場合、フィールドは昇順に並べ替えられます。  
  
## <a name="remarks"></a>解説  
 このプロパティでは、 [カーソル位置](./cursorlocation-property-ado.md) プロパティを **adUseClient**に設定する必要があります。 インデックスがまだ存在しない場合は、 **Sort** プロパティで指定された各フィールドに対して一時インデックスが作成されます。  
  
 データは物理的には再配置されませんが、単純にインデックスで指定された順序でアクセスされるため、並べ替え操作は効率的です。  
  
 **Sort**プロパティの値が空の文字列以外の場合、**並べ替え**プロパティの順序は、**レコードセット**を開くために使用される SQL ステートメントに含まれる**order BY**句で指定されている順序よりも優先されます。  
  
 **Sort**プロパティにアクセスする前に、**レコードセット**を開く必要はありません。**レコード**セットオブジェクトがインスタンス化された後、いつでも設定できます。  
  
 **Sort**プロパティを空の文字列に設定すると、行が元の順序にリセットされ、一時インデックスが削除されます。 既存のインデックスは削除されません。  
  
 **レコードセット**に*firstName*、 *middleInitial*、 *lastName*という3つのフィールドが含まれているとします。 [ **並べ替え** ] プロパティを "" に設定します。この文字列は、 `lastName DESC, firstName ASC` **レコードセット** を姓で降順に並べ替え、名を昇順に並べ替えます。 ミドルネームのイニシャルは無視されます。  
  
 "ASC" または "DESC" という名前のフィールドは使用できません。これらの名前は、キーワード **ASC** および **DESC**と競合しています。 **レコードセット**を返すクエリで AS キーワードを使用する**と**、競合する名前を持つフィールドの別名を作成できます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Sort プロパティの例 (VB)](./sort-property-example-vb.md)   
 [Sort プロパティの例 (VC + +)](./sort-property-example-vc.md)   
 [Optimize プロパティ-動的 (ADO)](./optimize-property-dynamic-ado.md)   
 [SortColumn プロパティ (RDS)](../rds-api/sortcolumn-property-rds.md)   
 [SortDirection プロパティ (RDS)](../rds-api/sortdirection-property-rds.md)