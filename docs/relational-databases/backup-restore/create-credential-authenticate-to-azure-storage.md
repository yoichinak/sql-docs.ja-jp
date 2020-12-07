---
title: 資格情報の作成- Azure ストレージに対する認証 | Microsoft Docs
description: SQL Server では、[データベースのバックアップ] ダイアログ ボックスの [資格情報の作成] ページを使用して、接続を検証するための Azure 管理証明書を指定します。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: cawrites
ms.author: chadam
ms.openlocfilehash: 331d973e3290c5528ba811f7d6306f7505b55041
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129265"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>資格情報の作成- Azure ストレージに対する認証
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **[Backup To URL - 資格情報の作成]** ダイアログ ボックスを使用すると、新しい SQL 資格情報を作成できます。  
  
 このダイアログ ボックスを使用して資格情報を作成する場合、サブスクリプションとストレージ アカウント情報を検証するために、ローカル証明書ストアに追加した Azure 管理証明書、またはコンピューターにダウンロードした公開プロファイルを指定する必要があります。  
  
 **[SQL 資格情報]**  
 作成する SQL 資格情報の名前を指定します。  
  
## <a name="azure-credentials"></a>Azure 資格情報  
 **[管理証明書]**  
 このオプションを使用して、Azure からの管理証明書に一致するローカル証明書ストアの証明書を指定します。 Azure 管理証明書の詳細については、「[Azure の管理証明書の作成とアップロード](/previous-versions/azure/gg551722(v=azure.100))」を参照してください。  
  
 **サブスクリプション**  
 ローカル証明書ストアの管理証明書と一致する Azure サブスクリプション ID を選択、入力、または貼り付けます。  
  
 **[公開プロファイル]**  
 コンピューターにダウンロードした公開プロファイルがある場合は、このオプションを使用します。 このオプションを使用すると、サブスクリプション ID と証明書が自動的に入力されます。  
  
> [!CAUTION]  
>  SQL Server では現在、公開プロファイルのバージョン 2.0 がサポートされています。 公開プロファイルのサポート対象バージョンをダウンロードするには、「 [公開プロファイルのバージョン 2.0 のダウンロード](https://go.microsoft.com/fwlink/?LinkId=396421)」をご覧ください。  
  
## <a name="storage-account"></a>ストレージ アカウント  
 バックアップ ファイルを格納するために使用するストレージ アカウントを選択します。  
  
