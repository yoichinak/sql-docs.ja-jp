---
title: 拡張キー管理 (EKM) | Microsoft Docs
description: 拡張キー管理を構成して使用する方法と、それが SQL Server のデータ暗号化機能にどのように適合するかについて説明します。
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 0524aa4738ae7003d763422c20db17e39e89e964
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867848"
---
# <a name="extensible-key-management-ekm"></a>拡張キー管理 (EKM)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、 *拡張キー管理* (EKM) を含むデータ暗号化機能が用意されています。暗号化とキーの生成には *Microsoft Cryptographic API* (MSCAPI) が使用されます。 データとキーの暗号化のための暗号化キーは一時的なキー コンテナーに作成され、それらをデータベースに格納するには、まずプロバイダーからエクスポートする必要があります。 この方法により、暗号化キー階層とキーのバックアップを含むキー管理を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で処理できるようになります。  
  
 法規制遵守の必要性やデータ プライバシーに対する関心の高まりを受けて、組織では、"多層防御" のソリューションを実現するための手段として暗号化が活用されるようになっています。 このアプローチは多くの場合、データベースの暗号化管理ツールを使用するだけで実現できるものではありません。 各ハードウェア ベンダーからは、 *ハードウェア セキュリティ モジュール* (HSM) を使用して企業のキー管理の問題に対処する製品が提供されています。 HSM デバイスでは、暗号化キーがハードウェア モジュールまたはソフトウェア モジュールに格納されます。 この場合、暗号化キーが暗号化データと一緒に保管されないため、より安全なソリューションが実現されます。  
  
 多くのベンダーにより、キー管理と暗号化アクセラレーションの両方に対応する HSM が提供されています。 HSM デバイスでは、アプリケーションと HSM の仲介として、サーバー プロセスとのハードウェア インターフェイスが使用されます。 また、モジュール上に MSCAPI プロバイダー (ハードウェアの場合もあればソフトウェアの場合もあります) が実装されています。 MSCAPI では、多くの場合、HSM でサポートされている機能の一部しかサポートされません。 その他、HSM、キーの構成、およびキーへのアクセスのための管理ソフトウェアが用意されている場合もあります。  
  
 HSM の実装はベンダーによってさまざまです。したがって、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でそれらを使用するには、共通のインターフェイスが必要です。 このインターフェイスを提供するのが MSCAPI ですが、HSM の機能の一部しかサポートされません。 MSCAPI には、これ以外にも、対称キーをネイティブのまま永続化できない、セッション指向の通信がサポートされていないなどの制限があります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の拡張キー管理では、サードパーティの EKM/HSM ベンダーがそれぞれのモジュールを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に登録できます。 登録すると、その EKM モジュールに格納されている暗号化キーを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ユーザーが使用できるようになります。 これにより、それらのモジュールでサポートされている一括暗号化/暗号化解除などの高度な暗号化機能や、キー エージングやキー ローテーションなどのキー管理機能を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から利用できます。  
  
 Azure 仮想マシンで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行している場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、 [Azure Key Vault](/azure/key-vault/general/basic-concepts)に格納されたキーを使用できます。 詳細については、「 [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)で処理できるようになります。  
  
