---
title: コード化された UI テストのベスト プラクティス
description: コード化された UI テストの開発に関する推奨事項について説明します。 これらのガイドラインは、柔軟性のあるコード化された UI テストを作成するのに役立ちます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests, best practices
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a4a79ca397b46d06e18c62fde2034551ff7afe0
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95441808"
---
# <a name="best-practices-for-coded-ui-tests"></a>コード化された UI テストのベスト プラクティス

このトピックでは、コード化された UI テストの開発に関する推奨事項について説明します。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="best-practices"></a>ベスト プラクティス

柔軟性のあるコード化された UI テストを作成するには、次のガイドラインを使用します。

- 可能な限り **コード化された UI テスト ビルダー** を使用します。

- *UIMap.designer.cs* ファイルを直接変更しないでください。 ファイルを変更すると、その変更内容が上書きされます。

- 記録されたメソッドのシーケンスとしてテストを作成します。 メソッドを記録する方法の詳細については、「[コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)」を参照してください。

- 記録された各メソッドは、単一のページ、フォーム、またはダイアログ ボックスで動作する必要があります。 新しいページ、フォーム、またはダイアログ ボックスごとに新しいテスト メソッドを作成してください。

- メソッドを作成するときには、既定のメソッド名の代わりに、わかりやすい名前を使用します。 わかりやすい名前を付けておくと、メソッドの用途が明確になります。

- 可能な場合は、記録される各メソッドを 10 未満の操作に制限します。 このモジュール式のアプローチにより、UI が変更された場合にメソッドを置き換えやすくなります。

- 各アサーションは、**コード化された UI テスト ビルダー** を使用して作成します。この場合、アサーション メソッドは *UIMap.Designer.cs* ファイルに自動的に追加されます。

- ユーザー インターフェイス (UI) が変更された場合は、テスト メソッドまたはアサーション メソッドを再記録するか、既存のテスト メソッドの、影響を受けるセクションを再記録します。

- テスト対象のアプリケーションのモジュールごとに、個別の [UIMap](/previous-versions/dd580454(v=vs.140)) ファイルを作成します。 詳細については、「[複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)」をご覧ください。

- テスト対象のアプリケーションの UI コントロールを作成するときは、わかりやすい名前を使用します。 意味のある名前を使うと、自動生成されたコントロール名がいっそうわかりやすくて使いやすくなります。

- API を使用したコーディングによりアサーションを作成する場合は、*UIMap.cs* ファイル内の [UIMap](/previous-versions/dd580454(v=vs.140)) クラスの部分でアサーションごとにメソッドを作成します。 アサーションを実行するには、このメソッドをテスト メソッドから呼び出します。

- API を使用してコーディングを直接行う場合は、可能な限り、*UIMap.Designer.cs* ファイルに生成されたクラスのプロパティとメソッドをコードで使用します。 これらのクラスを使用すると、作業が楽になり、信頼性と生産性が高まります。

コード化された UI テストは、ユーザー インターフェイス内の多くの変更に自動的に適応します。 たとえば、UI 要素の位置や色が変更された場合、通常はコード化された UI テストにより適切な要素が検索されます。

テストの実行中、テスト フレームワークは一連の検索プロパティを使って UI コントロールを特定します。 検索プロパティは、**コード化された UI テスト ビルダー** によって作成された *UIMap.Designer.cs* ファイルの定義の各コントロール クラスに適用されます。 検索プロパティには、コントロールの識別に使用できるプロパティ名とプロパティ値の名前と値のペアが含まれます (コントロールの <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.FriendlyName%2A> プロパティ、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.Name%2A> プロパティ、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.ControlType%2A> プロパティなど)。 検索プロパティが変更されない場合、コード化された UI テストにより UI 内のコントロールが正常に検索されます。 検索プロパティが変更された場合、コード化された UI テストでは、UI 内のコントロールとウィンドウを検索するためのヒューリスティックを適用する高度な一致検出アルゴリズムを使用できます。 UI が変更されている場合は、以前識別された要素が確実に検出されるように、その要素の検索プロパティを変更できます。

## <a name="if-your-user-interface-changes"></a>ユーザー インターフェイスが変更された場合

開発中にユーザー インターフェイスが変更されることはよくあります。 このような変更の影響を軽減する方法を次に示します。

- このコントロールを参照する記録されたメソッドを見つけ、**コード化された UI テスト ビルダー** を使用してこのメソッドの操作を再記録します。 メソッドに同じ名前を使用すると、既存の操作を上書きできます。

- 有効ではなくなったアサーションがコントロールにある場合は、次の操作を実行します。

  - アサーションが含まれるメソッドを削除します。

  - テスト メソッドからこのメソッドへの呼び出しを削除します。

  - 十字線のボタンを UI コントロールにドラッグすることで新しいアサーションを追加し、UI マップを開いて新しいアサーションを追加します。

コード化された UI テストを記録する方法の詳細については、「[UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)」を参照してください。

## <a name="if-a-background-process-needs-to-complete-before-the-test-can-continue"></a>バック グラウンド プロセスが完了しないとテストを継続できない場合

プロセスが完了するまで待機しないと、次の UI 操作に進むことができない場合があります その場合は、次の例に示すように、テストを継続できるようになるまで、<xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyLevel%2A> を使用して待機できます。

```csharp
// Set the playback to wait for all threads to finish
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.AllThreads;

// Press the submit button
this.UIMap.ClickSubmit();

// Reset the playback to wait only for the UI thread to finish
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.UIThreadOnly;
```

## <a name="see-also"></a>関連項目

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UITesting>
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)
- [複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)
- [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
