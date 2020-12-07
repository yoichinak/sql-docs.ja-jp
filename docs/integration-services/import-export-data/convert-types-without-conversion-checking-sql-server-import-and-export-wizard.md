---
description: '[変換の確認を伴わない型変換] (SQL Server インポートおよびエクスポート ウィザード)'
title: 変換の確認を伴わない型変換 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.nomappingfile.f1
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5d7c53d4117d7634b6651069260c289657f82315
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88391468"
---
# <a name="convert-types-without-conversion-checking-sql-server-import-and-export-wizard"></a>[変換の確認を伴わない型変換] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  指定したクエリをコピーまたは確認する既存のテーブルやビューを選択すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインポートおよびエクスポート ウィザードに **[変換の確認を伴わない型変換]** が表示される場合があります。 ウィザードで、変換元と変換先でデータ型のマップに必要なデータ型変換およびマッピング ファイルを 1 つ以上特定できない場合、このページが表示されます。 このページには、不足している事項を把握するために役立つ情報が掲載されています。
  
 データ型の変換が成功するかどうかはわからないまま継続するには、 **[次へ]** をクリックします。 それ以外の場合は、 **[戻る]** をクリックして選択内容を変更するか、 **[キャンセル]** をクリックしてウィザードを終了します。

## <a name="screen-shot-of-the-convert-types-page"></a>[型変換] ページのスクリーン ショット  
  
次のスクリーンショットは、ウィザードの **[変換の確認を伴わない型変換]** ページの例です。

![型変換](../../integration-services/import-export-data/media/convert-types.png)

問題は、選択した変換先のデータ型をマップするマッピング ファイルを、ウィザードが見つけることができないことです。

このページの情報には、不足しているマッピング ファイルの名前が含まれていません。 指定したデータ プロバイダーのファイルが存在するかどうかをウィザードは把握していないため、ウィザードは不足しているファイルの名前を提供できません。

## <a name="whats-next"></a>次の手順  
 **[次へ]** をクリックしてデータ型の変換が成功するかどうかはわからないまま継続する場合、次のページは **[パッケージの保存および実行]** です。 このページでは、コピー操作をすぐに実行するかどうかを指定します。 構成によっては、ウィザードによって作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを保存して、それをカスタマイズし、後から再利用することができます。 詳細については、 [パッケージの保存および実行](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)に関するページを参照してください。  

## <a name="see-also"></a>関連項目
[SQL Server インポートおよびエクスポート ウィザードのデータ型マッピング](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
