---
title: 警告 (トランザクション パブリケーション情報)
description: '[トランザクション パブリケーション情報] ダイアログ ボックスの [警告] タブについて説明します。'
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 5e80d035960e9232281f5a633422b51d3356b7b7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463203"
---
# <a name="publication-information-warnings-transactional-publication"></a>パブリケーション情報、[警告] \(トランザクション パブリケーション)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **以降を実行しているディストリビューターでは、** [警告] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] タブを使用できます。 **[警告]** タブでは、選択されているパブリケーションに対して次の操作を実行できます。  
  
-   レプリケーション モニターに警告を表示します。  
  
-   警告に関連するしきい値を指定する。  
  
-   警告に関連する通知を定義する。  
  
## <a name="warnings-thresholds-and-alerts"></a>警告、しきい値、および通知  
 既定では、レプリケーション モニターは、初期化されていないサブスクリプションに対して警告を表示します。サブスクリプション情報を含むページの **[状態]** 列に、警告として **[初期化されていないサブスクリプション]** という状態が表示されます。 トランザクション パブリケーションの場合は、次のような追加の条件で警告を生成するかどうかを指定できます。  
  
-   差し迫ったサブスクリプションの有効期限。  
  
     これは、 **[サブスクリプションの有効期限がしきい値内で切れる場合に警告します。]** オプションに対応します。 指定したしきい値に到達するか、しきい値を超過すると、(より優先度が高い問題を表示する必要がない限り) **[まもなく期限切れ/期限切れ]** というサブスクリプション状態が表示されます。  
  
-   指定した待機時間の超過。 トランザクションがパブリッシャー側でコミットされたときから、サブスクライバー側で対応するトランザクションがコミットされるまでに経過した時間です。  
  
     これは、 **[待機時間がしきい値を超えた場合に警告します。]** オプションに対応します。 指定したしきい値に到達するか、しきい値を超過すると、(より優先度が高い問題を表示する必要がない限り) **[パフォーマンス クリティカル]** というサブスクリプション状態が表示されます。 しきい値は、サブスクリプション情報を含むページの **[パフォーマンス]** 列に表示されるパフォーマンス評価にも使用されます。 パフォーマンス評価は、次のいずれかの値になります。  
  
    -   [非常に良い]  
  
    -   [良い]  
  
    -   [普通]  
  
    -   悪い  
  
    -   Critical  
  
 警告を有効にする場合は、しきい値も設定します。 たとえば、 **[待機時間がしきい値を超えた場合に警告します。]** 警告を有効にした場合は、パブリッシャー側でトランザクションをコミットしたときからサブスクライバー側でトランザクションをコミットするまでに許容する時間を選択します。  
  
 しきい値に到達した場合は、レプリケーション モニターに警告を表示でき、さらに通知を発行することができます。 通知を定義するには、 **[警告の構成]** をクリックし、 **[レプリケーションの警告の構成]** ダイアログ ボックスに情報を入力します。  
  
## <a name="options"></a>オプション  
 **有効**  
 警告を有効にする場合に選択します。その場合は、しきい値を指定します。  
  
 **警告**  
 しきい値に関連付けられている警告の説明です。  
  
 **しきい値**  
 しきい値の値を指定します。  
  
 **[警告の構成]**  
 **[警告]** グリッドの行を選択し、 **[警告の構成]** をクリックすると、 **[レプリケーションの警告の構成]** ダイアログ ボックスが表示されます。 このダイアログ ボックスでは、選択したしきい値および警告に関連付けた通知を定義できます。  
  
 **[変更の破棄]**  
 クリックすると、警告およびしきい値に対する変更が破棄されます。  
  
> [!NOTE]  
>  **[変更の破棄]** をクリックしても、 **[レプリケーションの警告の構成]** ダイアログ ボックスに定義されている通知は影響を受けません。  
  
 **[変更の保存]**  
 クリックすると、警告およびしきい値に対する変更が保存されます。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーション モニターを使用したパフォーマンスの監視](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [レプリケーション モニターのしきい値と警告の設定](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
