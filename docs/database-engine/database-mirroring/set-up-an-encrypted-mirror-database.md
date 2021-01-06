---
title: 暗号化されたミラー データベースの設定 | Microsoft Docs
description: sp_control_dbmasterkey_password を使用して資格情報を作成し、ミラー データベースのデータベース マスター キーの自動暗号化解除を有効にする方法について説明します。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- database master key [SQL Server], database mirroring
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6611528bd3d5b12f01ecebb48e63ee3b01d73215
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641982"
---
# <a name="set-up-an-encrypted-mirror-database"></a>暗号化されたミラー データベースの設定
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  ミラー データベースのデータベース マスター キーの暗号化を自動的に解除できるようにするには、マスター キーの暗号化に使用したパスワードをミラー サーバー インスタンスに指定する必要があります。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンには、パスワードを転送するメカニズムがあります。 データベース ミラーリングを開始する前にデータベース マスター キーに対する資格情報を作成するには、 **sp_control_dbmasterkey_password** を使用します。 この処理は、ミラー化するすべてのデータベースに対して行う必要があります。 詳細については、「 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)」を参照してください。  
  
> [!CAUTION]  
>  **sa** など高いレベルの特権を持つサーバー プリンシパルからのアクセスを禁止したままにしておく必要のあるデータベースについては、フェールオーバー時の暗号化解除を有効にしないでください。 データベースのキー階層をサービス マスター キーで暗号化解除できないようにデータベースを構成できます。 このオプションは、 **sa** など特権レベルの高いサーバー プリンシパルからアクセスできてはならない情報を格納しているデータベースに対する多層防御の 1 つとしてサポートされています。 このようなデータベースに対してフェールオーバー時の暗号化解除を有効にすると、この多層防御が効力を失います。その結果、 **sa** など特権レベルの高いサーバー プリンシパルによるデータベースの暗号化解除が可能になります。  
  
## <a name="see-also"></a>参照  
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  
