---
title: セキュア エンクレーブを使用する Always Encrypted
description: セキュリティで保護されたエンクレーブが設定された SQL Server の Always Encrypted について説明します。
ms.custom: seo-lt-2019
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: e84635c1f32396e033841c546dafc1796624d5ab
ms.sourcegitcommit: b1cec968b919cfd6f4a438024bfdad00cf8e7080
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99237084"
---
# <a name="always-encrypted-with-secure-enclaves"></a>セキュア エンクレーブを使用する Always Encrypted

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用すると、インプレース暗号化と豊富な機密クエリが有効になることで、[Always Encrypted](always-encrypted-database-engine.md) の機密コンピューティング機能が拡張されます。 セキュリティで保護されたエンクレーブが設定された Always Encrypted は、[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] と [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] (プレビュー) で利用できます。

2015 の [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] および [!INCLUDE[sssql16](../../../includes/sssql16-md.md)] で導入された Always Encrypted により、注意が必要なデータの機密性が、マルウェアや、次のような高い特権を持つ "*未承認の*" SQL ユーザーから保護されます: サーバー インスタンスやハードウェアなどに対する正当なアクセス権を持ちながら、実際のデータの一部またはすべてにアクセスしてはならない、DBA、コンピューター管理者、クラウド管理者、その他のユーザー。  

この記事で説明されている拡張機能を使用しないと、データは、Always Encrypted により、クライアント側で暗号化され、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]内でデータまたは対応する暗号化キーをプレーンテキストで表示 "*できない*" ようにすることで保護されます。 その結果、データベース内の暗号化された列に対する機能が大幅に制限されます。 暗号化されたデータに対して[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]で実行できる操作は、等価比較のみです ([決定論的暗号化](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)でのみ使用できます)。 暗号化操作 (最初のデータ暗号化や、キーのローテーション) や高度なクエリ (パターン マッチングなど) などの他のすべての操作は、データベース内ではサポートされていません。 ユーザーがクライアント側でこのような操作を実行するには、データベースの外部にデータを移動する必要があります。

"*セキュリティで保護されたエンクレーブ*" が設定された Always Encrypted では、サーバー側のセキュリティで保護されたエンクレーブ内でプレーンテキストに対する一部の計算を許可することにより、このような制限に対応しています。 セキュリティで保護されたエンクレーブは、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)] プロセス内のメモリの保護された領域です。 セキュリティで保護されたエンクレーブは、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]の他の部分や、ホスティング マシン上の他のプロセスからは、不透明なボックスとして認識されます。 デバッガーを使用しても、外部からエンクレーブ内のデータやコードを表示する方法はありません。 これらの特徴により、セキュリティで保護されたエンクレーブは "*高信頼実行環境*" になり、データの機密性を損なうことなく、プレーンテキストで暗号化キーと機密データに安全にアクセスできます。

Always Encrypted は、次の図のようにセキュリティで保護されたエンクレーブを使用します。

![データ フロー (data flow)](./media/always-encrypted-enclaves/ae-data-flow.png)

アプリケーションによって送信された Transact-SQL ステートメントを解析するときは、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]により、セキュリティで保護されたエンクレーブを使用する必要がある暗号化されたデータに対する操作がステートメントに含まれているかどうかが判断されます。 そのようなステートメントの場合:

- クライアント ドライバーにより、操作に必要な列の暗号化キーが (セキュリティで保護されたチャネルを介して) セキュリティで保護されたエンクレーブに送信され、実行するステートメントが送信されます。

- ステートメントを処理するときは、[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]により、暗号化された列に対する暗号化操作または計算が、セキュリティで保護されたエンクレーブに委任されます。 必要に応じて、エンクレーブによりデータが解読され、プレーンテキストで計算が実行されます。

ステートメントの処理の間、データと列暗号化キーのどちらも、セキュリティで保護されたエンクレーブの外部にある[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]において、プレーンテキストで公開されることはありません。

## <a name="supported-enclave-technologies"></a>サポートされているエンクレーブ テクノロジ

