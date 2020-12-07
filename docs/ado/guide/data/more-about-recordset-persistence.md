---
description: レコードセットの保持に関する詳細情報
title: レコードセット永続化の詳細 |Microsoft Docs
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
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: rothja
ms.author: jroth
ms.openlocfilehash: 1dca646b07c441a4fccd617723aba98536f1a7e1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980333"
---
# <a name="more-about-recordset-persistence"></a>レコードセットの保持に関する詳細情報
ADO レコードセットオブジェクトは、 [Save](../../reference/ado-api/save-method.md)メソッドを使用して、**レコードセット**オブジェクトの内容をファイルに格納することをサポートしています。 永続的に格納されたファイルは、ローカルドライブ、サーバー、または Web サイト上の URL として存在する場合があります。 その後、**レコードセット**オブジェクトの[Open](../../reference/ado-api/open-method-ado-recordset.md)メソッドまたは[Connection](../../reference/ado-api/connection-object-ado.md)オブジェクトの[Execute](../../reference/ado-api/execute-method-ado-connection.md)メソッドのいずれかを使用して、ファイルを復元できます。  
  
 さらに、 [GetString](../../reference/ado-api/getstring-method-ado.md) メソッドは、 **レコードセット** オブジェクトを、指定した文字で区切られた列と行を含む形式に変換します。  
  
 **レコードセット**を永続化するには、まず、ファイルに格納できる形式に変換します。 **レコードセット** オブジェクトは、独自の高度なデータ tablegram (ADTG) 形式または open 拡張マークアップ言語 (XML) 形式で格納できます。 ADTG の例については、次のセクションで説明します。 XML 永続化の詳細については、「 [xml 形式でのレコードの永続](./persisting-records-in-xml-format.md)化」を参照してください。  
  
 保留中の変更を保存ファイルに保存します。 これにより、 **レコード** セットオブジェクトを返すクエリの実行、 **レコードセット**の編集、および保留中の変更の保存を行うことができます。後で **レコードセット**を復元し、保存されている保留中の変更を使用してデータソースを更新します。  
  
 **ストリーム**オブジェクトを永続的に格納する方法の詳細については、「[ストリームと永続](./streams-and-persistence.md)化」を参照してください。  
  
 **レコードセット**の永続化の例については、「XML レコードセットの永続化シナリオ」を参照してください。  
  
## <a name="example"></a>例  
  
### <a name="save-a-recordset"></a>レコードセットを保存します。  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>レコードセットを使用して、永続化されたファイルを開きます。  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 必要に応じて、 **レコードセット** にアクティブな接続がない場合は、すべての既定値をそのまま使用し、次のコードを記述します。  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Connection.Exeかわいらしいを使用して、永続化されたファイルを開きます。  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>RDS で永続化されたファイルを開きます。DataControl  
 この場合、 **サーバー** プロパティが設定されていません。  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>参照  
 [GetString メソッド (ADO)](../../reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 永続化プロバイダー (ADO サービスプロバイダー)](../appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Recordset オブジェクト (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [ストリームと永続性](./streams-and-persistence.md)