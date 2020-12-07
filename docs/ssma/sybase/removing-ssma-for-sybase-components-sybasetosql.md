---
description: SSMA for Sybase コンポーネントの削除 (SybaseToSQL)
title: SSMA for Sybase コンポーネントの削除 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4c4e0f94f5672c96972a3cf3f3d35255dce91208
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468831"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>SSMA for Sybase コンポーネントの削除 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) からへのデータベースの移行が完了したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA コンポーネントのアンインストールが必要になる場合があります。 クライアントコンポーネントはいつでもアンインストールできますが、移行した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースが**sysdb**データベースの**ssma_syb**スキーマの関数を使用しなくなったことが確実でない限り、から拡張機能パックをアンインストールしないでください。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>SSMA for Sybase クライアントのアンインストール  
SSMA をアンインストールするには、[ **プログラムの追加と削除**] を使用します。  
  
**SSMA をアンインストールするには**  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  **Sybase の Microsoft SQL Server Migration Assistant**を選択し、[**削除**] をクリックします。  
  
3.  SSMA をアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックのアンインストール  
移行したデータベースで **ssma_syb** スキーマのオブジェクトが使用されていないことが確実な場合は、[ **プログラムの追加と削除**] を使用して拡張機能パックを削除できます。  
  
拡張機能パックをアンインストールするには  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  **Sybase 拡張パックの Microsoft SQL Server Migration Assistant**を選択し、[**削除**] をクリックします。  
  
3.  拡張パックをアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
4.  [ユーティリティを使用したインスタンスデータベーススクリプト] ページで、[ **次へ**] をクリックします。  
  
5.  [接続パラメーター] ページで、認証方法を選択し、[ **次へ**] をクリックします。  
  
    Windows 認証では、Windows 資格情報を使用して SQL Server のインスタンスにログオンしようとします。 SQL Server 認証を選択した場合は、SQL Server のログイン名とパスワードを入力する必要があります。  
  
6.  [操作が完了しました] ページで、[ **OK]** をクリックします。  
  
7.  [完了] ページで、[ **終了**] をクリックします。  
  
をアンインストールした後、を使用して、 **sysdb. ssma_syb**スキーマ、および場合によっては**sysdb**データベース全体が削除されたことを確認できます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ただし、他の SSMA 製品を使用する場合は、 **sysdb** データベースも使用します。 データベースが存在し、他のデータベースがこのデータベース内のオブジェクトを参照していない場合は、データベースをデタッチできます。  
  
## <a name="see-also"></a>関連項目  
[SSMA for Sybase Client &#40;SybaseToSQL&#41;のインストール ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SSMA コンポーネントの SQL Server &#40;SybaseToSQL&#41;のインストール ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
