---
title: デバッガーでデータのカスタム ビューを作成する | Microsoft Docs
ms.date: 01/09/2019
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 63dc11736e92013719fcda2bae0ba9599a8835aa
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72568993"
---
# <a name="create-custom-views-of-data-in-the-visual-studio-debugger-c-visual-basic-c"></a>Visual Studio デバッガーでデータのカスタム ビューを作成する (C#、Visual Basic、C++)

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーには、プログラムの状態を調べて変更するための多数のツールが用意されています。 ほとんどのツールは、中断モードだけで機能します。

## <a name="create-custom-views-of-data-in-variable-windows-and-datatips"></a>変数ウィンドウとデータヒントでのデータのカスタム ビューを作成する

 多くの[デバッガー ウィンドウ](../debugger/debugger-windows.md) ( **[自動変数]** や **[ウォッチ]** など) で、変数を調べることができます。 C++ 型、マネージド オブジェクト、および独自の型を、デバッガー変数ウィンドウと[データヒント](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)にどのように表示するかをカスタマイズできます。 詳細については、「[C++ オブジェクトのカスタム ビューを作成する](../debugger/create-custom-views-of-native-objects.md)」と「[マネージド オブジェクトのカスタム ビューを作成する](../debugger/create-custom-views-of-managed-objects.md)」を参照してください。

## <a name="create-custom-visualizers"></a>カスタム ビジュアライザーを作成する

 ビジュアライザーを使用して、オブジェクトや変数の内容をわかりやすく表示できます。 Visual Studio デバッガーのビジュアライザーでは、虫眼鏡 ![ビジュアライザー アイコン](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン") アイコンを使用して開くことができるウィンドウとは別のウィンドウが参照されます。 たとえば、HTML ビジュアライザーには、HTML 文字列をどのように変換してブラウザーに表示するかが示されます。 ビジュアライザーには、データヒント、 **[ウォッチ]** ウィンドウ、 **[自動変数]** ウィンドウ、および **[ローカル]** ウィンドウからアクセスできます。 **[クイックウォッチ]** ダイアログ ボックスにも、ビジュアライザーが用意されています。 詳細については、「[Create Custom Visualizers](../debugger/create-custom-visualizers-of-data.md)」 (カスタム ビジュアライザーを作成する) を参照してください。

## <a name="see-also"></a>関連項目

- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [コマンド ウィンドウ](../ide/reference/command-window.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
