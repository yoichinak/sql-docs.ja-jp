---
description: データの保持
title: データの永続化 |Microsoft Docs
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
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: rothja
ms.author: jroth
ms.openlocfilehash: 86789dbce8ab86035f815f36f8eff369b55401a3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980103"
---
# <a name="persisting-data"></a>データの保持
ポータブルコンピューティング (ラップトップの使用など) によって、接続状態と切断状態の両方で実行できるアプリケーションが生成されます。 ADO では、クライアントカーソル **レコードセット** をディスクに保存し、後で再読み込みする機能を開発者に提供することにより、このサポートが追加されました。  
  
 この種類の機能を使用するには、次のようないくつかのシナリオがあります。  
  
-   **移動:** アプリケーションを配置する際には、変更を加えて新しいレコードを追加する機能を提供し、後でデータベースに再接続できるようにすることが重要です。  
  
-   **更新頻度の低い参照:** 多くの場合、アプリケーションでは、テーブルが参照として使用されます。たとえば、州の税テーブルなどです。 更新頻度は低いため、読み取り専用です。 アプリケーションを起動するたびに、このデータをサーバーから再度読み取るのではなく、単にローカルに保存された **レコードセット**からデータを読み込むことができます。  
  
 ADO では、**レコード**セットを保存して読み込むには、Ado**レコードセット**オブジェクトに対して、**レコードセット** **(,,,, adcmdfile)** メソッドを使用します。  
  
 **Recordset Save**メソッドを使用して、ADO**レコードセット**をディスク上のファイルに保存することができます。 ( **レコードセット** を ADO **Stream** オブジェクトに保存することもできます。 **ストリーム** オブジェクトについては、このガイドで後ほど説明します)。その後、使用する準備ができたら、 **Open** メソッドを使用して **レコードセット** を再度開くことができます。 既定では、ADO は、独自の Microsoft Advanced Data TableGram (ADTG) 形式で **レコードセット** を保存します。 このバイナリ形式は、 **AdPersistADTG PersistFormatEnum** 値を使用して指定します。 代わりに、 **Adpersistxml**を使用して、**レコードセット**を XML として保存することもできます。 レコードセットを XML として保存する方法の詳細については、「 [Xml 形式でのレコードの永続](../../../ado/guide/data/persisting-records-in-xml-format.md)化」を参照してください。  
  
 **Save**メソッドの構文は次のとおりです。  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 **レコードセット**を初めて保存するときは、*変換先*を指定することはできません。 *Destination*を省略した場合は、**レコードセット**の[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)プロパティの値に設定された名前で新しいファイルが作成されます。  
  
 最初の保存後、または実行時エラーが発生した後に**保存**を呼び出すと、 *destination*は省略されます。 その後、新しい*変換先*で [**保存**] を呼び出すと、**レコードセット**が新しい変換先に保存されます。 ただし、新しい変換先と元の転送先は両方とも開いています。  
  
 [**保存**] では、**レコードセット**または*変換先*が閉じられないため、**レコードセット**を引き続き使用して、最新の変更を保存することができます。 *変換先* は、 **レコードセット** が閉じられるまで開いたままになります。その間、他のアプリケーションは読み取りますが、 *変換先*に書き込むことはできません。  
  
 セキュリティの理由により、 **Save** メソッドでは、Microsoft Internet Explorer によって実行されるスクリプトの低レベルおよびカスタムセキュリティ設定の使用のみが許可されます。  
  
 非同期の**レコードセット**のフェッチ、実行、または更新の操作の実行中に**save**メソッドが呼び出された場合、非同期操作が完了するまで**保存**を待機します。  
  
 レコードは、レコード **セット**の最初の行から保存されます。 **Save**メソッドが終了すると、現在の行の位置が**レコードセット**の最初の行に移動します。  
  
 最適な結果を得るには、[ [カーソルの場所](../../../ado/reference/ado-api/cursorlocation-property-ado.md) ] プロパティを [ **adUseClient** with **Save**] に設定します。 プロバイダーが、 **レコードセット** オブジェクトを保存するために必要なすべての機能をサポートしていない場合は、カーソルサービスによってその機能が提供されます。  
  
 [**カーソルの場所**] プロパティを**aduseserver**に設定して**レコードセット**を永続化すると、**レコードセット**の更新機能が制限されます。 通常、単一テーブルの更新、挿入、および削除のみが許可されます (プロバイダーの機能によって異なります)。 この構成では、再 [同期](../../../ado/reference/ado-api/resync-method.md) メソッドも使用できません。  
  
 *Destination*パラメーターは OLE DB **IStream**インターフェイスをサポートする任意のオブジェクトを受け入れることができるため、**レコードセット**を ASP**応答**オブジェクトに直接保存できます。  
  
 次の例では、 **保存** と **オープン** のメソッドを使用して **レコードセット** を永続化し、後で再度開くことができます。  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>解説  
 このセクションでは、次のトピックを扱います。  
  
-   [レコードセットの保持に関する詳細情報](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [フィルター処理されたレコードセットおよび階層レコードセットの保持](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
