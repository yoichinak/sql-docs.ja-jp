---
description: プロジェクトの設定 (型のマッピング) (SybaseToSQL)
title: プロジェクトの設定 (型のマッピング) (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 99ab880b69d2c06d462ed42ca0a2529ba6bf7bc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372118"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>プロジェクトの設定 (型のマッピング) (SybaseToSQL)
[ **プロジェクトの設定** ] ダイアログボックスの [型マッピング] ページには、Ssma が Sybase Adaptive Server ENTERPRISE (ASE) データ型をデータ型に変換する方法をカスタマイズする設定が含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[型マッピング] ページは、[ **プロジェクトの設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。  
  
-   すべての今後の SSMA プロジェクトに対して型マッピング設定を指定するには、[ **ツール** ] メニューの [ **既定のプロジェクト設定**] を選択し、[移行先の **バージョン** ] ドロップダウンから表示または変更する設定が必要な [移行プロジェクトの種類] を選択して、左側のウィンドウの下部にある [ **型マッピング** ] を選択します。  
  
-   現在のプロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックし、左側のウィンドウの下部にある [ **型マッピング** ] を選択します。  
  
## <a name="options"></a>オプション  
**ソースの種類**  
マップされた ASE データ型。  
  
**ターゲットの種類**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定された ASE データ型のターゲットデータ型。  
  
既定の SSMA for Sybase の型マッピングについては、次のセクションの表を参照してください。  
  
**追加**  
[マッピング] ボックスの一覧にデータ型を追加する場合にクリックします。  
  
**[編集]**  
[マッピング] ボックスの一覧で選択したデータ型を編集する場合にクリックします。  
  
**Remove**  
クリックすると、選択したデータ型マッピングが [マッピング] ボックスの一覧から削除されます。  
  
**既定値にリセット**  
クリックすると、[型マッピング] の一覧が SSMA の既定値にリセットされます。  
  
## <a name="default-type-mapping"></a>既定の型マッピング  
次の表に、ASE とデータ型の既定の型マッピングを示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
|ASE データ型|SQL Server データ型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**[バイナリ]**|**[バイナリ]**|  
|**バイナリ [ \* ..8000]**|**binary [ \* ]**|  
|**バイナリ [8001.. \* ]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**char varying [ \* ..8000]**|**varchar [ \* ]**|  
|**文字の変化 [8001.. \* ]**|**varchar(max)**|  
|**char [ \* ..8000]**|**char [ \* ]**|  
|**char [8001.. \* ;]**|**varchar(max)**|  
|**記号**|**char**|  
|**文字の変化**|**varchar**|  
|**文字の変化 ( \* ..8000]**|**varchar [ \* ]**|  
|**文字の変化 [8001.. \* ]**|**varchar(max)**|  
|**文字 [ \* ..8000]**|**char [ \* ]**|  
|**文字 [8001.. \* ]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**alpha**|**decimal**|  
|**dec [ \* .. \* ]**|**decimal [ \* ]**|  
|**dec [ \* .. \* ][\*..\*]**|**decimal [ \* ] [ \* ]**|  
|**decimal**|**decimal**|  
|**decimal [ \* .. \* ]**|**decimal [ \* ]**|  
|**decimal [ \* .. \* ][\*..\*]**|**decimal [ \* ] [ \* ]**|  
|**double precision**|**float [53]**|  
|**float**|**float [53]**|  
|**float [ \* ..最大**|**float [24]**|  
|**float [16.. \* ]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**national char**|**nchar**|  
|**national char [ \* ..4000]**|**nchar [ \* ]**|  
|**各国語文字の変化**|**nvarchar**|  
|**national char varying [ \* ..4000]**|**nvarchar [ \* ]**|  
|**national char varying [4001.. \* ]**|**nvarchar(max)**|  
|**national char [4001.. \* ]**|**nvarchar(max)**|  
|**national character**|**nchar**|  
|**national character [ \* ..4000]**|**nchar [ \* ]**|  
|**national 文字 [4001.. \* ]**|**nvarchar(max)**|  
|**各国語文字の変化**|**nvarchar**|  
|**各国語文字の変化 [ \* ..4000]**|**nvarchar [ \* ]**|  
|**各国語文字のさまざまな [4001.. \* ]**|**nvarchar(max)**|  
|**national varchar**|**nvarchar**|  
|**national varchar [ \* ..4000]**|**nvarchar [ \* ]**|  
|**national varchar [4001.. \* ]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar の変化**|**nvarchar**|  
|**nchar の変化 [ \* ..4000]**|**nvarchar [ \* ]**|  
|**nchar の変化 [4001.. \* ]**|**nvarchar(max)**|  
|**nchar [ \* ..4000]**|**nchar [ \* ]**|  
|**nchar [4001.. \* ]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**数値 [ \* .. \* ]**|**数値 [ \* ]**|  
|**数値 [ \* .. \* ][\*..\*]**|**数値 [ \* ] [ \* ]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [ \* ..4000]**|**nvarchar [ \* ]**|  
|**nvarchar [4001.. \* ]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [ \* .. \* ]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**時刻 [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**ユニホーム**|**nchar**|  
|**多様**|**nvarchar**|  
|**さまざまな変更 [ \* ..4000]**|**nvarchar [ \* ]**|  
|**さまざまなバリエーション [4001.. \* ]**|**nvarchar(max)**|  
|**[ \* ..4000]**|**nchar [ \* ]**|  
|**このようにして、[4001.. \* ]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [ \* ..4000]**|**nvarchar [ \* ]**|  
|**univarchar [4001.. \* ]**|**nvarchar(max)**|  
|**符号なし bigint**|**数値 [20] [0]**|  
|**unsigned int**|**bigint**|  
|**unsigned smallint**|**int**|  
|**unsigned tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [ \* ..8000]**|**varbinary [ \* ]**|  
|**varbinary [8001.. \* ]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [ \* ..8000]**|**varchar [ \* ]**|  
|**varchar [8001.. \* ]**|**varchar(max)**|  
  
