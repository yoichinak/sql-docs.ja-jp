---
description: INSERT - SQL コマンド
title: INSERT-SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92c4b2068149164716d52fd3693e56164ab788ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449504"
---
# <a name="insert---sql-command"></a>INSERT - SQL コマンド
指定されたフィールド値を含むテーブルの末尾にレコードを追加します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブな Visual FoxPro 言語構文がサポートされています。 ドライバー固有の情報については、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>引数  
 INSERT INTO *dbf_name*  
 新しいレコードを追加するテーブルの名前を指定します。 *dbf_name* にはパスを含めることができ、名前式を使用できます。  
  
 指定したテーブルが開いていない場合は、新しい作業領域で排他的に開かれ、新しいレコードがテーブルに追加されます。 新しい作業領域が選択されていません。現在の作業領域は選択されたままです。  
  
 指定したテーブルが開いている場合は、INSERT によって新しいレコードがテーブルに追加されます。 テーブルが現在の作業領域以外の作業領域で開かれている場合は、レコードの追加後に選択されません。現在の作業領域は選択されたままです。  
  
 [( *fname1*[, *fname2*[,...]])]  
 新しいレコードに、値が挿入されるフィールドの名前を指定します。  
  
 値 ( *eExpression1*[, *eExpression2*[,...]])  
 新しいレコードに挿入されるフィールド値を指定します。 フィールド名を省略した場合は、テーブル構造によって定義された順序でフィールド値を指定する必要があります。  
  
## <a name="remarks"></a>解説  
 新しいレコードには、VALUES 句に一覧表示されたデータが含まれています。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションが ODBC SQL ステートメントの INSERT をデータソースに送信すると、Visual FoxPro ODBC ドライバーは、コマンドを変換せずに Visual FoxProINSERT コマンドに変換します。  
  
## <a name="see-also"></a>参照  
 [CREATE TABLE-SQL コマンド](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL コマンド](../../odbc/microsoft/select-sql-command.md)
