---
description: レコードをレコードセットに追加する
title: レコードの追加 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: rothja
ms.author: jroth
ms.openlocfilehash: b39a0920d9816837b6d737df00e6bb4560358356
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033402"
---
# <a name="adding-records-to-a-recordset"></a>レコードをレコードセットに追加する
**AddNew** メソッドを使用して、既存のレコード **セット** 内の新しいレコードを作成して初期化します。 **サポート** メソッドと **カーソルオプションの列挙** 値 **adaddnew** を使用すると、現在の **レコードセット** オブジェクトにレコードを追加できるかどうかを確認できます。

 **AddNew** メソッドを呼び出すと、新しいレコードが現在のレコードになり、 **Update** メソッドを呼び出した後も最新の状態が維持されます。 **Recordset** オブジェクトがブックマークをサポートしていない場合、別のレコードに移動すると、新しいレコードにアクセスできなくなる可能性があります。 したがって、カーソルの種類によっては、新しいレコードにアクセスできるようにするために、 **Requery** メソッドを呼び出す必要がある場合があります。

 現在のレコードを編集しているとき、または新しいレコードを追加しているときに **AddNew** を呼び出した場合、ADO は **Update** メソッドを呼び出して変更を保存し、新しいレコードを作成します。

 このセクションでは、次のトピックを扱います。

-   [AddNew を使用してレコードを追加する](./adding-records-using-addnew.md)

-   [複数のフィールドの追加](./adding-multiple-fields.md)

-   [編集モードの決定](./determining-edit-mode.md)

-   [イミディエイト モードとバッチ モードで AddNew を使用する](./using-addnew-in-immediate-and-batch-modes.md)