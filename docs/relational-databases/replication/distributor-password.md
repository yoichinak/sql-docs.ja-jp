---
description: '[ディストリビューター パスワード]'
title: ディストリビューター パスワード | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8740af3ff189bf929c1a97caaf5d3cc31e283714
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498755"
---
# <a name="distributor-password"></a>[ディストリビューター パスワード]
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  このサーバーをリモート ディストリビューターとして使用する 1 つ以上のパブリッシャーを、このウィザードの **[パブリッシャー]** ページで有効にしている場合は、レプリケーションが **distributor_admin** ログインを使用してパブリッシャーとリモート ディストリビューターとの間で確立する接続のパスワードを指定する必要があります。 このリモート ディストリビューターを使用するそれぞれのパブリッシャーに対して、パブリケーションの新規作成ウィザードまたはディストリビューションの構成ウィザードの **[管理パスワード]** ページに、同じパスワードを入力する必要があります。 ディストリビューターのセキュリティの詳細については、「[ディストリビューターのセキュリティ保護](../../relational-databases/replication/security/secure-the-distributor.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **パスワード**  
 パブリッシャーとリモート ディストリビューターとの間の接続に使用する複雑なパスワードを入力します。  
  
 **[パスワードの確認入力]**  
 正しく入力されたことを確認するために、パスワードを再入力します。  
  
## <a name="see-also"></a>参照  
 [[ディストリビューションの構成]](../../relational-databases/replication/configure-distribution.md)   
 [パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