[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] のセキュリティで保護されたエンクレーブが設定された Always Encrypted は、Windows で[仮想化ベースのセキュリティ (VBS)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) のセキュリティで保護されたメモリ エンクレーブ (仮想保護モード (VSM) エンクレーブとも呼ばれます) を使用します。

[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] では、セキュリティで保護されたエンクレーブが設定された Always Encrypted により、[Intel Software Guard Extensions (Intel SGX)](https://itpeernetwork.intel.com/microsoft-azure-confidential-computing/) のエンクレーブが使用されます。 Intel SGX は、[DC シリーズ](https://docs.microsoft.com/azure/azure-sql/database/service-tiers-vcore?tabs=azure-portal#dc-series)のハードウェア構成を使用するデータベースでサポートされる、ハードウェアベースの信頼された実行環境テクノロジです。

## <a name="secure-enclave-attestation"></a>セキュリティで保護されたエンクレーブの構成証明

[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]内のセキュリティで保護されたエンクレーブからは、機密データと列暗号化キーにプレーンテキストでアクセスできます。 このため、エンクレーブ計算が含まれるステートメントが[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]に送信される前に、アプリケーション内のクライアント ドライバーにより、セキュリティで保護されたエンクレーブが正規の VBS または SGX エンクレーブであること、および、セキュリティで保護されたエンクレーブ内で実行されるコードが、インプレース暗号化および機密クエリでサポートされる操作のための Always Encrypted の暗号化アルゴリズムが実装されている、正規の Always Encrypted ライブラリであることが、確認される必要があります。

エンクレーブを検証するプロセスは、**エンクレーブの構成証明** と呼ばれ、アプリケーション内のクライアント ドライバーと、外部の構成証明サービスに接続する[!INCLUDE[ssde-md](../../../includes/ssde-md.md)]の両方が含まれます。 構成証明プロセスの詳細は、エンクレーブの種類 (VBS または SGX) と、構成証明サービスによって異なります。

[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] での VBS のセキュリティで保護されたエンクレーブに対する構成証明プロセスは [Windows Defender System Guard ランタイム構成証明](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/)であり、構成証明サービスとしてホスト ガーディアン サービス (HGS) が必要です。 

[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] での Intel SGX エンクレーブの構成証明には、[Microsoft Azure Attestation](https://docs.microsoft.com/azure/attestation/overview) が必要です。

> [!NOTE]
> [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] では、Microsoft Azure Attestation はサポートされていません。 [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] での VBS エンクレーブに対してサポートされている唯一の構成証明ソリューションは、ホスト ガーディアン サービスだけです。

## <a name="supported-client-drivers"></a>サポートされるクライアント ドライバー

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するには、アプリケーションでこの機能をサポートするクライアント ドライバーを使用する必要があります。 エンクレーブの計算とエンクレーブの構成証明が有効になるように、アプリケーションとクライアント ドライバーを構成します。 サポートされているクライアント ドライバーの一覧などの詳細については、「[Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)」を参照してください。

## <a name="terminology"></a>用語

### <a name="enclave-enabled-keys"></a>エンクレーブ対応キー

セキュリティで保護されたエンクレーブが設定された Always Encrypted では、エンクレーブ対応キーの概念が導入されました。

- **エンクレーブ対応の列マスター キー** - データベース内の列マスター キー メタデータ オブジェクトで `ENCLAVE_COMPUTATIONS` プロパティが指定されている列マスター キー。 列マスター キー メタデータ オブジェクトには、メタデータ プロパティの有効な署名も含める必要があります。 詳細については、「[CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)」を参照してください
- **エンクレーブ対応列暗号化キー**: エンクレーブ対応列マスター キーで暗号化された列暗号化キーです。 セキュリティで保護されたエンクレーブ内での計算に使用できるのは、エンクレーブ対応の列暗号化キーだけです。 

詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーの管理](always-encrypted-enclaves-manage-keys.md)」を参照してください。

### <a name="enclave-enabled-columns"></a>エンクレーブ対応列

エンクレーブ対応列は、エンクレーブ対応列暗号化キーを使用して暗号化されたデータベース列です。

## <a name="confidential-computing-capabilities-for-enclave-enabled-columns"></a>エンクレーブ対応列のための機密コンピューティング機能

セキュリティで保護されたエンクレーブが設定された Always Encrypted の 2 つの主な利点は、インプレース暗号化と豊富な機密クエリです。

### <a name="in-place-encryption"></a>インプレース暗号化

インプレース暗号化を使用すると、データをデータベースの外部に移動することなく、セキュリティで保護されたエンクレーブ内でデータベース列の暗号化操作を行うことができます。 インプレース暗号化により、暗号化のパフォーマンスと信頼性が向上します。 インプレース暗号化は、[ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) ステートメントを使用して実行できます。 

インプレースでサポートされる暗号化操作は次のとおりです。

- エンクレーブ対応の列暗号化キーによるプレーンテキストの列の暗号化。
- 次のことを目的とする、暗号化されたエンクレーブ対応列の再暗号化:
  - 列暗号化キーのローテーション - 新しいエンクレーブ対応列暗号化キーを使用して列を再暗号化します。
  - エンクレーブ対応列の暗号化の種類の変更 (たとえば、決定論的からランダム化に)。
- エンクレーブ対応列に格納されているデータの解読 (列からプレーンテキスト列への変換)。

暗号化操作に含まれる列暗号化キーがエンクレーブ対応である限り、決定論的とランダム化の両方の暗号化で、インプレース暗号化を使用できます。

### <a name="confidential-queries"></a>機密クエリ

機密クエリは、セキュリティで保護されたエンクレーブ内で実行されるエンクレーブ対応列の操作を伴う [DML クエリ](../../../t-sql/queries/queries.md)です。

セキュリティで保護されたエンクレーブでサポートされる操作は次のとおりです。

| 操作| [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] | [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] |
|:---|:---|:---|
| [比較演算子](../../../mdx/comparison-operators.md) | サポートされています | サポートされています |
| [BETWEEN (Transact-SQL)](../../../t-sql/language-elements/between-transact-sql.md) | サポートされています | サポートされています |
| [IN (Transact-SQL)](../../../t-sql/language-elements/in-transact-sql.md) | サポートされています | サポートされています |
| [LIKE (Transact-SQL)](../../../t-sql/language-elements/like-transact-sql.md) | サポートされています | サポートされています |
| [DISTINCT](../../../t-sql/queries/select-transact-sql.md#c-using-distinct-with-select) | サポートされています | サポートされています |
| [結合](../../performance/joins.md) | 入れ子になったループ結合のみがサポートされます | サポートされています |
| [SELECT - ORDER BY 句 (Transact-SQL)](../../../t-sql/queries/select-order-by-clause-transact-sql.md) | サポートされていません | サポートされています |
| [SELECT - GROUP BY- Transact-SQL](../../../t-sql/queries/select-group-by-transact-sql.md) | サポートされていません | サポートされています |

> [!NOTE]
> セキュリティで保護されたエンクレーブでの上記の操作は、**ランダム化された** 暗号化を使用するエンクレーブ対応列でのみサポートされており、決定論的な暗号化ではサポートされていません。 決定論的な暗号化を使用する列でサポートされている計算が等価比較だけであることは変わらず、列がエンクレーブ対応かどうかにかかわらず、エンクレーブの外部で暗号文を比較することによって実行されます。 等価比較に関連する次の操作が、決定論的な暗号化でサポートされています。 
> - ポイント参照、検索、結合での [= (等しい)](../../../t-sql/language-elements/equals-transact-sql.md)
> - [IN](../../../t-sql/language-elements/in-transact-sql.md)
> - [SELECT - GROUP BY](../../../t-sql/queries/select-group-by-transact-sql.md)
> - [DISTINCT](../../../t-sql/queries/select-transact-sql.md#c-using-distinct-with-select)
>
> [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] では、文字列型の列 (`char`、`nchar`) に対してエンクレーブを使用する機密クエリを実行するには、列でバイナリ 2 並べ替え順序 (BIN2) の照合順序が使用されている必要があります。 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] で文字列に対して機密クエリを実行するには、BIN2 照合順序または UTF-8 照合順序が必要です。 

### <a name="indexes-on-enclave-enabled-columns"></a>エンクレーブ対応列でのインデックス

ランダム化された暗号化を使用してエンクレーブ対応列で非クラスター化インデックスを作成することにより、セキュリティで保護されたエンクレーブを使用する機密 DML クエリの実行を高速化できます。

ランダム化された暗号化を使用して暗号化された列のインデックスで、機密データが漏えいしないようにするため、インデックス データ構造 (B ツリー) 内のキーの値は、プレーンテキストの値に基づいて暗号化され、並べ替えられます。 プレーンテキスト値による並べ替えは、エンクレーブ内でのクエリの処理にも役立ちます。 [!INCLUDE[ssde-md](../../../includes/ssde-md.md)]内のクエリ Executor により、エンクレーブ内での計算のために暗号化された列のインデックスが使用されるときに、インデックスを検索して列に格納されている特定の値が探索されます。 各検索には、複数の比較が含まれる場合があります。 クエリ Executor では各比較がエンクレーブにデリゲートされ、エンクレーブでは列に格納されている値と比較対象の暗号化されたインデックス キーの値が復号化されて、プレーンテキストで比較が実行された後、比較の結果が Executor に返されます。

ランダム化された暗号化を使用し、エンクレーブ対応ではない列でのインデックスの作成は、やはりサポートされていません。

決定論的な暗号化を使用する列でのインデックスは、列がエンクレーブ対応かどうかに関係なく、(プレーンテキストではなく) 暗号化テキストに基づいて並べ替えられます。

詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)」を参照してください。 [!INCLUDE[ssde-md](../../../includes/ssde-md.md)]でのインデックス作成のしくみに関する一般的な情報については、「[クラスター化インデックスと非クラスター化インデックスの概念](../../indexes/clustered-and-nonclustered-indexes-described.md)」の記事を参照してください。

### <a name="database-recovery"></a>データベースの回復

SQL Server のインスタンスで障害が発生した場合、そのデータベースは、完了しなかったトランザクションによる変更がデータ ファイルに含まれ状態のままになる可能性があります。 インスタンスが起動されると、[データベース復旧](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started)と呼ばれるプロセスが実行されます。このプロセスでは、トランザクション ログで見つかったすべての未完了のトランザクションがロールバックされて、データベースの整合性が保持されます。 未完了のトランザクションによってインデックスの変更が行われた場合、それらの変更も元に戻す必要があります。 たとえば、インデックス内の一部のキー値は、削除するか、再挿入する必要があります。

> [!IMPORTANT]
> ランダム化された暗号化を使用して暗号化されているエンクレーブ対応の列で最初のインデックスを作成する **前** に、データベースに対して [高速データベース復旧 (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) を有効にすることを強くお勧めします。 ADR は、[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] では既定で有効になりますが、[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] ではなりません。

[従来のデータベース復旧プロセス](/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) ([ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf) 復旧モデルに従うもの) では、インデックスに対する変更を元に戻すには、アプリケーションが列の列暗号化キーをエンクレーブに提供するまで SQL Server は待機する必要があり、長くかかることがあります。 高速データベース復旧 (ADR) を使用すると、エンクレーブ内のキャッシュで列暗号化キーを使用できないために遅延する必要がある元に戻す操作の数が、劇的に減少します。 その結果、新しいトランザクションがブロックされる可能性が最小限になり、データベースの可用性が大幅に向上します。 ADR を有効にしても、SQL Server ではやはり古いデータ バージョンのクリーンアップを完了するために列暗号化キーが必要になる場合がありますが、データベースまたはユーザーのトランザクションの可用性に影響を与えないバックグラウンド タスクとして行われます。 ただし、列暗号化キーがないためにクリーンアップ操作が失敗したことを示すエラー メッセージが、エラー ログに記録されることがあります。

## <a name="security-considerations"></a>セキュリティに関する考慮事項

セキュリティで保護されたエンクレーブが設定された Always Encrypted に対しては、次のセキュリティに関する考慮事項が適用されます。

- エンクレーブ内のデータのセキュリティは、構成証明プロトコルと構成証明サービスに依存します。 そのため、構成証明サービスと、構成証明サービスによって適用される構成証明ポリシーを、信頼できる管理者が管理する必要があります。 また、通常、構成証明サービスではさまざまなポリシーと構成証明プロトコルがサポートされており、そのうちの一部は、エンクレーブとその環境の最小限の検証を実行する、テストと開発用に設計されたものです。 お使いの構成証明サービスに固有のガイドラインに厳密に従って、運用環境の配置には推奨される構成とポリシーを使うようにしてください。 
- エンクレーブ対応の列暗号化キーでランダム化された暗号化を使用して列を暗号化すると、列による範囲比較のサポートのため、列に格納されたデータの順序がリークする可能性があります。 たとえば、従業員の給与が含まれる暗号化された列にインデックスがある場合、悪意のある DBA はインデックスをスキャンして暗号化された給与の最大値を検索し、給与が最高の個人を特定できます (ユーザーの名前は暗号化されていないものとします)。 
- Always Encrypted を使用して、DBA による不正アクセスから機密データを保護する場合は、列マスター キーまたは列暗号化キーを DBA と共有しないでください。 DBA は、キーに直接アクセスできなくても、エンクレーブ内の列暗号化キーのキャッシュを利用して、暗号化された列のインデックスを管理できます。

## <a name="considerations-for-business-continuity-disaster-recovery-and-data-migration"></a><a name="anchorname-1-considerations-availability-groups-db-migration"></a> 事業継続、ディザスター リカバリー、データ移行に関する考慮事項

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するデータベース用に高可用性またはディザスター リカバリー ソリューションを構成するときは、すべてのデータベース レプリカでセキュリティで保護されたエンクレーブを使用できることを確認します。 プライマリ レプリカにはエンクレーブを使用できても、セカンダリ レプリカには使用できない場合、セキュリティで保護されたエンクレーブが設定された Always Encrypted の機能を使用しようとするすべてのステートメントは、フェールオーバー後に失敗します。

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用してデータベースをコピーまたは移行するときは、ターゲット環境でエンクレーブが常にサポートされていることを確認します。 そうでない場合、エンクレーブを使用するステートメントは、コピーまたは移行されたデータベースで機能しません。

留意する必要のある具体的な考慮事項をいくつか示します。

- **SQL Server**
  - [Always On 可用性グループ](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)を構成するときは、可用性グループ内のデータベースがホストされてい各 SQL Server インスタンスで、セキュリティで保護されたエンクレーブが設定された Always Encrypted がサポートされ、エンクレーブと構成証明が構成されていることを確認します。
  - エンクレーブが構成されていない SQL Server インスタンスで、セキュリティで保護されたエンクレーブが設定された Always Encrypted の機能を使用するデータベースのバックアップ ファイルから復元すると、復元操作は成功し、エンクレーブに依存しないすべての機能が使用可能になります。 しかし、エンクレーブ機能を使用する後続のステートメントは失敗し、ランダム化された暗号化を使用するエンクレーブ対応列のインデックスは無効になります。 エンクレーブが構成されていないインスタンスで、セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するデータベースをアタッチしたときも、同じようになります。
  - ランダム化された暗号化を使用するエンクレーブ対応列のインデックスがデータベースに含まれる場合は、データベースのバックアップを作成する前に、データベースで[高速データベース復旧 (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) を有効にします。 ADR では、データベースを復元した後すぐに、インデックスも含めて、データベースを使用できることが保証されます。 詳しくは、「[データベース復旧](#database-recovery)」をご覧ください。
  
- **Azure SQL Database**
  - [アクティブ geo レプリケーション](https://docs.microsoft.com/azure/azure-sql/database/active-geo-replication-overview)を構成するとき、セキュリティで保護されたエンクレーブがプライマリ データベースでサポートされている場合は、セカンダリ データベースでもそうであることを確認します。

SQL Server と Azure SQL Database の両方で、bacpac ファイルを使用してデータベースを移行するときは、bacpac ファイルを作成する前に、ランダム化された暗号化を使用するエンクレーブ対応列のすべてのインデックスを削除する必要があります。

## <a name="known-limitations"></a>既知の制限事項

「[エンクレーブ対応列のための機密コンピューティング機能](#confidential-computing-capabilities-for-enclave-enabled-columns)」で説明したように、セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用すると、インプレース暗号化と、インデックスを使用した豊富な機密クエリがサポートされることで、Always Encrypted のいくつかの制限が対処されます。

「[機能の詳細](always-encrypted-database-engine.md#feature-details)」に記載されている Always Encrypted での他のすべての制限は、セキュリティで保護されたエンクレーブが設定された Always Encrypted にも適用されます。

次の制限事項は、セキュリティで保護されたエンクレーブが設定された Always Encrypted に固有のものです。

- ランダム化された暗号化を使用するエンクレーブ対応の列では、クラスター化インデックスを作成できません。
- ランダム化された暗号化を使用するエンクレーブ対応の列を、主キー列にすることはできず、外部キー制約または一意キー制約によって参照することはできません。
- [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] の場合 (この制限は [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] には適用されません)、ランダム化された暗号化を使用するエンクレーブ対応列では、入れ子になったループ結合 (可能な場合はインデックスを使用) のみがサポートされます。 異なる製品間のその他の違いについては、「[機密クエリ](#confidential-queries)」を参照してください。
- 同じコード ページ内の照合順序および NULL 値の許容の変更を除き、インプレース暗号化操作を、列メタデータの他の変更と組み合わせることはできません。 たとえば、1 つの `ALTER TABLE`/`ALTER COLUMN` Transact-SQL ステートメントで列を暗号化、再暗号化、または復号化し、さらに列のデータ型を変更することはできません。 2 つの異なるステートメントを使用します。
- インメモリ テーブルの列にエンクレーブ対応キーを使用することは、サポートされていません。
- 計算列を定義する式では、ランダム化された暗号化を使用してエンクレーブが有効な列の計算を実行することはできません (計算が「[機密クエリ](#confidential-queries)」に記載されているサポート対象の操作に含まれる場合でも)。
- ランダム化された暗号化を使用するエンクレーブ対応の列では、LIKE 演算子のパラメーターでのエスケープ文字はサポートされていません。
- (暗号化の後でラージ オブジェクトになる) 次のデータ型のいずれかを使用するクエリ パラメーターを持つ LIKE 演算子または比較演算子を含むクエリでは、インデックスは無視され、テーブル スキャンが実行されます。
  - `nchar[n]`、`nvarchar[n]` (n が 3967 より大きい場合)。
  - `char[n]`、`varchar[n]`、`binary[n]`、`varbinary[n]` (n が 7935 より大きい場合)。
- ツールの制限事項:
  - エンクレーブ対応列マスター キーを格納するためにサポートされるキー ストアは、Windows 証明書ストアと Azure Key Vault のみです。
  - エンクレーブ対応のキーが含まれるデータベースのインポート/エクスポートは、サポートされていません。
  - `ALTER TABLE`/`ALTER COLUMN` を使用してインプレース暗号化操作をトリガーするには、SSMS でクエリ ウィンドウを使用してステートメントを発行するか、ステートメントを発行する独自のプログラムを作成する必要があります。 現在、SqlServer PowerShell モジュールの Set-SqlColumnEncryption コマンドレットと SQL Server Management Studio の Always Encrypted ウィザードでは、インプレース暗号化はサポートされていません。操作に使用される列暗号化キーがエンクレーブ対応であっても、暗号化操作のためにデータベースからデータが移動されます。

## <a name="next-steps"></a>次のステップ

- [チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を構成して使用する](configure-always-encrypted-enclaves.md)

## <a name="see-also"></a>関連項目

- [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](always-encrypted-enclaves-manage-keys.md)