---
title: Sybase の SQL Server Migration Assistant (SybaseToSQL) |Microsoft Docs
description: SSMA for Sybase の詳細については、SQL Server または Azure SQL Database に ASE データベースを移行するための詳細な手順に従ってください。
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59e63eac-8a7e-4d54-be1c-0633a9bf510d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: d32f59e4f9c81236199203cfa063b7d26152986b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100030750"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase の SQL Server Migration Assistant (SybaseToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) For Sybase Adaptive Server Enterprise (ase) は、ase データベースをに移行する [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ためのツールです。2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 on Windows および Linux、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2019 (windows と linux)、または [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database。 SSMA for Sybase は、ASE データベースオブジェクトをデータベースオブジェクトに変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、それらのオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に作成した後、ase からまたは Azure SQL Database にデータを移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。
  
このドキュメントでは、SSMA for Sybase について説明します。また、ASE データベースをまたは Azure SQL Database に移行する手順 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と、移行後に発生する可能性がある問題に関する情報を示します。 詳細については、以下の記事をお読みください。  
  
## <a name="contents"></a>内容  
  
|Section|説明|
|-----------|---------------|
|[SSMA for Sybase &#40;SybaseToSQL&#41;の新機能 ](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|SSMA リリースに対する変更の一覧を示します。|  
|[SSMA for Sybase &#40;SybaseToSQL&#41;のインストール ](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|SSMA for Sybase クライアントおよび必要なコンポーネントを、インスタンスを実行しているコンピューターにインストールするための前提条件と手順を説明した記事が含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|[SSMA for Sybase のはじめに &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|ユーザーインターフェイス、プロジェクト、および構成オプションについて説明します。|  
|[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|変換プロセスの概要と、プロセスの各手順に関する詳細情報について説明します。|  
|[ユーザーインターフェイスリファレンス &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|SSMA for Sybase のダイアログボックスのドキュメントが含まれています。|  
|[SSMA for Sybase Console の操作](working-with-ssma-for-sybase-console-sybasetosql.md)|SSMA コンソールアプリケーションに関するドキュメントが含まれています。|  
|[SSMA for Sybase のサポートを取得する](../sql-server-migration-assistant.md)|追加のサポートを受ける方法について説明します。|