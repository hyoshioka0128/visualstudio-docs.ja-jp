---
title: DOM イベントリスナーの表示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- DOM events, viewing [Windows Store apps]
- event listeners, viewing [Windows Store apps]
ms.assetid: d5b679e7-87dd-4cec-9176-883db6ff0781
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 64d4892080aaf0cf04e4b208b1a0bdb7a7a4480d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65693581"
---
# <a name="view-dom-event-listeners"></a>DOM イベント リスナーの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows および Windows Phone] (../Image/windows_and_phone_content.png "windows_and_phone_content")

 DOM Explorer の [ **イベント** ] タブには、DOM 要素に関連付けられているイベントが表示されます。 [ **イベント** ] タブの最上位ノードは、アクティブなサブスクライバーを持つイベントを表します。 最上位のノードには、特定のイベントのために登録されたイベント リスナーを表すサブノードが含まれます。 イベント リスナーの表示に加えて、このタブを使用して、JavaScript コード内のイベント リスナーの場所に移動できます。 このトピックの情報は、HTML および JavaScript を使用するストア アプリに適用します。

 [ **イベント** ] タブの一覧は動的です。 アプリの実行中にイベント リスナーを追加すると、新しいイベント リスナーが一覧に表示されます。 イベントリスナーの追加と削除の詳細については、このトピックの「 [イベントリスナーに関する問題の解決に関するヒント](#Tips) 」を参照してください。

> [!NOTE]
> DOM 要素ではないコード要素 (など) のイベントリスナーは `xhr` 、[ **イベント** ] タブに表示されません。

## <a name="view-event-listeners-for-dom-elements"></a>DOM 要素のイベント リスナーの表示
 この例は、Windows Phone ストア アプリを示します。 ここで説明する DOM Explorer の機能は、Windows ストア アプリでもサポートされます。

#### <a name="to-view-event-listeners"></a>イベント リスナーを表示するには

1. Visual Studio で、Windows Phone ピボット アプリケーション プロジェクト テンプレートを使用する JavaScript アプリを作成します。

2. Visual Studio でテンプレートを開いた状態で、デバッガーの [デバッグ] ツールバーのドロップダウンリストから [ **Emulator 8.1 WVGA 4IN 512 mb** )] を選択します。

     ![デバッグのターゲットを選択する](../debugger/media/js-dom-debug-target-emu.png "JS_DOM_Debug_Target_Emu")

3. F5 キーを押して、アプリをデバッグ モードで実行します。

4. 実行中のアプリで、 **セクション 3** のピボットアイテムにアクセスします。

5. Visual Studio に切り替えます (Alt + Tab キーまたは F12 キーを押します)。

6. DOM Explorer で、右上の [`Find`] を選択します。

7. 「 `ListView`」と入力して Enter キーを押します。

8. 必要に応じて、[ **次へ** ] ボタンをクリックして、 `DIV` コントロールを表す要素を検索 `ListView` します (この要素の値はです `data-win-control` `WinJS.UI.ListView` )。

     DOM Explorer で `DIV` 要素が選択された状態になります。

9. DOM Explorer の右側にあるウィンドウで [ **イベント** ] タブを選択します。

     次に示すように、`DIV` 要素のアクティブ サブスクライバーがあるイベントが表示されます。

     ![DOM Explorer の [イベント] タブ](../debugger/media/js-dom-events.png "JS_DOM_Events")

10. これらのイベントのイベント リスナーに移動するには、関連付けられた JavaScript ファイルのリンクを選択します。

11. DOM 階層の親要素のイベント リスナーを迅速に特定するには、DOM Explorer の下側にある階層リストの親要素を選択します。

     ![DOM 階層で親要素を選択する](../debugger/media/js-dom-breadcrumbs.png "JS_DOM_Breadcrumbs")

     [ **イベント** ] タブには、[階層] ボックスの一覧で選択した任意の要素のイベントリスナーが表示されます。

### <a name="tips-for-resolving-issues-with-event-listeners"></a><a name="Tips"></a> イベントリスナーに関する問題の解決に関するヒント
 一部のアプリシナリオでは、イベントリスナーは [Removeeventlistener](https://msdn.microsoft.com/library/ie/ff975250\(v=vs.85\).aspx)を使用して明示的に削除する必要があります。 コードの実行中に DOM 要素からイベントリスナーが削除されたかどうかをテストするには、DOM Explorer の [ **イベント** ] タブを使用します。 これらの問題の解決に役立つヒントを次に示します。

- Visual Studio [プロジェクトテンプレート](https://msdn.microsoft.com/library/windows/apps/hh758331.aspx)で実装された単一ページナビゲーションモデルを使用するアプリでは、通常、ページの一部である DOM 要素などのオブジェクトに登録されているイベントリスナーを削除する必要はありません。 このシナリオでは、DOM 要素およびその関連付けられたイベント リスナーの有効期間は同じであり、ガベージ コレクションが可能です。

- DOM 要素またはオブジェクトの有効期間が関連付けられたイベント リスナーと異なる場合には、`removeEventListener` メソッドを呼び出す必要があります。 たとえば、`window.onresize` イベントを使用する場合に、イベントを処理するページから離れるとイベント リスナーを削除しなければならない場合があります。

- `removeEventListener` が指定のリスナーを削除できなかった場合は、別のオブジェクトのインスタンスが呼び出された可能性があります。 リスナーを追加するときに、 [Bind メソッド (Function)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) メソッドを使用してこの問題を解決できます。

- [Bind メソッド (Function)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)を使用するか、匿名関数を使用して追加されたイベントリスナーを削除するには、リスナーを追加するときに、関数のインスタンスを格納します。 このパターンを安全に使用するための 1 つの方法を次に示します。

    ```javascript
    // You could use the following code within the constructor function of an object, or
    // in the ready function of a PageControl object (Store app).
    this.storedHandler = this._handlerFunc.bind(this);
    elem.addEventListener('mouseup', this.storedHandler);

    // In this example, add the following code in the PageControl object's unload function.
    elem.removeEventListener('mouseup', this.storedHandler);

    ```

     バインドされた関数への参照を保存する代わりに次のコードを使用した場合、イベント リスナーを明示的に削除することはできなくなります。

    ```javascript
    // Avoid this pattern. No reference to the bound function is available.
    elem.addEventListener('mouseup', this._handlerFunc.bind(this));
    ```

- `removeEventListener` のような `obj.on<eventname>` 属性を使用して追加した場合には、`window.onresize = handlerFunc` を使用してイベント リスナーを削除することはできません。

- アプリケーションの [Javascript メモリ](../profiling/javascript-memory.md) に javascript メモリアナライザーを使用します。 明示的に削除されたイベント リスナーは、メモリー リークとして表示されることがあります。

## <a name="see-also"></a>参照

- [クイック スタート:HTML および CSS のデバッグ](../debugger/quickstart-debug-html-and-css.md)
- [DOM Explorer を使用した CSS スタイルのデバッグ](../debugger/debug-css-styles-using-dom-explorer.md)
- [DOM Explorer を使用したレイアウトのデバッグ](../debugger/debug-layout-using-dom-explorer.md)