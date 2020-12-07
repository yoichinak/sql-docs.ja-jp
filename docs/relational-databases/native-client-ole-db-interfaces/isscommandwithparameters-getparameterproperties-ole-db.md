---
description: 'SQL Server Native Client の ISSCommandWithParameters:: GetParameterProperties (OLE DB)'
title: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a0ec5b9666e5b61bfc018825848ca543e42d38c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490795"
---
# <a name="isscommandwithparametersgetparameterproperties-in-sql-server-native-client-ole-db"></a>SQL Server Native Client の ISSCommandWithParameters:: GetParameterProperties (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SSPARAMPROPS プロパティ セット構造体の配列を返します。各 UDT または XML パラメーターごとに 1 つの SSPARAMPROPS プロパティ セットが返されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>引数  
 *pcParams*[out][in]  
 *prgParamProperties* に返された SSPARAMPROPS 構造体の数を保持するメモリへのポインター。  
  
 *prgParamProperties*[out]  
 SSPARAMPROPS 構造体の配列が返されるメモリへのポインター。 プロバイダーは、構造体にメモリを割り当て、このメモリにアドレスを返します。コンシューマーは、構造が不要になったときに、 **Imalloc:: Free** を使用してこのメモリを解放します。 *PrgParamProperties*の**Imalloc:: Free**を呼び出す前に、コンシューマーは、バリアントに参照型 (BSTR など) が含まれている場合にメモリリークを防ぐために、各 DBPROP 構造体の*Vvalue*プロパティに対して**VariantClear**を呼び出す必要があります。出力時に*Pcparams*がゼロの場合、または DB_E_ERRORSOCCURRED 以外のエラーが発生した場合、プロバイダーはメモリを割り当てず、出力時に*prgParamProperties*が null ポインターであることを保証します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **Getparameterproperties**メソッドは、DB_S_ERRORSOCCURRED と DB_E_ERRORSOCCURED を発生させることができない点を除いて、Core OLE DB **ICommandProperties:: GetProperties**メソッドと同じエラーコードを返します。  
  
## <a name="remarks"></a>解説  
 **Isscommandwithparameters:: GetParameterProperties** は、 **getparameterinfo**に関して一貫して動作します。 [Isscommandwithparameters:: SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)または**setparameterinfo**が呼び出されていないか、または cparams が0と等しい場合に呼び出された場合、 **getparameterinfo**はパラメーター情報を取得し、これを返します。 **Isscommandwithparameters:: setparameterproperties**または**setparameterinfo**が少なくとも1つのパラメーターに対して呼び出されている場合、 **Isscommandwithparameters:: Getparameterproperties**は、 **isscommandwithparameters:: setparameterproperties**が呼び出されたパラメーターに対してのみプロパティを返します。 Isscommandwithparameters:: **getparameterproperties**または**getparameterinfo**の後に Isscommandwithparameters **:: setparameterproperties**を呼び出すと、Isscommandwithparameters:: **getparameterproperties**の後続の呼び出しで、 **isscommandwithparameters:: setparameterproperties**が呼び出されたこれらのパラメーターのオーバーライドされた値が返されます。  
  
 SSPARAMPROPS 構造体は、次のように定義されています。  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|メンバー|説明|  
|------------|-----------------|  
|*iOrdinal*|渡されるパラメーターの序数|  
|*cPropertySets*|*rgPropertySets* 内の DBPROPSET 構造体の数|  
|*rgPropertySets*|DBPROPSET 構造体の配列を返すメモリへのポインター|  
|||

## <a name="see-also"></a>参照  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
