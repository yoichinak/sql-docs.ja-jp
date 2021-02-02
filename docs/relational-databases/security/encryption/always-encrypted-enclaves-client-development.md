---
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64c628172ba95ff9de546c018ea00a9ba63943c9
ms.sourcegitcommit: f30b5f61c514437ea58acc5769359c33255b85b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2021
ms.locfileid: "99075604"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する
[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使うと、[Always Encrypted](always-encrypted-database-engine.md) が拡張され、暗号化された機密データベース列に対するアプリケーション クエリの高度な機能が有効になります。 セキュリティで保護されたエンクレーブのテクノロジを利用することで、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)] のクエリ Executor は、暗号化された列に対する計算を、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)] プロセス内のセキュリティで保護されたエンクレーブにデリゲートできるようになります。

## <a name="prerequisites"></a>前提条件

- [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] インスタンス、または [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 内のデータベースとサーバーが、エンクレーブと構成証明をサポートするように正しく構成されている必要があります。 詳細については、「[セキュリティで保護されたエンクレーブと構成証明を設定する](configure-always-encrypted-enclaves.md#set-up-the-secure-enclave-and-attestation)」を参照してください。
- 構成証明サービス管理者から、ご利用の環境用の構成証明 URL を取得する必要があります。

  - [!INCLUDE[ssnoversion-md](../../../includes/ssnoversion-md.md)] とホスト ガーディアン サービス (HGS) を使用している場合は、「[HGS 構成証明 URL を確認して共有する](../../../relational-databases/security/encryption/always-encrypted-enclaves-host-guardian-service-deploy.md#step-6-determine-and-share-the-hgs-attestation-url)」を参照してください。
  - [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] と Microsoft Azure Attestation を使用している場合は、「[構成証明ポリシーの構成証明 URL を確認する](/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sql-server-ver15#secure-enclave-attestation)」を参照してください。

- アプリケーションでは、セキュリティで保護されたエンクレーブをサポートする SQL クライアント ドライバーのバージョンを使用する必要があります。 詳細については、以下のセクションを参照してください。

- データベース接続用に構成証明プロトコルと構成証明 URL を構成する必要があります。 構成証明プロトコルと構成証明 URL の構成方法の詳細は、使用しているクライアント ドライバーによって異なります。

## <a name="client-drivers-for-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted 用のクライアント ドライバー

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用してアプリケーションを開発するには、セキュリティで保護されたエンクレーブがサポートされているバージョンの SQL クライアント ドライバーが必要です。 クライアント ドライバーでは、次の重要な役割が行われます。

- セキュリティで保護されたエンクレーブを使用するクエリが実行のために [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] に送信される前に、ドライバーによってエンクレーブの構成証明が開始され、セキュリティで保護されたエンクレーブが信頼できること、および機密データの処理に安全に使用できることが確認されます。 構成証明について詳しくは、「[セキュリティで保護されたエンクレーブの構成証明](always-encrypted-enclaves.md#secure-enclave-attestation)」をご覧ください。
- 構成証明が成功すると、クライアント ドライバーにより、共有シークレットをネゴシエートすることで、エンクレーブとのセキュリティで保護されたセッションが確立されます。
- ドライバーでは、共有シークレットを使用して、エンクレーブがクエリを処理するために必要な列暗号化キーが暗号化され、そのキーが [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] に送信されます。そこからキーは、キーの暗号化解除が行われるセキュリティで保護されたエンクレーブに転送されます。 
- 最後に、ドライバーによって実行のためにクエリが送信され、セキュリティで保護されたエンクレーブ内で計算がトリガーされます。

## <a name="next-steps"></a>次のステップ

セキュリティで保護されたエンクレーブが設定された Always Encrypted は、次のクライアント ドライバーでサポートされます。

- .NET Framework 4.6 以降および .NET Core 2.1 以降の Microsoft .NET Data Provider for SQL Server 
    - 詳しくは、「[Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)」をご覧ください。
    - 詳しいチュートリアルについては、「[チュートリアル: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET アプリケーションを開発する](../../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)」を参照してください。
    - [Azure Key Vault プロバイダーとセキュリティで保護されたエンクレーブが設定された Always Encrypted の使用を示す例](../../../connect/ado-net/sql/azure-key-vault-enclave-example.md)に関するページも参照してください。
- Microsoft ODBC Driver for SQL Server バージョン 17.4 以降。 
    - 詳しくは、「[Using Always Encrypted with the ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)」(ODBC ドライバーでの Always Encrypted の使用) をご覧ください。 
    - ODBC を使用するデータベース接続でエンクレーブ計算を有効にする方法については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves)」を参照してください。
- Microsoft JDBC Driver for SQL Server バージョン 8.2 以降。
    - 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を JDBC Driver と共に使用する](../../../connect/jdbc/using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver.md)」を参照してください
- .NET Framework 4.7.2 以降の .NET Framework Data Provider for SQL Server 
    - 詳しくは、「[Always Encrypted と .NET Framework Data Provider for SQL Server を使用する](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)」をご覧ください。
    - 詳しいチュートリアルについては、「[チュートリアル: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET Framework アプリケーションの開発](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="see-also"></a>関連項目

- [セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする](always-encrypted-enclaves-troubleshooting.md)
