---
description: StructureColumn (DMX)
title: StructureColumn (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 43e02efd8594497ad4f3c02679a475531489141c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500782"
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指定したケースに対応する構造列の値、または指定したケースの入れ子になったテーブルのテーブル値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>引数  
 構造列-名前。  
 ケースまたは入れ子になったテーブルのマイニング構造列の名前。  
  
## <a name="result-type"></a>結果の種類  
 返される型は、パラメーターで参照されている列の型によって異なり \<structure column name> ます。 たとえば、参照されるマイニング構造列がスカラー値を含む場合、関数はスカラー値を返します。  
  
 参照されるマイニング構造列が入れ子になったテーブルの場合、関数はテーブル値を返します。 返されるテーブル値は、サブ SELECT ステートメントの FROM 句で使用できます。  
  
## <a name="remarks"></a>解説  
 この関数はポリモーフィックであり、SELECT 式リスト、WHERE 条件式、および ORDER BY 式など、式を使用できるステートメント内の任意の場所で使用できます。  
  
 マイニング構造内の列の名前は文字列値であるため、単一引用符で囲む必要があります (たとえば、 `StructureColumn('` **列 1**) `')` 。 同じ名前を持つ列が複数ある場合、名前は SELECT ステートメントが含まれるコンテキスト内で解決されます。  
  
 **StructureColumn**関数を使用してクエリから返される結果は、モデルにフィルターが存在することによって影響を受けます。 つまり、モデルフィルターは、マイニングモデルに含まれるケースを制御します。 したがって、構造列に対するクエリは、マイニングモデルで使用されたケースのみを返すことができます。 ケーステーブルと入れ子になったテーブルの両方に対するマイニングモデルフィルターの効果を示すコードサンプルについては、このトピックの「例」のセクションを参照してください。  
  
 DMX SELECT ステートメントでこの関数を使用する方法の詳細については、「 [SELECT FROM &#60;model&#62;」を参照してください。DMX&#41;&#40;ケース ](../dmx/select-from-model-cases-dmx.md) は [&#60;構造&#62; から選択します。ケース](../dmx/select-from-structure-cases.md)。  
  
## <a name="error-messages"></a>エラー メッセージ  
 次のセキュリティエラーは、親のマイニング構造に対するドリルスルー権限がユーザーに与えられていない場合に発生します。  
  
 '% {User/} ' ユーザーには、'% {model/} ' マイニングモデルの親マイニング構造にドリルスルーする権限がありません。  
  
 次のエラー メッセージは、無効な構造列名が指定された場合に表示されます。  
  
 '% {Structure/column-name/} ' マイニング構造列が、現在のコンテキスト (行% {line/}、列% {column/}) の '% {structure/} ' 親マイニング構造に見つかりませんでした。  
  
## <a name="examples"></a>例  
 これらの例では、次のマイニング構造を使用します。 マイニング構造には、とという2つの入れ子になったテーブル列が含まれることに注意して `Products` `Hobbies` ください。 `Hobbies` 列の入れ子になったテーブルには、入れ子になったテーブルのキーとして使用される単一列があります。 列の入れ子になったテーブル `Products` は、キー列と入力に使用されるその他の列の両方を含む、複雑な入れ子になったテーブルです。 次の例は、モデルですべての列を使用しない場合でも、さまざまな列を含めるようにデータマイニング構造を設計する方法を示しています。 これらの列の一部は、モデル レベルでパターンの汎用化に役立たない可能性がありますが、ドリルスルーには非常に有効です。  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 次に、次のコード例を使用して、作成した構造に基づいてマイニングモデルを作成します。  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>サンプルクエリ 1: マイニング構造から列を取得する  
 次のサンプル クエリでは、マイニング モデルの一部として定義されている列 `CustomerName` および `Age` が返されます。 ただし、このクエリでは、構造の一部であってもマイニング モデルの一部ではない `Age` 列も返されます。  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 30歳以上の顧客に対してケースを制限する行のフィルター処理は、モデルのレベルで行われることに注意してください。 したがって、この式は、構造データに含まれているが、モデルから使用されないケースを返しません。 モデルの作成に使用されるフィルター条件 () では、製品を購入した `EXISTS (Products)` 顧客のみにケースが制限されるため、このクエリによって返されないケースが構造に含まれる場合があります。  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>サンプルクエリ 2: 構造列にフィルターを適用する  
 次のサンプルクエリは、モデルの列と、および入れ子になったテーブルを返すだけでなく、 `CustomerName` `Age` `Products` モデルの一部ではない、入れ子になったテーブルの列の値も返し `Quantity` ます。  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 この例では、[構造] 列にフィルターを適用して、職業が "アーキテクト" () の顧客にケースを限定することに注意して `WHERE StructureColumn('Occupation') = 'Architect'` ください。 モデルフィルター条件は、モデルの作成時に常に適用されるので、テーブル内の条件を満たす行が少なくとも1つ含まれているケースのみ `Products` がモデルケースに含まれます。 そのため、入れ子になったテーブルのフィルター `Products` とケースのフィルターの両方 `('Occupation')` が適用されます。  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>サンプルクエリ 3: 入れ子になったテーブルから列を選択する  
 次のサンプル クエリでは、トレーニング ケースとして使用された顧客の名前がモデルから返されます。 このクエリでは、顧客ごとに、購入の詳細を含む入れ子になったテーブルも返されます。 モデルには列が含まれていますが、モデルでは `ProductName` 列の値は使用されません `ProductName` 。 このモデルでは、製品が通常の価格で購入されたかどうかのみを確認し `NOT``OnSale` ます。 このクエリでは、製品名を返すだけでなく、モデルに含まれていない購入数量も返されます。  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 マイニング モデルでドリルスルーが有効でない限り、`ProductName` 列または `Quantity` 列を返すことはできません。  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>サンプルクエリ 4: フィルター処理と入れ子になったテーブル列の取得  
 次のサンプルクエリは、マイニング構造に含まれているがモデルに含まれていないケースおよび入れ子になったテーブル列を返します。 モデルは既に `OnSale` 製品が存在するかどうかでフィルター処理されていますが、このクエリはマイニング構造列 `Quantity` にフィルターを追加します。  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
