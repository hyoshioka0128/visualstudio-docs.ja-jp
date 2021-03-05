---
description: プロジェクト テンプレートが正しく動作するために必要なオペレーティング システムの最小バージョンを指定します。
title: RequiredPlatformVersion 要素 (Visual Studio テンプレート)
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 6f0e4986-3157-4bba-aed3-c28413ebe976
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5f281e51bd07c76d63bc0247d9d7f62fe0390283
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221783"
---
# <a name="requiredplatformversion-element-visual-studio-templates"></a>RequiredPlatformVersion 要素 (Visual Studio テンプレート)

プロジェクト テンプレートが正しく動作するために必要なオペレーティング システムの最小バージョンを指定します。 この要素は [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリを作成するプロジェクト テンプレートに使用されます。

 `RequiredPlatformVersion` の値は、オペレーティング システムのバージョンと直接比較されます。 `RequiredPlatformVersion`がオペレーティングシステムのバージョンよりも大きい場合、テンプレートは [**新しいプロジェクト**] ダイアログボックスに表示されません。 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 以上のテンプレートを指定するには、`RequiredPlatformVersion` を 6.2.0 に設定します。 以上のテンプレートを指定するに [!INCLUDE[win81](../debugger/includes/win81_md.md)] は、を `RequiredPlatformVersion` 6.3.0 に設定します。

 `RequiredPlatformVersion`=8 を指定できるテンプレートは、顧客の以前の [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] テンプレートと互換性があります。

 .Vstemplate TemplateData....TargetPlatformName RequiredPlatformVersion

## <a name="syntax"></a>構文

```xml
<RequiredPlatformVersion> OperatingSystem </RequiredPlatformVersion>
```

## <a name="attributes-and-elements"></a>属性と要素

 [なし] :

### <a name="attributes"></a>属性

 なし。

### <a name="child-elements"></a>子要素

 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplatePlatformName](../extensibility/templatedata-element-visual-studio-templates.md)|プロジェクト テンプレートの対象となるプラットフォームを指定します。|

## <a name="text-value"></a>テキスト値

 テキスト値が必要です。

## <a name="remarks"></a>解説

 このテキストは、テンプレートで必要なオペレーティング システムの最小バージョンを指定します。

## <a name="example"></a>例

 次の例では、プロジェクト テンプレートで [!INCLUDE[win8](../debugger/includes/win8_md.md)] 以降が対象となるように指定しています。

```xml
<VSTemplate Type="Project" Version="3.0.0"    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
            <RequiredPlatformVersion>6.3.0</RequiredPlatformVersion>

    </TemplateData>
    <TemplateContent>

    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目

- [TargetPlatformName 要素 (Visual Studio テンプレート)](../extensibility/targetplatformname-element-visual-studio-templates.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
