---
title: 混合モード アプリケーションをデバッグする | Microsoft Docs
description: Visual Studio で、共通言語ランタイムで実行されるマネージド コードとネイティブ コードを組み合わせるアプリである混合モード アプリケーションをデバッグします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], mixed-mode
- mixed-mode debugging, property evaluation
- Call Stack window
- mixed-mode debugging
- Call Stack window, mixed-mode debugging
- debugging managed code, mixed code
- mixed-mode debugging, call stack
ms.assetid: 60e34477-ae4e-48c7-9093-3e37f72e1bc3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6eff1cae9c1895e853712218d5e0ae55e3138c41
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99872613"
---
# <a name="debugging-mixed-mode-applications"></a>方法 : 混合モード アプリケーションをデバッグする
混合モード アプリケーションとは、ネイティブ コード (C++) とマネージド コード (共通言語ランタイムで動作する Visual Basic、Visual C#、C++ など) の組み合わせから成るアプリケーションです。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] での混合モード アプリケーションのデバッグはきわめて透過的です。つまり、単一モードのアプリケーションをデバッグする場合とほとんど同じです。 ただし、特殊な注意事項があります。

## <a name="enable-c-edit-and-continue-in-mixed-mode-debugging"></a>混合モードのデバッグでの C++ のエディット コンティニュの有効化

C++ のエディット コンティニュを有効にするには、[エディット コンティニュを有効または無効にする方法](../debugger/how-to-enable-and-disable-edit-and-continue.md)に関するページを参照してください。

> [!NOTE]
> Visual Studio 2013 で C++ に対してエディット コンティニュを使用するには、従来のデバッグ エンジンに戻る必要があります。 Microsoft アプリケーション ライフサイクル管理ブログにある「[Switching to Managed Compatibility Mode in Visual Studio 2013](https://devblogs.microsoft.com/devops/switching-to-managed-compatibility-mode-in-visual-studio-2013/)」 (Visual Studio 2013 でマネージド互換モードに切り替える) を参照してください。

## <a name="property-evaluation-in-mixed-mode-applications"></a>混合モード アプリケーションでのプロパティ評価
 混合モード アプリケーションでは、デバッガーを使用してプロパティを評価すると、負荷の高い操作になります。 そのため、ステップ実行などのデバッグ操作の処理速度が低下する場合があります。 詳細については、[ステップ実行](/previous-versions/visualstudio/visual-studio-2010/ek13f001(v=vs.100))に関するページを参照してください。 混合モードのデバッグでパフォーマンスが低下するような場合は、デバッガー ウィンドウのプロパティ評価をオフにできます。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

### <a name="to-turn-off-property-evaluation"></a>プロパティ評価をオフにするには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[オプション]** ダイアログ ボックスで、 **[デバッグ]** フォルダーを開き、 **[全般]** カテゴリを選択します。

3. **[プロパティの評価とその他の暗黙的な関数の呼び出しを常に有効にする]** チェック ボックスをオフにします。

   ネイティブな呼び出し履歴とマネージド呼び出し履歴は異なるため、デバッガーでは、混合コードに対して常に完全な呼び出し履歴を表示できるとは限りません。 ネイティブ コードがマネージド コードを呼び出したときに、不一致が生じていることがわかります。 詳細については、「[Mixed Code and Missing Information in the Call Stack Window](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)」 ([呼び出し履歴] ウィンドウの混合コードと不足情報) を参照してください。

## <a name="see-also"></a>関連項目

- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)