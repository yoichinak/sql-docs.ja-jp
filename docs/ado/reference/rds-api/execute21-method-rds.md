---
description: Execute21 メソッド (RDS)
title: Execute21 メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
author: rothja
ms.author: jroth
ms.openlocfilehash: fba16dc701ab402084633a7adbdceb4cea273b8d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720725"
---
# <a name="execute21-method-rds"></a>Execute21 メソッド (RDS)
要求を実行し、ado 2.1 で使用する ADO レコードセットを作成します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *文字列*  
 要求が実行のために送信される OLE DB プロバイダーに接続するために使用される文字列。 ハンドラーが handler *文字列*を使用して指定されている場合は、接続文字列を編集または置換できます。  
  
 *HandlerString*  
 文字列は、この実行で使用されるハンドラーを識別します。 文字列には2つの部分が含まれています。 最初の部分には、使用するハンドラーの名前 (ProgID) が含まれています。 文字列の2番目の部分には、ハンドラーに渡される引数が含まれています。 引数文字列の解釈方法は、ハンドラー固有です。 2つの部分は、文字列内のコンマの最初のインスタンスによって区切られます (ただし、引数の文字列には追加のコンマを含めることができます)。 引数は省略可能です。  
  
 *クエリ*  
 接続文字列で指定された OLE DB プロバイダーによってサポートされるコマンド言語のコマンドです。 SQL ベースのプロバイダーでは、コマンドステートメントが含まれている場合があり [!INCLUDE[tsql](../../../includes/tsql-md.md)] ますが、sql 以外のプロバイダー (MSDataShape など) の場合、これはクエリステートメントではない可能性があり [!INCLUDE[tsql](../../../includes/tsql-md.md)] ます。  
  
 また、ハンドラーが使用されている場合 (ハンドラーを使用することを強くお勧めします)、ハンドラーはここで指定された値を変更または置換できます。 たとえば、ハンドラーは通常、 *QueryString* を .ini ファイルのクエリ文字列に置き換えます。 既定では、Msdfmap.ini ファイルが使用されます。  
  
 *lMarshalOptions*  
 返される行セットまたはレコードセットのマーシャリングオプションを設定するために使用します。  
  
 *TableID*  
 VT_EMPTY または VT_BSTR 型のバリアント。 この値が VT_EMPTY 型の場合、この値は無視されます。 VT_BSTR 型の場合、ここで指定した値 **を使用してレコード** セットが作成され、 *QueryString* パラメーターは無視されます。  
  
 *lExecuteOptions*  
 実行オプションのビットマスク。  
  
 1 =*読み取り専用* : **adlockreadonly**を使用してレコードセットを開きます。  
  
 2 =*Nobatch* レコードセットは、 **adlockoptimistic**を使用して開かれます。  
  
 4 =*Allparaminfosupplied* 元は、すべてのパラメーターのパラメーター情報が *pparameters*に指定されていることを保証します。  
  
 8 = クエリの*GetInfo* パラメーター情報は OLE DB プロバイダーから取得され、 *pparameters* パラメーターに返されます。 クエリは実行されず、レコードセットは返されません。  
  
 16 = GetHiddenColumns レコードセットは **Adlockbatchoptimistic** を使用して開かれ、すべての非表示の列がレコードセットに含まれます。  
  
 *ReadOnly*、 *Nobatch* 、 *GetHiddenColumns*は相互に排他的なオプションですが、複数のオプションを設定することはできません。 複数のオプションが設定されている場合、 *GetHiddenColumns* は他のすべてのオプションよりも優先され、その後に *ReadOnly*が適用されます。 オプションが指定されていない場合、既定では、レコードセットは **Adlockbatchoptimistic** を使用して開かれますが、非表示の列はレコードセットに含まれません。  
  
 *pParameters*  
 パラメーター定義のセーフ配列を含むバリアント。 [ *GetInfo* ] オプションが *lexecuteoptions*で指定されている場合、このパラメーターを使用して、OLE DB プロバイダーから取得したパラメーター定義が返されます。 それ以外の場合、このパラメーターは空になることがあります。  
  
## <a name="remarks"></a>解説  
 *ハンドラー文字列*パラメーターは null にすることができます。 この場合の動作は、RDS サーバーの構成方法によって異なります。 "MSDFMAP. handler" のハンドラー文字列は、Microsoft 提供のハンドラー (Msdfmap.dll) を使用する必要があることを示します。 "sample.ini" のハンドラー文字列は、Msdfmap.dll ハンドラーを使用する必要があり、引数 "sample.ini" をハンドラーに渡す必要があることを示します。 MSDFMAP.dll は、sample.ini を使用して接続とクエリ文字列を確認する方向として引数を解釈します。  
  
> [!NOTE]
>  **Execute21**メソッドは、 [EXECUTE メソッド (RDS)](./execute-method-rds.md)の1つのバージョンです。 **Execute**メソッドを使用して ADO 2.1 と通信する必要がある場合は、代わりに**Execute21**メソッドを呼び出すことができます。 ADO 2.5 以降の **Execute** メソッドの機能は、ado 2.1 で同じメソッドに対して提供される機能のスーパーセットです。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](./datafactory-object-rdsserver.md)