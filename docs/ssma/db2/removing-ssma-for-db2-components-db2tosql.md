---
description: SSMA for DB2 コンポーネントの削除 (DB2ToSQL)
title: SSMA for DB2 コンポーネントの削除 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0341869ff5d39ad35fce6ac450d293eaac1feb38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488171"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>SSMA for DB2 コンポーネントの削除 (DB2ToSQL)
DB2 からへのデータベースの移行が完了したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA コンポーネントのアンインストールが必要になる場合があります。 クライアントコンポーネントはいつでもアンインストールできます。 ただし、移行した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで**sysdb**データベースの**ssma_DB2**スキーマの関数が使用されなくなっていない限り、から拡張パックをアンインストールしないでください。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>SSMA for DB2 クライアントのアンインストール  
SSMA をアンインストールするには、[ **プログラムの追加と削除**] を使用します。  
  
**SSMA をアンインストールするには**  
  
1.  [コントロール] パネルで **[プログラムの追加と削除]** を開きます。  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 の Migration Assistant**を選択し、[**削除**] をクリックします。  
  
3.  SSMA をアンインストールすることを確認するには、[ **はい**] をクリックします。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックのアンインストール  
移行したデータベースが **sysdb. ssma_DB2** スキーマのオブジェクトを使用していないことが確実な場合は、スキーマから拡張機能パックを削除することにより、拡張パックを削除できます。 Windows のアンインストールはありません。  
  
## <a name="see-also"></a>参照  
[SSMA for DB2 クライアント &#40;DB2ToSQL&#41;のインストール ](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server &#40;DB2ToSQL&#41;での SSMA コンポーネントのインストール ](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
