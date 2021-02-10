---
description: ADO MD と ADO の併用
title: ADO MD | での ADO の使用Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: rothja
ms.author: jroth
ms.openlocfilehash: d6844590043e0f806381f35c3f74123c24a6dc30
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032164"
---
# <a name="using-ado-with-ado-md"></a>ADO MD と ADO の併用
ADO と ADO MD は関連がありますが、個別のオブジェクトモデルです。 ADO には、データソースに接続したり、コマンドを実行したり、表形式のデータとスキーマメタデータを表形式で取得したり、プロバイダーのエラー情報を表示したりするためのオブジェクトが用意されています。 ADO MD には、多次元データを取得し、多次元スキーマメタデータを表示するためのオブジェクトが用意されています。  
  
 .MDP を使用する場合は、アプリケーションで ADO、ADO MD、またはその両方を使用することを選択できます。 プロジェクト内で両方のライブラリを参照することにより、.MDP によって提供される機能に完全にアクセスできるようになります。  
  
 多くの場合、コンシューマーは多次元データセットのフラット化された表形式ビューを取得すると便利です。 これを行うには、ADO [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトを使用します。 ADO MD **セル** セットのソースとしてではなく、_ * レコードセット * * の [Open](../../reference/ado-api/open-method-ado-recordset.md)メソッドの ***source** _ パラメーターとして、[セルセット](../../reference/ado-md-api/cellset-object-ado-md.md)のソースを指定します。  
  
 また、オブジェクトの階層としてではなく、表形式ビューでスキーマメタデータを表示すると便利な場合もあります。 [接続](../../reference/ado-api/connection-object-ado.md)オブジェクトの ADO [OpenSchema](../../reference/ado-api/openschema-method.md)メソッドを使用すると、スキーマ情報を含む **レコードセット** をユーザーが開くことができます。 **_ OpenSchema メソッドの _QueryType_*_ パラメーター*** には、具体的には Mdps に関連する複数の [schemaenum](../../reference/ado-api/schemaenum.md)値があります。 これらの値は次のとおりです。  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adschemameasame**  
  
-   **adSchemaMembers**  
  
 ADO MD のプロパティまたはメソッドで ADO 列挙値を使用するには、プロジェクトで ADO ライブラリと ADO MD ライブラリの両方を参照する必要があります。 たとえば、ADO MD [State](../../reference/ado-md-api/state-property-ado-md.md)プロパティで ADO **adstate** 列挙値を使用できます。 ライブラリへの参照を設定する方法の詳細については、開発ツールのドキュメントを参照してください。  
  
 ADO のオブジェクトとメソッドの詳細については、「 [ADO API リファレンス](../../reference/ado-api/ado-api-reference.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ADO MD オブジェクトモデル](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多次元) (ADO MD)](./ado-multidimensional-ado-md.md)   
 [多次元スキーマとデータの概要](./overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD を使用したプログラミング](./programming-with-ado-md.md)   
 [多次元データの操作](./working-with-multidimensional-data.md)