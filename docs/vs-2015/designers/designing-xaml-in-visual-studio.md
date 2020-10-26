---
title: XAML のデザイン
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 288e2415-9fcf-408e-bc35-9848315e14fd
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6c48e44e0488d61e3061d680962bf22e42935090
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72664711"
---
# <a name="designing-xaml-in-visual-studio"></a>Visual Studio で XAML をデザインする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio と Blend for Visual Studio の両方に、XAML ベースの Windows デスクトップ、Web、 [Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/jj683071.aspx)、および [Windows ストア](https://msdn.microsoft.com/library/windows/apps/jj129478.aspx) アプリ向けの、魅力的なユーザー インターフェイスとリッチ メディア体験を構築するためのビジュアルなツールが用意されています。 一般的なデザイン ウィンドウ と ツール ウィンドウ、および XAML エディターのセットはどちらにも共通のものですが、Blend for Visual Studio にはアニメーションやビヘイビアーなどのより高度なタスク向けに追加のデザイン ツールが用意されています。

## <a name="choosing-the-right-tool"></a>適切なツールの選択
 デザイン ツールの選択は、スキル セットに大きく依存します。 コード中心の場合は、Visual Studio で XAML コードを記述すれば高度なデザイン タスクを実行できます。 デザイン中心の場合は、Blend for Visual Studio を使用すると、コードを記述せずに高度なタスクを実行できます。

 Visual Studio と Blend for Visual Studio は自在に切り替えることができるだけでなく、両方で同時に同じプロジェクトを開くこともできます。 ある IDE で XAML ファイルに加えた変更は、その他の IDE に切り替える際に、自動再読み込みを使用して適用できます。 再読み込み動作は、いずれかの IDE で **[ツール]** にある **[オプション]** ダイアログ ボックスのオプションを使用して制御できます。

### <a name="shared-capabilities"></a>共有機能
 最も基本的なタスクに関しては、いくらかのわずかな相違はあるものの、Visual Studio と Blend for Visual Studio の IDE で同一のウィンドウおよび機能のセットを使用します。 いくつかの特徴を次に示します。

- **一貫性のあるユーザー インターフェイス:** アプリケーションを使い慣れた Visual Studio ユーザー インターフェイス環境で設計できるため、IDE 間の切り替えが快適になり、生産性も向上します。 Blend for Visual Studio では、コンテンツとユーザー インターフェイスの間のコントラストを上げることにより設計中のコンテンツに注意を集中するのに役立つ Visual Studio ダーク テーマを使用します。 「 [Creating a UI by using XAML Designer](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)」を参照してください。

     ![Blend for Visual Studio の IDE](../designers/media/blendide.png "BlendIDE")

- **XAML IntelliSense:** どちらの IDE も、ステートメント入力候補、コードへのコメント追加や書式設定などの一般的なエディター操作のサポート、およびリソース、バインディング、コードへのナビゲーションなど、IntelliSense に期待する一般的な機能すべてをサポートします。

- **基本的なデバッグ機能:** Blend では、実行中のアプリをデバッグするブレークポイントをコードに設定するなどの、新たなデバッグが可能です。 Visual Studio とデバッグ機能の一貫性を保つため、Blend for Visual Studio には Visual Studio の大半のデバッグ ウィンドウとツールバーが含まれています。 診断やコード分析などの高度なデバッグ機能は、Visual Studio でのみ使用できます。 「 [Debugging in Visual Studio](../debugger/debugging-in-visual-studio.md)」を参照してください。

- **ファイルの再読み込み操作:** XAML ファイルは、Blend for Visual Studio または Visual Studio のどちらでも編集でき、切り替え時に編集したファイルを自動的に再読み込みさせることができます。 ワークフローの中断を最小限に抑えるため、[ファイルの再読み込み] ダイアログでファイルの再読み込みの基本設定を設定できます。

     ![ファイルの再読み込みエクスペリエンス](../designers/media/blendfilereload.png "BlendFileReload")

- **レイアウトの同期と設定:** カスタム レイアウトを使用して、ツール ウィンドウのレイアウト変更を保存および適用できます。 同じ Microsoft アカウントでサインインすると、Visual Studio は Visual Studio と Blend for Visual Studio 双方の変更や基本設定をコンピューター間で同期します。 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)を参照してください。

- **共通のソリューション エクスプ ローラー:** ソリューション エクスプ ローラーによって、プロジェクトやファイルが整理して表示されるだけでなく、プロジェクトやファイルに関連付けられているコマンドに素早くアクセスできます。 ソリューション エクスプ ローラーを使用すると、大規模なエンタープライズ プロジェクトでの作業が容易になります。 「 [ソリューションとプロジェクト」を](../ide/solutions-and-projects-in-visual-studio.md)参照してください。

