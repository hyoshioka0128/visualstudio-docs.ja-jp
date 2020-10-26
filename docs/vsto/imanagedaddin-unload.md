---
title: IManagedAddin::Unload
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Unload method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1ec01ebc32472e315fe2c905ecfd2cfef0f4bbe1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85541012"
---
# <a name="imanagedaddinunload"></a>IManagedAddin::Unload
  管理対象の VSTO アドインがアンロードされる直前に呼び出されます。

## <a name="syntax"></a>構文

```csharp
HRESULT Unload();
```

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>解説
 このメソッドは、Microsoft Office の現在のバージョンでは呼び出されません。 このメソッドは将来使用するために予約されています。

## <a name="see-also"></a>関連項目
- [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Load](../vsto/imanagedaddin-load.md)
