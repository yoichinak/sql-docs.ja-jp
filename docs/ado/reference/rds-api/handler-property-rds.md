---
description: Handler プロパティ (RDS)
title: Handler プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: rothja
ms.author: jroth
ms.openlocfilehash: 5dc5a8cfc455d27a2bb17b40585e3e38cdd581cf
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722051"
---
# <a name="handler-property-rds"></a>Handler プロパティ (RDS)
[RDSServer](./datafactory-object-rdsserver.md)の機能を拡張するサーバー側のカスタマイズプログラム (ハンドラー) の名前と、*ハンドラー*によって使用されるすべてのパラメーターを示します。  
  
 **適用対象:** [DATACONTROL オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
 *String*  
 ハンドラーの名前とすべてのパラメーターをコンマで区切って指定した**文字列**値 ( `"handlerName,parm1,parm2,...,parm` *N*など `"` )。  
  
## <a name="remarks"></a>解説  
 このプロパティは、[[カーソルの場所](../ado-api/cursorlocation-property-ado.md)] プロパティを**adUseClient**に設定する必要がある機能である[カスタマイズ](../../guide/remote-data-service/datafactory-customization.md)をサポートします。  
  
 ハンドラーの名前とそのパラメーター (存在する場合) は、コンマ (",") で区切られます。 *文字列*内の任意の場所にセミコロン (";") がある場合、予期しない動作が発生します。 **IDataFactoryHandler**インターフェイスがサポートされていれば、独自のハンドラーを作成できます。  
  
 既定のハンドラーの名前は **Msdfmap です。ハンドラー**とその既定のパラメーターは、 **MSDFMAP.INI**という名前のカスタマイズファイルです。 このプロパティを使用して、サーバー管理者によって作成された代替のカスタマイズファイルを呼び出します。  
  
 **ハンドラー**プロパティを設定する代わりに、 [ConnectionString](../ado-api/connectionstring-property-ado.md)プロパティでハンドラーとパラメーターを指定することもできます。つまり、"**Handler =**_handlername, parameter1, parameter2,...;_" となります。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [Handler プロパティの例 (VB)](./handler-property-example-vb.md)   
 [DataFactory のカスタマイズ](../../guide/remote-data-service/datafactory-customization.md)   
 [DataFactory オブジェクト (RDSServer)](./datafactory-object-rdsserver.md)