---
title: コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests
ms.assetid: 544742b5-4ec1-4d51-b941-72b2f6ff17bc
caps.latest.revision: 108
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 946373cc304e4eddb9f724941d583ab653cfe140
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851752"
---
# <a name="supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings"></a>コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio Enterprise のコード化された UI テストがサポートされる構成とプラットフォームを、次の表に示します。 この構成は、 [!INCLUDE[MTRlong](../includes/mtrlong-md.md)]を使用して作成される操作の記録にも適用されます。

> [!NOTE]
> コード化された UI テスト プロセスには、テスト対象のアプリケーションと同じ特権が必要です。

 **必要条件**

- Visual Studio Enterprise

## <a name="supported-configurations"></a>サポートされている構成

|構成|サポートされています|
|-------------------|---------------|
|オペレーティング システム|[!INCLUDE[win7](../includes/win7-md.md)]<br /><br /> [!INCLUDE[winsvr08_r2](../includes/winsvr08-r2-md.md)]<br /><br /> [!INCLUDE[win8](../includes/win8-md.md)]<br /><br /> Windows 10|
|32 ビットと 64 ビットのサポート|32 ビットの [!INCLUDE[TCMext](../includes/tcmext-md.md)] を実行している 32 ビットの Windows では、32 ビット アプリケーションをテストできます。<br /><br /> 32 ビットの [!INCLUDE[TCMext](../includes/tcmext-md.md)] を実行している 64 ビットの Windows では、UI 同期を行う 32 ビットの WOW アプリケーションをテストできます。<br /><br /> 32 ビットの [!INCLUDE[TCMext](../includes/tcmext-md.md)] を実行している 64 ビットの Windows では、UI 同期を行わない 64 ビットの Windows フォーム アプリケーションおよび WPF アプリケーションをテストできます。|
|Architecture|x86 および x64 **注:** Internet Explorer は、[!INCLUDE[win8](../includes/win8-md.md)] 以降のバージョンで実行される場合を除き、64 ビット モードではサポートされていません。|
|.NET|.NET 2.0、3.0、3.5、4、および 4.5。 **注:** [!INCLUDE[TCMext](../includes/tcmext-md.md)] および Visual Studio が動作するには、いずれも .NET 4 が必要です。 ただし、一覧のバージョンの .NET を使用して開発されたアプリケーションはサポートされます。|

> [!NOTE]
> *UI 同期* とは、各コントロールのメッセージ キューで再生を検証する機能です。 送信されたイベントに対してコントロールが応答しなかった場合は、イベントが再度送信されます。

## <a name="platform-support"></a>プラットフォームのサポート

