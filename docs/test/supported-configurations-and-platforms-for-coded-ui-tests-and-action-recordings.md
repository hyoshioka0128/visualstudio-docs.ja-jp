---
title: コード化された UI テストの構成とプラットフォーム
ms.date: 10/04/2015
ms.topic: reference
helpviewer_keywords:
- coded UI tests
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: e18e50537f35080f9796f4a090b3806953ae5170
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75845809"
---
# <a name="supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings"></a>コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム

Visual Studio Enterprise のコード化された UI テストがサポートされる構成とプラットフォームを、次の表に示します。 この構成は、 [!INCLUDE[MTRlong](../test/includes/mtrlong_md.md)]を使用して作成される操作の記録にも適用されます。

> [!NOTE]
> コード化された UI テスト プロセスには、テスト対象のアプリケーションと同じ特権が必要です。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**必要条件**

- Visual Studio Enterprise

## <a name="supported-configurations"></a>サポートされている構成

| 構成 | サポートされています |
|-| - |
| オペレーティング システム | [!INCLUDE[win7](../debugger/includes/win7_md.md)]<br /><br /> [!INCLUDE[winsvr08_r2](../debugger/includes/winsvr08_r2_md.md)]<br /><br /> [!INCLUDE[win8](../debugger/includes/win8_md.md)]<br /><br /> Windows 10 |
| 32 ビットと 64 ビットのサポート | 32 ビットの [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] を実行している 32 ビットの Windows では、32 ビット アプリケーションをテストできます。<br /><br /> 32 ビットの [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] を実行している 64 ビットの Windows では、UI 同期を行う 32 ビットの WOW アプリケーションをテストできます。<br /><br /> 32 ビットの [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] を実行している 64 ビットの Windows では、UI 同期を行わない 64 ビットの Windows フォーム アプリケーションおよび WPF アプリケーションをテストできます。 |
| Architecture | x86 および x64 **注:** Internet Explorer は、[!INCLUDE[win8](../debugger/includes/win8_md.md)] 以降のバージョンで実行される場合を除き、64 ビット モードではサポートされていません。 |
| .NET | .NET 2.0、3.0、3.5、4、および 4.5。 **注:** [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] および Visual Studio が動作するには、いずれも .NET 4 が必要です。 ただし、一覧のバージョンの .NET を使用して開発されたアプリケーションはサポートされます。 |

> [!NOTE]
> *UI 同期* とは、各コントロールのメッセージ キューで再生を検証する機能です。 送信されたイベントに対してコントロールが応答しなかった場合は、イベントが再度送信されます。

## <a name="platform-support"></a>プラットフォームのサポート

