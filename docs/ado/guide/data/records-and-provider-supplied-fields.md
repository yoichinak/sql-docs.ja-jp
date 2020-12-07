---
description: レコードとプロバイダーが指定したフィールド
title: レコードとプロバイダーが指定したフィールド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: rothja
ms.author: jroth
ms.openlocfilehash: 7cc7b8c4fb0116f96a2470a7161f9fbd30c7efb9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979953"
---
# <a name="records-and-provider-supplied-fields"></a>レコードとプロバイダーが指定したフィールド
[Record](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトが開かれている場合、そのソースは、開いている[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)の現在の行、絶対 url、または開いている[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトと組み合わせた相対 url にすることができます。  
  
 **レコードがレコード****セット**から開かれた場合、**レコード**オブジェクト[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクションには、レコード**セット**のすべてのフィールドに加えて、基になるプロバイダーによって追加されたすべてのフィールドが含まれます。  
  
 プロバイダーは、 **レコード**の補助特性として機能する追加のフィールドを挿入する場合があります。 その結果、**レコード**は、レコード**セット**全体またはレコード**セット**の別の行から派生した**レコード**ではなく、一意のフィールドを持つことができます。  
  
 たとえば、電子メールデータソースから派生した **レコードセット** のすべての行に、From、To、Subject などの列が含まれている場合があります。 そのレコード**セット**から派生した**レコード**のフィールドは同じになります。 ただし、 **レコード** には、添付ファイルや cc (カーボンコピー) など、その **レコード**によって表される特定のメッセージに固有の他のフィールドが存在する場合もあります。  
  
 **レコードオブジェクトと**レコード**セット**の現在の行のフィールドは同じですが、**レコード**および**レコードセット**オブジェクトのメソッドとプロパティが異なるため、これらは異なります。  
  
 **レコード**とレコード**セット**によって共通して保持されているフィールドは、どちらのオブジェクトでも変更できます。 ただし、 **レコード** オブジェクトでフィールドを削除することはできませんが、基になるプロバイダーでは、フィールドを null に設定することがサポートされている場合があります。  
  
 **レコード**を開いた後、プログラムを使用してフィールドを追加できます。 追加したフィールドを削除することもできますが、元の **レコードセット**からフィールドを削除することはできません。  
  
 また、URL から直接 **レコード** オブジェクトを開くこともできます。 この場合、 **レコード** に追加されるフィールドは、基になるプロバイダーによって異なります。 現在、ほとんどのプロバイダーは、 **レコード**によって表されるエンティティを記述するフィールドのセットを追加します。 エンティティが、単純ファイルなどのバイトストリームで構成されている場合は、通常、**レコード**から[ストリーム](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクトを開くことができます。  
  
## <a name="special-fields-for-document-source-providers"></a>ドキュメントソースプロバイダーの特別なフィールド  
 *ドキュメントソースプロバイダー*と呼ばれる特殊なプロバイダーのクラスは、フォルダーとドキュメントを管理します。 **レコード**オブジェクトがドキュメントを表す場合、または**レコードセット**オブジェクトがドキュメントのフォルダーを表す場合、ドキュメントソースプロバイダーは、実際のドキュメントそのものではなく、ドキュメントの特性を記述するフィールドの一意のセットをそれらのオブジェクトに挿入します。 通常、1つのフィールドには、ドキュメントを表す **ストリーム** への参照が含まれます。  
  
 これらのフィールドは、リソース **レコード** または **レコードセット** を構成し、 [付録 a: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)でサポートされている特定のプロバイダーに対して一覧表示されます。  
  
 2つの定数は、リソース**レコード**または**レコードセット**の**フィールド**コレクションのインデックスを作成して、よく使用されるフィールドのペアを取得します。 **Field**オブジェクトの[Value](../../../ado/reference/ado-api/value-property-ado.md)プロパティは、必要なコンテンツを返します。  
  
-   **Addefaultstream**定数でアクセスされるフィールドには、**レコード**または**レコードセット**オブジェクトに関連付けられた既定のストリームが含まれています。 プロバイダーは、オブジェクトに既定のストリームを割り当てます。  
  
-   **AdRecordURL**定数でアクセスされるフィールドには、ドキュメントを識別する絶対 URL が含まれています。  
  
 ドキュメントソースプロバイダーは、**レコード**および**フィールド**オブジェクトの[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションをサポートしていません。 このようなオブジェクトの場合、 **Properties** コレクションの内容は null になります。  
  
 ドキュメントソースプロバイダーは、 **Datasource 型** などのプロバイダー固有のプロパティを追加して、ドキュメントソースプロバイダーであるかどうかを識別できます。 プロバイダーの種類を確認する方法の詳細については、プロバイダーのドキュメントを参照してください。  
  
## <a name="resource-recordset-columns"></a>リソースレコードセットの列  
 *リソースレコードセット*は、次の列で構成されます。  
  
|列名|Type|説明|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|読み取り専用。 リソースの URL を示します。|  
|RESOURCE_PARENTNAME|AdVarWChar|読み取り専用。 親レコードの絶対 URL を示します。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|読み取り専用。 PARENTNAME と PARSENAME の連結であるリソースの絶対 URL を示します。|  
|RESOURCE_ISHIDDEN|AdBoolean|リソースが非表示の場合は True。 行が返されるのは、行セットを作成するコマンドが RESOURCE_ISHIDDEN が True の行を明示的に選択した場合だけです。|  
|RESOURCE_ISREADONLY|AdBoolean|リソースが読み取り専用の場合は True。 DBBINDFLAG_WRITE を使用してこのリソースを開こうとすると、DB_E_READONLY で失敗します。 このプロパティは、リソースが読み取り用に開かれている場合でも編集できます。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|ドキュメントが使用されている可能性があることを示します。たとえば、弁護士の brief などです。 これは、ドキュメントの作成に使用された Office テンプレートに対応する場合があります。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|ドキュメントの MIME の種類を示します。 "" などの形式を示し `text/html` ます。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|コンテンツが格納される言語を示します。|  
|RESOURCE_CREATIONTIME|adFileTime|読み取り専用。 リソースが作成された時刻を含む FILETIME 構造体を示します。 時刻は協定世界時 (UTC) 形式で報告されます。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|読み取り専用。 リソースが最後にアクセスされた時刻を含む FILETIME 構造体を示します。 時刻は UTC 形式です。 プロバイダーがこの時間メンバーをサポートしていない場合、FILETIME メンバーは0になります。|  
|RESOURCE_LASTWRITETIME|AdFileTime|読み取り専用。 リソースが最後に書き込まれた時刻を含む FILETIME 構造体を示します。 時刻は UTC 形式です。 プロバイダーがこの時間メンバーをサポートしていない場合、FILETIME メンバーは0になります。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|読み取り専用。 リソースの既定のストリームのサイズ (バイト単位) を示します。|  
|RESOURCE_ISCOLLECTION|AdBoolean|読み取り専用。 リソースがディレクトリなどのコレクションである場合は True。 リソースが単純なファイルの場合は False。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|リソースが構造化ドキュメントである場合は True。 リソースが構造化ドキュメントでない場合は False。 コレクションまたは単純なファイルを指定できます。|  
|DEFAULT_DOCUMENT|AdVarWChar|読み取り専用。 このリソースに、フォルダーまたは構造化ドキュメントの既定の単純ドキュメントへの URL が含まれていることを示します。 リソースから既定のストリームが要求されるときに使用されます。 単純なファイルの場合、このプロパティは空白になります。|  
|CHAPTERED_CHILDREN|AdChapter|読み取り専用。 省略可能。 リソースの子を含む行セットのチャプターを示します。 ( *インターネット発行用の OLE DB プロバイダー* では、この列は使用されません)。|  
|RESOURCE_DISPLAYNAME|AdVarWChar|読み取り専用。 リソースの表示名を示します。|  
|RESOURCE_ISROOT|AdBoolean|読み取り専用。 リソースがコレクションまたは構造化ドキュメントのルートである場合は True。|  
  
## <a name="see-also"></a>参照  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
