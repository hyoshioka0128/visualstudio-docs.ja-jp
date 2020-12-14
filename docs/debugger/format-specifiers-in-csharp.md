---
title: デバッガーでの書式指定子 (C#) | Microsoft Docs
description: 書式指定子を使用すると、ウォッチ ウィンドウに表示される値の書式を変更できます。 この記事では、使用方法の詳細について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- expressions [C#], formatting values
- variables [debugger], watch variable symbols
- symbols, watch variable formatting
- QuickWatch dialog box, using format specifiers
- specifiers, watch variable format
- QuickWatch dialog box, format specifiers in C#
- specifiers
- watch variable symbols
- Watch window, format specifiers in C#
- format specifiers, debugger
- debugger, format specifiers recognized by
ms.assetid: 345c8589-5f36-4d34-a58c-e56271687dd6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 31739b9c8fecc862c891173a792986b467730400
ms.sourcegitcommit: 47da50a74fcd3db66d97cb20accac983bc41912f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96862790"
---
# <a name="format-specifiers-in-c-in-the-visual-studio-debugger"></a>Visual Studio デバッガーでの書式指定子 (C#)
書式指定子を使用して、**ウォッチ** ウィンドウに表示される値の書式を変更することができます。 また、**イミディエイト** ウィンドウ、**コマンド** ウィンドウ、[トレースポイント](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)、ソースのウィンドウでも、書式指定子を使用できます。 これらのウィンドウで式の上にカーソルを合わせると、結果が指定した書式で[データヒント](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)に表示されます。

書式指定子を使用するには、可変式に続けてコンマと適切な指定子を入力します。

## <a name="set-format-specifiers"></a>書式指定子の設定
次のコード例を使用します。

```csharp
{
    int my_var1 = 0x0065;
    int my_var2 = 0x0066;
    int my_var3 = 0x0067;
}
```

デバッグ中に `my_var1` 変数を **ウォッチ** ウィンドウに追加します ( **[デバッグ]**  >  **[Windows]**  >  **[ウォッチ]**  >  **[ウォッチ 1]** )。 次に、変数を右クリックし、 **[16 進数で表示]** を選択します。 これで、**ウォッチ** ウィンドウに値 0x0065 が示されます。 この値を 16 進数の整数ではなく 10 進数の整数で表示するには、 **[名前]** 列で変数名の後に 10 進数の書式指定子 **, d** を追加します。 **[値]** 列には **101** が表示されています。

![WatchFormatCSharp](../debugger/media/watchformatcsharp.png "WatchFormatCSharp")

::: moniker range=">= vs-2019" 

**ウォッチ** ウィンドウの値にコンマ (,) を追加することで、使用できる書式指定子の一覧を表示して選択できます。 

![FormatSpecCSharp](../debugger/media/vs-2019/format-specs-csharp.png "FormatSpecCSharp")

::: moniker-end

## <a name="format-specifiers"></a>書式指定子
次の表では、Visual Studio デバッガーの C# 書式指定子について説明します。

|指定子|形式|元の [ウォッチ] の値|表示|
|---------------|------------|--------------------------|--------------|
|ac|式の評価を強制します。これは、プロパティの暗黙の評価および暗黙の関数呼び出しがオフの場合に便利です。|メッセージ "暗黙的な関数の評価はユーザーによってオフにされました"|\<value>|
|d|10 進整数|0x0065|101|
|dynamic|動的ビューを使用して、指定されたオブジェクトを表示します。|動的ビューを含む、オブジェクトのすべてのメンバーを表示します。|動的ビューのみが表示されます。|
|h|16 進整数|61541|0x0000F065|
|nq|引用符なしの文字列。|"My String"|My String|
|nse|形式ではなく動作を指定します。 式は "副作用なし" で評価されます。 式を解釈できず、評価によってのみ解決できる場合 (関数呼び出しなど)、代わりにエラーが表示されます。|N/A|N/A|
|hidden|パブリック メンバーとパブリックでないメンバーをすべて表示します。|パブリック メンバーを表示します。|すべてのメンバーを表示します。|
|raw|未処理の項目ノードで表示されるように項目を表示します。 プロキシ オブジェクトのみで有効です。|Dictionary\<T>|Dictionary\<T> の未加工ビュー|
|results|IEnumerable または IEnumerable\<T> を実装する型の変数と共に使用します。通常はクエリ式の結果です。 クエリ結果を含むメンバーのみを表示します。|すべてのメンバーを表示します|クエリの条件に一致するメンバーを表示します|

## <a name="see-also"></a>関連項目
- [[ウォッチ] および [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)
- [[自動変数] ウィンドウと [ローカル] ウィンドウ](../debugger/autos-and-locals-windows.md)
