---
description: '[HOST_NAME 値]'
title: HOST_NAME 値 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 32926ab1c2e5dcd2c97d296d07c5fab725793f47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427954"
---
# <a name="host_name-values"></a>[HOST_NAME 値]
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

パラメーター化されたフィルター付きのマージ パブリケーションは、SUSER_SNAME() 関数または HOST_NAME() 関数を使用してデータにフィルターをかけます。 関数は、パブリケーションの新規作成ウィザードまたは **[パブリケーションのプロパティ]** ダイアログ ボックスで指定します。  
  
既定では、HOST_NAME() 関数は、パブリッシャーに接続しているコンピューターの名前を返します。 通常、パラメーター化されたフィルターを使用する場合は、ウィザードのこのページで値を指定してこの値をオーバーライドします。 これにより、HOST_NAME() 関数は、コンピューターの名前ではなく、指定された値を返します。 詳細については、「[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」 (パラメーター化された行フィルター) の "Overriding the HOST_NAME() Value" (HOST_NAME() 値のオーバーライド) をご覧ください。  
  
> [!NOTE]  
>  HOST_NAME() をオーバーライドした場合、HOST_NAME() 関数のすべての呼び出しは、指定された値を返します。 他のアプリケーションが、コンピューター名を返す HOST_NAME() 関数に依存していないことを確認してください。  
  
## <a name="options"></a>Options  
 **[サブスクリプションのプロパティ]**  
 サブスクライバーごとに **[HOST_NAME 値]** 列に値を入力するか、既定値を受け入れます。既定値は、サブスクライバー コンピューターの名前です。  
  
## <a name="see-also"></a>参照  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME (Transact-SQL)](../../t-sql/functions/host-name-transact-sql.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
