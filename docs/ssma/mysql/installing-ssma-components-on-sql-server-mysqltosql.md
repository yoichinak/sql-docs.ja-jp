---
title: SQL Server での SSMA コンポーネントのインストール (MySQLToSql) |Microsoft Docs
description: Ssma 拡張パックと MySQL プロバイダーを含む SSMA での MySQL データベースの変換をサポートするために、SQL Server を実行するサーバーにコンポーネントをインストールします。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 48c111ab342d7410031851a5635fa73fe143b96b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100070197"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>SQL Server での SSMA コンポーネントのインストール (MySQLToSql)

SSMA のインストールに加えて、を実行しているコンピューターにコンポーネントをインストールする必要もあり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのコンポーネントには、データの移行をサポートする SSMA 拡張パックと、サーバーとサーバー間の接続を有効にする MySQL プロバイダーが含まれます。

## <a name="ssma-for-mysql-extension-pack"></a>SSMA for MySQL extension pack

SSMA 拡張パックは、指定されたインスタンスにデータベース **sysdb** を追加し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このデータベースには、データの移行に必要なテーブルとストアドプロシージャが含まれています。

また、データをに移行するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、サーバー側のデータ移行エンジンを使用してデータを移行するときに、ssma によってエージェントジョブが作成され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

### <a name="prerequisites"></a>前提条件

SSMA for MySQL サーバーコンポーネントをにインストールする前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、コンピューターが次の要件を満たしていることを確認してください。

- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- MySQL クライアントプロバイダーと、移行する MySQL データベースへの接続。 プロバイダーは、MySQL 製品メディアまたは MySQL Web サイトからインストールできます。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストール中に Browser サービスが実行されている必要があります。 これは、セットアップウィザードでのインスタンスの一覧を設定するために使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 インストール後に Browser サービスを無効にすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  

  > [!NOTE]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser サービスが実行されていても、セットアップにインスタンスの一覧が表示されない場合は、UDP ポート1434のブロックを解除する必要があります。 Windows ファイアウォールを使用して、一時的にポートのブロックを解除することも、Windows ファイアウォールを一時的に無効にすることもできます。 また、ウイルス対策ソフトウェアを一時的に無効にすることが必要になる場合もあります。 インストール後に、ファイアウォールとウイルス対策ソフトウェアが有効になっていることを確認してください。

### <a name="installing-the-extension-pack"></a>拡張機能パックのインストール

にデータを移行する前に、いつでも拡張機能パックをインストールでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

> [!IMPORTANT]
> 拡張機能パックをインストールするには、のインスタンスの **sysadmin** サーバーロールのメンバーである必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

拡張機能パックをインストールするには:

1. SSMA for **SSMAforMySQLExtensionPack_ *n*.msi** をコピーします。ここで、 *n* はビルド番号であり、を実行しているコンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] なります。
2. **SSMAforMySQLExtensionPack_ *n*.msi** をダブルクリックします。
3. [ **ようこそ** ] ダイアログボックスで、[ **次へ**] をクリックします。
4. [使用許諾 **契約書** ] ダイアログボックスで、使用許諾契約書を確認します。 同意する場合は、[ **契約に同意** します] オプションを選択し、[ **次へ**] をクリックします。
5. [ **セットアップの種類の選択** ] ダイアログボックスで、[ **標準**] をクリックします。
6. [ **インストールの準備完了** ] ダイアログボックスで、[ **インストール**] をクリックします。
7. [ **インストールの最初の手順を完了しまし** た] ダイアログボックスで、[ **次へ**] をクリックします。

   新しいダイアログボックスが表示されます。このダイアログボックスで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張機能パックのインストール用のインスタンスを選択します。
  
8. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MySQL スキーマを移行するのインスタンスを選択し、[**次へ**] をクリックします。
  
   既定のインスタンスには、コンピューターと同じ名前が付けられています。 名前付きインスタンスの後には、円記号とインスタンス名が続きます。

9. [接続] ページで、認証方法を選択し、[ **次へ**] をクリックします。
  
    Windows 認証では、Windows 資格情報を使用してのインスタンスにログオンしようとし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [サーバー認証] を選択した場合は、ログイン名とパスワードを入力する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

10. 次の手順では、サーバー側のデータの移行中に拡張パックデータベースに格納されている機微なデータを暗号化するために使用されるマスターキーのパスワードを設定する必要があります。 強力なパスワードを入力し、[ **次へ**] をクリックします。

11. 次のダイアログボックスで、[ **Install Utilities Database *n***] を選択し、Extension Pack library をインストールします。ここで、 *n* はバージョン番号です。次に、[ **次へ**] をクリックします。

    **Sysdb** データベースは、(サーバー側のデータ移行エンジンを使用して) データの移行に必要なテーブルとストアドプロシージャがこのデータベースに作成された状態で作成されます。

12. の別のインスタンスにユーティリティをインストールするには、[はい] を選択し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [**次へ**] をクリックします。  または、ウィザードを終了するには、[ **いいえ**] をクリックします。

## <a name="see-also"></a>関連項目

- [SSMA for MySQL クライアントのインストール](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)
- [MySQL データベースの SQL Server Azure SQL Database への移行](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
