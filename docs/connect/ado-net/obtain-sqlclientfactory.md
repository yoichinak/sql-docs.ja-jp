---
title: SqlClientFactory の取得
description: .NET で特定のデータ ソースを操作するために、DbProviderFactories クラスから SqlClientFactory を取得する方法について説明します。
ms.date: 12/22/2020
ms.assetid: a16e4a4d-6a5b-45db-8635-19570e4572ae
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 891cabf04bc8e63537983a91d8526a5cbdf238bf
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771764"
---
# <a name="obtain-a-sqlclientfactory"></a>SqlClientFactory の取得

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:System.Data.Common.DbProviderFactory> を取得する過程では、データ プロバイダーに関する情報が <xref:System.Data.Common.DbProviderFactories> クラスに渡されます。 <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> メソッドはこの情報に基づいて、厳密に型指定されたプロバイダー ファクトリを作成します。 たとえば、<xref:Microsoft.Data.SqlClient.SqlClientFactory> を作成するには、"**Microsoft. Data. SqlClient**" として指定されたプロバイダー名を持つ文字列 `GetFactory` を渡すことができます。

`GetFactory` には、<xref:System.Data.DataRow> を引数として受け取るオーバーロードも存在します。 プロバイダー ファクトリを作成すると、対応するメソッドを使って他のオブジェクトを作成できるようになります。 `SqlClientFactory` のメソッドには、<xref:Microsoft.Data.SqlClient.SqlClientFactory.CreateConnection%2A>、<xref:Microsoft.Data.SqlClient.SqlClientFactory.CreateCommand%2A>、<xref:Microsoft.Data.SqlClient.SqlClientFactory.CreateDataAdapter%2A> などがあります。

## <a name="register-sqlclientfactory"></a>SqlClientFactory の登録

.NET Framework の <xref:System.Data.Common.DbProviderFactories> クラスによって <xref:Microsoft.Data.SqlClient.SqlClientFactory> オブジェクトを取得するには、それを **App.config** または **web.config** ファイルに登録する必要があります。 次の構成ファイル フラグメントは、<xref:Microsoft.Data.SqlClient> の構文と形式を示しています。  

```xml  
<system.data>
  <DbProviderFactories>
    <add name="Microsoft SqlClient Data Provider"
      invariant="Microsoft.Data.SqlClient"
      description="Microsoft SqlClient Data Provider for SQL Server"
      type="Microsoft.Data.SqlClient.SqlClientFactory, Microsoft.Data.SqlClient, Version=2.0.20168.4, Culture=neutral, PublicKeyToken=23ec7fc2d6eaa4a5"/>
  </DbProviderFactories>
</system.data>  
```  

基になるデータ プロバイダーは **invariant** 属性によって識別されます。 この 3 つの部分から成る命名構文は、新しいファクトリを作成するときのほか、プロバイダー名とそれに関連付けられた接続文字列を実行時に取得できるようにするために、アプリケーションの構成ファイルでプロバイダーを指定するときにも使用されます。  

> [!NOTE]  
> .NET Core では、GAC もグローバル構成もサポートされていないため、<xref:Microsoft.Data.SqlClient.SqlClientFactory> オブジェクトを登録するには、プロジェクトで <xref:System.Data.Common.DbProviderFactories.RegisterFactory%2A> メソッドを呼び出す必要があります。

次のサンプルは、.NET Core アプリケーションで <xref:Microsoft.Data.SqlClient.SqlClientFactory> を使用する方法を示しています。

[!code-csharp[SqlClientFactory_Netcoreapp#1](~/../sqlclient/doc/samples/SqlClientFactory_Netcoreapp.cs#1)]

## <a name="see-also"></a>関連項目

- [DbProviderFactories](dbproviderfactories.md)
- [接続文字列](connection-strings.md)
- [構成クラスの使用](/previous-versions/aspnet/ms228063(v=vs.100))
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
