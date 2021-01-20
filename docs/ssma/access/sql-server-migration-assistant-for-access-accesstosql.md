---
title: アクセスの SQL Server Migration Assistant (アクセス可能な Sql) |Microsoft Docs
description: SSMA for Access の詳細については、SQL Server または Azure SQL Database にアクセスデータベースを移行するための詳細な手順に関するページを参照してください。
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 25e7694505f7f67702f476983c33120a87539887
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596424"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>アクセスのための SQL Server Migration Assistant (アクセス可能な Sql)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access の Migration Assistant (SSMA) は、から [!INCLUDE[msCoName](../../includes/msconame_md.md)] データベースを移行するためのツールです。バージョン97から2010、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 (windows および Linux の場合)、2019 (windows と linux の場合)、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database にアクセス [!INCLUDE[msCoName](../../includes/msconame_md.md)] できます。 SSMA for Access は、Access データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または AZURE SQL database オブジェクトに変換し、それらのオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に読み込み、Access からまたは Azure SQL Database にデータを移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。
  
このドキュメントでは、アクセスのための SSMA について説明します。また、アクセスデータベースをまたは Azure SQL Database に移行する手順 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と、移行後に発生する可能性がある問題に関する情報を示します。  
  
## <a name="contents"></a>内容  
  
|Section|説明|
|-----------|---------------|
|[SSMA for Access の新機能](./what-s-new-in-ssma-for-access-accesstosql.md)|SSMA リリースに対する変更の一覧を示します。|  
|[アクセスのための SQL Server Migration Assistant のインストール](installing-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA をインストールするための前提条件、SSMA をインストールおよびライセンスする手順、および最新バージョンへのリンクを示します。|  
|[アクセスのための SQL Server Migration Assistant を使用したはじめに &#40;アクセス許可 SQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA とそのユーザーインターフェイスについて説明します。|  
|[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)|/SQL Azure に変換するために Access データベースを準備する方法について説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|変換プロセスの概要と、プロセスの各手順に関する詳細情報について説明します。|  
|[Access アプリケーションの SQL Server へのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|既存の Access アプリケーションをで使用する方法について説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|[ユーザーインターフェイスリファレンス](user-interface-reference-accesstosql.md)|SSMA ダイアログボックスのドキュメントが含まれています。|  
|[SSMA for Access コンソールの操作](working-with-ssma-for-access-console-accesstosql.md)|SSMA コンソールアプリケーションに関するドキュメントが含まれています。|  
|[SSMA のアクセス権の取得](../sql-server-migration-assistant.md)|追加のサポートを受ける方法について説明します。|