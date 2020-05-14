---
title: JavaScript IntelliSense の XML ドキュメントコメントを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code comments, JavaScript IntelliSense
- XML documentation comments, JavaScript IntelliSense
- documentation comments [JavaScript]
- IntelliSense [JavaScript], XML documentation comments
ms.assetid: a27f5b50-9807-436f-a0cf-6f3137ecbaf0
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 21fdc15b161b7d1cef30effe82e518a174bc9666
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619549"
---
# <a name="create-xml-documentation-comments-for-javascript-intellisense"></a>JavaScript IntelliSense の XML ドキュメント コメントを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*XML ドキュメントコメント*は、関数、フィールド、変数などのコード要素に関する情報を提供するためにスクリプトに追加する JavaScript コメントです。 Visual Studio では、スクリプト関数を参照するときに、これらのテキストの説明が IntelliSense と共に表示されます。

 このトピックでは、XML ドキュメントコメントの使用に関する基本的なチュートリアルについて説明します。 [@No__t_1var >](../ide/var-javascript.md)や[\<value >](../ide/value-javascript.md)などの他の要素の使用方法、およびその他のコード例については、「 [XML ドキュメントコメント](../ide/xml-documentation-comments-javascript.md)」を参照してください。 @No__t_0 などの非同期コールバックに IntelliSense 情報を提供する方法の詳細については、「 [\<returns >](../ide/returns-javascript.md)」を参照してください。

> [!NOTE]
> XML ドキュメントのコメントは、参照されるファイル、アセンブリ、およびサービスでのみ使用できます。

### <a name="to-create-xml-documentation-comments-for-a-javascript-function"></a>JavaScript 関数の XML ドキュメントコメントを作成するには

- 関数で、 [\<summary >](../ide/summary-javascript.md)、 [\<param >](../ide/param-javascript.md)、および[\<returns](../ide/returns-javascript.md) > 要素を追加し、各要素の前に3つのスラッシュ記号 (///) を付けます。

    > [!NOTE]
    > 各要素は1行に配置する必要があります。

     次の例は、JavaScript 関数を示しています。

    ```javascript
    function getArea(radius)
    {
        /// <summary>Determines the area of a circle that has the specified radius parameter.</summary>
        /// <param name="radius" type="Number">The radius of the circle.</param>
        /// <returns type="Number">The area.</returns>
        var areaVal;
        areaVal = Math.PI * radius * radius;
        return areaVal;
    }
    ```

- XML ドキュメントのコメントを表示するには、次の例に示すように、XML ドキュメントのコメントでマークされた関数の名前と始めかっこを入力します。

    ```javascript
    var areaVal = getArea(
    ```

     XML ドキュメントコメントを含む関数の始めかっこを入力すると、コードエディターは、IntelliSense を使用して XML ドキュメントコメントに定義されている情報を表示します。

### <a name="to-create-xml-documentation-comments-for-a-javascript-field"></a>JavaScript フィールドの XML ドキュメントコメントを作成するには

- コンストラクター関数またはオブジェクト定義で、3つのスラッシュ記号 (///) の前に[\<field >](../ide/field-javascript.md)要素を追加します。

     次の例は、コンストラクター関数での `<field>` 要素の使用方法を示しています。 その他の例については、「 [\<field >](../ide/field-javascript.md)」を参照してください。

    ```javascript
    function Engine() {
        /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>
        this.HorsePower = 150;
    }
    ```

- XML ドキュメントコメントを表示するには、次の例に示すように、XML ドキュメントコメントでマークされた関数コンストラクターを使用してオブジェクトを作成します。

    ```javascript
    var eng = new Engine();
    ```

- 次の行に、オブジェクトの名前とピリオドを入力して、フィールドの IntelliSense 情報を表示します。

    ```javascript
    eng.
    ```

### <a name="to-create-xml-documentation-comments-for-an-overloaded-function"></a>オーバーロードされた関数の XML ドキュメントコメントを作成するには

1. 関数で、各オーバーロードの[\<signature >](../ide/signature-javascript.md)要素を追加します。 これらの要素には、`<summary>`、`<param>`、`<returns>` などの他の要素を追加します。各要素の前には、3つのスラッシュ記号 (///) を付けます。

     次の例は、オーバーロードされた JavaScript 関数を示しています。 この例では、オーバーロードはパラメーターの型によって異なります。

    ```javascript
    function calc(a) {
        /// <signature>
        /// <summary>Function summary 1.</summary>
        /// <param name="a" type="Number">A number.</param>
        /// <returns type="Number" />
        /// </signature>
        /// <signature>
        /// <summary>Function summary 2.</summary>
        /// <param name="a" type="String">A string.</param>
        /// <returns type="Number" />
        /// </signature>
        return a;
    }
    ```

2. XML ドキュメントのコメントを表示するには、次の例に示すように、XML ドキュメントのコメントでマークされている関数の名前と始めかっこを入力します。

    ```javascript
    calc(
    ```

### <a name="to-create-localized-intellisense"></a>ローカライズされた IntelliSense を作成するには

1. OpenAjax MessageBundle 形式のドキュメントコメントを含む XML ファイルを作成します。

    > [!IMPORTANT]
    > MessageBundle は推奨される形式です。 この形式は、Microsoft Ajax または winmd ファイルではサポートされていません。 代替 `VSDoc` 形式の使用の詳細については、「 [\<loc >](../ide/loc-javascript.md)」を参照してください。

     次の例では、ローカライズされた IntelliSense 情報を含むサイドカーファイルの内容を示します。 これは、JA-JP のようなカルチャ固有のフォルダーにある XML ファイルです。 フォルダーは、`<loc>` 要素を含む .js ファイルと同じ場所にある必要があります。 XML ファイルのファイル名は、`<loc>` 要素で指定された `filename` パラメーターと一致している必要があります。

    ```
    <messagebundle>
      <msg name="1">A class that represents a rectangle</msg>
      <msg name="2">The length of the rectangle</msg>
      <msg name="3">The height of the rectangle</msg>
    </messagebundle>

    ```

2. .Js ファイルで、次のコードを追加します。 @No__t_0 要素は、スクリプトの前に宣言する必要があり、`<reference>` 要素と同じ使用規則に従います。 詳細については、「 [JavaScript IntelliSense](../ide/javascript-intellisense.md) 」および「 [\<loc >](../ide/loc-javascript.md)」を参照してください。

    ```javascript
    /// <loc filename="messageFilename.xml" format="messagebundle"/>

    ```

3. .Js ファイルで、XML ドキュメントの要素と既定の説明を追加します。 @No__t_0 属性値を、サイドカーファイルの対応する `name` 属性値に一致するように設定します。 既定の説明は、ローカライズされた IntelliSense 情報 (使用可能な場合) に置き換えられます。

    ```javascript
    function add(a,b)
    {
        /// <summary locid='1'>description</summary>
        /// <param name='a' locid='2'>parameter a description</param>
        /// <param name='b' locid='3'>parameter b description</param>
    }

    ```

4. XML ドキュメントのコメントを表示するには、次の例に示すように、関数の名前と始めかっこを入力します。

    ```javascript
    add(
    ```

## <a name="see-also"></a>参照
 [Javascript intellisense](../ide/javascript-intellisense.md) [XML ドキュメントコメント](../ide/xml-documentation-comments-javascript.md) [NIB: チュートリアル: ASP.NET での javascript intellisense](https://msdn.microsoft.com/4f6e0cc2-7f48-4dbf-abb0-7fb743a2d05b)
