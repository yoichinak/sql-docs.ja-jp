---
description: レプリケーション関数 - PUBLISHINGSERVERNAME
title: PUBLISHINGSERVERNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e6b42d4883053a32ec97f76278139fad8d0cf0f4
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036598"
---
# <a name="replication-functions---publishingservername"></a>レプリケーション関数 - PUBLISHINGSERVERNAME
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース ミラーリング セッションに参加しているパブリッシュされたデータベースの元のパブリッシャーの名前を返します。 この関数は、パブリケーション データベース上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパブリッシャー インスタンス側で実行されます。 パブリッシュされたデータベースの元のパブリッシャーを確認するために使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
PUBLISHINGSERVERNAME()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 **nvarchar**  
  
## <a name="remarks"></a>解説  
 PUBLISHINGSERVERNAME は、すべての種類のレプリケーションで使用できます。  
  
 PUBLISHINGSERVERNAME は、パブリッシャーとミラーリング パートナー インスタンスの間のパブリケーション データベースでデータベース ミラーリング セッションが開かれているときに使用します。  
  
 この関数はパブリケーション データベースのコンテキスト内で実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のミラーリング サーバー インスタンスのパブリケーション データベースで PUBLISHINGSERVERNAME を実行すると、パブリッシュされたデータベースの発行元パブリッシャー インスタンスの名前が返されます。 この関数が、パブリッシュされていない、またはフェールオーバー後にミラー サーバー インスタンスからパブリッシュされたミラー サーバー インスタンスにあるデータベース上で実行されると、ミラー サーバー インスタンスの名前が返されます。 この関数が元のパブリッシャー インスタンスで実行されると、パブリッシャーの名前が返されます。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [レプリケーションの動作 &#40;Transact-SQL&#41;]()  
  
