---
title: TEXT_DOC_ATTR_2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TEXT_DOC_ATTR_2
helpviewer_keywords:
- TEXT_DOC_ATTR_2 enumeration
ms.assetid: 2333b33b-042b-4ac6-9ebe-e66f95f52f51
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afbb7d7f4525050e73dafaed906dbc504cc8b52e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713452"
---
# <a name="text_doc_attr_2"></a>TEXT_DOC_ATTR_2
ドキュメントの属性を記述します。

## <a name="syntax"></a>構文

```cpp
typedef DWORD TEXT_DOC_ATTR_2;
const TEXT_DOC_ATTR_2 TEXT_DOC_ATTR_READONLY_2 = 0x00000001;
```

```csharp
public const uint TEXT_DOC_ATTR_READONLY_2 = 0x00000001;
```

## <a name="members"></a>メンバー
 `TEXT_DOC_ATTR_READONLY_2`\
 ドキュメントが読み取り専用であることを示します。

## <a name="remarks"></a>Remarks

> [!NOTE]
> この値は、実際には C# のアセンブリで定義されていません。 代わりに、定義をソース ファイルにコピーする必要があります。

 [メソッドに](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)引数として渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)
