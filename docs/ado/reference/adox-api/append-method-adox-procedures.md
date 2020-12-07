---
description: Append メソッド (ADOX Procedures)
title: Append メソッド (ADOX Procedures) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: rothja
ms.author: jroth
ms.openlocfilehash: 2bc35ccb48211f6a849dc102ba2d1806a79b2426
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985463"
---
# <a name="append-method-adox-procedures"></a>Append メソッド (ADOX Procedures)
[Procedures](./procedures-collection-adox.md)コレクションに新しい[プロシージャ](./procedure-object-adox.md)オブジェクトを追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 作成および追加するプロシージャの名前を示す **文字列** 値です。  
  
 *コマンド*  
 作成および追加するプロシージャを表す ADO [コマンド](../ado-api/command-object-ado.md) オブジェクト。  
  
## <a name="remarks"></a>解説  
 **コマンド**オブジェクトで指定された名前と属性を使用して、データソースに新しいプロシージャを作成します。  
  
 ユーザーが指定したコマンドテキストがプロシージャではなくビューを表している場合、その動作は使用されているプロバイダーによって異なります。 プロバイダーがコマンドの永続化をサポートしていない場合、 **Append**は失敗します。  
  
> [!NOTE]
>  OLE DB Provider for Microsoft Jet を使用する場合、 **Procedures** collection **Append**メソッドを使用すると、*コマンド*パラメーターで**プロシージャ**ではなく**ビュー**を指定できます。 **ビュー**がデータソースに追加され、**プロシージャ**コレクションに追加されます。 **追加**後、**プロシージャ**コレクションと**ビュー**コレクションが更新されると、その**ビュー**は**procedures**コレクションに含まれなくなり、 **views**コレクションに表示されます。  
  
## <a name="applies-to"></a>適用対象  
 [Procedures コレクション (ADOX)](./procedures-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [Procedures Append メソッドの例 (VB)](./procedures-append-method-example-vb.md)   
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Groups)](./append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](./append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](./append-method-adox-keys.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](./append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](./append-method-adox-views.md)