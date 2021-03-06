---
description: GetPathLocator (Transact-sql)
title: GetPathLocator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: fbdf65d45374fe9c85adaade284ac6a8aab65dbf
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99207454"
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable 内の指定されたファイルまたはディレクトリのパスロケーター ID 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>引数  
 *filenamespace_path*  
 FileTable 内の名前空間パス。 名前空間のパスの型は **nvarchar (max)** です。  
  
 データベースが Always On 可用性グループに属している場合、 **Getpathlocator** 関数は、仮想ネットワーク名 (vnn) またはコンピューター名を受け取ります。  
  
## <a name="return-type"></a>戻り値の型  
 **hierarchyid**  
  
## <a name="general-remarks"></a>全般的な解説  
 詳しくは、「 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)」をご覧ください。  
  
## <a name="examples"></a>例  
 ファイルサーバーから FileTable にファイルを移行する場合は、 **Getpathlocator** 関数を使用できます。 このシナリオでは、ファイルを FileTable に移動し、各ファイルの元の UNC パスを FileTable UNC パスに置き換えます。 完全な例については、「 [FileTables へのファイルの読み込み](../../relational-databases/blob/load-files-into-filetables.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
