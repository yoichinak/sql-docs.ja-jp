---
description: RAW ファイルのカスタム プロパティ
title: RAW ファイルのカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b1b7f0e1416b20ce641848abe47d3497f7c7b7f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92196404"
---
# <a name="raw-file-custom-properties"></a>RAW ファイルのカスタム プロパティ

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **変換元のカスタム プロパティ**  
  
 RAW ファイル ソースには、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、RAW ファイル ソースのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (列挙)|生データへのアクセスに使用するモード。 可能な値は、 **ファイル名** (0) および **変数からのファイル名** (1) です。 既定値は **ファイル名** (0) です。|  
|FileName|文字列型|ソース ファイルのパスおよびファイル名。|  
  
 RAW ファイル ソースの出力および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [RAW ファイル ソース](../../integration-services/data-flow/raw-file-source.md)」を参照してください。  
  
 **変換先のカスタム プロパティ**  
  
 RAW ファイル変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、RAW ファイル変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (列挙)|FileName プロパティにファイル名を含めるか、またはファイル名が含まれる変数名を含めるかを指定する値。 オプションは、 **ファイル名** (0) および **変数からのファイル名** (1) です。|  
|FileName|文字列型|RAW ファイル変換先が書き込むファイルの名前。|  
|WriteOption|Integer (列挙)|RAW ファイル変換先が、同じ名前の既存のファイルを削除するかどうかを指定する値。 オプションは、 **常に作成する** (0)、 **1 回だけ作成する** (1)、 **切り捨てと追加** (3)、 **追加** (2) です。 このプロパティの既定値は、 **常に作成する** (0) です。|  
  
> [!NOTE]  
>  追加操作では、追加するデータのメタデータが、ファイル内の既存データのメタデータと一致している必要があります。  
  
 RAW ファイル変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [RAW ファイル変換先](../../integration-services/data-flow/raw-file-destination.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
