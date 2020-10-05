---
title: Visual Studio の DPI 認識を無効にする
description: HDPI モニターでの Windows フォーム デザイナーの制限事項と Visual Studio を DPI 非対応プロセスとして実行する方法について説明します。
ms.date: 09/28/2020
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.topic: conceptual
ms.openlocfilehash: 08eb15914ad381fd81a838f5e09a1350bedff4fd
ms.sourcegitcommit: 31f216b5f7491d5558de5b7ea4ebb0eb1faa3b9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91493310"
---
# <a name="disable-dpi-awareness-in-visual-studio"></a>Visual Studio の DPI 認識を無効にする

Visual Studio はドット/インチ (DPI) 対応アプリケーションであり、ディスプレイが自動的に拡大縮小します。 アプリケーションが DPI 対応ではない場合、オペレーティング システムによってアプリケーションがビットマップとして拡大縮小します。 この動作は DPI 仮想化とも呼ばれています。 それでも、アプリケーションでは、100% のスケーリングまたは 96 dpi で実行されていると認識されます。

この記事では、HDPI モニターでの Windows フォーム デザイナーの制限事項と Visual Studio を DPI 非対応プロセスとして実行する方法について説明します。

## <a name="windows-forms-designer-on-hdpi-monitors"></a>HDPI モニターの Windows フォーム デザイナー

Visual Studio の **Windows フォーム デザイナー**はスケーリングに対応していません。 そのため、高ドット/インチ (HDPI) モニターで **Windows フォーム デザイナー**から一部のフォームを開くと、ディスプレイに問題が生じます。 たとえば、次の画像のように、コントロールが重なって見えることがあります。

![HDPI モニターの Windows フォーム デザイナー](./media/win-forms-designer-hdpi.png)

HDPI モニターで Visual Studio の **Windows フォーム デザイナー**からフォームを開くと、Visual Studio では、デザイナーの上部に黄色い情報バーが表示されます。

![DPI 非対応モードで再起動するための Visual Studio の情報バー](./media/scaling-gold-bar.png)

「**Scaling on your main display is set to 200% (192 dpi).This might cause rendering problems in the designer window.** 」 (メイン ディスプレイのスケーリングが 200% (192 dpi) に設定されています。デザイナー ウィンドウでレンダリング問題が発生する可能性があります。) というメッセージを確認できます。

> [!NOTE]
> この情報バーは Visual Studio 2017 バージョン 15.8 で導入されました。

