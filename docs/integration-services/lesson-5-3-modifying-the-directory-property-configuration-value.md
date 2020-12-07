---
description: レッスン 5-3:Directory プロパティの構成値の変更
title: 手順 3:Directory プロパティの構成値の変更 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a727a5c8d709e982582c26cff8d6cf09eb44ccc
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88345698"
---
# <a name="lesson-5-3-modify-the-directory-property-configuration-value"></a>レッスン 5-3:Directory プロパティの構成値の変更

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



ここでは、**SSISTutorial.dtsConfig** ファイルに保存されている構成設定を変更し、パッケージ レベル変数 `User::varFolderName` の **Value** プロパティを設定します。 この変数は、Foreach ループ コンテナーの **Directory** プロパティを更新します。 変更後の値は、前の実習で作成した **New Sample Data** フォルダーを参照するようにします。 構成設定を変更し、パッケージを実行すると、構成ファイルの変数の **Directory** プロパティが更新されます。 以前は、**Directory** プロパティ値はパッケージに含まれていました。  
  
## <a name="modify-the-configuration-setting-of-the-directory-property"></a>Directory プロパティの構成設定を変更する  
  
1.  前の実習でパッケージ構成ウィザードを使用して作成した **SSISTutorial.dtsConfig** 構成ファイルを探し、メモ帳などのテキスト エディターで開きます。  
  
2.  前の実習で作成した **New Sample Data** フォルダーのパスに合わせて、 **ConfiguredValue** 要素の値を変更します。 パスは引用符で囲まないでください。 **New Sample Data** フォルダーがドライブのルート レベルにある場合 (**C:\\** など)、更新された XML は次の例のようになります。  
  
    ```
    <?xml version="1.0"?>
    <DTSConfiguration>
      <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFEE1D3FA}" GeneratedDate="6/10/2018 8:16:50 AM"/>
      </DTSConfigurationHeading>
      <Configuration ConfiguredType="Property" 
          Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String">
        <ConfiguredValue>C:\New Sample Data</ConfiguredValue>
      </Configuration>
    </DTSConfiguration>  
    ```

    見出しの情報 **GeneratedBy**、**GeneratedFromPackageID**、**GeneratedDate** は、実際のファイルでは異なるものとなります。 **Configuration** 要素に注目してください。 変数の **Value** プロパティである `User::varFolderName` に、**C:\New Sample Data** が含まれています。  
  
3.  変更を保存し、テキスト エディターを閉じます。  
  
## <a name="go-to-next-task"></a>次のタスクに進む  
[手順 4:レッスン 5 のパッケージをテストする](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
