---
description: SSMA for MySQL コンポーネントの削除 (MySQLToSql)
title: SSMA for MySQL コンポーネントの削除 (MySQLToSql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 898b55146317a09b43b1b4df63a22a9a74882ee9
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100074633"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>SSMA for MySQL コンポーネントの削除 (MySQLToSql)
MySQL からへのデータベースの移行が完了したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA コンポーネントをアンインストールすることをお勧めします。 クライアントコンポーネントはいつでもアンインストールできます。 ただし、から拡張パックをアンインストールした場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA は Server-Side データ移行エンジンを使用して、MySQL からターゲットデータベースへのデータの移行 (SQL Server/SQL Azure) をサポートしなくなります。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>SSMA for MySQL クライアントのアンインストール  
SSMA をアンインストールするには、[ **プログラムの追加と削除**] を使用します。  
  
**SSMA をアンインストールするには**  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  [ **MySQL] の [Microsoft SQL Server Migration Assistant**] を選択し、[ **削除**] をクリックします。  
  
3.  SSMA をアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックのアンインストール  
拡張機能パックを削除するには、[ **プログラムの追加と削除**] を使用します。  
  
**拡張機能パックをアンインストールするには**  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  [ **MySQL Extension Pack] の [Microsoft SQL Server Migration Assistant**] を選択し、[ **削除**] をクリックします。  
  
3.  拡張パックをアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
4.  [ユーティリティを使用したインスタンスデータベーススクリプト] ページで、インスタンスを選択し、[ **次へ**] をクリックします。  
  
5.  [接続パラメーター] ページで、認証方法を選択し、[ **次へ**] をクリックします。  
  
    Windows 認証では、Windows 資格情報を使用してのインスタンスにログオンしようとし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [認証] を選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン名とパスワードを入力する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
6.  [操作が完了しました] ページで、[ **OK]** をクリックします。  
  
7.  [完了] ページで、[ **終了**] をクリックします。  
  
アンインストールプロセスが完了したら、を使用して、 **sysdb.ssma_MySQL** スキーマ内のオブジェクト、および場合によっては **sysdb** データベース全体が削除されたことを確認でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。 ただし、他の SSMA 製品を使用する場合は、 **sysdb** データベースも使用します。 データベースが存在し、このデータベース内のオブジェクトへの他のデータベースが参照されていない場合は、データベースをデタッチできます。  
  
## <a name="see-also"></a>参照  
[SSMA for MySQL クライアント &#40;MySQLToSQL&#41;のインストール ](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server での SSMA コンポーネントのインストール](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
