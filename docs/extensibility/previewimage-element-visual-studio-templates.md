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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e306f6453ca3abbc2ad881821254ca88a160d01b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967281"
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

## <a name="remarks"></a>解説
 `PreviewImage` は省略可能な要素です。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
