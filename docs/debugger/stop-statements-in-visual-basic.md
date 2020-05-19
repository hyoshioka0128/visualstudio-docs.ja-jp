---
title: Visual Basic の Stop ステートメント | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- End statements
- breakpoints, Stop statements
- debugging managed code, Stop statements vs breakpoints
- Stop statements, about Stop statements
- debugging [Visual Basic], Stop statements vs. breakpoints
ms.assetid: 4ad3fe5c-3dfb-4913-b2eb-a0b635751c18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f9ab4ef453a921371ab7ef4f272cd0e38f4108a
ms.sourcegitcommit: 4d2620bee4688fb881e09a07ea4a264b99f0743e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71322531"
---
# <a name="stop-statements-in-visual-basic"></a>Visual Basic の Stop ステートメント

ブレークポイントを設定する別の方法として、Visual Basic の Stop ステートメントをプログラムで使用できます。 デバッガーが Stop ステートメントを実行すると、プログラムの実行が中断されます。つまり、中断モードに入ります。 C# プログラマは、<xref:System.Diagnostics.Debugger.Break%2A?displayProperty=nameWithType> の呼び出しを使用して同じ効果を得ることができます。

ソース コードを編集することで Stop ステートメントを設定または削除できます。 デバッガー コマンドでは、ブレークポイントを設定またはクリアできますが、Stop ステートメントを設定またはクリアすることはできません。

Stop ステートメントは、End ステートメントとは異なり、変数をリセットしたり、デザイン モードに戻ったりすることはありません。 アプリケーションの実行を継続するには [デバッグ] メニューの [続行] をクリックします。

Just-In-Time デバッグが有効な場合は、デバッガーの外部で実行中の Visual Basic アプリケーションの Stop ステートメントによって、デバッガーが起動します。 Just-In-Time デバッグが有効でない場合、Stop ステートメントは End ステートメントと同様に機能し、実行を終了します。 QueryUnload イベントや Unload イベントが発生しないため、Visual Basic アプリケーションのリリース バージョンに設定されたすべての Stop ステートメントを削除する必要があります。 詳細については、「[Just-In-Time デバッグ](just-in-time-debugging-in-visual-studio.md)」を参照してください。

 Stop ステートメントを削除しなくて済むようにするには、次のような条件付きコンパイルを使用できます。

```vb
#If DEBUG Then
   Stop
#Else
   ' Don't stop
#End If
```

Stop ステートメントの代わりに、<xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> ステートメントを使用する方法もあります。 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> ステートメントを使用すると、指定された条件が満たされない場合にのみ実行が中断されます。 リリース バージョンをビルドすると、<xref:System.Diagnostics.Debug.Assert%2A> ステートメントは自動的に削除されます。 詳細については、「[マネージド コードのアサーション](assertions-in-managed-code.md)」を参照してください。 デバッグ バージョンで常に実行を中断する <xref:System.Diagnostics.Debug.Assert%2A> ステートメントが必要な場合は、次のコードを使用します。

```csharp
Debug.Assert(false);
```

```vb
Debug.Assert(False)
```

<xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> メソッドを使用するという方法もあります。

```csharp
Debug.Fail("a clever output string goes here");
```

```vb
Debug.Fail("a clever output string goes here")
```

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](debugger-security.md)
- [C#、F#、および Visual Basic のプロジェクト](debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [マネージド コードをデバッグする](debugging-managed-code.md)