|プラットフォーム|サポートのレベル|
|--------------|----------------------|
|Windows Phone アプリ|WinRT-XAML ベースの Phone アプリだけがサポートされます。|
|Windows ストア アプリ|XAML ベースのストア アプリだけがサポートされます。|
|ユニバーサル Windows アプリ|Windows Phone およびデスクトップでは XAML ベースのユニバーサル Windows アプリだけがサポートされます。|
|エッジ|Visual Studio 2015 Update 2 以降で、[コード化された UI のクロス ブラウザー テストの拡張機能](https://visualstudiogallery.msdn.microsoft.com/11cfc881-f8c9-4f96-b303-a2780156628d)を使用|
|Internet Explorer 8<br /><br /> Internet Explorer 9<br /><br /> Internet Explorer 10 **重要:** Internet Explorer 10 は、デスクトップでのみサポートされています。 <br /><br /> Internet Explorer 11 **重要:** Internet Explorer 11 は、デスクトップでのみサポートされています。|完全にサポートされます。<br /><br /> -   **Internet explorer 9 および Internet explorer 10 での HTML5 のサポート:** コード化された UI テストは、HTML5 コントロール (オーディオ、ビデオ、ProgressBar、スライダー) の記録、再生、および検証をサポートしています。 詳細については、「コード化された [UI テストでの HTML5 コントロールの使用](../test/using-html5-controls-in-coded-ui-tests.md)」を参照してください。 **警告:** Internet Explorer 10 でコード化された UI テストを作成した場合、そのテストは Internet Explorer 9 または Internet Explorer 8 を使用して実行できないことがあります。 これは、Internet Explorer 10 には Audio、Video、ProgressBar、Slider などの HTML5 コントロールが含まれているためです。 これらの HTML5 コントロールは、Internet Explorer 9 または Internet Explorer 8 で認識されません。 同様に、Internet Explorer 9 を使用するコード化された UI テストには、Internet Explorer 8 で認識されない HTML5 コントロールが含まれる場合があります。<br />-   **Internet Explorer 10 のスペルチェックのサポート:** Internet Explorer 10 には、すべてのテキストボックスに対するスペルチェック機能が含まれています。 この機能を使用すると、提示される修正の一覧から選択することができます。 コード化された UI テストでは、提示されるスペル候補の選択などのユーザー アクションは無視されます。 テキスト ボックスに入力された最終的なテキストのみが記録されます。<br />     スペル チェック コントロールを使用する一部の操作 (ディクショナリへの追加、コピー、すべて選択、および無視) は、コード化された UI テスト用に記録されます。<br />-   **Windows 8 で実行されている 64-Bit Internet Explorer のサポート:** 以前は、64ビットバージョンの Internet Explorer は、記録と再生がサポートされていませんでした。 [!INCLUDE[win8](../includes/win8-md.md)] と [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]によって、コード化された UI テストは、Internet Explorer の 64 ビット バージョンで使用可能になりました。 **警告:**      Internet Explorer の 64 ビット バージョンのサポートは、[!INCLUDE[win8](../includes/win8-md.md)] 以降を実行しているときにのみ適用されます。<br />-   **Internet Explorer 9 での固定サイトのサポート:** Internet Explorer 9 では、ピン留めされたサイトが導入されました。 固定サイトを使用すると、最初に Internet Explorer を開かなくても、Windows タスク バーからお気に入りのサイトに直接アクセスできます。 コード化された UI テストは、固定サイトでの目的に応じた操作を生成できるようになりました。 固定サイトの詳細については、「 [サイトの固定](https://windows.microsoft.com/en-US/internet-explorer/products/ie-9/features/pinned-sites)」を参照してください。<br />-   **Internet Explorer 9 のセマンティックタグのサポート:** Internet Explorer 9 では、セクション、nav、article、アサイド、hgroup、header、footer、figure、figcaption、および mark というセマンティックタグが導入されました。 コード化された UI テストでは、記録中はこれらのセマンティック タグがすべて無視されます。 コード化された UI テスト ビルダーを使用して、これらのタグのアサーションを追加できます。 コード化された UI テスト ビルダーで、ナビゲーション ダイヤルを使用してこれらの要素に移動し、そのプロパティを表示することができます。<br />-   **Internet Explorer のバージョン間での空白文字のシームレスな処理:** Internet Explorer 8、Internet Explorer 9、および Internet Explorer 10 の間には、空白文字の処理に違いがあります。 コード化された UI テストは、これらの違いをシームレスに処理します。 たとえば、Internet Explorer 8 で作成されたコード化された UI テストは、Internet Explorer 9 と Internet Explorer 10 で正常に再生されます。<br />-   **Internet Explorer の通知領域が "エラー時に続行" 属性を設定した状態で記録される:** Internet Explorer の通知領域のすべての操作が、"エラー時に続行" 属性を設定した状態で記録されるようになりました。 再生中に通知バーが表示されない場合、それに対する操作は無視され、コード化された UI テストは次の操作を続行します。|
|Windows フォームと WPF のサードパーティ製コントロール|完全にサポートされます。<br /><br /> Windows フォームと WPF アプリケーションでサードパーティ製コントロールを有効にするには、参照とコードを追加する必要があります。 詳細については、「[コントロールのコード化された UI テストの有効化](../test/enable-coded-ui-testing-of-your-controls.md)」をご覧ください。|
|Internet Explorer 6<br /><br /> Internet Explorer 7|サポートされていません。|
|Chrome<br /><br /> Firefox|操作手順の記録はサポートされていません。 コード化された UI テストは、Chrome および Firefox ブラウザー上で、Visual Studio 2012 Update 4 以降で再生できます。 詳細については、 [こちら](https://msdn.microsoft.com/library/jj835758.aspx) を参照してください。|
|Opera<br /><br /> Safari|サポートされていません。|
|Silverlight|サポートされていません。<br /><br /> ただし、Visual Studo 2013 の場合、Visual Studio ギャラリーから [Silverlight 用 Microsoft Visual Studio 2013 のコード化された UI テスト プラグイン](https://marketplace.visualstudio.com/items?itemName=PrachiBoraMSFT.MicrosoftVisualStudio2013CodedUITestPluginforSilve) をダウンロードできます。|
|Flash および Java|サポートされていません。|
|Windows フォーム 2.0 以降|完全にサポートされます。 **注:** NetFx コントロールは完全にサポートされていますが、一部のサードパーティ コントロールはサポートされていません。|
|WPF 3.5 以降|完全にサポートされます。<br /><br /> **メモ** NetFx コントロールは完全にサポートされていますが、一部のサードパーティコントロールはサポートされていません。|
|Windows Win32|既知の問題がいくつか存在しますが、動作する可能性があります。ただし、公式にはサポートされていません。|
|MFC|一部サポートされています。 サポートされる機能の詳細については、 [Microsoft Web サイト](https://blogs.msdn.com/b/vstsqualitytools/archive/2010/04/15/uitest-framework-mfc-support-in-vs-2010.aspx) を参照してください。|
|SharePoint|完全にサポートされます。|
|Office クライアント アプリケーション|サポートされていません。|
|Dynamics CRM Web クライアント|完全にサポートされます。|
|Dynamics (Ax) 2012 クライアント|操作の記録と再生が部分的にサポートされています。 詳細については、 [Microsoft Web サイト](https://blogs.msdn.com/b/dave_froslie/archive/2011/09/01/visual-studio-10-coded-ui-action-recordings-support-for-microsoft-dynamics-ax-2012.aspx) を参照してください。|
|SAP|サポートされていません。|
|Citrix およびターミナル サービス|ターミナル サーバーに対する操作の記録はお勧めしません。 レコーダーは、複数のインスタンスの同時実行をサポートしていません。|
|PowerBuilder|一部サポートされています。<br /><br /> サポートは、PowerBuilder コントロールに対してユーザー補助が有効である程度までです。|

 その他のプラットフォームをサポートするための拡張機能の作成方法については、「[コントロールのコード化された UI テストの有効化](../test/enable-coded-ui-testing-of-your-controls.md)」および「[コード化された UI テストと操作の記録を拡張して Microsoft Excel をサポート](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)」をご覧ください。

## <a name="see-also"></a>参照
 [UI オートメーションを使用して、](../test/use-ui-automation-to-test-your-code.md) [既存の操作の記録からコード化された ui テストを生成](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)するコードをテストする
