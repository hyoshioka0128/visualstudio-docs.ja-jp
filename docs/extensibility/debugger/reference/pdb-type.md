---
title: PDB_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PDB_TYPE
helpviewer_keywords:
- PDB_TYPE structure
ms.assetid: 1c1bb772-77d6-4870-90b2-fd9247d0004e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df6a41801f4cce272d896776745ac0cc507d0e38
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890020"
---
# <a name="pdb_type"></a>PDB_TYPE

この構造体は、PDB シンボルから取得されたフィールド型に関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTYPE_PDB {
    ULONG32 ulAppDomainID;
    GUID    guidModule;
    DWORD   symid;
} PDB_TYPE;
```

```csharp
public struct PDB_TYPE {
    public uint ulAppDomainID;
    public Guid guidModule;
    public uint symid;
};
```

## <a name="members"></a>メンバー

`ulAppDomainID`\
シンボルの取得元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

`guidModule`\
このフィールドを含むモジュールの GUID。

`symid`\
このフィールドに対応するシンボルの ID。

## <a name="remarks"></a>解説

この構造体は、構造体のフィールドがに設定されている場合に、 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体の共用体の一部として表示され `dwKind` `TYPE_INFO` `TYPE_KIND_PDB` ます ( [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値)。

## <a name="requirements"></a>要件

ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