デザイナーで作業しておらず、フォームのレイアウトを調整する必要がない場合、情報バーを無視し、コード エディターまたはその他の種類のデザイナーで作業を続行できます。 (情報バーを引き続き表示させないように、[通知を無効にする](#disable-notifications)こともできます。)**Windows フォーム デザイナー**のみが影響を受けます。 **Windows フォーム デザイナー**で作業する必要がある場合、[問題解決](#to-resolve-the-display-problem)には次のセクションが役立ちます。

## <a name="to-resolve-the-display-problem"></a>ディスプレイ問題を解決するには

ディスプレイ問題を解決するには、3 つの選択肢があります:

- [Visual Studio を DPI 非対応プロセスとして再起動する](#restart-visual-studio-as-a-dpi-unaware-process)
- [レジストリ エントリを追加する](#add-a-registry-entry)
- [ディスプレイのスケーリングを 100% に設定する](#set-your-display-scaling-setting-to-100)

> [!TIP]
> コマンド ラインから設定を管理する場合、[`devenv.exe`](../ide/reference/devenv-command-line-switches.md) を 100% のスケール モードで実行するにはコマンド ライン パラメーターとして `/noscale` を渡します。

### <a name="restart-visual-studio-as-a-dpi-unaware-process"></a>Visual Studio を DPI 非対応プロセスとして再起動する

黄色い情報バーでオプションを選択することで、Visual Studio を DPI 非対応プロセスとして再起動できます。 これは問題の推奨解決方法です。

Visual Studio が DPI 非対応プロセスとして実行されると、デザイナーのレイアウト問題は解決されますが、フォントがぼやけて表示されることがあります。 Visual Studio が DPI 非対応プロセスとして実行されているとき、「**Visual Studio is running as a DPI-unaware process.WPF and XAML designers might not display correctly.** 」 (Visual Studio が DPI 非対応プロセスとして実行されています。WPF デザイナーや XAML デザイナーが正しく表示されない可能性があります。) という別の黄色い情報メッセージが Visual Studio に表示されます。 また、この情報バーには、**Visual Studio を DPI 対応プロセスとして再起動する**オプションが表示されます。

> [!NOTE]
> - Visual Studio を DPI 非対応のプロセスとして再起動するオプションを選択したとき、ツール ウィンドウのドッキングを解除していた場合、ツール ウィンドウの位置が変更されることがあります。
> - 既定の Visual Basic プロファイルを使用する場合、または **[ツール]**  >  **[オプション]**  >  **[プロジェクトおよびソリューション]** で、 **[新しいプロジェクトを作成時に保存する]** オプションの選択を解除している場合、Visual Studio では、DPI 非対応プロセスとして再起動したとき、プロジェクトを再び開くことができません。 しかし、 **[ファイル]**  >  **[最近使ったプロジェクトとソリューション]** を選択することで、プロジェクトを開くことができます。

**Windows フォーム デザイナー**で作業が完了したら、Visual Studio を DPI 対応プロセスとして再起動することが重要です。 DPI 非対応のプロセスとして実行していると、フォントがぼやけて表示されたり、**XAML デザイナー**など、他のデザイナーで問題が発生したりする可能性があります。 DPI 非対応モードで実行されているときに Visual Studio を閉じて再び開くと、再び DPI 対応になります。 また、情報バーの **[DPI 対応のプロセスとして Visual Studio を再起動します]** オプションを選択できます。

### <a name="add-a-registry-entry"></a>レジストリ エントリを追加する

レジストリを変更することで、Visual Studio を DPI 非対応としてマークできます。 **レジストリ エディター**を起動し、**HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers** サブキーに次のエントリを追加します。

**エントリ**:Visual Studio (2017 または 2019) を使用しているか使用していないかに応じて、次のいずれかの値を使用します。

- C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe
- C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE\devenv.exe

> [!NOTE]
> Professional または Enterprise エディションの Visual Studio を使用している場合、エントリの **[Community]** を **[Professional]** または **[Enterprise]** に変更します。 また、必要に応じてドライブ文字を変更します。

**種類**: REG_SZ

**値**:DPIUNAWARE

> [!NOTE]
> Visual Studio は、レジストリ エントリを削除するまで DPI 非対応モードのままになります。

### <a name="set-your-display-scaling-setting-to-100"></a>ディスプレイのスケーリングを 100% に設定する

Windows 10 でディスプレイ スケーリングを 100% に設定するには、タスク バーの検索ボックスに「**ディスプレイ設定**」と入力し、 **[ディスプレイの設定を変更します]** を選択します。 **[設定]** ウィンドウで、 **[Change the size of text, apps, and other items]\(テキスト、アプリ、その他の項目のサイズを変更します\)** を **[100%]** に設定します。

ユーザー インターフェイスが小さすぎて使いづらくなるため、ディスプレイ スケーリングを 100% に設定することは望ましくない場合もあります。

## <a name="disable-notifications"></a>通知を無効にする

Visual Studio で DPI スケーリングの問題を通知しないことを選択できます。 たとえば、デザイナーで作業していない場合、通知を無効にすることが推奨されます。

通知を無効にするには、 **[ツール]**  >  **[オプション]** を選択し、 **[オプション]** ダイアログを開きます。 次に、 **[Windows フォーム デザイナー]**  >  **[全般]** を選択し、 **[DPI スケーリング通知]** を **[False]** に設定します。

![Visual Studio の DPI スケーリング通知オプション](./media/notifications-option.png)

後で再びスケーリング通知を有効にする場合、このプロパティを **[True]** に設定します。

## <a name="troubleshoot"></a>トラブルシューティング

Visual Studio で DPI 対応移行が予想どおり動作していない場合、レジストリ エディターで **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\devenv.exe** サブキーに `dpiAwareness` 値が含まれているかどうかを確認してください。 値が存在する場合、削除します。

## <a name="see-also"></a>関連項目

- [Windows フォームでの自動スケーリング](/dotnet/framework/winforms/automatic-scaling-in-windows-forms)
