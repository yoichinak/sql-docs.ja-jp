---
title: Transact-SQL ステートメント
description: Transact-SQL ステートメント
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Alter_TSQL
dev_langs:
- TSQL
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.custom: ''
ms.date: 04/17/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65f48884fff2fc5ce9fc018f8d79b3c2da5a4770
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98079756"
---
# <a name="transact-sql-statements"></a>Transact-SQL ステートメント

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL ステートメントは作業のアトミック単位であり、完全に成功するか完全に失敗するかのどちらかです。 SQL ステートメントは、識別子、パラメーター、変数、名前、データ型、および正常にコンパイルされる SQL 予約語で構成された命令のセットです。 `BeginTransaction` コマンドによってトランザクションの開始が指定されない場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって SQL ステートメントに対する "*暗黙の*" トランザクションが作成されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は常に、ステートメントが成功した場合に暗黙のトランザクションをコミットし、コマンドが失敗した場合に暗黙のトランザクションをロールバックします。  

ステートメントにはさまざまな種類があります。 おそらく、最も重要なのは [SELECT](../queries/select-transact-sql.md) です。これを使うと、データベースから行を取得したり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、1 つ以上のテーブルから 1 つ以上の行または列を選択することができます。 この記事には、`SELECT` ステートメントに加えて、Transact-SQL (T-SQL) で使うステートメントのカテゴリがまとめられています。 左側のナビゲーションでは、すべてのステートメントを確認できます。

## <a name="backup-and-restore"></a>バックアップと復元

バックアップおよび復元のステートメントは、バックアップを作成し、バックアップから復元する手段を提供します。  詳しくは、[バックアップと復元の概要](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)に関するページをご覧ください。

## <a name="data-definition-language"></a>データ定義言語

データ定義言語 (DDL) ステートメントはデータ構造を定義します。 これらのステートメントを使って、データベースのデータ構造を作成、変更、または削除できます。 これらのステートメントには、次のものがあります。

- ALTER
- 照合順序
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS
- TRUNCATE TABLE

## <a name="data-manipulation-language"></a>データ操作言語

データ操作言語 (DML) は、データベースに格納される情報に影響します。 データベースの行を挿入、更新、変更するには、以下のステートメントを使います。

- BULK INSERT
- DELETE
- INSERT
- SELECT
- UPDATE
- MERGE

## <a name="permissions-statements"></a>権限ステートメント

権限ステートメントは、どのユーザーとログインがデータにアクセスして操作を実行できるかを決定します。 認証とアクセスについて詳しくは、[セキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)に関するページをご覧ください。

## <a name="service-broker-statements"></a>Service Broker のステートメント

Service Broker は、メッセージング アプリケーションおよびキューイング アプリケーションのネイティブ サポートを提供する機能でます。 詳しくは、[Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md) に関するページをご覧ください。

## <a name="session-settings"></a>セッションの設定

SET ステートメントは、現在のセッションが実行時の設定を処理する方法を指定します。 概要については、「[SET ステートメント](set-statements-transact-sql.md)」をご覧ください。
