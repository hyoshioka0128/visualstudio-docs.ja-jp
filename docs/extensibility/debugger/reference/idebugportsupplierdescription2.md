---
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
ms.openlocfilehash: 3db59d4938911d0c47f0122a8727be8f1c8acd67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99840198"
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

|Method|説明|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|ポートサプライヤーの説明と説明のメタデータを取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
