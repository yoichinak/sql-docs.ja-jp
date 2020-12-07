---
description: トランザクション処理
title: トランザクション処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: rothja
ms.author: jroth
ms.openlocfilehash: bde1338e56f4685359f8d1260b36c39a24455083
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979333"
---
# <a name="transaction-processing"></a>トランザクション処理
*トランザクション*は、接続全体で実行される一連のデータアクセス操作の開始と終了を区切ります。 データソースのトランザクション機能に従って、 **Connection** オブジェクトを使用してトランザクションを作成および管理することもできます。 たとえば、Microsoft OLE DB Provider for SQL Server を使用して Microsoft SQL Server 上のデータベースにアクセスする場合、実行するコマンドに対して複数の入れ子になったトランザクションを作成できます。  
  
 ADO では、トランザクションの操作によって発生したデータソースへの変更が、正常にまとめられているかまったくないかを確認します。  
  
 トランザクションをキャンセルした場合、またはいずれかの操作が失敗した場合、トランザクション内のいずれの操作も行われなかった場合と同じ結果になります。 データソースは、トランザクションが開始される前の状態のままになります。  
  
 ADO には、トランザクションを制御するための次のメソッドが用意されています。 **BeginTrans**、 **CommitTrans**、および **RollbackTrans**です。 ソースデータに対して行われた一連の変更を1つの単位として保存またはキャンセルする場合は、これらのメソッドを **接続** オブジェクトと共に使用します。 たとえば、勘定科目間で通貨を転送する場合は、1つから金額を減算し、同じ金額をもう一方に追加します。 どちらかの更新が失敗した場合、アカウントの残高はなくなります。 開いているトランザクション内でこれらの変更を行うことによって、すべての変更が行われないようにすることができます。  
  
> [!NOTE]
>  すべてのプロバイダーがトランザクションをサポートするわけではありません。 プロバイダーがトランザクションをサポートしていることを示す、プロバイダー定義プロパティ "**TRANSACTION DDL**" が **接続** オブジェクトの [プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md) コレクションに表示されていることを確認します。 プロバイダーがトランザクションをサポートしていない場合、これらのメソッドのいずれかを呼び出すと、エラーが返されます。  
  
 **BeginTrans**メソッドを呼び出した後、このプロバイダーは、 **CommitTrans**または**RollbackTrans**を呼び出してトランザクションを終了するまで、加えた変更を即座にコミットしなくなります。  
  
 **CommitTrans**メソッドを呼び出すと、接続時に開いているトランザクション内で行われた変更が保存され、トランザクションが終了します。 **RollbackTrans**メソッドを呼び出すと、開いているトランザクション内で行われたすべての変更が元に戻され、トランザクションが終了します。 開いているトランザクションが存在しないときにいずれかのメソッドを呼び出すと、エラーが生成されます。  
  
 **接続**オブジェクトの[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティによっては、 **CommitTrans**メソッドまたは**RollbackTrans**メソッドを呼び出すと、新しいトランザクションが自動的に開始される場合があります。 **Attributes**プロパティが**adXactCommitRetaining**に設定されている場合、プロバイダーは、 **CommitTrans**呼び出しの後に新しいトランザクションを自動的に開始します。 **Attributes**プロパティが**Adxactabortretaining**に設定されている場合、プロバイダーは、呼び出しの後**RollbackTrans**に新しいトランザクションを自動的に開始します。  
  
## <a name="transaction-isolation-level"></a>トランザクション分離レベル  
 **接続**オブジェクトのトランザクションの分離レベルを設定するには、 **IsolationLevel**プロパティを使用します。 この設定は、次に [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) メソッドを呼び出したときまで有効になりません。 要求した分離レベルが使用できない場合、プロバイダーは次に高い分離レベルを返すことができます。 有効な値の詳細については、ADO プログラマーリファレンスの **IsolationLevel** プロパティを参照してください。  
  
## <a name="nested-transactions"></a>入れ子になったトランザクション  
 入れ子になったトランザクションをサポートするプロバイダーの場合、開いているトランザクション内で **BeginTrans** メソッドを呼び出すと、新しい入れ子になったトランザクションが開始されます。 戻り値は、入れ子のレベルを示します。戻り値 "1" は、最上位レベルのトランザクションを開いている (つまり、トランザクションが別のトランザクション内で入れ子になっていない) ことを示します。 "2" は、第2レベルのトランザクション (最上位レベルのトランザクション内で入れ子にされたトランザクション) が開かれたことを **CommitTrans**または**RollbackTrans**を呼び出すと、最後に開かれたトランザクションのみに影響します。上位レベルのトランザクションを解決する前に、現在のトランザクションを閉じるかロールバックする必要があります。
