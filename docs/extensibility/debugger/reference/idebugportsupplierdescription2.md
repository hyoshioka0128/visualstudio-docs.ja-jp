---
description: '[プロセスにアタッチ] ダイアログボックスの [トランスポート情報] セクション内にテキストを表示する Visual Studio UI を有効にします。'
title: IDebugPortSupplierDescription2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c3cd8d6fbeaf020ea772c9bd5cae783b6e8d127
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150381"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)][**プロセスにアタッチ**] ダイアログボックスの [**トランスポート情報**] セクション内のテキストを UI で表示できるようにします。

## <a name="syntax"></a>構文

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、ポートサプライヤーによって実装されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugPortSupplierDescription2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|ポートサプライヤーの説明と説明のメタデータを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
