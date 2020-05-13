---
title: カスタムデータシグネチャ要素 ( Visual Studio テンプレート ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <CustomDataSignature> Element (Visual Studio Templates)
- CustomDataSignature Element (Visual Studio Templates)
ms.assetid: 8c3db51d-7014-4484-802a-15aa1353dbdb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec8bae34da0f007bac65f26c4e442c1d03e56d08
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739445"
---
# <a name="customdatasignature-element-visual-studio-templates"></a>要素をカスタマイズする
カスタム データを検索するテキスト署名を指定します。

 \<カスタムデータシグネチャ\<>> \<VS テンプレート>テンプレートデータ

## <a name="syntax"></a>構文

```
<CustomDataSignature>"string"</CustomDataSignature>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、[**新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスでの表示方法を定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストは、カスタム データを検索するために必要なテキスト署名を持つ文字列です。

## <a name="remarks"></a>Remarks
 `CustomDataSignature` は省略可能な要素です。

## <a name="see-also"></a>関連項目
- [ビジュアル スタジオ テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
