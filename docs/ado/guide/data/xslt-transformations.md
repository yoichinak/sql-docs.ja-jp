---
description: XSLT 変換
title: XSLT 変換 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: rothja
ms.author: jroth
ms.openlocfilehash: a704245d166b0d53cb7ed17e6a5f8cdfa32d9447
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978803"
---
# <a name="xslt-transformations"></a>XSLT 変換
生成された XML に XSLT を適用して、別の形式に変換することができます。 ADO で XML 形式を理解することは、よりわかりやすい形式に変換できる XSLT テンプレートの開発に役立ちます。  
  
 たとえば、レコードセットの各行は、rs: data 要素内の z: row 要素として保存されていることがわかります。 同様に、レコードセットの各フィールドは、この要素の属性と値のペアとして保存されます。  
  
## <a name="remarks"></a>解説  
 次の XSLT スクリプトは、前のセクションで示した XML に適用して、ブラウザーに表示される HTML テーブルに変換できます。  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 XSLT は、ADO Save メソッドによって生成された XML ストリームを HTML テーブルに変換します。このテーブルでは、レコードセットの各フィールドがテーブル見出しと共に表示されます。 テーブルの見出しと行にも、異なるフォントと色が割り当てられます。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)