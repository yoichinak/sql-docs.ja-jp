---
description: catalog.create_customized_logging_level
title: catalog.create_customized_logging_level | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7aaf0fb0ccdd285944e5fceaba561bd626317121
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129902"
---
# <a name="catalogcreate_customized_logging_level"></a>catalog.create_customized_logging_level 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  新しいカスタマイズされたログ記録レベルを作成します。 カスタマイズされたログ記録レベルの詳細については、「[Integration Services &#40;SSIS&#41; のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @events_value = ] events_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>引数  
 [ @level_name = ] *level_name*  
 新しいの既存の名前は、ログ記録レベルをカスタマイズします。  
  
 *level_name* は **nvarchar(128)** です。  
  
 [ @level_description = ] *level_description*  
 新しいの既存の説明では、ログ記録レベルをカスタマイズします。  
  
 *level_description* は **nvarchar(max)** です。  
  
 [ @profile_value = ] *profile_value*  
 新しいする統計情報は、ログに記録するログ記録レベルをカスタマイズできます。  
  
 統計情報の有効な値には、次の項目が含まれます。 これらの値は、**[カスタマイズされたログ記録レベルの管理]** ダイアログ ボックスの **[統計]** タブの値に対応しています。  
  
-   実行 = 0  
  
-   ボリューム = 1  
  
-   パフォーマンス = 2    
  
 *profile_value* は **bigint** です。  
  
 [ @events_value = ] *events_value*  
 新しいイベントは、ログに記録するログ記録レベルをカスタマイズできます。  
  
 イベントの有効な値には、次の項目が含まれます。 これらの値は、**[カスタマイズされたログ記録レベルの管理]** ダイアログ ボックスの **[イベント]** タブの値に対応しています。  
  
|イベントをイベントのコンテキスト|イベントのコンテキストを持つイベント|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnostic = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext= 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 *events_value* は **bigint** です。  
  
 [ @level_id = ] *level_id* OUT  
 新しい ID では、ログ記録レベルをカスタマイズします。  
  
 *level_id* は **bigint** です。  
  
## <a name="remarks"></a>解説  
 Transact-SQL で *profile_value* または *events_value* 引数の複数の値を結合するには、この例に従います。 OnError (8) と DiagnosticEx (15) イベントをキャプチャする場合、*event_value* を計算する式は `2^8 + 2^15 = 33024` です。  
  
## <a name="return-codes"></a>リターン コード  
 成功した場合は 0 を返します。  
  
 ストアド プロシージャが失敗した場合は、エラーをスローします。  
  
## <a name="result-set"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 ストアド プロシージャが失敗する原因となる条件を以下に示します。  
  
-   ユーザーには、必要なアクセス許可がありません。  
  
  
