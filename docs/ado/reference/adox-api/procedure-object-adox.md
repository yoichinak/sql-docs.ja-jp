---
description: Procedure オブジェクト (ADOX)
title: プロシージャオブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedure
helpviewer_keywords:
- Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
author: rothja
ms.author: jroth
ms.openlocfilehash: b41e83033ab86810c4e26ff3c15fa4d9d1ea97ae
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983633"
---
# <a name="procedure-object-adox"></a>Procedure オブジェクト (ADOX)
ストアドプロシージャを表します。 ADO [コマンド](../ado-api/command-object-ado.md) オブジェクトと共に使用する場合、 **プロシージャ** オブジェクトを使用して、ストアドプロシージャの追加、削除、または変更を行うことができます。  
  
## <a name="remarks"></a>解説  
 **プロシージャ**オブジェクトを使用すると、プロバイダーの "create Procedure" 構文を知らない場合や使用しなくても、ストアドプロシージャを作成できます。  
  
 **プロシージャ**オブジェクトのプロパティを使用すると、次の操作を実行できます。  
  
-   [Name](./name-property-adox.md)プロパティを使用してプロシージャを識別します。  
  
-   [Command](./command-property-adox.md)プロパティを使用してプロシージャを作成または実行するために使用できる ADO**コマンド**オブジェクトを指定します。  
  
-   [DateCreated](./datecreated-property-adox.md)プロパティと[DateModified](./datemodified-property-adox.md)プロパティを使用して日付情報を返します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Procedure オブジェクトのプロパティ、メソッド、およびイベント](./procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Command プロパティと CommandText プロパティの例 (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Parameters コレクション、Command プロパティの例 (VB)](./parameters-collection-command-property-example-vb.md)   
 [Procedures Append メソッドの例 (VB)](./procedures-append-method-example-vb.md)   
 [Procedures Delete メソッドの例 (VB)](./procedures-delete-method-example-vb.md)   
 [Procedures コレクション (ADOX)](./procedures-collection-adox.md)