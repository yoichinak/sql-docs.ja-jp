---
title: データベース エンジン:重大な変更 | Microsoft Docs
titleSuffix: SQL Server 2017
description: 以前のバージョンの SQL Server が基になっているアプリケーション、スクリプト、または機能を使用できなくなる可能性がある変更について説明します。
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 18a129e630028d0384f10a373a2302ff57bd78cb
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670161"
---
# <a name="breaking-changes-to-database-engine-features-in-sssqlv14-md"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] におけるデータベース エンジン機能の重大な変更
[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]


  このトピックでは、[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] における重大な変更について説明します。 これらの変更によって、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に基づくアプリケーション、スクリプト、または機能が使用できなくなる場合があります。 この問題は、アップグレードするときに発生することがあります。  
  
## <a name="breaking-changes-in-sssqlv14-md-ssde"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] における重大な変更  
  
-  CLR では、セキュリティ境界としてサポートされなくなった、.NET Framework のコード アクセス セキュリティ (CAS) が使用されます。 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 以降、CLR アセンブリのセキュリティを強化するために `clr strict security` という `sp_configure` オプションが導入されました。 clr strict security は既定で有効になり、`SAFE` および `EXTERNAL_ACCESS` CRL アセンブリを `UNSAFE` とマークされている場合と同じように扱います。 `clr strict security` オプションは、旧バージョンとの互換性のために無効にできますが、これは推奨されません。 `clr strict security` を無効にすると、`PERMISSION_SET = SAFE` で作成された CLR アセンブリが、外部のシステム リソースにアクセスし、アンマネージ コードを呼び出し、**sysadmin** 特権を取得できる場合があります。 厳密なセキュリティを有効にした場合、未署名のアセンブリの読み込みは失敗します。 また、データベースに `SAFE` または `EXTERNAL_ACCESS` アセンブリがある場合、`RESTORE` または `ATTACH DATABASE` ステートメントは完了できますが、アセンブリの読み込みは失敗する可能性があります。   
  アセンブリを読み込むには、各アセンブリを変更または削除して再作成して、サーバーでの `UNSAFE ASSEMBLY` アクセス許可のある対応するログインを含む証明書または非対称キーで署名されるようにする必要があります。 詳しくは、「[CLR の厳密なセキュリティ](../database-engine/configure-windows/clr-strict-security.md)」をご覧ください。 
  
-  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] では、MD2、MD4、MD5、SHA、SHA1 のアルゴリズムは非推奨です。 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] までは、SHA1 を使用して自己署名証明書が作成されます。 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 以降では、SHA2_256 を使用して自己署名証明書が作成されます。

## <a name="previous-versions"></a><a name="previous-versions"></a> 以前のバージョン  

- [SQL Server 2016 におけるデータベース エンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)

- [SQL Server 2014 におけるデータベース エンジン機能の重大な変更](/previous-versions/sql/2014/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14)

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>SQL Server の非常に古いバージョンのアーカイブされたドキュメント

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>参照  
 [SQL Server 2016 データベース エンジンの非推奨の機能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 で廃止されたデータベース エンジンの機能](./discontinued-database-engine-functionality-in-sql-server.md)   
 [SQL Server データベース エンジンの旧バージョンとの互換性](./discontinued-database-engine-functionality-in-sql-server.md)   
 [ALTER DATABASE 互換性レベル &#40;TRANSACT-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
