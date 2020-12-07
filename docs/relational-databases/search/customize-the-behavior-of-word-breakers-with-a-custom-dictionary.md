---
description: ユーザー辞書によるワード ブレーカーの動作のカスタマイズ (SQL Server Search)
title: ユーザー辞書によるワード ブレーカーの動作のカスタマイズ
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 46fb0f6fa4e8607296ead7a2f5e77ac97e75f9d5
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866985"
---
# <a name="customize-behavior-of-word-breakers-with-a-custom-dictionary-sql-server-search"></a>ユーザー辞書によるワード ブレーカーの動作のカスタマイズ (SQL Server Search)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  言語固有のユーザー辞書ファイルを作成することで、特定の言語のワード ブレーカーの動作をカスタマイズできます。 たとえば、特定の用語やパターンがワード ブレーカーによって区切られないようにすることができます。  
  
 詳細については、次の SharePoint の記事を参照してください。  
  
 [ユーザー辞書を作成する (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/cc263242(v=office.14))  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、ユーザー辞書ファイルを次のフォルダーに配置します。  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 ユーザー辞書ファイルの作成または変更後、次のコマンドで SQL フルテキスト デーモン ランチャーを再起動します。  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
