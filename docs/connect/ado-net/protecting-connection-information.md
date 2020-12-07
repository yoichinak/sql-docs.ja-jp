---
title: 接続情報の保護
description: 接続文字列のセキュリティの脆弱性について説明します。これは、接続文字列の構築方法と保持方法、および認証の種類が原因で生じる場合があります。
ms.date: 11/13/2020
ms.assetid: 1471f580-bcd4-4046-bdaf-d2541ecda2f4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 87d8e2013693d2e8123adb97273309d6f22de03e
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126457"
---
# <a name="protecting-connection-information"></a>接続情報の保護

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

アプリケーションのセキュリティを実現するうえで、データ ソースへのアクセスを保護することは、最も重要な目標の 1 つです。 保護されていない接続文字列は脆弱性を招く原因になります。 接続情報をテキスト形式で保存したり、メモリ内に保持したりすると、システム全体のセキュリティが損なわれる可能性があります。 ソース コードに組み込まれた接続文字列は、[Ildasm.exe (IL Disassembler)](/dotnet/docs/framework/tools/ildasm-exe-il-disassembler.md) を使って、コンパイル済みアセンブリの Microsoft Intermediate Language (MSIL) を表示することで読み取ることができます。

接続文字列に関係したセキュリティ上の脆弱性は、使用されている認証の種類、メモリやディスクへの接続文字列の保存方法、実行時に接続文字列を作成する際の手法などから発生します。

## <a name="use-windows-authentication"></a>Windows 認証の使用

データ ソースへのアクセスを制限するには、ユーザー ID、パスワード、データ ソース名などの接続情報をセキュリティで保護する必要があります。 ユーザー情報の漏洩を防ぐためにも、できるだけ Windows 認証 ("*統合セキュリティ*" とも呼ばれます) を使用することをお勧めします。 Windows 認証は、接続文字列に `Integrated Security` キーワードまたは `Trusted_Connection` キーワードを使用することによって指定できます。こうすることで、ユーザー ID とパスワードを使う必要がなくなります。 Windows 認証を使用した場合、ユーザーは Windows によって認証され、サーバー リソースやデータベース リソースへのアクセスは Windows のユーザーおよびグループに付与された権限によって制御されます。

Windows 認証が使用できない場合、ユーザーの資格情報を接続文字列に含めることになるため、十分な注意が必要です。 ASP.NET アプリケーションでは、Windows アカウントを、データベースやその他のネットワーク リソースに接続する際の固定 ID として構成できます。 **web.config** ファイルの identity 要素で権限の借用を有効にし、ユーザー名とパスワードを指定します。

```xml  
<identity impersonate="true"
        userName="MyDomain\UserAccount"
        password="*****" />  
```  

固定 ID アカウントには、権限の低いアカウント、つまり、データベースに対する必要な権限だけが付与されたアカウントを使用してください。 さらに、ユーザー名とパスワードがクリア テキストで表示されないよう、構成ファイルを暗号化する必要があります。

## <a name="avoid-injection-attacks-with-connection-string-builders"></a>接続文字列ビルダーを使用したインジェクション攻撃の防止

ユーザー入力から文字列を動的に連結することによって接続文字列を構築している場合、接続文字列のインジェクション攻撃を受ける可能性があります。 ユーザー入力の検証や悪意のある文字のエスケープを怠ると、機密データなど、サーバー上のリソースへのアクセスを攻撃者に許してしまうことも考えられます。 この問題に対処するため、Microsoft SqlClient Data Provider for SQL Server には、接続文字列の構文を検証し、余分なパラメーターの追加を防ぐ新しい接続文字列ビルダー クラスが導入されています。 詳細については、「[接続文字列ビルダー](connection-string-builders.md)」をご覧ください。

## <a name="use-persist-security-infofalse"></a>Persist Security Info=False の使用

`Persist Security Info` の既定値は false です。すべての接続文字列には、この既定値を使用することをお勧めします。 `Persist Security Info` を `true` または `yes` に設定すると、ユーザー ID やパスワードなどのセキュリティ関連情報を、接続を開いた後にその接続から取得できます。 `Persist Security Info` を `false` または `no` に設定した場合、その情報を使って接続を開いた後で、セキュリティ情報が破棄されるため、信頼できないソースによってセキュリティ関連情報がアクセスされることを確実に防ぐことができます。

## <a name="encrypt-configuration-files"></a>構成ファイルの暗号化

[!INCLUDE[appliesto-netfx-netcore-xxxx-md](../../includes/appliesto-netfx-netcore-xxxx-md.md)]

接続文字列は構成ファイルに保存することもでき、そうすることで、アプリケーションのコードに接続文字列を組み込むことを避けられます。 構成ファイルは、.NET Framework が基本的な要素を定義するために使用する標準的な XML ファイルです。 通常、構成ファイル内の接続文字列は、**app.config** ファイル (Windows アプリケーションの場合) または **web.config** ファイル (ASP.NET アプリケーションの場合) の **\<connectionStrings>** 要素に格納されます。 構成ファイルへの接続文字列の格納、構成ファイルからの接続文字列の取得、および暗号化については、「[接続文字列と構成ファイル](connection-strings-and-configuration-files.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [保護された構成を使用した構成情報の暗号化](/previous-versions/aspnet/53tyfkaw(v=vs.100))
