---
description: METADATA_TYPE 構造体は、メタデータから取得したフィールド型に関する情報を指定します。
title: METADATA_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5a76e051e146985338564d497323b6232b35a4a1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079853"
---
# <a name="metadata_type"></a>METADATA_TYPE
この構造体は、メタデータから取得されたフィールド型に関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTYPE_METADATA {
   ULONG32  ulAppDomainID;
   GUID     guidModule;
   _mdToken tokClass;
} METADATA_TYPE;
```

```csharp
public struct METADATA_TYPE {
   public uint ulAppDomainID;
   public Guid guidModule;
   public int  tokClass;
};
```

## <a name="parameters"></a>パラメーター
 `ulAppDomainID`\
 シンボルの取得元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

 `guidModule`\
 このフィールドを含むモジュールの GUID。

 `tokClass`\
 この型のメタデータトークン ID。

 [C++] `_mdToken` は、 `typedef` 32 ビットのです `int` 。

## <a name="remarks"></a>注釈
 この構造体は、構造体のフィールドがに設定されている場合に、 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体の共用体の一部として表示され `dwKind` `TYPE_INFO` `TYPE_KIND_METADATA` ます ( [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値)。

 `tokClass`値は、型を一意に識別するメタデータトークンです。 メタデータトークン ID の上位ビットを解釈する方法の詳細については、 `CorTokenType` .NET FRAMEWORK SDK の corhdr .h ファイルの列挙体を参照してください。

## <a name="requirements"></a>要件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
