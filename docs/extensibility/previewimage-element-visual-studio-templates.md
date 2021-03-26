---
title: PreviewImage 要素 (Visual Studio テンプレート) |Microsoft Docs
description: PreviewImage 要素と、[新しいプロジェクト] ダイアログボックスまたは [新しい項目の追加] ダイアログボックスに表示されるプレビューイメージのファイル名を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <PreviewImage> Element (Visual Studio Templates)
- PreviewImage Element (Visual Studio Templates)
ms.assetid: d1796f20-523b-4e0d-8ac3-ca87f3b5a9b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fc7a370885d24a586262bebd4182daacd84a9b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090227"
---
# <a name="previewimage-element-visual-studio-templates"></a>PreviewImage 要素 (Visual Studio テンプレート)
[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスに表示されるプレビューイメージのプレビューイメージをファイル名として指定します。

 \<VSTemplate> \<TemplateData>
 \<PreviewImage>

## <a name="syntax"></a>構文

```
<PreviewImage>"filename"</PreviewImage>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、 **新しいプロジェクト** または [ **新しい項目の追加** ] ダイアログボックスでの表示方法を定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストは、ファイル名を表す文字列である必要があります。

## <a name="remarks"></a>注釈
 `PreviewImage` は省略可能な要素です。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
