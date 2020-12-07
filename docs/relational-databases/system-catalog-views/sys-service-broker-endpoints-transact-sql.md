---
description: service_broker_endpoints (Transact-sql)
title: service_broker_endpoints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ee3bd0e5e09ab2e8511596f3920e0e8408f1b6f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539567"
---
# <a name="sysservice_broker_endpoints-transact-sql"></a>service_broker_endpoints (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このカタログビューには、Service Broker エンドポイントの1つの行が含まれています。 このビューのすべての行には、TCP 構成メタデータを含む、 **tcp_endpoints**ビューに同じ**endpoint_id**を持つ対応する行があります。 Service Broker で使用できるプロトコルは TCP のみです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|**--**|[では、transact-sql&#41;&#40;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)から列を継承しています。|  
|**is_message_forwarding_enabled**|**bit**|エンドポイントがメッセージの転送をサポートします。 これは、最初は **0** (無効) に設定されます。 NULL 値は許容されません。|  
|**message_forwarding_size**|**int**|転送されるメッセージに使用できる **tempdb** 領域の最大値 (mb)。 初期設定は **10**に設定されています。 NULL 値は許容されません。|  
|**connection_auth**|**tinyint**|エンドポイントへの接続に必要な接続認証の種類。次のいずれかになります。<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -ネゴシエート<br /><br /> **4** -証明書<br /><br /> **5** -NTLM、証明書<br /><br /> **6** -KERBEROS、証明書<br /><br /> **7** -NEGOTIATE、CERTIFICATE<br /><br /> **8** -証明書、NTLM<br /><br /> **9** -証明書、KERBEROS<br /><br /> **10** -証明書、ネゴシエート<br /><br /> NULL 値は許容されません。|  
|**connection_auth_desc**|**nvarchar(60)**|このエンドポイントへの接続に必要な接続認証の種類の説明。次のいずれかになります。<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> ネゴシエーション<br /><br /> CERTIFICATE<br /><br /> NTLM、証明書<br /><br /> KERBEROS、証明書<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> 証明書、ネゴシエート<br /><br /> NULLABLE.|  
|**certificate_id**|**int**|認証で使用される証明書の ID (存在する場合)。<br /><br /> 0 = Windows 認証が使用されています。|  
|**encryption_algorithm**|**tinyint**|暗号化アルゴリズム。 使用可能な値とその説明および対応する DDL オプションを次に示します。<br /><br /> **0** : なし。 対応する DDL オプション: Disabled。<br /><br /> **1** : RC4。 対応する DDL オプション: {必須 &#124; アルゴリズム RC4}。<br /><br /> **2** : AES。 対応する DDL オプション: アルゴリズム AES が必要です。<br /><br /> **3** : なし、RC4。 対応する DDL オプション: {supported &#124; サポートされているアルゴリズム RC4}。<br /><br /> **4** : NONE、AES。 対応する DDL オプション: アルゴリズム AES がサポートされています。<br /><br /> **5** : RC4、AES。 対応する DDL オプション: アルゴリズム RC4 AES が必要です。<br /><br /> **6** : AES、RC4。 対応する DDL オプション: アルゴリズム AES RC4 が必要です。<br /><br /> **7** : NONE、RC4、AES。 対応する DDL オプション: アルゴリズム RC4 AES がサポートされています。<br /><br /> **8** : NONE、AES、RC4。 対応する DDL オプション: アルゴリズム AES RC4 がサポートされています。<br /><br /> NULL 値は許容されません。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|暗号化アルゴリズムの説明。 有効な値とそれに対応する DDL オプションを以下に示します。<br /><br /> なし: 無効<br /><br /> RC4: {必須 &#124; アルゴリズム RC4}<br /><br /> AES: アルゴリズム AES が必要です。<br /><br /> なし、RC4: {サポートされている &#124; アルゴリズム RC4}<br /><br /> NONE、AES: サポートされているアルゴリズム AES<br /><br /> RC4、AES: アルゴリズム RC4 AES が必要です。<br /><br /> AES、RC4: アルゴリズム AES RC4 が必要<br /><br /> NONE、RC4、AES: サポートされているアルゴリズム RC4 AES<br /><br /> NONE、AES、RC4: サポートされているアルゴリズム AES RC4<br /><br /> NULLABLE.|  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
