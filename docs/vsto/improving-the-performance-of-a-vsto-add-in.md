---
title: VSTO アドインのパフォーマンスを向上させる
description: Office アプリケーション用に作成した VSTO アドインを最適化して、すばやく開始、終了、アイテムのオープン、およびその他のタスクを実行できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 83ba2e9cc2cd55b3e3f6362250ffc1e9489b1626
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97524433"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>VSTO アドインのパフォーマンスを向上させる
  Office アプリケーション用に作成した VSTO アドインを最適化して、そのアドインの開始、終了、また、項目を開くなどのタスクの実行を素早く行えるようにして、ユーザー エクスペリエンスを向上させることができます。 VSTO アドインが Outlook を対象にしている場合は、不十分なパフォーマンスが原因で VSTO アドインが無効にされる可能性を低くすることができます。 次の方針を導入すると、VSTO アドインのパフォーマンスを向上させることができます。

- [必要に応じて VSTO アドインを読み込み](#Load)ます。

- [Windows インストーラーを使用して Office ソリューションを発行](#Publish)します。

- [リボンのリフレクションをバイパス](#Bypass)します。

- [負荷の高い操作を別の実行スレッドで実行](#Perform)します。

  Outlook VSTO アドインを最適化する方法の詳細については、「 [Vsto アドインを有効にするためのパフォーマンス条件](/previous-versions/office/jj228679(v=office.15)#performance-criteria-for-keeping-add-ins-enabled)」を参照してください。

## <a name="load-vsto-add-ins-on-demand"></a><a name="Load"></a> 必要に応じて VSTO アドインを読み込む
 次の状況でのみ読み込まれるように VSTO アドインを構成できます。

- VSTO アドインのインストール後にユーザーがアプリケーションを初めて起動するとき。

- それ以降にアプリケーションを起動した後、ユーザーが初めて VSTO アドインを操作するとき。

  たとえば、ユーザーが **[自分のデータを取得**] というラベルの付いたカスタムボタンを選択したときに、VSTO アドインによってワークシートにデータが入力される場合があります。 アプリケーションでは、 **[自分のデータを取得** ] ボタンがリボンに表示されるように、VSTO アドインを少なくとも1回読み込む必要があります。 ただし、ユーザーが次回アプリケーションを起動したときに、VSTO アドインが再度読み込まれることはありません。 VSTO アドインが読み込まれるのは、ユーザーが **[自分のデータを取得]** ボタンをクリックしたときのみです。

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>必要に応じて VSTO アドインを読み込むように ClickOnce ソリューションを構成するには

1. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

2. メニュー バーで **[表示]**  >  **[プロパティ ページ]** の順に選びます。

3. **[発行]** タブの **[オプション]** をクリックします。

4. **[発行オプション]** ダイアログ ボックスで、 **[Office の設定]** リスト項目を選択し、 **[必要に応じて読み込む]** オプションを選択してから、 **[OK]** をクリックします。

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>必要に応じて VSTO アドインを読み込むように Windows インストーラー ソリューションを構成するには

1. レジストリで、 `LoadBehavior` **_Root_\Software\Microsoft\Office \\ _ApplicationName_/Addins \\ _アドイン ID_** キーのエントリを **0x10** に設定します。

     詳細については、「 [VSTO アドインのレジストリエントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>ソリューションのデバッグ中に必要に応じて VSTO アドインを読み込むようにソリューションを構成するには

1. `LoadBehavior` **_ルート_\SOFTWARE\MICROSOFT\OFFICE \\ _ApplicationName_\ \\ _アドイン ID_** キーのエントリを **0x10** に設定するスクリプトを作成します。

     このスクリプトの例を次のコードに示します。

    ```cmd/sh
    [HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\MyAddIn]
    "Description"="MyAddIn"
    "FriendlyName"="MyAddIn"
    "LoadBehavior"=dword:00000010
    "Manifest"="c:\\Temp\\MyAddIn\\bin\\Debug\\MyAddIn.vsto|vstolocal"

    ```

2. スクリプトを使用してレジストリを更新するビルド後のイベントを作成します。

     次のコードに、ビルド後のイベントに追加できるコマンド文字列の例を示します。

    ```cmd/sh
    regedit /s "$(SolutionDir)$(SolutionName).reg"

    ```

     C# プロジェクトでビルド後のイベントを作成する方法の詳細については、「 [方法: ビルドイベントを指定する &#40;C&#35;&#41;](../ide/how-to-specify-build-events-csharp.md)」を参照してください。

     Visual Basic プロジェクトでビルド後のイベントを作成する方法の詳細については、「 [方法: ビルドイベントを指定する &#40;Visual Basic&#41;](../ide/how-to-specify-build-events-visual-basic.md)」を参照してください。

## <a name="publish-office-solutions-by-using-windows-installer"></a><a name="Publish"></a> Windows インストーラーを使用した Office ソリューションの発行
 Windows インストーラーを使用してソリューションを発行した場合、Visual Studio 2010 Tools for Office runtime は、VSTO アドインが読み込まれるときに次の手順を省略します。

- マニフェスト スキーマの検証。

- 更新プログラムの自動的な確認。

- 配置マニフェストのデジタル署名の検証。

  > [!NOTE]
  > VSTO アドインをユーザーのコンピューター上の安全な場所に配置する場合、この方法は必要ありません。

  詳細については、「 [Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="bypass-ribbon-reflection"></a><a name="Bypass"></a> リボンリフレクションのバイパス
 を使用してソリューションをビルドする場合は [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] 、ソリューションを配置するときに、ユーザーが Visual Studio 2010 Tools For Office runtime の最新バージョンをインストールしていることを確認してください。 リボンのカスタマイズを見つけるために、以前のバージョンの VSTO ランタイムがソリューションアセンブリに反映されています。 このプロセスを実行すると、VSTO アドインの読み込み速度がさらに低下する可能性があります。

 別の方法として、Visual Studio 2010 Tools for Office runtime のすべてのバージョンがリフレクションを使用してリボンのカスタマイズを識別できないようにすることもできます。 この戦略に従うには、 `CreateRibbonExtensibility` メソッドをオーバーライドし、明示的にリボンオブジェクトを返します。 VSTO アドインにリボンのカスタマイズが含まれていない場合は、メソッド内でを返し `null` ます。

 次の例では、フィールドの値に基づいてリボンオブジェクトを返します。

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs#1)]

## <a name="perform-expensive-operations-in-a-separate-execution-thread"></a><a name="Perform"></a> 負荷の高い操作を別の実行スレッドで実行する
 時間を要するタスク (長時間実行されるタスク、データベース接続、または他の種類のネットワークの呼び出しなど) を単独のスレッドで実行することを検討してください。 詳細については、「 [Office でのスレッドのサポート](../vsto/threading-support-in-office.md)」を参照してください。

> [!NOTE]
> Office オブジェクト モデルを呼び出すすべてのコードは、メイン スレッドで実行する必要があります。

## <a name="see-also"></a>関連項目

- [VSTO アドインのオンデマンド読み込み](/archive/blogs/andreww/demand-loading-vsto-add-ins)
- [Office アドイン内での CLR の遅延読み込み](/archive/blogs/andreww/delay-loading-the-clr-in-office-add-ins)
- [Visual Studio を使用して Office 用 VSTO アドインを作成する](create-vsto-add-ins-for-office-by-using-visual-studio.md)