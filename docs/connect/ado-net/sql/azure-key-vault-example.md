---
description: Always Encrypted での Azure Key Vault プロバイダーの使用を示す例
title: Always Encrypted での Azure Key Vault プロバイダーの使用を示す例 | Microsoft Docs
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
ms.openlocfilehash: 48c9fbbe5afbc5115aa52dbb13d258e6595b6efc
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464864"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>Always Encrypted での Azure Key Vault プロバイダーの使用を示す例

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

この例は、暗号化された列にアクセスするときの Azure Key Vault プロバイダーの使用を示しています。

## <a name="azurekeyvaultprovider-v20"></a>AzureKeyVaultProvider v2.0 以降

[!code-csharp [Azure Key Vault Provider 2.0 Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample_2_0.cs#1)]

## <a name="azurekeyvaultprovider-v1x"></a>AzureKeyVaultProvider v1.x

[!code-csharp [Azure Key Vault Provider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

> [!NOTE]
>
> - セキュリティで保護されたエンクレーブを使用しない Always Encrypted 機能を .NET Standard アプリケーションで使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。 サポートされている .NET Standard のバージョンは 2.0 以降です。
>
> - Linux と macOS で Always Encrypted の機能を使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。

## <a name="see-also"></a>関連項目

- [セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例](azure-key-vault-enclave-example.md)
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- [Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](sqlclient-support-always-encrypted.md)
