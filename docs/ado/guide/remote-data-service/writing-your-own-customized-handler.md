---
description: 独自のカスタム ハンドラーの記述
title: 独自のカスタマイズされたハンドラーを作成する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d761b781e7de4225f51fb3600ac467015a0c274
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722723"
---
# <a name="writing-your-own-customized-handler"></a>独自のカスタム ハンドラーの記述
既定の RDS サポートを必要とするが、ユーザーの要求とアクセス権をより細かく制御できる IIS サーバー管理者の場合は、独自のハンドラーを作成することもできます。  
  
 MSDFMAP。ハンドラーは、 **IDataFactoryHandler** インターフェイスを実装します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler インターフェイス  
 このインターフェイスには、 **Getrecordset** と **Reconnect**の2つのメソッドがあります。 どちらの方法でも、 [カーソル位置](../../reference/ado-api/cursorlocation-property-ado.md) プロパティを **adUseClient**に設定する必要があります。  
  
 どちらのメソッドも、"**Handler =**" キーワードの最初のコンマの後に表示される引数を受け取ります。 たとえば、 `"Handler=progid,arg1,arg2;"` は引数の文字列を渡し、は `"arg1,arg2"` `"Handler=progid"` null 引数を渡します。  
  
## <a name="getrecordset-method"></a>GetRecordset メソッド  
 このメソッドは、指定された引数を使用して、データソースに対してクエリを行い、新しい [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトを作成します。 **レコードセット**は**Adlockbatchoptimistic**で開かれている必要があり、非同期に開くことはできません。  
  
### <a name="arguments"></a>引数  
 ***conn***  接続文字列。  
  
 ***args***  ハンドラーの引数。  
  
 ***クエリ***  クエリを作成するためのコマンドテキスト。  
  
 ***ppRS*** **レコードセット** が返される位置のポインター。  
  
## <a name="reconnect-method"></a>Reconnect メソッド  
 このメソッドは、データソースを更新します。 このメソッドは、新しい [接続](../../reference/ado-api/connection-object-ado.md) オブジェクトを作成し、指定された **レコードセット**をアタッチします。  
  
### <a name="arguments"></a>引数  
 ***conn***  接続文字列。  
  
 ***args***  ハンドラーの引数。  
  
 ***pr*** **レコードセット** オブジェクトです。  
  
## <a name="msdfhdlidl"></a>msdfhdl .idl  
 これは、 **msdfhdl .idl**ファイルに表示される**IDataFactoryHandler**のインターフェイス定義です。  
  
```cpp
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>参照  
 [カスタマイズファイルの接続セクション](./customization-file-connect-section.md)   
 [カスタマイズファイルログセクション](./customization-file-logs-section.md)   
 [カスタマイズファイル SQL セクション](./customization-file-sql-section.md)   
 [カスタマイズファイルの UserList セクション](./customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](./datafactory-customization.md)   
 [必要なクライアント設定](./required-client-settings.md)   
 [カスタマイズ ファイルの概要](./understanding-the-customization-file.md)