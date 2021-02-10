---
title: 文字列ビジュアライザーでの文字列の表示 | Microsoft Docs
description: Visual Studio デバッガーで文字列ビジュアライザーを使用して、テキスト文字列、XML、HTML、JSON を表示します。 DataSet、DataTable を含む、その他のオブジェクトの種類を表示できます。
ms.custom: SEO-VS-2020
ms.date: 04/08/2019
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- string visualizer
- visualizers, string
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 287b5e4546d720160c5e73d19cfeaee5bc0c59e1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99933064"
---
# <a name="view-strings-in-a-string-visualizer-in-visual-studio"></a>Visual Studio の文字列ビジュアライザーで文字列を表示する

Visual Studio でのデバッグ中に、組み込みの文字列ビジュアライザーを使用して文字列を表示できます。 文字列ビジュアライザーには、データ ヒントまたはデバッガー ウィンドウに対して長すぎる文字列が表示されます。 また、形式に誤りがある文字列を識別するのにも役立ちます。

組み込みの文字列ビジュアライザーには、プレーンテキスト、XML、HTML、JSON オプションが含まれています。 [DataSet、DataTable、DataView](../debugger/dataset-visualizer-dialog-box.md) オブジェクトなど、他のいくつかの種類の組み込みビジュアライザーを、 **[自動変数]** またはその他のデバッガー ウィンドウから開くこともできます。

> [!NOTE]
> ビジュアライザーで XAML または WPF の UI 要素を検査する必要がある場合は、「[デバッグ中に XAML のプロパティを調べる](../xaml-tools/inspect-xaml-properties-while-debugging.md)」または「[方法: WPF ツリー ビジュアライザーを使用する](../debugger/how-to-use-the-wpf-tree-visualizer.md)」を参照してください。

## <a name="open-a-string-visualizer"></a>文字列ビジュアライザーを開く

文字列ビジュアライザーを開くには、デバッグ中に一時停止する必要があります。 プレーンテキスト、XML、HTML、または JSON 文字列値を持つ変数の上にマウス ポインターを移動し、虫眼鏡アイコン ![ビジュアライザー アイコン](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン") を選択します。

![文字列ビジュアライザーを開く](../debugger/media/dbg-tips-string-visualizers.png "文字列ビジュアライザーを開く")

## <a name="view-string-visualizer-data"></a>文字列ビジュアライザーのデータを表示する

文字列ビジュアライザー ウィンドウでは、 **[式]** フィールドに、カーソルを置いている変数または式が表示され、 **[値]** フィールドに文字列値が表示されます。

**[値]** が空白の場合は、選択したビジュアライザーで文字列を認識できないことを意味します。 たとえば、**XML ビジュアライザー** では、XML タグのないテキスト文字列または JSON 文字列に対して、空白の **[値]** が表示されます。

選択したビジュアライザーが認識できない文字列を表示するには、 **[テキスト ビジュアライザー]** を選択します。 **テキスト ビジュアライザー** にはプレーンテキストが表示されます。

### <a name="view-json-string-data"></a>JSON 文字列データを表示する

整形式の JSON 文字列は、次の図に示すように JSON ビジュアライザーに表示されます。 形式に誤りがある JSON には、エラー アイコンが表示されることがあります (または、認識できない場合は空白になります)。 JSON エラーを特定するには、文字列をコピーし、[JSLint](https://www.jslint.com/) などの JSON リンティング ツールに貼り付けます。

![JSON 文字列ビジュアライザー](../debugger/media/dbg-tips-string-visualizer-json.png "JSON 文字列ビジュアライザー")

### <a name="view-xml-string-data"></a>XML 文字列データを表示する

整形式の XML 文字列は、次の図に示すように XML ビジュアライザーに表示されます。 形式に誤りがある XML は、XML タグなしで表示されるか、認識されない場合は空白になります。

![XML 文字列ビジュアライザー](../debugger/media/dbg-string-visualizers-xml.png "XML 文字列ビジュアライザー")

### <a name="view-html-string-data"></a>HTML 文字列データを表示する

次の図に示すように、整形式の HTML 文字列は、ブラウザーに表示されているかのように表示されます。 形式に誤りがある HTML は、プレーンテキストとして表示される場合があります。

![HTML 文字列ビジュアライザー](../debugger/media/dbg-string-visualizers-html.png "HTML 文字列ビジュアライザー")

## <a name="see-also"></a>関連項目

- [カスタム ビジュアライザーを作成する (C#、Visual Basic)](../debugger/create-custom-visualizers-of-data.md)
- [Visual Studio for Mac でのデータの可視化](/visualstudio/mac/data-visualizations)