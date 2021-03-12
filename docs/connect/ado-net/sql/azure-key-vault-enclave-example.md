---
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2021
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: df1b2fb3c99eac35b2a742254b75a8f06b3f37bf
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464921"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

## <a name="azurekeyvaultprovider-v20"></a>AzureKeyVaultProvider v2.0 以降

[!code-csharp [Azure Key Vault Provider 2.0 with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample_2_0.cs#1)]

## <a name="azurekeyvaultprovider-v1x"></a>AzureKeyVaultProvider v1.x

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

> [!NOTE]
>
> - セキュリティで保護されたエンクレーブを使用する Always Encrypted を .NET Standard アプリケーションで使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。 サポートされている .NET Standard のバージョンは 2.1 以降です。
>
> - セキュリティで保護されたエンクレーブを使用する Always Encrypted を Linux と macOS で使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。

## <a name="see-also"></a>関連項目

- [Always Encrypted での Azure Key Vault プロバイダーの使用を示す例](azure-key-vault-example.md)
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- [Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](sqlclient-support-always-encrypted.md)
