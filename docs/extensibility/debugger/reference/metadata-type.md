---
title: METADATA_TYPE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afe5ea128775c7be0e48035ab4c7e7d370c9d233
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714281"
---
# <a name="metadata_type"></a>METADATA_TYPE
この構造体は、メタデータから取得したフィールド型に関する情報を指定します。

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
 シンボルの元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

 `guidModule`\
 このフィールドを含むモジュールの GUID。

 `tokClass`\
 この型のメタデータ トークン ID。

 [C++]`_mdToken`は`typedef`32 ビット`int`用です。

## <a name="remarks"></a>Remarks
 この構造体は、構造体`dwKind`のフィールドが[(dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)列挙体の値)`TYPE_INFO`に`TYPE_KIND_METADATA`設定されている場合[、TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)構造体の共用体の一部として表示されます。

 値`tokClass`は、型を一意に識別するメタデータ トークンです。 メタデータ トークン ID の上位ビットを解釈する方法の詳細については、.NET Framework SDK の corhdr.h ファイルの`CorTokenType`列挙を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
