---
description: '[警告のプロパティ] - [新しい警告] ([応答] ページ)'
title: '[警告のプロパティ] - [新しい警告] ([応答] ページ)'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5f8796a3103400a457559efc33ac295429562695
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036513"
---
# <a name="alert-properties---new-alert-response-page"></a>[警告のプロパティ] - [新しい警告] ([応答] ページ)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告に応答して、実行する必要があるジョブを指定し、通知されるオペレーターの一覧を取得できます。  

## <a name="options"></a>オプション  
**[ジョブの実行]**  
**[ジョブ一覧]**、 **[新しいジョブ]** 、および **[ジョブの表示]** の各オプションを有効にします。  
  
**[新しいジョブ]**  
**[新しいジョブ]** ダイアログ ボックスを開きます。 **[ジョブの実行]** が選択されていない場合、このボタンは使用できません。  
  
**ジョブの表示**  
選択されているジョブを表示または変更します。 **[ジョブの実行]** が選択されていない場合、このオプションは使用できません。  
  
**[オペレーターに通知する]**  
オペレーターを追加、削除、または変更できるようにするためのコントロールを有効にします。  
  
**[オペレーター一覧]**  
警告の発生時に通知するオペレーターの一覧を表示します。 通知方法を指定するには、オペレーター名の後に表示されている **[電子メール]**、 **[ポケットベル]**、または **[Net Send]** チェック ボックスをオンにします。 **[オペレーターに通知する]** が選択されていない場合、このオプションは使用できません。  
  
**電子メール**  
電子メールを使用してオペレーターに通知します。  
  
**ポケットベル**  
ポケットベルの電子メール アドレスを使用してオペレーターに通知します。  
  
**Net send**  
**net send** を使用してオペレーターに通知します。  
  
**[新しいオペレーター]**  
**[新しいオペレーター]** ダイアログ ボックスを表示します。このダイアログ ボックスを使用して、新しいオペレーターを作成できます。  
  
**[オペレーターの表示]**  
現在選択されているオペレーターの **[プロパティ]** ダイアログ ボックスを表示します。 **[オペレーターのプロパティ]** ダイアログ ボックスで、オペレーターのプロパティを表示および変更できます。  
  
## <a name="see-also"></a>参照  
[警告](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[警告](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
