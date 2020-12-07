---
description: 透過的なネットワーク IP の解決の使用
title: 透過的なネットワーク IP の解決の使用 | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: chris-rossi
ms.author: v-chross
ms.openlocfilehash: adaad0f80d6304c855af22f134d24f0d3f23d301
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88415018"
---
# <a name="using-transparent-network-ip-resolution"></a>透過的なネットワーク IP の解決の使用
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>目的
透過的なネットワーク IP の解決 (TNIR) は、既存の MultiSubnetFailover 機能の改訂です。 TNIR は、ホスト名の解決された最初の IP が応答せず、ホスト名に複数の IP が関連付けられている場合に、ドライバーの接続シーケンスに影響を及ぼします。 TNIR は、MultiSubnetFailover と連動して、次の 3 つの接続シーケンスを提供します。<br />
* 0:1 つの IP が試行され、その後にすべての IP が並列で試行されます
* 1:すべての IP が並列で試行されます
* 2:すべての IP が 1 つずつ試行されます

|TransparentNetworkIPResolution|MultiSubnetFailover|動作|
|--------|--------|--------|
|True|True|1|
|正しい|誤り|0|
|False|True|1|
|False|False|2|

## <a name="setting-transparent-network-ip-resolution"></a>透過的なネットワーク IP の解決の設定
TransparentNetworkIPResolution は既定では有効になっています。 MultiSubnetFailover は既定では無効になっています。 次のページでは、これらのプロパティを設定する方法の詳細を説明しています。 
- [OLE DB Driver for SQL Server での接続文字列キーワードの使用](..\applications\using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初期化プロパティと承認プロパティ](..\ole-db-data-source-objects\initialization-and-authorization-properties.md)

## <a name="see-also"></a>参照 
[OLE DB Driver for SQL Server の高可用性、ディザスター リカバリーに関するサポート](./oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)
