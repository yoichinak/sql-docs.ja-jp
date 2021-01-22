---
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する | Microsoft Docs
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
ms.openlocfilehash: 67b74e36ff5b2872e619a4b26fabdd05428e6a16
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534841"
---
# <a name="configure-column-encryption-in-place-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する 
[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使用すると、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)] のセキュリティで保護されたエンクレーブ内で、データベースの列に対するインプレースでの暗号化操作がサポートされます。 インプレース暗号化を使うと、そのような操作のためにデータをデータベースの外部に移動する必要がなくなり、暗号化操作の速度と信頼性が向上します。 

> [!NOTE]
> インプレース暗号化のパフォーマンス上の利点にもかかわらず、大きなテーブルの暗号化操作には時間がかかり、大量のリソースが消費され、アプリケーションのパフォーマンスと可用性が低下する可能性があります。

インプレース暗号化を使うと、[ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) ステートメントを使用して暗号化操作をトリガーすることもできます。これは、エンクレーブなしでは実行できません。

## <a name="prerequisites"></a>前提条件
サポートされている暗号化操作と、操作に使用される列暗号化キーの要件は、次のとおりです。
- プレーンテキスト列の暗号化。 列の暗号化に使用される列暗号化キーは、エンクレーブ対応である必要があります。
- 新しい暗号化の種類と新しい列暗号化キーの一方または両方を使用した、暗号化された列の再暗号化。 現在の列暗号化キーと新しい列暗号化キー (現在のキーと異なる場合) の両方が、エンクレーブ対応である必要があります。
- 暗号化された列の暗号化解除。列を保護している列暗号化キーは、エンクレーブ対応である必要があります。

列暗号化キーがエンクレーブ対応であることを確認する方法については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](always-encrypted-enclaves-manage-keys.md)」を参照してください。

また、ご利用の環境で一般的な、「[セキュリティで保護されたエンクレーブを使用してステートメントを実行するための前提条件](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves)」が満たされるようにする必要があります。

暗号化操作をトリガーするユーザーまたはアプリケーションには、影響を受ける列を含むテーブルでスキーマを変更し、操作に関係する列マスター キーとデータベース内の関連するキー メタデータにアクセスするための、アクセス許可が必要です。

SQL Server Management Studio またはカスタム アプリケーションから [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) を使用することによってのみ、インプレース暗号化をトリガーできます。 「[Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)」をご覧ください。

> [!NOTE]
> 現時点では、[Always Encrypted ウィザード](always-encrypted-wizard.md)および [Set-SqlColumnEncryption](/powershell/module/sqlserver/set-sqlcolumnencryption) コマンドレットではインプレース暗号化はサポートされておらず、構成が上記の要件を満たしている場合でも、データは暗号化操作のために常にダウンロードされます。 

## <a name="next-steps"></a>次の手順
- [Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>参照  
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする](always-encrypted-enclaves-troubleshooting.md)