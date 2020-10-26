---
title: XAML 概要
ms.date: 06/23/2020
ms.topic: overview
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: e14e23f9820301374bd435484ba784edf50294bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85331951"
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

## <a name="xaml-code-editor"></a>XAML コード エディター

Visual Studio IDE の [XAML コード エディター](xaml-code-editor.md)には、Windows プラットフォーム用と Xamarin.Forms 用の WPF と UWP アプリを作成するために必要なツールがすべて含まれています。 また、Visual Studio の IDE (統合開発環境) には、他のプラットフォーム用のアプリを開発するために使用できる多くの機能がありますが、XAML に固有の機能もいくつか用意されています。

## <a name="xaml-designer"></a>XAML デザイナー

Visual Studio と Blend for Visual Studio には、WPF、UWP、Xamarin. Forms アプリのユーザー インターフェイス (UI) を構築するのに役立つ [XAML デザイナー](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)が用意されています。 [ツールボックス] または [アセット] ウィンドウからコントロールをドラッグし、プロパティ ウィンドウのプロパティを設定できます。 これらを行うとき、Visual Studio と Blend for Visual Studio では、それに対応する XAML コードが作成されます。 XAML コードを直接編集する場合、それを行うこともできます。

## <a name="whats-new"></a>新機能

最新情報については、次のリソースを参照してください。

- **[Visual Studio 2019 バージョン 16.7 Preview 1 の XAML ツールの機能強化](https://devblogs.microsoft.com/visualstudio/improvements-to-xaml-tooling-in-visual-studio-2019-version-16-7-preview-1/)** に関するブログの投稿
- **[Visual Studio 2019 の XAML 開発者ツールの新機能](https://devblogs.microsoft.com/visualstudio/whats-new-in-xaml-developer-tools-in-visual-studio-2019-for-wpf-uwp/)** に関するブログの投稿
- **[Visual Studio での新しい XAML 機能](https://youtu.be/yI9OyA4ZM2E)** の YouTube ビデオ

## <a name="see-also"></a>関連項目

- [WPF アプリの XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP アプリの XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms アプリの XAML](/xamarin/xamarin-forms/xaml/)
