---
title: '[オプション]、[テキスト エディター]、[JavaScript]、[書式設定]'
ms.date: 10/29/2018
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Formatting.Spacing
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Formatting.New_Lines
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Formatting.Spacing
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Formatting.New_Lines
ms.assetid: 28a0aef1-9353-4d94-95a5-54b42e15c0dc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 957dbd557a15c4c1df6028672f204a06936767c1
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605994"
---
# <a name="options-dialog-box-text-editor--javascript--formatting"></a>[オプション] ダイアログ ボックス:[テキスト エディター] \> [JavaScript] \> [書式設定]

**[オプション]** ダイアログ ボックスの **[書式設定]** ページで、コード エディターでのコード書式オプションを設定します。 このページにアクセスするには、メニュー バーで **[ツール]**  >  **[オプション]** を選択し、 **[テキスト エディター]**  >  **[JavaScript/TypeScript]**  >  **[書式設定]** を展開します。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="automatic-formatting"></a>自動書式

次のオプションによって、**ソース** ビューで書式設定が実行される条件を指定します。

### <a name="uielement-list"></a>UIElement の一覧

|オプション|説明|
|------------|-----------------|
|**Enter キーを押して行を終了したときに書式設定する**|このオプションをオンにすると、コード エディターで Enter キーを押したときに自動的に行が書式設定されます。|
|**; を入力しステートメントを終了したときに書式設定する**|このオプションをオンにすると、コード エディターでセミコロン キーを押したときに自動的に行が書式設定されます。|
|**Format opened block on { ({ で開始したブロックを書式設定する)**|このオプションをオンにすると、コード エディターで左中かっこ ({) キーを押したときに自動的に行が書式設定されます。|
|**} を入力しブロックを終了したときに書式設定する**|このオプションをオンにすると、コード エディターで右中かっこ (}) キーを押したときに自動的に行が書式設定されます。|
|**貼り付け時に書式設定する**|このオプションをオンにすると、コード エディターにコードを貼り付けるとコードの書式が再設定されます。 エディターでは、現在定義されている書式指定規則が使用されます。 このオプションがオンになっていない場合、エディターでは、貼り付けられたコードの元の書式が使用されます。|

## <a name="new-lines"></a>改行

次のオプションによって、新しい行に関数およびコントロール ブロックの始めかっこを挿入するかどうかを指定します。

### <a name="uielement-list"></a>UIElement の一覧

|オプション|説明|
|------------|-----------------|
|**新しい行に関数の始めかっこを配置する**|このオプションをオンにすると、関数に関連付けられている始めかっこが新しい行に移動します。|
|**新しい行にコントロール ブロックの始めかっこを配置する**|このオプションをオンにすると、コントロール ブロック (`if` コントロール ブロック、`while` コントロール ブロックなど) に関連付けられている始めかっこが新しい行に移動します。|

## <a name="spacing"></a>スペース

次のオプションによって、 **[ソース]** ビューにスペースが挿入される条件を指定します。

### <a name="uielement-list"></a>UIElement の一覧

|オプション|説明|
|------------|-----------------|
|**コンマ区切り記号の後にスペースを追加する**|このオプションをオンにすると、コンマ区切り記号の後にスペースが挿入されます。|
|**'for' ステートメントでセミコロンの後にスペースを挿入する**|このオプションをオンにすると、`for` ループの最初の行に含まれる各セミコロンの後にスペースが挿入されます。|
|**バイナリ演算子の前後にスペースを挿入する**|このオプションをオンにすると、バイナリ演算子 (+, -, &&, &#124;&#124; など) の前後にスペースが挿入されます。|
|**制御フロー ステートメント内のキーワードの後にスペースを挿入する**|このオプションをオンにすると、制御フロー ステートメントの JavaScript キーワードの後にスペースが挿入されます。|
|**匿名関数に対する関数キーワードの後にスペースを挿入する**|このオプションをオンにすると、匿名関数に対する`function`キーワードの後にスペースが挿入されます。|
|**かっこ内が空でない場合に始めかっこの後ろと終わりかっこの前にスペースを挿入する**|このオプションをオンにすると、かっこ内が空でない場合に始めかっこの後ろと終わりかっこの前にスペースが挿入されます。|

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
