---
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを SSMS で実行する
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを SSMS で実行する | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 74149cdcf8dd12280103c592c5a8662dddf4e750
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470094"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを SSMS で実行する
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

この記事では、SQL Server Management Studio を使用して、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) に対するサーバー側のセキュリティで保護されたエンクレーブを使用する、次のようなクエリを発行する方法について説明します。
- インプレース暗号操作をトリガーするクエリ。
- エンクレーブ対応キーで暗号化された列に対する範囲比較やパターン マッチング操作など、高度な計算をトリガーするクエリ。
- ランダム化された暗号化およびエンクレーブ対応キーを使用して、暗号化された列のインデックスを作成または更新するクエリ。  

SSMS を使用して、セキュリティで保護されたエンクレーブが使用されている暗号化された列に対してクエリを実行するには、「[SQL Server Management Studio で Always Encrypted を使用した列のクエリを実行する](always-encrypted-query-columns-ssms.md)」の説明に従います。 ここでは、注意する必要のあるエンクレーブに固有の事柄を示します。

- SSMS バージョン18.3 以降が必要です。
- Always Encrypted とエンクレーブ計算が有効になっている接続から、セキュリティで保護されたエンクレーブを使用しているクエリ ウィンドウで、クエリを実行します。 詳しい手順については、「[チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)」および「[データベース接続での Always Encrypted の有効化と無効化](always-encrypted-query-columns-ssms.md#en-dis)」をご覧ください。

## <a name="next-steps"></a>次の手順
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>参照  
- [チュートリアル:SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)
- [セキュリティで保護されたエンクレーブ列が設定された Always Encrypted でのインデックスの作成と使用](always-encrypted-enclaves-create-use-indexes.md)

