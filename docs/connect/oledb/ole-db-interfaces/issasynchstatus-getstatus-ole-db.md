---
title: ISSAsynchStatus::GetStatus (OLE DB ドライバー) | Microsoft Docs
description: ISSAsynchStatus::GetStatus メソッドが OLE DB Driver for SQL Server で非同期に実行されている操作のステータスを返す方法について説明します。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b9d4e6011dac6555db090f5c4d2a68470746a60
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862192"
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  非同期に実行されている操作の状態を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>引数  
 *hChapter*[in]  
 チャプター ハンドル。 ポーリングされるオブジェクトが行セット オブジェクトではないか、操作がチャプターに適用されない場合は、DB_NULL_HCHAPTER に設定する必要があります。プロバイダーでは、この設定が無視されます。  
  
 *eOperation*[in]  
 非同期状態が要求されている操作。 次の値を使用する必要があります。  
  
 DBASYNCHOP_OPEN - コンシューマーは、行セットを開くか行セットにデータを設定する非同期操作に関する情報、またはデータ ソース オブジェクトを初期化する非同期操作に関する情報を要求します。 プロバイダーが URL の直接バインドをサポートする OLE DB 2.5 に準拠したプロバイダーの場合、コンシューマーは、データ ソース、行セット、行、またはストリーム オブジェクトの初期化やデータ設定の非同期操作に関する情報を要求します。  
  
 *pulProgress*[out]  
 *pulProgressMax* パラメーターで示される予想最大値と比較した、現在の非同期操作の進行状況を返すメモリへのポインター。 *pulProgress* の詳細については、*peAsynchPhase* の説明を参照してください。  
  
 *pulProgress* に NULL ポインターを指定すると、進行状況は返されません。  
  
 *pulProgressMax*[out]  
 *pulProgress* パラメーターの予想最大値を返すメモリへのポインター。 この値は、このメソッドを呼び出すたびに変化することがあります。 *pulProgressMax* の詳細については、*peAsynchPhase* の説明を参照してください。  
  
 *pulProgressMax* に NULL ポインターを指定すると、予想最大値は返されません。  
  
 *peAsynchPhase*[out]  
 非同期操作の進行状況に関する詳細情報を返すメモリへのポインター。 有効な値は、次のとおりです。  
  
 DBASYNCHPHASE_INITIALIZATION - オブジェクトは初期化フェーズにあります。 引数 *pulProgress* と *pulProgressMax* は、完了の推定比率を示します。 オブジェクトはまだ完全に具体化されていません。 そのため、他のインターフェイスの呼び出しを試みると失敗したり、このオブジェクトのすべてのインターフェイスを使用できない場合があります。 行を更新、削除、または挿入するコマンドに対して **ICommand::Execute** を呼び出すことにより非同期操作が実行された場合、および *cParamSets* が 1 より大きい場合、*pulProgress* と *pulProgressMax* は、パラメーターの 1 つのセットの進行状況か、パラメーター セットの配列全体の進行状況を示します。  
  
 DBASYNCHPHASE_POPULATION - オブジェクトは作成フェーズにあります。 行セットは完全に初期化されていて、オブジェクトのすべてのインターフェイスを使用できますが、まだ行セットに追加されていない行が存在する場合があります。 *pulProgress* と *pulProgressMax* は、設定した行数に基づくこともできますが、通常は、行セットの設定に必要な時間または作業に基づきます。 そのため、呼び出し元では最終的な行数ではなく、処理にかかる時間の大まかな推定値としてこの情報を使用する必要があります。 このフェーズが返されるのは、行セットの設定中のみです。データ ソース オブジェクトの初期化中や、行を更新、削除、または挿入するコマンドの実行により返されることはありません。  
  
 DBASYNCHPHASE_COMPLETE - オブジェクトのすべての非同期処理が完了しました。 **ISSAsynchStatus::GetStatus** メソッドにより、操作の結果を示す HRESULT が返されます。 通常、この HRESULT は、同期をとって操作を呼び出した場合に返される HRESULT です。 行を更新、削除、または挿入するコマンドに対して **ICommand::Execute** を呼び出すことにより非同期操作が実行された場合、*pulProgress* と *pulProgressMax* は、そのコマンドで処理された行の合計数と等しくなります。 *cParamSets* が 1 より大きい場合、この値は、コマンドの実行で指定したすべてのパラメーター セットによって処理された行の合計数になります。 *peAsynchPhase* に NULL ポインターを指定すると、状態コードは返されません。  
  
 DBASYNCHPHASE_CANCELED - オブジェクトの非同期処理が中止されました。 **ISSAsynchStatus::GetStatus** メソッドにより、DB_E_CANCELED が返されます。 行を更新、削除、または挿入するコマンドに対して **ICommand::Execute** を呼び出すことにより非同期操作が実行された場合、*pulProgress* は、そのコマンドに指定したすべてのパラメーター セットによってキャンセル前に処理された行の合計数と等しくなります。  
  
 *ppwszStatusText*[in/out]  
 操作に関する詳細情報を保持するメモリへのポインター。 プロバイダーは、この値を使用して操作の異なる要素 (アクセス中のさまざまなリソースなど) を区別できます。 この文字列は、データ ソース オブジェクトの DBPROP_INIT_LCID プロパティに従ってローカライズされます。  
  
 *ppwszStatusText* の入力値が NULL 以外の場合、プロバイダーは *ppwszStatusText* で識別される特定の要素に関連する状態を返します。 *ppwszStatusText* が *eOperation* の要素を示していない場合、*pulProgress* と *pulProgressMax* に同じ値を設定して S_OK を返します。 プロバイダーでテキスト識別子に基づいて要素を区別しない場合、*ppwszStatusText* に NULL を設定し、操作全体に関する情報を返します。要素を区別する場合、*ppwszStatusText* の入力値が NULL 以外であると、プロバイダーでは *ppwszStatusText* が処理されなくなります。  
  
 *ppwszStatusText* の入力値が NULL の場合、*ppwszStatusText* に操作の詳細を示す値を設定します。詳細情報が取得できない場合や、**ISSAsynchStatus::GetStatus** メソッドからエラーが返される場合は、NULL を設定します。 *ppwszStatusText* の入力値が NULL の場合、状態文字列用のメモリを割り当て、そのメモリのアドレスを返します。 コンシューマーでは、この文字列が不要になった時点で、**IMalloc::Free** を使用してこのメモリを解放します。  
  
 *ppwszStatusText* の入力値が NULL の場合、状態文字列は返されず、操作の要素に関する情報か、操作の概要情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドから正常に値が返されました。  
  
