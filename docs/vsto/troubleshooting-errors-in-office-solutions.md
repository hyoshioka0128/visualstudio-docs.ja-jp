---
title: Office ソリューションで発生したエラーのトラブルシューティング
description: Visual Studio で Microsoft Office ソリューションを開発するときに発生する可能性のあるエラーをトラブルシューティングする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: troubleshooting
f1_keywords:
- VST.Project.DesignerDisabled
- VST.Designer.CannotActivate
- VST.Project.ExcelBusy
- VST.SelectDocWizard.AlreadyCustomized
- VST.SelectDocWizard.DocPath
- VST.Project.CannotOpen
- VST.Designer.ErrorsOccurred
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- troubleshooting [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3bc1b674caf46dc84ff7bf57c983131b79cfde51
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827813"
---
# <a name="troubleshoot-errors-in-office-solutions"></a>Office ソリューションで発生したエラーのトラブルシューティング
  Visual Studio で Office ソリューションを開発する際、次のタスクを実行するときに問題が発生する場合があります。

- [プロジェクトの作成、アップグレード、および開く](#creating)

- [デザイナーを使用する](#designers)

- [コードの記述](#code)

- [プロジェクトをビルドする](#building)

- [プロジェクトのデバッグ](#debugging)

## <a name="create-upgrade-and-open-projects"></a><a name="creating"></a> プロジェクトの作成、アップグレード、および開く
 Office プロジェクトを作成、または開くときに、次のエラーが発生する場合があります。

### <a name="the-project-cannot-be-created"></a>プロジェクトを作成できません
 Office プロジェクトを作成または開こうとするときにエラーが発生しましたが、Visual Studio では、原因を特定するのに十分な情報がありませんでした。 プロジェクトを閉じ、Visual Studio を終了してから、再起動してみてください。

 ドキュメント レベルのプロジェクトを作成しようとしている場合、新しいプロジェクトのドキュメントと同じ名前を持つ別のドキュメントが Excel または Word で開いている可能性があります。 Excel または Word の他のすべてのインスタンスが閉じられていることを確認してください。

### <a name="control-properties-are-lost-when-you-create-a-new-project-based-on-a-document-from-an-existing-project"></a>既存のプロジェクトからドキュメントに基づいて新しいプロジェクトを作成すると、コントロールのプロパティが失われる
 既存のプロジェクトのドキュメントに基づいて新しい Office プロジェクトを作成する場合、既存のドキュメントにあるコントロールのプロパティが新しいプロジェクトにコピーされることはありません。 すべての既存のコントロールのプロパティを手動で設定する必要があります。 または、新しいプロジェクトを作成する代わりに既存のプロジェクトのコピーを作成するか、(デザイナーで) 新しいソリューションに既存のプロジェクトを読み込んだうえで、既存のドキュメントから新しいドキュメントにコントロールをコピーして貼り付ければ、コントロールのプロパティを保持できます。

### <a name="errors-when-you-create-an-excel-workbook-project-based-on-an-existing-workbook"></a>既存のブックに基づいて Excel ブックプロジェクトを作成するときにエラーが発生する
 既存のブックに基づいて新しい Excel ブックプロジェクトを作成すると、次のエラーの組み合わせが表示される場合があります。

 Excel から: "プライバシーに関する注意: このドキュメントには、マクロ、ActiveX コントロール、XML 拡張パック情報、または Web コンポーネントが含まれています。 これらには、ドキュメント検査で削除できない個人情報が含まれている場合があります。"

 Visual Studio から: "デザイナーの読み込みが正しくできませんでした。"

 これらのエラーは、ドキュメント検査を使用して削除された個人情報があったブックに基づいてプロジェクトを作成しようとしたときに、発生する可能性があります。 このエラーを回避するには、プロジェクトを作成する前に次の手順を実行します。

1. Excel でブックを開きます。

2. Excel でセキュリティ センターを開きます。

3. [ **プライバシーオプション** ] タブで、[ **保存時にファイルのプロパティから個人情報を削除** する] チェックボックスをオフにします。

4. ブックを保存し、Excel を終了します。

### <a name="cannot-open-a-project-after-migration"></a>移行後にプロジェクトを開くことができません
 Office のソリューションを Microsoft Office 2010 に移行後は、2007 Microsoft Office システムのみがインストールされている開発用コンピューターでは、プロジェクトを開くことができません。 次のエラー メッセージが表示される可能性があります。

 "ソリューション内の 1 つ以上のプロジェクトが正しく読み込まれていません。 詳細については、出力ウィンドウを確認してください。"

 "このプロジェクト タイプに関連付けられてるアプリケーションがこのコンピューターにインストールされていないため、プロジェクトを作成できません。 このプロジェクト タイプに関連付けられている Microsoft Office アプリケーションをインストールする必要があります。"

 この問題を解決するには、 *.vbproj* ファイルまたは *.csproj* ファイルを編集します。 Word プロジェクトの場合は、HostPackage="{763FDC83-64E5-4651-AC9B-28C4FEB985A1}" を、HostPackage="{6CE98B71-D55A-4305-87A8-0D6E368D9600}" に置き換えます。 Excel プロジェクトの場合は、HostPackage="{B284B16A-C42C-4438-BDCD-B72F4AC43CFB}" を、HostPackage="{825100CF-0BA7-47EA-A084-DCF3308DAF74}" に置き換えます。 Outlook プロジェクトの場合は、HostPackage="{D2B20FF5-A6E5-47E1-90E8-463C6860CB05}" を HostPackage="{20A848B8-E01F-4801-962E-25DB0FF57389}" に置き換えます。

 または、Microsoft Office 2010 が既にインストールされている開発用コンピューターでのみ、移行後のプロジェクトを開くようにします。

### <a name="errors-in-upgraded-office-2003-document-level-projects-that-contain-windows-forms-controls"></a>Windows フォームコントロールを含む、アップグレードされた Office 2003 ドキュメントレベルのプロジェクトでのエラー
 Microsoft Office 2003 ドキュメントレベルのプロジェクトをアップグレードし、ドキュメントに Windows フォームコントロールが含まれている場合、アップグレードされたプロジェクトにコンパイルエラーまたは実行時エラーが発生する可能性があります。 この問題を回避するには、プロジェクトをアップグレードする前に、Visual Studio 2005 Tools for Office Second Edition Runtime を開発用コンピューターにインストールします。 このバージョンのランタイムは、Microsoft ダウンロード センターの「 [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 SE) (x86)](https://www.microsoft.com/download/details.aspx?id=2392)」から再頒布可能パッケージとしてダウンロードできます。

 Visual Studio 2005 Tools for Office Second Edition Runtime は、他の Office ソリューションで使用されていない場合、プロジェクトのアップグレードが完了した後に開発用コンピューターからアンインストールできます。

## <a name="use-the-designers"></a><a name="designers"></a> デザイナーを使用する
 ドキュメント レベルのプロジェクトでドキュメント、ブック、またはワークシート デザイナーを使用する場合に、次のエラーが発生する可能性があります。

### <a name="designer-failed-to-load-correctly"></a>デザイナーを正しく読み込めませんでした
 Visual Studio は次の場合、デザイナーを開くことができません。

- Excel または Word が既に開いており、モーダル ダイアログ ボックスを表示している。 デザイナーを開くには、Excel または Word でモーダル ダイアログ ボックスが開いていないかを確認し、開いているモーダル ダイアログ ボックスがあればそれを閉じます。 開いているモーダル ダイアログ ボックスがない場合は、Excel または Word が応答する前に、何か別のアクションが必要な可能性があります。

- プロジェクトは現在デバッグ中である。 デザイナーを開くには、デバッグを停止または終了します。

- 開発用コンピューターにインストールされている Excel の VSTO アドインにより、Excel の開始時にダイアログ ボックスが表示される。 ドキュメント レベルの Excel プロジェクトを作成するには、まず、VSTO アドインを無効にする必要があります。

### <a name="controls-appear-as-black-rectangles-on-the-document-or-worksheet"></a>コントロールは、ドキュメントまたはワークシートの黒い四角形として表示されます。
 ドキュメントやワークシートでコントロールをグループ化すると、以降は Visual Studio がそのコントロールを認識しなくなります。 グループ化されたコントロールには [ **プロパティ** ] ウィンドウでアクセスできず、ドキュメントまたはワークシート上に黒い四角形として表示されます。 コントロールの機能を復元するには、グループ化を解除する必要があります。

### <a name="controls-on-a-word-template-are-not-visible-in-visual-studio"></a>Word テンプレートのコントロールが Visual Studio で表示されない
 Visual Studio デザイナーで Word テンプレートを開くと、テンプレート上のテキストの範囲内にないコントロールが表示されない場合があります。 これは、Visual Studio が **通常** の表示で Word テンプレートを開くためです。 コントロールを表示するには、[ **表示** ] メニューの [ **Microsoft Office Word ビュー** ] をポイントし、[ **印刷レイアウト**] をクリックします。

### <a name="insert-clip-art-command-does-nothing-in-the-visual-studio-designer"></a>クリップアートの挿入コマンドが Visual Studio デザイナーで何も実行しない
 Excel または Word が Visual Studio デザイナーで開かれている場合、リボンの [**図**] タブの [**クリップアート**] ボタンをクリックしても、[**クリップアート**] 作業ウィンドウは開きません。 クリップアートを追加するには、Visual Studio の外部にある ( *\bin* フォルダー内のコピーではなく) メインプロジェクトフォルダーにあるブックまたはドキュメントのコピーを開き、クリップアートを追加して、ブックまたはドキュメントを保存する必要があります。

## <a name="write-code"></a><a name="code"></a> コードの記述
 Office プロジェクトでコードを作成するときに、次のエラーが発生する場合があります。

### <a name="some-events-of-office-objects-are-not-accessible-when-using-c"></a>C を使用すると、Office オブジェクトの一部のイベントにアクセスできない\#
 場合によっては、Visual C# プロジェクトで Office プライマリ相互運用機能アセンブリ (PIA) 型のインスタンスの特定のイベントにアクセスしようとすると、次のようなコンパイラ エラーが表示される場合があります。

 "'Microsoft.Office.Interop.Excel._Application.NewWorkbook' と 'Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook' の間にあいまいさがあります"

 このエラーは、オブジェクトの別のプロパティやメソッドと同じ名前を持つイベントにアクセスしようとしていることを意味します。 イベントにアクセスするには、オブジェクトをその *イベントインターフェイス* にキャストする必要があります。

 イベントを持つ Office PIA の型は、すべてのプロパティとメソッドを持つコア インターフェイスと、オブジェクトによって公開されるイベントを含むイベント インターフェイスの、2 つのインターフェイスを実装します。 これらのイベントインターフェイスは、 *objectname* Events *n* _Event (やなど) の名前付け規則を使用し <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> <xref:Microsoft.Office.Interop.Word.ApplicationEvents2_Event> ます。 オブジェクト上で検出できることが予想されるイベントにアクセスできない場合は、オブジェクトをそのイベント インターフェイスにキャストします。

 たとえば、<xref:Microsoft.Office.Interop.Excel.Application> オブジェクトが、<xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> イベントおよび <xref:Microsoft.Office.Interop.Excel._Application.NewWorkbook%2A> プロパティを持つとします。 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> イベントを処理するには、<xref:Microsoft.Office.Interop.Excel.Application> を <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> インターフェイスにキャストします。 Excel のドキュメント レベルのプロジェクトでこれを実行する方法を、次のコード例に示します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingExcelCS/ThisWorkbook.cs" id="Snippet1":::

 Office Pia のイベントインターフェイスの詳細については、「 [office プライマリ相互運用機能アセンブリのクラスとインターフェイスの概要](/previous-versions/office/office-12//ms247299(v=office.12))」を参照してください。

### <a name="cannot-reference-office-pia-classes-in-projects-that-target-the-net_v40_short-or-the-net_v45"></a>またはを対象とするプロジェクトでは、Office PIA クラスを参照できません。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)][!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とするプロジェクトでは、Office PIA で定義されているクラスを参照するコードは、既定ではコンパイルされません。 Pia のクラスは、やなどの名前付け規則 *objectname* クラスを使用し <xref:Microsoft.Office.Interop.Word.DocumentClass> <xref:Microsoft.Office.Interop.Excel.WorkbookClass> ます。 たとえば、Word の VSTO アドイン プロジェクトの次のコードはコンパイルされません。

```vb
Dim document As Word.DocumentClass = Globals.ThisAddIn.Application.ActiveDocument
```

```csharp
Word.DocumentClass document = (Word.DocumentClass) Globals.ThisAddIn.Application.ActiveDocument;
```

 このコードを実行すると、次のようなコンパイル エラーが発生します。

- Visual Basic: アセンブリが非 PIA モードでリンクされている場合、クラス ' DocumentClass ' への参照は許可されません。 "

- Visual C#: "Interop type ' Microsoft.Office.Interop.Word.DocumentClass ' を埋め込むことはできません。 代わりに適用可能なインターフェイスを使用してください。"

  このエラーを解決するには、対応するインターフェイスを代わりに参照するようにコードを変更します。 たとえば、<xref:Microsoft.Office.Interop.Word.DocumentClass> オブジェクトを参照するのではなく、代わりに <xref:Microsoft.Office.Interop.Word.Document> インターフェイスを参照します。

```vb
Dim document As Word.Document = Globals.ThisAddIn.Application.ActiveDocument
```

```csharp
Word.Document document = Globals.ThisAddIn.Application.ActiveDocument;
```

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とするプロジェクトは、既定で自動的に Office PIA のすべての相互運用機能型を埋め込みます。 このコンパイル エラーは、埋め込まれた相互運用機能型の機能は、クラスでなくインターフェイスでのみ機能するために発生します。 Office Pia のインターフェイスとクラスの詳細については、「 [office プライマリ相互運用機能アセンブリのクラスとインターフェイスの概要](/previous-versions/office/office-12/ms247299(v=office.12))」を参照してください。 Office プロジェクトの [相互運用機能型の埋め込み] 機能の詳細については、「 [office ソリューションのデザインと作成](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

### <a name="references-to-office-classes-are-not-recognized"></a>Office クラスへの参照が認識されない
 たとえば、アプリケーションなどの一部のクラス名は、やなど、複数の名前空間にあり <xref:Microsoft.Office.Interop.Word> <xref:System.Windows.Forms> ます。 このため、  / プロジェクトテンプレートの先頭にある Imports **using** ステートメントには、次のような短縮修飾定数が含まれています。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs" id="Snippet2":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb" id="Snippet2":::

 **Imports** / **using** ステートメントを使用するには、Office クラスへの参照を、Word または Excel の修飾子を使用して区別する必要があります。次に例を示します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs" id="Snippet3":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb" id="Snippet3":::

 非修飾の宣言を使用した場合は、次のようにエラーが発生します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs" id="Snippet4":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb" id="Snippet4":::

 Word または Excel の名前空間をインポートし、その中のすべてのクラスにアクセスできる場合でも、名前空間のあいまいさを解消するには、すべての型を Word または Excel で完全に修飾する必要があります。

## <a name="build-projects"></a><a name="building"></a> プロジェクトのビルド
 Office プロジェクトをビルドするときに、次のエラーが発生する場合があります。

### <a name="cannot-build-a-document-level-project-that-is-based-on-a-document-with-restricted-permissions"></a>アクセス許可が制限されたドキュメントに基づくドキュメントレベルのプロジェクトをビルドできない
 Visual Studio は、ドキュメントのアクセス許可が制限されている場合、ドキュメント レベルのプロジェクトをビルドできません。 プロジェクトにアクセス許可が制限されているドキュメントが含まれている場合、プロジェクトはコンパイルされず、[ **エラー一覧** ] ウィンドウに次のメッセージが表示されます。

 "カスタマイズを追加できませんでした。"

 アクセス許可が制限されているドキュメントを含める場合は、ソリューションを開発およびビルドする間は、制限のないドキュメントを使用します。 次に、ソリューションを発行した後に、発行場所でアクセス許可の制限をドキュメントに適用します。

### <a name="compiler-errors-occur-after-a-namedrange-control-is-deleted"></a>NamedRange コントロールが削除された後にコンパイラエラーが発生する
 デザイナーで作業中のワークシートではないワークシートから <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを削除した場合、自動生成されたコードがプロジェクトから削除されず、コンパイラ エラーが発生することがあります。 コードが確実に削除されるようにするには、必ず、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを含むワークシートを選択し作業中のワークシートにしてからコントロールを削除します。 コントロールを削除するときに、自動生成されたコードが削除されない場合は、ワークシートをアクティブ化して、ワークシートが変更済みとしてマークされるように変更を加えれば、デザイナーによりコードが削除されます。 プロジェクトをリビルドするときに、コードが削除されます。

## <a name="debug-projects"></a><a name="debugging"></a> プロジェクトのデバッグ
 Office プロジェクトをデバッグするときに、次のエラーが発生する場合があります。

### <a name="prompt-to-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>開発用コンピューターにソリューションを発行してインストールすると、[アンインストールを求めるメッセージが表示される]
 Office ソリューションをデバッグするときに、次のエラー メッセージが表示されることがあります。

 "現在他のバージョンがインストールされており、この場所からアップグレードすることはできないため、このカスタマイズをインストールすることはできません。"

 このエラーは、開発用コンピューターで以前に Office ソリューションを発行し、インストールしたことを示しています。 メッセージが表示されないようにには、ソリューションをデバッグする前に、コンピューターにインストールされているプログラムの一覧からソリューションをアンインストールします。 または、開発コンピューターに別のユーザー アカウントを作成し、発行済みソリューションのインストールをテストすることもできます。

### <a name="document-level-projects-created-at-unc-network-locations-do-not-run-from-visual-studio"></a>UNC ネットワークの場所で作成されたドキュメントレベルのプロジェクトが Visual Studio から実行されない
 UNC ネットワークの場所で Excel または  Word のドキュメント レベルのプロジェクトを作成する場合は、Excel または Word の [信頼できる場所] リストに、そのドキュメントの場所を追加する必要があります。 そうしないと、Visual Studio でプロジェクトの実行またはデバッグを試行するときに、カスタマイズが読み込まれません。 信頼できる場所の詳細については、「 [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

### <a name="threads-are-not-stopped-correctly-after-debugging"></a>デバッグ後にスレッドが正しく停止されない
 Visual Studio の Office プロジェクトは、デバッガーがプログラムを正しく終了できるように、スレッドの名前付け規則に従うようになっています。 ソリューション内にスレッドを作成する場合、デバッグの停止時にこれらのスレッドが確実に正常に処理されるよう、各スレッドに VSTA _  というプレフィックスを付ける必要があります。 たとえば、 `Name` ネットワークイベントの **VSTA_NetworkListener** を待機するスレッドのプロパティを設定できます。

### <a name="cannot-run-or-debug-any-office-solution-on-the-development-computer"></a>開発用コンピューターで Office ソリューションを実行またはデバッグできない
 開発用コンピューターで Office プロジェクトを実行または開発できない場合に、次のエラー メッセージが表示されることがあります。

 "アプリケーション ドメインが作成されなかったため、カスタマイズは読み込まれませんでした。"

 Visual Studio は、Office ソリューションを読み込む前に、.NET Framework アセンブリ ローダーである Fusion を使用してアセンブリをキャッシュします。 Visual Studio が Fusion キャッシュへ書き込めることを確認し、もう一度やり直してください。 詳細については、「 [シャドウコピーアセンブリ](/dotnet/framework/app-domains/shadow-copy-assemblies)」を参照してください。

### <a name="error-when-stopping-the-debugger-in-a-document-level-project-after-using-edit-and-continue"></a>エディットコンティニュを使用した後、ドキュメントレベルのプロジェクトでデバッガーを停止するとエラーが発生する
 プロジェクトが中断モードのときに、Excel または Word のドキュメントレベルのプロジェクトのコードに変更を加えるために **エディット****コンティニュ** を使用すると、後でデバッガーを停止したときに、次のエラーメッセージが表示されるダイアログボックスが表示される場合があります。

 "このプロセスを現在の状態で終了すると、データを消失したりシステムが不安定になったりするなど、予期しない結果になる場合があります。" 

 ダイアログボックスで [ **はい** ] または [ **いいえ** ] をクリックすると、Visual Studio は Excel または Word のプロセスを終了し、デバッガーを停止します。 このダイアログ ボックスを表示せずにプロジェクトのデバッグを停止するには、Visual Studio のデバッガを停止するのではなく、直接、Excel または Word を終了します。

## <a name="see-also"></a>関連項目
- [Office ソリューションのトラブルシューティング](../vsto/troubleshooting-office-solutions.md)
- [Office ソリューションのセキュリティに関するトラブルシューティング](../vsto/troubleshooting-office-solution-security.md)
- [Office ソリューションの配置のトラブルシューティング](../vsto/troubleshooting-office-solution-deployment.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
