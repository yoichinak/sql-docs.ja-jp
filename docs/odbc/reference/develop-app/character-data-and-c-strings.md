---
description: 文字データと C 文字列
title: 文字データと C 文字列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e412976cb297af9a9e38bbc6991647eeab48483b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465924"
---
# <a name="character-data-and-c-strings"></a>文字データと C 文字列
可変長文字データ (列名、動的パラメーター、文字列属性値など) を参照する入力パラメーターには、関連付けられた長さパラメーターがあります。 C での一般的なように、アプリケーションが null 文字で文字列を終了する場合は、文字列の長さ (null 終端文字を除く) または SQL_NTS (Null で終わる文字列) のいずれかを引数として提供します。 負でない長さの引数は、関連付けられている文字列の実際の長さを指定します。 長さの引数を0に設定すると、長さが0の文字列を指定できます。これは、NULL 値とは異なります。 負の値 SQL_NTS は、null 終了文字を検索して文字列の長さを判断するようドライバーに指示します。  
  
 ドライバーからアプリケーションに文字データが返される場合、ドライバーは常に null で終了する必要があります。 これにより、データを文字列または文字配列として処理するかどうかをアプリケーションで選択できます。 アプリケーションバッファーが、すべての文字データを返すのに十分な大きさではない場合、ドライバーは、null 終端文字に必要なバイト数を下回るバッファーのバイト長に切り詰め、切り捨てられたデータを null で終了し、バッファーに格納します。 そのため、アプリケーションは、文字データを取得するために使用されるバッファー内の null 終端文字に対して、常に余分な領域を割り当てる必要があります。 たとえば、50文字のデータを取得するには、51バイトのバッファーが必要です。  
  
 **Sqlputdata**または**SQLGetData**を使用する部分で長い文字データを送信または取得する場合は、アプリケーションとドライバーの両方で特別な注意が必要です。 データが一連の null で終わる文字列として渡される場合、データを再構築する前に、これらの文字列の null 終端文字を削除する必要があります。  
  
 ODBC プログラマの多くは、文字データと C 文字列を混同しています。 これが発生したのは、ODBC 関数を定義するときに C 言語を使用する成果物です。 ODBC ドライバーまたはアプリケーションで別の言語が使用されている場合、ODBC は言語に依存しないため、この混乱が発生する可能性は低くなります。  
  
 C 文字列を使用して文字データを保持する場合、null 終了文字はデータの一部とは見なされず、バイト長の一部としてカウントされません。 たとえば、文字データ "ABC" は、C 文字列 "ABC\0" または文字配列 {' A ', ' B ', ' C '} として保持できます。 データのバイト長は、文字列または文字配列として扱われるかどうかにかかわらず、3になります。  
  
 アプリケーションやドライバーは、通常、文字データを保持するために C 文字列 (null で終わる文字配列) を使用しますが、これを行う必要はありません。 C では、文字データを文字の配列として処理することもできます (null 終端は使用しません)。バイト長は、長さ/インジケーターバッファーで個別に渡されます。  
  
 文字データは null で終わらない配列で保持でき、そのバイト長は個別に渡されるため、文字データに null 文字を埋め込むことができます。 ただし、この場合の ODBC 関数の動作は未定義であり、ドライバーがこれを正しく処理するかどうかはドライバーによって異なります。 そのため、相互運用可能なアプリケーションは、バイナリデータとして埋め込まれた null 文字を含むことができる文字データを常に処理する必要があります。
