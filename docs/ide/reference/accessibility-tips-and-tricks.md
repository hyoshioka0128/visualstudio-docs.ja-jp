---
title: Visual Studio のアクセシビリティのヒントとテクニック
description: 障碍のある方も含め、あらゆる人にとって Visual Studio 統合開発環境 (IDE) が使いやすくなるヒントとテクニックを紹介します。
ms.date: 08/06/2019
ms.topic: conceptual
helpviewer_keywords:
- accessibility [Visual Studio]
ms.assetid: 6b491d88-f79e-4686-8841-857624bdcfda
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 59206c206f04aaf3506771ee2310daebd0af273a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939748"
---
# <a name="accessibility-tips-and-tricks-for-visual-studio"></a>Visual Studio のアクセシビリティのヒントとテクニック

Visual Studio には、スクリーン リーダーやその他の支援テクノロジと互換性を持つユーザー補助機能が組み込まれています。 キーボード ショートカットを使用して IDE を操作する場合でも、ハイコントラストのテーマを使用して視認性を挙げる場合でも、その方法に関するヒントやテクニックがいくつかこのページで見つかります。

また、注釈を使用してコードに関する有用な情報を表示する方法と、ビルドおよびブレークポイントのイベントに対してサウンド キューを設定する方法についても説明します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac のユーザー補助機能](/visualstudio/mac/accessibility)に関するページを参照してください。

## <a name="save-your-ide-settings"></a>IDE 設定を保存する

