---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を構成して使用する | Microsoft Docs
description: SQL Server および Azure SQL Database でセキュリティで保護されたエンクレーブが設定された Always Encrypted を構成して使用する方法を学習します。これにより、機密データに対してより高度な機能を有効にすることができます。
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 73a1c9f3a39ce51ce6ecc347af2e2eb0fb173fb6
ms.sourcegitcommit: b1cec968b919cfd6f4a438024bfdad00cf8e7080
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99237299"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を構成して使用する 

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) は、既存の [Always Encrypted ](always-encrypted-database-engine.md) 機能を拡張して、データを機密性に保ちながら機密データに対してより高度な機能を有効にすることができます。 この記事では、この機能を構成して使用するための一般的なタスクを示します。

セキュリティで保護されたエンクレーブが設定された Always Encrypted をすぐに使い始める方法が示されたチュートリアルについては、以下を参照してください。

- [チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)

## <a name="set-up-the-secure-enclave-and-attestation"></a>セキュリティで保護されたエンクレーブと構成証明を設定する

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する前に、データベースで確実にセキュリティで保護されたエンクレーブを利用できるように環境を構成する必要があります。 また、[エンクレーブの構成証明](always-encrypted-enclaves.md#secure-enclave-attestation)を設定する必要があります。 

環境を設定するためのプロセスは、[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] と [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] のどちらを使用しているかによって異なります。

### <a name="set-up-the-secure-enclave-and-attestation-in-ssnoversion-md"></a>[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] でセキュリティで保護されたエンクレーブと構成証明を設定する

詳しくは、次の記事を参照してください。
- [ホスト ガーディアン サービスの構成証明の計画](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] のホスト ガーディアン サービスを配置する](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [ホスト ガーディアン サービスにコンピューターを登録する](./always-encrypted-enclaves-host-guardian-service-register.md)
- [SQL Server でセキュリティで保護されたエンクレーブを構成する](always-encrypted-enclaves-configure-enclave-type.md)

### <a name="set-up-the-secure-enclave-and-attestation-in-sssdsfull"></a>[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] でセキュリティで保護されたエンクレーブと構成証明を設定する

詳しくは、次の記事を参照してください。
- [[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] で Intel SGX エンクレーブと構成証明を計画する](/azure/azure-sql/database/always-encrypted-enclaves-plan)
- [Azure SQL Database に対して Intel SGX を有効にする](/azure/azure-sql/database/always-encrypted-enclaves-enable-sgx)
- [Azure SQL Database 論理サーバー用に Azure Attestation を構成する](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する - 概要](always-encrypted-enclaves-manage-keys.md)
- [エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)
- [エンクレーブ対応キーをローテーションする](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted で列を構成する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する - 概要](always-encrypted-enclaves-configure-encryption.md)
- [Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)
- [既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](always-encrypted-enclaves-enable-for-encrypted-columns.md)

## <a name="run-transact-sql-statements-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする](always-encrypted-enclaves-troubleshooting.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>エンクレーブ対応の列でインデックスを作成して使用する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブ列が設定された Always Encrypted でのインデックスの作成と使用](always-encrypted-enclaves-create-use-indexes.md)
  
## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)
