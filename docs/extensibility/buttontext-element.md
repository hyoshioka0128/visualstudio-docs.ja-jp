---
title: ButtonText 要素 |Microsoft Docs
description: ButtonText 要素を使用すると、さまざまなメニューに表示されるテキストを指定できます。 他のテキストフィールドが指定されている場合でも、ButtonText 要素を空白にすることはできません。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4fa9ad6aab9d42113f3e01760e191184e168b62d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068116"
---
# <a name="buttontext-element"></a>ButtonText 要素
このフィールドでは、さまざまなメニューに表示されるテキストを指定できます。 既定では、 `ButtonText` 要素はメニューコントローラーに表示されます。 `ButtonText`他のテキストフィールドが空白の場合も、要素が既定値になります。 `ButtonText`他のテキストフィールドが指定されている場合でも、要素を空白にすることはできません。

## <a name="syntax"></a>構文

```xml
<ButtonText>My Command</ButtonText>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Strings 要素](../extensibility/strings-element.md)|やなどのテキスト要素をグループ化し `ButtonText` `CommandName` ます。|

## <a name="text-value"></a>テキスト値
 要素のテキスト値は、 `ButtonText` テキストを表示するメニュー項目、combos、およびその他のユーザーインターフェイス (UI) の要素に対して表示されるテキストを提供します。

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
