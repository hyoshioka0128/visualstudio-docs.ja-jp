---
title: TemplateGroupID 要素 (Visual Studio テンプレート) |Microsoft Docs
description: TemplateGroupID 要素について、および項目テンプレートを表示するプロジェクトの種類を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateGroupID
helpviewer_keywords:
- TemplateGroupID element [Visual Studio Templates]
- <TemplateGroupID> element [Visual Studio Templates]
ms.assetid: bce7b49a-90bc-4691-aff3-a87e209f6d83
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d9db0d2744648901a9389bd2d2805d8c6a4073ae
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895363"
---
# <a name="templategroupid-element-visual-studio-templates"></a>TemplateGroupID 要素 (Visual Studio テンプレート)
項目テンプレートを表示するプロジェクトの種類を指定します。 この要素は、 [showbydefault Visual Studio テンプレート)](../extensibility/showbydefault-visual-studio-templates.md) がに設定されている場合に重要です `false` 。 [ [Showbydefault Visual Studio テンプレート)](../extensibility/showbydefault-visual-studio-templates.md) ] がに設定されている場合 `true` 、すべてのプロジェクトの種類で項目テンプレートを使用できます。

 \<VSTemplate> \<TemplateData>
 \<TemplateGroupID>

## <a name="syntax"></a>構文

```
<TemplateGroupID> ... </TemplateGroupID>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、項目テンプレートのカテゴリの識別子を指定します。

## <a name="remarks"></a>解説
 `TemplateGroupID` は要素です。

 要素の値 `TemplateGroupID` は、 \\ *\<version number>* \\ [**新しい項目の追加**] ダイアログボックスに表示されるテンプレートをフィルター処理するために、プロジェクトシステムの登録 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\ プロジェクト) と共に使用されます。

|Visual C++ の値|意味|
|------------------------|-------------|
|VC-Native|ネイティブ プロジェクトに使用されます。 プロジェクトの種類を特定できない場合は、これが既定値になります。|
|VC-Managed|マネージド (/clr) プロジェクトに使用されます|
|VC-Windows|Windows プラットフォーム (ネイティブ/マネージ/ストア) を対象とするすべてのプロジェクトに使用されます|
|WinRT-Native-UAP|Windows 10 ストア プロジェクトに使用されます|
|CodeSharing-Native|共有済みの項目のプロジェクトに使用されます|
|WinRT-Native-6.3|Windows 8.1 ストア プロジェクトに使用されます|
|WinRT-Native-Phone-6.3|Windows Phone 8.1 プロジェクトに使用されます|
|WinRT - ネイティブ|Windows 8.0 ストア プロジェクトに使用されます|
|VC-Android|Android プロジェクトに使用されます|

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
