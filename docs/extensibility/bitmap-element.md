---
title: ビットマップ要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d663351aad7d381dd5bfe4cbaa0a263cc70b821
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740000"
---
# <a name="bitmap-element"></a>ビットマップ要素
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
|guid|必須。 GUID/ID コマンド識別子の GUID です。<br /><br /> ビットマップの guid 属性は、VSPackage またはその他のコマンド グループに関連付けされていません。  ビットマップ定義に固有のものであり、他の目的には使用しないでください。|
|レシドID|GUID/ID コマンド ID の ID。 resID または href 属性が必要です。<br /><br /> resID 属性は、コマンド テーブルのマージ中にロードされるビットマップ ストリップを決定する整数リソース ID です。  コマンド テーブルが読み込まれると、リソース ID で指定されたビットマップが同じモジュールのリソースから読み込まれます。|
|使用リスト|resID 属性が存在する場合は必須です。 ビットマップ ストリップで使用可能なイメージを選択します。|
|href|ビットマップへのパス。 resID または href 属性が必要です。<br /><br /> インクルード パスは、結果のバイナリに埋め込まれている、示されたイメージ ファイルを検索します。  コマンド テーブルのマージ中に、イメージがコピーされ、リソースの参照や読み込みが不要になります。  usedList 属性が存在しない場合、ストリップ内のすべてのイメージが使用可能です。 **注:** イメージは *、.bmp* *、.png、* および *.gif*を含むいくつかの形式のいずれかで提供できます。  以前のバージョンのコンパイラでは、部分的な透過性を示すアルファ情報を持つ 32 ビット ビットマップ イメージはサポートされていませんでした。 これらのバージョンの回避策は *、.png*形式を使用することです。|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素
 [なし] :

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
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
