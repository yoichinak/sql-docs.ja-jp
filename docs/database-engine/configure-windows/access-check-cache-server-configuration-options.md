---
title: access check cache サーバー構成オプション | Microsoft Docs
description: アクセス チェックの結果キャッシュと、キャッシュの動作を制御するオプションについて説明します。 どのような場合に SQL Server でこれらのオプションを変更すべきかについて説明します。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 893400411c6f3d2faf6313923aa0f6127a3f2cf0
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98171074"
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache サーバー構成オプション
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

データベース オブジェクトに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からアクセスすると、アクセス チェックが **access check result cache** と呼ばれる内部構造にキャッシュされます。 
  
**access check cache bucket count** オプションは、access check result cache に使用されるハッシュ バケットの数を制御します。 

**access check cache quota** オプションは、access check result cache に格納されるエントリの数を制御します。 エントリが最大数に達すると、最も古いエントリが access check result cache から削除されます。
  
既定値は 0 で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がこれらのオプションを管理していることを示します。 [!INCLUDE[ssSQL15](../../includes/sssql16-md.md)] 以降では、既定値は次の内部構成に変換されます。
-   access check cache bucket count の値が 0 の場合、バケット数の既定値は 256 になります。
-   access check cache quota の値が 0 の場合、エントリの既定値は 1,024 になります。

まれに、これらのオプションを変更することによってパフォーマンスが向上する場合があります。 たとえば、メモリの使用率が高すぎる場合は、access check result cache のサイズを小さくした方がよいでしょう。 または、アクセス許可の再計算時に CPU の使用率が高い場合は、access check result cache のサイズを大きくした方がよいでしょう。
 
> [!IMPORTANT]
> これらのオプションはマイクロソフト カスタマー サポート サービスから指示があった場合にのみ変更することをお勧めします。 "access check cache bucket count" と "access check cache quota" の値を変更する必要がある場合は、1:4 の比率を使用してください。 たとえば、"access check cache bucket count" 値を 512 に変更した場合、"access check cache quota" 値は 2,048 に変更します。 
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
