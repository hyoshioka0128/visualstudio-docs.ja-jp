---
title: CustomParameter 要素 (Visual Studio テンプレート) |Microsoft Docs
description: CustomParameter 要素と、テンプレートからプロジェクトまたは項目を作成するときに使用するカスタムパラメーターの名前と値がどのように含まれているかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameter
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: 743c4489-74ac-403a-bbaa-eed7d785a3ac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61c118bbc85064beb10b99641f0803af7af12d56
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94671950"
---
# <a name="customparameter-element-visual-studio-templates"></a>CustomParameter 要素 (Visual Studio テンプレート)
プロジェクトまたは項目がテンプレートから作成されるときに使用する、カスタムパラメーターの名前と値を格納します。

## <a name="syntax"></a>構文

```
<CustomParameter Name="name" Value="value">
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 パラメーターの名前。 パラメーターの形式は $*name*$ です。|
|`Value`|必須。 パラメーターの置換値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|ウィザードがパラメーター置換を行うときに、テンプレートウィザードに渡すカスタムパラメーターをグループ化します。|

## <a name="remarks"></a>注釈
 テンプレートに要素が含まれている場合 `CustomParameter` 、すべてのインスタンス `Name` は、作成された `Value` プロジェクトまたは項目ファイルの属性で属性を置き換えます。

## <a name="example"></a>例
 次の例は、テンプレートでいくつかのカスタムパラメーターを使用する方法を示しています。 次のカスタムパラメーターを使用してテンプレートからプロジェクトまたは項目が作成されると、テンプレートファイル内のとのすべてのインスタンス `$color1$` が、それぞれとに置き換えられ `$color2$` `Red` `Blue` ます。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>関連項目
- [CustomParameters 要素 (Visual Studio テンプレート)](../extensibility/customparameters-element-visual-studio-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
