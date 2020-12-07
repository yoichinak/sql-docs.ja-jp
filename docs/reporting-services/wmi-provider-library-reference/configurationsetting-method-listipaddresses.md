---
description: ListIPAddresses メソッド (WMI MSReportServer_ConfigurationSetting)
title: ListIPAddresses メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 822b2022bd8a6ede5c750c1560f1e1424e9576ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480634"
---
# <a name="configurationsetting-method---listipaddresses"></a>ConfigurationSetting メソッド - ListIPAddresses
  レポート サーバー コンピューターの IP アドレスを一覧表示します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub ListIPAddresses (ByRef IPAddress() as String, _  
    ByRef IPVersion()as String, ByRef IsDhcpEnabled () as Boolean, _   
    ByRef Length as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListIPAddresses (out string[] IPAddress,   
    out string[] IPVersion, out bool[] isDhcpEnabled, out int length,   
    out int HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *IPAddress[]*  
 [out] コンピューターの IP アドレスの一覧。  
  
 *IPVersion[]*  
 [out] IP アドレスのバージョン。  
  
 *IsDhcpEnabled[]*  
 [out] IP アドレスが DHCP 対応かどうか。  
  
 *[データ型]*  
 [out] メソッドによって返される配列の長さ。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値が 0 の場合はメソッド呼び出しが正常に完了したことを示します。エラー コードの場合は呼び出しが失敗したことを示します。  
  
## <a name="remarks"></a>解説  
 *IPVersion* の文字列は、"V4" または "V6" です。  
  
 *IsDhcpEnabled* が **True**の場合、 *IPAddress* は動的です。 これは、TLS バインドには使用しないでください。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
