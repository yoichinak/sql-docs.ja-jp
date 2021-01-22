---
description: エンクレーブ対応キーの交換
title: 交換 | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 8ef5e2e3cbf4e00619aeb4b0d1643f0d07100aad
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534310"
---
# <a name="rotate-enclave-enabled-keys"></a>エンクレーブ対応キーの交換

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

Always Encrypted では、キーの交換は、既存の列マスター キーまたは列暗号化キーを新しいキーに置き換える処理です。 この記事では、初期キーまたはターゲット (新しい) キーのどちらか一方または両方がエンクレーブが有効なキーである場合に、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) に固有のキー ローテーションのユースケースと考慮事項について説明します。 Always Encrypted キーを管理するための一般的なガイドラインとプロセスについては、「[Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md)」を参照してください。 

セキュリティまたはコンプライアンス上の理由から、キーの交換が必要になる場合があります。 キーが侵害された場合や、組織のポリシーでキーを定期的に交換する必要がある場合などです。 さらに、セキュリティで保護されたエンクレーブが設定された Always Encrypted のキー ローテーションでは、暗号化された列に対してサーバー側のセキュア エンクレーブの機能を有効または無効にすることができます。

- エンクレーブが有効でないキーをエンクレーブが有効なキーで置き換える場合は、キーで保護されている列へのクエリに対するセキュリティで保護されたエンクレーブの機能のロックを解除します。 詳細については、「[既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted の有効化](always-encrypted-enclaves-enable-for-encrypted-columns.md)」を参照してください。
- エンクレーブが有効なキーをエンクレーブが有効でないキーで置き換える場合は、キーで保護されている列へのクエリに対するセキュリティで保護されたエンクレーブの機能を無効にします。

セキュリティまたはコンプライアンス上の理由だけでキーを交換し、列のエンクレーブ計算を有効または無効にしない場合は、ターゲット キーのエンクレーブに関する構成がソース キーと同じであることを確認してください。 たとえば、ソース キーのエンクレーブが有効な場合、ターゲット キーもエンクレーブが有効になっている必要があります。

以下の手順には、目的の交換シナリオに応じた詳細な記事へのリンクが含まれています。

1. 新しいキーを (列マスター キーまたは列暗号化キー) をプロビジョニングします。
    - 新しいエンクレーブ対応キーをプロビジョニングするには、「[エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)」を参照してください。
    - エンクレーブが有効でないキーをプロビジョニングするには、「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)」および「[PowerShell を使用した Always Encrypted キーのプロビジョニング](configure-always-encrypted-keys-using-powershell.md)」を参照してください。
2. 既存のキーを新しいキーで置き換えます。
    - 列暗号化キーを交換し、ソース キーとターゲット キーの両方のエンクレーブが有効になっている場合は、インプレースで交換を実行できます (データの再暗号化を含む)。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。
    - キーのローテーションの詳細な手順については、「[SQL Server Management Studio を使用した Always Encrypted キーの交換](rotate-always-encrypted-keys-using-ssms.md)」および「[PowerShell を使用した Always Encrypted キーの交換](rotate-always-encrypted-keys-using-powershell.md)」をご覧ください。

## <a name="next-steps"></a>次の手順

- [セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)
- [既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)  

## <a name="see-also"></a>参照  
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](always-encrypted-enclaves-manage-keys.md)