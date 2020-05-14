---
title: R コード用の IntelliSense
description: Visual Studio の IntelliSense では、R コードを入力すると、関数、オブジェクトのメンバー、コード スニペット、入力候補に関する情報が表示されます。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 854f7d410e327ca92d0c5156d89bc21765e13cc7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62999129"
---
# <a name="intellisense"></a>IntelliSense

Visual Studio の IntelliSense では、コードを入力するときに、呼び出すことのできる関数、オブジェクトのメンバー、関数の引数、[コード スニペット](code-snippets-for-r.md)に関する情報が、見える位置に表示されます。 また、入力に合わせて入力候補が表示され、**Tab** キーまたは **Enter** キーを押すと自動的に入力されます ([[詳細設定]](editing-r-code-in-visual-studio.md#editor-options) タブの**エディター オプション**を参照)。 IntelliSense は、エディターと[対話型ウィンドウ](interactive-repl-for-r-in-visual-studio.md)の両方で利用可能です。

![関数のシグネチャを示す IntelliSense](media/intellisense-function-signature.png)

関数または他のステートメントを入力するとき、IntelliSense は、既に入力したものによって (大文字/小文字を区別して) フィルター処理されたオート コンプリート メニューを提供します。

![IntelliSense のオート コンプリート メニュー](media/intellisense-auto-complete-menu.png)

**Tab** (または、オプションの設定によっては **Enter** や **Space**) キーを押すと、ドロップダウンで選択した項目が挿入されます。 選択は方向キーで変更できます。

また、IntelliSense は、R オブジェクトのメンバーの候補も提供します。

![IntelliSense によるオブジェクト メンバーの候補](media/intellisense-auto-complete-r-objects.png)

**Esc** キーを押すとメニューは消えます。 **Ctrl** + **Space** キーを押すと再び表示できます。

関数呼び出しの開始 `(` を入力すると、終了 `)` が挿入され、前述したようにシグネチャ ヘルプが表示されます。

![IntelliSense が示す関数のシグネチャ ヘルプ](media/intellisense-function-signature.png)

**Esc** キーを押すとポップアップは表示されなくなります。関数シグネチャの場合は、**Ctrl** +**Shift**+ **Space** キーを押すと再び表示されます。

> [!Tip]
> その下にあるパラメーターのヘルプ テキストが不明瞭になる場合、**Ctrl** キーを押したままにして、パラメーターのヘルプ テキストを半透明にします。

## <a name="intellisense-for-user-defined-functions-and-variables"></a>ユーザー定義の関数および変数に対する IntelliSense

IntelliSense は、同じファイルのユーザー定義関数に (名前 - パラメーターの入力候補を含め) 適用されます。

![ユーザー定義関数に対する IntelliSense](media/intellisense-same-file-functions.png)

![ユーザー定義関数に対する IntelliSense のパラメーター候補](media/intellisense-parameter-completion.png)

また、IntelliSense は、同じファイルと現在のセッションの変数にも対応します。

![IntelliSense の変数の入力候補](media/intellisense-variable-completion.png)

> [!Note]
> 対話型ウィンドウでは、IntelliSense は現在の R セッションの名前のみを考慮し、プロジェクト内のファイルを無視します。

## <a name="code-suggestions"></a>コードの提案

余白に電球 (スマート タグと呼ばれます) が表示されたときは、Visual Studio がよく使われるアクションに使用できるショートカットがあることを提案しています。 たとえば、エディターで `library` ステートメントを含む行をポイントすると、電球マークが表示されます。 電球を選択すると、使用可能なオプションが表示されます。

![エディターでの R のスマート タグ](media/intellisense-smart-tags.png)
