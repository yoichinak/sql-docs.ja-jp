---
description: Parameter オブジェクト
title: Parameter オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: rothja
ms.author: jroth
ms.openlocfilehash: 123ca1553ede61735565a6f82cb36b0035c56dcb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990173"
---
# <a name="parameter-object"></a>Parameter オブジェクト
パラメーター化クエリまたはストアドプロシージャに基づいて [Command](./command-object-ado.md) オブジェクトに関連付けられたパラメーターまたは引数を表します。  
  
## <a name="remarks"></a>解説  
 多くのプロバイダーがパラメーター化コマンドをサポートしています。 これらのコマンドは、必要なアクションが1回定義されていますが、変数 (またはパラメーター) を使用してコマンドの詳細を変更します。 たとえば、SQL の SELECT ステートメントでは、パラメーターを使用して WHERE 句の一致条件を定義し、別のステートメントを使用して SORT by 句の列名を定義することができます。  
  
 **パラメーター** オブジェクトは、パラメーター化クエリに関連付けられているパラメーター、またはストアドプロシージャの in/out 引数と戻り値を表します。 プロバイダーの機能によっては、 **パラメーター** オブジェクトの一部のコレクション、メソッド、またはプロパティが使用できないことがあります。  
  
 **Parameter**オブジェクトのコレクション、メソッド、およびプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado.md)プロパティを使用して、パラメーターの名前を設定または取得します。  
  
-   [Value](./value-property-ado.md)プロパティを使用して、パラメーターの値を設定または取得します。 **Value** は、 **Parameter** オブジェクトの default プロパティです。  
  
-   [属性](./attributes-property-ado.md)、[方向](./direction-property.md)、[有効桁数](./precision-property-ado.md)、 [numericscale](./numericscale-property-ado.md)、 [Size](./size-property-ado-parameter.md)、および[Type](./type-property-ado.md)プロパティを使用して、パラメーターの特性を設定または取得します。  
  
-   長いバイナリまたは文字データを、 [Appendchunk](./appendchunk-method-ado.md) メソッドを使用してパラメーターに渡します。  
  
-   [プロパティ](./properties-collection-ado.md)コレクションを使用して、プロバイダー固有の属性にアクセスします。  
  
 呼び出すストアドプロシージャまたはパラメーター化クエリに関連付けられているパラメーターの名前とプロパティがわかっている場合は、 [createparameter](./createparameter-method-ado.md) メソッドを使用して、適切なプロパティ設定を持つ **パラメーター** オブジェクトを作成し、 [Append](./append-method-ado.md) メソッドを使用 [してパラメーターコレクションに](./parameters-collection-ado.md) 追加することができます。 これにより、パラメーターコレクションの [Refresh](./refresh-method-ado.md) メソッドを呼び出さなくても、リソースを大量に消費する可能性のある操作であるプロバイダーからパラメーター情報を取得するため **に、パラメーター** の値を設定して返すことができます。  
  
 **パラメーター**オブジェクトは、スクリプト作成には安全ではありません。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Parameter オブジェクトのプロパティ、メソッド、およびイベント](./parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Command オブジェクト (ADO)](./command-object-ado.md)   
 [CreateParameter メソッド (ADO)](./createparameter-method-ado.md)   
 [Parameters コレクション (ADO)](./parameters-collection-ado.md)   
 [Properties コレクション (ADO)](./properties-collection-ado.md)