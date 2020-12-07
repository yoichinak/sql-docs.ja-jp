---
description: ドライバー対応接続プール
title: ドライバー対応接続プール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed2fa29a68095be9cfcc7d4192c6dc2e15f3eac7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494660"
---
# <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール
ドライバー対応接続プールは、Windows 8 のドライバーマネージャーの新機能です。 ドライバーを認識する接続プールを使用すると、ドライバー作成者は ODBC ドライバーの接続プールの動作をカスタマイズできます。  
  
> [!NOTE]  
>  ドライバー対応接続プールは、カーソルライブラリではサポートされていません。 ドライバー対応の接続プールが有効になっている場合、SQLSetConnectAttr 経由でカーソルライブラリを有効にしようとすると、アプリケーションでエラーメッセージが表示されます。  
  
 ドライバー対応接続プールは、ドライバーマネージャーの接続プールに関連する次の問題に対処します。  
  
 **プールの断片化** ドライバーマネージャーは、新しい接続要求の接続文字列と完全に一致する場合にのみ、プールからの接続を返します。  ドライバーマネージャーが完全に一致する必要がある理由の1つは、ドライバーマネージャーがドライバー固有のすべての接続文字列キーワードとその値を認識しないことです。  ただし、接続文字列のキーワード値 (データベースの名前など) によっては完全に一致する必要がない場合があります。これは、ドライバーが新しい接続を開くために必要な時間よりも短い時間でデータベースを変更できるためです (正確な時間差はデータソースによって異なります)。 また、一部の接続属性 (SQL_ATTR_CURRENT_CATALOG など) の違いは、他の属性 (SQL_ATTR_LOGIN_TIMEOUT など) の違いよりも変更に時間がかかることがあります。 これにより、ドライバーマネージャーがプールからの最低コストで再利用可能な接続を使用できなくなる可能性があります。 ドライバーが多数の新しい接続を作成する必要がある場合、アプリケーションのパフォーマンスが低下し、データソースのスケーラビリティが低下する可能性があります。 ドライバーが接続要求のためにプール内の接続を再利用するコストをより正確に推定できるため、ドライバー対応の接続プールによってプールの断片化が軽減される可能性があります。  
  
 **アプリケーションの設定は考慮しません** 一部のデータソースでは、いくつかの属性をリセットする場合と比較して、新しい接続を効率的に開くことができます。そのため、アプリケーションでは、プールから若干一致しない接続を再利用し、いくつかの値をリセットするのではなく、新しい接続を開くことをお勧めします ただし、アプリケーションによっては、サーバーの負荷が小さくなり、接続数が少なくなる場合がありますが、適切な動作の不一致を修正するには大きなコストがかかる可能性があります。 ドライバー対応接続プールを使用しない場合、ドライバーマネージャーはドライバー固有のすべての接続属性を認識しないため、このような設定を効果的に指定することはできません。 ドライバー対応接続プールを使用すると、ドライバーはユーザー設定 (SQLSetConnectAttr のドライバー固有の属性) を取得できるため、ユーザー設定に基づいてプールからの接続を再利用するコストをより正確に見積もることができます。  
  
 ドライバー対応接続プールの詳細については、「 [ODBC ドライバーでの接続プールの認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)」を参照してください。  
  
## <a name="determining-driver-support"></a>ドライバーサポートの決定  
 ドライバー対応接続プールは、ドライバーがサポートしていないオプションの機能です。 ドライバーでサポートされているかどうかを判断するには、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)の SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType*を使用します。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>ドライバー対応接続プールを有効にする方法  
 アプリケーションでは、SQL_ATTR_CONNECTION_POOLING 属性を [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)に SQL_CP_DRIVER_AWARE するように設定することによって、ドライバーの接続プール認識を使用できます。 ドライバーで接続プールの認識がサポートされていない場合は、ドライバーマネージャーの接続プールが使用されます (SQL_CP_DRIVER_AWARE ではなく SQL_CP_ONE_PER_HENV が指定されている場合と同じです)。 ODBC 2.x および2.x アプリケーションは、この機能を有効にすることができます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
