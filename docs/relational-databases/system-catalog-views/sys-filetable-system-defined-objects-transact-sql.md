---
description: sys.filetable_system_defined_objects (Transact-SQL)
title: filetable_system_defined_objects (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a437e9d701870192fc4ea4d5f3352b5bbb063e98
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539648"
---
# <a name="sysfiletable_system_defined_objects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Filetable に関連するシステム定義のオブジェクトの一覧を表示します。 システム定義オブジェクトごとに1行のレコードを格納します。  
  
 FileTable を作成すると、関連するオブジェクト (制約、インデックスなど) が同時に作成されます。 これらのオブジェクトを変更または削除することはできません。これらは、FileTable 自体が削除されると一緒に削除されます。  
  
 FileTables について詳しくは、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。  
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|**object_id**|**int**|FileTable に関連するシステム定義のオブジェクトのオブジェクト ID。<br /><br /> は、 **sys. オブジェクト**内のオブジェクトを参照します。|  
|**parent_object_id**|**int**|親 FileTable のオブジェクト ID。<br /><br /> は、 **sys. オブジェクト**内のオブジェクトを参照します。|  
  
## <a name="see-also"></a>参照  
 [FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
  
  
