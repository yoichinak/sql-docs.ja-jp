---
description: DataSpace (ADO - WFC 構文)
title: 領域スペース (ADO-WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: rothja
ms.author: jroth
ms.openlocfilehash: 40207634f4111852bc280823826c108c49fde070
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100034442"
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (ADO - WFC 構文)
すべてのクライアントアプリケーション要求 (*progid*) と通信プロトコルとサーバー (*接続*) を処理するビジネスオブジェクトを指定する場合は、このよう **に、このクラスの** **createObject** メソッドを指定します。 **createObject** は、サーバーを表す [objectproxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) オブジェクトを返します。  
  
## <a name="package-commswfcdata"></a>パッケージ com.. wfc. データ  
  
### <a name="constructor"></a>コンストラクター  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>メソッド  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>参照  
 [DataSpace オブジェクト (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)
