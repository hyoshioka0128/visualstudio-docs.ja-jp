---
title: '方法: 要素の CLR 属性を設定する'
description: System.object クラスから継承する属性を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8e566eafce9b5763830c00659a860e6329671bcd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922659"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>方法: 要素の CLR 属性を設定する
カスタム属性は、ドメイン要素、図形、コネクタ、および図に追加できる特殊な属性です。 クラスから継承する任意の属性を追加でき `System.Attribute` ます。

### <a name="to-add-a-custom-attribute"></a>カスタム属性を追加するには

1. **DSL エクスプローラー** で、カスタム属性を追加する要素を選択します。

2. [ **プロパティ** ] ウィンドウで、[ **カスタム属性** ] プロパティの横にある参照ボタン ([.**..**]) をクリックします。

     [ **属性の編集** ] ダイアログボックスが表示されます。

3. [ **名前** ] 列で、をクリックし、 **\<add attribute>** 属性の名前を入力します。 Enter キーを押します。

4. 属性名の下の行には、かっこが表示されます。 この行で、属性のパラメーターの型 (たとえば、) を入力 `string` し、enter キーを押します。

5. [ **名前] プロパティ** 列に、適切な名前 (たとえば、) を入力し `MyString` ます。

6. **[OK]** をクリックします。

     **カスタム属性** プロパティの属性が次の形式で表示されるようになりました。

     `[`*AttributeName* `(`*ParameterName* `=`*型*`)]`

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))