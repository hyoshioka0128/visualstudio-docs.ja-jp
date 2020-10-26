---
title: '方法: 要素の CLR 属性を設定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
ms.assetid: b3db3c74-920c-4701-9544-6f75cbe8b7c9
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 72ad9175729451c82fca3b61d06e449edaf8cf38
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662538"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>方法: 要素の CLR 属性を設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

カスタム属性は、ドメイン要素、図形、コネクタ、および図に追加できる特殊な属性です。 クラスから継承する任意の属性を追加でき `System.Attribute` ます。

### <a name="to-add-a-custom-attribute"></a>カスタム属性を追加するには

1. **DSL エクスプローラー**で、カスタム属性を追加する要素を選択します。

2. [ **プロパティ** ] ウィンドウで、[ **カスタム属性** ] プロパティの横にある参照ボタン ([.**..**]) をクリックします。

     [ **属性の編集** ] ダイアログボックスが表示されます。

3. [ **名前** ] 列で、をクリックし、 **\<add attribute>** 属性の名前を入力します。 Enter キーを押します。

4. 属性名の下の行には、かっこが表示されます。 この行で、属性のパラメーターの型 (たとえば、) を入力 `string` し、enter キーを押します。

5. [ **名前] プロパティ** 列に、適切な名前 (たとえば、) を入力し `MyString` ます。

6. **[OK]** をクリックします。

     **カスタム属性**プロパティの属性が次の形式で表示されるようになりました。

     `[`*AttributeName* `(`*ParameterName* `=`*型*`)]`

## <a name="see-also"></a>参照
 [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
