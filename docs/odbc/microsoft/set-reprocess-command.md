---
description: SET REPROCESS コマンド
title: 再処理コマンドの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8daeebd38f295d437dc02c1c34126c30f6426b68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421826"
---
# <a name="set-reprocess-command"></a>SET REPROCESS コマンド
ロックの試行が失敗した後、ファイルまたはレコードをロックする回数または長さを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引数  
 *N 試行回数*[秒]  
 最初の試行が失敗した後に、レコードまたはファイルのロックを試行する回数または秒数を指定します。 既定値は0です。最大値は32000です。  
  
 SECONDS Visual FoxPro が *Nattempts* 秒間、ファイルまたはレコードをロックしようとすることを指定します。 *Nattempts*が0より大きい場合にのみ使用できます。  
  
 たとえば、 *Nattempts* が30の場合、Visual FoxPro はレコードまたはファイルを最大30回ロックしようとします。 また、秒数を指定した場合 (再処理を30秒に設定した場合)、Visual FoxPro は、最大30秒間、レコードまたはファイルのロックを継続的に試みます。  
  
 ON ERROR ルーチンが有効で、レコードまたはファイルをロックするコマンドの試行が失敗した場合は、ON ERROR ルーチンが実行されます。 ただし、関数がロックを試みると、ON ERROR ルーチンは実行されず、関数は False (を返します。F.)。  
  
 ON ERROR ルーチンが有効でない場合、コマンドがレコードまたはファイルをロックしようとしたときに、ロックを配置できない場合は、エラーが生成されます。 関数がロックを配置しようとすると、警告は表示されず、関数は False (を返します。F.)。  
  
 *Nattempts*が 0 (既定値) で、レコードまたはファイルをロックしようとするコマンドまたは関数を発行した場合、Visual FoxPro はレコードまたはファイルを無期限にロックしようとします。 待機中にレコードまたはファイルがロックに使用できるようになると、ロックが適用され、システムメッセージがクリアされます。 関数がロックを配置しようとした場合、関数は True (を返します。T.)。  
  
 ON ERROR ルーチンが有効になっていて、コマンドがレコードまたはファイルをロックしようとしている場合、レコードまたはファイルをロックするための追加の試行よりも、ON ERROR ルーチンの方が優先されます。 ON ERROR ルーチンが直ちに実行されます。 Visual FoxPro は、追加のレコードまたはファイルロックを試行せず、システムメッセージを表示しません。  
  
 *Nattempts*が1の場合、Visual FoxPro はレコードまたはファイルを無期限にロックしようとし、ON ERROR ルーチンは実行されません。  
  
 ロックしようとしているレコードまたはファイルの別のユーザーによってロックが設定されている場合は、ユーザーがロックを解放するまで待機する必要があります。  
  
 自動に  
 Visual FoxPro がレコードまたはファイルを無期限にロックしようとすることを指定します。 (再処理を-2 に設定することは、同等のコマンドです)。  
  
## <a name="remarks"></a>解説  
 レコードまたはファイルを初めてロックしようとしても、常に成功するわけではありません。 多くの場合、レコードまたはファイルは、ネットワーク上の別のユーザーによってロックされています。 設定の再処理によって、最初の試行が失敗したときに、Visual FoxPro がレコードまたはファイルのロックをさらに試みるかどうかが決定されます。 追加の試行回数、または試行の実行時間を指定できます。 ON ERROR ルーチンは、ロックの試行が失敗した方法に影響します。
