---
title: Bitmap 要素 |Microsoft Docs
description: Bitmap 要素はビットマップを定義します。 ビットマップは、リソースまたはファイルから読み込まれます。 この記事には例が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 32f07857f2d04989b0de021988b2961d4a1553d2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068220"
---
# <a name="bitmap-element"></a>Bitmap 要素
ビットマップを定義します。 ビットマップは、リソースまたはファイルから読み込まれます。

## <a name="syntax"></a>構文

```
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。<br /><br /> ビットマップの guid 属性は、VSPackage またはその他のコマンドグループに関連付けられていません。  これはビットマップ定義に対して一意である必要があり、他の目的には使用できません。|
|resID|GUID/ID コマンド識別子の ID。 ResID または href 属性のいずれかが必要です。<br /><br /> ResID 属性は、コマンドテーブルのマージ中に読み込まれるビットマップストリップを決定する整数リソース ID です。  コマンドテーブルを読み込むときに、リソース ID によって指定されたビットマップが、同じモジュールのリソースから読み込まれます。|
|未使用のリスト|ResID 属性が存在する場合は必須です。 ビットマップストリップで使用可能なイメージを選択します。|
|href|ビットマップへのパス。 ResID または href 属性のいずれかが必要です。<br /><br /> インクルードパスは、指定されたイメージファイルを検索します。これは、結果のバイナリに埋め込まれています。  コマンドテーブルのマージ中に、イメージがコピーされ、追加のリソース参照や読み込みは必要ありません。  使用リスト属性が存在しない場合は、ストリップ内のすべてのイメージを使用できます。 **注:**  イメージは、 *.bmp*、 *.png*、 *.gif* を含む複数の形式のいずれかで指定できます。  以前のバージョンのコンパイラでは、部分的な透明度のアルファ情報を持つ32ビットビットマップイメージがサポートされていませんでした。 これらのバージョンの回避策は、 *.png* 形式を使用することです。|
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ビットマップ要素](../extensibility/bitmaps-element.md)|ビットマップ要素をグループ化します。|

## <a name="example"></a>例

```
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
  usedList="1, 2, 3, 4"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
