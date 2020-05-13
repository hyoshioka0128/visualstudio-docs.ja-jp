---
title: RequireJS の IntelliSense のカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 2be07ef8-9c08-444b-a21a-22a4fe6386a3
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 279ac7737460c90f86918ae673e8f64ef1215546
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665883"
---
# <a name="customizing-intellisense-for-requirejs"></a>RequireJS 用に IntelliSense をカスタマイズする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 2013 Update 4 以降では、人気のある RequireJS JavaScript ファイルとモジュール式ローダーがサポートされるようになりました。 RequireJS を使用すると、コード モジュール間の依存関係を定義し、必要な場合にのみモジュールを動的に読み込む処理が簡単になります。 RequireJS を使用する JavaScript コードを作成する際には、モジュール定義から参照するモジュールや、コード内から `require()` への呼び出しを使用して参照するモジュールに対して、IntelliSense による候補が提示されます。

 既定では、Visual Studio は RequireJS に対してごく基本的な構成のみのサポートを提供しますが、一般的には独自のカスタム構成設定をセットアップする (つまり、ライブラリの別名を定義する) のが通例となっています。 このトピックでは、プロジェクトの独特のセットアップを処理するために Visual Studio をカスタマイズするさまざまな方法について説明します。

 このトピックでは、次の方法を説明します。

- ASP.NET プロジェクトで RequireJS をカスタマイズする

- JSProj プロジェクトで RequireJS をカスタマイズして、Apache Cordova アプリ、Windows ストア アプリ、および LightSwitch HTML アプリを構築するために使用する

## <a name="customize-requirejs-in-aspnet-projects"></a>ASP.NET プロジェクトで RequireJS をカスタマイズする
 require.js という名前のファイルが現在の JavaScript ファイルで参照されている場合、自動的に RequireJS のサポートが有効になります (詳細については、「[JavaScript IntelliSense](../ide/javascript-intellisense.md)」の IntelliSense のコンテキスト確認に関するセクションを参照してください)。 ASP.NET プロジェクトでは、通常、_references.js ファイル内で /// \<reference/> ディレクティブを使用することによって require.js が参照されます。

### <a name="configure-the-data-main-attribute-in-an-aspnet-project"></a>ASP.NET プロジェクトで data-main 属性を構成する
 アプリを実行した時の動作を正確にシミュレートするには、require.js の設定時に最初に読み込まれるファイルを JavaScript エディターが認識する必要があります。 これは、通常、次に示すように require.js を参照する script 要素の `data-main` 属性を使用して、アプリケーションの HTML ファイル内で構成します。

```html
<script src="js/require.js" data-main="js/app.js"></script>
```

 この例では、data-main によって参照されるスクリプト (js/app.js) は、require.js の直後に読み込まれます。 直後に読み込まれるファイルは、RequireJS の使用を最初に構成するのに最適な場所です (`require.config()` を使用)。アプリケーション内で `data-main` のためにどのファイルを使用するかを JavaScript エディターに通知するには、`data-main` 属性を追加し、/// \<reference/> ディレクティブを変更してアプリケーション内で require.js を参照します。 たとえば、このディレクティブを使用することができます。

```javascript
/// <reference path="js/require.js" data-main="js/app.js" />
```

### <a name="configure-the-application-start-page-in-an-aspnet-project"></a>ASP.NET プロジェクトでアプリケーションのスタート ページを構成する
 アプリが実行されると、RequireJS はファイルへの相対パスを前提としています (例 "..\\ "パス" は、必要な .js ライブラリを読み込んだ HTML ファイルに対する相対パスです。 Visual Studio エディターで ASP.NET プロジェクトのコードを記述するときは、この開始ページが不明であるため、相対ファイル パスに使用する開始ページをエディターに知らせる必要があります。 そのためには、`start-page` 属性を /// \<reference/> ディレクティブに追加します。

```javascript
/// <reference path="js/require.js" data-main="js/app.js" start-page="/app/index.html" />
```

 `start-page` 属性には、アプリの実行時にブラウザーに表示されるページの URL を指定します。

## <a name="customize-requirejs-in-jsproj-projects"></a>JSProj プロジェクトで RequireJS をカスタマイズする
 JSProj プロジェクト (末尾に拡張子 .jsproj の付いたプロジェクト ファイル) は、Apache Cordova 用のアプリ、HTML ベースの Windows ストア アプリ、または LightSwitch HTML アプリをビルドするときに使用します。 ASP.NET のプロジェクトとは異なり、これらのプロジェクトは、プロジェクト内に存在する HTML ファイルから .js ファイルへの参照を読み取ります。 このため、JSProj プロジェクト内の JavaScript ファイルを編集する際に、require.js を参照する別の HTML ファイルで現在編集中の JavaScript ファイルが参照されている場合に、RequireJS のサポートが有効になっているのを見ることができます。

 JSProj プロジェクト ファイルでは、ASP.NET プロジェクトに必要なカスタマイズの手順は必要ありません。 つまり、require.js を参照する script タグの `data-main` 属性で使用されているスクリプト ファイルが自動的に読み込まれて require.js が構成されます。 require.js を参照する、HTML ファイルは、アプリケーションのスタート ページとしても使用されます。

## <a name="see-also"></a>参照
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)
