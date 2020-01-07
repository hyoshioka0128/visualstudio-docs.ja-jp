---
title: '[オプション]、[テキスト エディター]、[XAML]、[書式設定] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.XAML.Miscellaneous
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.Spacing
helpviewer_keywords:
- element spacing, XAML view settings
- attribute spacing, XAML view settings
- XAML view settings, auto-formatting events
- auto-formatting events, XAML view settings
- XAML view settings, tag wrapping
- XAML view settings, auto insert
- quotation mark style, XAML view settings
- XAML formatting, WPF Designer
- XAML view settings, Toolbox
- XAML view settings, element spacing
- default view, XAML view settings
- auto insert, XAML view settings
- XAML view settings, default view
- XAML view settings, quotation mark style
- tag wrapping, XAML view settings
- WPF Designer, XAML formatting
- XAML view settings, attribute spacing
ms.assetid: ad3820b1-0d94-4807-a74c-c3467ed973a2
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 319e09d2438b23c217f7820fe4288758a595be56
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662218"
---
# <a name="options-text-editor-xaml-formatting"></a>[オプション]、[テキスト エディター]、[XAML]、[書式設定]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[書式設定]** プロパティ ページを使用して、XAML ドキュメントで要素と属性をどのように書式設定するかを指定します。 **[オプション]** ダイアログ ボックスを開くには、 **[ツール]** メニューをクリックし、 **[オプション]** をクリックします。 **[書式設定]** プロパティ ページにアクセスするには、 **[テキスト エディター]** 、 **[XAML]** 、 **[書式設定]** ノードを展開します。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="auto-formatting-events"></a>オートフォーマット イベント
次のイベントのいずれかが検出されると、自動フォーマットが発生する場合があります。

- 終了タグまたは簡易タグの完成

- 開始タグの完成

- クリップボードからの貼り付け

- キーボード コマンドの書式設定

  自動フォーマットが発生するイベントを指定することができます。

|||
|-|-|
|**終了タグまたは簡易タグの完成時**|終了タグまたは簡易タグの入力が完了すると、自動フォーマットが発生します。 簡易タグには、`<Button />` などの属性はありません。|
|**開始タグの完成時**|開始タグの入力が完了すると、自動フォーマットが発生します。|
|**クリップボードからの貼り付け時**|クリップボードから XAML ビューに XAML を貼り付けると、自動フォーマットが発生します。|

## <a name="quotation-mark-style"></a>引用符のスタイル
この設定は、属性値を単一引用符または二重引用符で囲むかどうかを示します。 自動フォーマッタと IntelliSense オート コンプリートは、どちらもこの設定を使用します。

このオプションを設定すると、デザイナーを使用して、または XAML ビューで手動で後から追加される属性のみが影響を受けます。

|||
|-|-|
|**二重引用符 (")**|属性値が二重引用符で囲まれます。<br /><br /> `<Button Name="button1">Hello</Button>`|
|**単一引用符 (')**|属性値が単一引用符で囲まれます。<br /><br /> `<Button Name='button1'>Hello</Button>`|

## <a name="tag-wrapping"></a>[タグの折り返し]
タグの折り返しの行の長さを指定できます。 タグの折り返しを有効にすると、デザイナーを使用して後から追加される任意の XAML が適切に折り返されます。

|||
|-|-|
|**指定の長さを超えたタグを折り返す**|**[長さ]** で指定された行の長さで行を折り返すかどうかを指定します。|
|**長さ**|1 行に含めることができる文字数です。 一部の XAML 行は、必要に応じて指定した行の長さを超えることができます。|

## <a name="attribute-spacing"></a>属性間のスペース
XAML ドキュメント内で属性を配置する方法を制御するには、この設定を使用します。

|||
|-|-|
|**属性間の改行とスペースを保持する**|新しい行と属性間のスペースは、自動フォーマットの影響を受けません。<br /><br /> `<Button Height="23" Name="button1"`<br /><br /> `Width="75">Hello</Button>`|
|**属性間に 1 文字のスペースを挿入する**|属性は 1 行を占領し、隣接する属性は 1 個の空白で分離されます。 タグの折り返しの設定が適用されます。<br /><br /> `<Button Height="23" Name="button1" Width="75">Hello</Button>`|
|**各属性を別の行に配置する**|属性ごとに 1 行を占領します。 これは多くの属性が存在する場合に便利です。<br /><br /> `<Button`<br /><br /> `Height="23"`<br /><br /> `Name="button1"`<br /><br /> `Width="75">Hello</Button>`|
|**最初の属性を開始タグと同じ行に配置する**|オンにすると、最初の属性が要素の開始タグと同じ行に表示されます。<br /><br /> `<Button Height="23"`<br /><br /> `Name="button1"`<br /><br /> `Width="75">Hello</Button>`|

## <a name="element-spacing"></a>要素間のスペース
XAML ドキュメント内で要素を配置する方法を制御するには、この設定を使用します。

|                                                               |                                                                                                                                                                                       |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **コンテンツ内の改行を保持する**                             | 要素のコンテンツ内の空白行は削除されません。<br /><br /> `<Grid>`<br /><br /><br /><br /><br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /><br /><br /> `</Grid>\`   |
| **コンテンツ内の複数の空白行を単一行に折りたたむ** | 要素のコンテンツ内の空白行は、1 行に折りたたまれます。<br /><br /> `<Grid>`<br /><br /><br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /><br /><br /> `</Grid>` |
| **コンテンツ内の空の行を削除する**                             | 要素のコンテンツ内のすべての空白行が削除されます。<br /><br /> `<Grid>`<br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /> `</Grid>`                                        |

## <a name="auto-insert"></a>自動挿入
タグと引用符が自動的に生成されるタイミングを制御するには、この設定を使用します。

|||
|-|-|
|**終了タグ**|大なり記号 (>) で開始タグを閉じたときに、要素の終了タグが自動的に生成されるかどうかを指定します。|
|**属性値の引用符**|ステートメント入力候補のドロップダウン リストから属性値を選択したときに、それを囲む引用符が生成されるかどうかを指定します。|
|**MarkupExtension の終わり中かっこ**|左中かっこ ({) を入力したときに、マークアップ拡張の右中かっこ (}) が自動的に生成されるかどうかを指定します。|
|**MarkupExtension のパラメーターを区切るコンマ**|マークアップ拡張に複数のパラメーターを入力したときに、コンマが生成されるかどうかを指定します。|

## <a name="default-view"></a>既定のビュー
この設定を使用して、XAML ドキュメントが読み込まれるときに表示されるデザイン ビューを制御します。

|||
|-|-|
|**常に完全な XAML ビューでドキュメントを開く**|Xaml ドキュメントを XAML ビューだけにデザインビューせずに表示するかどうかを指定します。 大きなドキュメントを読み込む場合に便利です。|

## <a name="toolbox"></a>ツールボックス
この設定を使用して、ユーザーコントロールとカスタムコントロールをツールボックスに表示するかどうかを指定します。

|||
|-|-|
|**ツールボックスの項目を自動取得する**|現在のソリューションのユーザー コントロールとカスタム コントロールが、ツールボックスに自動的に表示されるかどうかを指定します。|

## <a name="see-also"></a>参照
[WPF の xaml](https://msdn.microsoft.com/library/5d858575-a83b-42df-ad3f-047ed2d6e3c8) 
[方法: Xaml ビューの設定を変更する](https://msdn.microsoft.com/aee87c79-ca01-4f84-8fb7-a9e47048ee47)[Xaml とコード](https://msdn.microsoft.com/b3ff41a0-a2a3-4f61-b698-ac88ec8f799c)
 のチュートリアル
