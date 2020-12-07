---
description: CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
title: CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 91478060af31e142f94730b9df3c0a3cdf2a24ef
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124101"
---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で、拡張キー管理 (EKM: Extensible Key Management) プロバイダーから暗号化サービス プロバイダーを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *provider_name*  
 拡張キー管理プロバイダーの名前を指定します。  
  
 *path_of_DLL*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張キー管理インターフェイスを実装する .dll ファイルのパスを指定します。 **SQL Server コネクタ for Microsoft Azure Key Vault** を使うときの既定の場所は、**'C:\Program Files\Microsoft SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll'** です。  
  
## <a name="remarks"></a>解説  
 プロバイダーによって作成されるキーはいずれも、プロバイダーをその GUID で参照します。 GUID は、DLL のすべてのバージョン間で保持されます。  
  
 SQLEKM インターフェイスを実装する DLL は、任意の証明書を使用して、デジタル署名する必要があります。 この署名は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって検証されます。 これにはその証明書チェーンも含まれます。証明書チェーンのルートは、Windows システムの **信頼されたルート証明機関** がある場所にインストールされている必要があります。 署名が正しく検証されなかった場合は、CREATE CRYPTOGRAPHIC PROVIDER ステートメントが失敗します。 証明書と証明書チェーンについて詳しくは、「[SQL Server の証明書と非対称キー](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
 EKM プロバイダーの dll で必要なメソッドの一部が実装されなかった場合は、CREATE CRYPTOGRAPHIC PROVIDER から次のエラー 33085 が返されることがあります。  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 EKM プロバイダーの dll の作成に使用されたヘッダー ファイルが古い場合は、CREATE CRYPTOGRAPHIC PROVIDER から次のエラー 33032 が返されることがあります。  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で .dll ファイルから `SecurityProvider` という暗号化サービス プロバイダーを作成します。 この .dll ファイルは `c:\SecurityProvider\SecurityProvider_v1.dll` という名前でサーバーにインストールされています。 最初にプロバイダーの証明書をサーバーにインストールする必要があります。  
  
```sql  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>参照  
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Azure Key Vault を使用した SQL Server TDE 拡張キー管理を設定する](../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)  
 [sys.cryptographic_providers](../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)  
 [sys.dm_cryptographic_provider_properties](../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)
  
  
