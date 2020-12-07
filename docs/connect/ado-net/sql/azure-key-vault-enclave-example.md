---
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例 | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2020
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 39d03c4ddcf7edc7d0df1176c9aed1b92f9af9d5
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "96123979"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted での Azure Key Vault プロバイダーの使用を示す例

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

この例は、暗号化された列にアクセスするときの Azure Key Vault プロバイダーの使用を示しています。

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

> [!NOTE]
> - セキュリティで保護されたエンクレーブを使用する Always Encrypted を .NET Standard アプリケーションで使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。 サポートされている .NET Standard のバージョンは 2.1 以降です。 
>
> - セキュリティで保護されたエンクレーブを使用する Always Encrypted を Linux と macOS で使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。

## <a name="see-also"></a>参照

- [Always Encrypted での Azure Key Vault プロバイダーの使用を示す例](azure-key-vault-example.md)
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- [Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](sqlclient-support-always-encrypted.md)
