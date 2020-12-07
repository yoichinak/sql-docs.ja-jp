---
description: Provider プロパティ (ADO)
title: Provider プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c3f45e8652568bd0440121e27ee6ee0c116e676
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989913"
---
# <a name="provider-property-ado"></a>Provider プロパティ (ADO)
[接続](./connection-object-ado.md)オブジェクトのプロバイダーの名前を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 プロバイダー名を示す **文字列** 値を設定または返します。  
  
## <a name="remarks"></a>解説  
 **プロバイダー**のプロパティを使用して、接続のプロバイダーの名前を設定または取得します。 このプロパティは、 [connectionstring](./connectionstring-property-ado.md)プロパティの内容、または[Open](./open-method-ado-connection.md)メソッドの*connectionstring*引数によって設定することもできます。ただし、 **Open**メソッドを呼び出しているときに複数の場所でプロバイダーを指定すると、予期しない結果になる可能性があります。 プロバイダーが指定されていない場合、プロパティは既定で MSDASQL ([Microsoft OLE DB provider FOR ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)) に設定されます。  
  
 **プロバイダー**プロパティは、接続が閉じられている場合は読み取り/書き込みが、開いている場合は読み取り専用になります。 **接続オブジェクトを**開くか、**接続**オブジェクトの[Properties](./properties-collection-ado.md)コレクションにアクセスするまで、この設定は有効になりません。 設定が有効でない場合は、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Provider および DefaultDatabase プロパティの例 (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider および DefaultDatabase プロパティの例 (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [付録 A: プロバイダー](../../guide/appendixes/appendix-a-providers.md)