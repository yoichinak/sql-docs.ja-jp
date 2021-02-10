---
description: 失敗した更新の処理
title: 失敗した更新プログラムの処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: rothja
ms.author: jroth
ms.openlocfilehash: a5ce736c8dd24f2398d7c8c374be260080c32e11
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037642"
---
# <a name="dealing-with-failed-updates"></a>失敗した更新の処理
更新がエラーで終了した場合、エラーの解決方法は、エラーの性質と重大度、およびアプリケーションのロジックによって異なります。 ただし、データベースが他のユーザーと共有されている場合、一般的なエラーとして、他のユーザーがフィールドを変更することがあります。 この種類のエラーは競合と呼ばれます。 ADO はこの状況を検出し、エラーを報告します。  
  
## <a name="remarks"></a>解説  
 更新エラーが発生した場合は、エラー処理ルーチンでトラップされます。 競合する行だけが表示されるように、Adfilter衝突 Tingrecords 定数でレコードセットをフィルター処理します。 この例では、エラー解決方法は、作成者の姓と名 (au_fname と au_lname) を出力するだけです。  
  
 更新の競合についてユーザーに通知するコードは、次のようになります。  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>参照  
 [バッチ モード](./batch-mode.md)