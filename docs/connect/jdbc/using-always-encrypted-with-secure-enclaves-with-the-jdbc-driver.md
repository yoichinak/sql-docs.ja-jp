---
description: JDBC Driver でのセキュリティで保護されたエンクレーブが設定された Always Encrypted の使用
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を JDBC Driver と共に使用する | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: reneye
ms.author: v-reye
ms.openlocfilehash: 8035e1d5890bf51d80341f740436d586053d4e90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487924"
---
# <a name="using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を JDBC Driver と共に使用する
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

このページでは、[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) と Microsoft JDBC Driver 8.2 (以降) for SQL Server を使用して Java アプリケーションを開発する方法について説明します。

セキュア エンクレーブは、既存の [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 機能に対する追加の機能です。 セキュア エンクレーブの目的は、Always Encrypted データを使用する際の制限に対処することです。 以前は、ユーザーが Always Encrypted データに対して実行できるのは等価比較だけであり、他の操作を実行するためには、データを取得して暗号化を解除する必要がありました。 セキュア エンクレーブは、セキュア エンクレーブ内のプレーンテキスト データに対してサーバー側で計算ができるようにすることで、このような制限に対応しています。 セキュリティで保護されたエンクレーブは、SQL Server プロセス内のメモリの保護された領域であり、SQL Server エンジン内の機密データを処理するための信頼できる実行環境として機能します。 セキュリティで保護されたエンクレーブは、その他の SQL Server やホスティング マシン上の他のプロセスに対してはブラック ボックスに見えます。 デバッガーを使用しても、外部からエンクレーブ内のデータやコードを表示する方法はありません。

## <a name="prerequisites"></a>前提条件
- 開発用マシンに Microsoft JDBC Driver 8.2 (以降) for SQL Server がインストールされていることを確認します。
- DLL や KeyStores など、環境の依存関係が正しいパスに配置されていることを確認します。 セキュリティで保護されたエンクレーブは既存の [Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md) 機能のアドオンであり、前提条件が類似しています。

> [!Note]
> 以前のバージョンの JDK 8 を使用している場合は、必要に応じて、Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files (JCE 管轄ポリシー ファイル (無制限強度)) をダウンロードしてインストールします。 インストール手順、および考えられるエクスポート/インポート問題に関する詳細について、zip ファイルに含まれる Readme を必ず読んでください。  
>
> [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) からポリシー ファイルをダウンロードできます。

## <a name="setting-up-secure-enclaves"></a>セキュア エンクレーブの設定
セキュア エンクレーブの使用を開始するには、こちらの[チュートリアル](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)に従ってください。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。

## <a name="connection-string-properties"></a>接続文字列プロパティ
**enclaveAttestationUrl:** 構成証明サービスのエンドポイント URL です。

**enclaveAttestationProtocol:** 構成証明サービスのプロトコルです。 現在唯一サポートされている値は **HGS** (ホスト ガーディアン サービス) です。

セキュア エンクレーブを使用する Always Encrypted をユーザーが [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] から有効にするためには、**columnEncryptionSetting** を有効にし、上記の接続文字列プロパティの**両方**を正しく設定する必要があります。

## <a name="working-with-secure-enclaves"></a>セキュア エンクレーブの使用
エンクレーブ接続プロパティが適切に設定されている場合、この機能の動作は透過的です。 セキュア エンクレーブをクエリに使用する必要があるかどうかが、ドライバーによって自動的に判断されます。 エンクレーブの計算をトリガーするクエリの例を次に示します。 データベースとテーブルの設定については [Always Encrypted エンクレーブの概要](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)に関するページを参照してください。

高度なクエリを実行すると、エンクレーブの計算がトリガーされます。
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL)) {
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SSN LIKE ?")) {
        p.setString(1, "%6818");
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
    
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SALARY > ?")) {
        ((SQLServerPreparedStatement) p).setMoney(1, new BigDecimal(0));
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
}
```

列の暗号化を切り替えた場合も、エンクレーブの計算がトリガーされます。
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL);Statement s = c.createStatement()) {
    s.executeUpdate("ALTER TABLE Employees ALTER COLUMN SSN CHAR(11) NULL WITH (ONLINE = ON)");
}
```

## <a name="java-8-users"></a>Java 8 ユーザー
この機能には、RSASSA-PSA 署名アルゴリズムが必要です。 このアルゴリズムは JDK 11 で追加されましたが、JDK 8 へのバックポートはされていません。 JDK 8 バージョンの [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] でこの機能を使用する場合は、RSASSA-PSA 署名アルゴリズムをサポートする独自のプロバイダーを読み込むか、BouncyCastleProvider のオプションの依存関係を含める必要があります。 今後、JDK 8 に署名アルゴリズムがバックポートされるか、JDK 8 のサポート ライフサイクルが終了した場合は、依存関係は削除されます。

## <a name="see-also"></a>関連項目
[JDBC ドライバーでの Always Encrypted の使用](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
