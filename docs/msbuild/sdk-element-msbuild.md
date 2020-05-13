---
title: Sdk 要素 (MSBuild) | Microsoft Docs
ms.date: 01/25/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Project
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Sdk element [MSBuild]
- <Sdk> element [MSBuild]
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a704744032c5dea70246463a816ba8e1f5c84e8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632473"
---
# <a name="sdk-element-msbuild"></a>Sdk 要素 (MSBuild)

MSBuild プロジェクト SDK が参照されます。

 \<Project> \<Sdk>

## <a name="syntax"></a>構文

```xml
<Sdk Name="My.Custom.Sdk"
     Version="1.0.0" />
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須の属性です。<br /><br /> プロジェクト SDK の名前です。|
|`Version`|省略可能な属性です。<br /><br /> プロジェクト SDK のバージョンです。|

### <a name="child-elements"></a>子要素

 なし。

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |

## <a name="see-also"></a>関連項目

- [方法: MSBuild プロジェクト SDK の参照](../msbuild/how-to-use-project-sdk.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [MSBuild](../msbuild/msbuild.md)
