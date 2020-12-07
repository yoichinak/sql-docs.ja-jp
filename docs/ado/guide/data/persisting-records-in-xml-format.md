---
description: レコードを XML 形式で保持する
title: XML 形式でのレコードの保持 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 31512fd9843ae5ff15fc2f7c6981fccdc926dbb5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980063"
---
# <a name="persisting-records-in-xml-format"></a>レコードを XML 形式で保持する
ADTG 形式と同様に、XML 形式の **レコードセット** の永続化は、Microsoft OLE DB の永続化プロバイダーと共に実装されます。 このプロバイダーは、ADO によって生成されたスキーマ情報を格納する、保存されている XML ファイルまたはストリームから、順方向専用の読み取り専用の行セットを生成します。 同様に、ADO **レコードセット**を取得し、XML を生成して、COM **IStream** インターフェイスを実装するファイルまたは任意のオブジェクトに保存することもできます。 (実際には、ファイルは、 **IStream**をサポートするオブジェクトの別の例にすぎません)。バージョン2.5 以降では、ADO は Microsoft XML Parser (MSXML) を使用して XML を **レコードセット**に読み込みます。そのため msxml.dll が必要です。  
  
> [!NOTE]
>  階層的な **レコードセット** (データ図形) を XML 形式に保存する際には、いくつかの制限が適用されます。 階層 **レコードセット** に保留中の更新が含まれている場合は XML に保存できません。また、パラメーター化された階層 **レコードセット**を保存することもできません。 詳細については、「フィルター処理された [レコードセットと階層レコードセットの永続](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)化  
  
 データを XML に永続化し、ADO を使用して再度読み込む方法としては、それぞれ **Save** メソッドと **Open** メソッドを使用する方法が最も簡単です。 次の ADO コード例 **は、titles テーブルの** データを sav という名前のファイルに保存する方法を示しています。  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO では、 **レコードセット** オブジェクト全体が常に保持されます。 **Recordset**オブジェクトの行のサブセットを保持する場合は、**フィルター**メソッドを使用して行を絞り込むか、選択句を変更します。 ただし、フィルターメソッドを使用して行のサブセットを保存するには、クライアント側のカーソル (**cursor location**adUseClient) を使用して**レコードセット**オブジェクトを開く必要があり  =  **adUseClient** **Filter**ます。 たとえば、文字 "b" で始まるタイトルを取得するには、開いている **レコードセット** オブジェクトにフィルターを適用できます。  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO は常にクライアントカーソルエンジンの行セットを使用して、永続化プロバイダーによって生成される順方向専用データの上にスクロール可能な bookmarkable **Recordset** オブジェクトを生成します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [XML 保存形式](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [名前空間](../../../ado/guide/data/namespaces.md)  
  
-   [スキーマ セクション](../../../ado/guide/data/schema-section.md)  
  
-   [データ セクション](../../../ado/guide/data/data-section.md)  
  
-   [XML での階層レコードセット](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [XML でのレコードセットの動的プロパティ](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT 変換](../../../ado/guide/data/xslt-transformations.md)  
  
-   [XML DOM オブジェクトへの保存](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML のセキュリティに関する考慮事項](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [XML レコードセットの保持シナリオ](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
