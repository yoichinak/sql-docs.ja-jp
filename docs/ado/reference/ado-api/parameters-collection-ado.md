---
description: Parameters コレクション (ADO)
title: Parameters コレクション (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: rothja
ms.author: jroth
ms.openlocfilehash: bad2570c368e469afeb7c69e4f283bdbdfe04674
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990123"
---
# <a name="parameters-collection-ado"></a>Parameters コレクション (ADO)
[Command](./command-object-ado.md)オブジェクトのすべての[パラメーター](./parameter-object.md)オブジェクトを含みます。  
  
## <a name="remarks"></a>解説  
 **Command**オブジェクトには、 **Parameter**オブジェクトで構成される**Parameters**コレクションがあります。  
  
 **Command**オブジェクトの**Parameters**コレクションに対して[Refresh](./refresh-method-ado.md)メソッドを使用すると、 **command**オブジェクトで指定されたストアドプロシージャまたはパラメーター化クエリのプロバイダーパラメーター情報が取得されます。 一部のプロバイダーでは、ストアドプロシージャ呼び出しまたはパラメーター化クエリをサポートしていません。このようなプロバイダーを使用するときに**Parameters**コレクションの**Refresh**メソッドを呼び出すと、エラーが返されます。  
  
 独自の**パラメーター**オブジェクトを定義しておらず、 **Refresh**メソッドを呼び出す前に**Parameters**コレクションにアクセスすると、ADO は自動的にメソッドを呼び出し、コレクションにデータを設定します。  
  
 呼び出すストアドプロシージャやパラメーター化されたクエリに関連付けられているパラメーターのプロパティがわかっている場合は、プロバイダーへの呼び出しを最小化してパフォーマンスを向上させることができます。 [Createparameter](./createparameter-method-ado.md)メソッドを使用して、適切なプロパティ設定を持つ**パラメーター**オブジェクトを作成し、 [Append](./append-method-ado.md)メソッドを使用して**Parameters**コレクションに追加します。 これにより、パラメーター情報のプロバイダーを呼び出さなくても、パラメーター値を設定して返すことができます。 パラメーター情報を提供しないプロバイダーに書き込む場合は、このメソッドを使用してパラメーター **コレクションを** 手動で設定し、パラメーターを使用できるようにする必要があります。 必要に応じて、 [Delete](./delete-method-ado-parameters-collection.md)メソッドを使用して**Parameters**コレクションから**パラメーター**オブジェクトを削除します。  
  
 レコード**セットの** **Parameters**コレクション内のオブジェクトは、**レコードセット**が閉じられたときにスコープから除外されます (したがって使用できなくなります)。  
  
 **コマンド**を使用してストアドプロシージャを呼び出すと、ストアドプロシージャの戻り値/出力パラメーターが次のように取得されます。  
  
1.  パラメーターのないストアドプロシージャを呼び出す場合は、 **Command**オブジェクトの**Execute**メソッドを呼び出す前に、 **parameters**コレクションの**Refresh**メソッドを呼び出す必要があります。  
  
2.  パラメーターを指定してストアドプロシージャを呼び出し、 **パラメーターコレクションに** **Append**を指定してパラメーターを明示的に追加する場合、戻り値/出力パラメーターを **parameters** コレクションに追加する必要があります。 戻り値は、最初に **Parameters** コレクションに追加する必要があります。 他のパラメーターを定義の順序で**parameters**コレクションに追加するには、 **Append**を使用します。 たとえば、ストアドプロシージャ SPWithParam には2つのパラメーターがあります。 最初のパラメーターである *Inparam*は、adVarChar (20) として定義されている入力パラメーターであり、2番目のパラメーターである *Outparam*は、adVarChar (20) として定義された出力パラメーターです。 戻り値/出力パラメーターを取得するには、次のコードを使用します。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  パラメーターを使用してストアドプロシージャを呼び出し、 **parameters コレクションで** **Item**メソッドを呼び出すことによってパラメーターを構成する場合は、ストアドプロシージャの戻り値/出力パラメーターを**parameters**コレクションから取得できます。 たとえば、ストアドプロシージャ SPWithParam には2つのパラメーターがあります。 最初のパラメーターである *Inparam*は、adVarChar (20) として定義されている入力パラメーターであり、2番目のパラメーターである *Outparam*は、adVarChar (20) として定義された出力パラメーターです。 戻り値/出力パラメーターを取得するには、次のコードを使用します。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 ここでは、次のトピックについて説明します。  
  
-   [Parameters コレクションのプロパティ、メソッド、およびイベント](./parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Append メソッド (ADO)](./append-method-ado.md)   
 [CreateParameter メソッド (ADO)](./createparameter-method-ado.md)   
 [Parameter オブジェクト](./parameter-object.md)