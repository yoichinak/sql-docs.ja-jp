---
description: Open メソッド (ADO Stream)
title: Open メソッド (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: rothja
ms.author: jroth
ms.openlocfilehash: ef760da2bad97cec017c7a58735200be1a14f85d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990323"
---
# <a name="open-method-ado-stream"></a>Open メソッド (ADO Stream)
[ストリーム](./stream-object-ado.md)オブジェクトを開き、バイナリデータまたはテキストデータのストリームを操作します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 省略可能。 **ストリーム**のデータソースを指定する**バリアント**値。 *ソース* には、電子メールやファイルシステムなど、よく知られているツリー構造内の既存のノードを指す絶対 URL 文字列を含めることができます。 Url は、url キーワード ("url =*scheme*://*server* / *フォルダー*") を使用して指定する必要があります。 または、 *ソース* に既に開いている [レコード](./record-object-ado.md) オブジェクトへの参照が含まれている場合もあります。これにより、 **レコード**に関連付けられている既定のストリームが開きます。 *Source*が指定されていない場合、既定では、基になるソースが関連付けられていない**ストリーム**がインスタンス化され、開かれます。 URL スキームとそれに関連付けられているプロバイダーの詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
 *モード*  
 省略可能。 結果の**ストリーム**のアクセスモード (たとえば、読み取り/書き込みまたは読み取り専用) を指定する[connectmodeenum](./connectmodeenum.md)値。 既定値は **Admodeunknown**です。 アクセスモードの詳細については、 [Mode](./mode-property-ado.md) プロパティを参照してください。 *Mode*が指定されていない場合は、ソースオブジェクトによって継承されます。 たとえば、ソース **レコード** が読み取り専用モードで開かれている場合、 **ストリーム** も既定で読み取り専用モードで開かれます。  
  
 *OpenOptions*  
 省略可能。 [Streamopenoptionsenum](./streamopenoptionsenum.md)値。 既定値は **Adopenstreamunspecified**です。  
  
 *UserName*  
 省略可能。 必要に応じて**ストリーム**オブジェクトにアクセスするユーザー id を表す**文字列**値です。  
  
 *パスワード*  
 省略可能。 必要に応じて**ストリーム**オブジェクトにアクセスするパスワードを含む**文字列**値です。  
  
## <a name="remarks"></a>解説  
 **Record**オブジェクトが source パラメーターとして渡された場合、**レコード**オブジェクトへのアクセスは既に使用可能であるため、 *UserID*パラメーターと*Password*パラメーターは使用されません。 同様に、 **record**オブジェクトの[モード](./mode-property-ado.md)が**ストリーム**オブジェクトに転送されます。 *Source*が指定されていない場合、開いている**ストリーム**にはデータが含まれず、[サイズ](./size-property-ado-stream.md)はゼロ (0) になります。 **ストリーム**が閉じられ**たときにストリームに**書き込まれるデータが失われないようにするには、 [CopyTo](./copyto-method-ado.md)メソッドまたは[SaveToFile](./savetofile-method.md)メソッドを使用して**ストリーム**を保存するか、別のメモリ位置に保存します。  
  
 **Adopenstreamfromrecord**の*openoptions*値は、 *Source*パラメーターの内容が既に開いている**レコード**オブジェクトであることを示します。 既定の動作では、 *ソース* は、ファイルなどのツリー構造のノードを直接指す URL として扱われます。 そのノードに関連付けられている既定のストリームが開きます。  
  
 **ストリーム**が開かれていなくても、**ストリーム**のすべての読み取り専用プロパティを読み取ることができます。 **ストリーム**が非同期的に開かれている場合は、**開い**ている操作が完了するまで、後続のすべての操作 ([状態](./state-property-ado.md)のチェックとその他の読み取り専用プロパティを除く) はブロックされます。  
  
 前に説明したオプションに加えて、 *Source*を指定しないことで、ストリームオブジェクトを基になるソースに関連付けずに、メモリ内に **ストリーム** オブジェクトのインスタンスを作成できます。 [書き込み](./write-method.md)または[WriteText](./writetext-method.md)を使用して**ストリーム**にバイナリまたはテキストデータを書き込むことによって、または[LoadFromFile](./loadfromfile-method-ado.md)を使用してファイルからデータを読み込むことによって、ストリームにデータを動的に追加できます。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Open メソッド (ADO Connection)](./open-method-ado-connection.md)   
 [Open メソッド (ADO Record)](./open-method-ado-record.md)   
 [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)   
 [OpenSchema メソッド](./openschema-method.md)   
 [SaveToFile メソッド](./savetofile-method.md)