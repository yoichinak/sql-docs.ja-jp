---
description: 記述子
title: 記述子 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae01f093ef1b67f1326f8aa7719b74100fcba462
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429334"
---
# <a name="descriptors"></a>記述子
記述子ハンドルは、列または動的パラメーターに関する情報を保持するデータ構造を参照します。  
  
 列およびパラメーターデータを操作する ODBC 関数は、記述子フィールドを暗黙的に設定および取得します。 たとえば、 **SQLBindCol** を呼び出して列データをバインドすると、バインドを完全に記述する記述子フィールドが設定されます。 列データを記述するために **Sqlcolattribute** を呼び出すと、記述子フィールドに格納されているデータが返されます。  
  
 ODBC 関数を呼び出すアプリケーションは、記述子を使用する必要はありません。 データベース操作では、アプリケーションが記述子への直接アクセスを取得する必要はありません。 ただし、アプリケーションによっては、記述子への直接アクセスを取得すると、多くの操作が効率化されます。 たとえば、記述子への直接アクセスでは、列データを再バインドする方法が提供されますが、 **SQLBindCol** を再度呼び出すよりも効率的な場合があります。  
  
> [!NOTE]  
>  記述子の物理的表現が定義されていません。 アプリケーションは、記述子ハンドルで ODBC 関数を呼び出すことによってフィールドを操作することによってのみ、記述子への直接アクセスを取得します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [記述子の種類](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [記述子フィールド](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [記述子の割り当てと解放](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [記述子フィールドの取得と設定](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
