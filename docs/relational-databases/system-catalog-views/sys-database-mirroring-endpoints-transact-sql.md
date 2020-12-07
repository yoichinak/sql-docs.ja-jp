---
description: sys.database_mirroring_endpoints (Transact-SQL)
title: database_mirroring_endpoints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6b45e1caf164cd367af4811d8e7cbc1f33a70921
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550498"
---
# <a name="sysdatabase_mirroring_endpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンスのデータベースミラーリングエンドポイント用の1行のデータを格納 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
> [!NOTE]  
>  データベースミラーリングエンドポイントでは、データベースミラーリングパートナーと監視サーバーの間のセッション、および Always On 可用性グループとそのセカンダリレプリカのプライマリレプリカ間のセッションの両方がサポートされます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|-|から列を継承し **ます。** 詳細については、「 [sys. エンドポイント &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md))」を参照してください。|  
|**role**|**tinyint**|ミラーリング ロール。次のいずれかになります。<br /><br /> **0** = なし<br /><br /> **1** = パートナー<br /><br /> **2** = ミラーリング監視<br /><br /> **3** = すべて<br /><br /> 注: この値はデータベースミラーリングにのみ関連します。|  
|**role_desc**|**nvarchar(60)**|ミラーリング ロールの説明。次のいずれかになります。<br /><br /> **NONE**<br /><br /> **企業**<br /><br /> **監視**<br /><br /> **ALL**<br /><br /> 注: この値はデータベースミラーリングにのみ関連します。|  
|**is_encryption_enabled**|**bit**|**1** は、暗号化が有効になっていることを示します。<br /><br /> **0** は、暗号化が無効であることを示します。|  
|**connection_auth**|**tinyint**|エンドポイントへの接続に必要な接続認証の種類。次のいずれかになります。<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -ネゴシエート<br /><br /> **4** -証明書<br /><br /> **5** -NTLM、証明書<br /><br /> **6** -KERBEROS、証明書<br /><br /> **7** -NEGOTIATE、CERTIFICATE<br /><br /> **8** -証明書、NTLM<br /><br /> **9** -証明書、KERBEROS<br /><br /> **10** -証明書、ネゴシエート|  
|**connection_auth_desc**|**Nvarchar (60)**|このエンドポイントへの接続に必要な認証の種類の説明。次のいずれかになります。<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> ネゴシエーション<br /><br /> CERTIFICATE<br /><br /> NTLM、証明書<br /><br /> KERBEROS、証明書<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> 証明書、ネゴシエート|  
|**certificate_id**|**int**|認証で使用される証明書の ID (存在する場合)。<br /><br /> 0 = Windows 認証が使用されています。|  
|**encryption_algorithm**|**tinyint**|暗号化アルゴリズム。次のいずれかになります。<br /><br /> **0** -なし<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -なし、RC4<br /><br /> **4** -NONE、AES<br /><br /> **5** -RC4、AES<br /><br /> **6** -AES、RC4<br /><br /> **7** -なし、RC4、AES<br /><br /> **8** -なし、AES、RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|暗号化アルゴリズムの説明。次のいずれかになります。<br /><br /> NONE<br /><br /> RC4<br /><br /> AES<br /><br /> なし、RC4<br /><br /> NONE、AES<br /><br /> RC4、AES<br /><br /> AES、RC4<br /><br /> NONE、RC4、AES<br /><br /> NONE、AES、RC4|  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降では、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材の暗号化を解除できます。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [可用性レプリカを追加または変更するときにエンドポイント URL を指定する &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [database_mirroring &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [database_mirroring_witnesses &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
