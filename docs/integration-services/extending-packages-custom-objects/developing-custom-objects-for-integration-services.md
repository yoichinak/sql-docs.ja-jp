---
description: Integration Services 用のカスタム オブジェクトの開発
title: Integration Services 用のカスタム オブジェクトの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8064836dcfe27a19339363301b876ab723b78294
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193152"
---
# <a name="developing-custom-objects-for-integration-services"></a>Integration Services 用のカスタム オブジェクトの開発

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる制御フロー オブジェクトおよびデータ フロー オブジェクトが、求める条件を満たしていない場合は、次のようなさまざまな種類のカスタム オブジェクトを独自に開発できます。  
  
-   **カスタム タスク**。  
  
-   **カスタム接続マネージャー。** 現在サポートされていない外部データ ソースに接続します。  
  
-   **カスタム ログ プロバイダー。** 現在サポートされていない形式でパッケージ イベントのログを記録します。  
  
-   **カスタム列挙子。** 現在サポートされていないオブジェクト形式または値形式のセットを繰り返し処理できるようにします。  
  
-   **カスタム データ フロー コンポーネント。** 変換元、変換、変換先のいずれかとして構成できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクト モデルにはこのカスタム開発を容易にする複数の基本クラスがあります。これらの基本クラスによって、カスタム実装に対し、一貫した信頼性の高いフレームワークが提供されます。  
  
 カスタム機能を複数のパッケージで再利用する必要がない場合には、スクリプト タスクおよびスクリプト コンポーネントを使用すると、マネージド プログラミング言語を最大限に活用でき、記述するインフラストラクチャ コードが大幅に削減されます。 詳細については、「[スクリプティング ソリューションとカスタム オブジェクトとの比較](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)」を参照してください。  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Integration Services 用カスタム オブジェクトの開発手順  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用するカスタム オブジェクトを開発する際には、クラス ライブラリ (DLL) を開発します。このクラス ライブラリは、デザイン時に SSIS デザイナーによって、また実行時に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムによって、それぞれ読み込まれます。 実装の必要がある最も重要なメソッドは、独自のコードから呼び出すメソッドではなく、ランタイムによって適切な時点で呼び出され、コンポーネントの初期化および検証や、機能の呼び出しを行うメソッドです。  
  
 次に、カスタム オブジェクトの開発手順を示します。  
  
1.  種類がクラス ライブラリの新規プロジェクトを、任意のマネージド プログラミング言語で作成します。  
  
2.  次の表に示す、適切な基本クラスを継承します。  
  
3.  次の表に示す、適切な属性を新しいクラスに適用します。  
  
4.  必要に応じて基本クラスのメソッドをオーバーライドし、オブジェクトのカスタム機能のコードを記述します。  
  
5.  必要に応じて、コンポーネント用のカスタム ユーザー インターフェイスを構築します。 配置を容易にするため、同一ソリューション内の別個のプロジェクトとしてユーザー インターフェイスを開発し、別個のアセンブリとしてビルドすることもできます。  
  
6.  必要に応じて、カスタム オブジェクトのサンプルおよびヘルプ コンテンツへのリンクを **SSIS ツールボックス**内に表示します。  
  
7.  「[カスタム オブジェクトのビルド、配置、およびデバッグ](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)」の説明に従って、新しいカスタム オブジェクトのビルド、配置、およびデバッグを行います。  
  
## <a name="base-classes-attributes-and-important-methods"></a>基本クラス、属性、および重要なメソッド  
 この表では、開発可能な各種カスタム オブジェクトに対する、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクト モデルの最も重要な要素を簡単に参照できます。  
  
|カスタム オブジェクト|基底クラス|属性|重要なメソッド|  
|-------------------|----------------|---------------|-----------------------|  
|タスク|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|[ODBC 入力元エディター]|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|ログ プロバイダー|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|列挙子|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|カスタム データ フロー コンポーネント|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>サンプルとヘルプ コンテンツへのリンクの提供  
 マネージド コードで記述されたカスタム オブジェクトのサンプルおよびヘルプ コンテンツへのリンクを **SSIS ツールボックス**に表示するには、次のプロパティを使用します。  
  
-   [Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag*](/dotnet/api/microsoft.sqlserver.dts.pipeline.dtspipelinecomponentattribute.samplestag)  
  
