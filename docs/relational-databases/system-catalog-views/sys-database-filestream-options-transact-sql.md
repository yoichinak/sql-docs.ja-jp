---
description: database_filestream_options (Transact-sql)
title: database_filestream_options (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c2255471d44962aae91147f7a3e903bfe9a240cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537388"
---
# <a name="sysdatabase_filestream_options-transact-sql"></a>database_filestream_options (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable 内の有効化された FILESTREAM データに対する非トランザクション アクセスのレベルに関する情報を表示します。 SQL Server インスタンス内のデータベースごとに1行のデータを格納します。  
  
 FileTables について詳しくは、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。  
  
  
|Column|種類|説明|  
|------------|----------|-----------------|  
|**database_id**|**int**|データベースの ID です。 この値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意になっています。|  
|**directory_name**|**nvarchar (255)**|すべての FileTable 名前空間のデータベースレベルのディレクトリです。|  
|**non_transacted_access**|**tinyint**|有効になっている FILESTREAM データへの非トランザクションアクセスのレベル。 アクセスのレベルは、 **CREATE database** または **ALTER database** ステートメントの NON_TRANSACTED_ACCESS オプションによって設定されます。<br /><br /> この設定には、次のいずれかの値が含まれます。<br /><br /> 0-有効ではありません。 これが既定値です。 このレベルは、 **NON_TRANSACTED_ACCESS**オプションに値**OFF**を指定することによって設定します。<br /><br /> 1-読み取り専用アクセス。 このレベルは、 **NON_TRANSACTED_ACCESS**オプションの**READ_ONLY**値を指定することによって設定されます。<br /><br /> 3-フルアクセス。 このレベルは、 **NON_TRANSACTED_ACCESS**オプションに値**FULL**を指定することによって設定されます。<br /><br /> 5 - READONLY に移行中。<br /><br /> 6-OFF に移行中|  
|**non_transacted_access_desc**|**nvarchar(60)**|Non_transacted_access で特定された非トランザクションアクセスのレベルの説明。<br /><br /> この設定には、次のいずれかの値が含まれます。<br /><br /> NONE-これは既定値です。<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>参照  
 [FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
