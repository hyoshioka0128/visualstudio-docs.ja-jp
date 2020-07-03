---
title: エラー - Web サービスのデバッグ中にタイムアウトしました | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
- XML Web services, timeout while debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: efb77689c33d263723f146f9b2484748505406b6
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460274"
---
# <a name="error-timeout-while-debugging-web-services"></a>エラー :Web サービスのデバッグ中にタイムアウトになりました
呼び出し元のコードから XML Web サービスにステップ インしている場合は、呼び出しがタイムアウトになってデバッグを継続できなくなることがあります。 この場合は、次のエラー メッセージが表示されます。

```cmd
An unhandled exception of type 'System.Net.WebException' occurred in
system.Web.services.dll
Additional information: The operation has timed-out.
```

## <a name="solution"></a>ソリューション
 この問題を回避するには、次の例で示すように、XML Web サービス呼び出しのタイムアウト値を無限に設定します。

```csharp
Service1 obj = new Service1();
obj.TimeOut = -1; // infinite time out.
```

## <a name="see-also"></a>関連項目
- [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
