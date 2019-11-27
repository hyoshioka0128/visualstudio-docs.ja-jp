---
title: JavaScript
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-javascript
ms.topic: conceptual
ms.assetid: f3eee13e-30e4-4bc1-81f5-058d7e379b75
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 175cb6f6a8a3f240c244e139406841b0546209cc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295901"
---
# <a name="javascript-in-visual-studio"></a>Visual Studio の JavaScript
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript は Visual Studio の第一級の言語です。 Visual Studio IDE で JavaScript コードを記述する場合に、ほとんどの標準的な編集補助機能 (コード スニペット、IntelliSense など) を使用できます。 多くの種類のアプリケーションやサービスの JavaScript コードを記述できます。

 JavaScript 言語のリファレンス ドキュメントについては、「[JavaScript 言語リファレンス](https://msdn.microsoft.com/library/d1et7k7c\(v=vs.94\).aspx)」を参照してください。

 特定のバージョンの Visual Studio、または特定の Visual Studio 拡張機能では、HTML および JavaScript を使用して特定の種類のアプリケーションとサービスを開発する必要があります。 次の一覧には詳細情報へのリンクがあります。

- Apache Cordova を使用してクロスプラットフォーム アプリを作成するには、[Apache Cordova 用の Visual Studio Tools を取得](https://go.microsoft.com/fwlink/p/?LinkId=397606)します。

- [Windows ストア](https://developer.microsoft.com/)、[Windows Phone](https://developer.microsoft.com/)、ユニバーサル アプリ (両方のプラットフォームをサポートするアプリ) を作成するには、[ツールを入手](https://developer.microsoft.com/windows/downloads)します。

- クラウドベースのサービスを作成するには、[Microsoft Azure サイト](https://azure.microsoft.com/documentation/)を参照してください。

- Web サイトと Web アプリを作成するには、[ASP.NET サイト](https://dotnet.microsoft.com/apps/aspnet/web-apps)を参照してください。

  > [!NOTE]
  > 空の ASP.Net Web サイトを作成して、HTML、CSS、および JavaScript のプログラミング用に使用できます。 ASP.NET によって提供される Webconfig ファイルは、Visual Studio でのデバッグを使用可能にします (またはアプリの実行時に F12 ツールを使用できます)。

  Visual Studio の JavaScript エディターでは IntelliSense をサポートしています。 詳細については、「[JavaScript IntelliSense](../ide/javascript-intellisense.md)」を参照してください。

## <a name="whats-new-in-javascript"></a>JavaScript の新機能
 JavaScript の新機能は、以下の表にリストされています。

|機能|説明|
|-------------|-----------------|
|クラス|[クラス](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/class)の宣言をサポートする新しい構文です。|
|Promise|[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) を使用すると、より簡単で読みやすい非同期コーディングができます。 Promise コンストラクターは、`all` および `race` の各ユーティリティ メソッドと一緒にサポートされます。|
|反復子|反復可能なオブジェクト (配列、配列に似たオブジェクト、および反復子を含む) を使用して反復処理を行い、それぞれの別個のプロパティの値に対して実行するステートメントを伴うカスタム反復フックを呼び出すことができるようになりました。 詳細については、「[反復子とジェネレーター](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Iterators_and_Generators)」を参照してください。 **注:** ジェネレーターはまだサポートされていません。|
|アロー関数|アロー関数 (=>) は、レキシカルな `function` によるバインドの機能を持つ `this` キーワードの略式の構文を提供します。|
|組み込みオブジェクトの新しいメソッド|[Array オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)、[Math オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math)、[Number オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)、[Object オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)、および [String オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)の組み込みオブジェクトに、データの操作や確認に使用できる多くの新しいユーティリティ関数とプロパティが含まれています。|
|オブジェクト リテラルの機能強化|オブジェクトにおいて、計算プロパティ、簡潔なメソッドの定義、および同じ名前の変数に値が初期化されるプロパティの略式の構文がサポートされるようになりました。 詳細については、「[オブジェクトの作成](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)」を参照してください。|
|プロキシ|[プロキシ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Proxy)により、オブジェクトのカスタム動作を設定できます。|
|Rest パラメーター|rest パラメーターを使用すると、関数呼び出しの連続する引数を配列に変換できます。 詳細については、「[関数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)」を参照してください。|
|spread 演算子|[spread 演算子](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/Spread_operator) (`…`) は、反復可能な式を個々の引数に展開します。 たとえば、`a.b(…array)` は `a.b.apply(a, array)` とほとんど同じです。|
|記号|[Symbol](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Symbol) オブジェクトを使用して既存のオブジェクトにプロパティを追加すると、既存のオブジェクトのプロパティと干渉する可能性がなく、意図せずに可視になる可能性もなく、他のコードから整合性のない追加が実行される可能性もありません。|
|テンプレート文字列|[テンプレート文字列](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Template_literals)では、その文字列リテラルを式として評価し、そのリテラル文字列に連結することができます。|
|Unicode の機能強化|Unicode のサポートが向上しました。 たとえば、エスケープ シーケンスの新しい形式では、アストラル コード ポイント (16 進数字 4 桁を超えるコード ポイント) がサポートされます。 詳細については、「[特殊文字](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Regular_Expressions#Types_of_special_characters)」を参照してください。|
|WeakSet|[WeakSet](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/WeakSet) は、他の場所から参照されていない場合にガベージ コレクションの対象となるオブジェクトのコレクションです。|
