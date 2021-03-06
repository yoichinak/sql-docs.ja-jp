---
description: SQL Server への接続 (SybaseToSQL)
title: SQL Server への接続 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 30179b25-409b-4e23-bc73-2f226657098f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b2b9c2d3f776ba41263e23d593ee3a4ef0f739df
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100064287"
---
# <a name="connect-to-sql-server-sybasetosql"></a>SQL Server への接続 (SybaseToSQL)
[ **SQL Server への接続** ] ダイアログボックスを使用すると、に移行するのインスタンスに接続 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] できます。 [ **SQL Server への接続** ] ダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **SQL Server に接続**] をクリックします。  
  
## <a name="options"></a>Options  
**サーバー名**  
接続する SQL Server のインスタンスを入力または選択します。 既定では、最近接続したインスタンスが表示されます。  
  
-   ローカルコンピューター上の既定のインスタンスに接続している場合は、 **localhost** またはドット (**.**) のいずれかを入力できます。  
  
-   別のコンピューター上の既定のインスタンスに接続している場合は、コンピューターの名前を入力します。  
  
-   別のコンピューター上の名前付きインスタンスに接続する場合は、コンピューター名、円記号、インスタンス名 ( *MyServer* \\ *myinstance* など) を入力します。  
  
**[サーバー ポート]**  
のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定のポート (1433) で接続を受け入れるように構成されていない場合は、ポート番号を入力します。 それ以外の場合は、この値を空白のままにします。  
  
**データベース**  
オブジェクトとデータを移行するデータベースを指定します。 このオプションは、に再接続するときには使用できません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
**認証**  
への接続に使用する認証方法を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 現在の Windows アカウントを使用するには、[Windows 認証] を選択します。 ログインとパスワードを指定するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[認証] を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**ユーザー名**  
認証を使用している場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、のインスタンスのログインを入力し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 Windows 認証を使用している場合、このオプションは使用できません。  
  
**パスワード**  
認証を使用している場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、のインスタンスにログインするためのパスワードを入力し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 Windows 認証を使用している場合、このオプションは使用できません。  
  
**[暗号化接続]**  
SQL Server に安全に接続する場合は、[ **暗号化接続** ] チェックボックスをオンにして、暗号化接続を使用します。  
  
**[Trust Server Certificate]**  
このオプションを使用する場合は、[ **サーバー証明書を信頼** する] チェックボックスをオンにします。  
  
> [!NOTE]  
> 信頼された **サーバー証明書** を有効にするには、"Encrypt" を **True** に設定する必要があります。  
  
