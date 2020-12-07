---
description: Microsoft Drivers for PHP for SQL Server における高可用性とディザスター リカバリーのサポート
title: Microsoft SQL Server 用 Drivers for PHP における高可用性とディザスター リカバリーのサポート | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875c5944a0b74c7140843388da1e783e9f2ba5b8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726761"
---
# <a name="support-for-high-availability-disaster-recovery"></a>高可用性、障害復旧のサポート
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、高可用性とディザスター リカバリーのための [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] のサポート (バージョン 3.0 で追加されています) について説明します。

Microsoft SQL Server 用 Drivers for PHP のバージョン 3.0 以降では、高可用性の可用性グループ リスナー、ディザスター リカバリーの可用性グループ、またはサーバーとしてのフェールオーバー クラスター インスタンスを、接続文字列の中で指定できます。

**MultiSubnetFailover** 接続プロパティを指定すると、アプリケーションが可用性グループまたはフェールオーバー クラスター インスタンスに配置され、ドライバーでは、すべての IP アドレスに対して接続を試行することで、プライマリ SQL Server インスタンス上のデータベースへの接続が試行されます。 SQL Server 可用性グループ リスナーまたは SQL Server フェールオーバー クラスター インスタンスに接続するときには、必ず **MultiSubnetFailover=True** を指定してください。 フェールオーバーが発生した AlwaysOn データベースにアプリケーションが接続されている場合、元の接続は切断され、アプリケーションではフェールオーバー後に処理を続行するために新しい接続を開く必要があります。

Always On 可用性グループの完全な詳細については、[高可用性とディザスター リカバリー](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)に関するドキュメントのページを参照してください。

## <a name="transparent-network-ip-resolution-tnir"></a>透過的なネットワーク IP の解決 (TNIR)

透過的なネットワーク IP の解決 (TNIR) は、既存の **MultiSubnetFailover** 機能の改訂です。 ホスト名の解決された最初の IP が応答せず、ホスト名に複数の IP が関連付けられている場合、ドライバーの接続シーケンスに影響を及ぼします。 対応する接続オプションは **TransparentNetworkIPResolution** です。 **MultiSubnetFailover** と共に、次の 4 つの接続シーケンスが提供されています。 

- TNIR が有効かつ **MultiSubnetFailover** が無効になっている:1 つの IP が試行され、その後にすべての IP が並列で試行されます
- TNIR が有効かつ **MultiSubnetFailover** が有効になっている:すべての IP が並列で試行されます
- TNIR が無効かつ **MultiSubnetFailover** が無効になっている:すべての IP が 1 つずつ試行されます
- TNIR が無効かつ **MultiSubnetFailover** が有効になっている:すべての IP が並列で試行されます

TNIR は既定で有効になっており、**MultiSubnetFailover** は既定で無効になっています。

次に、PDO_SQLSRV ドライバーを使用して、TNIR と **MultiSubnetFailover** の両方を有効にする例を示します。

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>データベース ミラーリングから複数のサブネット クラスターを使用するためのアップグレード  
接続文字列に **MultiSubnetFailover** および **Failover_Partner** の接続キーワードが存在する場合、接続エラーが発生します。 また、**MultiSubnetFailover** が使用されており、データベース ミラーリング ペアに属していることを示すフェールオーバー パートナーの応答が SQL Server から返された場合にも、エラーが発生します。  
  
現在データベース ミラーリングを使用している PHP アプリケーションをマルチサブネットのシナリオにアップグレードする場合は、**Failover_Partner** 接続プロパティを削除して **True** に設定した **MultiSubnetFailover** に置き換え、接続文字列内のサーバー名を可用性グループ リスナーに置き換えます。 接続文字列で **Failover_Partner** および **MultiSubnetFailover=true** が使用されている場合、ドライバーでエラーが発生します。 ただし、接続文字列に **Failover_Partner** と **MultiSubnetFailover=false** (または **ApplicationIntent=ReadWrite**) が使用されている場合、アプリケーションではデータベース ミラーリングが使用されます。  
  
AG のプライマリ データベースでデータベース ミラーリングが使用されている場合、および可用性グループ リスナーではなく、プライマリ データベースに接続する接続文字列内で **MultiSubnetFailover=true** が使用されている場合、ドライバーではエラーが返されます。  

[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>参照  
[サーバーへの接続](../../connect/php/connecting-to-the-server.md)  
