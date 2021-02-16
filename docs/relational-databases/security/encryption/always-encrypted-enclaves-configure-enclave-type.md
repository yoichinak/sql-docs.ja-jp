---
title: SQL Server でセキュリティで保護されたエンクレーブを構成する
description: SQL Server でセキュリティで保護されたエンクレーブが設定された Always Encrypted 用に、セキュリティで保護されたエンクレーブを構成します。
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b2bd51dffb858f30e29b4a1b60e1c728afdbeb93
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100067257"
---
# <a name="configure-the-secure-enclave-in-sql-server"></a>SQL Server でセキュリティで保護されたエンクレーブを構成する

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

SQL Server で[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使用する前に、起動時にセキュリティで保護されたエンクレーブを初期化するようにインスタンスを構成する必要があります。 既定では、SQL Server によってセキュリティで保護されたエンクレーブは初期化されません。 **列暗号化エンクレーブの型** というサーバー構成オプションを、ご利用の環境の有効なエンクレーブ型を表す値に設定することで、これを変更できます。

> [!NOTE]
> セキュリティで保護されたエンクレーブの構成を担当するロールは DBA です。 「[HGS で構成証明を構成する場合のロールと責任](always-encrypted-enclaves-host-guardian-service-plan.md#roles-and-responsibilities-when-configuring-attestation-with-hgs)」を参照してください。

[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] でサポートされているエンクレーブの型は仮想化ベースのセキュリティ (VBS) です。 VBS エンクレーブの型を構成する前に、インスタンスをホストしているコンピューターに対してホスト ガーディアン サービス (HGS) を使用して構成証明を設定することをお勧めします。 HGS の概要については、「[ホスト ガーディアン サービスの構成証明の計画](always-encrypted-enclaves-host-guardian-service-plan.md)」を参照してください。 構成証明を設定すると、VBS エンクレーブが適切に初期化されるために必要な仮想化ベースのセキュリティも有効になります。 詳細については、「[仮想化ベースのセキュリティが実行されていることを確認する](always-encrypted-enclaves-host-guardian-service-register.md#step-2-verify-virtualization-based-security-is-running)」を参照してください。

エンクレーブの型を構成する方法の詳細については、「[Always Encrypted サーバー構成オプションのエンクレーブの種類を構成する](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)」を参照してください。

## <a name="next-steps"></a>次の手順

 [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](always-encrypted-enclaves-manage-keys.md)

## <a name="see-also"></a>参照  
 
 [サーバー構成オプション (SQL Server)](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)
