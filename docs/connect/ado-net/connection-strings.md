---
title: Connection strings
description: Microsoft SqlClient Data Provider for SQL Server の接続文字列について説明します。これには、データ プロバイダーからデータ ソースにパラメーターとして渡される初期化情報が含まれます。
ms.date: 11/13/2020
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e37d77304644d1adb50bb195dd32d4c4e1222c09
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126497"
---
# <a name="connection-strings-in-adonet"></a>ADO.NET での接続文字列

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

接続文字列には、データ プロバイダーからデータ ソースにパラメーターとして渡す初期化情報が含まれています。 データ プロバイダーでは、<xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType> プロパティの値として接続文字列を受け取ります。 プロバイダーによって接続文字列が解析されて、構文が正しいことと、キーワードがサポートされていることが確認されます。 その後、<xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> メソッドにより、解析された接続パラメーターがデータ ソースに渡されます。 データ ソースでは、さらに検証が行われて、接続が確立されます。

## <a name="connection-string-syntax"></a>接続文字列の構文

接続文字列は、キーと値パラメーターのペアをセミコロンで区切ったリストです。

```csharp
keyword1=value; keyword2=value;
```

キーワードの大文字と小文字は区別されません。 ただし、データ ソースによっては、値の大文字小文字が区別されます。 キーワードと値はどちらも、[空白文字](https://en.wikipedia.org/wiki/Whitespace_character#Unicode)が含まれていてもかまいません。 キーワードおよび引用符で囲まれていない値では、先頭と末尾の空白文字は無視されます。

値にセミコロン、[Unicode 制御文字](https://en.wikipedia.org/wiki/Unicode_control_characters)、先頭または末尾の空白が含まれている場合は、単一引用符または二重引用符で囲む必要があります。 次に例を示します。

```csharp
Keyword=" whitespace  ";
Keyword='special;character';
```

囲んでいる文字が、囲まれた値内に出現することはできません。 したがって、単一引用符が含まれる値は、二重引用符でのみ囲むことができます。その逆も同様です。

```csharp
Keyword='double"quotation;mark';
Keyword="single'quotation;mark";
```

また、囲んでいる文字を 2 つ続けて使用することにより、エスケープすることもできます。

```csharp
Keyword="double""quotation";
Keyword='single''quotation';
```

引用符自体と等号は、エスケープする必要がないため、次の接続文字列は有効です。

```csharp
Keyword=no "escaping" 'required';
Keyword=a=b=c
```

各値は、次のセミコロンまたは文字列の末尾まで読み取られるため、後者の例の値は `a=b=c` であり、最後のセミコロンは省略可能です。

すべての接続文字列の基本的な構文は、上で説明したものと同じです。 認識されるキーワードのセットは、プロバイダーによって異なります。 *Microsoft SqlClient* Data Provider for *SQL Server* では、古い API からの多くのキーワードがサポートされていますが、一般に、より柔軟であり、一般的な接続文字列キーワードの多くでシノニムを使用できます。

入力ミスによってエラーが発生する可能性があります。 たとえば、`Integrated Security=true` は有効ですが、`IntegratedSecurity=true` ではエラーが発生します。

実行時に検証されていないユーザー入力から接続文字列を手動で構築すると、文字列のインジェクション攻撃に弱くなり、データ ソースのセキュリティが脅かされます。 これらの問題に対処するため、[接続文字列ビルダー](connection-string-builders.md)が作成されています。 この接続文字列ビルダーにより、厳密に型指定されたプロパティとしてパラメーターが公開され、データ ソースに送信される前に接続文字列を検証できるようになります。

## <a name="in-this-section"></a>このセクションの内容

[接続文字列ビルダー](connection-string-builders.md)\
`ConnectionStringBuilder` クラスを使用して、実行時に有効な接続文字列を作成する方法を示します。

[接続文字列と構成ファイル](connection-strings-and-configuration-files.md)\
構成ファイルを使用した接続文字列の格納と取得の方法について説明します。

[接続文字列の構文](connection-string-syntax.md)\
`SqlClient` 用にプロバイダー固有の接続文字列を構成する方法について説明します。

[接続情報の保護](protecting-connection-information.md)\
データ ソースへの接続に使用する情報を保護する方法を示します。
