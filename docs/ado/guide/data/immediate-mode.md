---
title: イミディエイトモード |Microsoft Docs
description: LockType プロパティが adLockOptimistic または Adlockoptimistic に設定されている場合に有効な、イミディエイトモードについて説明します。
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: rothja
ms.author: jroth
ms.openlocfilehash: 9838a86c66abba0a73014a08a32e8e24d18849af
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037312"
---
# <a name="immediate-mode"></a>イミディエイト モード
イミディエイトモードは、 **LockType** プロパティが **adlockoptimistic** または **adlockoptimistic** に設定されている場合に有効です。 イミディエイトモードでは、 **Update** メソッドを呼び出すことによって行の作業が完了するとすぐに、レコードへの変更がデータソースに反映されます。  
  
## <a name="calling-update"></a>更新を呼び出しています  
 **更新** メソッドを呼び出す前に追加または編集しているレコードから移動すると、ADO は自動的に **update** を呼び出して変更を保存します。 現在のレコードに対して行われた変更を取り消す場合や、新しく追加したレコードを破棄する場合は、ナビゲーションの前に **CancelUpdate** メソッドを呼び出す必要があります。  
  
 **Update** メソッドを呼び出した後、現在のレコードは最新のままです。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 **CancelUpdate** メソッドを使用して、現在の行に対して行われた変更を取り消すか、新しく追加した行を破棄します。 **Update** メソッドを呼び出した後、現在の行または新しい行への変更を取り消すことはできません。ただし、変更がトランザクションの一部である場合は、 **RollbackTrans** メソッドまたはバッチ更新の一部を使用してロールバックすることができます。 バッチ更新の場合は、 **CancelUpdate** または **CancelBatch** メソッドを使用して **更新** を取り消すことができます。  
  
 **CancelUpdate** メソッドを呼び出すときに新しい行を追加する場合、現在の行は、 **AddNew** 呼び出しの前の現在の行になります。  
  
 現在の行を変更していないか、新しい行を追加していない場合は、 **CancelUpdate** メソッドを呼び出すとエラーが生成されます。
