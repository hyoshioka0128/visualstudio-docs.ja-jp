---
description: 対象のコンピュータに関する情報のクエリを実行できるようにします。
title: IDebugWindowsComputerPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a9c7e940c2284b5b39097226f9a5b0c3b34a0d18
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222953"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
対象のコンピュータに関する情報のクエリを実行できるようにします。

## <a name="syntax"></a>構文

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、セッションデバッグマネージャーのポートオブジェクトによって実装されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugWindowsComputerPort2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|デバッガーが実行されているコンピューターに関する情報を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
