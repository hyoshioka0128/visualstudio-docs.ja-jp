---
title: TargetPlatformName 要素 (Visual Studio テンプレート) |Microsoft Docs
description: TargetPlatformName 要素について、およびプロジェクトテンプレートが対象とするプラットフォームをどのように指定するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 3a6b1f45-b5d6-418e-add1-87ee8f15033d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5b8f81ad86c98ab31e8f5d5dddf0efa1b2c89d85
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903989"
---
# <a name="targetplatformname-element-visual-studio-templates"></a>TargetPlatformName 要素 (Visual Studio テンプレート)
プロジェクト テンプレートの対象となるプラットフォームを指定します。 この要素は、 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリを作成するためにプロジェクト テンプレートを使用することを指定するために使用されます。

## <a name="syntax"></a>構文

```xml
<VSTemplate>
    <TemplateData>
        <TargetPlatformName> OperatingSystem</TargetPlatformName>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[RequiredPlatformVersion](../extensibility/requiredplatformversion-element-visual-studio-templates.md)|プロジェクト テンプレートの対象となるオペレーティング システムのバージョンを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

## <a name="remarks"></a>解説
 テキストは、 **Windows** である必要があります。

## <a name="example"></a>例
 次の例では、プロジェクト テンプレートで [!INCLUDE[win8](../debugger/includes/win8_md.md)] 以降が対象となるように指定しています。

```xml
<VSTemplate Type="Project" Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
        <RequiredPlatformVersion>8</RequiredPlatformVersion>
    </TemplateData>
    <TemplateContent> </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
