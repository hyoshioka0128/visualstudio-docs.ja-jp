---
title: デコレーターのプロパティ
description: デコレーターは、図の図形またはコネクタに表示されるアイコン、テキスト、または展開/折りたたみの山かっこであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef863d0d3dab394c2ca427a27d039c19e5921a51
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97360834"
---
# <a name="properties-of-decorators"></a>デコレーターのプロパティ
デコレーターは、図の図形またはコネクタに表示されるアイコン、テキスト、または展開/折りたたみの山かっこです。 次の表は、3種類のデコレータのプロパティを示しています。 一部のプロパティは、図形デコレーターまたはコネクタデコレーターにのみ表示されます。

 詳細については、「 [Domain-Specific 言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「 [Domain-Specific 言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

## <a name="expandcollapse-decorator"></a>デコレータの展開/折りたたみ

|プロパティ|説明|Default|
|-|-|-|
|DisplayName|生成されたデザイナーに表示されるデコレータの名前。|折りたたみデコレータの展開|
|名前|デコレータの名前。|ExpandCollapseDecorator|
|メモ|このデコレータに関連付けられている非公式のメモ。|\<none>|
|System.windows.controls.primitives.iscrollinfo.horizontaloffset|デコレータの既定の位置を基準とする水平方向のオフセット (インチ単位)。 (図形のみ)。|0|
|System.windows.controls.primitives.popup.verticaloffset|デコレータの既定の位置を基準とする垂直方向のオフセット (インチ単位)。 (図形のみ)。|0|
|OffsetFromLine|既定の位置を基準とした、線からのデコレータのオフセット (インチ単位)。 (コネクタの場合のみ)。|0|
|OffsetFromShape|形状からの、既定の位置を基準とする、インチ単位の、デコレータのオフセット。 (コネクタの場合のみ)。|0|
|[位置]|デコレータの既定の位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.sourcetop|

## <a name="icon-decorator"></a>アイコンデコレータ

|プロパティ|説明|Default|
|-|-|-|
|DefaultIcon|表示するアイコンまたはイメージファイルのパス。|\<none>|
|DisplayName|生成されたデザイナーに表示されるデコレータの名前。|アイコンデコレータ|
|名前|デコレータの名前。|IconDecorator|
|メモ|デコレータに関連付けられている非公式のメモ。|\<none>|
|System.windows.controls.primitives.iscrollinfo.horizontaloffset|デコレータの既定の位置を基準とする水平方向のオフセット (インチ単位)。 (図形のみ)。|0|
|System.windows.controls.primitives.popup.verticaloffset|デコレータの既定の位置を基準とする垂直方向のオフセット (インチ単位)。 (図形のみ)。|0|
|OffsetFromLine|既定の位置を基準とした、線からのデコレータのオフセット (インチ単位)。 (コネクタの場合のみ)。|0|
|OffsetFromShape|形状からの、既定の位置を基準とする、インチ単位の、デコレータのオフセット。 (コネクタの場合のみ)。|0|
|[位置]|デコレータの既定の位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.sourcetop|

## <a name="textdecorator"></a>TextDecorator

|プロパティ|説明|Default|
|-|-|-|
|DefaultText|表示される既定のテキスト。|Label|
|DisplayName|生成されたデザイナーに表示されるデコレータの名前。|Label|
|FontSize|デコレータに表示されるテキストのフォントサイズ。|8|
|FontStyle|デコレータに表示されるテキストのフォントスタイル。|通常|
|名前|デコレータの名前。|Label|
|メモ|デコレータに関連付けられている非公式のメモ。|\<none>|
|System.windows.controls.primitives.iscrollinfo.horizontaloffset|デコレータの既定の位置を基準とする水平方向のオフセット (インチ単位)。 (図形のみ)。|0|
|System.windows.controls.primitives.popup.verticaloffset|デコレータの既定の位置を基準とする垂直方向のオフセット (インチ単位)。 (図形のみ)。|0|
|OffsetFromLine|既定の位置を基準とした、線からのデコレータのオフセット (インチ単位)。 (コネクタの場合のみ)。|0|
|OffsetFromShape|形状からの、既定の位置を基準とする、インチ単位の、デコレータのオフセット。 (コネクタの場合のみ)。|0|
|[位置]|デコレータの既定の位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.targetbottom|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))