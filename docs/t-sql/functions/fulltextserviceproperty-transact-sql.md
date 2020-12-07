---
description: FULLTEXTSERVICEPROPERTY (Transact-SQL)
title: FULLTEXTSERVICEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXTSERVICEPROPERTY_TSQL
- FULLTEXTSERVICEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- FULLTEXTSERVICEPROPERTY function
- services [SQL Server], full-text search properties
- test
ms.assetid: b7dcacb0-af83-4807-9d1e-49148b56b59c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b47a991aa2500236aec9d80d2ae4c51144619f90
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "91116037"
---
# <a name="fulltextserviceproperty-transact-sql"></a>FULLTEXTSERVICEPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Full-Text Engine のプロパティに関する情報を返します。 これらのプロパティは、**sp_fulltext_service** を使用して設定および取得できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
FULLTEXTSERVICEPROPERTY ('property')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *property*  
 フルテキスト サービス レベルのプロパティ名を含む式です。 次の表は、プロパティと、返される情報についての説明の一覧です。  
  
> [!NOTE]
>  次のプロパティは、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **ConnectTimeout**, **DataTimeout**, and **ResourceUsage** の将来のリリースで削除される予定です。 新しい開発作業では、これらのプロパティの使用は避け、現在これらのプロパティのいずれかを使用しているアプリケーションは修正するようにしてください。  
  
|プロパティ|値|  
|--------------|-----------|  
|**ResourceUsage**|0 を返します。 旧バージョンとの互換性のためにのみサポートされています。|  
|**ConnectTimeout**|0 を返します。 旧バージョンとの互換性のためにのみサポートされています。|  
|**IsFulltextInstalled**|フルテキスト コンポーネントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスと共にインストールされます。<br /><br /> 0 = フルテキストはインストールされていない<br /><br /> 1 = フルテキストはインストールされている<br /><br /> NULL = 無効な入力またはエラー|  
|**DataTimeout**|0 を返します。 旧バージョンとの互換性のためにのみサポートされています。|  
|**LoadOSResources**|オペレーティング システムのワード ブレーカーやフィルターを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに登録し、使用するかどうかを指定します。 オペレーティング システム (OS) に行われた更新によって予期しない動作が起こるのを防ぐため、既定ではこのプロパティは無効になっています。 OS リソースの使用を有効にすると、インスタンス固有のリソースがインストールされていない [!INCLUDE[msCoName](../../includes/msconame-md.md)] Indexing Service に登録されている、言語とドキュメントの種類に応じたリソースにアクセスできます。 OS リソースの読み込みを有効にする場合は、OS リソースが信頼された署名付きバイナリであることを確認してください。信頼された署名付きバイナリでない場合、**VerifySignature** が 1 に設定されたときに、OS リソースを読み込むことができません。<br /><br /> 0 = この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス固有のフィルターとワード ブレーカーのみを使用<br /><br /> 1 = OS のフィルターとワード ブレーカーを読み込む。|  
|**VerifySignature**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Search サービスによって署名付きバイナリのみを読み込むかどうかを指定します。 既定では、信頼された署名付きバイナリのみが読み込まれます。<br /><br /> 0 = バイナリが署名付きかどうかを確認しない<br /><br /> 1 = 信頼された署名付きバイナリのみを確認して読み込む|  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="examples"></a>例  
 次の例では、署名付きバイナリのみが読み込まれるかどうかを確認し、戻り値は、この検証が行われていないことを示します。  
  
```sql  
SELECT fulltextserviceproperty('VerifySignature');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
0  
```  
  
 署名の検証を既定値の 1 に戻すには、次の `sp_fulltext_service` ステートメントを使用できます。  
  
```sql  
EXEC sp_fulltext_service @action='verify_signature', @value=1;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
  
