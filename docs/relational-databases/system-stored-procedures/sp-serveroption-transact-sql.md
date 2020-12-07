---
description: sp_serveroption (Transact-SQL)
title: sp_serveroption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs:
- TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ba6045caf5d95aed6d11c0844c16afd93365368f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547393"
---
# <a name="sp_serveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  リモートサーバーおよびリンクサーバーのサーバーオプションを設定します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>引数  
`[ @server = ] 'server'` オプションを設定するサーバーの名前を指定します。 *server* のデータ型は **sysname**で、既定値はありません。  
  
`[ @optname = ] 'option_name'` 指定されたサーバーに設定するオプションです。 *option_name* は **varchar (** 35 **)**,、既定値はありません。 *option_name* は、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**照合順序互換**|リンク サーバーに対する分散クエリの実行に影響を与えます。 このオプションが **true**に設定されている場合、では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文字セットと照合順序 (並べ替え順序) に関して、リンクサーバーのすべての文字がローカルサーバーと互換性があると見なされます。 これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からプロバイダーに文字を含む列の比較を送信できるようになります。 このオプションが設定されていない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では文字列を含む列の比較の評価は常にローカルで行われます。<br /><br /> このオプションは、リンク サーバーに対応するデータ ソースがローカル サーバーと同じ文字セットと並べ替え順を持っていることが確認できている場合のみ設定します。|  
|**照合順序名**|[ **リモート照合順序を使用する** ] が **true** で、データソースがデータソースでない場合に、リモートデータソースによって使用される照合順序の名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がサポートしている照合順序名のいずれかを指定する必要があります。<br /><br /> このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外の OLE DB データ ソースにアクセスし、その照合順序が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序のいずれかと一致する場合に使用します。<br /><br /> リンク サーバーは、そのサーバー内のすべての列で使用される単一の照合順序をサポートしている必要があります。 リンク サーバーが、単一のデータ ソース内で複数の照合順序をサポートしている、またはリンク サーバーの照合順序が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序のいずれかと一致するかどうかが判断できない場合は、このオプションを設定しないでください。|  
|**接続のタイムアウト**|リンクサーバーに接続するときのタイムアウト (秒単位)。<br /><br /> **0**の場合は**sp_configure**既定値を使用します。|  
|**データアクセス**|分散クエリ アクセスに対してリンク サーバーを有効または無効にします。 **Sp_addlinkedserver**によって追加された**sys. サーバー**エントリに対してのみ使用できます。|  
|**dist**|ディストリビューターです。|  
|**lazy schema validation (lazy schema validation)**|リモート テーブルのスキーマをチェックするかどうかを指定します。<br /><br /> **True**の場合、クエリの先頭でリモートテーブルのスキーマチェックをスキップします。|  
|**pub**|文書.|  
|**クエリタイムアウト**|リンク サーバーに対するクエリのタイムアウト値です。<br /><br /> **0**の場合は**sp_configure**既定値を使用します。|  
|**rpc-epmap**|指定されたサーバーからの RPC を有効にします。|  
|**rpc 出力**|指定されたサーバーへの RPC を有効にします。|  
|**sub**|サブスクライバ.|  
|**システム**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**リモート照合順序を使用する**|リモート列とローカル サーバーのどちらの照合順序を使用するかを指定します。<br /><br /> **True**の場合、データソースにはリモート列の照合順序が使用され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データソース以外には [**照合順序名**] で指定された照合順序が使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br /> **False**の場合、分散クエリは常にローカルサーバーの既定の照合順序を使用しますが、**照合順序名**とリモート列の照合順序は無視されます。 既定値は **false** です。 **False**値は、7.0 で使用される照合順序セマンティクスと互換性が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] あります。|  
|**remote proc transaction promotion**|このオプションを使用して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) トランザクションにより、サーバー間のプロシージャのアクションを保護します。 このオプションが TRUE (ON) の場合、リモートストアドプロシージャを呼び出すと分散トランザクションが開始され、トランザクションは MS DTC に参加します。 リモート ストアド プロシージャを呼び出す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、トランザクションを実行したインスタンスであり、このインスタンスによってトランザクションが制御されます。 この接続に対して引き続き COMMIT TRANSACTION または ROLLBACK TRANSACTION ステートメントを実行すると、制御側のインスタンスは MS DTC 対して、コンピューター間の分散トランザクションの完了を管理することを要求します。<br /><br /> [!INCLUDE[tsql](../../includes/tsql-md.md)]分散トランザクションが開始されると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リンクサーバーとして定義されているの他のインスタンスに対して、リモートストアドプロシージャ呼び出しを行うことができます。 リンクサーバーはすべて分散トランザクションに参加 [!INCLUDE[tsql](../../includes/tsql-md.md)] しており、MS DTC は各リンクサーバーに対してトランザクションが完了していることを確認します。<br /><br /> このオプションが FALSE (または OFF) に設定されている場合、リンクサーバーでリモートプロシージャコールを呼び出すと、ローカルトランザクションは分散トランザクションに昇格されません。<br /><br /> サーバー間のプロシージャ コールを行う前にトランザクションが既に分散トランザクションである場合、このオプションに効力はありません。 リンク サーバーに対するプロシージャ コールは、同じ分散トランザクションで実行されます。<br /><br /> サーバーからサーバーへのプロシージャ呼び出しを行う前に、接続にアクティブなトランザクションがない場合、このオプションは無効になります。 次に、アクティブなトランザクションを使用せずに、リンクサーバーに対してプロシージャを実行します。<br /><br /> このオプションの既定値は TRUE (ON) です。|  
  
`[ @optvalue = ] 'option_value'`*Option_name*を有効にするかどうかを指定します (**TRUE**または**on**)。または無効 (**FALSE**または**オフ**)。 *option_value* は **varchar (** 10 **)**,、既定値はありません。  
  
 *option_value* は、 **接続タイムアウト** オプションと **クエリタイムアウト** オプションで負でない整数を指定できます。 **照合順序名**オプションでは、 *option_value*照合順序名または NULL を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **照合順序互換**オプションが TRUE に設定されている場合、**照合順序名**は自動的に NULL に設定されます。 **照合順序名**が null 以外の値に設定されている場合、**照合順序の互換性**が自動的に FALSE に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER ANY LINKED SERVER 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、の別のインスタンスに対応するリンクサーバーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `SEATTLE3` 、のローカルインスタンスと互換性のある照合順序になるように構成し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>参照  
 [分散クエリストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
