---
title: コード化された UI テストのベスト プラクティス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests, best practices
ms.assetid: d5aef766-a24c-4f1f-ac9b-e5462b6627d4
caps.latest.revision: 41
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2dffebeaa0349c149e319d20794f8b065baa5647
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660688"
---
# <a name="best-practices-for-coded-ui-tests"></a>コード化された UI テストのベスト プラクティス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、コード化された UI テストの開発手順におけるベスト プラクティスについて説明します。

 **必要条件**

- Visual Studio Enterprise

## <a name="best-practices"></a>ベスト プラクティス
 柔軟性のあるコード化された UI テストを作成するには、次のガイドラインを使用します。

- 可能な限り**コード化された UI テスト ビルダー**を使用します。

- `UIMap.designer.cs` ファイルは直接変更しないでください。 このファイルを直接変更すると、その変更内容が上書きされます。

- 記録されたメソッドのシーケンスとしてテストを作成します。 メソッドを記録する方法の詳細については、「コード化された [UI テストの作成](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)」を参照してください。

- 記録された各メソッドは、単一のページ、フォーム、またはダイアログ ボックスで動作する必要があります。 新しいページ、フォーム、またはダイアログ ボックスごとに新しいテスト メソッドを作成してください。

- メソッドを作成するときには、既定のメソッド名の代わりに、わかりやすい名前を使用します。 わかりやすい名前を付けておくと、メソッドの用途が明確になります。

- 可能な場合は、記録される各メソッドを 10 未満の操作に制限します。 このモジュール式のアプローチにより、UI が変更された場合にメソッドを置き換えやすくなります。

- 各アサーションは、**コード化された UI テスト ビルダー**を使用して作成します。この場合、アサーション メソッドは `UIMap.Designer.cs` ファイルに自動的に追加されます。

- ユーザー インターフェイス (UI) が変更された場合は、テスト メソッドまたはアサーション メソッドを再記録するか、既存のテスト メソッドの、影響を受けるセクションを再記録します。

- テスト対象のアプリケーションのモジュールごとに、個別の [UIMap](/previous-versions/dd580454(v=vs.140)) ファイルを作成します。 詳細については、「 [複数の UI マップを使用した大規模なアプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)」を参照してください。

- テスト対象のアプリケーションの UI コントロールを作成するときは、わかりやすい名前を使用します。 これにより、自動生成されたコントロール名に意味が加えられて使いやすくなります。

- API を使用してコーディングすることによってアサーションを作成する場合は、ファイル内にある [Uimap](/previous-versions/dd580454(v=vs.140)) クラスの部分でアサーションごとにメソッドを作成し `UIMap.cs` ます。 このメソッドをテスト メソッドから呼び出してアサーションを実行します。

- API を使用してコーディングを直接行う場合は、可能な限り、`UIMap.Designer.cs` ファイルに生成されたクラスのプロパティとメソッドをコードで使用します。 これらのクラスを使用すると、作業が楽になり、信頼性と生産性が高まります。

  コード化された UI テストは、ユーザー インターフェイス内の多くの変更に自動的に適応します。 たとえば、UI 要素の位置や色が変更された場合、通常はコード化された UI テストにより適切な要素が検索されます。

  テストの実行中、UI コントロールはテスト フレームワークによって検索されます。その際、**コード化された UI テスト ビルダー**によって `UIMap.Designer.cs` ファイルに作成された定義の各コントロール クラスに適用される、一連の検索プロパティが使用されます。 検索プロパティには、コントロールの識別に使用できるプロパティ名とプロパティ値の名前と値のペアが含まれます (コントロールの <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.FriendlyName%2A> プロパティ、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.Name%2A> プロパティ、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.ControlType%2A> プロパティなど)。 検索プロパティが変更されない場合、コード化された UI テストにより UI 内のコントロールが正常に検索されます。 検索プロパティが変更された場合、コード化された UI テストでは、UI 内のコントロールとウィンドウを検索するためのヒューリスティックを適用する高度な一致検出アルゴリズムを使用できます。 UI が変更されている場合は、以前識別された要素が確実に検出されるように、その要素の検索プロパティを変更できます。

## <a name="what-to-do-if-your-user-interface-changes"></a>ユーザー インターフェイスが変更された場合の作業
 開発中にユーザー インターフェイスが変更されることはよくあります。 このような変更の影響を軽減する方法を次に示します。

- このコントロールを参照する記録されたメソッドを見つけ、**コード化された UI テスト ビルダー**を使用してこのメソッドの操作を再記録します。 メソッドに同じ名前を使用すると、既存の操作を上書きできます。

- 有効ではなくなったアサーションがコントロールにある場合は、次の操作を実行します。

  - アサーションが含まれるメソッドを削除します。

  - テスト メソッドからこのメソッドへの呼び出しを削除します。

  - 十字線のボタンを UI コントロールにドラッグすることで新しいアサーションを追加し、UI マップを開いて新しいアサーションを追加します。

  コード化された UI テストを記録する方法の詳細については、「 [Ui オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)」を参照してください。

## <a name="what-to-do-if-a-background-process-needs-to-complete-before-the-test-can-continue"></a>バック グラウンド プロセスが完了しないとテストを継続できない場合の作業
 プロセスが完了するまで待機しないと、次の UI 操作に進むことができない場合があります その場合は、次のサンプルに示すように、テストを継続できるようになるまで、<xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyLevel%2A> を使用して待機できます。

```
// Set the playback to wait for all threads to finish
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.AllThreads;

// Press the submit button
this.UIMap.ClickSubmit();

// Reset the playback to wait only for the UI thread to finish
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.UIThreadOnly;
```

## <a name="see-also"></a>こちらもご覧ください

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UITesting>
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストの作成](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)
- [複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)
- [コード化された UI テストと操作の記録でサポートされる構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
