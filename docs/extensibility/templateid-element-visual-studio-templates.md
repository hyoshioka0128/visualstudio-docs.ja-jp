---
title: TemplateID 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateID
helpviewer_keywords:
- <TemplateID> element [Visual Studio Templates]
- TemplateID element [Visual Studio Templates]
ms.assetid: 6ca24b4e-0325-4a9e-855e-0cbbe7361d8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8eb5abac9c837b3022354d6da743ac8f21d5e41d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699064"
---
# <a name="templateid-element-visual-studio-templates"></a>TemplateID 要素 (Visual Studio テンプレート)
[Templategroupid](../extensibility/templategroupid-element-visual-studio-templates.md)要素によって項目テンプレートのグループに分類される項目テンプレートの識別子を指定します。

 \<VSTemplate> \<TemplateData>
 \<TemplateID>

## <a name="syntax"></a>構文

```
<TemplateID> ... </TemplateID>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 `string`要素によって項目テンプレートのグループに分類される項目テンプレートの識別子を表す `TemplateGroupID` 。

## <a name="remarks"></a>解説
 `TemplateID` は省略可能な要素です。

 .Vstemplate ファイルで要素が省略されている場合は、 `TemplateID` [Name](../extensibility/name-element-visual-studio-templates.md) 要素がテンプレートの識別子として使用されます。

 要素の値 `TemplateID` は、プロジェクトシステムの登録 (HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\11.0\projects) と共に使用して \\ 、[ **新しい項目の追加** ] ダイアログボックスに表示されるテンプレートをフィルター処理します。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
