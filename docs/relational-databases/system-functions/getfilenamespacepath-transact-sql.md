---
description: GetFileNamespacePath (Transact-SQL)
title: GetFileNamespacePath (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
author: rothja
ms.author: jroth
ms.openlocfilehash: 046ff4071ae4ac45338d45916afeb9d2491d2d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419576"
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable 内のファイルまたはディレクトリの UNC パスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>引数  
 *列名*  
 FileTable 内の VARBINARY (MAX) **file_stream** 列の列名。  
  
 *列名*の値は、有効な列名である必要があります。 式、または別のデータ型の列から変換またはキャストされた値を指定することはできません。  
  
 *is_full_path*  
 相対パスと絶対パスのどちらを返すかを指定する整数式です。 *is_full_path* には、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|データベース レベルのディレクトリ内の相対パスを返します。<br /><br /> これは、既定値です。|  
|**1**|で始まる完全な UNC パスを返し `\\computer_name` ます。|  
  
 *\@オプション*  
 パスのサーバー コンポーネントの書式設定の方法を定義する整数式です。 * \@ オプション*には、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|サーバー名を次のような NetBIOS 形式に変換して返します。<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> これが既定値です。|  
|**1**|次のように、サーバー名を変換せずに返します。<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|次のような、完全なサーバー パスを返します。<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>戻り値の型  
 **nvarchar(max)**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスがフェールオーバークラスターでクラスター化されている場合、このパスの一部として返されるコンピューター名は、クラスター化されたインスタンスの仮想ホスト名になります。  
  
 データベースが Always On 可用性グループに属している場合、 **FileTableRootPath** 関数は、コンピューター名ではなく仮想ネットワーク名 (vnn) を返します。  
  
## <a name="general-remarks"></a>全般的な解説  
 **GetFileNamespacePath**関数が返すパスは、次の形式の論理ディレクトリまたはファイルパスです。  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 この論理パスは、物理的な NTFS パスに直接対応していません。 FILESTREAM のファイルシステムフィルタードライバーと FILESTREAM エージェントによって物理パスに変換されます。 論理パスと物理パスを分離することにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、パスの有効性に影響を与えることなく内部的にデータを再構成できます。  
  
## <a name="best-practices"></a>推奨する運用方法  
 コードとアプリケーションが現在のコンピューターとデータベースから切り離された状態を維持するには、絶対ファイル パスに依存したコードを記述しないでください。 代わりに、次の例に示すように、 **FileTableRootPath** 関数と **GetFileNamespacePath** 関数を一緒に使用して、実行時にファイルの完全なパスを取得します。 既定では、 **GetFileNamespacePath** 関数は、データベースのルート パスの下のファイルの相対パスを返します。  
  
```sql  
USE MyDocumentDatabase;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="remarks"></a>解説  
  
## <a name="examples"></a>例  
 次の例は、 **GetFileNamespacePath** 関数を呼び出して、FileTable 内のファイルまたはディレクトリの UNC パスを取得する方法を示しています。  
  
```  
-- returns the relative path of the form "\MyFileTable\MyDocDirectory\document.docx"  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N'document.docx';  
  
-- returns "\\MyServer\MSSQLSERVER\MyDocumentDatabase\MyFileTable\MyDocDirectory\document.docx"  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="see-also"></a>参照  
 [FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
