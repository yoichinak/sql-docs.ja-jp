---
description: Microsoft SDK for Java を使用する
title: Microsoft SDK for Java の使用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: rothja
ms.author: jroth
ms.openlocfilehash: 8471d7e80599b96315fae47e130aaba8c23bd4f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990943"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Microsoft SDK for Java を使用する

> [!IMPORTANT]
> Microsoft は、2004年1月に Visual J++ のサポートを中止しました。

Microsoft SDK for Java は、Microsoft Internet Explorer 環境の developer kit です。 JDK 1.1 および Microsoft Win32 仮想マシン (Microsoft VM) に基づいた Java プログラムとアプレットを開発する際に役立つツール、情報、サンプルが用意されています。 Microsoft SDK for Java は、Microsoft Visual J++ に関連付けられていません。 この SDK をダウンロードするには、ここをクリックしてください。  
  
 Jactivex.exe ユーティリティは、タイプライブラリからクラスを生成しますが、コマンドラインでのみ呼び出すことができます。 この機能は、Visual J++ 開発環境には統合されていません。 Java タイプライブラリウィザードによって生成されるクラスとは異なり、SDK によって作成されたクラスラッパーにステップインできます。 これは、コードで ADO ラッパークラスを使用する方法をデバッグする場合に便利です。  
  
 この機構は、ADO タイプライブラリを読み取り、アプリケーション内でインスタンス化できるクラスを生成します。 これらのクラスは、 \\<windows directory \Java\trustlib\msado15. に生成されます。 \>  
  
 Microsoft SDK for Java を使用して Java で ADO アプリケーションを作成することは、ソースコードの観点から Java タイプライブラリウィザードを使用することと基本的に同じです。 サンプルコードについては、「 [ADO Java クラスラッパー](./ado-java-class-wrappers.md)」を参照してください。 実際の違いは、次の手順に示すように、最初にラッパークラスを生成する方法です。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Microsoft SDK for Java を使用して ADO プロジェクトを作成するには  
  
1.  コマンドプロンプトで次のコマンドを実行します。 Microsoft SDK for Java Bin ディレクトリを含めるようにパスを設定するか、その場所からコマンドを実行する必要があります。 通常、Microsoft SDK for Java は、Visual Studio と同じ場所にインストールされます。 これは単一のコマンドステートメントです。  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  次のコマンドを実行して、生成されたクラスをコンパイルします。 /G: t スイッチはデバッグシンボルの生成をオンにして、にトレースできるようにします。Java シンボル。 リリースビルドの場合は削除します。  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  これらのファイルを使用するには、Visual J++ でプロジェクトを開きます。 [ **プロジェクト** ] メニューの [ **プロジェクトに追加**] をクリックします。 [ **ファイル**] を選択し、すべてのを追加します。Trustlib\msado15 ディレクトリに生成された JAVA ファイルをプロジェクトに出力します。  
  
## <a name="see-also"></a>参照  
 [ADO Java クラス ラッパー](./ado-java-class-wrappers.md)