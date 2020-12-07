---
description: GetReportServerUrls メソッド (WMI MSReportServer_Instance)
title: GetReportServerUrls メソッド (WMI MSReportServer_Instance) | Microsoft Docs
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e3b3e0f7e521cd2a105a3cf093c0a179bd7306d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257525"
---
# <a name="msreportserver_instance-methods---getreportserverurls"></a>MSReportServer_Instance メソッド - GetReportServerUrls
  ユーザーがレポート サーバーと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]へのアクセスに使用できる URL の一覧を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *ApplicationName[]*  
 インストールされているアプリケーションを含む配列。 値は **ReportServerWebService** または **ReportServerWebApp**です。  
  
 *URLs[]*  
 正常に登録された URL を含む配列。  
  
 *Length*  
 返された配列の長さを含む整数値。  
  
 *HRESULT*  
 成功を表す値またはエラー コード。  
  
## <a name="return-values"></a>戻り値  
  
## <a name="remarks"></a>解説  
 WMI 管理オブジェクトによって公開されるメソッドは、InvokeMethod 関数によって呼び出されます。 詳細については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI ドキュメントの「管理オブジェクトのメソッドの実行」を参照してください。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
