---
title: SSMA for SAP ASE のインストール (SybaseToSQL) |Microsoft Docs
description: この記事では、クライアントアプリケーションと拡張機能パックを含む SAP ASE の SQL Server Migration Assistant をインストール、アップグレード、およびアンインストールする方法について説明します。
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8fca8219dfe89c8229b8d296fe355b97417d9daf
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100073366"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>SSMA for SAP ASE のインストール (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SAP Adaptive Server Enterprise (ASE) の Migration Assistant (SSMA) は、SAP ASE からまたは Azure SQL Database への移行を実行するために使用するクライアントアプリケーションで構成さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れています。 また、データの移行と、移行したデータベースでの ASE システム関数の使用をサポートする拡張パックも含まれています。  
  
移行手順を実行するコンピューターにクライアントアプリケーションをインストールします。 を実行しているコンピューターに、移行されたデータベースをホストする拡張パックファイルをインストールし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="upgrading-ssma-for-sap-ase"></a>SSMA for SAP ASE のアップグレード  
SSMA for SAP ASE の新しいバージョンにアップグレードする場合は、最初にクライアントとサーバー拡張機能パックをアンインストールする必要があります。 その後、新しいバージョンをインストールします。  
  
以前のバージョンの SSMA for SAP ASE からプロジェクトを開くと、プロジェクトを新しいバージョンに変換するかどうかを確認するメッセージが表示されます。 新しいバージョンの SSMA でプロジェクトを使用する場合は、[ **はい** ] をクリックします。  
  
## <a name="contents"></a>内容  
  
|[アーティクル]|説明|  
|---------|---------------|  
|[SSMA for SAP ASE クライアント &#40;SybaseToSQL&#41;のインストール ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|SSMA for SAP ASE クライアントをインストールするための情報と手順について説明します。|  
|[SSMA コンポーネントの SQL Server &#40;SybaseToSQL&#41;のインストール ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|のインスタンスに拡張機能パックをインストールするための情報と手順について説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|[SSMA for SAP ASE コンポーネントの削除 &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|クライアントプログラムと拡張機能パックをアンインストールする手順について説明します。|  
  
## <a name="see-also"></a>関連項目  
[SAP ASE データベースの SQL Server Azure SQL Database &#40;SybaseToSQL&#41;への移行 ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
