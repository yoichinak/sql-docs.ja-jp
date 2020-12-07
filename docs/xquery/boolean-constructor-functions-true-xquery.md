---
title: true 関数 (XQuery) |Microsoft Docs
description: ブール値 True を返す XQuery 関数 true () について説明します。
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 8dc3582cb34c80f488005f5a2eaf1c6022c5e1be
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035795"
---
# <a name="boolean-constructor-functions---true-xquery"></a>ブール値コンストラクター関数 - true (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  xs:boolean 値 True を返します。 これは、`xs:boolean("1")` と同じです。  
  
## <a name="syntax"></a>構文  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. XQuery 論理関数 true() の使用  
 次の例では、型指定されていない **xml** 変数をクエリします。 **Value ()** メソッドの式は、"aaa" が属性値の場合にブール値**true ()** を返します。 **Xml**データ型の**value ()** メソッドは、ブール値をビットに変換して返します。  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 次の例では、型指定された **xml** 列に対してクエリが指定されています。 式は、 `if` <> 要素の型指定されたブール値をチェック `ROOT` し、それに従って構築された XML を返します。 この例では、次の処理を実行します。  
  
-   Xs: boolean 型の <> 要素を定義する XML スキーマコレクションを作成し `ROOT` ます。  
  
-   XML スキーマコレクションを使用して、型指定された **xml** 列を含むテーブルを作成します。  
  
-   XML インスタンスを列に保存し、クエリを実行します。  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>参照  
 [ブール型コンストラクター関数 &#40;XQuery&#41;](./xquery-functions-against-the-xml-data-type.md)  
  
