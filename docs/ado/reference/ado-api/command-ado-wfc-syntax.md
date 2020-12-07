---
description: Command (ADO - WFC 構文)
title: Command (ADO-WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
author: rothja
ms.author: jroth
ms.openlocfilehash: b9a79d343458969fcfdc72979f1b413f9b2a8742
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975243"
---
# <a name="command-ado---wfc-syntax"></a>Command (ADO - WFC 構文)
## <a name="package-commswfcdata"></a>パッケージ com.. wfc. データ  
  
### <a name="constructor"></a>コンストラクター  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>メソッド  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 **Executeupdate**メソッドは、特定のパラメーターを使用して基になる ADO **execute**メソッドを呼び出す特殊なケースメソッドです。 **Executeupdate**メソッドでは、**レコードセット**オブジェクトの戻りがサポートされていないため、 **execute**メソッドの*options*パラメーターは**AdoEnums.Executeoptions**を使用して変更されます。 **Execute**メソッドが完了すると、更新された*RecordsAffected*パラメーターが**executeupdate**メソッドに戻されます。このメソッドは、最後に**int**として返されます。  
  
### <a name="properties"></a>プロパティ  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>参照  
 [Command オブジェクト (ADO)](./command-object-ado.md)