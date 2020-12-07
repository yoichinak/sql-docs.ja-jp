---
description: プロジェクト オプションの設定 (MySQLToSQL)
title: プロジェクトオプションの設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: df2a29b2d411c2502573ede95feefe9c1e061c5b
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987898"
---
# <a name="setting-project-options-mysqltosql"></a>プロジェクト オプションの設定 (MySQLToSQL)
SSMA プロジェクトごとに、プロジェクトレベルのオプションを設定できます。 これらのオプションでは、オブジェクトの変換方法、データの移行方法、およびソースデータ型とターゲットデータ型のマッピング方法を指定します。  オブジェクトを SQL Server に変換したり、SQL Server または SQL Azure にデータを SQL Azure または移行したりする前に、構成オプションがプロジェクトに適していることを確認してください。  
  
SSMA を使用すると、すべてのプロジェクトの既定のオプションを構成できます。 これらのオプションは、作成するすべての新しいプロジェクトに適用されます。 その後、各プロジェクトのオプションをカスタマイズできます。  
  
## <a name="configuration-options-and-modes"></a>構成オプションとモード  
SSMA には、次の5つのプロジェクト設定があります。  
  
-   プロジェクト情報  
  
-   全般 (変換、移行、SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   型マッピング  
  
プロジェクト設定は、次の4つの方法で構成できます。  
  
-   Default  
  
-   Optimistic  
  
-   [完全]  
  
-   Custom  
  
ほとんどのユーザーには、既定のモードを使用することをお勧めします。 オプティミスティックモードでは、現在の MySQL 構文がより多く保持されるため、読みやすくなります。 ただし、現在の構文を維持するのは正確ではない可能性があります。 MySQL 構文を同等の SQL Server または SQL Azure 構文に変換する必要がある場合、フルモードでは完全な変換が実行されます。 ただし、結果として得られるコードは読みにくくなる可能性があります。 カスタムモードでは、オプションを設定できます。  
  
各モードでの設定と設定の適用方法の詳細については、次のトピックを参照してください。  
  
-   [プロジェクト設定 &#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [プロジェクト設定 &#40;移行&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [プロジェクトの設定 (GUI) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md)  
  
-   [プロジェクト設定 &#40;型マッピング&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [プロジェクト設定 &#40;同期&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [プロジェクト設定 &#40;Azure SQL Database&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>プロジェクト オプションの設定  
SSMA では、すべてのプロジェクトの既定の設定を構成できます。 これらの設定は、SSMA 構成ファイルに保存され、作成した新しいプロジェクトに適用されます。  
  
**既定のプロジェクトオプションを設定するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  [ **既定のプロジェクト設定** ] ダイアログボックスで、次のいずれかの手順を実行します。  
  
    1.  [移行 **先のバージョン** ] ドロップダウンから表示/変更する設定が必要な移行プロジェクトの種類を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックして、[変換] または [ **移行] または [SQL Azure** ] オプションを選択します。  
  
    2.  定義済みのモードを選択するには、[**モード**] ボックスの一覧から [**既定**]、[**オプティミスティック**]、または [**完全**] を選択します。  
  
    3.  カスタム設定を指定するには、新しい設定または値を選択または入力します。  
  
3.  **[OK]** をクリックして設定を保存します。  
  
また、現在のプロジェクトの設定をカスタマイズすることもできます。 設定は、現在のプロジェクトファイルに保存されます。  
  
**現在のプロジェクトの設定をカスタマイズするには**  
  
1.  [ **ツール** ] メニューの [ **projectsettings**] をクリックします。  
  
2.  [ **Projectsettings** ] ダイアログボックスで、次のいずれかの手順を実行します。  
  
    1.  定義済みのモードを選択するには、[**モード**] ボックスの一覧から [**既定**]、[**オプティミスティック**]、または [**完全**] を選択します。  
  
    2.  カスタムモードを指定するには、[**モード**] ボックスの一覧の [**カスタム**] を選択します。 次に、適切なプロジェクト設定を選択します。  
  
3.  **[OK]** をクリックして設定を保存します。  
  
## <a name="next-step"></a>次の手順  
移行の次のステップは、プロジェクトのニーズによって異なります。  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするには、「 [MySQL と SQL Server のデータ型 &#40;MySQLToSQL&#41;のマッピング](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)」を参照してください。  
  
-   それ以外の場合は、MySQL データベースオブジェクト定義を SQL Server または SQL Azure オブジェクト定義に変換できます。 詳細については、「 [MySQL データベース &#40;MySQLToSQL の変換](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)」を参照してください&#41;  
  
## <a name="see-also"></a>参照  
[MySQL と SQL Server のデータ型のマッピング &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
