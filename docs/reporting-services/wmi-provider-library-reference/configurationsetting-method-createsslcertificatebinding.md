---
description: CreateSSLCertificateBinding メソッド (WMI MSReportServer_ConfigurationSetting)
title: CreateSSLCertificateBinding メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b45f1f0344f00053978dd24db334c7dafad0a066
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497965"
---
# <a name="configurationsetting-method---createsslcertificatebinding"></a>ConfigurationSetting メソッド - CreateSSLCertificateBinding
  TLS/SSL 証明書のバインドを作成します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *Application*  
 証明書のバインドを作成する必要があるアプリケーションの名前。  
  
 *CertificateHash*  
 証明書のハッシュ。  
  
 *IPAddress*  
 アプリケーションの IP アドレス。  
  
 *[ポート]*  
 バインドに関連付けられた TLS ポート。  
  
 *Lcid*  
 返されるエラー メッセージに使用するロケール。  
  
 *Error*  
 [out] 発生したエラーの説明。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値が 0 の場合はメソッド呼び出しが正常に完了したことを示します。エラー コードの場合は呼び出しが失敗したことを示します。  
  
## <a name="remarks"></a>解説  
 このメソッドは、アプリケーションの rsreportserver.config にバインドを追加します。 バインドが HTTP.SYS に存在しない場合は作成されます。  
  
 バインドを作成する前に、メソッドの呼び出しによって、指定されたアプリケーションの URL 予約が調査され、TLS/SSL 証明書のバインドが有効かどうかが確認されます。  
  
 次の条件が検証されて、その結果エラーが発生する場合があります。  
  
1.  証明書が存在しない。  
  
2.  指定された IP アドレスがこのコンピューターの IP アドレスと一致しない。  
  
3.  指定された IP アドレスが DHCP の IP アドレス (定期的に変更される) であるため、代わりにワイルドカードの IP アドレス (0.0.0.0) が使用されている。  
  
4.  指定された IP アドレスが URL 予約の IP アドレスと一致せず、ワイルドカードまたはホスト名の URL 予約も存在しない。  
  
5.  ホスト名を指定する URL 予約は存在するが、ホスト名が証明書のホスト名と一致しない。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
