---
description: コマンド ストリーム
title: コマンドストリーム |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: rothja
ms.author: jroth
ms.openlocfilehash: 2ae54835836fecdfbf3b026fe9e6a701a5602d3d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991543"
---
# <a name="command-streams"></a>コマンド ストリーム
ADO では、常に **CommandText** プロパティによって指定された文字列形式のコマンド入力がサポートされていました。 また、ADO 2.7 以降では、コマンド入力に情報ストリームを使用することもできます。これを行うには、ストリームを **commandstream** プロパティに割り当てます。 ADO **ストリーム** オブジェクト、または COM **IStream** インターフェイスをサポートする任意のオブジェクトを割り当てることができます。  
  
 コマンドストリームの内容は ADO からプロバイダーに渡されるだけなので、この機能を使用するには、プロバイダーがストリームによるコマンド入力をサポートする必要があります。 たとえば、SQL Server では、Transact-sql の XML テンプレートまたは OpenXML 拡張機能の形式でクエリをサポートしています。  
  
 ストリームの詳細はプロバイダーによって解釈される必要があるため、 **言語** のプロパティを設定して、コマンドの言語を指定する必要があります。 **Dialect**の値は、プロバイダーによって定義される GUID を含む文字列です。 プロバイダーでサポートされている **言語** の有効な値の詳細については、プロバイダーのドキュメントを参照してください。  
  
## <a name="xml-template-query-example"></a>XML テンプレートのクエリ例  
 次の例は、VBScript で Northwind データベースに記述されています。  
  
 最初に、クエリストリームを格納するために使用される **ストリーム** オブジェクトを初期化して開きます。  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 クエリストリームの内容は、XML テンプレートクエリになります。  
  
 このテンプレートクエリには、タグの sql: prefix によって識別される XML 名前空間への参照が必要です \<sql:query> 。 SQL SELECT ステートメントは XML テンプレートの内容として含まれており、次のように文字列変数に割り当てられます。  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 次に、文字列をストリームに書き込みます。  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 AdoStreamQuery を、ADO**コマンド**オブジェクトの**commandstream**プロパティに割り当てます。  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 SQL Server OLE DB プロバイダーがコマンドストリームを解釈する方法を示す **コマンド言語言語を指定**します。 プロバイダー固有の GUID によって指定される言語:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 最後に、クエリを実行し、結果を **レコードセット** オブジェクトに返します。  
  
```  
Set objRS = adoCmd.Execute  
```
