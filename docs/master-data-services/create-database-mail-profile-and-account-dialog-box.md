---
description: '[データベース メール プロファイルとアカウントの作成] ダイアログ ボックス'
title: '[データベース メール プロファイルとアカウントの作成] ダイアログ ボックス'
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d6c9b1c9b455b7e192c5c4c4ec921b8b9cdebcba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461806"
---
# <a name="create-database-mail-profile-and-account-dialog-box"></a>[データベース メール プロファイルとアカウントの作成] ダイアログ ボックス

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  **[データベース メール プロファイルとアカウントの作成]** ダイアログ ボックスを使用すると、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのデータベース メール プロファイルおよびデータベース メール アカウントを作成できます。 このプロファイルは、ビジネス ルールの検証が失敗したときに電子メールでユーザーやグループに通知する際に使用されます。  
  
## <a name="database-mail-profile-and-account"></a>データベース メール プロファイルとアカウント  
 *データベースメールプロファイル*は、データベースメールアカウントのコレクションです。 *データベースメールアカウント*には、が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SMTP サーバーに電子メールメッセージを送信するために使用する情報が含まれています。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]でプロファイルとアカウントを作成すると、アカウントは自動的にプロファイルに追加され、そのアカウント情報が電子メールの送信に使用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を使用して既存のデータベース メール プロファイルまたはアカウントを更新したり、1 つのプロファイルに対して複数のアカウントを構成したりすることはできません。 データベース メールを使用したより高度なタスクを実行するには、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] または Transact-SQL スクリプトを使用できます。 詳細については、SQL Server オンライン ブックの「 [データベース メール構成オブジェクト](../relational-databases/database-mail/database-mail-configuration-objects.md) 」を参照してください。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|[**プロファイル名**]|新しいデータベース メール プロファイルの名前を入力します。 この名前は、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース用に構成されたデータベース メール プロファイルの中で一意である必要があります。<br /><br /> このプロファイルは、作成すると、 **の** [データベース] [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]ページに表示され選択されます。|  
|**アカウント名**|このプロファイルに関連付ける新しいデータベース メール アカウントの名前を入力します。 この名前は、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース用に構成されたデータベース メール アカウントの中で一意である必要があります。 このアカウントは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アカウントおよび Windows ユーザー アカウントとは関係ありません。|  
  
## <a name="outgoing-smtp-mail-server"></a>送信 (SMTP) メール サーバー  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**電子メール アドレス**|アカウントの電子メール アドレスの名前を入力します。 これは、電子メールの送信元の電子メールアドレスであり、 *email_name*domain_name の形式である必要があり @ *domain_name*ます。 例の電子メール アドレスは sales@contoso.com です。|  
|**表示名**|この設定は省略可能です。 このアカウントから送信する電子メール メッセージに表示する名前を入力します。 たとえば、表示名は Contoso Sales Group のようになります。|  
|**[返信用電子メール アドレス]**|この設定は省略可能です。 このアカウントから送信した電子メール メッセージに対する返信に使用する電子メール アドレスを入力します。 例の返信用電子メール アドレスは admin@contoso.com です。|  
|**[SMTP サーバー]**|アカウントが電子メールの送信に使用する SMTP サーバーの名前または IP アドレスを入力します。 たとえば、SMTP サーバーの形式は **smtp.***<company_name>***.com** のようになります。 詳細については、電子メールの管理者に問い合わせてください。|  
|**ポート番号**|このアカウントで使用する SMTP サーバーのポート番号を入力します。 既定の SMTP ポートは 25 です。|  
|**[このサーバーはセキュリティで保護された接続 (SSL) を必要とする]**|トランスポート層セキュリティ (TLS) を使用して通信を暗号化します。これは、以前は Secure Sockets Layer (SSL) と呼ばれていました。|  
  
## <a name="smtp-authentication"></a>SMTP 認証  
 データベース メールは、 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]の資格情報、または指定したその他の資格情報を使用して送信できます。または、匿名で送信することもできます。 電子メール サーバーで認証が要求される場合は、データベース メールに使用する特定のユーザー アカウントを作成することをお勧めします。 このユーザー アカウントには最小限の権限を設定し、他の目的に使用されないようにします。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**[データベース エンジン サービスの資格情報を使用する Windows 認証]**|データベースメールが、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] SMTP サーバーでの認証に Windows サービスアカウントの資格情報を使用することを指定します。|  
|**基本認証**|データベース メールでは、SMTP サーバーの認証に特定のユーザー名とパスワードを使用することを指定します。 この情報は、電子メール サーバーとの認証だけに使用されるため、アカウントは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーザー、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を実行しているコンピューターのユーザーに対応している必要はありません。|  
|**ユーザー名**|データベース メールで SMTP サーバーへのログオンに使用されるユーザー アカウントの名前を入力します。 SMTP サーバーで基本認証が求められる場合、ユーザー名が必要になります。|  
|**パスワード**|データベース メールで SMTP サーバーへのログオンに使用されるパスワードを入力します。 SMTP サーバーで基本認証が求められる場合、パスワードが必要になります。|  
|**[パスワードの確認入力]**|パスワードに間違いがないことを確認するために、設定したパスワードをもう一度入力します。|  
|**匿名認証**|SMTP サーバーで認証を要求しないことを指定します。 SMTP サーバーの認証には資格情報をまったく使用しません。|  
  
## <a name="see-also"></a>参照  
 [[データベースの構成] ページ &#40;マスターデータサービス構成マネージャー&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[マスター データ サービスのイントールと構成](../master-data-services/master-data-services-installation-and-configuration.md)
  
  
