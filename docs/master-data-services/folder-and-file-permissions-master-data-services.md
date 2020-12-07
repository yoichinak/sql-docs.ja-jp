---
description: フォルダーとファイルの権限 (マスター データ サービス)
title: フォルダーとファイルの権限
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], file and folder
- folders [Master Data Services]
- files [Master Data Services]
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0d06fb6aaacdac159ab9241209c862e22758e999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88388828"
---
# <a name="folder-and-file-permissions-master-data-services"></a>フォルダーとファイルの権限 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]のインストール時に、ファイル システムで指定のインストール パスにフォルダーとファイルが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 共有機能用にインストールされます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 共有機能に既定のインストール パスを使用する場合、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] のインストール パスは *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services です。 共有機能のインストール パスは変更できますが、親フォルダーから継承される権限と [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]に対して明示的に設定されている権限に注意する必要があります。  
  
## <a name="inherited-permissions"></a>継承された権限  
 **Microsoft SQL Server** フォルダー、 **Master Data Services** フォルダー、および大半のサブフォルダーとファイルは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のセットアップで指定した親フォルダーから権限を継承します。 既定のインストール場所を使用している場合、権限の継承元の親フォルダーは *drive*:\Program Files です。 次の表では、 **Program Files**に対する既定の権限について説明します。  
  
> [!NOTE]  
>  **Program Files**に対する既定の権限を変更するか、または別のインストール場所を選択すると、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] のフォルダーとファイルは対応する親フォルダーから権限を継承します。そのため、次の表で説明する権限と異なる場合があります。  
  
###### <a name="program-files-default-permissions"></a>Program Files の既定の権限  
  
|グループ名またはアカウント名|アクセス許可|  
|---------------------------|-----------------|  
|CREATOR OWNER|特別な権限|  
|SYSTEM|特別な権限|  
|管理者|特別な権限|  
|ユーザー|読み取りと実行、フォルダー内容の一覧表示、読み取り|  
|TrustedInstaller|フォルダー内容の一覧表示、特別な権限|  
  
## <a name="explicit-permissions"></a>明示的権限  
 **MDSTempDir** フォルダーと [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config ファイル ( **WebApplication** フォルダーにあります) は、権限を継承しません。 これらには、選択したインストール パスに関係なく、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]をインストールするときに明示的に設定された権限があります。 これらの権限を変更しないでください。  
  
###### <a name="mdstempdir-permissions"></a>MDSTempDir 権限  
  
|グループ名またはアカウント名|アクセス許可|  
|---------------------------|-----------------|  
|SYSTEM|変更、読み取りと実行、フォルダー内容の一覧表示、読み取り、書き込み|  
|管理者|変更、読み取りと実行、フォルダー内容の一覧表示、読み取り、書き込み|  
|MDS_ServiceAccounts|変更、読み取りと実行、フォルダー内容の一覧表示、読み取り、書き込み|  
  
###### <a name="webconfig-permissions"></a>Web.config 権限  
  
|グループ名またはアカウント名|アクセス許可|  
|---------------------------|-----------------|  
|SYSTEM|フル コントロール、変更、読み取りと実行、読み取り、書き込み|  
|管理者|フル コントロール、変更、読み取りと実行、読み取り、書き込み|  
|MDS_ServiceAccounts|読み取りと実行、読み取り|  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config ファイルのコンテンツの詳細については、「[Web 設定リファレンス (マスター データ サービス)](../master-data-services/web-configuration-reference-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](../master-data-services/install-windows/install-master-data-services.md)  
  
  
