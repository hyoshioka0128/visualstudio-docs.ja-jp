---
title: '[ツールボックス アイテムの選択]、[WPF コンポーネント]'
ms.date: 06/21/2017
ms.topic: reference
f1_keywords:
- vs.chooseitems.wpfcomponents
helpviewer_keywords:
- WPF Components tab, Choose Toolbox Items dialog box
- Choose Toolbox Items dialog box, WPF Components tab
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28576fab1ed4b39810b6f4cc32fb2955a7a44039
ms.sourcegitcommit: 9c57730000d5ced37d3887f3928b17076f49d0f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92099350"
---
# <a name="choose-toolbox-items-wpf-components"></a>ツールボックス アイテムの選択、WPF コンポーネント

**[ツールボックス アイテムの選択]** ダイアログ ボックスのこのタブには、ローカル コンピューターで利用可能な Windows Presentation Foundation (WPF) コントロールの一覧が表示されます。 この一覧を表示するには、 **[ツール]** メニューの **[ツールボックス アイテムの選択]** を選んで **[ツールボックス アイテムの選択]** ダイアログ ボックスを表示し、次に **[WPF コンポーネント]** タブを選びます。コンポーネントの一覧を並べ替えるには、列ヘッダーをクリックします。

- コンポーネントの横にあるチェック ボックスをオンにすると、そのコンポーネントのアイコンが **[ツールボックス]** に表示されます。

    > [!TIP]
    > 編集用に開かれているプロジェクト ドキュメントに WPF コントロールを追加するには、その**ツールボックス** アイコンをデザイン ビュー サーフェイスにドラッグします。 コンポーネントの既定のマークアップとコードがプロジェクトに挿入されて、変更できるようになります。 詳細については、「[ツールボックス](../../ide/reference/toolbox.md)」をご覧ください。

- コンポーネントの横にあるチェック ボックスをオフにすると、対応するアイコンが **[ツールボックス]** に表示されなくなります。

    > [!NOTE]
    > コンピューターにインストールされている .NET コンポーネントは、アイコンが **[ツールボックス]** に表示されているかどうかに関係なく使用できます。

**[WPF コンポーネント]** タブの列には次の情報が含まれます。

**Name**

コンピューターのレジストリにエントリが存在する WPF コントロールの名前が一覧表示されます。

**名前空間**

コンポーネントの構造を定義している [.NET API](/dotnet/api/?view=netframework-4.7&preserve-view=true) 名前空間の階層構造が表示されます。 コンピューターにインストールされている各 .NET 名前空間内で使用可能なコンポーネントを一覧表示するには、この列で並べ替えます。

**アセンブリ名**

各コンポーネントの名前空間を含む .NET アセンブリの名前が表示されます。 コンピューターにインストールされている各 .NET アセンブリに含まれる名前空間を一覧表示するには、この列で並べ替えます。

**ディレクトリ**

.NET アセンブリの場所が表示されます。 アセンブリはすべて、既定では、グローバル アセンブリ キャッシュにあります。 グローバル アセンブリ キャッシュについて詳しくは、「[アセンブリとグローバル アセンブリ キャッシュの使用](/dotnet/framework/app-domains/working-with-assemblies-and-the-gac)」をご覧ください。

## <a name="uielement-list"></a>UIElement の一覧

### <a name="filter"></a>フィルター

テキスト ボックスに入力した文字列に基づいて、WPF コントロールの一覧をフィルター処理します。 4 つの列のいずれかで一致したものがすべて表示されます。

**クリア**

フィルター文字列をクリアします。

**参照**

**[開く]** ダイアログ ボックスが開き、WPF コントロールを含むアセンブリに移動することができます。 グローバル アセンブリ キャッシュに含まれないアセンブリを読み込むには、これを使います。

**Language**

選んだ WPF コントロールを含むアセンブリのローカライズされた言語を表示します。

## <a name="limitations"></a>制限事項

ツールボックスにカスタム コントロールや <xref:System.Windows.Controls.UserControl> を追加するとき、次の制限があります。

- 現在のプロジェクトの外部で定義されたカスタム コントロールに対してのみ機能します。

- ソリューションの構成をデバッグからリリース、またはリリースからデバッグに変更したときに、正しく更新されません。 これは、参照がプロジェクト参照ではなく、ディスク上のアセンブリに対するものであるためです。 コントロールが現在のソリューションの一部である場合、デバッグからリリースに変更しても、プロジェクトは引き続きコントロールのデバッグ バージョンを参照します。

さらに、デザイン時のメタデータがカスタム コントロールに適用されていて、[Microsoft.Windows.Design.ToolboxBrowsableAttribute](/previous-versions/visualstudio/visual-studio-2010/bb547991(v=vs.100)) が `false` に設定されていることがこのメタデータで指定されている場合、コントロールはツールボックスに表示されません。

コントロールの名前空間とアセンブリをマッピングすることにより、XAML ビューでコントロールを直接参照できます。

## <a name="see-also"></a>関連項目

- [ツールボックス](../../ide/reference/toolbox.md)
- [WPF の使用を開始する](../../designers/getting-started-with-wpf.md)
