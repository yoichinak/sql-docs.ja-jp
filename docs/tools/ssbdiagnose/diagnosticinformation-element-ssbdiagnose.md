---
title: diagnosticinformation 要素
description: SQL Server では、DiagnosticInformation は、ssbdiagnostic XML 出力ファイルのルート要素です。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 2824c25e2dcf04d3982332e22ef436b6757497ce
ms.sourcegitcommit: 00be343d0f53fe095a01ea2b9c1ace93cdcae724
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98813108"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 要素 (ssbdiagnose)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**DiagnosticInformation** 要素には、ユーティリティによって検出された診断情報を報告するすべての要素が含まれます。 **DiagnosticInformation** は、 **ssbdiagnostic** XML 出力ファイルのルート要素です。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>要素の属性  
  
|属性|説明|  
|---------------|-----------------|  
|**なし**|該当なし|  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特徴|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|**ssbdiagnose** XML 出力ファイルごとに 1 つ。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[なし] :|  
|**子要素**|[Banner 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Issue 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>解説  
 XML 名前空間の詳細については、「[XML ドキュメントにおける名前空間](/dotnet/standard/data/xml/managing-namespaces-in-an-xml-document)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ssbdiagnose ユーティリティ &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
