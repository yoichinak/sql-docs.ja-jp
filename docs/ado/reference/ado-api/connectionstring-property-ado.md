---
description: ConnectionString プロパティ (ADO)
title: ConnectionString プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: rothja
ms.author: jroth
ms.openlocfilehash: 2add76a640e89bebe8a941afa5896bb2300750a9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974773"
---
# <a name="connectionstring-property-ado"></a>ConnectionString プロパティ (ADO)
データソースへの接続を確立するために使用される情報を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **文字列**値を設定または返します。  
  
## <a name="remarks"></a>解説  
 **ConnectionString**プロパティを使用して、セミコロンで区切られた一連の*引数* *= value*ステートメントを含む詳細な接続文字列を渡して、データソースを指定します。  
  
 ADO は **ConnectionString** プロパティの5つの引数をサポートしています。その他の引数は、ADO によって処理されることなくプロバイダーに直接渡されます。 ADO でサポートされる引数は次のとおりです。  
  
|引数|説明|  
|--------------|-----------------|  
|*プロバイダー =*|接続に使用するプロバイダーの名前を指定します。|  
|*ファイル名 =*|事前設定された接続情報を含むプロバイダー固有のファイル (永続化されたデータソースオブジェクトなど) の名前を指定します。|  
|*リモートプロバイダー =*|クライアント側接続を開くときに使用するプロバイダーの名前を指定します。 (リモートデータサービスのみ)。|  
|*リモートサーバー =*|クライアント側接続を開くときに使用するサーバーのパス名を指定します。 (リモートデータサービスのみ)。|  
|*URL =*|ファイルやディレクトリなど、リソースを識別する絶対 URL として接続文字列を指定します。|  
  
 **ConnectionString**プロパティを設定し、[接続](./connection-object-ado.md)オブジェクトを開くと、プロバイダーはプロパティの内容を変更する可能性があります。たとえば、ADO によって定義された引数名を特定のプロバイダーの同等の名前にマップします。  
  
 **Connectionstring**プロパティは、 [Open](./open-method-ado-connection.md)メソッドの*connectionstring*引数に使用される値を自動的に継承するため、 **open**メソッド呼び出し中に current **connectionstring**プロパティをオーバーライドできます。  
  
 *ファイル名*引数によって ADO によって関連付けられたプロバイダーが読み込まれるため、*プロバイダー*と*ファイル名*の両方の引数を渡すことはできません。  
  
 **ConnectionString**プロパティは、接続が閉じられている場合は読み取り/書き込み、開いている場合は読み取り専用です。  
  
 **ConnectionString**プロパティの引数の重複は無視されます。 任意の引数の最後のインスタンスが使用されます。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況****ConnectionString**プロパティには、クライアント側の**接続**オブジェクトで使用する場合、*リモートプロバイダー*と*リモートサーバー*のパラメーターのみを含めることができます。  
  
 次の表は、各 Windows オペレーティングシステムの既定の ADO プロバイダーを示しています。  
  
|既定の ADO プロバイダー|Windows オペレーティング システム|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (ソースコードの読みやすさを向上させるには、接続文字列でプロバイダー名を明示的に指定します)。|Windows 2000 (32 ビット)<br /><br /> Windows XP (32 ビット)<br /><br /> Windows 2003 Server (32 ビット)<br /><br /> Windows Vista (32 ビット)<br /><br /> Windows Vista Service Pack 1 以降 (32 ビットおよび64ビット)<br /><br /> Windows Vista 以降の windows バージョン (32 ビットおよび64ビット)|  
|既定値はありません。<br /><br /> ADO アプリケーションが次のオペレーティングシステムで実行され、プロバイダーが明示的に指定されていない場合、ADO は "ADODB" というエラーを返します。接続: プロバイダーが指定されていないため、指定された既定のプロバイダーがありません "|Windows 2000 (64 ビット)<br /><br /> Windows XP (64 ビット)<br /><br /> Windows 2003 Server (64 ビット)<br /><br /> Windows Vista (64 ビット)|  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ConnectionString、ConnectionTimeout、State プロパティの例 (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout、State プロパティの例 (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [付録 A: プロバイダー](../../guide/appendixes/appendix-a-providers.md)