---
title: '&lt;loc &gt; (JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <loc> JavaScript XML tag
- loc JavaScript XML tag
ms.assetid: 0d3349b6-4bdd-418f-bc11-73665305baae
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cf6016b2c12fd5ebe7cfb76c14c776508d99d2db
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651478"
---
# <a name="ltlocgt-javascript"></a>&lt;loc &gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ローカライズされた IntelliSense 情報を提供するサイドカー ファイルの場所と種類を指定します。

## <a name="syntax"></a>構文

```
<loc filename="filename"
    format="vsdoc|messagebundle" />
```

#### <a name="parameters"></a>パラメーター
 `filename` 省略可能。 ニュートラル カルチャのローカリゼーション情報を含むサイドカー ファイルのルート名。 Visual Studio は、ローカリゼーション情報を検索するとき、このファイルのカルチャ固有のバージョンを確認しようとします。 たとえば、`filename` が jquery.xml の場合、Visual Studio は `<loc>` 要素を格納する .js ファイルと同じ場所で正しいカルチャ固有のフォルダー (JA など) を検索します。 カルチャ固有のフォルダーが見つかった場合は、その中に jquery.xml ファイルがあるかどうかをチェックします。 正しいファイルを見つけることができない場合は、代わりにマネージド リソースの場所の規則を使用します。 `filename` の既定値は現在のファイルの名前ですが、拡張子は .js ではなく .xml です。

 `format` 省略可能。 ローカリゼーションに使用するサイドカー ファイルの種類。 `messagebundle` を使用して、Open Ajax メタデータによって定義されるメッセージ バンドルの使用を指定します。 `messagebundle` は推奨される形式です。 ただし、この形式は Microsoft Ajax または .winmd ファイルではサポートされません。 `vsdoc` を使用して、Microsoft Ajax および Windows ランタイムで使用される標準の .NET Framework のローカリゼーション形式を指定します。 この属性は省略できます。 `vsdoc` は既定の形式です。

## <a name="remarks"></a>解説
 `<loc>` 要素は、`<reference>` 要素と同じセクションのファイルの先頭に記述する必要があります。 `<loc>` 要素の使い方の規則は `<reference>` 要素と同じです。 詳細については、「 [JavaScript IntelliSense](../ide/javascript-intellisense.md)」の「参照ディレクティブ」セクションを参照してください。

 Visual Studio は、.js ファイルごとに 1 つの `<loc>` 要素を処理します。 複数の `<loc>` 要素が存在する場合は、1 つの `<loc>` 要素だけが使用されます。 どの `<loc>` 要素を使用するかを決めるための動作は定義されていません。

 メッセージ バンドル形式を使用しているときは、XML ドキュメント コメントで `locid` 属性を使用して `name` 属性の値を指定します。

## <a name="example"></a>例
 次の例は、messagebundle 形式で `<loc>` 要素を使用する方法を示しています。 次の XML を messageFilename.xml という名前のファイルに追加し、そのファイルを `filename` パラメーターの記述で指定されたように正しいカルチャ固有のフォルダーに配置します。

```
<?xml version="1.0" encoding="utf-8" ?>
<messagebundle>
  <msg name="1">A class that represents a rectangle</msg>
  <msg name="2">The height of a rectangle</msg>
  <msg name="3">The width of a rectangle</msg>
</messagebundle>

```

 messagebundle の例では、以下のコードをプロジェクトの JavaScript ファイルに追加します。 `<loc>` 要素は、JavaScript ファイルの最初の行に記述する必要があります。 このコード内の説明は、可能な場合はローカライズされた説明と置き換えられます。

```javascript
/// <loc filename="messageFilename.xml" format="messagebundle"/>

function doSomething(a,b)
{
    /// <summary locid='1'>description</summary>
    /// <param name='a' locid='2'>parameter a description</param>
    /// <param name='b' locid='3'>parameter b description</param>
}

```

 次の例では、VSDoc 形式を使用します。 次の XML を scriptFilename.xml という名前のファイルに追加し、そのファイルを正しいカルチャ固有のフォルダーに配置します。

```
<?xml version="1.0" encoding="utf-8" ?>
<doc>
  <assembly>
    <name>Lights</name>
  </assembly>
  <members>
    <member name="M:illuminate">
      <summary>Activates a light. </summary>
      <param name='a'>The light to activate. </param>
    </member>
  </members>
</doc>

```

 VSDoc の例では、以下のコードをプロジェクトの JavaScript ファイルに追加します。 このコード内の説明は、可能な場合はローカライズされた説明と置き換えられます。

```javascript
/// <loc filename="scriptFilename.xml" format="vsdoc" />

function illuminate(a)
{
    /// <summary locid='M:illuminate'>description</summary>
    /// <param name='a' type='Number'>parameter a description</param>
}

```

## <a name="see-also"></a>関連項目
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)
