---
description: SET BLOCKSIZE コマンド
title: SET BLOCKSIZE コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f1777b62d279db78154383a3f328591776c0a5c5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208656"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE コマンド
メモフィールドを格納するためのディスク領域の割り当て方法を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>引数  
 *nBytes*  
 メモフィールドのディスク領域を割り当てるブロックサイズを指定します。 *Nbytes* が0の場合、ディスク領域は1バイト (1 バイトのブロック) で割り当てられます。 *Nbytes* が 1 ~ 32 の整数である場合、ディスク領域は *nbytes* バイトに512を掛けたブロックで割り当てられます。 *Nbytes* が32より大きい場合は、 *nbytes* バイトのブロックにディスク領域が割り当てられます。 32より大きいブロックサイズの値を指定した場合は、大量のディスク領域を節約できます。  
  
## <a name="remarks"></a>コメント  
 SET BLOCKSIZE の既定値は64です。 ファイルの作成後にブロックサイズを別の値にリセットするには、新しい値に設定してから、COPY を使用して新しいテーブルを作成します。 新しいテーブルには、指定されたブロックサイズがあります。
