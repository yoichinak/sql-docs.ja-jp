---
description: データの更新と保持
title: データの更新と保持 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: rothja
ms.author: jroth
ms.openlocfilehash: 05ca0196ef59df1f67d5f65f3abc52133b81869a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979173"
---
# <a name="updating-and-persisting-data"></a>データの更新と保持
前の章では、ADO を使用してデータソース内のデータを取得する方法、データ内を移動する方法、およびデータを編集する方法について説明しました。 もちろん、アプリケーションの目的が、ユーザーがデータに変更を加えることができるようにする場合は、それらの変更を保存する方法を理解する必要があります。 保存方法を使用して **レコードセット** の変更をファイルに **保存** するか、 **Update** または **UpdateBatch** メソッドを使用してストレージのデータソースに変更を戻すことができます。  
  
 前の章では、 **レコードセット**の複数行のデータを変更しました。 ADO では、データ行の追加、削除、および変更に関連する2つの基本的な概念がサポートされています。  
  
 最初の概念は、変更がすぐに **レコードセット**に反映されないことです。代わりに、内部 *コピーバッファー*に対して行われます。 変更が不要な場合は、コピーバッファーの変更が破棄されます。 変更を保持する場合は、コピーバッファーの変更が **レコードセット**に適用されます。  
  
 2つ目の概念は、行全体での作業を宣言した直後 (つまり *イミディエイト* モード) に変更がデータソースに反映されるか、または一連の行に対するすべての変更が、セットの完了 (つまり *バッチ* モード) の作業を宣言するまで収集されることです。 **LockType**プロパティは、基になるデータソースに変更が加えられるタイミングを決定します。 **Adlockoptimistic** または **adlockoptimistic** はイミディエイトモードを指定し、 **adlockbatchオプティミスティック** はバッチモードを指定します。 [ **カーソルの場所** ] プロパティは、使用可能な **LockType** 設定に影響を与える可能性があります。 たとえば、[**カーソルの場所**] プロパティが**adUseClient**に設定されている場合、 **adlockpessimistic**設定はサポートされません。  
  
 イミディエイトモードでは、 **Update** メソッドを呼び出すたびに、変更がデータソースに反映されます。 バッチモードでは、現在の行の位置の **更新** または移動を呼び出すたびに、コピーバッファーへの変更が保存されますが、変更内容がデータソースに反映されるのは、 **UpdateBatch** メソッドだけです。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [データの更新](../../../ado/guide/data/updating-data.md)  
  
-   [データの保持](../../../ado/guide/data/persisting-data.md)