- **チーム エクスプ ローラー:** チーム エクスプ ローラーを使用すると、プロジェクトを GIT または TFS リポジトリを使用して管理でき、チームのコラボレーションが容易になります。 [チーム エクスプローラーでの作業](https://msdn.microsoft.com/library/fd7a5cf7-7916-4fa0-b5e6-5a83cf377a02)を参照してください。

- **NuGet:** Visual Studio と Blend for Visual Studio の両方で NuGet パッケージを管理できます。 NuGet は、パッケージのインストールと、ソリューションからの削除を簡略化する .NET Framework 用のパッケージ マネージャーです。

## <a name="advanced-capabilities-in-blend-for-visual-studio"></a>Blend for Visual Studio での高度な機能
 生産性を高めるため、次のようなタスクには Blend for Visual Studio の使用をご検討ください。 Blend for Visual Studio が Visual Studio デザイナーまたはコード単独より短い時間でより多くの機能を提供する領域は以下のとおりです。

|目的|Visual Studio|Blend for Visual Studio|説明|
|--------|-------------------|-----------------------------|----------------------|
|**アニメーションを作成する**|アニメーション用のデザイン ツールはないため、プログラムで作成する必要があります。 これを行うには、WPF におけるアニメーションおよびタイミング システムを理解し、広範なコーディングの専門知識を持っている必要があります。|アニメーションを視覚的に作成し、Blend for Visual Studio でプレビューできます。 これは、コーディングでアニメーションを構築するよりもすばやく正確です。 ユーザーとの対話を処理するトリガーを追加できるほか、コードに切り替えてイベント ハンドラーとその他の機能を追加することができます。|[オブジェクトのアニメーション化](../designers/animate-objects-in-xaml-designer.md)|
|**簡単に操作できるよう、図形やテキストをパスに変換する**|サポートされていません。|図形 (四角形、楕円など) をパスに変換することで、図形に対して軽微な変更や劇的な変更を行えます。そうすることで、より良い編集コントロールができます。  形状を変更したり、パスを結合するとともに、複数の図形から複合パスを作成することができます。<br /><br /> さらに、テキスト ブロックをパスに変換して、ベクター イメージとして操作することもできます。|[図形とパスの描画](../designers/draw-shapes-and-paths.md)|
|**UI の設計に対話機能を追加する**|C#、Visual Basic、または C++ コードが必要です。|静的な設計に対話機能を追加するため、コントロールにビヘイビアーをドラッグ アンド ドロップします。 ビヘイビアーは、ドラッグ アンド ドロップ、ズーム、表示状態の変更などの機能をカプセル化する、すぐに使用できるコード スニペットです。 選択できる一連のビヘイビアーは増大しつつありますが、独自に作成することができます。<br /><br /> 次に、Blend for Visual Studio でビヘイビアーのプロパティを変更するか、コードでイベント ハンドラーを追加することにより、各ビヘイビアーをカスタマイズできます。|[コントロールの挿入およびそのビヘイビアーの変更](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md)|
|**Adobe アートワークを使用する**|サポートされていません。|Adobe FXG、PhotoShop、または Illustrator のアートワークをインポートし、Blend for Visual Studio に UI を実装します。|[イメージ、ビデオ、およびオーディオ クリップの挿入](../designers/insert-images-videos-and-audio-clips-in-xaml-designer.md)|
|**コントロール、テンプレート、スタイルを編集する**|コーディングおよび WPF のスタイルとテンプレートの知識が必要です。|イメージをコントロールに変換します。<br /><br /> コントロール、スタイル、テンプレートを数回マウスでクリックするだけで変更するには、テンプレート編集ツールを使用します。<br /><br /> たとえば、Blend for Visual Studio のスタイル リソースを使用して一般的な WPF コントロール (ボタン、リスト ボックス、スクロール バー、メニューなど) を実装し、Blend for Visual Studio で色、スタイル、または基になるテンプレートを直接変更できます。 次に、必要な場合はコードに切り替えてタッチを仕上げます。|[オブジェクト スタイルを変更する](../designers/modify-the-style-of-objects-in-blend.md)|
|**UI をデータに接続する**|SQL Server データベース、WCF や Web サービス、オブジェクト、または SharePoint リストなどのリソースからデータ ソースを作成し、データ ソースを UI コントロールにバインドします。<br /><br /> デザイン時のデータは、対話型のデザイン エクスペリエンスのため手動で作成する必要があります。|プロトタイプの作成とテスト用のサンプル データは簡単に作成できます。 準備ができたら、ライブ データに切り替えます。<br /><br /> Blend for Visual Studio のデータ生成機能は並外れており (その場で迅速かつ簡単に、名前、番号、URL、写真の追加が可能)、多くの時間を節約できます。<br /><br /> ライブ データの場合は、UI コントロールを XML ファイルまたは任意の CLR データ ソースにバインドできます。|[データの表示](../designers/display-data-in-blend.md)|

 高度な XAML デザインの詳細については、次の項目を参照してください。 [Blend for Visual Studio を使用して UI を作成する](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
