---
description: URL プロパティ (RDS)
title: URL プロパティ (RDS) |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: rothja
ms.author: jroth
ms.openlocfilehash: 0d693aab0c01e1a65715597c6f8905569aebbcae
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724674"
---
# <a name="url-property-rds"></a>URL プロパティ (RDS)
相対 URL または絶対 URL を含む文字列を示します。  
  
 **URL**プロパティを設定するには、デザイン時に[DATACONTROL](./datacontrol-object-rds.md)オブジェクトのオブジェクトタグを使用するか、スクリプトコードの実行時に設定します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>パラメーター  
 *サーバー*  
 有効な URL を含む **文字列** 値です。  
  
 *DataControl*  
 **DataControl**オブジェクトを表すオブジェクト変数です。  
  
## <a name="remarks"></a>解説  
 通常、URL は、 [レコードセット](../ado-api/recordset-object-ado.md)を生成して返すことができる Active Server ページ (.asp) ファイルを識別します。 そのため、ユーザーは、サーバー側の[DataFactory](./datafactory-object-rdsserver.md)オブジェクトを呼び出さなくても**レコードセット**を取得できます。また、カスタムビジネスオブジェクトをプログラムすることもできます。  
  
 **Url**プロパティが設定されている場合、 [SubmitChanges](./submitchanges-method-rds.md)は url で指定された場所に変更を送信します。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [URL プロパティの例 (VBScript)](./url-property-example-vbscript.md)