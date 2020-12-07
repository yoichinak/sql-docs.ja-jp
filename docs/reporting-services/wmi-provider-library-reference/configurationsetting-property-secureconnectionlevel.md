---
description: SecureConnectionLevel プロパティ (WMI MSReportServer_ConfigurationSetting)
title: SecureConnectionLevel プロパティ (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dcf7fdc038f5284d78835e64e568bb348756a3d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373158"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>ConfigurationSetting プロパティ - SecureConnectionLevel
  RSReportServer.config ファイルに指定された、セキュリティで保護された接続レベルを返します。 読み取り専用です。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>プロパティ値  
 セキュリティで保護された接続レベルを表す **整数** 値。 この戻り値は、TLS が構成されているかどうかを示します。 1 以上の値は、TLS がオンであることを示します。 値 0 は、TLS がオフであることを示します。  
  
## <a name="example-code"></a>コード例  
 [MSReportServer_ConfigurationSetting クラス](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>解説

SQL Server 2008 R2 で、SecureConnectionLevel はオン/オフのスイッチとして使用されます。 詳細については、「[ConfigurationSetting メソッド - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)」を参照してください。

## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
