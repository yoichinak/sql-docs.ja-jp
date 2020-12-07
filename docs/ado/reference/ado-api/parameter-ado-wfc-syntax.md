---
description: Parameter (ADO - WFC 構文)
title: Parameter (ADO-WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
author: rothja
ms.author: jroth
ms.openlocfilehash: 365e843693def4f8a050dbc5f12c4a23768923f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990183"
---
# <a name="parameter-ado---wfc-syntax"></a>Parameter (ADO - WFC 構文)
## <a name="package-commswfcdata"></a>パッケージ com.. wfc. データ  
  
### <a name="constructor"></a>コンストラクター  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>メソッド  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>パラメーターアクセサーメソッド  
 [Parameter](./parameter-object.md)オブジェクトの[Value](./value-property-ado.md)プロパティは、そのオブジェクトのコンテンツを取得または設定します。 コンテンツは、値と複数のデータ型のいずれかを割り当てることができる、バリアント型のオブジェクトで表されます。  
  
 ADO/WFC は、VARIANT オブジェクトを返す**getValue**メソッドを使用して**Value**プロパティを実装します。また、 **setValue**を引数として受け取る setValue メソッドもあります。 バリアントは、Microsoft Visual Basic などの特定の言語では非常に効率的です。  
  
 ADO/WFC は、 **Value**プロパティに加えて、Java データ型を使用して**パラメーター**オブジェクトのコンテンツを取得および設定する*アクセサー*メソッドを提供します。 これらのメソッドのほとんどには、 **get**_datatype_ または **set**_datatype_という形式の名前があります。  
  
 注目すべき例外が1つあります。 **Getnull** プロパティがありません。その代わりに、フィールドが null かどうかを示すブール値を返す **isNull** プロパティがあります。  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>参照  
 [Parameter オブジェクト](./parameter-object.md)