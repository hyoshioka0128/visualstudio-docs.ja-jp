---
title: カスタムパラメーター要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
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
ms.openlocfilehash: 9063a354f03b896e189566e8d84a18caf7509db8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739431"
---
# <a name="customparameter-element-visual-studio-templates"></a>要素
テンプレートからプロジェクトまたは項目を作成するときに使用するカスタム パラメーター名と値を格納します。

## <a name="syntax"></a>構文

```
<CustomParameter Name="name" Value="value">
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 パラメーターの名前。 パラメータの形式は$*name*$です。|
|`Value`|必須。 パラメーターの置換値。|

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|ウィザードでパラメーターを置換するときにテンプレート ウィザードに渡されるカスタム パラメータをグループ化します。|

## <a name="remarks"></a>Remarks
 テンプレートに要素が`CustomParameter`含まれる場合、属性`Name`はすべてのインスタンスに置き`Value`換えられ、作成されたプロジェクトまたは項目ファイルの属性に置き換えられます。

## <a name="example"></a>例
 テンプレートで複数のカスタム パラメータを使用する方法を次の例に示します。 次のカスタム パラメータを使用してテンプレートからプロジェクトまたは項目を作成すると、テンプレート ファイル`$color1$`のすべての`$color2$`インスタンスが、`Red`および`Blue`で置き換えられます。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>関連項目
- [要素](../extensibility/customparameters-element-visual-studio-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
