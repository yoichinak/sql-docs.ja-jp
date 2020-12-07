---
description: 集計関数、CALC 関数、NEW キーワード
title: 集計関数、CALC 関数、および NEW キーワード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b62e392325306bc358283874f4638077d8a4178
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991633"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>集計関数、CALC 関数、NEW キーワード
データシェイプは、次の関数をサポートしています。 操作対象の列を含むチャプターに割り当てられた名前は、 *チャプターエイリアス*です。  
  
 チャプターエイリアスは完全修飾することができます。各チャプター列名は、 *列名* を含む章に至るまで、ピリオドで区切られています。 たとえば、親章 chap1 に、amount 列を含む chap2 という子のチャプターが含まれている場合、修飾名は chap1 になります。  
  
|集計関数|説明|  
|-------------------------|-----------------|  
|SUM (*チャプターエイリアス*。*列名*)|指定された列のすべての値の合計を計算します。|  
|AVG (*チャプターエイリアス*。*列名*)|指定された列のすべての値の平均を計算します。|  
|MAX (*チャプターエイリアス)*。*列名*)|指定された列の最大値を計算します。|  
|MIN (*チャプターエイリアス)*。*列名*)|指定された列の最小値を計算します。|  
|COUNT (*chapter-alias*[.*列名*])|指定された別名の行数をカウントします。 列が指定されている場合、その列が Null 以外の行だけがカウントに含まれます。|  
|STDEV (*チャプターエイリアス*。*列名*)|指定された列の標準偏差を計算します。|  
|任意 (*チャプターエイリアス*。*列名*)|指定された列の値。 では、列の値がチャプター内のすべての行で同じ場合にのみ、予測可能な値が使用されます。<br /><br /> **メモ** 列に、チャプター内のすべての行に対して同じ値が含まれていない場合、SHAPE コマンドは任意の値を ANY 関数の値として返します。|  
  
|計算式|説明|  
|---------------------------|-----------------|  
|CALC (*式*)|任意の式を計算しますが、CALC 関数を含む **レコードセット** の行のみを計算します。 これらの [Visual Basic for Applications (VBA) 関数](./visual-basic-for-applications-functions.md) を使用する式はすべて許可されます。|  
  
|NEW キーワード|説明|  
|-----------------|-----------------|  
|新しい *フィールドの種類* [(*width* &#124; *scale* &#124; *precision* &#124; *error* [, *scale* &#124; *error*])]|指定した型の空の列を **レコードセット**に追加します。|  
  
 NEW キーワードで渡される *フィールド型* には、次のいずれかのデータ型を指定できます。  
  
|データ型の OLE DB|ADO データ型に相当するもの|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary、AdVarBinary、adLongVarBinary|  
|DBTYPE_STR|adChar、adVarChar、adLongVarChar|  
|DBTYPE_WSTR|adWChar、adVarWChar、adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 新しいフィールドの型が decimal (OLE DB、DBTYPE_DECIMAL、または ADO で adDecimal) の場合、有効桁数と小数点以下桁数の値を指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](./data-shaping-example.md)   
 [仮形の文法](./formal-shape-grammar.md)   
 [一般的な Shape コマンド](./shape-commands-in-general.md)