-   [Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection*](/dotnet/api/microsoft.sqlserver.dts.pipeline.dtspipelinecomponentattribute.helpcollection)  
  
-   [Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword*](/dotnet/api/microsoft.sqlserver.dts.pipeline.dtspipelinecomponentattribute.helpkeyword)  
  
-   [Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag*](/dotnet/api/microsoft.sqlserver.dts.runtime.dtstaskattribute.samplestag)  
  
-   [Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection*](/dotnet/api/microsoft.sqlserver.dts.runtime.dtstaskattribute.helpcollection)  
  
-   [Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword*](/dotnet/api/microsoft.sqlserver.dts.runtime.dtstaskattribute.helpkeyword)  
  
 ネイティブ コードで記述されたカスタム オブジェクトのサンプルおよびヘルプ コンテンツへのリンクを表示するには、レジストリ スクリプト (.rgs) ファイルに SamplesTag、HelpKeyword、および HelpCollection のエントリを追加します。 以下に例を示します。  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>カスタム ユーザー インターフェイスの提供  
 カスタム オブジェクトのプロパティをユーザーが構成できるようにするには、カスタム ユーザー インターフェイスの開発も必要になる場合があります。 カスタム ユーザー インターフェイスが特に必要ない場合も、既定のエディターよりもユーザー フレンドリなカスタム ユーザー インターフェイスを作成できます。  
  
 1 つのカスタム ユーザー インターフェイス プロジェクトまたはアセンブリには、通常 2 つのクラスがあります。特定の種類のカスタム オブジェクトのユーザー インターフェイスに対して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] インターフェイスを実装するクラスと、このクラスによって表示される、ユーザーから情報を収集するための Windows フォームです。 実装するインターフェイスに含まれるメソッドは少数であるため、カスタム ユーザー インターフェイスの開発は難しくありません。  
  
> [!NOTE]  
>  多くの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ログ プロバイダーには、カスタム ユーザー インターフェイスがあります。カスタム ユーザー インターフェイスには <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> が実装され、 **[構成]** テキスト ボックスが、使用可能な接続マネージャーがフィルター選択されたドロップダウン リストに置き換えられます。 ただし、カスタム ログ プロバイダーのカスタム ユーザー インターフェイスは、このリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では実装されていません。 そのため、<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> プロパティに値を指定しても、影響がありません。  
  
 次の表では、各種カスタム オブジェクトに対するカスタム ユーザー インターフェイスの開発時に実装が必要なインターフェイスを、簡単に参照できます。 また、オブジェクトに対するカスタム ユーザー インターフェイスを開発しなかった場合や、オブジェクトの属性の **UITypeName** プロパティを使用して、オブジェクトをそのユーザー インターフェイスにリンクできなかった場合に、ユーザーに対してどのように表示されるのかについても説明します。 データ フロー コンポーネントにとっては強力な詳細エディターで十分な場合もありますが、タスクや接続マネージャーにとっては [プロパティ] ウィンドウは比較的わかりにくいソリューションであり、カスタム ForEach 列挙子はカスタム フォームなしでは構成不可能です。  
  
|カスタム オブジェクト|ユーザー インターフェイス用の基本クラス|カスタム ユーザー インターフェイスを指定しなかった場合の既定の編集動作|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|タスク|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|[プロパティ] ウィンドウのみ。|  
|[ODBC 入力元エディター]|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|[プロパティ] ウィンドウのみ。|  
|ログ プロバイダー|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> ([!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では未実装)|**[構成]** 列のテキスト ボックス|  
|列挙子|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|プロパティ ウィンドウのみ。 エディターの列挙子構成領域は空です。|  
|カスタム データ フロー コンポーネント|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|[詳細エディター]|  
  
## <a name="external-resources"></a>外部リソース  
  
-   blogs.msdn.com のブログ「[Visual Studio solution build process give a warning about indirect dependency on the .NET Framework assembly due to SSIS references](/archive/blogs/jason_howell/visual-studio-2010-solution-build-process-give-a-warning-about-indirect-dependency-on-the-net-framework-assembly-due-to-ssis-references)」 (Visual Studio ソリューションのビルド プロセスで示される、SSIS 参照による .NET Framework アセンブリの間接的な依存関係に関する警告)  
  
## <a name="see-also"></a>参照  
 [カスタム オブジェクトの永続化](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [カスタム オブジェクトのビルド、配置、デバッグ](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
