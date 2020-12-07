---
description: Field (ADO - WFC 構文)
title: Field (ADO-WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: rothja
ms.author: jroth
ms.openlocfilehash: b9b35f89911c0b016c52eed00f8165b767968180
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973253"
---
# <a name="field-ado---wfc-syntax"></a>Field (ADO - WFC 構文)
## <a name="package-commswfcdata"></a>パッケージ com.. wfc. データ  
  
### <a name="methods"></a>メソッド  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>プロパティ  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (詳細については、IDataFormat インターフェイスのドキュメントを参照してください)。  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>フィールドアクセサーメソッド  
 [Field](../../../ado/reference/ado-api/field-object.md)オブジェクトの[Value](../../../ado/reference/ado-api/value-property-ado.md)プロパティは、そのオブジェクトのコンテンツを取得または設定します。 コンテンツは、値と複数のデータ型のいずれかを割り当てることができる、バリアント型のオブジェクトで表されます。  
  
 ADO/WFC は、VARIANT オブジェクトを返す**getValue**メソッドを使用して**Value**プロパティを実装します。また、 **setValue**を引数として受け取る setValue メソッドもあります。 バリアントは、Microsoft Visual Basic などの特定の言語では非常に効率的です。  
  
 ADO/WFC は、 **Value**プロパティに加えて、Java データ型を使用して**Field**オブジェクトのコンテンツを取得および設定する*アクセサー*メソッドを提供します。 これらのメソッドのほとんどには、 **get**_datatype_ または **set**_datatype_という形式の名前があります。  
  
 注目すべき例外が2つあります。いずれかの **getObject** メソッドが、指定されたクラスに強制変換されたオブジェクトを返します。 **Getnull**プロパティはありません。その代わりに、フィールドが null かどうかを示すブール値を返す**isNull**プロパティがあります。  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>参照  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)
