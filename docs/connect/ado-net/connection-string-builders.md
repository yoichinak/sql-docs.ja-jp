---
title: 接続文字列ビルダー
description: ADO.NET のさまざまなプロバイダー向けに使用される接続文字列ビルダー クラスについて説明します。これらはすべて DbConnectionStringBuilder から継承されます。
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: bdb4294fda1f26ec346f786ec29061f8d4f9ee27
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419803"
---
# <a name="connection-string-builders"></a>接続文字列ビルダー

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

以前のバージョンの ADO.NET では、文字列値の連結によって構築された接続文字列がコンパイル時にはチェックされません。そのため、不適切なキーワードが使用された場合、実行時に <xref:System.ArgumentException> が発生します。 Microsoft SqlClient Data Provider for SQL Server には、<xref:System.Data.Common.DbConnectionStringBuilder> から継承される、厳密に型指定された接続文字列ビルダー クラス <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType> が含まれています。

## <a name="connection-string-injection-attacks"></a>接続文字列のインジェクション攻撃

ユーザー入力から文字列を動的に連結することによって接続文字列を構築している場合、接続文字列のインジェクション攻撃を受ける可能性があります。 文字列の検証や悪意のある文字のエスケープを怠ると、機密データなど、サーバー上のリソースへのアクセスを攻撃者に許してしまうことも考えられます。 たとえば、セミコロンに続けて値を追加するだけでも攻撃が成立します。 接続文字列は "**ラスト ワン ウィン**" アルゴリズムを使用して解析され、悪意のある入力は正当な値に置き換えられます。

接続文字列ビルダー クラスは推測に頼った作業を排除し、構文エラーやセキュリティ上の脆弱性を防ぐことを目的に設計されています。 これらによって、データ プロバイダーによって許可されている既知のキーと値のペアに対応するメソッドとプロパティが提供されます。 それぞれのクラスは、あらかじめ決められた一連のシノニムを管理しており、特定のシノニムを対応する既知のキー名に変換することができます。 有効なキーと値のペアに対してチェックが実行され、無効なペアが見つかると例外がスローされます。 また、挿入された値は安全な方法で処理されます。

次の例を実行すると、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> の設定に対して挿入された余分な値が、`Initial Catalog` によってどのように処理されるかを確認できます。

[!code-csharp[SqlConnectionStringBuilder_InjectionAttack#1](~/../sqlclient/doc/samples/SqlConnectionStringBuilder_InjectionAttack.cs#1)]

その出力は、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> によって、余分な値が、新しいキーと値のペアとして接続文字列に追加するのではなく、二重引用符でエスケープすることで正しく処理されたことを示しています。

```output
data source=(local);Integrated Security=True;
initial catalog="AdventureWorks;NewValue=Bad"
```

## <a name="building-connection-strings-from-configuration-files"></a>構成ファイルからの接続文字列の作成

接続文字列の特定の要素があらかじめわかっている場合、接続文字列を構成ファイルに格納しておき、それを実行時に取得することによって完全な接続文字列を作成できます。 たとえば、サーバー名は不明でも、データベースの名前はあらかじめ把握できる場合があります。 または、ユーザーに名前とパスワードだけを実行時に指定してもらい、それ以外の値を接続文字列に挿入できないようにしたい場合もあります。

接続文字列ビルダーには、<xref:System.String> を引数として受け取るオーバーロード コンストラクターがあります。この引数に対して接続文字列を部分的に指定しておき、それ以外の部分をユーザー入力で補完することも可能です。 部分的な接続文字列は構成ファイルに保存し、実行時に取得できます。

> [!NOTE]
> 構成ファイルへのプログラム アクセスは <xref:System.Configuration> 名前空間によって実現できます。Web アプリケーションの場合は <xref:System.Web.Configuration.WebConfigurationManager> を、Windows アプリケーションの場合は <xref:System.Configuration.ConfigurationManager> を使用します。 接続文字列と構成ファイルの使用について詳しくは、「[接続文字列と構成ファイル](connection-strings-and-configuration-files.md)」をご覧ください。

### <a name="example"></a>例

この例では、接続文字列の一部を構成ファイルから取得し、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> の <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A> プロパティ、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> プロパティ、および <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> プロパティを設定することによって接続文字列全体を作成します。 構成ファイルは次のように定義されています。

```xml
<connectionStrings>
  <clear/>
  <add name="partialConnectString"
    connectionString="Initial Catalog=Northwind;"
    providerName="Microsoft.Data.SqlClient" />
</connectionStrings>
```

> [!NOTE]
> このコードを実行するには、プロジェクトで `System.Configuration.dll` を参照設定する必要があります。

[!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](~/../sqlclient/doc/samples/SqlConnectionStringBuilder_UserNamePwd.cs#1)]
  
## <a name="see-also"></a>関連項目

- [接続文字列](connection-strings.md)
