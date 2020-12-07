---
description: トラブルシューティング (Visual FoxPro ODBC ドライバー)
title: トラブルシューティング (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73f98f66a09b0ff17987186103b38643047f1762
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471435"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>トラブルシューティング (Visual FoxPro ODBC ドライバー)
以下のセクションでは、Visual FoxPro ODBC ドライバーの使用中に発生する可能性のあるパフォーマンスを向上させ、問題を解決する方法について説明します。  
  
## <a name="accessing-parameterized-views"></a>パラメーター化されたビューへのアクセス  
 ドライバーを使用して、Visual FoxPro データベースのパラメーター化されたビューにアクセスすることはできません。 パラメーター化されたビューでは、ビューの SQL **SELECT** ステートメントに where 句が作成されます。これにより、パラメーターに指定された値を使用して構築された where 句の条件を満たすレコードだけが、そのレコードに対して作成されます。 ドライバーはビューへのパラメーターの引き渡しをサポートしていないため、ドライバーを使用してパラメーター化されたビューにアクセスしようとすると失敗します。  
  
 パラメーター値は、実行時に指定することも、プログラムによってビューに渡すこともできます。  
  
## <a name="accessing-remote-views"></a>リモートビューへのアクセス  
 ドライバーを使用して Visual FoxPro データベースのリモートビューにアクセスすることはできません。 リモートビューは、FoxPro 以外のデータにアクセスするビュー、または FoxPro と foxpro 以外のデータの組み合わせにアクセスするビューです。 リモートビューにアクセスするには、Visual FoxPro を使用します。  
  
## <a name="deleting-records"></a>レコードの削除  
 ドライバーを使用してレコードを削除するようにマークすることはできますが、データベースからレコードを完全に削除することはできません。 テーブルからレコードを完全に削除するには、Visual FoxPro を使用します。  
  
## <a name="increasing-performance-using-background-fetching"></a>バックグラウンドフェッチを使用したパフォーマンスの向上  
 大規模なフェッチでは、ドライバーのバックグラウンドフェッチ機能を使用してパフォーマンスを向上させることができます。 バックグラウンドフェッチでは、個別のスレッドを使用して、特定のデータソースから要求されたデータをフェッチします。  
  
 データソースのバックグラウンドフェッチは、次のいずれかの方法で使用できます。  
  
-   [ [ODBC Visual FoxPro セットアップ] ダイアログボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)の [**バックグラウンドでデータをフェッチ**する] チェックボックスをオンにします。  
  
-   接続文字列で BackgroundFetch attribute キーワードを使用します。  
  
 接続文字列の属性キーワードについては、「 [接続文字列の使用](../../odbc/microsoft/using-connection-strings.md)」を参照してください。  
  
## <a name="updating-multitiered-views"></a>多層ビューの更新  
 多層ビューは、ベーステーブルではなく、1つまたは複数のビューに基づくビューです。 多層ビューでデータを更新すると、最上位レベルのビューの基になっているビューに対して、1つのレベルだけが更新されます。ベーステーブルは更新されません。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>ストアドプロシージャでのデータ定義言語 (DDL) の使用  
 Visual FoxPro ストアドプロシージャでは、CREATE TABLE や ALTER TABLE などの DDL を使用できません。  
  
 ストアドプロシージャで使用できる言語の詳細については、「 [ルール、トリガー、既定値、およびストアドプロシージャのサポート](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)」を参照してください。  
  
## <a name="using-positioned-updates"></a>位置指定更新の使用  
 ドライバーは位置指定更新をサポートしていません。 SQL の WHERE 句を使用して、更新する行を特定します。  
  
## <a name="using-the-set-ansi-command"></a>SET ANSI コマンドの使用  
 Visual foxpro 開発者の場合は、既定の設定である Visual FoxPro の既定の設定とは対照的に、SET ANSI の既定の設定がドライバーに対してオンになっていることに注意してください。 SET ANSI の既定の設定では、Visual FoxPro データソースは、通常は正確な比較を実行する他の ODBC データソースと一貫して動作します。 既定の設定を変更することができます。 詳細については、「 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)」を参照してください。
