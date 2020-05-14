---
title: テンプレート グループ ID 要素 ( ビジュアル スタジオ テンプレート ) |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: affc324418e3745f85fb0b91a0ef7abda0ab28b0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699079"
---
# <a name="templategroupid-element-visual-studio-templates"></a>TemplateGroupID 要素 (Visual Studio テンプレート)
項目テンプレートを表示するプロジェクトの種類を指定します。 この要素は、[表示によって既定 (Visual Studio テンプレート)](../extensibility/showbydefault-visual-studio-templates.md) `false`が に設定されている場合に重要です。 [ShowByDefault (Visual Studio テンプレート)](../extensibility/showbydefault-visual-studio-templates.md) `true`が に設定されている場合、項目テンプレートはすべてのプロジェクトの種類で使用できます。

 \<テンプレート>\<テンプレート\<データ> テンプレート グループ ID>

## <a name="syntax"></a>構文

```
<TemplateGroupID> ... </TemplateGroupID>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、項目テンプレートのカテゴリの識別子を指定します。

## <a name="remarks"></a>Remarks
 `TemplateGroupID` は要素です。

 `TemplateGroupID`要素の値は、プロジェクト システム登録 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<バージョン番号>* \Projects)\\と共に使用され、[**新しい項目の追加**] ダイアログ ボックスに表示されるテンプレートをフィルター処理します。

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
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
