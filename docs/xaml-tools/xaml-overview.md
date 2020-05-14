---
title: XAML 概要
ms.date: 01/10/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 2556387f523769bba93708a9c00d1f7c62429c0f
ms.sourcegitcommit: aa302af53de342e75793bd05b10325939dc69b53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "82921227"
---
# <a name="overview-of-xaml"></a>XAML の概要

Extensible Application Markup Language (XAML) は XML を基盤とする宣言型言語です。 XAML は、ユーザー インターフェイスを構築するために、次の種類のアプリケーションで広く使用されています。

- [Windows Presentation Foundation (WPF) アプリ](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [ユニバーサル Windows プラットフォーム (UWP) アプリ](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms アプリ](/xamarin/xamarin-forms/xaml/)

次の XAML コードでは、単純なボタン コントロールが定義されます。

```xaml
<Button Click="ButtonClick">Show updates</Button>
```

XAML は、[Windows WorkFlow Foundation (WF) アプリ](/dotnet/framework/windows-workflow-foundation/serializing-workflows-and-activities-to-and-from-xaml)のワークフローを定義するためにも使用されます。

## <a name="xaml-designer"></a>XAML デザイナー

Visual Studio と Blend for Visual Studio には、WPF、UWP、Xamarin. Forms アプリのユーザー インターフェイス (UI) を構築するのに役立つ XAML デザイナーが付属しています。 [ツールボックス] または [アセット] ウィンドウからコントロールをドラッグし、プロパティ ウィンドウのプロパティを設定できます。 その場合、Visual Studio と Blend for Visual Studio は、対応する XAML コードを作成します。 XAML コードを直接編集する場合、それを行うこともできます。

このドキュメント セットの記事では、Visual Studio と Blend for Visual Studio の XAML デザイナーについて説明します。

## <a name="whats-new"></a>新機能

最新情報については、 [Visual studio 2019 の xaml 開発者ツール](https://devblogs.microsoft.com/visualstudio/whats-new-in-xaml-developer-tools-in-visual-studio-2019-for-wpf-uwp/)の新機能に関するブログ投稿と、YouTube の[visual Studio ビデオの新しい xaml 機能](https://youtu.be/yI9OyA4ZM2E)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

- [WPF アプリの XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP アプリの XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms アプリの XAML](/xamarin/xamarin-forms/xaml/)
