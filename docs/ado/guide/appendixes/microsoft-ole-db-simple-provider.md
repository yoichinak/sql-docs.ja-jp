---
description: Microsoft OLE DB Simple Provider の概要
title: Microsoft OLE DB Simple Provider |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 4eb4635aafa67d2b6c96f88580811c204ff73423
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990983"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB Simple Provider の概要
Microsoft OLE DB Simple Provider (OSP) を使用すると、ADO は、 [OLE DB Simple provider (osp) Toolkit](/previous-versions/windows/desktop/ms715822(v=vs.85))を使用して、プロバイダーが記述されているすべてのデータにアクセスできます。 単純なプロバイダーは、メモリ内配列や XML ドキュメントなどの基本的な OLE DB サポートのみを必要とするデータソースにアクセスすることを目的としています。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 OLE DB の単純なプロバイダー DLL に接続するには、 *provider* 引数を [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) プロパティに設定します。

```vb
MSDAOSP
```

 この値は、 [プロバイダー](../../reference/ado-api/provider-property-ado.md) プロパティを使用して設定または読み取ることもできます。

 プロバイダーのライターによって決定される登録済みプロバイダー名を使用して、完全な OLE DB プロバイダーとして登録されている単純なプロバイダーに接続できます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 文字列は、次のキーワードで構成されています。

|キーワード|説明|
|-------------|-----------------|
|**プロバイダー**|SQL Server の OLE DB プロバイダーを指定します。|
|**データ ソース**|サーバーの名前を指定します。|

## <a name="xml-document-example"></a>XML ドキュメントの例
 MDAC 2.7 以降の OLE DB Simple Provider (OSP) と Windows Data Access Components (Windows DAC) は、任意の XML ファイルに対する階層型 ADO **レコードセット** のオープンをサポートするように強化されています。 これらの XML ファイルには ADO XML 永続化スキーマが含まれている場合がありますが、必須ではありません。 これは、OSP を **MSXML2.DLL**に接続することによって実装されています。したがって、 **MSXML2.DLL** 以降が必要です。

 次の例で使用される **portfolio.xml** ファイルには、次のツリーが含まれています。

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML DSO は、組み込みのヒューリスティックを使用して、XML ツリー内のノードを階層 **レコードセット**内のチャプターに変換します。

 これらの組み込みのヒューリスティックを使用して、XML ツリーは次の形式の2レベルの階層 **レコードセット** に変換されます。

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 ポートフォリオタグと情報タグは、階層 **レコードセット**では表されないことに注意してください。 Xml DSO が XML ツリーを階層的な **レコードセット**に変換する方法の詳細については、次のルールを参照してください。 $Text の列については、次のセクションで説明します。

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>列および行への XML 要素と属性の割り当てに関する規則
 XML DSO は、データバインドアプリケーションの列および行に要素と属性を割り当てる手順に従います。 XML は、階層全体を含む1つのタグを持つツリーとしてモデル化されます。 たとえば、書籍の XML 記述には、章タグ、図タグ、およびセクションタグを含めることができます。 最上位レベルには、サブ要素の章、図、およびセクションを含む book タグがあります。 Xml DSO が XML 要素を行と列にマップする場合、最上位レベルの要素ではなく、サブ要素が変換されます。

 XML DSO は、サブ要素を変換するために次の手順を使用します。

-   各サブ要素および属性は、階層内の一部の **レコードセット** 内の列に対応します。

-   列の名前は、サブ要素または属性の名前と同じです。ただし、親要素に同じ名前のサブ要素がある場合は、"!" がサブ要素の列名の前に付加されます。

-   各列は、スカラー値 (通常は文字列) または子**レコード**セットを含む**レコードセット**列を含む*単純*な列です。

-   属性に対応する列は、常に単純です。

-   サブ要素が独自のサブ要素または属性 (またはその両方) を持つか、サブ要素の親が子として複数のサブ要素のインスタンスを持つ場合、サブ要素に対応する列は **レコードセット** 列です。 それ以外の場合、列は単純です。

-   サブ要素の複数のインスタンス (異なる親の下) がある場合、*いずれか*のインスタンスが**レコードセット**列を意味する場合、その列は**レコードセット**列になります。この列は、*すべて*のインスタンスが単純な列を意味する場合にのみ単純です。

-   すべての **レコードセット** には、$Text という名前の列が追加されています。

 **レコードセット**を作成するために必要なコードは次のとおりです。

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  データファイルのパスは、4つの異なる名前付け規則を使用して指定できます。

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 **レコードセット**が開かれるとすぐに、通常の ADO**レコードセット**ナビゲーションコマンドを使用できるようになります。

 OSP によって生成される**レコードセット**には、いくつかの制限があります。

-   クライアントカーソル (**adUseClient**) はサポートされていません。

-   任意の XML に対して作成された階層 **レコードセット** は、 **レコードセット**を使用して保存することはできません。

-   OSP で作成された**レコードセット**は読み取り専用です。

-   XMLDSO は、階層内の各 **レコードセット** にデータの列 ($Text) を追加します。

 OLE DB 単純なプロバイダーの詳細については、「 [単純なプロバイダーの構築](/previous-versions/windows/desktop/ms721067(v=vs.85))」を参照してください。

## <a name="code-example"></a>コード例
 次の Visual Basic コードは、任意の XML ファイルを開き、階層 **レコードセット**を構築し、各レコード **セット** の各レコードをデバッグウィンドウに再帰的に書き込む方法を示しています。

 株価を含む単純な XML ファイルを次に示します。 次のコードでは、このファイルを使用して、2レベルの階層 **レコードセット**を作成します。

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 2つの Visual Basic サブプロシージャを次に示します。 1つ目の方法では、**レコードセット**が作成され、そのレコードセットが*ウォーク hier*サブプロシージャに渡されます。これは、階層を再帰的に処理し、各レコード**セット**内の各レコードの各**フィールド**をデバッグウィンドウに書き込みます。

```vb
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```