---
description: Server プロパティ (RDS)
title: サーバーのプロパティ (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: rothja
ms.author: jroth
ms.openlocfilehash: ad10cbb434c1fda57f684438499bf6e4b885cf9b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724240"
---
# <a name="server-property-rds"></a>Server プロパティ (RDS)
インターネットインフォメーションサービス (IIS) 名と通信プロトコルを示します。  
  
 RDS のオブジェクトタグで、 **サーバー** プロパティをデザイン時に設定でき[ます。DataControl](./datacontrol-object-rds.md) オブジェクト、またはスクリプトコードの実行時に発生します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
 **HTTP**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 実行時の構文  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 実行時の構文  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 実行時の構文  
  
```  
  
DataControl.Server="computername"  
```  
  
 **インプロセス**  
  
 デザイン時の構文  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 実行時の構文  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>パラメーター  
 *awebsrvr*または *computername*  
 サーバーがリモートコンピューター上にある場合は、インターネットまたはイントラネットのパス、またはコンピューター名を含む **文字列** 値。または、サーバーがローカルコンピューター上にある場合は、空の文字列です。  
  
 *port*  
 省略可能。 IIS を実行しているサーバーに接続するために使用されるポート。 ポート番号は Internet Explorer で設定されます ([ **表示** ] メニューの [ **オプション**] をクリックし、[ **接続** ] タブを選択します)。または、IIS で設定します。  
  
 *DataControl*  
 RDS を表すオブジェクト変数です **。DataControl** オブジェクト。  
  
## <a name="remarks"></a>解説  
 サーバーは、RDS が配置されている場所です **。DataControl** 要求 (つまり、クエリまたは更新) が処理されます。 既定では、すべての要求は、 [RDSServer DataFactory](./datafactory-object-rdsserver.md) オブジェクトである Msdfmap によって処理され [ます。ハンドラー](../../guide/remote-data-service/datafactory-customization.md) コンポーネント、および指定されたサーバー上の [MSDFMAP.INI](../../guide/remote-data-service/understanding-the-customization-file.md) ファイル。 古いファイルと新しい **MSDFMAP.INI** ファイルの設定を調整するようにサーバーを変更する場合は注意してください。 非互換性があると、あるサーバーで成功した要求が別のサーバーで失敗する可能性があります。 サーバープロパティが空の文字列 "" に設定されている場合、これらのオブジェクトはローカルコンピューターで使用されます。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [Server プロパティの例 (VBScript)](./server-property-example-vbscript.md)   
 [Connect プロパティ (RDS)](./connect-property-rds.md)   
 [SQL プロパティ](./sql-property.md)   
 [SubmitChanges メソッド (RDS)](./submitchanges-method-rds.md)