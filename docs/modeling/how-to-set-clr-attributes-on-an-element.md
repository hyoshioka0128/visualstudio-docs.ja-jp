---
title: '方法: 要素の CLR 属性を設定する'
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebda963bf1afa55fa8d7f98774c72a75d242ceef
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532458"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>方法: 要素の CLR 属性を設定する
カスタム属性は、ドメイン要素、図形、コネクタ、および図に追加できる特殊な属性です。 クラスから継承する任意の属性を追加でき `System.Attribute` ます。

### <a name="to-add-a-custom-attribute"></a>カスタム属性を追加するには

1. **DSL エクスプローラー**で、カスタム属性を追加する要素を選択します。

2. [**プロパティ**] ウィンドウで、[**カスタム属性**] プロパティの横にある参照ボタン ([.**..**]) をクリックします。

     [**属性の編集**] ダイアログボックスが表示されます。

3. [**名前**] 列で、をクリックし、 **\<add attribute>** 属性の名前を入力します。 Enter キーを押します。

4. 属性名の下の行には、かっこが表示されます。 この行で、属性のパラメーターの型 (たとえば、) を入力 `string` し、enter キーを押します。

5. [**名前] プロパティ**列に、適切な名前 (たとえば、) を入力し `MyString` ます。

6. **[OK]** をクリックします。

     **カスタム属性**プロパティの属性が次の形式で表示されるようになりました。

     `[`*AttributeName* `(`*ParameterName* `=`*型*`)]`

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)