## <a name="ekm-configuration"></a>EKM の構成  
 拡張キー管理は [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のすべてのエディションでサポートされているわけではありません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 既定では、拡張キー管理は無効です。 この機能を有効にするには、次のオプションと値を使用して sp_configure コマンドを実行します。  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  EKM をサポートしていないエディションの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でこのオプションを使用して sp_configure コマンドを実行すると、エラーが表示されます。  
  
 この機能を無効にするには、値を **0** に設定します。 サーバー オプションの設定方法については、「[sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」を参照してください。  
  
## <a name="how-to-use-ekm"></a>EKM を使用する方法  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 拡張キー管理を使用すると、データベース ファイルを保護する暗号化キーを外部デバイス (スマート カード、USB デバイス、EKM/HSM モジュールなど) に格納できます。 これにより、データベース管理者 (sysadmin グループのメンバーを除く) からのデータの保護も実現され、 そのデータベース ユーザー以外はアクセスできない外部 EKM/HSM モジュール上の暗号化キーを使用してデータを暗号化できます。  
  
 拡張キー管理にはその他、次のような利点があります。  
  
-   追加の承認チェック (職務の分離の実現)。  
  
-   ハードウェア ベースの暗号化/暗号化解除のパフォーマンスの向上。  
  
-   外部での暗号化キーの生成。  
  
-   外部での暗号化キーの格納 (データとキーの物理的な分離)。  
  
-   暗号化キーの取得。  
  
-   外部での暗号化キーの保持 (暗号化キーのローテーションの実現)。  
  
-   暗号化キーのより簡単な復元。  
  
-   暗号化キーの管理可能な配布。  
  
-   暗号化キーの安全な破棄。  
  
 拡張キー管理は、ユーザー名とパスワードの組み合わせに対して使用することも、EKM ドライバーで定義されたその他の方法に対して使用することもできます。  
  
> [!CAUTION]  
>  トラブルシューティングの際には、EKM プロバイダーから取得した暗号化キーを [!INCLUDE[msCoName](../../../includes/msconame-md.md)] テクニカル サポートに提供する必要性や、 問題を解決するためにベンダーのツールやプロセスにアクセスする必要性が生じる場合もあります。  
  
### <a name="authentication-with-an-ekm-device"></a>EKM デバイスによる認証  
 EKM モジュールでは複数の種類の認証をサポートできますが、 各プロバイダーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に公開する認証の種類は 1 つだけです。したがって、モジュールで基本認証とその他の認証方法がサポートされている場合、公開されるのはいずれか一方だけで、両方は公開されません。  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>ユーザー名/パスワードを使用する EKM デバイス固有の基本認証  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、*ユーザー名/パスワード*のペアを使用する基本認証をサポートしている EKM モジュールで、資格情報による透過的な認証を利用できます。 資格情報の詳細については、「[資格情報 &#40;データベース エンジン&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md)」を参照してください。  
  
 EKM プロバイダーに対して資格情報を作成し、それをログイン (Windows アカウントと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントの両方) にマップすることにより、ログインごとに EKM モジュールにアクセスできます。 資格情報の *[ID]* フィールドにはユーザー名が含まれ、 *[シークレット]* フィールドには EKM モジュールに接続するためのパスワードが含まれます。  
  
 ログインにマップされた EKM プロバイダーの資格情報がない場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントにマップされた資格情報が使用されます。  
  
 それぞれが異なる EKM プロバイダーに対して使用される資格情報であれば、1 つのログインに複数の資格情報をマップできます。 マップされた資格情報は、各ログインで各 EKM プロバイダーにつき 1 つだけ存在する必要があります。 同じ資格情報を他のログインにマップすることはできます。  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>その他の種類の EKM デバイス固有の認証  
 Windows 認証や *ユーザー/パスワード* の組み合わせの認証以外を使用する EKM モジュールに対しては、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]とは別に認証を行う必要があります。  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>EKM デバイスによる暗号化および暗号化解除  
 対称キーと非対称キーを使用してデータを暗号化および暗号化解除するには、以下の関数と機能を使用できます。  
  
|関数または機能|リファレンス|  
|-------------------------|---------------|  
|対称キー暗号化|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|非対称キー暗号化|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, 'cleartext', ...)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(ciphertext, ...)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey(key_guid, 'cleartext')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>EKM キーによるデータベース キーの暗号化  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、EKM キーを使用してデータベースのその他のキーを暗号化できます。 EKM デバイスで対称キーと非対称キーの両方を作成および使用できます。 EKM 非対称キーを使用してネイティブ (EKM 以外) の対称キーを暗号化することができます。  
  
 次の例では、データベースの対称キーを作成し、それを EKM モジュールのキーを使用して暗号化しています。  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータベースとサーバー キーの詳細については、「[SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)」を参照してください。  
  
> [!NOTE]  
>  別の EKM キーを使用して EKM キーを暗号化することはできません。  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、EKM プロバイダーから生成された非対称キーを使用してモジュールに署名することをサポートしていません。  
  
## <a name="related-tasks"></a>Related Tasks  
 [EKM provider enabled サーバー構成オプション](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [EKM の使用による TDE の有効化](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Reporting Services の暗号化キーのバックアップと復元](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [暗号化キーの削除と再作成  &#40;SSRS 構成マネージャー&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [スケールアウト配置に関する暗号化キーの追加と削除 &#40;SSRS 構成マネージャー&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [サービス マスター キーのバックアップ](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [サービス マスター キーの復元](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [データベース マスター キーの作成](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [データベース マスター キーのバックアップ](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [データベース マスター キーの復元](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [2 台のサーバーでの同じ対称キーの作成](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
