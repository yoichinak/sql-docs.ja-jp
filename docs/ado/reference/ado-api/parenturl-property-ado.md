---
description: ParentURL プロパティ (ADO)
title: ParentURL プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: rothja
ms.author: jroth
ms.openlocfilehash: e3a8323223f97034750c7e6bf7927ac87aefd3bd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990113"
---
# <a name="parenturl-property-ado"></a>ParentURL プロパティ (ADO)
現在の**レコード**オブジェクトの親[レコード](./record-object-ado.md)を指す絶対 URL 文字列を示します。  
  
## <a name="return-value"></a>戻り値  
 親**レコード**の URL を示す**文字列**値を返します。  
  
## <a name="remarks"></a>解説  
 **Parenturl**プロパティは、 **Record**オブジェクトを開くために使用されるソースによって異なります。 たとえば、 [ActiveConnection](./activeconnection-property-ado.md)プロパティによって参照されるディレクトリの相対パス名を含むソースで**レコード**を開くことができます。  
  
 "Second" が "first" の下に含まれるフォルダーであるとします。 次の構文を使用して、 **レコード** オブジェクトを開きます。  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 ここで、 `the` **parenturl** プロパティの値は `"https://first"` 、 **ActiveConnection**と同じです。  
  
 ソースには、のような絶対 URL を指定することもでき `"https://first/second"` ます。 **Parenturl**プロパティは `"https://first"` 、上記のレベルです `"second"` 。  
  
 このプロパティは、次の場合に null 値になることがあります。  
  
-   現在のオブジェクトの親がありません。たとえば、 **レコード** オブジェクトがディレクトリのルートを表しているとします。  
  
-   **レコード**オブジェクトは、URL で指定できないエンティティを表します。  
  
 このプロパティは読み取り専用です。  
  
> [!NOTE]
>  このプロパティは、 [Microsoft OLE DB Provider For Internet Publishing](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)などのドキュメントソースプロバイダーによってのみサポートされます。 詳細については、「 [レコードとプロバイダーが指定](../../guide/data/records-and-provider-supplied-fields.md)したフィールド」を参照してください。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
> [!NOTE]
>  現在のレコードに ADO **レコードセット**のデータレコードが含まれている場合、 **parenturl** プロパティにアクセスすると、url が不可能であることを示す実行時エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](./record-object-ado.md)