---
title: Icon 要素 |Microsoft Docs
description: Icon 要素について説明します。これは、Visual Studio IDE 拡張機能で使用されるアイコンを表します。これには、使用されるビットマップの属性やビットマップストリップのスロットが含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Icon
- Icon element (VSCT XML schema)
ms.assetid: 73c58fe3-d53c-4f4e-b025-29567c6cbb7c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c4e68889ae6ea8396795137243cf732a9b028931
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99883273"
---
# <a name="icon-element"></a>Icon 要素
Icon タグの guid 属性は、定義されているビットマップの guid です。 属性は、 `id` ビットマップストリップ内のスロットを選択します。 この要素は省略可能です。 この要素が含まれていない場合、 **guidOfficeIcon: msotcidNoIcon** の値は暗黙的に指定されます。

## <a name="syntax"></a>構文

```xml
<Icon guid="guidImages" id="bmpPic1" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 定義されたビットマップの guid。|
|id|必須。 ビットマップストリップ内のスロットを選択します。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|[なし] :|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Buttons 要素](../extensibility/buttons-element.md)||

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
