---
description: フルテキスト インデックスの作成のトラブルシューティング
title: フルテキスト インデックスの作成のトラブルシューティング | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c11c753528ed4fdc723ee45884093d9c5ec95dc8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88325903"
---
# <a name="troubleshoot-full-text-indexing"></a>フルテキスト インデックスの作成のトラブルシューティング
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
     
##  <a name="troubleshoot-full-text-indexing-failures"></a><a name="failure"></a> フルテキスト インデックスの作成エラーのトラブルシューティング  
 フルテキスト インデックスの作成時または保守時には、後述の理由により、フルテキスト インデクサーが 1 つ以上の行のインデックス作成に失敗することがあります。 このような行レベルのエラーでは、インデックスの作成は中止されることなく完了します。 インデクサーは、エラーが発生した行をスキップします。そのため、エラーが発生した行に含まれる内容のクエリはできません。  
  
 インデックス作成は、次の場合に失敗する可能性があります。  
  
-   インデクサーが、フィルター コンポーネントやワード ブレーカー コンポーネントを検出できないか、読み込むことができない。 このエラーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに登録されていない言語のドキュメント形式や内容がテーブル行に含まれる場合に発生することがあります。 また、登録済みのワード ブレーカー コンポーネントやフィルター コンポーネントを読み込むときに、コンポーネントに署名されていないか、署名の検証に失敗した場合にも発生します。  
  
-   ワード ブレーカーやフィルターなどのコンポーネントが失敗してインデクサーにエラーを返す。 このエラーは、インデックスが作成されたドキュメントが破損し、フィルターがドキュメントからテキストを抽出できない場合に発生することがあります。 また、フルテキスト フィルター デーモン ホスト (fdhost.exe) でのメモリ制限により、1 行の内容が一定サイズを超え、コンポーネントでは処理できない場合にも発生することがあります。  
  
 行レベルのエラーが発生するたびに、クロール ログにエラーの理由の詳細が記録されます。 エラー数は、完全作成または増分作成の最後に集計されます。  
  
 他に、インデックス作成のプロセス自体に影響を与え、作成を完了できない次のようなエラーもあります。  
  
-   フルテキスト インデックスが、フルテキスト カタログに含むことができる行数の制限を超える。  
  
-   インデックスが作成されているテーブルのクラスター化インデックスまたはフルテキスト キー インデックスが変更、削除または再構築される。  
  
-   ハードウェア エラーやディスクの破損などによりフルテキスト カタログが破損する。  
  
-   フルテキスト インデックスが作成されているテーブルを含むファイル グループがオフラインになるか、読み取り専用になる。  
  
 すべての重要なフルテキスト インデックス作成操作の最後、または作成が完了していないことがわかったときは、クロール ログを確認します。  
  
### <a name="unsigned-components"></a>署名されていないコンポーネント  
 既定では、フルテキスト インデクサーでは、読み込むフィルターやワード ブレーカーに署名が必要です。 コンポーネントに署名されていない場合、つまり署名されていないカスタム コンポーネントをインストールする可能性がある場合は、署名の検証が無視されるようにフルテキスト インデクサーを構成する必要があります。  
  
> [!IMPORTANT]  
>  署名の検証を無視すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのセキュリティが低くなります。 実装するすべてのコンポーネントに署名するか、入手するすべてのコンポーネントの署名を確認することをお勧めします。 コンポーネントの署名についての詳細は、「[sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)」を参照して下さい。  
  
  
##  <a name="full-text-index-in-inconsistent-state-after-transaction-log-restored"></a><a name="state"></a> トランザクション ログの復元後のフルテキスト インデックスの一貫性の喪失  
 データベースのトランザクション ログを復元する場合、フルテキスト インデックスの状態に一貫性がないという警告が表示されることがあります。 この警告の原因は、データベースのバックアップ後にテーブルのフルテキスト インデックスが変更されたことにあります。 フルテキスト インデックスを一貫性のある状態に戻すには、テーブルに対してすべてのカタログの作成 (クロール) を実行します。 詳細については、「 [フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)」をご覧ください。  
  
  
## <a name="see-also"></a>関連項目  
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
