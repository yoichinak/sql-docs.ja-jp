---
title: SQL Server コネクタのエラーと情報のログ記録
description: この記事では、レジストリ エントリを変更し、SQL Server コネクタのエラーとログ記録を有効にする方法について説明します
ms.date: 10/08/2020
ms.localizationpriority: medium
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: how-to
author: rupp29
ms.author: arupp
ms.openlocfilehash: 85be425e0e352961841f5317c7db219153a6c008
ms.sourcegitcommit: 9122251ab8bbd46ea3c699e741d6842c995195fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91847771"
---
# <a name="sql-server-connector-error-and-information-logging"></a>SQL Server コネクタのエラーと情報のログ記録

この記事では、SQL Server コネクタのエラーおよび情報のログ記録を有効にするためのレジストリ エントリの変更について説明します。

## <a name="sql-server-connector-for-microsoft-azure-key-vault"></a>SQL Server コネクタ for Microsoft Azure Key Vault

[SQL Server コネクタ for Microsoft Azure Key Vault](https://www.microsoft.com/download/details.aspx?id=45344) を使用すると、SQL Server 暗号化で Microsoft Azure Key Vault を拡張キー管理 (EKM) プロバイダーとして利用して、その暗号化キーを保護することができます。

[ダウンロード](https://www.microsoft.com/download/details.aspx?id=45344)は、SQL Server コネクタと、SQL Server 管理者が SQL Server コネクタを構成して SQL Server 暗号化シナリオを有効にする方法を学習できるようにするサンプル スクリプトで構成されています。 詳細については、[Key Vault を使用する拡張キー管理 (SQL Server)](https://go.microsoft.com/fwlink/p/?LinkId=521690) に関するページを参照してください。

[Azure Key Vault フォーラム](https://social.msdn.microsoft.com/Forums/AzureKeyVault)を利用して、質問をしたり、分析情報を共有したり、SQL Server コネクタについて話し合うことができます。

> [!NOTE]
> 通常の実行中に、SQL Server コネクタ DLL によって、Azure Key Vault への接続を確立するためのレジストリ エントリが動的に作成され、キー `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQL Server Cryptographic Provider]` が作成されます。 SQL Server 開始アカウントがローカル管理者であるか、そのサービス アカウントが **NT SERVICE\MSSQLSERVER** である必要があります

## <a name="upgrade-sql-server-connector-to-the-latest-version"></a>SQL Server コネクタを最新バージョンにアップグレードする

SQL Server コネクタ (バージョン: 1.0.5.0、日付: 2020 年 9 月) を最新バージョンの DLL 暗号化プロバイダーにアップグレードするには、これらの手順に従います。

### <a name="upgrade"></a>アップグレード

1. SQL Server 構成マネージャーを使用して、SQL Server サービスを停止します
1. **[コントロール パネル] > [プログラム] > [プログラムと機能]** を使用して、古いバージョンをアンインストールします
    1. アプリケーション名: SQL Server コネクタ for Microsoft Azure Key Vault
    1. バージョン:15.0.300.96
    1. DLL ファイルの日付: 01/30/2018 3:00 PM
1. 新しい SQL Server コネクタ for Microsoft Azure Key Vault をインストール (アップグレード) します
    1. バージョン:15.0.2000.367
    1. DLL ファイルの日付: 09/11/2020 ‏‎5:17 AM
1. SQL Server サービスを開始します
1. 暗号化された DB がアクセス可能であることをテストします

### <a name="rollback"></a>ロールバック

1. SQL Server 構成マネージャーを使用して、SQL Server サービスを停止します
1. **[コントロール パネル] > [プログラム] > [プログラムと機能]** を使用して、新しいバージョンをアンインストールします
    1. アプリケーション名: SQL Server コネクタ for Microsoft Azure Key Vault
    1. バージョン:15.0.2000.367
    1. DLL ファイルの日付: 09/11/2020 ‏‎5:17 AM
1. 古いバージョンの SQL Server コネクタ for Microsoft Azure Key Vault をインストールします
    1. バージョン:15.0.300.96
    1. DLL ファイルの日付: 01/30/2018 3:00 PM
1. SQL Server サービスを開始します
1. 暗号化された DB がアクセス可能であることをテストします

> [!NOTE]
> - 1\.0.0.440 以前のバージョンの SQL Server コネクタは置き換えられ、運用環境でサポートされなくなりました。 SQL Server コネクタの問題のトラブルシューティングの詳細については、「[SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)」を参照してください。
> - バージョン 1.0.3.0 以降の SQL Server コネクタでは、関連するエラー メッセージがトラブルシューティングのために Windows イベント ログにレポートされます。
> - [1.0.4.0: (バージョン 13.0.811.168)](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/SQLServerConnectorforMicrosoftAzureKeyVault.msi) 以降では、Azure China、Azure Germany、Azure Government などのプライベート Azure クラウドがサポートされています。
> - バージョン 1.0.5.0 では、サムプリントのアルゴリズムについて破壊的変更があります。 1\.0.5.0 にアップグレードした後、データベースの復元でエラーが発生する可能性があります。 詳細については、[サポート技術情報の記事 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0) を参照してください。
> - **バージョン 1.0.5.0 以降 (ファイルの日付が 2020 年 9 月) の SQL Server コネクタで、メッセージのフィルター処理とネットワーク要求の再試行ロジックがサポートされます。**
> - "*SQL Server コネクタの古いバージョンも、バージョン: [1.0.5.0 (バージョン 15.0.300.96) – ファイルの日付: 2018 年 1 月](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/ENU/SQLServerConnectorforMicrosoftAzureKeyVault.msi)* " です。 問題が発生した場合は、最新の SQL Server コネクタにアップグレードしてください。

**システム要件** - サポートされている SQL Server バージョン:

- SQL Server 2019 RTM Enterprise 64 ビット
- SQL Server 2017 RTM Enterprise 64 ビット
- SQL Server 2016 RTM Enterprise 64 ビット
- SQL Server 2014 RTM Enterprise 64 ビット
- SQL Server 2012 SP2 Enterprise 64 ビット
- SQL Server 2012 SP1 CU6 Enterprise 64 ビット
- SQL Server 2008 R2 SP2 CU8 Enterprise 64 ビット

上の一覧に記載されているものより前の SQL Server 2008 および 2012 バージョンでは、次のサポート技術情報の記事で指定されているパッチをインストールする必要があります: [https://support2.microsoft.com/kb/2859713](https://support2.microsoft.com/kb/2859713)。

また、SQL Server コネクタ for Microsoft Azure Key Vault には、Azure 上の Microsoft SQL Server 仮想マシンに .NET バージョン 4.5.1 も必要です。 SQL Server コネクタをインストールする前に、このライブラリをインストールする必要があります。

実行している SQL Server のバージョンに基づいて、適切なバージョンの Visual Studio C++ 再頒布可能パッケージをインストールしておいてください。

- SQL Server バージョン 2008、2008 R2、2012、および 2014 の場合は、2013 Visual C++ 再頒布可能パッケージをインストールします。

- SQL Server 2016 の場合は、2015 Visual C++ 再頒布可能パッケージをインストールします。

## <a name="modify-windows-registry-steps"></a>Windows レジストリの変更手順

レジストリ エントリを変更し、Windows アプリケーション イベント ログでの SQL Server コネクタのエラーおよび情報イベントのログ記録を有効にします。

> [!CAUTION]
> ご自身の責任で慎重にこのセクションの手順に従ってください。 レジストリの変更の方法を誤った場合、深刻な問題が発生することがあります。 レジストリを変更する前に、問題が発生した場合に備えて、[復元用にレジストリをバックアップ](https://support.microsoft.com/help/322756)しておいてください。

1. Windows 10 でレジストリ エディターを開くには、次の 2 つの方法があります。
    - タスク バーの検索ボックスに、「**regedit**」と入力します。 その後、レジストリ エディター (デスクトップ アプリ) の上位の結果を選択します。

    ![ekm regedit open](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-open.png "ekm regedit open")
    - [スタート] ボタンを押したままにするか右クリックして、[実行] を選択します。 ダイアログ ボックスに「**regedit**」と入力し、 **[OK]** を選択します。

   ![ekm regedit start](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-start.png "ekm regedit start")

1. このレジストリ キーに移動します:

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\**

    ![ekm regedit akv](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv.png "ekm regedit akv")  

1. **Azure Key Vault** の下に、`Log` という名前の新しいキーを追加します。

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\Log\\**

    ![ekm regedit akv log](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log.png "ekm regedit akv log.png")  

1. **Log** キーの下に、`Level` という名前の DWORD (32 ビット) の値を追加します。

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\Log\\**

    ![ekm regedit akv log dword](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log-dword.png "ekm regedit akv log dword")  

1. DWORD の値を適切なログ レベル (0、1、2) に設定します。
   1. 0 (情報) - **既定値**
   1. 1 (エラー)
   1. 2 (ログなし)

   ![ekm regedit akv log level](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log-level.png "ekm regedit akv log level")  

この記事で説明されているレジストリ エントリは、このキーの下にあります。

```console
\Computer
    \HKEY_LOCAL_MACHINE
       \SOFTWARE
          \Microsoft
             \SQL Server Cryptographic Provider
                \Azure Key Vault
                   \Log\
                      <Level>
```

必要に応じて、コマンドラインを使用してキーを生成できます。

```cmd
--Create the logging parameter using (Administrator) Command Line:
REG ADD "HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\Log" /v Level /t REG_DWORD /d 1 

--Validate the new registry entry
REG QUERY "HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\Log" /v Level
```

メッセージが欠落しているアプリケーション イベント ログ エントリも、レジストリ エントリを使用して修正できます。 イベント ログには、`The description for Event ID 0 from source SQL Server Connector for Microsoft Azure Key Vault cannot be found...` というメッセージを含めることができます。  

```cmd
--Create the registry entry to enable missing messages (this works with any version)
REG ADD "HKLM\SYSTEM\ControlSet001\Services\EventLog\Application\SQL Server Connector for Microsoft Azure Key Vault" /v EventMessageFile /t REG_EXPAND_SZ /d "C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll"

--Validate the new registry entry
REG QUERY "HKLM\SYSTEM\ControlSet001\Services\EventLog\Application\SQL Server Connector for Microsoft Azure Key Vault" /v EventMessageFile
```

## <a name="related-articles"></a>関連記事

- 追加のサンプル スクリプトについては、「[SQL Server Transparent Data Encryption and Extensible Key Management with Azure Key Vault (Azure Key Vault を使用した SQL Server Transparent Data Encryption と拡張キー管理)](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549)」のブログをご覧ください。
- [拡張キー管理 (EKM)](extensible-key-management-ekm.md)  
- [Azure Key Vault を使用した拡張キー管理](extensible-key-management-using-azure-key-vault-sql-server.md)
- [SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
