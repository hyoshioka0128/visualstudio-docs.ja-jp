---
title: 再生中に特定のイベントを待機するようにコード化された UI テストを設定 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 41981ad6-673e-492e-b739-9863b14157b1
caps.latest.revision: 26
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 266c4fd418b71c61391ac3b9b20ac93e5c77428c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302551"
---
# <a name="making-coded-ui-tests-wait-for-specific-events-during-playback"></a>再生中に特定のイベントを待機するようにコード化された UIT テストを設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード化された UI テストの再生では、テストに対して指示することで、ウィンドウの表示やプログレス バーの非表示などの特定のイベントが発生するまで待機することができます。 これを実行するには、次の表で説明されているように、該当する UITestControl.WaitForControlXXX() メソッドを使用します。 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A> メソッドで有効化されるコントロールを待機するコード化された UI テストの例については、「[チュートリアル: コード化された UI テストの作成、編集、および保守](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)」を参照してください。

 **Requirements**

 Visual Studio Enterprise

> [!TIP]
> またコード化された UI テスト エディターで操作の前に遅延を追加することもできます。 詳細については、「[How to: Insert a Delay Before a UI Action Using the Coded UI Test Editor](https://msdn.microsoft.com/library/509f8ef7-e105-4049-b11b-d64549e055b0) (方法: コード化された UI テスト エディターを使用して UI アクションの前に遅延を挿入する)」をご覧ください。

 **UITestControl.WaitForControlXXX() メソッド**

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlReady%2A>

 コントロールでマウスおよびキーボード入力を受け入れる準備が整うまで待機します。 エンジンは、すべての操作についてこの API を暗黙的に呼び出してコントロールの準備が整うまで待機し、その後、なんらかの操作を実行します。 ただし、複雑なシナリオでは、明示的に呼び出すことが必要になる場合があります。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>

 サーバーを呼び出すことでウィザードが入力の非同期の検証を実行するときに、コントロールが有効化されるまで待機します。 たとえば、このメソッドを使用してウィザードの **[次へ]** ボタンが有効化されるまで待機します。 このメソッドの使用例については、「[Walkthrough: Creating, Editing and Maintaining a Coded UI Test](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md) (チュートリアル: コード化された UI テストの作成、編集、および保守)」をご覧ください。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlExist%2A>

 コントロールが UI に表示されるまで待機します。 たとえば、アプリケーションでパラメーターの検証が行われた後にエラー ダイアログの表示を必要とする場合などです。 検証にかかる時間はさまざまです。 このメソッドを使用してエラー ダイアログ ボックスを待機することができます。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlNotExist%2A>

 コントロールが UI から非表示になるまで待機します。 たとえば、プログレス バーが表示されなくなるまで待機する場合などです。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyEqual%2A>

 指定されたコントロールのプロパティが指定された値になるまで待機します。 たとえば、ステータス テキストが**完了**になるまで待機します。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyNotEqual%2A>

 指定されたコントロールのプロパティが指定された値の逆になるまで待機します。 たとえば、編集ボックスが読み取り専用ではなくなる、つまり、編集可能になるまで待機します。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlCondition%2A>

 指定された述語で `true` が返されるまで待機します。 これは、指定されたコントロールでの複合的な待機操作 (OR 条件など) で使用できます。 たとえば、次のコードに示されているように、ステータス テキストが **Succeeded** または **Failed** になるまで待機する場合があります。

```csharp

// Define the method to evaluate the condition
private static bool IsStatusDone(UITestControl control)
{
    WinText statusText = control as WinText;
    return statusText.DisplayText == "Succeeded" || statusText.DisplayText == "Failed";
}

// In test method, wait till the method evaluates to true
statusText.WaitForControlCondition(IsStatusDone);

```

 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForCondition%2A>

 上に示したメソッドはすべて UITestControl のインスタンス メソッドです。 このメソッドは静的なメソッドです。 このメソッドも指定された述語が `true` になるまで待機しますが、複数のコントロールの複合的な待機操作 (OR 条件など) で使用される場合があります。 たとえば、次のコードに示されているように、ステータス テキストが **Succeeded** になるか、エラー メッセージが表示されるまで待機する場合があります。

```csharp

// Define the method to evaluate the condition
private static bool IsStatusDoneOrError(UITestControl[] controls)
{
    WinText statusText = controls[0] as WinText;
    WinWindow errorDialog = controls[1] as WinWindow;
    return statusText.DisplayText == "Succeeded" || errorDialog.Exists;
}

// In test method, wait till the method evaluates to true
UITestControl.WaitForCondition<UITestControl[]>(new UITestControl[] { statusText, errorDialog }, IsStatusDoneOrError);

```

 上記のメソッドはすべて次のように動作します。

 待機が成功すれば true を返し、失敗すれば false を返します。

 待機操作の暗黙的なタイムアウトは、<xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyTimeout%2A> プロパティによって指定されます。 このプロパティの既定値は 60000 ミリ秒 (1 分) です。

 メソッドには、ミリ秒単位の明示的なタイムアウトを取得するためのオーバーロードがあります。 ただし、待機操作の結果、コントロールが暗黙的に検索されたり、アプリケーションがビジー状態であったりすると、実際の待機時間が指定されたタイムアウトよりも長くなる可能性があります。

 上で説明した機能は強力で柔軟性があり、ほとんどの条件を満たすと考えられます。 しかし、これらのメソッドでもニーズが満たされず、コード内で <xref:Microsoft.VisualStudio.TestTools.UITesting.Playback.Wait%2A> または <xref:System.Threading.Thread.Sleep%2A> をコード化する必要がある場合は、Thread.Sleep() API の代わりに Playback.Wait() を使用することをお勧めします。 これには次の理由があります。

 <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.ThinkTimeMultiplier%2A> プロパティを使用してスリープの継続時間を変更できます。 既定ではこの変数は 1 ですが、値を増減させてコード全体で待機時間を変更することができます。 たとえば、低速なネットワークで特別にテストを実行する場合や、その他のパフォーマンスが低下している状況で、特定の位置で (または構成ファイル内で) この変数を 1.5 に変更すると、あらゆる位置の待機時間を 50% 余分に追加できます。

 Playback.Wait() は、ユーザー取り消し/ブレーク操作の確認中に for ループ内の小さなチャンクで Thread.Sleep() を呼び出します (上記の計算後)。 つまり、Playback.Wait() を使用すると、スリープにならなかったり、例外が発生しても、待機が完了する前に再生を取り消すことができます。

> [!TIP]
> コード化された UI テスト エディターを使用すると、コード化された UI テストを簡単に変更できます。 Coded UI Test Editor (コード化された UI テスト エディター) を使用すると、テスト メソッドを検索、表示、および編集できます。 また、UI コントロール マップ内の UI 操作および関連コントロールを編集することもできます。 詳細については、「[コード化された UI テスト エディターを使用したコード化された UI テストの編集](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)」をご覧ください。

 **ガイダンス**

 追加のガイダンスについては、「[Testing for Continuous Delivery with Visual Studio 2012 – Chapter 5: Automating System Tests](https://go.microsoft.com/fwlink/?LinkID=255196) (Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 5 章: システム テストの自動化)」をご覧ください。

## <a name="see-also"></a>参照
 [Use UI Automation To Test Your Code](../test/use-ui-automation-to-test-your-code.md) [Creating Coded UI Tests](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate) [Walkthrough: Creating, Editing and Maintaining a Coded UI Test](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md) [Anatomy of a Coded UI Test](../test/anatomy-of-a-coded-ui-test.md) [Supported Configurations and Platforms for Coded UI Tests and Action Recordings](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md) [How to: Insert a Delay Before a UI Action Using the Coded UI Test Editor](https://msdn.microsoft.com/library/509f8ef7-e105-4049-b11b-d64549e055b0)
