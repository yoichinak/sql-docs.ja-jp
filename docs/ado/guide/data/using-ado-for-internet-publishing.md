---
description: インターネットへの発行に ADO を使用する
title: インターネット発行に ADO を使用する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: rothja
ms.author: jroth
ms.openlocfilehash: 774ff9b0728d362822c72047b573ab9def944d18
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979037"
---
# <a name="using-ado-for-internet-publishing"></a>インターネットへの発行に ADO を使用する
[インターネット発行用の OLE DB プロバイダーは、](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) ADO を使用して異種データにアクセスする具体的な例を示しています。 このセクションの例は、インターネット公開プロバイダーの使用に固有のものですが、他のプロバイダーで ADO を電子メールストアのプロバイダーなどの異種データに対して使用する場合は、このような原則が似ています。  
  
## <a name="urls"></a>URL  
 接続文字列の代わりに Uniform Resource locator (Url) を使用して、データソースとファイルやディレクトリの場所を指定できます。 既存の [接続](../../../ado/reference/ado-api/connection-object-ado.md) および **レコードセット** オブジェクトと、 **レコード** オブジェクトおよび **ストリーム** オブジェクトで url を使用できます。  
  
 Url の使用方法の詳細については、「 [絶対 url と相対 url](../../../ado/guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="record-fields"></a>レコードフィールド  
 異種データと同種データの違いは、前者の場合、データの各行 (または **レコード**) は、異なる列または **フィールド**のセットを持つことができるという点です。 同種データの場合、各行の列セットは同じになります。 インターネット公開プロバイダーに固有のフィールドの詳細については、「 [レコード」および「プロバイダーが提供する追加フィールド](../../../ado/guide/data/records-and-provider-supplied-fields.md)」を参照してください。  
  
### <a name="appending-new-fields"></a>新しいフィールドの追加  
 いくつかの ADO オブジェクトが、 **レコード** オブジェクトおよび **ストリーム** オブジェクトと共に機能するように拡張されています。  
  
-   [フィールドオブジェクトを](../../../ado/reference/ado-api/field-object.md)作成してコレクションに追加する[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクション[追加](../../../ado/reference/ado-api/append-method-ado.md)メソッドは、**フィールド**の値を指定することもできます。  
  
-   [Update](../../../ado/reference/ado-api/update-method.md)メソッドは、コレクションへのフィールドの追加または削除を終了します。  
  
-   **Append**メソッドの代替手段として、未定義のフィールドまたは以前に削除されたフィールドに値を割り当てることにより、フィールドを作成できます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [インターネットへの発行のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [絶対 URL と相対 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [レコードとプロバイダーが指定したフィールド](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>参照  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 履歴](../../../ado/guide/ado-history.md)
