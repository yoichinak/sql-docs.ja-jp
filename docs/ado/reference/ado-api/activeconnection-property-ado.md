---
description: ActiveConnection プロパティ (ADO)
title: ActiveConnection プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: rothja
ms.author: jroth
ms.openlocfilehash: bc1a54d70639e4e3ff78748b4e04483fcfefafdb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976963"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection プロパティ (ADO)
指定した[コマンド](./command-object-ado.md)、[レコードセット](./recordset-object-ado.md)、または[レコード](./record-object-ado.md)オブジェクトが現在どの[接続](./connection-object-ado.md)オブジェクトに属しているかを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 接続が閉じられている場合は接続の定義を含む**文字列**値、または接続が開いている場合は現在の**接続**オブジェクトを含む**バリアント**を設定または返します。 既定値は null オブジェクト参照です。 [ConnectionString](./connectionstring-property-ado.md)プロパティを参照してください。  
  
## <a name="remarks"></a>解説  
 **ActiveConnection**プロパティを使用して、指定した**コマンド**オブジェクトを実行する**接続**オブジェクトを決定します。指定した**レコードセット**が開かれます。  
  
## <a name="command"></a>command  
 **Command**オブジェクトの場合、 **ActiveConnection**プロパティは読み取り/書き込み可能です。  
  
 このプロパティを開いている**接続**オブジェクトまたは有効な接続文字列に設定する前に**Command**オブジェクトで[Execute](./execute-method-ado-command.md)メソッドを呼び出そうとすると、エラーが発生します。  
  
 **接続**オブジェクトが**ActiveConnection**プロパティに割り当てられている場合は、オブジェクトを開く必要があります。 閉じた接続オブジェクトを割り当てると、エラーが発生します。  
  
### <a name="note"></a>注意  
 **Microsoft Visual Basic****ActiveConnection**プロパティを*Nothing*に設定すると、現在の**接続**から**コマンド**オブジェクトの関連付けが解除され、プロバイダーによって、データソースに関連付けられているすべてのリソースが解放されます。 その後、 **コマンド** オブジェクトを同じまたは別の **接続** オブジェクトに関連付けることができます。 プロバイダーによっては、プロパティを最初に*Nothing*に設定しなくても、プロパティ設定をある接続から別の**接続**に変更することができます。  
  
 **コマンド**オブジェクトの[parameters](./parameters-collection-ado.md)コレクションにプロバイダーによって提供されるパラメーターが含まれている場合、 **ActiveConnection**プロパティを*Nothing*または別の**接続**オブジェクトに設定すると、コレクションはクリアされます。 [パラメーター](./parameter-object.md)オブジェクトを手動で作成し、それを使用して**Command**オブジェクトの**Parameters**コレクションを設定する場合は、 **ActiveConnection**プロパティを*Nothing*または別の**接続**オブジェクトに設定しても、**パラメーター**コレクションはそのまま残ります。  
  
 **Command**オブジェクトが関連付けられている**接続**オブジェクトを閉じると、 **ActiveConnection**プロパティが*Nothing*に設定されます。 閉じている **接続** オブジェクトにこのプロパティを設定すると、エラーが生成されます。  
  
## <a name="recordset"></a>レコードセット  
 Open **recordset**オブジェクト、または[Source](./source-property-ado-recordset.md)プロパティが有効な**Command**オブジェクトに設定されている**レコードセット**オブジェクトの場合、 **ActiveConnection**プロパティは読み取り専用です。 それ以外の場合は、読み取り/書き込みです。  
  
 このプロパティは、有効な **接続** オブジェクトまたは有効な接続文字列に設定できます。 この場合、プロバイダーはこの定義を使用して新しい **接続** オブジェクトを作成し、接続を開きます。 さらに、プロバイダーは、このプロパティを新しい **接続** オブジェクトに設定することにより、 **接続** オブジェクトにアクセスして、エラーの詳細情報を表示したり、その他のコマンドを実行したりすることができます。  
  
 [Open](./open-method-ado-recordset.md)メソッドの*ActiveConnection*引数を使用して**レコードセット**オブジェクトを開くと、 **ActiveConnection**プロパティは引数の値を継承します。  
  
 **Recordset**オブジェクトの**Source**プロパティを有効な**command**オブジェクト変数に設定した場合、**レコードセット**の**ActiveConnection**プロパティは、 **command**オブジェクトの**ActiveConnection**プロパティの設定を継承します。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** クライアント側の **レコードセット** オブジェクトで使用する場合、この *プロパティを設定*できるのは、接続文字列または (Microsoft Visual Basic または Visual Basic Scripting Edition の場合) のみです。  
  
## <a name="record"></a>Record  
 このプロパティは、 **Record** オブジェクトが閉じている場合は読み取り/書き込み可能であり、接続文字列または開いている **接続** オブジェクトへの参照が含まれている場合があります。 このプロパティは、 **Record** オブジェクトが開いていて、開いている **接続** オブジェクトへの参照が含まれている場合に読み取り専用になります。  
  
 **接続**オブジェクトは、**レコード**オブジェクトが URL から開かれたときに暗黙的に作成されます。 **接続**オブジェクトをこのプロパティに割り当てるか、 [open](./open-method-ado-record.md)メソッド呼び出しのパラメーターとして**connection**オブジェクトを使用して、既存の開いている**接続**オブジェクトを含む**レコード**を開きます。 **レコード**が既存の**レコード**またはレコード[セット](./recordset-object-ado.md)から開かれた場合は、その**レコードまたは**レコード**セット**オブジェクトの**接続**オブジェクトに自動的に関連付けられます。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Command オブジェクト (ADO)](./command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record オブジェクト (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Connection オブジェクト (ADO)](./connection-object-ado.md)   
 [ConnectionString プロパティ (ADO)](./connectionstring-property-ado.md)