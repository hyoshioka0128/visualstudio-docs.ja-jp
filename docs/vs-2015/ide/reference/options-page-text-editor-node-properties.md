---
title: '[テキスト エディター] ノード プロパティ ([オプション] ページ) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Tools Options settings, Text Editor node properties
- automation [Visual Studio], controlling Tools Options
ms.assetid: 19438302-0677-4f4d-9720-5667e6a22ab2
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 62dddacaea1846c8e5d5da404ad7a16fde90f209
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662413"
---
# <a name="options-page-text-editor-node-properties"></a>[テキスト エディター] ノード プロパティ ([オプション] ページ)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このドキュメントでは、 **[オプション]** ダイアログ ボックスの **[テキスト エディター]** カテゴリ (`DTE.Properties("TextEditor", <Property Page>)`) に関連付けられている一部のページ (またはプロパティ コレクション) について説明します。 各サブセクションの見出しは、`Properties` コレクションにアクセスするための呼び出しです。その下の表では、コレクションのプロパティを示します。

 「[オプション設定の制御](https://msdn.microsoft.com/library/a09ed242-7494-4cde-bbd1-7a8ec617965d)」の Visual Basic マクロでは、 **[オプション]** ダイアログ ボックスの各ページにおける現在のオプションとその値の表示方法を示します。

## <a name="general"></a>全般
 `DTE.Properties("TextEditor", "General")`

|プロパティ項目名|[値]|説明|
|------------------------|-----------|-----------------|
|GoToAnchorAfterEscape|Get/Set (Boolean)|`True` の場合は、文字列を選択した状態で Esc キーを押すと、挿入ポイントが選択範囲の開始位置に移動します。 `False` の場合は、挿入ポイントが選択範囲の終了位置に移動します。|
|DragNDropTextEditing|Get/Set (Boolean)|選択したテキストをドキュメント内のある場所から別の場所にドラッグして、コピー操作または切り取りと貼り付け操作を実行できるようにするかどうかを指定します。|
|HorizontalScrollBar|Get/Set (Boolean)|エディターのウィンドウに水平スクロール バーを表示するかどうかを指定します。|
|VerticalScrollBar|Get/Set (Boolean)|エディターのウィンドウに垂直スクロール バーを表示するかどうかを指定します。|
|SelectionMargin|Get/Set (Boolean)|テキスト ペインの左側に特殊な選択操作やブレークポイント アイコンの描画などのための余白を表示するかどうかを指定します。|
|MarginIndicatorBar|Get/Set (Boolean)|テキスト ペインの左端余白を本体と区切る垂直な線を表示するかどうかを指定します。|
|UndoCaretActions|Get/Set (Boolean)|`True` の場合、バッファーを変更する編集操作だけでなく、挿入ポイントの移動や選択コマンドなども元に戻す操作の対象になります。|
|AutoDelimiterHighlighting|Get/Set (Boolean)|右側の区切り記号を入力したときに左側の区切り記号を強調表示するかどうかを指定します。 左側の区切り記号は、このプロパティの値に関係なく常に太字で表示されます。|
|EditorEmulation|Get/Set (Enum)||
|DetectUTF8WithoutSignature|Get/Set (Boolean)|エンコーディング シグネチャがない場合にファイルで UTF-8 エンコーディングを使用するかどうかを検出します。|
|TrackChanges|Get/Set (Boolean)||

## <a name="plain-text"></a>プレーンテキスト
 `DTE.Properties("TextEditor", "PlainText")`

 `PlainText` エディター オプションは、テキスト ファイル編集時のエディターの設定に影響します。 それぞれのプログラミング言語および [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] パッケージには、固有の **[テキスト エディター]** の設定を指定できます。 たとえば、[!INCLUDE[csprcs](../../includes/csprcs-md.md)] エディターの設定を表示または変更するには、`DTE.Properties("TextEditor", "CSharp") or DTE.Properties("TextEditor", "CSharp-Specific")` を使用します。 **[SQL スクリプト]`DTE.Properties("TextEditor", "SQL ")` エディターの設定の場合は、** を使用します。

|プロパティ項目名|[値]|説明|
|------------------------|-----------|-----------------|
|AutoListMembers|Get/Set (Boolean)|変数参照の後にピリオドを入力した場合に使用可能なメンバーの一覧が自動的に表示されるようにするかどうかを指定します。|
|AutoListParams|Get/Set (Boolean)|関数名の後に "(" を入力した場合に引数リストの説明が自動的に表示されるようにするかどうかを指定します。|
|HideAdvancedMembers|Get/Set (Boolean)|ステートメント入力候補にすべてのメンバーを表示するか、よく使用されるメンバーだけを表示するかを指定します。|
|VirtualSpace|Get/Set (Boolean)|空白文字をグラフィックスとして表示するかどうかを指定します。 このプロパティを `true` に設定すると、(この一覧にある) `WordWrap` プロパティ項目が `false` に設定されます。|
|WordWrap|Get/Set (Boolean)|長い行をワード境界で折り返すかどうかを指定します。 このプロパティを `true` に設定すると、(この一覧にある) `VirtualSpace` プロパティ項目が `false` に設定されます。|
|WordWrapGlyphs|Get/Set (Boolean)|行末にグリフを表示します。これは、その行を次の行に折り返すことを示します。|
|EnableLeftClickForURLs|Get/Set (Boolean)|URL に下線を付け、マウスの左ボタンを 1 回クリックするだけで、システムに登録されている Web ブラウザーでその URL にジャンプできるようにするかどうかを指定します。|
|IndentStyle|Get/Set (<xref:EnvDTE.vsIndentStyle>)|インデントのスタイルを指定します ([既定]、[スマート]、または [なし])。|
|TabSize|Get/Set (Long)|1 つのタブに相当するスペースの数を表します。1 ～ 60 以外の整数は設定できません。|
|InsertTabs|Get/Set (Boolean)|`True` の場合、インデントの設定時にタブ文字が使用されません。|
|IndentSize|Get/Set (Long)|1 インデント レベルに相当するスペースの数を表します。 1 ～ 60 以外の整数値は設定できません。|
|ShowLineNumbers|Get/Set (Boolean)|コア エディター ドキュメントの左端余白に行番号を表示するかどうかを指定します。|
|ShowNavigationBar|Get/Set (Boolean)|エディター ウィンドウの最上部にドロップダウン リストとボタンを表示するかどうかを指定します。|
|CutCopyBlankLines|Get/Set (Boolean)|選択時に空白行を切り取るか、コピーします。|

## <a name="see-also"></a>関連項目
 オプション[設定の制御](https://msdn.microsoft.com/library/a09ed242-7494-4cde-bbd1-7a8ec617965d)オプションページの[プロパティ項目の名前を決定する](https://msdn.microsoft.com/library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)オプションページ、[環境] ノードの [[プロパティ](../../ide/reference/options-page-environment-node-properties.md)][ページ、[フォントおよび色] ノードプロパティ](../../ide/reference/options-page-fonts-and-colors-node-properties.md)
