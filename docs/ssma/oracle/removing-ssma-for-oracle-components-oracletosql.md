---
description: SSMA for Oracle コンポーネントの削除 (OracleToSQL)
title: SSMA for Oracle コンポーネントの削除 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 263d04b401146ce2975a810b084e4957f1daf718
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492408"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>SSMA for Oracle コンポーネントの削除 (OracleToSQL)
Oracle からへのデータベースの移行が完了したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA コンポーネントのアンインストールが必要になる場合があります。 クライアントコンポーネントはいつでもアンインストールできます。 ただし、移行した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで**sysdb**データベースの**ssma_oracle**スキーマの関数が使用されなくなっていない限り、から拡張パックをアンインストールしないでください。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>SSMA for Oracle クライアントのアンインストール  
SSMA をアンインストールするには、[ **プログラムの追加と削除**] を使用します。  
  
**SSMA をアンインストールするには**  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  [ ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle] の [Migration Assistant**] を選択し、[**削除**] をクリックします。  
  
3.  SSMA をアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックのアンインストール  
移行したデータベースで **ssma_oracle** スキーマのオブジェクトが使用されていないことが確実な場合は、[ **プログラムの追加と削除**] を使用して拡張機能パックを削除できます。  
  
**拡張機能パックをアンインストールするには**  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  [ **Oracle Extension Pack] の [Microsoft SQL Server Migration Assistant**] を選択し、[ **削除**] をクリックします。  
  
3.  拡張パックをアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
4.  [ユーティリティを使用したインスタンスデータベーススクリプト] ページで、インスタンスを選択し、[ **次へ**] をクリックします。  
  
5.  [接続パラメーター] ページで、認証方法を選択し、[ **次へ**] をクリックします。  
  
    Windows 認証では、Windows 資格情報を使用してのインスタンスにログオンしようとし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [認証] を選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン名とパスワードを入力する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
6.  [操作が完了しました] ページで、[ **OK]** をクリックします。  
  
7.  [完了] ページで、[ **終了**] をクリックします。  
  
アンインストール後、を使用して、 **ssma_oracle** スキーマのオブジェクトと、場合によっては **sysdb** データベース全体が削除されたことを確認でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。 ただし、他の SSMA 製品を使用する場合は、 **sysdb** データベースも使用します。 データベースが存在し、他のデータベースがこのデータベース内のオブジェクトを参照していない場合は、データベースをデタッチできます。  
  
## <a name="see-also"></a>関連項目  
[SSMA for Oracle Client &#40;OracleToSQL&#41;のインストール ](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server &#40;OracleToSQL&#41;での SSMA コンポーネントのインストール ](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
