---
description: SetSecureConnectionLevel メソッド (WMI MSReportServer_ConfigurationSetting)
title: SetSecureConnectionLevel メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b7cc099e20e27f16e1d58779bba7d76f47f5d269
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480594"
---
# <a name="configurationsetting-method---setsecureconnectionlevel"></a>ConfigurationSetting メソッド - SetSecureConnectionLevel
  レポート サーバーのセキュリティで保護された接続レベルを設定します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *Level*  
 セキュリティで保護された接続レベルを表す整数値。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>解説  
 このメソッドを呼び出すと、レポート サーバーの SecureConnectionLevel プロパティ値が指定した値に設定されます。 値 0 は、TLS がオフであることを示します。 1 以上の値は、TLS がオンであることを示します。  
  
-   値を設定すると、レポート サーバー構成ファイルの SecureConnectionLevel 要素が変更されます。指定した **Level** が 1 以上の場合は、構成ファイルの *URLRoot* 要素が "https://" を使用するように設定されます。指定した *Level* が 0 の場合は、"http://" を使用するように設定されます。  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]で、SecureConnectionLevel がオン/オフのスイッチとして使用されます。既定値は 0 です。 SetSecureConnectionLevel メソッド API に渡された値が 1 以上である場合、TLS はオンであると見なされ、それに従って rsreportserver.config ファイルで構成プロパティ SecureConnectionLevel が設定されます。 値 2 と 3 は、旧バージョンとの互換性のために許可されています。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
