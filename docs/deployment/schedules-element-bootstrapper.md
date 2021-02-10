---
title: '&lt;スケジュール &gt; 要素 (ブートストラップ) |Microsoft Docs'
description: Schedule 要素には、Command 要素で定義されたコマンドを実行する特定の時刻を定義する Schedule 要素が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Schedules> element [bootstrapper]
ms.assetid: 28d094cf-64f5-42b1-bd8a-3697082aab4f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0154816985076373c3ced4981aa714971a9ded29
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949650"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;スケジュール &gt; 要素 (ブートストラップ)
要素には、要素 `Schedules` `Schedule` によって定義されたコマンドを実行する特定の時刻を定義する要素が含まれ `Command` ます。

## <a name="syntax"></a>構文

```xml
<Schedules>
    <Schedule
        Name
    >
        <BuildList />
        <BeforePackage />
        <AfterPackage />
    </Schedule>
</Schedules>
```

## <a name="elements-and-attributes"></a>要素と属性
 要素は `Schedules` 要素の子です `Product` 。 各 `Product` 要素は、最大で1つの要素を持つことができ `Schedules` ます。 `Schedules` 要素に属性はありません。

## <a name="schedule"></a>スケジュール
 要素は `Schedule` 要素の子です `Schedules` 。 要素には、 `Schedules` 少なくとも1つの要素が必要 `Schedule` です。

 `Schedule` には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 スケジュール項目の名前。 これは `ScheduleName` 、要素のプロパティに対応 `Command` します。 は、指定されたスケジュールを参照するときに、 `Command` その要素によって示される時刻にのみ実行され `Schedule` ます。 スケジュールは、および要素に関連付けられている場合もあり `FailIf` `BypassIf` ます。これにより、指定したスケジュールでこれらの条件テストを実行することが制限されます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|

 指定された `Schedule` 要素は、次の子のうち1つだけを持つことができます。

## <a name="buildlist"></a>BuildList
 要素は、 `BuildList` ブートストラップアプリケーションが開始された直後にコマンドを実行するようにインストーラーに指示します。

## <a name="beforepackage"></a>BeforePackage
 要素は、 `BeforePackage` 指定されたパッケージがインストールされる前にコマンドを実行するようにインストーラーに指示します。

## <a name="afterpackage"></a>AfterPackage
 要素は、 `AfterPackage` 指定されたパッケージのインストール後にコマンドを実行するようにインストーラーに指示します。

## <a name="see-also"></a>関連項目
- [\<Product> 要素](../deployment/product-element-bootstrapper.md)
- [製品およびパッケージスキーマリファレンス](../deployment/product-and-package-schema-reference.md)