---
description: チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET Framework アプリケーションを開発する
title: チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET Framework アプリケーションを開発する | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 092220a2ef2715b8d5cd414ab5a4bc3e3493acb5
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534741"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET Framework アプリケーションを開発する

[!INCLUDE [sqlserver2019-windows-only-asdb](../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

このチュートリアルでは、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](encryption/always-encrypted-enclaves.md) に対してサーバー側のセキュリティで保護されたエンクレーブを使用するデータベース クエリを発行する、アプリケーションを開発する方法について説明します。 

## <a name="prerequisites"></a>前提条件
このチュートリアルの次の手順に従う前に、以下のチュートリアルのいずれかを完了していることを確認してください。

- [チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](tutorial-getting-started-with-always-encrypted-enclaves.md)
- [チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)

Visual Studio (バージョン 2019 を推奨) も必要です。[https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com) からダウンロードしてください。 アプリケーション開発用コンピューターで、.NET Framework 4.7.2 以降が実行されている必要があります。

## <a name="step-1-set-up-your-visual-studio-project"></a>手順 1:Visual Studio プロジェクトを設定する

.NET Framework アプリケーションでセキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するには、.NET Framework 4.7.2 をターゲットにしてアプリケーションを構築し、[Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders) と統合する必要があります。 さらに、列マスター キーを Azure Key Vault に格納する場合は、アプリケーションを [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider) バージョン 2.2.0 以降と統合する必要があります。 

1. Visual Studio を開きます。

2. 新しい C\# コンソール アプリ (.NET Framework) プロジェクトを作成します。

3. プロジェクトは必ず .NET Framework 4.7.2 以降をターゲットにします。 ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロパティ]** を選択して、 **[ターゲット フレームワーク]** を [.NET Framework 4.7.2] に設定します。

4. **[ツール]** (メイン メニュー) > **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** に移動して、次の NuGet パッケージをインストールします。 パッケージ マネージャー コンソールで次のコードを実行します。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Azure Key Vault を使用して列マスター キーを格納する場合は、 **[ツール]** (メイン メニュー) > **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** に移動して、次の NuGet パッケージをインストールします。 パッケージ マネージャー コンソールで次のコードを実行します。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. プロジェクトの App.config ファイルを開きます。

7. `<configuration>` セクションを見つけて、`<configSections>` セクションを追加または更新します。

   1. `<configuration>` セクションに `<configSections>` セクションが含まれて **いない** 場合は、`<configuration>` のすぐ下に次の内容を追加します。

      ```xml
      <configSections>
        <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```

   2. `<configuration>` セクションに `<configSections>` セクションが既に含まれている場合は、`<configSections>` セクション内に次の行を追加します。

      ```xml
      <section name="SqlColumnEncryptionEnclaveProviders"  type="System.   Data.SqlClient.   SqlColumnEncryptionEnclaveProviderConfigurationSection, System.   Data,  Version=4.0.0.0, Culture=neutral,    PublicKeyToken=b77a5c561934e089" />
      ```

8. `<configuration>` セクション内で、`</configSections>` の下に新しいセクションを追加します。これにより、構成証明、およびサーバー側のセキュリティで保護されたエンクレーブとのやり取りに使用されるエンクレーブ プロバイダーが指定されます。

   1. [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] とホスト ガーディアン サービス (HGS) を使用する (「[チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](tutorial-getting-started-with-always-encrypted-enclaves.md)」のデータベースを使用する) 場合は、以下のセクションを追加します。

      ```xml
      <SqlColumnEncryptionEnclaveProviders>
        <providers>
          <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
        </providers>
      </SqlColumnEncryptionEnclaveProviders>
      ```

      単純なコンソール アプリケーションの app.config ファイルの完全な例を次に示します。

      ```xml
      <?xml version="1.0" encoding="utf-8" ?>
      <configuration>
        <configSections>
          <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </configSections>
        <SqlColumnEncryptionEnclaveProviders>
          <providers>
            <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
          </providers>
        </SqlColumnEncryptionEnclaveProviders>
        <startup> 
         <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
        </startup>
      </configuration>
      ```

   1. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] と Microsoft Azure Attestation を使用する (「[チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)」のデータベースを使用する) 場合は、以下のセクションを追加します。

      ```xml
      <SqlColumnEncryptionEnclaveProviders>
        <providers>
          <add name="SGX" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.AzureAttestationEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
        </providers>
      </SqlColumnEncryptionEnclaveProviders>
      ```

      単純なコンソール アプリケーションの app.config ファイルの完全な例を次に示します。

      ```xml
      <?xml version="1.0" encoding="utf-8" ?>
      <configuration>
        <configSections>
          <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </configSections>
        <SqlColumnEncryptionEnclaveProviders>
          <providers>
            <add name="SGX" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.AzureAttestationEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
          </providers>
        </SqlColumnEncryptionEnclaveProviders>
        <startup> 
         <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
        </startup>
      </configuration>
      ```

## <a name="step-2-implement-your-application-logic"></a>手順 2:アプリケーションのロジックを実装する

このアプリケーションでは、**ContosoHR** データベース (「[チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](tutorial-getting-started-with-always-encrypted-enclaves.md)」または「[チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)」に接続し、**SSN** 列に対する `LIKE` 述語と、**Salary** 列に対する範囲比較が含まれるクエリを実行します。

1. (Visual Studio によって生成された) Program.cs ファイルの内容を、次のコードに置き換えます。 データベース接続文字列を、お使いのサーバー名、データベース認証設定、およびご利用の環境のエンクレーブ構成証明 URL で更新します。

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                //string connectionString = "Data Source = myserver.database.windows.net; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = https://myattestationprovider.uks.attest.azure.net/attest/SgxEnclave; User ID=user; Password=password";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [HR].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%9838";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 20000;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```

2. アプリケーションをビルドして実行します。  

## <a name="see-also"></a>参照

- [Always Encrypted と .NET Framework Data Provider for SQL Server を使用する](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
