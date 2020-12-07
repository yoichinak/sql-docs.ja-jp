---
description: 変換オプションと移行オプションの設定 (アップグレード)
title: 変換オプションと移行オプションの設定 (アップグレード)Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cc9a5328095f2ef839eb0c9617798299e46371fd
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987685"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>変換オプションと移行オプションの設定 (アップグレード)
SSMA プロジェクトごとに、プロジェクトレベルのオプションを設定できます。 これらのオプションでは、オブジェクトの変換方法、データの移行方法、およびソースデータ型とターゲットデータ型のマッピング方法を指定します。 オブジェクトをに変換したり、データを SQL Azure または SQL Azure に移行したりする前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、構成オプションがプロジェクトに適していることを確認してください。  
  
## <a name="configuration-options-and-modes"></a>構成オプションとモード  
SSMA には、4セットの構成設定と4つのモードがあります。既定、オプティミスティック、Full、および Custom です。 ほとんどのユーザーには、既定のモードを使用することをお勧めします。 単純な変換にはオプティミスティックモードを使用します。 すべてのメッセージを表示する場合は、フルモードを使用します。 カスタムモードでは、オプションを設定します。  
  
設定については、このドキュメントの「ユーザーインターフェイスリファレンス」セクションで説明します。 各モードでの設定と設定の適用方法の詳細については、次のトピックを参照してください。  
  
-   [プロジェクトの設定 (変換)](./project-settings-conversion-accesstosql.md)  
  
-   [プロジェクトの設定 (移行)](./project-settings-migration-accesstosql.md)  
  
-   [プロジェクトの設定 (GUI)](../sybase/project-settings-gui-sybasetosql.md)  
  
-   [プロジェクトの設定 (型のマッピング)](./project-settings-type-mapping-accesstosql.md)  
  
-   [プロジェクトの設定 (SQL Azure)](./project-settings-azure-sql-db-accesstosql.md)  
  
## <a name="setting-project-options"></a>プロジェクト オプションの設定  
SSMA では、すべてのプロジェクトの既定の設定を構成できます。 これらの設定は、SSMA 構成ファイルに保存され、作成した新しいプロジェクトに適用されます。  
  
**既定のプロジェクトオプションを設定するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  [ **既定のプロジェクト設定** ] ダイアログボックスで、次のいずれかの操作を行います。  
  
    -   [移行 **先のバージョン** ] ドロップダウンから表示または変更する設定が必要な移行プロジェクトの種類を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックしてから、[変換] または [ **移行] または [SQL Azure**] を選択します。  
  
        > [!NOTE]  
        > SQL Azure オプションは、作成されたプロジェクトの種類が SQL Azure 場合にのみ、 **[全般** ] タブで使用できます。  
  
    -   定義済みのモードを選択するには、[**モード**] ボックスの一覧で [**既定**]、[**オプティミスティック**]、または [**完全**] を選択します。  
  
    -   カスタムモードを指定するには、[**モード**] ボックスで [**カスタム**] を選択し、左ペインでオプションを選択します。次に、右ペインで設定または値をクリックし、新しい設定または値を選択または入力します。  
  
3.  **[OK]** をクリックして設定を保存します。  
  
また、現在のプロジェクトの設定をカスタマイズすることもできます。 これらの設定は、現在のプロジェクトファイルに保存されます。  
  
**現在のプロジェクトの設定をカスタマイズするには**  
  
1.  [ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックします。  
  
2.  [ **プロジェクトの設定** ] ダイアログボックスで、次のいずれかの操作を行います。  
  
    -   定義済みのモードを選択するには、[**モード**] ボックスの一覧で [**既定**]、[**オプティミスティック**]、または [**完全**] を選択します。  
  
    -   カスタムモードを指定するには、[**モード**] ボックスで [**カスタム**] を選択し、左ペインでオプションを選択します。次に、右ペインで設定または値をクリックし、新しい設定または値を選択または入力します。  
  
3.  **[OK]** をクリックして設定を保存します。  
  
## <a name="next-steps"></a>次の手順  
移行の次のステップは、プロジェクトのニーズによって異なります。  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするには、「[ソースとターゲットのデータ型のマッピング](mapping-source-and-target-data-types-accesstosql.md)」を参照してください。  
  
-   ソースデータベースとターゲットデータベースのマッピングをカスタマイズするには、「[ソースデータベースとターゲットデータベースのマッピング](mapping-source-and-target-databases-accesstosql.md)」を参照してください。  
  
-   それ以外の場合は、Access データベースオブジェクト定義を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure オブジェクト定義に変換できます。 詳細については、「 [Access データベースオブジェクトの変換](converting-access-database-objects-accesstosql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
