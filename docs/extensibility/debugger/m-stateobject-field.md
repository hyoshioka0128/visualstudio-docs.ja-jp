---
title: m_stateObject Field |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fed70f2eda19ad96454a83217c20c046809f3034
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738374"
---
# <a name="m_stateobject-field"></a>m_stateObject フィールド
アクションが使用するデータを表すオブジェクト。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>解説
 これは、 `state` コンストラクターのパラメーターです <xref:System.Threading.Tasks.Task.%23ctor%2A> 。 これは、プロパティのバッキングフィールドでも <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> あります。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
