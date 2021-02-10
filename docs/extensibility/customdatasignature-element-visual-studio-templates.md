---
title: CustomDataSignature 要素 (Visual Studio テンプレート) |Microsoft Docs
description: CustomDataSignature 要素について、およびカスタムデータを検索するためのテキスト署名をどのように指定するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <CustomDataSignature> Element (Visual Studio Templates)
- CustomDataSignature Element (Visual Studio Templates)
ms.assetid: 8c3db51d-7014-4484-802a-15aa1353dbdb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e5f42b3c5fe1dc5b9ab9697275876509eb0f8509
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99946060"
---
# <a name="customdatasignature-element-visual-studio-templates"></a>CustomDataSignature 要素 (Visual Studio テンプレート)
カスタムデータを検索するテキスト署名を指定します。

 \<VSTemplate> \<TemplateData>
 \<CustomDataSignature>

## <a name="syntax"></a>構文

```
<CustomDataSignature>"string"</CustomDataSignature>
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

 テキストは、カスタムデータを検索するために必要なテキスト署名が含まれている文字列です。

## <a name="remarks"></a>解説
 `CustomDataSignature` は省略可能な要素です。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
