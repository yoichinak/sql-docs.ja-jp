---
description: Web 設定リファレンス (Master Data Services)
title: Web 設定リファレンス
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7f4baf9f3ef626f5e2dcdc62092afaf1e586df33
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196096"
---
# <a name="web-configuration-reference-master-data-services"></a>Web 設定リファレンス (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では Web.config ファイルを使用することで、インターネット インフォメーション サービス (IIS) を有効にして [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションおよび Web サービスをホストできるようにする構成設定を取り込みます。 この Web.config ファイルは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インストール パスの WebApplication フォルダーにあります。 パスと権限の詳細については、「[フォルダーとファイルの権限 (マスター データ サービス)](../master-data-services/folder-and-file-permissions-master-data-services.md)」を参照してください。  
  
## <a name="webconfig-elements"></a>Web.Config 要素  
 Web.config ファイルには、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **\<masterDataServices>** 標準の IIS、.NET Framework、ASP.NET、および WINDOWS COMMUNICATION FOUNDATION (WCF) 構成要素に加えて、カスタム要素が含まれています。 次の表では、Web.config ファイルに含まれている要素について説明します。  
  
|Configuration 要素|説明|  
|---------------------------|-----------------|  
|**masterDataServices**|Custom 要素。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web サービスを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに接続します。|  
|**connectionStrings**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [connectionStrings 要素 (ASP.NET 設定スキーマ)](/previous-versions/dotnet/netframework-4.0/bf7sd233(v=vs.100)) 」を参照してください。|  
|**system.web**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [system.web 要素 (ASP.NET 設定スキーマ)](/previous-versions/dotnet/netframework-4.0/dayb112d(v=vs.100)) 」を参照してください。|  
|**代替**|.NET Framework 要素。 詳細については、MSDN ライブラリの「 [ \<startup> Element](/dotnet/framework/configure-apps/file-schema/startup/startup-element) 」を参照してください。|  
|**ランタイム**|.NET Framework 要素。 詳細については、MSDN ライブラリの「 [ \<runtime> Element](/dotnet/framework/configure-apps/file-schema/runtime/runtime-element) 」を参照してください。|  
|**system.codedom**|.NET Framework 要素。 詳細については、MSDN ライブラリの「 [ \<system.codedom> Element](/dotnet/framework/configure-apps/file-schema/compiler/system-codedom-element) 」を参照してください。|  
|**system.web. 拡張子**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [system.web.extensions 要素 (ASP.NET 設定スキーマ)](/previous-versions/dotnet/netframework-4.0/bb546044(v=vs.100)) 」を参照してください。|  
|**system.webServer**|IIS 要素を含んだセクション グループ。 詳細については、MSDN ライブラリの「[system.webServer セクション グループ \[IIS 7 設定スキーマ\]](/previous-versions/iis/settings-schema/ms689429(v=vs.90))」を参照してください。|  
|**system.serviceModel**|WCF 要素。 詳細については、MSDN ライブラリの「」を参照してください [\<system.serviceModel>](/dotnet/framework/configure-apps/file-schema/wcf/system-servicemodel) 。|  
|**system.diagnostics**|.NET Framework 要素。 詳細については、MSDN ライブラリの「 [ \<system.diagnostics> Element](/dotnet/framework/configure-apps/file-schema/trace-debug/system-diagnostics-element) 」を参照してください。|  
|**appSettings**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [appSettings 要素 (全般設定スキーマ)](/previous-versions/dotnet/netframework-4.0/ms228154(v=vs.100)) 」を参照してください。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 要素  
 要素は、 **\<masterDataServices>** [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web サービスをデータベースに接続するために使用されるカスタム要素です [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
### <a name="syntax"></a>構文  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>要素と属性  
  
|Item|説明|  
|----------|-----------------|  
|**instance**|子要素。 Web サービスとデータベース接続文字列の情報を指定する属性を含みます。|  
|**virtualPath**|Attribute。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションとサービスの仮想パスを指定します。 これは、IIS ApplicationHost.config ファイルの要素の下にある要素の **パス** 属性に対応し **\<application>** **\<site>** ます。|  
|**siteName**|Attribute。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションとサービスをホストするサイトの名前を指定します。 これは、IIS ApplicationHost.config ファイルのの下の要素の **name** 属性に対応して **\<site>** **\<sites>** います。|  
|**connectionName**|Attribute。 使用する接続の名前を指定します。 これは Web.config の要素の下にある要素の **name** 属性に対応して **\<add>** **\<connectionStrings>** います。|  
|**serviceName**|Attribute。 Web サービスの名前を指定します。 これは Web.config の要素の下にある要素の **name** 属性に対応して **\<service>** **\<services>** います。|  
  
### <a name="example"></a>例  
 次の例は、Contoso サイト上の MDS1 という名前のサービスと、MDSDB によって指定された接続文字列を使用した /MDS パスを示しています。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
