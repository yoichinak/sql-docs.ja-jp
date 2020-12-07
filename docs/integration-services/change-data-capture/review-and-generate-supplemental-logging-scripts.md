---
description: 補足ログ スクリプトの確認および生成
title: 補足ログ スクリプトの確認および生成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- scripts
ms.assetid: 5c858ae2-37d6-42e8-a252-7f6ed4e628a7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 77a6b4f11ea2e01f43f1be335fad893ee87f1e90
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88457686"
---
# <a name="review-and-generate-supplemental-logging-scripts"></a>補足ログ スクリプトの確認および生成

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  補足ログを設定する Oracle ソース データベースでスクリプトを実行または再実行するには、 **[スクリプト]** タブを使用します。  
  
 スクリプトを実行する前に、次のいずれかを選択します。  
  
 **[このセッションの変更を含める]**  
 CDC インスタンスに追加された任意の新しいテーブルまたはプロパティ エディターを使用して任意の方法で変更されたテーブルでスクリプトを実行するには、これを選択します。  
  
> [!NOTE]  
>  CDC インスタンスのテーブルが変更されていない場合、Oracle の補足ログ スクリプト領域は空になります。  
  
 **[すべてのテーブルを含める/インスタンスをキャプチャする]**  
 すべてのテーブルでスクリプトを実行し、CDC インスタンス内のインスタンスをキャプチャするには、これを選択します。  
  
 これらのオプションのいずれかを選択したら、補足ログ スクリプトを実行します。  
  
### <a name="to-run-the-supplemental-logging-scripts"></a>補足ログ スクリプトを実行するには  
  
1.  **[スクリプトの実行]** をクリックして、CDC インスタンスに定義されているテーブルで補足ログ スクリプトを実行します。 このスクリプトは、キャプチャされるテーブルに UPDATE 操作のログを記録するときに、必要なすべての列をトランザクション ログに書き込むように Oracle データベースに対して指示します。 通常、このスクリプトは Oracle システム管理者によって検査されて実行されます。  
  
2.  補足ログ スクリプトを実行すると、[スクリプトを実行するための Oracle 資格情報] ダイアログ ボックスが表示されます。このダイアログ ボックスで、有効な Oracle ユーザー名とパスワードを指定します。 適切な Oracle 資格情報を指定する方法については、「 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)」を参照してください。  
  
 必要に応じて、SQL\*Plus を使用してスクリプトを手動で実行することもできます。  
  
### <a name="to-run-the-scripts-manually"></a>スクリプトを手動で実行するには  
  
1.  **[コピー]** をクリックしてスクリプトをクリップボードに貼り付けます。 SQL*Plus を開き、Oracle ソース データベースのディレクトリに移動します。 SQL\*Plus にスクリプトを貼り付けて実行します。  
  
### <a name="to-save-the-supplemental-logging-script-in-a-text-file"></a>補足ログ スクリプトをテキスト ファイルに保存するには  
  
1.  **[名前を付けて保存]** をクリックし、ファイルを保存する場所を参照します。  
  
2.  ファイルに名前を付け、 **[保存]** をクリックしてファイルを保存します。  
  
## <a name="see-also"></a>参照  
 [CDC インスタンスのプロパティを編集する方法](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)  
  
  
