---
title: Image 図形のプロパティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.selectimagedialog
- vs.dsltools.dsldesigner.imageshape
helpviewer_keywords:
- Domain-Specific Language, image shape
ms.assetid: 9ce00ccd-07f2-4640-ac96-2a60481d0d72
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 79ec5470a8bac83d8e60454c984739f1e520b634
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671386"
---
# <a name="properties-of-image-shapes"></a>イメージ シェイプのプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

イメージ図形を使用して、生成されたデザイナーでのドメインクラスの表示方法を指定できます。 `Image`クラスのプロパティを定義済みのイメージファイルに設定して、イメージシェイプを定義します。 次の形式がサポートされています。

- .gif

- .jpg

- .jpeg

- .bmp

- .wmf

- .emf

- .png

  既定では、イメージファイルなどのデザイナーリソースファイルは、 **Dsl**プロジェクトの**Resources**フォルダーに配置されます。

  詳細については、「 [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「 [ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

  イメージ図形には、次の表に示すプロパティがあります。

|プロパティ|説明|Default|
|--------------|-----------------|-------------|
|[塗りつぶしの色]|この図形の塗りつぶしの色。|White|
|塗りつぶしのグラデーションモード|この図形の塗りつぶしのグラデーションモード。|水平|
|既定の接続ポイントがある|の場合 `True` 、図形は生成されたデザイナーで top、bottom、left、および right の各接続ポイントを使用します。|×|
|輪郭の色|この図形の輪郭の色。|Black|
|輪郭の破線のスタイル|この図形の輪郭の破線のスタイル (実線、ダッシュ、ドット、ダッシュドット、ダッシュ Dotドット、またはカスタム)。|[実線]|
|アウトラインの太さ|この図形の輪郭の太さ。|0.03125|
|テキストの色|この図形に関連付けられているテキストデコレーターに使用される色。|Black|
|アクセス修飾子|ジオメトリシェイプのアクセス修飾子 (パブリックまたは内部)。|パブリック|
|カスタム属性|この図形から生成されるソースコードクラスに属性を追加するために使用します。|\<none>|
|2つの派生を生成します|`True`の場合、基本クラスと部分クラス (オーバーライドによるカスタマイズをサポートする) の両方が生成されます。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|×|
|カスタムコンストラクターがある|`True`の場合、カスタムコンストラクターがソースコードで提供されます。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|×|
|継承修飾子|イメージシェイプ ( `none` 、または) から生成されるソースコードクラスの継承の種類について説明し `abstract` `sealed` ます。|なし|
|基本イメージシェイプ|この図形の基本クラス。|(なし)|
|名前|この図形の名前。|現在の名前|
|名前空間|この図形に関連付けられている名前空間。|現在の名前空間|
|ツールヒントの種類|ツールヒントが定義されている場所 (fixed、variable、none)。 固定されている場合は、 `Fixed Tooltip Text` プロパティの値がツールヒントとして使用されます。変数の場合は、ツールヒントがカスタムコードで定義されます。|なし|
|メモ|この図形に関連付けられている非公式のメモ。|\<none>|
|初期の高さ|この図形の初期の高さ (インチ単位)。|1|
|初期の幅|この図形の初期の幅 (インチ単位)。|1.5|
|プロパティとして塗りつぶされた塗りつぶしの色<br /><br /> 露出塗りつぶしのグラデーションモード<br /><br /> プロパティとして公開されたアウトラインの色<br /><br /> プロパティとしてアウトラインの破線のスタイルを公開<br /><br /> プロパティとしてアウトラインの太さを公開<br /><br /> テキストの色を公開します|の場合 `True` 、ユーザーは図形の指定されたプロパティを設定できます。 これを設定するには、図形定義を右クリックし、[ **公開の追加**] をクリックします。|×|
|説明|生成されたデザイナーを文書化するために使用します。|\<none>|
|表示名|この図形に対して生成されたデザイナーに表示される名前。|\<none>|
|固定ツールヒントのテキスト|固定のツールヒントに使用されるテキスト。|\<none>|
|ヘルプ キーワード|この要素の F1 ヘルプのインデックスを作成するために使用されるキーワード。|\<none>|
|Image|この図形に使用されるイメージファイルのパス。|\<none>|

## <a name="see-also"></a>参照
 [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
