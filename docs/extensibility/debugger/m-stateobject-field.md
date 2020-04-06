---
title: m_stateObjectフィールド |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738374"
---
# <a name="m_stateobject-field"></a>m_stateObjectフィールド
アクションで使用されるデータを表すオブジェクト。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 この内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>Remarks
 これは<xref:System.Threading.Tasks.Task.%23ctor%2A>、コンストラクター`state`のパラメーターです。 また、<xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName>プロパティのバッキング フィールドでもあります。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
