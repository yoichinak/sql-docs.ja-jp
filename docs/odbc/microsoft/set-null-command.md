---
description: SET NULL コマンド
title: SET NULL Command |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a190c913b2f8cc9d7a111a0c95d0408de2c1c6c2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208604"
---
# <a name="set-null-command"></a>SET NULL コマンド
ALTER TABLE-SQL、CREATE TABLE SQL、および INSERT-SQL コマンドで null 値をどのようにサポートするかを決定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 (ドライバーの既定値は、Visual FoxPro の既定値は OFF です)。ALTER TABLE および CREATE TABLE で作成されたテーブル内のすべての列で null 値を許容することを指定します。 列の定義に NOT NULL 句を含めることにより、テーブル内の列の null 値のサポートを無効にできます。  
  
 また、insert-sql が、INSERT-SQL VALUE 句に含まれていない列に null 値を挿入することを指定します。 INSERT-SQL では、null 値を許容する列にのみ null 値が挿入されます。  
  
 OFF  
 ALTER TABLE および CREATE TABLE で作成されたテーブル内のすべての列で null 値を許容しないように指定します。 列の定義に NULL 句を含めることによって、ALTER TABLE と CREATE TABLE の列に null 値のサポートを指定できます。  
  
 また、insert-SQL が、INSERT-SQL VALUE 句に含まれていない列に空白の値を挿入することを指定します。  
  
## <a name="remarks"></a>コメント  
 SET NULL は、ALTER TABLE、CREATE TABLE、および INSERT によって null 値がサポートされる方法にのみ影響します。 他のコマンドは、SET NULL によって影響を受けません。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE-SQL コマンド](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE-SQL コマンド](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL コマンド](../../odbc/microsoft/insert-sql-command.md)
