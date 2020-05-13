---
title: '[オプション]、[テキスト エディター]、[JavaScript]、[IntelliSense] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Intellisense.References
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Intellisense.General
ms.assetid: b4a9816d-cf87-4dc6-a8d4-1591d6a48103
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1b0d9dec8ec9b3eb8860bb8b3a4ed8f7347aa54d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662228"
---
# <a name="options-text-editor-javascript-intellisense"></a>[オプション]、[テキスト エディター]、[JavaScript]、[IntelliSense]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

JavaScript での IntelliSense の動作設定を変更するには、 **[オプション]** ダイアログ ボックスの **[IntelliSense]** ページを使用します。 **[IntelliSense]** ページにアクセスするには、メニュー バーの **[ツール]** , **[オプション]** をクリックし、 **[テキスト エディター]** , **[JavaScript]** , **[IntelliSense].** と展開します。

 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

 **[IntelliSense]** ページには、以下のセクションがあります。

## <a name="validation"></a>検証
 これらの設定を使用して、JavaScript エディターがドキュメントの構文を検証する方法を設定できます。

## <a name="uielement-list"></a>UIElement の一覧
 **構文エラーの表示**このチェックボックスがオフの場合、JavaScript コードエディターでは構文エラーは表示されません。 このオプションは、自分が記述したものではなく、構文エラーを修正する必要がないコードを扱うときに便利です。

 このチェック ボックスをオンにすると、 **[エラーを警告として表示]** チェック ボックスをオンにできるようになります。

 **エラーを警告として表示**このチェックボックスがオンの場合、JavaScript エラーはエラー一覧にエラーではなく警告として表示されます。

 **その他のファイルプロジェクト内のファイルのリモート参照 (例: http://) をダウンロードする**このチェックボックスをオンにすると、プロジェクトのコンテキストの外部で開かれた JavaScript ファイルがある場合、Visual Studio は IntelliSense 情報を提供するために、ファイルで参照されているリモート JavaScript ファイルをダウンロードします。 このオプションを選択している場合、JavaScript ファイルに参照として含まれるファイルがダウンロードされます。

> [!NOTE]
> Web プロジェクトでは、プロジェクトで参照されるリモート ファイルは既定でダウンロードされます。

## <a name="statement-completion"></a>[入力候補]
 これらのオプションを使用して、IntelliSense のステートメントの入力候補の動作を変更できます。

## <a name="uielement-list"></a>UIElement の一覧
 **Tab キーまたは enter キーのみをコミットに使用する**このチェックボックスがオンの場合、JavaScript コードエディターは、Tab キーまたは Enter キーを押した後にのみ、入力候補一覧で選択された項目を含むステートメントを追加します。 このチェック ボックスがオフの場合、ピリオド、コンマ、コロン、始めかっこ、始め中かっこ ({) など、その他の文字でも選択された項目を含むステートメントを追加できます。

## <a name="references"></a>関連項目
 これらのオプションを使用して、JavaScript のさまざまなプロジェクトの種類のスコープ内にある IntelliSense (.js) ファイルの種類を指定できます。 通常、IntelliSense 参照は、グローバル オブジェクトに IntelliSense サポートを提供するために使用されます。 このページを使用して、実行時に読み込む必要があるスクリプトの読み込み順序を設定したり、IntelliSense の拡張ファイルを追加したりすることもできます。

## <a name="uielement-list"></a>UIElement の一覧
 **参照グループ**このオプションは、参照グループの種類を指定します。 3 つの参照グループがサポートされています。

 定義済みの参照グループを使用して、特定の IntelliSense (.js) ファイルがさまざまな JavaScript プロジェクトのスコープ内にあることを指定できます。 4 つの参照グループを使用できます。

- 暗黙 (Windows *バージョン*)、JavaScript を使用する [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] アプリケーション用。 このグループに含まれるファイルは、JavaScript を使用する [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] アプリケーションのコード エディターで開かれる、すべての .js ファイルのスコープ内にあります。

- 暗黙 (Web)、HTML5 プロジェクト用。 このグループに含まれるファイルは、これらのプロジェクト タイプのコード エディターで開かれる、すべての .js ファイルのスコープ内にあります。

- 専用のワーカーの参照グループ、HTML5 Web ワーカー用。 このグループで指定されたファイルは、専用のワーカーの参照グループへの明示的な参照がある .js ファイルのスコープ内にあります。

- ジェネリック、他の JavaScript プロジェクト タイプ用。

  **インクルードファイル**このオプションは、ファイルが言語サービスのコンテキストに読み込まれる順序を指定します。 **[削除]** 、 **[上へ移動]** 、および **[下へ移動]** ボタンを使用して順序を構成できます。 IntelliSense が正しく動作するためには、別のファイルに依存しているファイルはその別のファイルの後に読み込む必要があります。

> [!CAUTION]
> オブジェクトが複数の暗黙的な参照で無条件で定義されている場合、その一覧内の最後の参照を使用してオブジェクトが定義されます。

 **グループへの参照を追加する**このオプションを使用すると、適切なファイルを参照することにより、追加の IntelliSense .js ファイルを追加できます。

## <a name="see-also"></a>関連項目
 [JavaScript IntelliSense](../../ide/javascript-intellisense.md)
