---
title: VSTO アドインのパフォーマンスを向上させる
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
ms.openlocfilehash: dccff7206aa9ef71596816d34a863695a10aff6b
ms.sourcegitcommit: b32fbbcbc43910b0ed7ce79aa9a22f2ed36ab57e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79416550"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>VSTO アドインのパフォーマンスを向上させる
  Office アプリケーション用に作成した VSTO アドインを最適化して、そのアドインの開始、終了、また、項目を開くなどのタスクの実行を素早く行えるようにして、ユーザー エクスペリエンスを向上させることができます。 VSTO アドインが Outlook を対象にしている場合は、不十分なパフォーマンスが原因で VSTO アドインが無効にされる可能性を低くすることができます。 次の方針を導入すると、VSTO アドインのパフォーマンスを向上させることができます。

- [VSTO アドインをオンデマンドで読み込む](#Load):

- [Windows インストーラを使用して Office ソリューションを発行](#Publish)する :

- [リボンのリフレクションをバイパス](#Bypass)する :

- [別の実行スレッドで負荷の高い操作を実行](#Perform)する 。

  Outlook VSTO アドインを最適化する方法の詳細については、「 [VSTO アドインを有効に保つためのパフォーマンス条件](/previous-versions/office/jj228679(v=office.15)#performance-criteria-for-keeping-add-ins-enabled)」を参照してください。

## <a name="load-vsto-add-ins-on-demand"></a><a name="Load"></a>VSTO アドインをオンデマンドで読み込む
 次の状況でのみ読み込まれるように VSTO アドインを構成できます。

- VSTO アドインのインストール後にユーザーがアプリケーションを初めて起動するとき。

- それ以降にアプリケーションを起動した後、ユーザーが初めて VSTO アドインを操作するとき。

  たとえば、VSTO アドインは、ユーザーが [**自分のデータの取得**] というラベルの付いたカスタム ボタンを選択したときに、ワークシートにデータを入力する場合があります。 [**マイ データの取得**] ボタンがリボンに表示されるように、アプリケーションは VSTO アドインを少なくとも 1 回読み込む必要があります。 ただし、次回アプリケーションを起動したときに、VSTO アドインが再度読み込まれるわけではありません。 VSTO アドインが読み込まれるのは、ユーザーが **[自分のデータを取得]** ボタンをクリックしたときのみです。

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>必要に応じて VSTO アドインを読み込むように ClickOnce ソリューションを構成するには

1. **ソリューション エクスプローラー**で、プロジェクト ノードを選択します。

2. メニュー バーの [**View** > **プロパティ ページ**の表示] をクリックします。

3. **[発行]** タブの **[オプション]** をクリックします。

4. **[発行オプション]** ダイアログ ボックスで、 **[Office の設定]** リスト項目を選択し、 **[必要に応じて読み込む]** オプションを選択してから、 **[OK]** をクリックします。

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>必要に応じて VSTO アドインを読み込むように Windows インストーラー ソリューションを構成するには

1. レジストリで、**_ルート_\ソフトウェア\マイクロソフト\\\Office_アプリケーション名_\アドイン\\ID**キーの`LoadBehavior`エントリを**0x10**に設定します。

     詳細については、「 [VSTO アドインのレジストリ エントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>ソリューションのデバッグ中に必要に応じて VSTO アドインを読み込むようにソリューションを構成するには

1. **_ルート_\ソフトウェア\マイクロソフト\\\Office_アプリケーション名_\アドイン\\ID**キーの`LoadBehavior`エントリを**0x10**に設定するスクリプトを作成します。

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

     C# プロジェクトでビルド後のイベントを作成する方法については、「[方法: C&#35;&#41;&#40;ビルド イベントを指定する](../ide/how-to-specify-build-events-csharp.md)」を参照してください。

     Visual Basic プロジェクトでビルド後のイベントを作成する方法については、「方法[: Visual Basic&#41;&#40;ビルド イベントを指定する](../ide/how-to-specify-build-events-visual-basic.md)」を参照してください。

## <a name="publish-office-solutions-by-using-windows-installer"></a><a name="Publish"></a>Windows インストーラーを使用して Office ソリューションを発行する
 Windows インストーラーを使用してソリューションを発行する場合、VsTO アドインが読み込まれるときに、Office ランタイム用の Visual Studio 2010 ツールは、次の手順をバイパスします。

- マニフェスト スキーマの検証。

- 更新プログラムの自動的な確認。

- 配置マニフェストのデジタル署名の検証。

  > [!NOTE]
  > VSTO アドインをユーザーのコンピューター上の安全な場所に展開する場合、この方法は必要ありません。

  詳細については、「 [Windows インストーラを使用して Office ソリューションを配置する](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="bypass-ribbon-reflection"></a><a name="Bypass"></a>リボンのリフレクションをバイパスする
 を使用[!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]してソリューションをビルドする場合は、ソリューションを配置するときに、ユーザーが Office ランタイム用 Visual Studio 2010 ツールの最新バージョンをインストールしていることを確認します。 VSTO ランタイムの古いバージョンは、ソリューション アセンブリに反映され、リボンのカスタマイズを見つけます。 このプロセスを実行すると、VSTO アドインの読み込み速度がさらに低下する可能性があります。

 別の方法として、Visual Studio 2010 Office ランタイム用ツールの任意のバージョンが、リボンのカスタマイズを識別するためにリフレクションを使用できないようにすることができます。 この方法に従うには、メソッド`CreateRibbonExtensibility`をオーバーライドし、明示的にリボン オブジェクトを返します。 VSTO アドインにリボンのカスタマイズが含まれていない場合は、メソッド内に`null`戻ります。

 次の使用例は、フィールドの値に基づいて Ribbon オブジェクトを返します。

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs#1)]

## <a name="perform-expensive-operations-in-a-separate-execution-thread"></a><a name="Perform"></a>別の実行スレッドで負荷の高い操作を実行する
 時間を要するタスク (長時間実行されるタスク、データベース接続、または他の種類のネットワークの呼び出しなど) を単独のスレッドで実行することを検討してください。 詳細については、「 [Office でのスレッドのサポート](../vsto/threading-support-in-office.md)」を参照してください。

> [!NOTE]
> Office オブジェクト モデルを呼び出すすべてのコードは、メイン スレッドで実行する必要があります。

## <a name="see-also"></a>関連項目

- [VSTO アドインのデマンド ローディング](https://blogs.msdn.microsoft.com/andreww/2008/07/14/demand-loading-vsto-add-ins/)
- [Office アドイン内での CLR の遅延読み込み](https://blogs.msdn.microsoft.com/andreww/2008/04/19/delay-loading-the-clr-in-office-add-ins/)
- [Visual Studio を使用して Office 用 VSTO アドインを作成する](create-vsto-add-ins-for-office-by-using-visual-studio.md)
