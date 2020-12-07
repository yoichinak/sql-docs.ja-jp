---
description: ConvertToString メソッド (RDS)
title: ConvertToString メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: rothja
ms.author: jroth
ms.openlocfilehash: ec87fd4bc4495874aae88b3051081e30dda9bbb9
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722428"
---
# <a name="converttostring-method-rds"></a>ConvertToString メソッド (RDS)
レコードセットを、レコードセットデータを表す MIME [文字列に変換](../ado-api/recordset-object-ado.md) します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataFactory*  
 [RDSServer DataFactory](./datafactory-object-rdsserver.md)オブジェクトを表すオブジェクト変数です。  
  
 *レコードセット*  
 **レコードセット**オブジェクトを表すオブジェクト変数です。  
  
## <a name="remarks"></a>解説  
 .Asp ファイルの場合は、 **Converttostring** を使用して、サーバー上で生成された HTML ページに **レコードセット** を埋め込み、クライアントコンピューターに転送します。  
  
 **Converttostring** は、まず **レコードセット** をカーソルサービステーブルに読み込み、次に MIME 形式でストリームを生成します。  
  
 クライアントでは、リモートデータサービスは MIME 文字列を完全に機能する **レコードセット**に変換できます。 行ごとに1024バイト以下のデータを400行未満で処理する場合に適しています。 BLOB データのストリーミングと HTTP 経由の大きな結果セットには使用しないでください。 文字列に対してワイヤ圧縮は実行されません。したがって、リモートデータサービスによって定義され、ネイティブトランスポートプロトコル形式としてデプロイされたワイヤ最適化 tablegram 形式と比較すると、非常に大きなデータセットが HTTP 経由で転送されるのにかなりの時間がかかります。  
  
> [!NOTE]
>  Active Server のページを使用して、生成された MIME 文字列をクライアントの HTML ページに埋め込む場合は、バージョン2.0 より前のバージョンの VBScript では、文字列のサイズが32K に制限されていることに注意してください。 この制限を超えた場合は、エラーが返されます。 .Asp ファイルを使用して MIME を埋め込む場合は、クエリスコープを比較的小さいままにします。 この問題を解決するには、Microsoft Windows スクリプトテクノロジの Web サイトから最新バージョンの VBScript をダウンロードします。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>参照  
 [ConvertToString メソッドの例 (VB)](../ado-api/converttostring-method-example-vb.md)   
 [ConvertToString メソッドの例 (VBScript)](./converttostring-method-example-vbscript.md)