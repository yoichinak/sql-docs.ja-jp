---
description: sysssispackages (Transact-SQL)
title: sysssispackages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d1a1bda3bfea233f7a586a8147f268fbdb1e6ade
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419036"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  に保存されているパッケージごとに1行の値を格納 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このテーブルは、 **msdb** データベースに格納されます。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|パッケージの一意識別子です。|  
|**id**|**uniqueidentifier**|パッケージの GUID。|  
|**description**|**nvarchar**|パッケージの説明 (省略可)。|  
|**createdate**|**datetime**|パッケージが作成された日付。|  
|**folderid**|**uniqueidentifier**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] によってパッケージの一覧が格納される論理フォルダーの GUID。|  
|**ownersid**|**varbinary**|パッケージを作成したユーザーの一意のセキュリティ識別子。|  
|**(microsoft.sql.chainer.packagedata.dll**|**image**|パッケージです。|  
|**packageformat**|**int**|パッケージが保存される形式は次のとおりです。<br /><br /> 値が2の場合は、パッケージが形式で保存されていることを示し [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ます。<br /><br /> 値3は、パッケージが以降の形式で保存されることを示し [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ます。|  
|**packagetype**|**int**|パッケージを作成したクライアント。 次のような値が考えられます。<br /><br /> 0 (既定値)<br /><br /> 1 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポートウィザード)<br /><br /> 3 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション)<br /><br /> 5 ( [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナー)<br /><br /> 6 (メンテナンス プラン デザイナーまたはメンテナンス プラン ウィザード)<br /><br /> <br /><br /> この列の値は列挙型に対応していることに注意して <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType> ください。|  
|**vermajor**|**int**|パッケージの最新のメジャー バージョン。|  
|**verminor**|**int**|パッケージの最新のマイナー バージョン。|  
|**verbuild**|**int**|パッケージの最新のビルドです。|  
|**vercomments**|**nvarchar**|パッケージ バージョンについてのコメント。|  
|**verid**|**uniqueidentifier**|パッケージのバージョンの GUID。|  
|**isencrypted**|**bit**|パッケージが暗号化されているかどうかを示すブール値です。|  
|**readロール id**|**varbinary**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パッケージを読み込むことができるロール。|  
|**writerolesid**|**varbinary**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パッケージを保存できるロール。|  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; パッケージ](../../integration-services/integration-services-ssis-packages.md)  
  
  
