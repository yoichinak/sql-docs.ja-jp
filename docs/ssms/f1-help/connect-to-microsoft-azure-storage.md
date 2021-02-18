---
description: Microsoft Azure Storage への接続
title: Microsoft Azure Storage への接続
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/12/2017
ms.openlocfilehash: 073a2a9597fa05d36ee3fe4724dffd7b38284493
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100351667"
---
# <a name="connect-to-microsoft-azure-storage"></a>Microsoft Azure Storage への接続

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
ストレージ アカウントを指定したり、Azure への接続を検証したりするには、 **[Azure Storage Connection]\(Azure Storage の接続\)** ダイアログを使用します。  
  
## <a name="options"></a>オプション  
Azure アカウントに関する次の情報を指定し、 **[次へ]** を選択して続行します。  
  
1.  **[ストレージ アカウント]** : ストレージ アカウント名を指定します。

   >[!NOTE]
   > [汎用のストレージ アカウント](/azure/storage/common/storage-introduction#azure-storage-services)にのみ接続できます。 他の種類のストレージ アカウントに接続すると、次のようなエラーが発生することがあります。
   >
   >  The value for one of the HTTP headers is not in the correct format. (いずれかの HTTP ヘッダーの値の形式が正しくありません。) (Microsoft.SqlServer.StorageClient)
   >
   >  リモート サーバーがエラーを返しました: (400) 無効な要求。 (System)

2.  **[アカウント キー]** : 指定したストレージ アカウントのアカウント キーを指定します。  
  
3.  **[セキュリティ保護されたエンドポイントを使用する (HTTPS)]** : 暗号化された通信とネットワーク Web サーバーのセキュア ID を利用します。  
  
4.  **[アカウント キーを保存する]** : 暗号化されたファイルにパスワードが保存されます。  
