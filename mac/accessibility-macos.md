---
title: macOS のアクセシビリティ オプションの使用
description: ハイ コントラスト、キーボード ナビゲーション、VoiceOver など、macOS のアクセシビリティ オプションと機能の使用
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/23/2019
ms.assetid: 598FC25A-6DA3-44BB-B128-AD979E9F86EA
ms.topic: how-to
ms.openlocfilehash: 6796ab12716d1d2f3ec2570c32b410c8360b8a81
ms.sourcegitcommit: 72a49c10a872ab45ec6c6d7c4ac7521be84526ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94998387"
---
# <a name="accessibility-features-of-macos"></a>macOS のアクセシビリティ機能

macOS はアクセシビリティ対応のオペレーティング システムであり、さまざまな身体機能のユーザーを補助する多くの機能を備えています。 たとえば、ハイコントラスト モード、キーボード ナビゲーション、VoiceOver (macOS のスクリーン リーダー) などの機能があります。

## <a name="enable-accessibility-features"></a>アクセシビリティ機能を有効にする

Visual Studio for Mac では、支援技術のサポートは既定ではオフです。 アクセシビリティのサポートを有効にするには:

1. **[Visual Studio (メニュー)]**  >  **[ユーザー設定]**  >  **[その他]** に移動し、 **[アクセシビリティ]** を選択します。

1. **[アクセシビリティの有効化]** チェック ボックスをオンにします。

   ![[アクセシビリティの有効化] がオンのアクセシビリティ設定のスクリーンショット](media/accessibility-preferences.png)

1. **[Visual Studio を再起動]** を選択して、Apple の支援技術のサポートを有効にします。

または、コマンド ラインを使用してユーザー補助機能を有効にすることもできます。 これを行うには、ターミナルで次のコマンドを入力します。

```bash
defaults write com.microsoft.visual-studio com.monodevelop.AccessibilityEnabled 1
```

コマンド ラインを使用してこの設定を変更した後、Visual Studio を再起動する必要があります。

## <a name="increase-the-contrast-in-macos"></a>macOS のコントラストを上げる

Visual Studio for Mac では、macOS でコントラストを上げる機能がサポートされており、UI 要素のコントラストを上げ、枠線をよりはっきりさせることができます。 これを有効にするには:

1. **[System Preferences]\(システム環境設定\)** を開きます。

1. **[アクセシビリティ]** に移動し、**[ディスプレイ]** を選択します。

1. **[Increase contrast]\(コントラストを上げる\)** チェック ボックスをオンにします。
