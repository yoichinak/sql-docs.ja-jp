---
title: 接続イベント
description: データ ソースから情報メッセージを取得し、その状態が変更されたかどうかを判断する接続イベント。
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 5a29de74-acfc-4134-8616-829dd7ce0710
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 67b805e4ec95047b843e6b72ba10dc8fee4688d5
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419823"
---
# <a name="connection-events"></a>接続イベント

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server には、データ ソースから情報メッセージを取得したり、**Connection** の状態が変更されたかどうかを判断したりするために使用できる、2 つのイベントを持った **Connection** オブジェクトがあります。 **Connection** オブジェクトのイベントを次の表に示します。

|event|説明|  
|-----------|-----------------|  
|**InfoMessage**|データ ソースから情報メッセージが返されたときに発生します。 情報メッセージはデータ ソースからのメッセージであり、例外はスローされません。|  
|**StateChange**|**Connection** の状態が変化したときに発生します。|  

## <a name="working-with-the-infomessage-event"></a>InfoMessage イベントの使用

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection> イベントを使用して、SQL Server データ ソースから警告や情報メッセージを取得できます。 重大度レベルが 11 から 16 のエラーがデータ ソースから返されると、例外がスローされます。 <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントを使用して、エラーに関連付けられていないメッセージをデータ ソースから取得することもできます。 Microsoft SQL Server の場合は、重大度レベルが 10 以下のエラーは情報メッセージと見なされ、<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントでキャプチャされます。 詳しくは、「[データベース エンジン エラーの重大度](/sql/relational-databases/errors-events/database-engine-error-severities)」をご覧ください。

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントは <xref:Microsoft.Data.SqlClient.SqlInfoMessageEventArgs> オブジェクトを受け取り、その **Errors** プロパティにはデータ ソースからのメッセージのコレクションが格納されています。 このコレクションの中の **Error** オブジェクトにエラー番号、メッセージ テキスト、およびエラーの原因を問い合わせることができます。 また、Microsoft SqlClient Data Provider for SQL Server には、メッセージの送信元のデータベース、ストアド プロシージャ、および行番号に関する詳細も含まれています。

### <a name="example"></a>例

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントのイベント ハンドラーを追加する方法を次のコード サンプルに示します。

[!code-csharp[SqlConnection_._InfoMessage#1](~/../sqlclient/doc/samples/SqlConnection_InfoMessage_StateChange.cs#1)]

## <a name="handling-errors-as-infomessages"></a>InfoMessages としてのエラー処理

<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントは通常、サーバーが情報メッセージまたは警告メッセージを送信した場合に限り発生します。 ただし、実際にエラーが発生した場合は、サーバーの操作を開始した **ExecuteNonQuery** メソッドまたは **ExecuteReader** メソッドの実行は停止され、例外がスローされます。

サーバーでエラーが発生してもコマンド内の残りのステートメントの処理を続行する場合は、<xref:Microsoft.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A> の <xref:Microsoft.Data.SqlClient.SqlConnection> プロパティを `true` に設定します。 このように設定すると、エラーが発生したとき、接続は例外をスローして処理を中断する代わりに、<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントを発生させます。 クライアント アプリケーションは、このイベントを処理し、エラーに応答できます。

> [!NOTE]
> 重大度レベルが 17 以上のエラーが発生すると、サーバーのコマンド処理が停止します。このエラーは、例外として処理する必要があります。 この場合、<xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> イベントによるエラー処理の方法にかかわらず例外がスローされます。

## <a name="working-with-the-statechange-event"></a>StateChange イベントの使用

**StateChange** イベントは、**Connection** の状態が変化したときに発生します。 **StateChange** イベントは、**OriginalState** プロパティと **CurrentState** プロパティを使用して、**Connection** の状態の変化を判別できる <xref:System.Data.StateChangeEventArgs> を受け取ります。 **OriginalState** プロパティは、**Connection** の状態が変更される前の状態を示す <xref:System.Data.ConnectionState> 列挙型です。 **CurrentState** は、**Connection** の状態が変更された後の状態を示す <xref:System.Data.ConnectionState> 列挙型です。

**StateChange** イベントを使用して **Connection** の状態が変化したときにコンソールにメッセージを出力するコード サンプルを次に示します。

[!code-csharp[SqlConnection_._StateChange#2](~/../sqlclient/doc/samples/SqlConnection_InfoMessage_StateChange.cs#2)]

## <a name="see-also"></a>関連項目

- [データ ソースへの接続](connecting-to-data-source.md)
