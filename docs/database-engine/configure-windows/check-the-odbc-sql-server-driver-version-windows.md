---
title: ODBC SQL Server のドライバーのバージョンを確認する方法 (Windows) | Microsoft Docs
description: Windows ODBC データ ソース アドミニストレーターを使用して、コンピューターにインストールされている ODBC ドライバーのバージョンを確認する方法について説明します。
ms.custom: ''
ms.date: 11/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- driver version number [ODBC]
- ODBC drivers, version number
ms.assetid: 43451080-a562-4231-b1d4-1ba35ca0ea79
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 3de893c474fbff853c16eaf537c14d64163835a4
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670646"
---
# <a name="check-the-odbc-sql-server-driver-version-windows"></a>ODBC SQL Server のドライバーのバージョンを確認する方法 (Windows)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  コンピューターによっては、[!INCLUDE[msCoName](../../includes/msconame-md.md)] や他社製のさまざまな ODBC ドライバーが組み込まれています。 このトピックでは、Windows の **ODBC データ ソース アドミニストレーター** を使用して、インストールされている ODBC ドライバーのバージョンを確認する方法について説明します。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-check-the-odbc-sql-server-driver-version-32-bit-odbc"></a>ODBC SQL Server のドライバーのバージョンを確認するには (32 ビット ODBC)  
  
-   **ODBC データ ソース アドミニストレーター**で **[ドライバー]** タブをクリックします。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [バージョン] **列に、Microsoft** エントリの情報が表示されます。  


> [!NOTE]  
>  SQL Database の Azure Active Directory 認証への接続には、[ODBC Driver 17 for SQL Server](../../connect/odbc/download-odbc-driver-for-sql-server.md) などの最新ドライバーをインストールします。   

  
## <a name="see-also"></a>参照  
 [ODBC データ ソース アドミニストレーターの起動](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
