---
description: オペレーターへの通知タスク
title: オペレーターへの通知タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d6bcdb94260a5fe1190e6f96ada085f004458c54
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194234"
---
# <a name="notify-operator-task"></a>オペレーターへの通知タスク

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  オペレーターへの通知タスクは、通知メッセージを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント オペレーターに送信します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント オペレーターは、電子通知を受信できる人またはグループの別名です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オペレーターの詳細については、「 [オペレーター](../../ssms/agent/operators.md)」を参照してください。  
  
 オペレーターへの通知タスクを使用すると、パッケージは電子メール、ポケットベル、または **Net Send** 経由で、1 人以上のオペレーターに通知できます。 通知方法は、オペレーターごとに変更できます。 たとえば、オペレーター A には電子メールとポケットベルで通知し、オペレーター B にはポケットベルと **Net Send** で通知します。 オペレーターへの通知タスクから通知を受信するオペレーターは、このタスク上にある **OperatorNotify** コレクションのメンバーである必要があります。  
  
 オペレーターへの通知タスクは、Transact-SQL ステートメントや DBCC コマンドをカプセル化しない、唯一のデータベース メンテナンス タスクです。  
  
## <a name="configuration-of-the-notify-operator-task"></a>オペレーターへの通知タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[オペレーターへの通知タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
