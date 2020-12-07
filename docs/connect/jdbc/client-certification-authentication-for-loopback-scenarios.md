---
description: ループバック シナリオにおけるクライアント証明書の認証
title: ループバック シナリオにおけるクライアント証明書の認証 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: peterbae
ms.author: v-hyba
ms.openlocfilehash: bfc8816c30020669918b3632f94e289524097537
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438444"
---
# <a name="client-certificate-authentication-for-loopback-scenarios"></a>Loopback シナリオにおけるクライアント証明書の認証

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

sp_execute_external_script (SPEES) という新しいストアド プロシージャが、SQL Server 2016 に追加されました。 このストアド プロシージャを使用すると、拡張作業の一部として、SQL Server から SQL Server 外の外部スクリプトを起動して実行することができます。 これにより、R および Python スクリプトがサポートされるようになりました。どちらの場合も、JDBC ドライバーを使用して SQL Server に接続できるライブラリが用意されています。 SQL Servers on Windows ボックスによって、Windows 統合認証を使用して、クエリを開始したユーザーと同じ資格情報でこれらのループバック接続を認証できますが、Linux SQL Server から同じことを行うことはできません。 そのため、ユーザーが証明書とキーを使用して認証できるように、クライアント証明書の認証が追加されています。

## <a name="connecting-using-client-certificate-authentication"></a>クライアント証明書の認証を使用して接続する

JDBC ドライバーによって、この機能の 3 つの接続プロパティが追加されます。

* clientCertificate – 認証に使用する証明書を指定します。 JDBC ドライバーでは、PFX、PEM、DER、CER ファイル拡張子がサポートされます。

形式
```
clientCertificate=<file_location>
``` 
ドライバーによって、証明書ファイルが使用されます。 PEM、DER、CER 形式の証明書の場合、clientKey 属性が必要です。 ファイルの場所には、相対または絶対のいずれかを指定できます。
 
* clientKey – clientCertificate 属性に指定された PEM、DER、CER 証明書の秘密キーのファイルの場所を指定します。

形式
```
clientKey=<file_location>
```
秘密キー ファイルの場所を指定します。 秘密キー ファイルがパスワードで保護されている場合は、password キーワードが必要です。 ファイルの場所には、相対または絶対のいずれかを指定できます。

* clientKeyPassword – clientKey ファイルの秘密キーにアクセスするために提供される、省略可能なパスワード文字列。

この機能は、Linux SQL Server 2019 以上のループバック認証のシナリオでのみ公式にサポートされています。

## <a name="see-also"></a>関連項目

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
