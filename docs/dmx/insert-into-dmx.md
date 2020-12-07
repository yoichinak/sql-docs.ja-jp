---
description: INSERT INTO (DMX)
title: INSERT INTO (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 37a7a0e8be59136eb3ab6e0454c7910b9c9e3198
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726163"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指定されたデータマイニングオブジェクトを処理します。 マイニングモデルとマイニング構造の処理の詳細については、「 [データマイニング&#41;&#40;処理の要件と考慮事項 ](/analysis-services/data-mining/processing-requirements-and-considerations-data-mining)」を参照してください。  
  
 マイニング構造が指定されている場合、ステートメントはマイニング構造とそれに関連付けられているすべてのマイニングモデルを処理します。 マイニングモデルが指定されている場合、ステートメントはマイニングモデルだけを処理します。  
  
## <a name="syntax"></a>構文  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデル識別子。  
  
 *データ*  
 構造体識別子。  
  
 *マップされたモデル列*  
 列の識別子と入れ子になった識別子のコンマ区切りのリストです。  
  
 *source data query*  
 プロバイダー定義形式のソースクエリ。  
  
## <a name="remarks"></a>解説  
 **マイニングモデル**または**マイニング構造**を指定しない場合、は [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 名前に基づいてオブジェクトの種類を検索し、正しいオブジェクトを処理します。 サーバーに同じ名前のマイニング構造とマイニングモデルが含まれている場合は、エラーが返されます。  
  
 2番目の構文形式を使用して、をに挿入 *\<object>* します。COLUMN_VALUES、モデルをトレーニングしなくても、モデル列にデータを直接挿入できます。 この方法では、階層または順序付けられた列を含むデータセットを操作する場合に便利な簡潔な順序で列データをモデルに提供します。  
  
 **INSERT INTO**をマイニングモデルまたはマイニング構造と共に使用し、引数と引数を省略した場合、 \<mapped model columns> \<source data query> 既に存在するバインドを使用して、ステートメントは**processdefault**のように動作します。 バインドが存在しない場合、ステートメントはエラーを返します。 **Processdefault**の詳細については、「[処理オプションと設定 &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)」を参照してください。 構文の例を次に示します。  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 **マイニングモデル**を指定し、マップされた列とソースデータクエリを指定すると、モデルと関連する構造が処理されます。  
  
 次の表は、オブジェクトの状態に依存する、異なる形式のステートメントの結果について示しています。  
  
|ステートメント|オブジェクトの状態|結果|  
|---------------|----------------------|------------|  
|マイニングモデルへの挿入*\<model>*|マイニング構造が処理されます。|マイニング モデルは処理されます。|  
||マイニング構造は未処理です。|マイニング モデルとマイニング構造は処理されます。|  
||マイニング構造には、追加のマイニングモデルが含まれています。|処理は失敗します。 構造と、関連するマイニングモデルを再処理する必要があります。|  
|マイニング構造への挿入*\<structure>*|マイニング構造が処理または処理されていません。|マイニング構造と関連するマイニングモデルが処理されます。|  
|*\<model>* ソースクエリを含むマイニングモデルの挿入<br /><br /> or<br /><br /> *\<structure>* ソースクエリを含むマイニング構造への挿入|構造またはモデルのどちらかが既に内容に含まれます。|処理は失敗します。 この操作を実行する前に、[ [&#40;DMX&#41;の削除 ](../dmx/delete-dmx.md)] を使用してオブジェクトをクリアする必要があります。|  
  
## <a name="mapped-model-columns"></a>マップされたモデル列  
 要素を使用することにより、 \<mapped model columns> データソースの列をマイニングモデルの列にマップできます。 \<mapped model columns>要素には、次の形式があります。  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 **SKIP**を使用すると、ソースクエリに存在する必要があるが、マイニングモデルに存在しない特定の列を除外できます。 SKIP は、入力行セットに含まれる列を制御できない場合に便利です。 独自の OPENQUERY を作成する場合は、SKIP を使用するのではなく、[列の選択] の一覧から列を除外することをお勧めします。  
  
 SKIP は、入力行セットの列が結合を実行するために必要であるが、その列がマイニング構造で使用されていない場合にも便利です。 一般的な例として、入れ子になったテーブルを含むマイニング構造とマイニングモデルがあります。 この構造の入力行セットには、SHAPE 句を使用して階層的な行セットを作成するために使用される外部キー列が含まれますが、外部キー列がモデルで使用されることはほとんどありません。  
  
 SKIP の構文では、対応するマイニング構造列がない入力行セットの個々の列の位置に SKIP を挿入する必要があります。 たとえば、次の入れ子になったテーブルの例では、APPEND 句で OrderNumber を選択して、結合を指定するために関連付け句で使用できるようにする必要があります。ただし、マイニング構造の入れ子になったテーブルに OrderNumber データを挿入する必要はありません。 そのため、この例では、INSERT INTO 引数で OrderNumber ではなく SKIP キーワードを使用しています。  
  
## <a name="source-data-query"></a>ソースデータクエリ  
 要素には \<source data query> 、次のデータソースの種類を含めることができます。  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **オート**  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]行セットを返すクエリ  
  
 データソースの種類の詳細については、「 [&#60;source data query&#62;](../dmx/source-data-query.md)」を参照してください。  
  
## <a name="basic-example"></a>基本的な例  
 次の例では、 **OPENQUERY** を使用して、データベース内の対象メーリングデータに基づいて Naive Bayes モデルをトレーニングし [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] ます。  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>入れ子になったテーブルの例  
 次の例では、 **図形** を使用して、入れ子になったテーブルを含むアソシエーションマイニングモデルをトレーニングします。 最初の行には、 **SHAPE_APPEND**ステートメントで必要ながマイニングモデルで使用されていない、 **SKIP**の代わりに ordernumber が含まれていることに注意してください。  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
