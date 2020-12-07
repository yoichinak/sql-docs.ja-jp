---
description: RightsEnum
title: 右 Senum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: rothja
ms.author: jroth
ms.openlocfilehash: be2bd513cf41247fd6ce5c8f1172353557287144
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983413"
---
# <a name="rightsenum"></a>RightsEnum
オブジェクトのグループまたはユーザーの権限または権限を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**Adall の作成**|16384 (&H4000)|このユーザーまたはグループには、この種類の新しいオブジェクトを作成する権限があります。|  
|**Adall の削除**|65536 (&H10000)|ユーザーまたはグループには、オブジェクトからデータを削除する権限が与えられています。 **テーブル**などのオブジェクトの場合、ユーザーはレコードからデータ値を削除する権限を持っています。|  
|**Adの削除**|256 (&H100)|ユーザーまたはグループには、カタログからオブジェクトを削除する権限があります。 たとえば、 **テーブル** は DROP TABLE SQL コマンドで削除できます。|  
|**Adexclusive 排他**|512 (&H200)|ユーザーまたはグループは、オブジェクトに排他的にアクセスする権限を持っています。|  
|**Adall の実行**|536870912 (&H20000000)|このユーザーまたはグループには、オブジェクトを実行する権限があります。|  
|**Adfull フル**|268435456 (&H10000000)|ユーザーまたはグループは、オブジェクトに対するすべての権限を持っています。|  
|**Adの右挿入**|32768 (&H8000)|このユーザーまたはグループには、オブジェクトを挿入する権限があります。 **テーブル**などのオブジェクトの場合、ユーザーにはテーブルにデータを挿入する権限があります。|  
|**Adall Maximumallowed**|33554432 (&H2000000)|このユーザーまたはグループには、プロバイダーが許可するアクセス許可の最大数が設定されています。 特定の権限は、プロバイダに依存します。|  
|**Adall なし**|0|このユーザーまたはグループには、オブジェクトに対する権限がありません。|  
|**Adread-only の読み取り**|-2147483648 (&H80000000)|このユーザーまたはグループには、オブジェクトを読み取る権限があります。 [テーブル](./table-object-adox.md)などのオブジェクトの場合、ユーザーはテーブル内のデータを読み取る権限を持っています。|  
|**adRightReadDesign**|1024 (&H400)|ユーザーまたはグループには、オブジェクトのデザインを読み取るためのアクセス許可があります。|  
|**adRightReadPermissions**|131072 (&H20000)|ユーザーまたはグループは、カタログ内のオブジェクトに対する特定の権限を表示できますが、変更することはできません。|  
|**Adall リファレンス**|8192 (&H2000)|このユーザーまたはグループには、オブジェクトを参照する権限があります。|  
|**Ada の更新**|1073741824 (&H40000000)|このユーザーまたはグループには、オブジェクトを更新する権限があります。 **テーブル**などのオブジェクトの場合、ユーザーはテーブル内のデータを更新する権限を持っています。|  
|**Adall Withgrant**|4096 (&H1000)|ユーザーまたはグループは、オブジェクトに対する権限を許可する権限を持っています。|  
|**adRightWriteDesign**|2048 (&H800)|ユーザーまたはグループには、オブジェクトのデザインを変更する権限があります。|  
|**adRightWriteOwner**|524288 (&H80000)|ユーザーまたはグループは、オブジェクトの所有者を変更する権限を持っています。|  
|**adRightWritePermissions**|262144 (&H40000)|ユーザーまたはグループは、カタログ内のオブジェクトに対する特定の権限を変更できます。|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [GetPermissions メソッド (ADOX)](./getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [SetPermissions メソッド (ADOX)](./setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::