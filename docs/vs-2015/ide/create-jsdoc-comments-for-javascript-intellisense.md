---
title: JavaScript IntelliSense の JSDoc コメントを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: a0dadc81-3755-4a47-bcee-c1010819ff2a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b974f3450b88ab22e58e284881f270c1b3d72298
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72619272"
---
# <a name="create-jsdoc-comments-for-javascript-intellisense"></a>JavaScript IntelliSense の JSDoc コメントを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IntelliSense in Visual Studio は、標準的な JSDoc コメントを使用してスクリプトに追加する情報を表示します。 JSDoc コメントを使用すると、関数、フィールド、変数などのコード要素についての情報を指定できます。

## <a name="jsdoc-comment-tags"></a>JSDoc コメント用のタグ
 次の標準的な JSDoc コメント タグは、コードについての情報を表示するために IntelliSense によって使用されます。

|  JSDoc タグ   |                       Syntax                        |                                                     メモ                                                      |
|--------------|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| @deprecated  |              @deprecated*説明*              |                                   非推奨の関数またはメソッドを指定します。                                   |
| @description |             @description*説明*              |                              関数またはメソッドの説明を指定します。                               |
|    @param    | @param {*型*} *パラメーター名*<em>説明</em> | 関数またはメソッドのパラメーターの情報を指定します。<br /><br /> TypeScript でもサポートさ @paramTag れています。 |
|  @property   |          @property {*型*} *プロパティ名*          |   オブジェクトで定義されているフィールドまたはメンバーについて、説明を含む情報を指定します。    |
|   @returns   |                  @returns {*type*}                  |           戻り値を指定します。<br /><br /> TypeScript の場合は、の代わりにを使用 @returnType @returns します。           |
|   @summary   |               @summary*説明*                |                   関数またはメソッドの説明を指定します (と同じ @description )。                   |
|    @type     |                   @type {*type*}                    |                                定数または変数の種類を指定します。                                |
|   @typedef   |         @typedef {*型*} *カスタム型名*          |                                            カスタム型を指定します。                                            |

### <a name="examples"></a>例
 次の例は、という名前の関数に対して、、、JSDoc の各タグを使用する方法を示して @description @param @return `getArea` います。

```javascript
/** @description Determines the area of a circle that has the specified radius parameter.
 * @param {number} radius The radius of the circle.
 * @return {number}
 */
function getArea(radius) {
    var areaVal;
    areaVal = Math.PI * radius * radius;
    return areaVal;
}
```

 前の例では、IntelliSense は説明、パラメーター、および `getArea` の始めかっこを入力したときに返す情報を表示します。

 ![関数の IntelliSense の情報](../ide/media/js-intellisense-jsdoc-comments.png "JS_IntelliSense_JSDoc_Comments")

 タグをタグと共に使用する方法を次の例に示し @typedef @property ます。

```javascript
/**
  * @typedef {object} Weather
  * @property {string} current The current weather.
  */
function getForecast(Weather) {
}

var w = new Weather();
```

 次の例は、JSDoc タグの使用方法を示して @type います。 この例で示すように、最初のアスタリスクのペア (\*\*) の後に続く 1 つのアスタリスク (*) は必須ではありません。

```javascript
/**
    @type {string}
*/
const RED = 'FF0000';

```

 次の例は、JSDoc タグの使用方法を示して @deprecated います。

```javascript
/**
 * @deprecated since version 2.0
 */
function old() {
}
```
