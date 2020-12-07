---
description: プロジェクト オプションの設定 (SybaseToSQL)
title: プロジェクトオプションの設定 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: df912a5a58bdcfb2777177bddef80899f31f38c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468727"
---
# <a name="setting-project-options-sybasetosql"></a>プロジェクト オプションの設定 (SybaseToSQL)
SSMA プロジェクトごとに、プロジェクトレベルのオプションを設定できます。 これらのオプションは、オブジェクトの変換、オブジェクトの読み込み、SQL azure、ユーザーインターフェイス、およびデータ移行の設定を指定します。 オブジェクトをに変換したり、データを SQL Azure または SQL Azure に移行したりする前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、構成オプションがプロジェクトに適していることを確認してください。  
  
SSMA では、すべてのプロジェクトの既定のオプションを構成できます。 これらのオプションは、作成するすべての新しいプロジェクトに適用されます。 その後、各プロジェクトのオプションをカスタマイズできます。  
  
## <a name="configuration-options-and-modes"></a>構成オプションとモード  
SSMA には、次の5つのプロジェクト設定があります。  
  
1.  プロジェクト情報  
  
2.  全般 (変換、移行、データの収集)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  型マッピング  
  
また、これらの設定を構成するための4つのモードもあります。  
  
1.  Default  
  
2.  Optimistic  
  
3.  [完全]  
  
4.  Custom  
  
ほとんどのユーザーには、既定のモードを使用することをお勧めします。 オプティミスティックモードでは、現在の Sybase Adaptive Server Enterprise (ASE) 構文がより多く保持されるため、読みやすくなります。 ただし、現在の構文を維持するのは正確ではない可能性があります。 ASE 構文を同等または SQL Azure 構文に変換する必要がある場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、フルモードでは完全な変換が実行されますが、結果のコードは読みにくくなる可能性があります。 カスタムモードでは、オプションを設定します。  
  
設定については、このドキュメントの「ユーザーインターフェイスリファレンス」で説明されています。 各モードでの設定と設定の適用方法の詳細については、次のトピックを参照してください。  
  
-   [プロジェクト設定 &#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [プロジェクト設定 &#40;移行&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [プロジェクト設定 &#40;同期&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [プロジェクト設定 &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [プロジェクト設定 &#40;型マッピング&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [プロジェクト設定 &#40;Azure SQL Database &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>プロジェクト オプションの設定  
SSMA では、すべてのプロジェクトの既定の設定を構成できます。 これらの設定は、SSMA 構成ファイルに保存され、作成した新しいプロジェクトに適用されます。  
  
**既定のプロジェクトオプションを設定するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  [ **既定のプロジェクト設定** ] ダイアログボックスで、次のいずれかの手順を実行します。  
  
    -   [移行 **先のバージョン** ] ドロップダウンから [設定の表示または変更が必要な移行プロジェクトの種類] を選択し、左側のウィンドウの下部にある [全般] をクリックしてから、[変換] または [移行] または [SQL Azure] を選択します。  
  
    -   定義済みのモードを選択するには、[ **モード** ] ボックスの一覧で [ **既定**]、[ **オプティミスティック**]、または [ **完全**] を選択します。  
  
    -   カスタム設定を指定するには、単に新しい設定または値を選択または入力します。  
  
3.  **[OK]** をクリックして設定を保存します。  
  
また、現在のプロジェクトの設定をカスタマイズすることもできます。 これらの設定は、現在のプロジェクトファイルに保存されます。  
  
**現在のプロジェクトの設定をカスタマイズするには**  
  
1.  [ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックします。  
  
2.  [ **プロジェクトの設定** ] ダイアログボックスで、次のいずれかの手順を実行します。  
  
    -   定義済みのモードを選択するには、[ **モード** ] ボックスの一覧で [ **既定**]、[ **オプティミスティック**]、または [ **完全**] を選択します。  
  
    -   カスタムモードを指定するには、[ **モード** ] ボックスの一覧で [ **カスタム**] を選択し、左ペインでオプションを選択します。次に、右ペインで設定または値をクリックし、新しい設定または値を選択または入力します。  
  
3.  **[OK]** をクリックして設定を保存します。  
  
## <a name="next-steps"></a>次の手順  
移行の次のステップは、プロジェクトのニーズによって異なります。  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズする場合は、「 [SYBASE ASE と SQL Server のデータ型 &#40;SybaseToSQL&#41;にマップ ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)する」を参照してください。  
  
-   それ以外の場合は、Sybase データベースオブジェクト定義を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure オブジェクト定義に変換できます。 詳細については、「 [SYBASE ASE データベースオブジェクトの &#40;SybaseToSQL&#41;の変換 ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
