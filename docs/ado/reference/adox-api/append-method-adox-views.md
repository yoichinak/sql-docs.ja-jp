---
description: Append メソッド (ADOX Views)
title: Append メソッド (ADOX Views) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 77682d479d65c7ccc0dd01fd1fd86627a580d8c5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985393"
---
# <a name="append-method-adox-views"></a>Append メソッド (ADOX Views)
新しい [ビュー](./view-object-adox.md) オブジェクトを作成し、 [Views](./views-collection-adox.md) コレクションに追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 作成するビューの名前を指定する **文字列** 値。  
  
 *コマンド*  
 作成するビューを表す ADO [コマンド](../ado-api/command-object-ado.md) オブジェクト。  
  
## <a name="remarks"></a>解説  
 **コマンド**オブジェクトで指定された名前と属性を使用して、データソースに新しいビューを作成します。  
  
 ユーザーが指定したコマンドテキストがビューではなくプロシージャを表している場合、その動作はプロバイダーに依存します。 プロバイダーがコマンドの永続化をサポートしていない場合、 **Append**は失敗します。  
  
> [!NOTE]
>  OLE DB Provider for Microsoft Jet を使用する場合、 **Views** collection **Append**メソッドを使用すると、*コマンド*パラメーターで**ビュー**ではなく**プロシージャ**を指定できます。 **プロシージャ**がデータソースに追加され、 **Views**コレクションに追加されます。 **追加**後、**プロシージャ**と**ビュー**のコレクションが更新されると、その**プロシージャ**は**views**コレクションに含まれなくなり、 **procedures**コレクションに表示されます。  
  
## <a name="applies-to"></a>適用対象  
 [Views コレクション (ADOX)](./views-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [Views Append メソッドの例 (VB)](./views-append-method-example-vb.md)   
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Groups)](./append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](./append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](./append-method-adox-keys.md)   
 [Append メソッド (ADOX Procedures)](./append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](./append-method-adox-users.md)