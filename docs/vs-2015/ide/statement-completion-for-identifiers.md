---
title: 識別子の入力候補 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [JavaScript], statement completion
- statement completion, JavaScript IntelliSense
ms.assetid: c2cd4945-c67e-471b-8057-96cfd25f7fb2
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f5e52bf174e5a41d79fa23bfca39121db668e40e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72643855"
---
# <a name="statement-completion-for-identifiers"></a>識別子の入力候補
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript では、変数宣言に対して明示的な型指定は許可されません。 その結果、IntelliSense は常にオブジェクトのコンプリートリストを提供できません。 これは、さまざまな状況で発生する可能性があります。 いくつかの一般的なものを次に示します。

- パラメーターが宣言されていますが、次の例に示すように、アクティブなドキュメントの他の場所で呼び出されていません。

  ```javascript
  function illuminate(light) {
           light.  // Accurate statement completion is not available
                   // unless illuminate is called elsewhere with a
                   // parameter that has a value. If it is called only
                   // in a function that is a sibling to
                   // illuminate(light) in the call hierarchy, the
                   // IntelliSense engine also cannot determine the
                   // parameter type.
       }

  // Sibling function. No statement completion for light
  // object in preceding code.
  function lightLamp() {
      var x = illuminate(1);
  }

  // Uncomment the next line to obtain statement completion for
  // light object in preceding code.
  // var x = illuminate(1);
  ```

- オブジェクトは、イベントへの応答として呼び出される関数に含まれています。 デザイン時に、IntelliSense エンジンは、この状況で使用されるオブジェクトの種類を特定できません。

   IntelliSense エンジンで、イベントを呼び出す必要があると判断できた場合 (通常は、 `addEventListener` アクティブドキュメントのイベントにを使用します)、より正確な IntelliSense 情報が提供されます。

  IntelliSense がオブジェクトを識別できない場合、IntelliSense エンジンは、アクティブなドキュメントに存在する名前付きエンティティ (識別子) を入力候補リストに追加します。 入力候補一覧にこれらの識別子が含まれている場合は、その横に情報アイコンが表示されます。 また、各識別子のツールヒントは、式が不明であることを示します。 次の図は、 `light` オブジェクトとそのプロパティが未定義であるために識別できない型のオブジェクトのステートメント入力候補オプションを示しています。 ただし、プロパティは、 `intensity` 関数で使用されているため、識別子の一覧で使用でき `illuminate` ます。

  **識別できないオブジェクトの完了オプション**

  ![識別子の JavaScript IntelliSense](../ide/media/js-intellisense-identifiers.png "js_intellisense_identifiers")

  XML ドキュメントコメントまたは JavaScript IntelliSense 機能拡張機能を使用して、オブジェクトのコンプリートリストをオーバーライドできます。 これらの機能を使用して、型情報を提供したり、他の方法では使用できない場合にはよりわかりやすい IntelliSense 情報を指定したりすることができます。 詳細については、「 [JavaScript IntelliSense の拡張](../ide/extending-javascript-intellisense.md) 」および「 [XML ドキュメントコメントの作成](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)」を参照してください。

## <a name="see-also"></a>参照
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)
