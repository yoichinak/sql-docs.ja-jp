---
description: Microsoft OLE DB 永続化プロバイダー (ADO サービスプロバイダー)
title: Microsoft OLE DB 永続化プロバイダー (ADO サービスプロバイダー) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b9cfce1762ef678e544a2148df4a4d79074e152
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991073"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 永続化プロバイダーの概要
Microsoft OLE DB 永続化プロバイダーを使用すると、 [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトをファイルに保存し、後でその **レコードセット** オブジェクトをファイルから復元できます。 スキーマ情報、データ、および保留中の変更は保持されます。

 この **レコードセット** は、独自の高度なデータテーブルグラム (ADTG) 形式または open 拡張マークアップ言語 (XML) 形式のいずれかで保存できます。

## <a name="provider-keyword"></a>Provider キーワード
 このプロバイダーを呼び出すには、接続文字列に次のキーワードと値を指定します。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>エラー
 このプロバイダーによって発行された次のエラーは、アプリケーションで検出できます。

|定数|説明|
|--------------|-----------------|
|E_BADSTREAM|開かれたファイルの形式が有効ではありません (つまり、形式が ADTG または XML ではありません)。|
|E_CANTPERSISTROWSET|保存された **レコードセット** オブジェクトには、保存されないようにする特性があります。|

## <a name="remarks"></a>解説
 Microsoft OLE DB 永続化プロバイダーは動的プロパティを公開しません。

 現時点では、パラメーター化された階層的な **レコードセット** オブジェクトのみを保存することはできません。

 **レコードセット**オブジェクトを永続的に格納する方法の詳細については、「[レコードセット永続](../data/more-about-recordset-persistence.md)化」を参照してください。

 ストリームを使用して**レコードセット**を開くときに、 **Open**メソッドの*Source*パラメーター以外にパラメーターを指定しないようにする必要があります。

## <a name="see-also"></a>参照
[Microsoft OLE DB 永続化プロバイダー (ADO サービスプロバイダー)]()