ウィンドウのレイアウト、キーボード マップ スキーム、およびその他の設定を保存することにより、IDE エクスペリエンスをカスタマイズできます。 詳細については、「[Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="modify-your-ide-for-high-contrast-viewing"></a>ハイ コントラスト表示のための IDE の変更

一部の人たちには、見えにくい色があります。 コードを書くときにコントラストを強くしたいが一般的な "ハイ コントラスト" テーマは使用したくない場合は、"青 (エクストラ コントラスト)" テーマをお勧めします。

  ![青のテーマと青のエクストラ コントラスト テーマの比較](media/blue-extra-contrast-theme.png "青のテーマと青 (エクストラ コントラスト) テーマの違い示すスクリーンショット")

## <a name="use-annotations-to-reveal-useful-information-about-your-code"></a>注釈を使用してコードに関する有用な情報を表示する

Visual Studio エディターには多くのテキスト "表示要素" が含まれています。これにより、ねじ回し、電球のアイコン、エラーおよび警告の "波線"、ブックマークなど、コード行の特定のポイントで、特性や機能について知ることができます。 "行注釈の表示" コマンド セットを使用すると、これらの表示要素の検出およびこれらの表示要素間の移動が簡単になります。

  ![行注釈の表示コマンド セットを使用する](media/show-line-annotations-command-set.png "[行注釈の表示] メニュー項目のスクリーンショット")

## <a name="access-toolbars-by-using-keyboard-shortcuts"></a>キーボード ショートカットを使用してツールバーにアクセスする

Visual Studio IDE には、多くのツール ウィンドウと同様に機能するツールバーがあります。 次のキーボード ショートカットを使用してアクセスできます。

|機能|説明|キーボード ショートカット|
|-------------|-----------------| - |
|IDE ツール バー|標準ツール バーの最初のボタンを選択します。|**Alt**、**Ctrl**+**Tab**|
|ツール ウィンドウのツール バー|ツール ウィンドウのツール バーにフォーカスを移動します。 <br> <br> **注:** この操作はほとんどのツール ウィンドウで可能です。ただし、フォーカスがツール ウィンドウ内になければなりません。 また、Shift キーを押してから、Alt キーを押す必要があります。 チーム エクスプローラーなど、一部のツール ウィンドウでは、Shift キーをしばらく押したままにしてから、Alt キーを押す必要があります。|**Shift**+**Alt**|
|ツールバー|次のツールバーの最初の項目に移動します (特定のツールバーにフォーカスが置かれている場合)。|**Ctrl**+**Tab**|

### <a name="other-useful-keyboard-shortcuts"></a>その他の便利なキーボード ショートカット

他にもいくつか次のような便利なキーボード ショートカットがあります。

|機能|説明|キーボード ショートカット|
|-------------|-----------------| - |
|IDE|ハイ コントラストのオンとオフを切り替えます。 <br> <br> **注:** 標準的な Windows キーボード ショートカット|**左 Alt**+**左 Shift**+**PrtScn**|
|ダイアログ ボックス|ダイアログ ボックスのチェック ボックス オプションをオンまたはオフにします。 <br> <br> **注:** 標準的な Windows キーボード ショートカット|**Space キー**|
|コンテキスト メニュー|(右クリックして) コンテキスト メニューを開きます。 <br> <br> **注:** 標準的な Windows キーボード ショートカット|**Shift**+**F10**|
|メニュー|アクセラレータ キーを使用して、メニュー項目にすばやくアクセスします。 **Alt** キーを押してからメニュー内の下線付きの文字を選択して、コマンドをアクティブにします。 たとえば、Visual Studio の [プロジェクトを開く] ダイアログ ボックスを表示するには、**ALT**+**F**+**O**+**P** キーを押します。  <br><br> **注:** 標準的な Windows キーボード ショートカット|**ALT** +  **[文字]**|
|検索ボックス|Visual Studio の検索機能を使用します。|**Ctrl**+**Q**|
|[ツールボックス] ウィンドウ|[ツールボックス] のタブ間を移動します。|**Ctrl**+**上矢印**<br /><br /> and<br /><br /> **Ctrl**+**下矢印**|
|[ツールボックス] ウィンドウ|[ツールボックス] からフォームまたはデザイナーにコントロールを追加します。|**Enter**|
|[オプション] ダイアログ ボックス:[環境] > [キーボード]|**[ショートカット キー]** オプションに入力されたキーの組み合わせを削除します。|**バックスペース**|
|[通知] ツール ウィンドウ|2 つのキーボード ショートカットキーを組み合わせ (順番に実行し)、[通知] ツール ウィンドウを開きます。 次に、方向キーを使用して通知を表示し、それを選択します。| **Ctrl**+ **&#92;** 、**Ctrl**+**N**|

> [!NOTE]
> 使用している設定またはエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。

## <a name="access-notifications-by-using-keyboard-shortcuts"></a>キーボード ショートカットを使用して通知にアクセスする

IDE に通知が表示されたら、次のように、キーボード ショートカットを使用して [通知] ウィンドウにアクセスできます。

1. IDE 内の任意の場所から、次の 2 つのキーボード ショートカットを順番に押します。**Ctrl**+ **&#92;** を押し、次に **Ctrl**+**N** を押します。

   **[通知]** ウィンドウが開きます。

   ![Visual Studio IDE の [通知] ツール ウィンドウ](media/toast-notification.png "Visual Studio IDE の [通知] ウィンドウのスクリーンショット")

1. **Tab** キーと矢印キーのいずれかを使用して通知を選択します。

## <a name="use-the-sound-applet-to-set-build-and-breakpoint-cues"></a>サウンド アプレットを使用してビルドおよびブレークポイントのキューを設定する

Windows のサウンド アプレットを使用して、Visual Studio プログラム イベントにサウンドを割り当てることができます。 具体的には、次のプログラム イベントにサウンドを割り当てることができます。

* ブレークポイントのヒット
* ビルドが取り消されました
* ビルドに失敗しました
* ビルドに成功しました

次の手順に従います。

1. Windows 10 を実行しているコンピューター上の **検索** ボックスに「**システムが出す音の変更**」と入力します。

   ![Windows 10 の検索ボックス](media/type-here-to-search.png "Windows 10 の検索ボックスのスクリーンショット")

   (あるいは、Cortana が有効になっている場合は、「コルタナさん」と言ってから、「システムが出す音の変更」と言います。)

1. **[システムが出す音の変更]** をダブルクリックします。

   ![Windows 10 の検索結果](media/change-system-sounds.png "Windows 10 の [システムが出す音の変更] 検索結果のスクリーンショット")

1. **[サウンド]** ダイアログ ボックスで、 **[サウンド]** タブをクリックします。

1. **[プログラム イベント]** で、 **[Microsoft Visual Studio]** にスクロールし、選択したイベントに適用するサウンドを選択します。

   ![Windows 10 の [サウンド] アプレットの [サウンド] タブ](media/sound-applet.png "Windows 10 の [サウンド] アプレットの [サウンド] タブ")

1. **[OK]** をクリックします。

::: moniker range="vs-2017"

> [!TIP]
> アクセシビリティの更新の詳細については、ブログ記事「[Accessibility improvements in Visual Studio 2017 version 15.3 ](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)」 (Visual Studio 2017 バージョン 15.3 でのアクセシビリティの機能強化) をご覧ください。

::: moniker-end

## <a name="see-also"></a>関連項目

* [Visual Studio のユーザー補助機能](../../ide/reference/accessibility-features-of-visual-studio.md)
* [方法: Visual Studio でメニューおよびツール バーをカスタマイズする](../../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)
* [Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)
* [ユーザー補助 (Visual Studio for Mac)](/visualstudio/mac/accessibility)
* [Microsoft ユーザー補助機能](https://www.microsoft.com/Accessibility)
