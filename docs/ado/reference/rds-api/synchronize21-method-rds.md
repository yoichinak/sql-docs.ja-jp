---
description: Synchronize21 メソッド (RDS)
title: Synchronize21 メソッド (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: 46d0d13fa6e735b7763a35186beff59f293cc278
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724700"
---
# <a name="synchronize21-method-rds"></a>Synchronize21 メソッド (RDS)
指定したレコードセットを、ADO 2.1 で使用する接続文字列で指定されたデータベースと同期します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *文字列*  
 要求が送信される OLE DB プロバイダーに接続するために使用される文字列。 ハンドラーが使用されている場合、ハンドラーは接続文字列を編集または置換できます。  
  
 *HandlerString*  
 文字列は、この実行で使用されるハンドラーを識別します。 文字列には2つの部分が含まれています。 最初の部分には、使用するハンドラーの名前 (ProgID) が含まれています。 文字列の2番目の部分には、ハンドラーに渡される引数が含まれています。 引数文字列の解釈方法は、ハンドラー固有です。 2つの部分は、文字列内のコンマの最初のインスタンスによって区切られます。 Arguments 文字列には、追加のコンマを含めることができます。 引数は省略可能です。  
  
 *lSynchronizeOptions*  
 同期オプションのビットマスク。  
  
 1 = データベースに対する*Updatetransact* 更新は、トランザクションでラップされます。 更新のいずれかが失敗すると、トランザクションは中止されます。  
  
 2 =*Refreshwithupdate* では、 *更新* も *refreshconflicts* も設定されていない場合、行の状態が返されます。  
  
 4 = レコードセットを*更新* するには、データベースの現在のデータを使用して更新します。 保留中の更新はデータベースにプッシュされません。 このビットが設定されていない場合、レコードセットは更新されず、保留中の更新はデータベースにプッシュされます。  
  
 8 =*Refreshconflicts* は、保留中の変更があるすべての行を更新できません。 更新に失敗した行は、データベースの現在のデータで更新されます。  
  
 *ppRecordset*  
 同期されるレコードセットへのポインターへのポインター。  
  
 *pStatusArray*  
 Synchronize の影響を受ける行の状態の安全な配列を返すために使用されるバリアント。 *Refreshwithupdate*、 *Refresh* 、および*refreshconflicts*のいずれの同期オプションも設定されていない場合は設定されません。  
  
## <a name="remarks"></a>解説  
 *ハンドラー文字列*パラメーターには null を指定できます。 この場合の動作は、RDS サーバーがどのように構成されているかによって異なります。 "MSDFMAP. handler" のハンドラー文字列は、Microsoft 提供のハンドラー (Msdfmap.dll) を使用する必要があることを示します。 "sample.ini" のハンドラー文字列は、Msdfmap.dll ハンドラーを使用する必要があり、引数 "sample.ini" をハンドラーに渡す必要があることを示します。 Msdfmap.dll は、sample.ini を使用して接続とクエリ文字列を確認する方向として引数を解釈します。  
  
> [!NOTE]
>  **Synchronize21**メソッドは、単に[同期メソッド (RDS)](./synchronize-method-rds.md)の1つのバージョンです。 **Synchronize**メソッドを使用して ADO 2.1 と通信する必要がある場合は、代わりに**Synchronize21**メソッドを呼び出すことができます。 ADO 2.5 以降の **Synchronize** メソッドの機能は、ado 2.1 で同じメソッドに対して提供される機能のスーパーセットです。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](./datafactory-object-rdsserver.md)