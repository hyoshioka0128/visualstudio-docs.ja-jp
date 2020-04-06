---
title: テンプレート ID 要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699064"
---
# <a name="templateid-element-visual-studio-templates"></a>TemplateID 要素 (Visual Studio テンプレート)
[TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md)要素によって項目テンプレートのグループに分類される項目テンプレートの識別子を指定します。

 \<テンプレート>\<テンプレート\<データ> テンプレート ID>

## <a name="syntax"></a>構文

```
<TemplateID> ... </TemplateID>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 要素`string`によって項目テンプレートのグループに分類される項目テンプレートの識別子を表す`TemplateGroupID`A。

## <a name="remarks"></a>Remarks
 `TemplateID` は省略可能な要素です。

 .vstemplate ファイルで要素を省略`TemplateID`した場合[、Name](../extensibility/name-element-visual-studio-templates.md)要素がテンプレートの識別子として使用されます。

 要素の値は、プロジェクト システム登録 (HKEY_LOCAL_MACHINE\SOFTWARE\VisualStudio\11.0\Projects)\\と共に使用され、[**新しい項目の追加**] ダイアログ ボックスに表示されるテンプレートをフィルター処理します。 `TemplateID`

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
