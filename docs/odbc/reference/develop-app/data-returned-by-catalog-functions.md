---
description: カタログ関数によって返されるデータ
title: カタログ関数 | によって返されるデータMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c42319520696060cd52c14c46f968badee27e20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429364"
---
# <a name="data-returned-by-catalog-functions"></a>カタログ関数によって返されるデータ
各カタログ関数は、結果セットとしてデータを返します。 この結果セットは、他の結果セットと同じではありません。 通常は、ドライバーにハードコーディングされているか、データソースのプロシージャに格納されている、定義済みのパラメーター化された **SELECT** ステートメントによって生成されます。 結果セットからデータを取得する方法については、「 [結果セットが作成されましたか](../../../odbc/reference/develop-app/was-a-result-set-created.md)」を参照してください。  
  
 各カタログ関数の結果セットは、その関数の参照エントリに記述されています。 表示される列に加えて、結果セットには、最後に定義された列の後にドライバー固有の列を含めることができます。 これらの列 (存在する場合) については、ドライバーのドキュメントを参照してください。  
  
 アプリケーションでは、ドライバー固有の列を結果セットの末尾に対して相対的にバインドする必要があります。 つまり、ドライバー固有の列の数を、 **Sqlnumresultcols** で取得した最後の列の数として計算する必要があります。これは、必要な列の後に出現する列の数を下回っています。 これにより、今後のバージョンの ODBC またはドライバーで新しい列が結果セットに追加されたときに、アプリケーションを変更する必要がなくなります。 このスキームを機能させるには、ドライバー固有の古い列の前にドライバー固有の新しい列を追加して、結果セットの末尾に対して列番号が変更されないようにする必要があります。  
  
 結果セットで返される識別子は、特殊文字が含まれている場合でも、引用符で囲まれません。 たとえば、識別子の引用符文字 (たとえば、ドライバー固有であり、 **SQLGetInfo**を介して返される) が二重引用符 (") で、買掛金テーブルに Customer Name という名前の列が含まれているとします。 この列の **Sqlcolumns** によって返される行では、TABLE_NAME 列の値は "accounts 買掛" ではなく、"accounts 買掛" となり、COLUMN_NAME 列の値は "customer name" ではなく "customer name" になります。 勘定科目テーブル内の顧客の名前を取得するために、アプリケーションは次の名前を引用します。  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 詳細については、「 [引用符で囲ま](../../../odbc/reference/develop-app/quoted-identifiers.md)れた識別子」を参照してください。  
  
 カタログ関数は、ユーザー名とパスワードに基づいて接続が行われる、SQL に似た承認モデルに基づいており、ユーザーが権限を持っているデータのみが返されます。 このモデルに適合しない個々のファイルのパスワード保護は、ドライバーによって定義されます。  
  
 カタログ関数によって返される結果セットはほとんど更新できません。アプリケーションでは、これらの結果セットのデータを変更することによって、データベースの構造を変更できないようにする必要があります。
