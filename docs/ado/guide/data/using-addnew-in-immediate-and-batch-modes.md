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
ms.openlocfilehash: 689b8fbc6c8bb9446adfeb9fec98d53d59b28917
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979053"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>イミディエイト モードとバッチ モードで AddNew を使用する
**AddNew**メソッドの動作は、**レコードセット**オブジェクトの更新モードと、 *FieldList*引数と*Values*引数を渡すかどうかによって異なります。  
  
 **Update**メソッドを呼び出した後、プロバイダーが基になるデータソースに変更を書き込む即時更新モードでは、引数を指定せずに**AddNew**メソッドを呼び出すと、 **EditMode**プロパティが adEditAdd に設定され**ます。** プロバイダーは、フィールド値の変更をローカルにキャッシュします。 **Update**メソッドを呼び出すと、新しいレコードがデータベースにポストされ、 **EditMode**プロパティが adEditNone にリセットされ**ます。** *FieldList*引数と*Values*引数を渡すと、ADO はすぐに新しいレコードをデータベースにポストします (**更新**呼び出しは必要ありません)。**EditMode**プロパティ値は変更されません (**adEditNone**)。  
  
 バッチ更新モードでは、引数を指定せずに **AddNew** メソッドを呼び出すと、 **EditMode** プロパティが **adEditAdd**に設定されます。 プロバイダーは、フィールド値の変更をローカルにキャッシュします。 **Update**メソッドを呼び出すと、新しいレコードが現在の**レコードセット**に追加され、 **EditMode**プロパティが**adEditNone**にリセットされます。ただし、プロバイダーは、 **UpdateBatch**メソッドを呼び出すまで、基になるデータベースに変更を送信しません。 *FieldList*引数と*Values*引数を渡すと、ADO はキャッシュ内のストレージ用に新しいレコードをプロバイダーに送信します。新しいレコードを基になるデータベースにポストするには、 **UpdateBatch**メソッドを呼び出す必要があります。 **Update**と**UpdateBatch**の詳細については、「[データの更新と永続](../../../ado/guide/data/updating-and-persisting-data.md)化」を参照してください。
