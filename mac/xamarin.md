---
title: Xamarin
description: 'Xamarin を Visual Studio for Mac で使用すると、iOS、Mac、Android、tvOS、および watchOS を対象とするクロス プラットフォーム アプリケーションを作成できます。 '
author: therealjohn
ms.author: johmil
ms.date: 06/18/2019
ms.assetid: 339F6051-5F90-48DC-8237-EBBC8A03A32B
ms.openlocfilehash: 31fb7fa4c2a87820285809d24b98fe8e59a6be01
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "73714481"
---
# <a name="xamarin-mobile-app-development"></a>Xamarin のモバイル アプリ開発

[Xamarin](/xamarin) のファーストクラス サポートにより、Android、macOS、iOS、tvOS、watchOS のために機能が豊富なネイティブ エクスペリエンスを開発できます。 Xamarin.Forms のクロスプラットフォーム アプリケーションにより、ネイティブ機能へのアクセスを制限することなく、Android、iOS、macOS 間で XAML ベースの UI コードを共有できます。

## <a name="xamarinforms"></a>Xamarin.Forms

Visual Studio for Mac バージョン 8.3 以降では、Xamarin.Forms 用の XAML ホット リロードがビルドされています。 この機能を有効にすると、ファイルを保存するたびに、変更が実行中のアプリに直ちに反映されます。

**Visual Studio > [基本設定] > [プロジェクト] > [Xamarin ホット リロード]** で **[Enable Xamarin Hot Reload]\(Xamarin ホット リロードを有効にする\)** チェックボックスをオンすることで、XAML ホット リロードを有効にすることができます。

ホット リロードの詳細については、ドキュメント内の [Xamarin. Forms の XAML ホット リロードについてのガイド](/xamarin/xamarin-forms/xaml/hot-reload)を参照してください。

## <a name="android"></a>Android

Visual Studio for Mac には、ご自分のアプリが対象とする SDK へのアクセスを可能にする独自の Android SDK マネージャーが統合されています。

Android アプリケーションの場合、Visual Studio for Mac には独自のデザイナーがあり、Android の `.axml` ファイルと連携してユーザー インターフェイスを視覚的に構築できます。 Visual Studio for Mac は次の画像のように Android Designer でこれらのファイルを開きます。

![Android UI デザイナー](media/intro-image31.png)

Android Designer の詳細については、[Xamarin.Android Designer の概要](/xamarin/android/user-interface/android-designer/index)に関するガイドを参照してください。

## <a name="ios"></a>iOS

iOS Designer は Visual Studio for Mac と完全に統合されているので、.xib ファイルおよび Storyboard ファイルを視覚的に編集し、iOS、tvOS、および watchOS の UI と遷移を作成できます。 ツールボックスとデザイン サーフェイス間でドラッグ アンド ドロップ機能を使用してユーザー インターフェイス全体を構築できるだけでなく、直感的な方法でイベントを処理できます。 iOS Designer は、デザイン時のレンダリングにさらに役立つ[カスタム コントロール](/xamarin/ios/user-interface/designer/ios-designable-controls-overview)もサポートしています。

![iOS Storyboard デザイナー](media/intro-image30.png)

iOS Designer の使用方法については、[Designer](/xamarin/ios/user-interface/designer/?tabs=macos) に関するガイドを参照してください。

### <a name="mac"></a>Mac

Xamarin にはネイティブの Mac API バインディングが用意されているので、見栄えのよい Mac アプリケーションを作成できます。

Visual Studio for Mac で Mac アプリケーションを作成する方法の詳細については、[Xamarin.Mac](/xamarin/mac/get-started/index) に関するガイドを参照してください。

## <a name="xamarin-enterprise-features"></a>Xamarin Enterprise 機能

> [!Note]
> これらの製品は、Visual Studio Enterprise サブスクリプションでのみ使用できます。

### <a name="profiler"></a>プロファイラー

Xamarin Profiler には、プロファイルに使用できる 3 つのツールがあります。 「[Introduction to the Xamarin Profiler](/xamarin/tools/profiler/index?tabs=macos)」(Xamarin プロファイラー) ガイドでは、これらのインストルメントで測定する内容、アプリケーションの分析方法、各画面に表示されるデータの意味について説明します。

### <a name="inspector"></a>インスペクター

Xamarin Inspector は、対話型 C# コンソールをユーザー ツールで提供しています。 ライブ アプリケーションを調査するときのデバッグまたは診断支援として、教育ツール、ドキュメント作成ツール、または実験ツールとして使用できます。

![Xamarin Inspector](media/intro-inspector.png)

多様なプログラミング プラットフォーム (Android、iOS、Mac、および Windows) を対象にすることができ、お使いの IDE のデバッグ ワークフローに統合できる高機能な C# コンソールを提供するスタンドアロン アプリケーションから構成されます。

詳細については、「[Xamarin Inspector](/xamarin/tools/inspector/)」のガイドを参照してください。