-   *peAsynchPhase* が DBASYNCHPHASE_INITIALIZATION の場合、オブジェクトはまだ完全に初期化されていません。そのため、他のインターフェイスの呼び出しを試みると失敗したり、このオブジェクトのすべてのインターフェイスを使用できない場合があります。  
  
-   *peAsynchPhase* が DBASYNCHPHASE_POPULATION の場合、行セットは完全に初期化されていて、オブジェクトのすべてのインターフェイスを使用できますが、まだ行セットに追加されていない行が存在する場合があります。  
  
-   *peAsynchPhase* が DBASYNCHPHASE_COMPLETE の場合、オブジェクトのすべての非同期操作は完了しています。 オブジェクトは、完全に初期化され、データが設定されています。  
  
 DB_E_CANCELED  
 行セットの設定中に非同期操作が取り消されたことを示します。 この場合、データ設定操作は停止されますが、既に設定した行セットの行は有効なままです。  
  
 また、データ ソース オブジェクトの初期化中に非同期処理が取り消されたことを示している場合もあります。 この場合、データ ソース オブジェクトは初期化されていない状態です。  
  
 E_INVALIDARG  
 *hChapter* パラメーターが正しくありません。  
  
 E_UNEXPECTED  
 **IDBInitialize::Initialize** が呼び出されていないデータ ソース オブジェクトに対して **ISSAsynchStatus::GetStatus** メソッドが呼び出されたことを示します。  
  
 また、**ITransaction::Commit** や **ITransaction::Abort** が呼び出された行セットに対して **ISSAsynchStatus::GetStatus** メソッドが呼び出されたことを示している場合もあります。この場合、オブジェクトはゾンビ状態になります。  
  
 初期化フェーズで非同期に取り消された行セットに対して **ISSAsynchStatus::GetStatus** メソッドが呼び出された場合もこの値が返されます。 行セットはゾンビ状態になります。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。  
  
## <a name="remarks"></a>解説  
 **ISSAsynchStatus::GetStatus** メソッドの動作は、**IDBAsynchStatus::GetStatus** メソッドとまったく同じです。ただし、データ ソース オブジェクトの初期化が中止された場合は、DB_E_CANCELED ではなく E_UNEXPECTED が返されます ([ISSAsynchStatus::WaitForAsynchCompletion](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) の場合は DB_E_CANCELED が返されます)。 これは、初期化の中止後、追加の初期化操作が試行される場合に備えて、データ ソース オブジェクトの状態が通常のゾンビ状態のままにならないためです。  
  
 行セットを初期化またはデータ設定する非同期操作では、このメソッドをサポートする必要があります。  
  
 **ISSAsynchStatus::GetStatus** では、上記の戻り値に加えて、非同期操作を開始するメソッドから返されることになる、操作の成功または失敗を示す HRESULT を返すことができます。  
  
 一部の非同期操作では、"完了" または "未完了" 以外の状態を返すことができません。 これらの操作では、*pulProgressMax* の値を 1 に設定する必要があります。これにより、推定値の粒度がすべて完了したか、まったく処理されていないかの状態になるので、0/1 または 1/1 が返されます。  
  
 プロバイダーでは、タスクの完了の度合いに応じて推定値が向上する場合、これを *pulProgressMax* に反映して、連続した呼び出しでこの値が変化したり、場合のよっては前回よりも少ない比率を返すこともあります。  
  
 プロバイダーは、より正確な値を保証することが義務付けられているわけではありませんが、可能な場合は妥当な推定完了率を返すように設定されています。 この関数の主な目的は、ユーザーへの進行状況のフィードバックを提供することなので、このような動作によりユーザー インターフェイスの品質が向上します。 非表示で行われる、実行時間が長いタスクに対するフィードバックの品質を向上することで、ユーザーの満足度も向上します。  
  
 初期化されたデータ ソース オブジェクトまたはデータが設定された行セットに対して **ISSAsynchStatus::GetStatus** を呼び出すか、*eOperation* に DBASYNCHOP_OPEN 以外の値を渡すと、*pulProgress* と *pulProgressMax* に同じ値が設定され、S_OK が返されます。 行を更新、削除、または挿入するコマンドの実行により作成されたオブジェクトに対して **ISSAsynchStatus::GetStatus** メソッドを呼び出した場合、*pulProgress* と *pulProgressMax* は、どちらもそのコマンドによって処理された行の合計数を示します。  
  
## <a name="see-also"></a>参照  
 [非同期操作の実行](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
