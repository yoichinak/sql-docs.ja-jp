---
description: sp_configure (Transact-SQL)
title: sp_configure (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e02f07a78dc5f3022bfd1f374738f22b326ca94e
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955863"
---
# <a name="sp_configure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  現在のサーバーのグローバル構成設定を表示または変更します。

> [!NOTE]  
> データベースレベルの構成オプションについては、「 [ALTER DATABASE スコープ構成 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」を参照してください。 ソフト NUMA を構成するには、「 [ソフト numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>引数  
`[ @configname = ] 'option_name'` 構成オプションの名前を指定します。 *option_name* は **varchar(35)** 、既定値は NULL です。 は、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 構成名の一部である一意の文字列を認識します。 指定しない場合、オプションの完全な一覧が返されます。  
  
 使用可能な構成オプションとその設定の詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
`[ @configvalue = ] 'value'` 新しい構成設定を示します。 *value* のデータ型は **int**で、既定値は NULL です。 最大値はオプションごとに異なります。  
  
 各オプションの最大値を確認するには、 **sys.configurations**カタログビューの**最大**列を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 パラメーターを指定せずに実行すると、次の表に示すように、 **sp_configure** によって5つの列を含む結果セットが返され、アルファベット順にアルファベット順に並べ替えられます。  
  
 **Config_value**と**run_value**の値は、自動的には等価ではありません。 **Sp_configure**を使用して構成設定を更新した後、システム管理者は、上書きを使用して再構成または再構成のいずれかを使用して、実行中の構成値を更新する必要があります。 詳細については、「解説」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|構成オプションの名前。|  
|**minimum**|**int**|構成オプションの最小値。|  
|**maximum**|**int**|構成オプションの最大値。|  
|**config_value**|**int**|**Sp_configure** ( **sys.configurations**値) を使用して構成オプションが設定された値。 これらのオプションの詳細については、次を参照してください。 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md) および [sys.configUrations &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)です。|  
|**run_value**|**int**|構成オプションの現在実行中の値 ( **sys.configurations.value_in_use**)。<br /><br /> 詳細については、「 [ transact-sql&#41;&#40;sys.configurations ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)を参照してください。|  
  
## <a name="remarks"></a>注釈  
 サーバーレベルの設定を表示または変更するには、 **sp_configure** を使用します。 データベースレベルの設定を変更するには、ALTER DATABASE を使用します。 現在のユーザー セッションのみに影響する設定を変更するには、SET ステートメントを使用します。  
  
### [!INCLUDE [ssbigdataclusters-ss-nover](../../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE [big-data-clusters-master-instance-ha-endpoint-requirement](../../includes/big-data-clusters-master-instance-ha-endpoint-requirement.md)]

## <a name="updating-the-running-configuration-value"></a>実行中の構成値の更新  
 *オプション*に新しい*値*を指定すると、結果セットには**config_value**列にこの値が表示されます。 この値は、最初は [ **run_value** ] 列の値とは異なり、現在実行中の構成値が表示されます。 **Run_value**列で実行中の構成値を更新するには、システム管理者が、上書きを使用して再構成または再構成のいずれかを実行する必要があります。  
  
 すべての構成オプションを使用して、上書きによる再構成と再構成の両方を行うことができます。 ただし、基本的な再構成ステートメントでは、適切な範囲外のオプション値が拒否されるか、オプション間で競合が発生する可能性があります。 たとえば、 **recovery interval** の値が60分を超える場合、または **関係マスク** の値が **affinity i/o mask** の値と重複する場合、再構成ではエラーが生成されます。 これに対して、上書きを使用して再構成すると、適切なデータ型のオプション値が許可され、指定した値で強制的に再構成されます。  
  
> [!CAUTION]  
> オプション値が適切でない場合、サーバー インスタンスの構成に悪影響を及ぼす可能性があります。 上書きを伴う再構成を慎重に使用してください。  
  
 一部のオプションは、RECONFIGURE ステートメントにより動的に更新されます。その他のオプションを使用する場合は、サーバーの停止と再起動が必要になります。 たとえば、 **min server memory** および **max server memory** server memory オプションは、で動的に更新されます [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。したがって、サーバーを再起動しなくても、これらを変更できます。 これに対して、 **FILL FACTOR** オプションの実行中の値を再構成するには、を再起動する必要があり [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
 構成オプションで再構成を実行した後、 **sp_configure '***option_name***'** を実行することで、オプションが動的に更新されたかどうかを確認できます。 動的に更新されるオプションでは、 **run_value** 列と **config_value** 列の値が一致する必要があります。 また、 **sys.configurations**カタログビューの [ **is_dynamic** ] 列を参照して、どのオプションが動的であるかを確認することもできます。  
 
 変更は、SQL Server のエラーログにも書き込まれます。
  
> [!NOTE]  
>  指定された *値* がオプションに対して大きすぎる場合、 **run_value** 列には、が [!INCLUDE[ssDE](../../includes/ssde-md.md)] 有効ではない設定を使用するのではなく、動的メモリに既定値が設定されているという事実が反映されます。  
  
 詳細については、「 [transact-sql&#41;の再構成 &#40;](../../t-sql/language-elements/reconfigure-transact-sql.md)」を参照してください。  
  
## <a name="advanced-options"></a>詳細オプション  
 **Affinity mask**や**recovery interval**などの一部の構成オプションは、詳細設定オプションとして指定されています。 既定では、これらのオプションを表示および変更することはできません。 使用できるようにするには、 **[詳細オプションの表示** ] 構成オプションを1に設定します。 
 
> [!CAUTION]  
> **[詳細オプションを表示**する] オプションが1に設定されている場合、この設定はすべてのユーザーに適用されます。 この状態は一時的に使用することをお勧めします。また、詳細オプションの表示が必要なタスクが完了したら、0に戻すことをお勧めします。  
  
 構成オプションとその設定の詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを使用して **sp_configure** を実行し、構成オプションを変更するか、または再構成ステートメントを実行するには、ALTER SETTINGS サーバーレベルのアクセス許可が付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. 詳細構成オプションの一覧表示  
 次の例は、すべての構成オプションを設定および一覧表示する方法を示しています。 詳細な構成オプションは、最初の設定でに表示され `show advanced option` `1` ます。 このオプションを変更した後、 `sp_configure` パラメーターを指定せずにを実行すると、すべての構成オプションが表示されます。  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 "構成オプション ' show advanced options ' が0から1に変更されました。 再構成ステートメントを実行してインストールします。 "  
  
 `RECONFIGURE` を実行し、すべての構成オプションを表示します。  
  
```sql  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. 構成オプションの変更  
 次の例では、システムの `recovery interval` を `3` 分に設定します。  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-sspdw"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. すべての使用可能な構成設定を一覧表示する  
 次の例では、すべての構成オプションを一覧表示する方法を示します。  
  
```sql  
EXEC sp_configure;  
```  
  
 結果は、オプションの最小値と最大値が続くオプション名を返します。 **Config_value**は、再 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 構成が完了したときにが使用する値です。 **run_value** は、現在使用されている値です。 値が変更中のプロセスではない限り、 **config_value** と **run_value** は、通常は同じ値です。  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. 1 つの構成名の構成設定を一覧表示する  
  
```sql  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. Hadoop 接続を設定する  
 Hadoop 接続を設定するには、sp_configure の実行に加えて、さらにいくつかの手順が必要です。 詳細な手順については、「 [CREATE EXTERNAL DATA SOURCE &#40;transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [ソフト NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