| プラットフォーム | サポートのレベル |
|-| - |
| Windows Phone アプリ | WinRT-XAML ベースの Phone アプリだけがサポートされます。 |
| UWP アプリ | XAML ベースの UWP アプリだけがサポートされます。 |
| ユニバーサル Windows アプリ | Windows Phone およびデスクトップでは XAML ベースのユニバーサル Windows アプリだけがサポートされます。 |
| エッジ | 操作手順の記録と、ビルダーを利用したオブジェクトのプロパティの表示はサポートされていません。 テストは Visual Studio 2015 Update 2 以降のバージョンを利用し、Microsoft Edge ブラウザーで再生できます。その際、[コード化された UI のクロス ブラウザー テスト拡張](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)を利用してください。 |
| Internet Explorer 8<br /><br /> Internet Explorer 9<br /><br /> Internet Explorer 10 **重要:** Internet Explorer 10 は、デスクトップでのみサポートされています。 <br /><br /> Internet Explorer 11 **重要:** Internet Explorer 11 は、デスクトップでのみサポートされています。 | 完全にサポートされます。<br /><br /> -   **Internet Explorer 9 および Internet Explorer 10 での HTML5 のサポート:** コード化された UI テストは、HTML5 コントロール (Audio、Video、ProgressBar、および Slider) の記録、再生、および検証をサポートします。 詳細については、「[コード化された UI テストでの HTML5 コントロールの使用](../test/using-html5-controls-in-coded-ui-tests.md)」をご覧ください。 **警告:** Internet Explorer 10 でコード化された UI テストを作成した場合、そのテストは Internet Explorer 9 または Internet Explorer 8 を使用して実行できないことがあります。 これは、Internet Explorer 10 には Audio、Video、ProgressBar、Slider などの HTML5 コントロールが含まれているためです。 これらの HTML5 コントロールは、Internet Explorer 9 または Internet Explorer 8 で認識されません。 同様に、Internet Explorer 9 を使用するコード化された UI テストには、Internet Explorer 8 で認識されない HTML5 コントロールが含まれる場合があります。<br />-   **Internet Explorer 10 のスペル チェックのサポート:** Internet Explorer 10 には、すべてのテキスト ボックスに対するスペル チェック機能が含まれています。 この機能を使用すると、提示される修正の一覧から選択することができます。 コード化された UI テストでは、提示されるスペル候補の選択などのユーザー アクションは無視されます。 テキスト ボックスに入力された最終的なテキストのみが記録されます。<br />     スペル チェック コントロールを使用する一部の操作 (ディクショナリへの追加、コピー、すべて選択、および無視) は、コード化された UI テスト用に記録されます。<br />-   **Windows 8 上で実行する 64 ビット Internet Explorer のサポート:** 以前は、Internet Explorer の 64 ビット バージョンは記録および再生用にサポートされていませんでした。 [!INCLUDE[win8](../debugger/includes/win8_md.md)] と [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] によって、コード化された UI テストは、Internet Explorer の 64 ビット バージョンで使用可能になりました。 **警告:**      Internet Explorer の 64 ビット バージョンのサポートは、[!INCLUDE[win8](../debugger/includes/win8_md.md)] 以降を実行しているときにのみ適用されます。<br />-   **Internet Explorer 9 の固定サイトのサポート:** Internet Explorer 9 で固定サイトが導入されました。 固定サイトを使用すると、最初に Internet Explorer を開かなくても、Windows タスク バーからお気に入りのサイトに直接アクセスできます。 コード化された UI テストは、固定サイトでの目的に応じた操作を生成できるようになりました。 固定サイトの詳細については、[サイトの固定](https://support.microsoft.com/hub/4230784/internet-explorer-help)に関するページを参照してください。<br />-   **Internet Explorer 9 のセマンティック タグのサポート:** Internet Explorer 9 で、セマンティック タグ (section、nav、article、aside、hgroup、header、footer、figure、figcaption、および mark) が導入されました。 コード化された UI テストでは、記録中はこれらのセマンティック タグがすべて無視されます。 コード化された UI テスト ビルダーを使用して、これらのタグのアサーションを追加できます。 コード化された UI テスト ビルダーで、ナビゲーション ダイヤルを使用してこれらの要素に移動し、そのプロパティを表示することができます。<br />-   **Internet Explorer のバージョン間の空白文字のシームレスな処理:** Internet Explorer 8、Internet Explorer 9、Internet Explorer 10 の間には、空白文字の処理に違いがあります。 コード化された UI テストは、これらの違いをシームレスに処理します。 たとえば、Internet Explorer 8 で作成されたコード化された UI テストは、Internet Explorer 9 と Internet Explorer 10 で正常に再生されます。<br />-   **Internet Explorer の通知領域が "エラー時に続行" 属性を設定した状態で記録される:** Internet Explorer の通知領域のすべての操作が、"エラー時に続行" 属性を設定した状態で記録されるようになりました。 再生中に通知バーが表示されない場合、それに対する操作は無視され、コード化された UI テストは次の操作を続行します。 |
| Windows フォームと WPF のサードパーティ製コントロール | 完全にサポートされます。<br /><br /> Windows フォームと WPF アプリケーションでサードパーティ製コントロールを有効にするには、参照とコードを追加する必要があります。 詳細については、「[コントロールのコード化された UI テストを有効化する](../test/enable-coded-ui-testing-of-your-controls.md)」をご覧ください。 |
| Internet Explorer 6<br /><br /> Internet Explorer 7 | サポートされていません。 |
| Chrome<br /><br /> Firefox | 操作手順の記録はサポートされていません。 コード化された UI テストは、Chrome および Firefox ブラウザー上で、Visual Studio 2012 Update 4 以降で再生できます。 詳細については、 [こちら](using-different-web-browsers-with-coded-ui-tests.md) を参照してください。 |
| Opera<br /><br /> Safari | サポートされていません。 |
| Silverlight | サポートされていません。<br /><br /> ただし、Visual Studio 2013 の場合、Visual Studio ギャラリーから [Silverlight 用 Microsoft Visual Studio 2013 のコード化された UI テスト プラグイン](https://marketplace.visualstudio.com/items?itemName=PrachiBoraMSFT.MicrosoftVisualStudio2013CodedUITestPluginforSilve) をダウンロードできます。 |
| Flash および Java | サポートされていません。 |
| Windows フォーム 2.0 以降 | 完全にサポートされます。 **注:** NetFx コントロールは完全にサポートされていますが、一部のサードパーティ コントロールはサポートされていません。 |
| WPF 3.5 以降 | 完全にサポートされます。<br /><br /> **メモ** NetFx コントロールは完全にサポートされていますが、一部のサードパーティ コントロールはサポートされていません。 |
| Windows Win32 | 既知の問題がいくつか存在しますが、動作する可能性があります。ただし、公式にはサポートされていません。 |
| MFC | 一部サポートされています。 サポートされている機能について詳しくは、「[UITest framework](https://blogs.msdn.microsoft.com/vstsqualitytools/2010/04/15/uitest-framework-mfc-support-in-vs-2010/)」(UITest フレームワーク) をご覧ください。 |
| SharePoint | 完全にサポートされます。 |
| Office クライアント アプリケーション | サポートされていません。 |
| Dynamics CRM Web クライアント | 完全にサポートされます。 |
| Dynamics (Ax) 2012 クライアント | 操作の記録と再生が部分的にサポートされています。 詳しくは、「[Visual Studio 10 Coded UI / Action Recordings support for Microsoft Dynamics](https://blogs.msdn.microsoft.com/dave_froslie/2011/09/01/visual-studio-10-coded-ui-action-recordings-support-for-microsoft-dynamics-ax-2012/)」(Visual Studio 10 のコード化された UI/Microsoft Dynamics の操作の記録のサポート) をご覧ください。 |
| SAP | サポートされていません。 |
| Citrix およびターミナル サービス | ターミナル サーバーに対する操作の記録はお勧めしません。 レコーダーは、複数のインスタンスの同時実行をサポートしていません。 |
| PowerBuilder | 一部サポートされています。<br /><br /> サポートは、PowerBuilder コントロールに対してユーザー補助が有効である程度までです。 |

その他のプラットフォームをサポートするための拡張機能の作成方法については、「[コントロールのコード化された UI テストを有効化する](../test/enable-coded-ui-testing-of-your-controls.md)」および「[コード化された UI テストと操作の記録を拡張する](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)」をご覧ください。

## <a name="see-also"></a>参照

- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
