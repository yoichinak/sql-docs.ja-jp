---
description: Visual C++ でエラーを処理する
title: Visual C++ でのエラーの処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: rothja
ms.author: jroth
ms.openlocfilehash: 61435c9d66800704e962cd4a399c87e72f6558c8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037372"
---
# <a name="handling-errors-in-visual-c"></a>Visual C++ でエラーを処理する
COM では、ほとんどの操作は、関数が正常に完了したかどうかを示す HRESULT リターンコードを返します。 #Import ディレクティブは、"生の" メソッドまたはプロパティごとにラッパーコードを生成し、返された HRESULT を確認します。 HRESULT が失敗を示している場合、ラッパーコードは、HRESULT リターンコードを引数として _com_issue_errorex () を呼び出すことによって COM エラーをスローします。 COM エラーオブジェクトは、 **try-catch** ブロックでキャッチできます。 (効率を上げるために、_com_error オブジェクトへの参照をキャッチします。)  
  
 これらは ADO エラーであり、ADO 操作が失敗した場合に発生します。 基になるプロバイダーから返されたエラーは、**接続** オブジェクトの **エラー** コレクションに **エラー** オブジェクトとして表示されます。  
  
 #Import ディレクティブは、ADO .dll で宣言されたメソッドおよびプロパティに対してのみ、エラー処理ルーチンを作成します。 ただし、独自のエラーチェックマクロまたはインライン関数を記述することで、この同じエラー処理機構を利用できます。 例については、®拡張機能の Visual C++ に関するトピックを参照してください。
