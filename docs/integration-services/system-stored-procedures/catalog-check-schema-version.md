---
description: catalog.check_schema_version
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa47e5107551ec2d4ded0832ff52922ffb4bfd55
ms.sourcegitcommit: 0bcda4ce24de716f158a3b652c9c84c8f801677a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247528"
---
# <a name="catalogcheck_schema_version"></a>catalog.check_schema_version 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SSISDB カタログ スキーマと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] バイナリ (ISServerExec および SQLCLR アセンブリ) に互換性があるかどうかを示します。  
  
 スキーマとバイナリに互換性がない場合、ISServerExec.exc でエラー メッセージが記録されます。  
  
 SSISDB スキーマのバージョンは、修正プログラムや更新プログラムの適用時にスキーマが変更された場合に増加します。 SSISDB バックアップの復元後にこのストアド プロシージャを実行して、スキーマとバイナリに互換性があるようにすることをお勧めします。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.check_schema_version [ @use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>引数  
 [ @use32bitruntime= ] *use32bitruntime*  
 パラメーターが **1** に設定されている場合、32 ビット バージョンの dtexec が呼び出されます。 *use32bitruntime* は、**int** です。  
  
 
## <a name="return-code-value"></a>リターン コード値 
成功した場合は 0 を返します。 

## <a name="result-set"></a>結果セット  

次の形式のテーブルを返します。

| 列名 | データ型 | 説明 |
|---|---|---|
| SERVER_BUILD | **decimal** | SQL Server のバージョン。 たとえば、SQL Server 2014 を実行しているサーバーは `14.0.3335.7` です。 |
| SCHEMA_VERSION | **tinyint** | SQL Server のバージョン番号。 たとえば、SQL Server 2017 と 2019 はそれぞれ `6` と `7` になります。|
| SCHEMA_BUILD | **string** | スキーマのビルド。 |
| ASSEMBLY_BUILD | **string** | アセンブリのビルド。 |
| SHARED_COMPONENT_VERSION | **string** | 共有コンポーネントのバージョン。 | 

## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限が必要です。  
  
-   **ssis_admin** データベース ロールのメンバーシップ。  
  
  
