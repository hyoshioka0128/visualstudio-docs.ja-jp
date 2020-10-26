---
title: IDebugWindowsComputerPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ef4162469651e4b69502d3a9639d1e86c62e0b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718229"
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
