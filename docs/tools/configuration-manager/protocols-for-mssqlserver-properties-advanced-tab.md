---
title: MSSQLSERVER のプロトコルのプロパティ ([詳細設定] タブ)
description: SQL Server データベース エンジンに対する認証の拡張保護の利点と要件について説明します。 これを有効にして構成する方法を確認します。
ms.custom: seo-lt-2019
ms.date: 01/24/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f430d2be5a9b1af495b296f59c172e16401c01eb
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901120"
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER のプロトコルのプロパティ ([詳細設定] タブ)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

**[MSSQLSERVER のプロトコルのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] の**認証の拡張保護**を構成します。 **拡張保護** とは、オペレーティング システムで実装されているネットワーク コンポーネントの機能です。 **拡張保護** は、Windows 7 および Windows Server 2008 R2 で使用でき、それ以前のオペレーティング システムではサービス パックに含まれています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続を **拡張保護**を使用して確立することで、安全性を高めることができます。 **拡張保護** の利点には、 **[フラグ]** タブで **[強制的に暗号化]** を選択していないと得られないものもあります。

> [!IMPORTANT]  
> 既定では、Windows の **拡張保護** は有効になっていません。 **拡張保護**を有効にする方法の詳細については、次を参照してください。
> - [Windows 拡張保護 \<extendedProtection\>](/iis/configuration/system.webserver/security/authentication/windowsauthentication/extendedprotection/)
> - [認証の拡張保護の概要](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のサービスの構成方法と **拡張保護**の詳細については、 [Microsoft.com](https://go.microsoft.com/fwlink/?LinkId=177752)の最新情報を参照してください。

**拡張保護** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降の [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]Native Client によって完全にサポートされています。 その他の **クライアント プロバイダーでは、** 拡張保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は現時点ではサポートされていません。

## <a name="options"></a>Options

### <a name="extended-protection"></a>で始まる

指定可能な 3 つの値は次のとおりです。  

- **Off**:**拡張保護**が無効になっていることを意味します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、クライアントが保護されているかどうかに関係なく、任意のクライアントからの接続を許可します。 **[オフ]** は、古いオペレーティング システムや修正プログラムの適用が解除されたオペレーティング システムと互換性がありますが、安全性は低くなります。 この設定は、クライアント オペレーティング システムで拡張保護がサポートされていないことがわかっている場合にのみ使用してください。

- **[許可]** : **[拡張保護]** をサポートするオペレーティング システムからの接続に **[拡張保護]** が必要になります。 保護されたクライアント オペレーティング システムで実行されている保護されていないクライアント アプリケーションからの接続は拒否されます。 保護されていないオペレーティング システムからの接続では、**拡張保護** が無視されます。 この設定は、 **[オフ]** よりも安全性が高いですが、最も安全な設定ではありません。 この設定は、 **拡張保護** をサポートするオペレーティング システムやアプリケーションとサポートしないオペレーティング システムやアプリケーションが混在する環境で使用します。

- **必須**:接続の許可を受けるには、保護されているオペレーティング システム上の保護されているアプリケーションから接続されている必要があることを意味します。 この設定は、3 つのオプションの中で最も安全です。 **拡張保護**をサポートしないオペレーティング システムからの接続では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することができません。

### <a name="accepted-ntlm-spns"></a>[承認された NTLM SPN]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、複数の NTLM サービス プリンシパル名 (SPN) によって識別できます。 SPN はセミコロンで区切った文字列として一覧表示します。 たとえば、値 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** は、**MSSQLSvc/HOST1.Contoso.com** または **MSSQLSvc/HOST2.Contoso.com** という名前の SPN への接続を試みているクライアントが許可されることを示します。 変数の最大長は 2048 文字です。

## <a name="see-also"></a>参照

[Reporting Services での認証の拡張保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)