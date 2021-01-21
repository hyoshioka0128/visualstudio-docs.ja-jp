---
title: 挿入されたコードをデバッグする | Microsoft Docs
description: Visual Studio で提供される挿入されたコードを表示するための 2 つの方法について学習します。1) [逆アセンブリ] ウィンドウ内、2) 挿入された、および元のコードの両方を含むソース ファイル内。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.injected
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- assembly language, viewing
- debugging [C++], viewing assembly code
- debugging [C++], injected code
- debugging [C++], enabling source annotation
- injected code
- Show Source Code command [debugger]
- debugging [C++], using attributes
- disassembly code, debugging
ms.assetid: a1b4104d-d49e-451f-a91e-e39ceaf35875
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5bce49eebf430ccaca9919c74966fb9efd00b09b
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903949"
---
# <a name="how-to-debug-injected-code"></a>方法: 挿入されたコードをデバッグする

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

属性を使用すると、C++ でのプログラミングが簡単になります。 詳細については、[概念](/cpp/windows/attributed-programming-concepts)に関するページを参照してください。 一部の属性は、コンパイラによって直接解釈されます。 プログラム ソースにコードを挿入するタイプの属性もあります。この場合、コンパイラは、コードが挿入されてからプログラム ソースをコンパイルします。 このようにコードが挿入されることにより、実際に記述するコードの量が減り、プログラミングがいっそう簡単になります。 しかし、挿入されたコードの実行中に、バグが発生してアプリケーションが正しく動作しなくなる場合があります。 このような場合は、挿入されたコードを確認する必要があります。 Visual Studio では、次の 2 つの方法で、挿入されたコードを参照できます。

- 挿入されたコードを **[逆アセンブリ]** ウィンドウに表示できます。

- [/Fx](/cpp/build/reference/fx-merge-injected-code) を使用して、元のコードと挿入されたコードをマージしたソース ファイルを作成できます。

**[逆アセンブリ]** ウィンドウには、ソース コードと、属性によって挿入されたコードに対応するアセンブリ言語命令が表示されます。 また、 **[逆アセンブリ]** ウィンドウには、ソース コードの注釈を表示することもできます。

## <a name="to-turn-on-source-annotation"></a>ソースの注釈を表示するには

- **[逆アセンブリ]** ウィンドウを右クリックし、ショートカット メニューの **[ソース コードの表示]** を選びます。

     ソース ウィンドウ内の属性の位置がわかっている場合は、ショートカット メニューを使用して、その属性が挿入したコードを **[逆アセンブリ]** ウィンドウに表示できます。

## <a name="to-view-injected-code"></a>挿入されたコードを表示するには

1. デバッガーは中断モードである必要があります。

2. ソース コード ウィンドウで、挿入されたコードを表示する対象の属性の直前にカーソルを置きます。

3. 右クリックし、ショートカット メニューの **[逆アセンブリを表示]** を選択します。

     属性の位置が現在の実行ポイントに近い場合は、 **[デバッグ]** メニューの **[逆アセンブリ]** ウィンドウを選択できます。

## <a name="to-view-the-disassembly-code-at-the-current-execution-point"></a>現在の実行ポイントにあるコードを表示するには

1. デバッガーは中断モードである必要があります。

2. **[デバッグ]** メニューの **[Windows]** を選び、 **[逆アセンブリ]** をクリックします。

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)