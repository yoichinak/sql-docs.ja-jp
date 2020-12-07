---
title: ファイルの瞬時初期化の構成
description: Analytics Platform System でファイルの瞬時初期化を構成します。 ファイルの瞬時初期化は、データファイル操作をより迅速に実行できるようにする SQL Server の機能です。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 62b76b616786c593d395ee8720bba4c012390290
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766891"
---
# <a name="instant-file-initialization-configuration"></a>ファイルの瞬時初期化の構成
ファイルの瞬時初期化は、データファイル操作をより迅速に実行できるようにする SQL Server の機能です。 ファイルの瞬時初期化をオンにするチェックボックスをオンにすると、SQL Server PDW のパフォーマンスが向上します。 ただし、これによってビジネスに対するセキュリティ上のリスクが生じた場合は、チェックボックスをオフのままにします。  
  
> [!IMPORTANT]  
> ファイルの瞬時初期化が有効になっている場合、SQL Server は、削除されたビットをゼロで上書きしません。  この動作により、権限のないユーザーが削除されたデータにアクセスした場合に、セキュリティ上の脆弱性が生じます。 ただし SQL Server PDW は、SQL Server データベースとバックアップファイルが常に SQL Server のインスタンスにアタッチされるようにすることで、このリスクを軽減します。SQL Server PDW 上の削除されたデータにアクセスできるのは、SQL Server サービスアカウントとローカル管理者のみです。  
  
ファイルの瞬時初期化は、TDE が有効になっている場合は使用できません。  
  
## <a name="add-permission-for-the-backup-account"></a>バックアップアカウントのアクセス許可を追加する  
バックアッププロセスでは、バックアップストレージの場所にアクセスできるネットワーク資格情報 (Windows ユーザーアカウント) が必要です。 [Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)プロシージャを使用して、PDW がアカウントを使用することを承認します。 バックアッププロセス全体については、「 [BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=sql-server-ver15) 」を参照してください。 ファイルの瞬時初期化を使用するには、バックアップアカウントにアクセス許可が付与されている必要があり `Perform volume maintenance tasks` ます。  
  
1.  バックアップサーバーで、 **ローカルセキュリティポリシー** アプリケーション () を開き `secpol.msc` ます。  
  
2.  左側のペインで **[ローカル ポリシー]** を展開し、 **[ユーザー権利の割り当て]** をクリックします。  
  
3.  右側のペインで、 **[ボリュームの保守タスクを実行]** をダブルクリックします。  
  
4.  **[ユーザーまたはグループの追加]** をクリックし、バックアップに使用される任意のユーザー アカウントを追加します。  
  
5.  **[適用]** をクリックし、 **[ローカル セキュリティ ポリシー]** ダイアログ ボックスをすべて閉じます。  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>ファイルの瞬時初期化を有効または無効にするには  
  
1.  Configuration Manager を起動します。 詳細については、「 [Configuration Manager &#40;Analytics Platform System&#41;の起動 ](launch-the-configuration-manager.md)」を参照してください。  
  
2.  Configuration Manager の左側のウィンドウで、[ **ファイルの瞬時初期化**] をクリックします。  
  
3.  ファイルの瞬時初期化を有効にするには、[ **すべてのノードでファイルの瞬時初期化を有効**にする] の横にあるチェックボックスをオンにします。 ファイルの瞬時初期化をオフにするには、[ **すべてのノードでファイルの瞬時初期化を有効**にする] の横にあるチェックボックスをオフにします。  
  
    > [!WARNING]  
    > ファイルの瞬時初期化を無効にすると、ファイルの瞬時初期化が有効になっている間に、上記の機能について説明したセキュリティの考慮事項が、削除されたファイルに引き続き適用される場合があります。  
  
4.  **[Apply]** をクリックします。 この変更は、次にアプライアンスサービスが再起動されたときに SQL Server PDW の SQL Server インスタンスに反映されます。 ここでアプライアンスサービスを再起動するには、「 [PDW サービスの状態 &#40;Analytics Platform System&#41;](pdw-services-status.md)」を参照してください。  
  
5.  **ボリュームの保守タスクを実行**するアクセス許可を削除するには、前述の手順を**バックアップアカウントの追加アクセス許可**として繰り返すことをお勧めします。  
  
![DWConfig アプライアンス PDW のファイルの瞬時初期化](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
ファイルの瞬時初期化の詳細については、「 [ファイルの瞬時初期化](/previous-versions/sql/sql-server-2008-r2/ms175935(v=sql.105))」を参照してください。  
