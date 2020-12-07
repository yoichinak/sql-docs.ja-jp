---
description: プログラムによるパッケージのロールの管理 (SSIS Service)
title: プログラムによるパッケージのロールの管理 (SSIS Service) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 33922748916193e875799839fbbf6fe0f7a76a26
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88495529"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>プログラムによるパッケージのロールの管理 (SSIS Service)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  プログラムによって [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を操作する際に、どのロールをパッケージに適用できるかどうかを確認したり、個々のパッケージに適用されているロールを確認または設定することが必要な場合があります。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 名前空間の <xref:Microsoft.SqlServer.Dts.Runtime> クラスは、これらの要件を満たすさまざまなメソッドを提供します。  
  
 ロールは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** データベースに格納されたパッケージにのみ適用されます。 パッケージ ロールの詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。  
  
 このトピックで説明するすべてのメソッドには、**Microsoft.SqlServer.ManagedDTS** アセンブリへの参照が必要です。 新しいプロジェクトに参照を追加した後、**using** または **Imports** ステートメントを使用して <xref:Microsoft.SqlServer.Dts.Runtime> 名前空間をインポートします。  
  
> [!IMPORTANT]  
>  SSIS パッケージ ストアを操作するための <xref:Microsoft.SqlServer.Dts.Runtime.Application> クラスのメソッドでは、"."、localhost、またはローカル サーバーのサーバー名のみがサポートされます。 "(local)" は使用できません。  
  
## <a name="determining-which-roles-are-available"></a>使用できるロールの確認  
 特定のサーバーに格納されているパッケージで使用できるロールを確認するには、<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> クラスの <xref:Microsoft.SqlServer.Dts.Runtime.Application> メソッドを呼び出します。  
  
## <a name="determining-which-roles-are-assigned"></a>割り当てられたロールの確認  
 特定のパッケージに既に割り当てられているロールを確認するには、<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> メソッドを呼び出します。 パッケージにロールを割り当てるには、<xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のロール (SSIS サービス)](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
