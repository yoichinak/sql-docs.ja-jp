---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする
ms.custom: ''
ms.date: 01/15/2021
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: how-to
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: c7bffa36b256b959048953a5438fec6a336c3acc
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534886"
---
# <a name="troubleshoot-common-issues-for-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする

この記事では、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使用して Transact-SQL (TSQL) ステートメントを実行するときに、発生する可能性のある一般的な問題を特定して解決する方法について説明します。

セキュリティで保護されたエンクレーブを使用してクエリを実行する方法の詳細については、「[セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する](always-encrypted-enclaves-query-columns.md)」を参照してください。

## <a name="database-connection-errors"></a>データベース接続エラー

セキュリティで保護されたエンクレーブを使用してステートメントを実行するには、Always Encrypted を有効にし、データベース接続の構成証明 URL を指定する必要があります。詳細については、「[セキュリティで保護されたエンクレーブを使用してステートメントを実行するための前提条件](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves)」を参照してください。 ただし、構成証明 URL を指定しても、[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] のデータベースまたはターゲットである [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] インスタンスがセキュリティで保護されたエンクレーブをサポートしていない場合、または正しく構成されていない場合、接続は失敗します。

- [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] を使用している場合は、データベースで [DC シリーズ](https://docs.microsoft.com/azure/azure-sql/database/service-tiers-vcore?tabs=azure-portal#dc-series)のハードウェア構成が使用されていることを確認してください。 詳細については、「[Azure SQL データベースに対して Intel SGX を有効にする](/azure/azure-sql/database/always-encrypted-enclaves-enable-sgx)」を参照してください。
- [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] を使用している場合は、セキュリティで保護されたエンクレーブがインスタンスに対して正しく構成されていることを確認してください。 詳細については、「[SQL Server でセキュリティで保護されたエンクレーブを構成する](always-encrypted-enclaves-configure-enclave-type.md)」を参照してください。

## <a name="attestation-errors-when-using-microsoft-azure-attestation"></a>Microsoft Azure Attestation 使用時の構成証明エラー

> [!NOTE]
> このセクションは [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] のみに適用されます。

クライアント ドライバーから Azure SQL 論理サーバーに実行対象の T-SQL ステートメントが送信される前に、次のエンクレーブ構成証明ワークフローがドライバーによって Microsoft Azure Attestation を使用してトリガーされます。

1. クライアント ドライバーから Azure SQL 論理サーバーに、データベース接続で指定された構成証明 URL が渡されます。
2. エンクレーブ、そのホスティング環境、およびエンクレーブ内で実行されているコードに関する証拠が Azure SQL 論理サーバーによって収集されます。 次に、サーバーから構成証明 URL で参照されている構成証明プロバイダーに、構成証明要求が送信されます。
3. 構成証明プロバイダーによって、構成されたポリシーに照らした証拠の検証と、Azure SQL 論理サーバーに対する構成証明トークンの発行が行われます。 構成証明プロバイダーによって、構成証明トークンが秘密キーを使用して署名されます。
4. Azure SQL 論理サーバーからクライアント ドライバーに構成証明トークンが送信されます。
5. クライアントは、指定された構成証明 URL で構成証明プロバイダーに接続して公開キーを取得し、構成証明トークン内の署名を検証します。

構成の誤りにより、上記のワークフローのさまざまな手順でエラーが発生する可能性があります。 一般的な構成証明エラー、その根本原因、および推奨されるトラブルシューティング手順は次のとおりです。

- Azure SQL 論理サーバーから、構成証明 URL で指定された Azure Attestation (上記のワークフローの手順 2) の構成証明プロバイダーに接続できません。 次の原因が考えられます。
  - 構成証明 URL が正しくないか、不完全である。 詳細については、「[構成証明ポリシーの構成証明 URL を確認する](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation#determine-the-attestation-url-for-your-attestation-policy)」を参照してください。
  - 構成証明プロバイダーが誤って削除された。
  - 構成証明プロバイダーに対してファイアウォールが構成されたが、そこで Microsoft サービスへのアクセスが許可されていない。
  - 間欠的なネットワーク エラーのために、構成証明プロバイダーを使用できない。
- Azure SQL 論理サーバーに、構成証明プロバイダーに構成証明要求を送信する権限がありません。 構成証明プロバイダーの管理者によって、データベース サーバーが構成証明リーダー ロールに追加されていることを確認します。 詳細については、「[Azure SQL Database サーバーへのアクセス権を構成証明プロバイダーに付与する](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation#grant-your-azure-sql-database-server-access-to-your-attestation-provider)」を参照してください。
- 構成証明ポリシーの検証が失敗します (上記のワークフローの手順 3)。
  - 正しくない構成証明ポリシーが根本原因と考えられます。 Microsoft 推奨のポリシーを使用していることを確認してください。 詳細については、「[構成証明プロバイダーの作成と構成](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation#create-and-configure-an-attestation-provider)」を参照してください。
  - また、セキュリティ違反によってサーバー側のエンクレーブが侵害された結果として、ポリシーの検証が失敗する場合もあります。
- クライアント アプリケーションから構成証明プロバイダーに接続できず、(手順 5 で) 公開署名キーを取得できません。 次の原因が考えられます。
  - アプリケーションと構成証明プロバイダーの間にファイアウォールを構成すると、接続がブロックされる可能性があります。 ブロックされた接続のトラブルシューティングを行うには、構成証明プロバイダーの OpenId エンドポイントに接続できることを確認します。 たとえば、アプリケーションをホストしているコンピューターから OpenID エンドポイントに Web ブラウザーを使用して接続できるかどうかを確認します。 詳細については、「[Metadata Configuration - Get](https://docs.microsoft.com/rest/api/attestation/metadataconfiguration/get)」を参照してください。

## <a name="attestation-errors-when-using-host-guardian-service"></a>ホスト ガーディアン サービス使用時の構成証明エラー

> [!NOTE]
> このセクションは [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] のみに適用されます。

クライアント ドライバーから [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] に実行対象の T-SQL ステートメントが送信される前に、ドライバーによって次のエンクレーブ構成証明ワークフローが、ホスト ガーディアン サービス (HGS) を使用してトリガーされます。

1. クライアント ドライバーによって [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] が呼び出されて、構成証明が開始されます。
2. エンクレーブ、そのホスティング環境、およびエンクレーブ内で実行されているコードに関する証拠が [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] によって収集されます。 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] から、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] をホストしているマシンが登録されている HGS インスタンスに正常性証明書が要求されます。 詳細については、「[ホスト ガーディアン サービスにコンピューターを登録する](always-encrypted-enclaves-host-guardian-service-register.md)」を参照してください。
3. HGS によって証拠が検証され、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] に対して正常性証明書が発行されます。 HGS により、秘密キーを使用して正常性証明書が署名されます。
4. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] からクライアント ドライバーに正常性証明書が送信されます。
5. HGS 公開キーを取得するために、データベース接続用に指定された構成証明 URL でクライアント ドライバーから HGS への接続が行われます。 正常性証明書の署名がクライアント ドライバーによって検証されます。

構成の誤りにより、上記のワークフローのさまざまな手順でエラーが発生する可能性があります。 一般的ないくつかの構成証明エラー、その根本原因、および推奨されるトラブルシューティング手順を次に示します。

- 間欠的なネットワーク エラーのために、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] から HGS に接続できない (上記のワークフローの手順 2)。 接続の問題をトラブルシューティングするには、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの管理者が、そのコンピューターから HGS コンピューターに接続できることを確認する必要があります。
- 手順 3 の検証が失敗する。 検証の問題をトラブルシューティングするには、次のようにします。
  - [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの管理者がクライアント アプリケーション管理者と協力して、クライアント側の構成証明 URL で参照されているインスタンスと同じ HGS インスタンスに [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターが登録されていることを確認する必要があります。
  - [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの管理者が、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターで正常に構成証明ができることを確認する必要があります。そのためには、「[手順 5: ホストが正常に証明できることを確認する](always-encrypted-enclaves-host-guardian-service-register.md#step-5-confirm-the-host-can-attest-successfully)」の手順に従います。
- クライアント アプリケーションから HGS に接続して公開署名キーを取得することができない (手順 5)。 考えられる原因は次のとおりです。
  - アプリケーションと構成証明プロバイダーの間にある、いずれかのファイアウォールの構成によって、接続がブロックされる可能性があります。 アプリをホストしているコンピューターから HGS コンピューターに接続できることを確認します。

## <a name="in-place-encryption-errors"></a>インプレース暗号化のエラー

このセクションでは、インプレース暗号化のために `ALTER TABLE`/`ALTER COLUMN` を使用する場合に、(前のセクションで説明した構成証明のエラーに加えて) 発生する可能性のある一般的なエラーを示します。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。

- データの暗号化、暗号化の解除、または再暗号化に使用しようとしている列暗号化キーが、エンクレーブに対応していません。 インプレース暗号化の前提条件の詳細については、「[前提条件](always-encrypted-enclaves-configure-encryption.md#prerequisites)」を参照してください。 エンクレーブ対応キーをプロビジョニングする方法の詳細については、「[エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)」を参照してください。
- データベース接続に対して Always Encrypted とエンクレーブ計算を有効にしていません。 「[セキュリティで保護されたエンクレーブを使用してステートメントを実行するための前提条件](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves)」を参照してください。
- `ALTER TABLE`/`ALTER COLUMN` ステートメントで暗号化操作をトリガーし、列のデータ型を変更するか、現在の照合順序コード ページとは異なるコード ページを使用して照合順序を設定しています。 暗号化操作をデータ型または照合順序ページの変更と組み合わせることはできません。 この問題を解決するには、個別のステートメントを使用します (データ型または照合順序コード ページを変更するために 1 つのステートメント、およびインプレース暗号化のために別のステートメント)。

## <a name="errors-when-running-confidential-dml-queries-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用した機密 DML クエリ実行時のエラー

このセクションでは、セキュリティで保護されたエンクレーブを使用して機密 DML クエリを実行するときに、(前のセクションで説明した構成証明のエラーに加えて) 発生する可能性のある一般的なエラーを示します。

- クエリ対象の列に対して構成されている列暗号化キーが、エンクレーブ対応キーではありません。
- データベース接続に対して Always Encrypted とエンクレーブ計算を有効にしていません。 詳細については、「[セキュリティで保護されたエンクレーブを使用してステートメントを実行するための前提条件](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves)」を参照してください。
- クエリ対象の列で決定論的な暗号化を使用しています。 セキュリティで保護されたエンクレーブを使用した機密 DML クエリは、決定論的な暗号化の対象としてサポートされていません。 暗号化の種類をランダムへと変更する方法の詳細については、「[既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](always-encrypted-enclaves-enable-for-encrypted-columns.md)」を参照してください。
- クエリ対象の文字列型の列で、BIN2 または UTF-8 照合順序ではない照合順序を使用しています。 照合順序を BIN2 または UTF-8 に変更します。 詳細については、「[セキュリティで保護されたエンクレーブを使用する DML ステートメント](always-encrypted-enclaves-query-columns.md#dml-statements-using-secure-enclaves)」を参照してください。
- サポートされていない操作をクエリでトリガーしています。 エンクレーブ内でサポートされる操作の一覧については、「[セキュリティで保護されたエンクレーブを使用する DML ステートメント](always-encrypted-enclaves-query-columns.md#dml-statements-using-secure-enclaves)」を参照してください。
## <a name="next-steps"></a>次の手順

- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>関連項目

- [セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)
- [セキュリティで保護されたエンクレーブ列が設定された Always Encrypted でのインデックスの作成と使用](always-encrypted-enclaves-create-use-indexes.md)