---
description: CopyRecord メソッド (ADO)
title: CopyRecord メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 0056d33f1ad07ed48002bb7638acd84a963fb566
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974583"
---
# <a name="copyrecord-method-ado"></a>CopyRecord メソッド (ADO)
[レコード](./record-object-ado.md)によって表されるエンティティを別の場所にコピーします。  
  
## <a name="syntax"></a>構文  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 省略可能。 コピーするエンティティ (ファイルやディレクトリなど) を指定する URL を含む **文字列** 値です。 *Source*を省略した場合、または空の文字列を指定した場合は、現在の[レコード](./record-object-ado.md)によって表されるファイルまたはディレクトリがコピーされます。  
  
 *宛先*  
 省略可能。 *Source*をコピーする場所を指定する URL を含む**文字列**値です。  
  
 *UserName*  
 省略可能。 必要に応じて、*宛先*へのアクセスを承認するユーザー ID を表す**文字列**値です。  
  
 *パスワード*  
 省略可能。 必要に応じて*ユーザー名*を確認するパスワードを含む**文字列**値です。  
  
 *Options*  
 省略可能。 **Adcopyunspecified**の既定値を持つ[CopyRecordOptionsEnum](./copyrecordoptionsenum.md)値。 このメソッドの動作を指定します。  
  
 *非同期*  
 省略可能。 **ブール**値。 **True**の場合、この操作は非同期であることを指定します。  
  
## <a name="return-value"></a>戻り値  
 通常、*変換先*の値を返す**文字列**値。 ただし、返される正確な値はプロバイダーに依存します。  
  
## <a name="remarks"></a>解説  
 *Source*と*Destination*の値を同じにすることはできません。それ以外の場合は、実行時エラーが発生します。 少なくとも1つのサーバー、パス、またはリソース名が異なる必要があります。  
  
 **AdCopyNonRecursive**が指定されていない場合、*ソース*のすべての子 (サブディレクトリなど) が再帰的にコピーされます。 再帰演算では、 *Destination* を *Source*のサブディレクトリにすることはできません。それ以外の場合、操作は完了しません。  
  
 このメソッドは、 **Adcopyoverwrite**が指定されていない限り、 *Destination*が既存のエンティティ (ファイルやディレクトリなど) を識別する場合に失敗します。  
  
> [!IMPORTANT]
>  **Adcopyoverwrite**オプションは慎重に使用してください。 たとえば、ディレクトリにファイルをコピーするときにこのオプションを指定すると、ディレクトリが *削除* され、ファイルに置き換えられます。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](./record-object-ado.md)