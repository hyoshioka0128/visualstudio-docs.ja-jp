---
title: デバッガーでのデータのカスタム ビューの作成 |Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], inspecting programs
- debugger, viewing data
ms.assetid: 13e1105f-f987-402e-9108-ec6ac12be042
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 59e6c1879d5463682ee41d60e3928fce85c74a8d
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305144"
---
# <a name="create-custom-views-of-data-in-the-visual-studio-debugger"></a>Visual Studio デバッガーでのデータのカスタム ビューを作成します。
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]デバッガーには、検査およびプログラムの状態を変更するための多くのツールが用意されています。 ほとんどのツールは、中断モードだけで機能します。

## <a name="create-custom-views-of-data-in-variable-windows-and-datatips"></a>変数ウィンドウとデータヒントでのデータのカスタム ビューを作成します。
 多くは、[デバッガー ウィンドウ](../debugger/debugger-windows.md)など、 **[自動変数]** と**ウォッチ**ウィンドウ、変数を検査することができます。 ネイティブ型、管理対象のオブジェクトをカスタマイズして、デバッガー変数ウィンドウとで独自の型が表示されます[データヒント](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)します。 詳細については、次を参照してください。[ネイティブ オブジェクトのカスタム ビューを作成](../debugger/create-custom-views-of-native-objects.md)と[マネージ オブジェクトのカスタム ビューを作成する](../debugger/create-custom-views-of-dot-managed-objects.md)します。
  
## <a name="create-custom-visualizers"></a>カスタム ビジュアライザーを作成する  
 ビジュアライザーを使用すると、わかりやすい方法でオブジェクトや変数の内容を表示できます。 Visual Studio デバッガー ビジュアライザーは虫眼鏡を使用して開くことができる別の windows を指します![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン")アイコン。 たとえば、HTML ビジュアライザーは、HTML 文字列は解釈され、ブラウザーで表示する方法を示します。 データヒントからビジュアライザーにアクセスできる、**ウォッチ**ウィンドウで、 **[自動変数]** ウィンドウで、および**ローカル**ウィンドウ。 **クイック ウォッチ**  ダイアログ ボックスには、ビジュアライザーも用意されています。 詳細については、「[Create Custom Visualizers](../debugger/create-custom-visualizers-of-data.md)」 (カスタム ビジュアライザーを作成する) を参照してください。
  
## <a name="see-also"></a>関連項目  
 [デバッガーの基本事項](../debugger/getting-started-with-the-debugger.md)   
 [コマンド ウィンドウ](../ide/reference/command-window.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)