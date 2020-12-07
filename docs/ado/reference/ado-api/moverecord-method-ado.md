---
description: MoveRecord メソッド (ADO)
title: MoveRecord メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: rothja
ms.author: jroth
ms.openlocfilehash: 3425326f9693d7c411f97f04ab5f87bba46578b4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990513"
---
# <a name="moverecord-method-ado"></a>MoveRecord メソッド (ADO)
[レコード](./record-object-ado.md)によって表されるエンティティを別の場所に移動します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 省略可能。 移動する**レコード**を識別する URL を含む**文字列**値です。 *Source*を省略した場合、または空の文字列を指定した場合は、この**レコード**によって表されるオブジェクトが移動されます。 たとえば、 **レコード** がファイルを表している場合、ファイルの内容は *Destination*によって指定された場所に移動されます。  
  
 *宛先*  
 省略可能。 *ソース*を移動する場所を指定する URL を含む**文字列**値です。  
  
 *UserName*  
 省略可能。 必要に応じて、*宛先*へのアクセスを承認するユーザー ID を表す**文字列**値です。  
  
 *パスワード*  
 省略可能。 必要に応じて*ユーザー名*を確認するパスワードを含む**文字列**。  
  
 *Options*  
 省略可能。 既定値が**Admoveunspecified**である[MoveRecordOptionsEnum](./moverecordoptionsenum.md)値。 このメソッドの動作を指定します。  
  
 *非同期*  
 省略可能。 **ブール**値。 **True**の場合、この操作は非同期であることを指定します。  
  
## <a name="return-value"></a>戻り値  
 **文字列**値。 通常、 *Destination* の値が返されます。 ただし、返される正確な値はプロバイダーに依存します。  
  
## <a name="remarks"></a>解説  
 *Source*と*Destination*の値を同じにすることはできません。それ以外の場合は、実行時エラーが発生します。 少なくともサーバー、パス、およびリソース名が異なる必要があります。  
  
 インターネット公開プロバイダーを使用して移動されたファイルの場合、このメソッドは、 *オプション*で指定されていない限り、移動されるファイル内のすべてのハイパーテキストリンクを更新します。 このメソッドは、 **Admoveoverwrite**が指定されていない限り、 *Destination*が既存のオブジェクト (ファイルやディレクトリなど) を識別する場合に失敗します。  
  
> [!NOTE]
>  **Admoveoverwrite**オプションは慎重に使用してください。 たとえば、ディレクトリにファイルを移動するときにこのオプションを指定すると、ディレクトリが削除され、ファイルに置き換えられます。  
  
 [Parenturl](./parenturl-property-ado.md)プロパティなど、**レコード**オブジェクトの特定の属性は、この操作の完了後に更新されません。 レコードを閉じて**レコードオブジェクトのプロパティを更新****し、ファイル**またはディレクトリが移動された場所の URL で再度開いてください。  
  
 この **レコード** が [レコードセット](./recordset-object-ado.md)から取得された場合、移動したファイルまたはディレクトリの新しい場所は、 **レコードセット**に直ちに反映されません。 レコードセットを閉じてから再度開いて、 **レコードセット** を更新します。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Move メソッド (ADO)](./move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (ADO)](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS)](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)