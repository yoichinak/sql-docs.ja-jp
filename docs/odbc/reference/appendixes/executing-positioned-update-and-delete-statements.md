---
description: 位置指定更新と Delete ステートメントの実行
title: 位置指定更新と Delete ステートメントの実行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2e11843085f28ceeec965e079bb2942968d15b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466199"
---
# <a name="executing-positioned-update-and-delete-statements"></a>位置指定更新と Delete ステートメントの実行
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 アプリケーションは、 **Sqlfetchscroll**を使用してデータのブロックをフェッチした後、ブロック内のデータを更新または削除できます。 位置指定更新または削除を実行するには、アプリケーションを次のように指定します。  
  
1.  **SQLSetPos**を呼び出して、更新または削除する行にカーソルを置きます。  
  
2.  次の構文を使用して、位置指定の update または delete ステートメントを構築します。  
  
     **UPDATE** *テーブル名の*更新  
  
     **SET** *列識別子* **=** {*expression* &#124; **NULL**} の設定  
  
     [**,** *列識別子* **=** {*式* &#124; **NULL**}]  
  
     *カーソル名***の現在の場所**  
  
     テーブル**からの削除** *-名前***の現在の***カーソル名*  
  
     位置指定の update ステートメントで **SET** 句を構築する最も簡単な方法は、更新する各列に対してパラメーターマーカーを使用し、 **SQLBindParameter** を使用して更新する行の行セットバッファーにバインドすることです。 この場合、パラメーターの C データ型は、行セットバッファーの C データ型と同じになります。  
  
3.  位置指定の update ステートメントを実行する場合は、現在の行の行セットバッファーを更新します。 位置指定更新ステートメントが正常に実行されると、カーソルライブラリによって、現在の行の各列の値がキャッシュにコピーされます。  
  
    > [!CAUTION]  
    >  配置された update ステートメントを実行する前に、アプリケーションが行セットバッファーを正しく更新しないと、ステートメントの実行後にキャッシュ内のデータが正しくなくなります。  
  
4.  カーソルに関連付けられているステートメントとは異なるステートメントを使用して、位置指定の update または delete ステートメントを実行します。  
  
    > [!CAUTION]  
    >  現在の行を識別するためにカーソルライブラリによって構築された **where** 句は、行の識別、別の行の識別、または複数の行の識別に失敗することがあります。 詳細については、「 [検索ステートメントの構築](../../../odbc/reference/appendixes/constructing-searched-statements.md)」を参照してください。  
  
 すべての位置指定の update および delete ステートメントには、カーソル名が必要です。 カーソル名を指定するために、アプリケーションはカーソルが開かれる前に **SQLSetCursorName** を呼び出します。 ドライバーによって生成されたカーソル名を使用するために、アプリケーションはカーソルを開いた後に **Sqlgetcursor name** を呼び出します。  
  
 カーソルライブラリが位置指定の update または delete ステートメントを実行すると、カーソルライブラリによって保持されている状態配列、行セットバッファー、およびキャッシュには、次の表に示す値が含まれます。  
  
|使用されるステートメント|行ステータス配列の値|の値<br /><br /> 行セットバッファー|の値<br /><br /> キャッシュバッファー|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|位置指定更新を行う|SQL_ROW_UPDATED|新しい値 [1]|新しい値 [1]|  
|位置指定削除|SQL_ROW_DELETED|古い値|古い値|  
  
 [1] 配置された update ステートメントを実行する前に、アプリケーションで行セットバッファーの値を更新する必要があります。位置指定の update ステートメントを実行すると、カーソルライブラリによって行セットバッファー内の値がキャッシュにコピーされます。
