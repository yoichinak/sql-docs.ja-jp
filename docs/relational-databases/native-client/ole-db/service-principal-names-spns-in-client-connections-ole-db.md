---
description: クライアント接続 (OLE DB) でのサービス プリンシパル名 (SPN)
title: サービスプリンシパル名の接続の OLE DB
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7215c4d2727ece82b223e7546480fafc5808bc32
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448285"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>クライアント接続 (OLE DB) でのサービス プリンシパル名 (SPN)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  このトピックでは、クライアント アプリケーションでサービス プリンシパル名 (SPN) をサポートする OLE DB のプロパティとメンバー関数について説明します。 クライアント アプリケーションでの SPN の詳細については、「[クライアント接続でのサービス プリンシパル名 &#40;SPN&#41; のサポート](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)」を参照してください。 サンプルについては、「[統合 Kerberos 認証 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md)」を参照してください。  
  
## <a name="provider-initialization-string-keywords"></a>プロバイダー初期化文字列のキーワード  
 次に示すプロバイダー初期化文字列のキーワードは、OLE DB アプリケーションで SPN をサポートします。 次の表の "キーワード" 列の値は、IDBInitialize::Initialize のプロバイダー文字列に使用されます。 "説明" 列の値は、ADO または IDataInitialize::GetDataSource を使用して接続するときに初期化文字列で使用されます。  
  
|Keyword|説明|値|  
|-------------|-----------------|-----------|  
|ServerSPN|サーバー SPN|サーバーの SPN。 既定値は空の文字列です。この場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|FailoverPartnerSPN|フェールオーバー パートナー SPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。この場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
  
## <a name="data-source-initialization-properties"></a>データ ソース初期化プロパティ  
 **DBPROPSET_SQLSERVERDBINIT** プロパティ セット内の次のプロパティは、アプリケーションによる SPN の指定を可能にします。  
  
|Name|種類|使用法|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR、読み取り/書き込み|サーバーの SPN を指定します。 既定値は空の文字列です。この場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR、読み取り/書き込み|フェールオーバー パートナーの SPN を指定します。 既定値は空の文字列です。この場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
  
## <a name="data-source-properties"></a>データ ソースのプロパティ  
 **DBPROPSET_SQLSERVERDATASOURCEINFO** プロパティ セット内の次のプロパティは、アプリケーションによる認証方法の検出を可能にします。  
  
|Name|種類|使用法|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR、読み取り専用|接続に使用された認証方法を返します。 アプリケーションに返される値は、Windows が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client に返す値です。 返される値は次のとおりです。 <br />"NTLM"。これは NTLM 認証を使用して接続を開いたときに返されます。<br />"Kerberos"。これは Kerberos 認証を使用して接続を開いたときに返されます。<br /><br /> 接続が開いていて認証方法を特定できない場合は、VT_EMPTY が返されます。<br /><br /> このプロパティは、データ ソースが初期化されている場合にのみ読み取ることができます。 データ ソースが初期化される前にこのプロパティを読み取ろうとすると、IDBProperties::GetProperies から DB_S_ERRORSOCCURRED または DB_E_ERRORSOCCURRED が返され、必要に応じて、このプロパティの DBPROPSET_PROPERTIESINERROR に DBPROPSTATUS_NOTSUPPORTED が設定されます。 この動作は、OLE DB のコア仕様に従っています。|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL、読み取り専用|接続されているサーバーが相互に認証されている場合は VARIANT_TRUE を返し、それ以外の場合は VARIANT_FALSE を返します。<br /><br /> このプロパティは、データ ソースが初期化されている場合にのみ読み取ることができます。 データ ソースが初期化される前にこのプロパティを読み取ろうとすると、IDBProperties::GetProperies から DB_S_ERRORSOCCURRED または DB_E_ERRORSOCCURRED が返され、必要に応じて、このプロパティの DBPROPSET_PROPERTIESINERROR に DBPROPSTATUS_NOTSUPPORTED が設定されます。 この動作は、OLE DB のコア仕様に従っています。<br /><br /> Windows 認証を使用していない接続に対してこの属性が照会されると、VARIANT_FALSE が返されます。|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB API による SPN のサポート  
 次の表では、クライアント接続で SPN をサポートする OLE DB メンバー関数について説明します。  
  
|メンバー関数|説明|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* には、新しいキーワードである **ServerSPN** と **FailoverPartnerSPN** を含めることができます。|  
|IDataInitialize::GetInitializationString|SSPROP_INIT_SERVERSPN および SSPROP_INIT_FAILOVERPARTNERSPN の値が既定値以外の場合は、それらの値が *ppwszInitString* を介して **ServerSPN** および **FailoverPartnerSPN** のキーワード値として初期化文字列に取り込まれます。 それ以外の場合、これらのキーワードは初期化文字列に取り込まれません。|  
|IDBInitialize::Initialize|データ ソース初期化プロパティに DBPROP_INIT_PROMPT を設定して入力要求を有効にすると、OLE DB の [ログイン] ダイアログ ボックスが表示されます。 これにより、プリンシパル サーバーとそのフェールオーバー パートナーの両方に対して SPN を入力できます。<br /><br /> DPPROP_INIT_PROVIDERSTRING にプロバイダー文字列が設定されている場合、その文字列は新しいキーワード **ServerSPN** および **FailoverPartnerSPN** を認識し、キーワードに値が指定されていれば、その値を使用して SSPROP_INIT_SERVER_SPN および SSPROP_INIT_FAILOVER_PARTNER_SPN を初期化します。<br /><br /> IDBInitialize::Initialize を呼び出す前に IDBProperties::SetProperties を呼び出して、プロパティ SSPROP_INIT_SERVER_SPN および SSPROP_INIT_FAILOVER_PARTNER_SPN を設定することができます。 この方法は、プロバイダー文字列を使用する代わりに使用できます。<br /><br /> プロパティが複数の場所で設定されている場合は、プログラムによって設定された値が、プロバイダー文字列に設定された値より優先されます。 初期化文字列に設定された値は、ログイン ダイアログ ボックスで設定された値より優先されます。<br /><br /> プロバイダー文字列に同じキーワードが複数回使用されている場合は、最初に使用された値が優先されます。|  
|IDBProperties::GetProperties|IDBProperties::GetProperties を呼び出すことで、新しいデータ ソース初期化プロパティ SSPROP_INIT_SERVERSPN と SSPROP_INIT_FAILOVERPARTNERSPN の値、および新しいデータ ソース プロパティ SSPROP_AUTHENTICATIONMETHOD と SSPROP_MUTUALLYAUTHENTICATED の値を取得できます。|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo には、新しいデータ ソース初期化プロパティ SSPROP_INIT_SERVERSPN と SSPROP_INIT_FAILOVERPARTNERSPN、または新しいデータ ソース プロパティ SSPROP_AUTHENTICATION_METHOD と SSPROP_MUTUALLYAUTHENTICATED が含められます。|  
|IDBProperties::SetProperties|IDBProperties::SetProperties を呼び出すことで、新しいデータ ソース初期化プロパティ SSPROP_INITSERVERSPN と SSPROP_INIT_FAILOVERPARTNERSPN の値を設定できます。<br /><br /> これらのプロパティはいつでも設定できますが、データ ソースが既に開いている場合は、次のエラーが返されます。DB_E_ERRORSOCCURRED、"複数ステップの OLE DB の操作でエラーが発生しました。 各 OLE DB の状態の値を確認してください。 作業は終了しませんでした。"|  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
