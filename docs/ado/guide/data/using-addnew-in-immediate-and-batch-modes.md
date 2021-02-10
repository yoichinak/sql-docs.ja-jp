---
title: イミディエイトモードとバッチモードで AddNew を使用する |Microsoft Docs
description: イミディエイトモードとバッチモードで AddNew を使用する方法について説明します。
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
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: rothja
ms.author: jroth
ms.openlocfilehash: b68d4870c7c256495bb16b7bfba7176d60445ea7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100036792"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>イミディエイト モードとバッチ モードで AddNew を使用する
**AddNew** メソッドの動作は、**レコードセット** オブジェクトの更新モードと、 *FieldList* 引数と *Values* 引数を渡すかどうかによって異なります。  
  
 **Update** メソッドを呼び出した後、プロバイダーが基になるデータソースに変更を書き込む即時更新モードでは、引数を指定せずに **AddNew** メソッドを呼び出すと、 **EditMode** プロパティが adEditAdd に設定され **ます。** プロバイダーは、フィールド値の変更をローカルにキャッシュします。 **Update** メソッドを呼び出すと、新しいレコードがデータベースにポストされ、 **EditMode** プロパティが adEditNone にリセットされ **ます。** *FieldList* 引数と *Values* 引数を渡すと、ADO はすぐに新しいレコードをデータベースにポストします (**更新** 呼び出しは必要ありません)。**EditMode** プロパティ値は変更されません (**adEditNone**)。  
  
 バッチ更新モードでは、引数を指定せずに **AddNew** メソッドを呼び出すと、 **EditMode** プロパティが **adEditAdd** に設定されます。 プロバイダーは、フィールド値の変更をローカルにキャッシュします。 **Update** メソッドを呼び出すと、新しいレコードが現在の **レコードセット** に追加され、 **EditMode** プロパティが **adEditNone** にリセットされます。ただし、プロバイダーは、 **UpdateBatch** メソッドを呼び出すまで、基になるデータベースに変更を送信しません。 *FieldList* 引数と *Values* 引数を渡すと、ADO はキャッシュ内のストレージ用に新しいレコードをプロバイダーに送信します。新しいレコードを基になるデータベースにポストするには、 **UpdateBatch** メソッドを呼び出す必要があります。 **Update** と **UpdateBatch** の詳細については、「[データの更新と永続](../../../ado/guide/data/updating-and-persisting-data.md)化」を参照してください。
