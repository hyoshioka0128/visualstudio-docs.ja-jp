---
title: '[ツールボックス アイテムの選択]、[WPF コンポーネント] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.chooseitems.wpfcomponents
helpviewer_keywords:
- WPF Components tab, Choose Toolbox Items dialog box
- Choose Toolbox Items dialog box, WPF Components tab
ms.assetid: 6ce1d178-88c0-4295-8915-59fdeedabb11
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5c7967635d8e5d64907587fcd1a9b4d84a31d569
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660923"
---
# <a name="choose-toolbox-items-wpf-components"></a>[ツールボックス アイテムの選択]、[WPF コンポーネント]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[ツールボックス アイテムの選択]** ダイアログ ボックスのこのタブには、ローカル コンピューターで利用可能な Windows Presentation Foundation (WPF) コントロールの一覧が表示されます。 この一覧を表示するには、 **[ツール]** メニューの **[ツールボックス アイテムの選択]** を選んで **[ツールボックス アイテムの選択]** ダイアログ ボックスを表示し、次に **[WPF コンポーネント]** タブを選びます。コンポーネントの一覧を並べ替えるには、列ヘッダーをクリックします。

- コンポーネントの横にあるチェック ボックスをオンにすると、そのコンポーネントのアイコンが **[ツールボックス]** に表示されます。

  > [!TIP]
  > 編集用に開かれるプロジェクト ドキュメントに WPF コントロールのインスタンスを追加するには、その**ツールボックス** アイコンをデザイン ビュー サーフェイスにドラッグします。 コンポーネントの既定のマークアップとコードがプロジェクトに挿入されて、変更できるようになります。 詳しくは、「[方法: ツールボックス ウィンドウの管理](https://msdn.microsoft.com/a022c3fe-298c-4a59-a48f-b050da90ebc2)」および「[[ツールボックス] タブの操作方法](https://msdn.microsoft.com/21285050-cadd-455a-b1f5-a2289a89c4db)」をご覧ください。

- コンポーネントの横にあるチェック ボックスをオフにすると、対応するアイコンが **[ツールボックス]** に表示されなくなります。

  > [!NOTE]
  > コンピューターにインストールされている .NET Framework コンポーネントは、アイコンが **[ツールボックス]** に表示されているかどうかに関係なく使用できます。

  **[WPF コンポーネント]** タブの列には次の情報が含まれます。

  名前コンピューターのレジストリにエントリが存在する WPF コントロールの名前を一覧表示します。

  名前空間には、コンポーネントの構造を定義する[NIB: .NET Framework クラスライブラリ](https://msdn.microsoft.com/6c4f3a62-6a0f-41f2-9d52-ee0b13686f29)名前空間の階層が表示されます。 コンピューターにインストールされている各 .NET Framework 名前空間内で使用可能なコンポーネントを一覧表示するには、この列で並べ替えます。

  アセンブリ名各コンポーネントの名前空間を含む .NET Framework アセンブリの名前が表示されます。 コンピューターにインストールされている各 .NET Framework アセンブリに含まれる名前空間を一覧表示するには、この列で並べ替えます。

  ディレクトリ .NET Framework アセンブリの場所を表示します。 アセンブリはすべて、既定では、グローバル アセンブリ キャッシュにあります。 グローバル アセンブリ キャッシュについて詳しくは、「[アセンブリとグローバル アセンブリ キャッシュの使用](https://msdn.microsoft.com/library/8a18e5c2-d41d-49ef-abcb-7c27e2469433)」をご覧ください。

## <a name="uielement-list"></a>UIElement の一覧
 **フィルター**テキストボックスで指定した文字列に基づいて、WPF コントロールの一覧をフィルター処理します。 4 つの列のいずれかで一致したものがすべて表示されます。

 **クリア**フィルター文字列をクリアします。

 **参照** **[開く]** ダイアログボックスを開きます。このダイアログボックスでは、WPF コントロールを含むアセンブリに移動できます。 グローバル アセンブリ キャッシュに含まれないアセンブリを読み込むには、これを使います。

 **言語**選択した WPF コントロールを含むアセンブリのローカライズされた言語を表示します。

## <a name="limitations"></a>制限事項
 ツールボックスにカスタム コントロールや <xref:System.Windows.Controls.UserControl> を追加するとき、次の制限があります。

- 現在のプロジェクトの外部で定義されたカスタム コントロールに対してのみ機能します。

- ソリューションの構成をデバッグからリリース、またはリリースからデバッグに変更したときに、正しく更新されません。 これは、参照がプロジェクト参照ではなく、ディスク上のアセンブリに対するものであるためです。 コントロールが現在のソリューションの一部である場合、デバッグからリリースに変更しても、プロジェクトは引き続きコントロールのデバッグ バージョンを参照します。

  さらに、デザイン時のメタデータがカスタムコントロールに適用され、このメタデータによって[ToolboxBrowsableAttribute](/previous-versions/visualstudio/visual-studio-2010/bb547991(v=vs.100))が `false` に設定されている場合、コントロールはツールボックスに表示されません。

  コントロールの名前空間とアセンブリをマッピングすることにより、XAML ビューでコントロールを直接参照できます。 詳しくは、「[方法 : 名前空間を XAML にインポートする](https://msdn.microsoft.com/6cda7c7a-369c-47dd-9c2d-13a35dcf737c)」をご覧ください。

## <a name="see-also"></a>関連項目

- [[ツールボックス アイテムの選択] ダイアログ ボックス (Visual Studio)](https://msdn.microsoft.com/bd07835f-18a8-433e-bccc-7141f65263bb)
- [ツールボックス](../../ide/reference/toolbox.md)
- [方法 : WPF アプリケーション内でサードパーティの WPF コントロールを使用する](https://msdn.microsoft.com/f4c0b601-3818-4f9f-85e5-77905f3b427f)
- [WPF デザイナー](https://msdn.microsoft.com/c6c65214-8411-4e16-b254-163ed4099c26)