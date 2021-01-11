---
title: コマンドの実行
description: Microsoft SqlClient Data Provider for SQL Server の `Command` オブジェクトについて、またそれを使用してデータ ソースに対してクエリとコマンドを実行する方法について説明します。
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 772ecef470b69a34e4bd4b0eba2ca60255657eaf
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771424"
---
# <a name="executing-a-command"></a>コマンドの実行

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server には、<xref:System.Data.Common.DbCommand> から継承される <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトがあります。 このオブジェクトでは、次の表に示すように、コマンドの種類と必要な戻り値に基づいて各コマンドを実行するためのメソッドが公開されています。

|コマンド|戻り値|  
|-------------|------------------|  
|`ExecuteReader`|`DataReader` オブジェクトを返します。|  
|`ExecuteScalar`|単一のスカラー値を返します。|  
|`ExecuteNonQuery`|行を一切返さないコマンドを実行します。|  
|`ExecuteXMLReader`|<xref:System.Xml.XmlReader> を返します。 `SqlCommand` オブジェクトでのみ使用できます。|

厳密に型指定された各コマンド オブジェクトは、次の表に示す <xref:System.Data.CommandType> 列挙値をサポートしています。これらの列挙値を使用してコマンド文字列の解釈方法を指定できます。

|CommandType|説明|
|-----------------|-----------------|  
|`Text`|データ ソース側で実行されるステートメントを定義する SQL コマンド。|  
|`StoredProcedure`|ストアド プロシージャの名前。 呼び出す `Parameters` メソッドに関係なく、コマンドの `Execute` プロパティを使用して入力パラメーターと出力パラメーターにアクセスし、戻り値を取得できます。|  
|`TableDirect`|テーブルの名前。|

> [!IMPORTANT]
> `ExecuteReader` を使用した場合は、`DataReader` を閉じるまで戻り値および出力パラメーターにアクセスすることはできません。

## <a name="example"></a>例

<xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを作成し、そのプロパティを設定することによってストアド プロシージャを実行するコード サンプルを次に示します。 ストアド プロシージャへの入力パラメーターは、<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトを使って指定します。 このコマンドを <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReader%2A> メソッドで実行し、<xref:Microsoft.Data.SqlClient.SqlDataReader> からの出力をコンソール ウィンドウに表示します。

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](~/../sqlclient/doc/samples/SqlCommand_StoredProcedure.cs#1)]

### <a name="troubleshooting-commands"></a>コマンドのトラブルシューティング

[!INCLUDE[appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

Microsoft SqlClient Data Provider for SQL Server では、失敗したコマンド実行に関連する断続的な問題を検出できるようにするための **パフォーマンス カウンター** が追加されています。 詳細については、「[SqlClientのパフォーマンス カウンター](performance-counters.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [コマンドとパラメーター](commands-parameters.md)
- [DataAdapter と DataReader](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
