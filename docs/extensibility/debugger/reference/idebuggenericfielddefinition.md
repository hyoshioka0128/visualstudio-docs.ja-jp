---
description: マネージコードのジェネリック型のフィールドの定義を表します。
title: IDebugGenericFieldDefinition |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldDefinition interface
ms.assetid: b5a853b7-221e-4d62-8948-07423089d75d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0c9b2a4b9dbdbf5d1b5faefb8dfbf498f873ec01
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063358"
---
# <a name="idebuggenericfielddefinition"></a>IDebugGenericFieldDefinition
マネージコードのジェネリック型のフィールドの定義を表します。

## <a name="syntax"></a>Syntax

```
IDebugGenericFieldDefinition : IUnknown
```

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[ConstructInstantiation](../../../extensibility/debugger/reference/idebuggenericfielddefinition-constructinstantiation.md)|型引数の配列を指定して、フィールドインスタンスを構築します。|
|[GetFormalTypeParams](../../../extensibility/debugger/reference/idebuggenericfielddefinition-getformaltypeparams.md)|パラメーターの数を指定して、型パラメーターを取得します。|
|[TypeParamCount](../../../extensibility/debugger/reference/idebuggenericfielddefinition-typeparamcount.md)|ジェネリックフィールドに関連付けられている型パラメーターの数を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
