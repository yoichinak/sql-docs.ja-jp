---
description: JDBC ドライバーの JDBC 4.3 への準拠
title: JDBC ドライバーの JDBC 4.3 への準拠 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ce01ec71649549166aa6a3d2f33d9dbb157e08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438354"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC ドライバーの JDBC 4.3 への準拠

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Microsoft JDBC Driver 6.4 for SQL Server より前のバージョンは、Java Database Connectivity (JDBC) API 4.2 仕様にのみ準拠しています。 このセクションは、6.4 リリースより前のバージョンには適用されません。

バージョン 6.4 以降、Microsoft jdbc Driver for SQL Server は JAVA 9 と互換性があり、メソッドが実装されていない新しい JDBC 4.3 API の `SQLFeatureNotSupportedException` をスローします。

Microsoft JDBC Driver 7.0 for SQL Server のリリースにより、ドライバーは Java 10 と互換性を持ち、以下の API をサポートするようになりました。 このドライバーは、JDBC 4.3 仕様の他の実装されていないメソッドの `SQLFeatureNotSupportedException` をスローします。

|新しい API|説明|注目に値する実装|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|この接続で要求 (独立した作業単位) が開始されることを示すドライバーへのヒント。 詳細については、「[java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)」を参照してください。|パブリック API メソッド `databaseAutoCommitMode`、`transactionIsolationLevel`、`networkTimeout`、`holdability`、`sendTimeAsDatetime`、`statementPoolingCacheSize`、`disableStatementPooling`、`serverPreparedStatementDiscardThreshold`、`enablePrepareOnFirstPreparedStatementCall`、`catalogName`、`sqlWarnings`、`useBulkCopyForBatchInsert` によって変更可能な接続フィールドの値を保存します。|
|void java.sql.connection.endRequest()|要求 (独立した作業単位) が完了したことを示すドライバーへのヒント。 詳細については、「[java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)」を参照してください。|作業単位中に作成されたステートメントを閉じ、開いているすべてのトランザクションをロールバックします。 このメソッドはさらに、上記の接続フィールドに対する変更を元に戻します。|
