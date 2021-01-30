---
description: DELETE TAG コマンド
title: DELETE TAG コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa431c50fcd151d57ce7613586587a1c2342a5c7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181569"
---
# <a name="delete-tag-command"></a>DELETE TAG コマンド
複合インデックス (cdx) ファイルからタグまたはタグを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引数  
 *TagName1* OF *CDXFileName1*[, *TagName2*[of *CDXFileName2*]]...  
 複合インデックスファイルから削除するタグを指定します。 1つの DELETE タグを含む複数のタグを削除するには、タグ名のリストをコンマで区切って追加します。 開いているインデックスファイルに同じ名前のタグが2つ以上存在する場合は、 *Cdxfilename* を含めることで、特定のインデックスファイルからタグを削除できます。  
  
 すべて [ *Cdxfilename*]  
 複合インデックスファイルからすべてのタグを削除します。 現在のテーブルに構造的な複合インデックスファイルがある場合は、すべてのタグがインデックスファイルから削除され、インデックスファイルがディスクから削除されます。また、テーブルのヘッダー内のフラグによって、関連付けられている構造体複合インデックスファイルの存在が削除されていることが示されます。 構造体の複合インデックスファイル以外の開いている複合インデックスファイルからすべてのタグを削除するには、 *Cdxfilename* のすべてのを使用します。  
  
## <a name="remarks"></a>コメント  
 インデックスを使用して作成された複合インデックスファイルには、インデックスエントリに対応するタグが含まれています。 [タグの削除] は、開いている複合インデックスファイルからタグまたはタグを削除するために使用します。 現在の作業領域で開いている複合インデックスファイルからのみ、タグを削除できます。 複合インデックスファイルからすべてのタグを削除すると、そのファイルがディスクから削除されます。  
  
 Visual FoxPro は、最初に構造複合インデックスファイル内のタグを検索します (開いている場合)。 タグが構造的な複合インデックスファイルにない場合、Visual FoxPro は、他の開いている複合インデックスファイル内のタグを検索します。  
  
## <a name="see-also"></a>参照  
 [INDEX コマンド](../../odbc/microsoft/index-command.md)
