---
title: SqlClient による LocalDB のサポート
description: SqlClient による LocalDB データベースのサポートについて説明します。
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 4760e4928421e0acdeca22f31a00cb148b82019c
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384371"
---
# <a name="sqlclient-support-for-localdb"></a>SqlClient による LocalDB のサポート

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server コード名 Denali 以降、SQL Server の簡易バージョンである LocalDB を使用できるようになります。 ここでは、LocalDB データベースに接続する方法について説明します。  
  
## <a name="remarks"></a>解説  
LocalDB のインストール方法や LocalDB インスタンスの構成方法など、LocalDB の詳細については、SQL Server オンライン ブックを参照してください。  
  
LocalDB で実行できる操作の概要を次に示します。  
  
- sqllocaldb.exe または app.config ファイルを使用して LocalDB インスタンスを作成し、開始します。  
  
- sqlcmd.exe を使用し、LocalDB インスタンスにデータベースを追加し、変更します。 たとえば、「 `sqlcmd -S (localdb)\myinst` 」のように入力します。  
  
- お使いの LocalDB インスタンスにデータベースを追加するには、`AttachDBFilename` 接続文字列キーワードを使用します。 `AttachDBFilename` を使用するときに、`Database` 接続文字列キーワードを使用してデータベース名を指定しなかった場合、データベースはアプリケーションの終了時に LocalDB インスタンスから削除されます。  
  
- 接続文字列では、次のように LocalDB インスタンスを指定します。 たとえば、インスタンス名が `myInstance` の場合、接続文字列は次のようになります。  
  
```console
server=(localdb)\\myInstance  
```  
  
LocalDB データベースに接続する場合、`User Instance=True` は許可されません。  
  
LocalDB は [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041) からダウンロードできます。 sqlcmd.exe を使用し、LocalDB インスタンスのデータを変更する場合、SQL Server 2012 の sqlcmd が表になります。これは SQL Server 2012 Feature Pack からも入手できます。  
  
## <a name="programmatically-create-a-named-instance"></a>プログラムによって名前付きインスタンスを作成する  
アプリケーションで名前付きインスタンスを作成し、次のようにデータベースを指定できます。  
  
- app.config ファイルに作成する LocalDB インスタンスを次のように指定します。  インスタンスのバージョン番号は、LocalDB インストールのバージョン番号と同じである必要があります。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- `server` 接続文字列キーワードを使用して、インスタンスの名前を指定します。  `server` 接続文字列キーワードで指定されたインスタンス名は app.config ファイルで指定された名前と一致する必要があります。  
  
- `AttachDBFilename` 接続文字列キーワードを指定して、.MDF ファイルを指定します。  
  
## <a name="next-steps"></a>次のステップ
- [SQL Server の機能と ADO.NET](sql-server-features-adonet.md)
