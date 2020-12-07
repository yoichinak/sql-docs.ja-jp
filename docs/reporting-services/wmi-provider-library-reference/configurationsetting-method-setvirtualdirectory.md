---
description: SetVirtualDirectory メソッド (WMI MSReportServer_ConfigurationSetting)
title: SetVirtualDirectory メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8c0ef6785a38b0b9dacce50e6b52e63979f255e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480584"
---
# <a name="configurationsetting-method---setvirtualdirectory"></a>ConfigurationSetting メソッド - SetVirtualDirectory
  指定したアプリケーションの仮想ディレクトリの名前を設定します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *Application*  
 仮想ディレクトリを設定するアプリケーションの名前。  
  
 *VirtualDirectory*  
 仮想ディレクトリの名前。  
  
 *lcid*  
 仮想ディレクトリのロケール ID。  
  
 *Error*  
 [out] 発生したエラーの説明。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値が 0 の場合はメソッド呼び出しが正常に完了したことを示します。エラー コードの場合は呼び出しが失敗したことを示します。  
  
## <a name="remarks"></a>解説  
 アプリケーションは、すべての URL 予約に対して仮想ディレクトリの名前を 1 つだけ持つことができます。  
  
 VirtualDirectory に指定する値は、仮想ディレクトリの名前付け規則に準拠している必要があります。 VirtualDirectory には空の文字列または空白を指定できません。  
  
 Configuration\URLReservations\Application\VirtualDirectory 要素の値を更新します。 URL 予約が作成されていない場合でも成功します。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
