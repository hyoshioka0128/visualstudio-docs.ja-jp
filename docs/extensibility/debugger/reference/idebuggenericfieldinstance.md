---
description: マネージコードのジェネリック型のフィールドのインスタンスを表します。
title: IDebugGenericFieldInstance |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldInstance interface
ms.assetid: f68b4761-be8b-4801-9d4b-cde90e01d95e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf87999768ae12b9ae10702bc0e8ae8efe16e000
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072755"
---
# <a name="idebuggenericfieldinstance"></a>IDebugGenericFieldInstance
マネージコードのジェネリック型のフィールドのインスタンスを表します。

## <a name="syntax"></a>Syntax

```
IDebugGenericFieldInstance : IUnknown
```

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebuggenericfieldinstance-gettypearguments.md)|このインスタンスの型パラメーターの引数を取得します。|
|[TypeArgumentCount](../../../extensibility/debugger/reference/idebuggenericfieldinstance-typeargumentcount.md)|このインスタンスの型パラメーター引数の数を返します。|

## <a name="requirements"></a>要件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
