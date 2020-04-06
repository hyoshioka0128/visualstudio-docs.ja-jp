---
title: Iデバッグエンジン3::セットシンボルパス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetSymbolPath
helpviewer_keywords:
- IDebugEngine3::SetSymbolPath
ms.assetid: 47b48f84-8a96-401f-84df-0baa8a96d26e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1fbe5128900fa10147c747cbcba4129e96d4c4ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730663"
---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
デバッグ シンボルを検索するパスを設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetSymbolPath (
   LPOLESTR            szSymbolSearchPath,
   LPOLESTR            szSymbolCachePath,
   LOAD_SYMBOLS_FLAGS  Flags
);
```

```csharp
int SetSymbolPath(
   string                    szSymbolSearchPath,
   string                    szSymbolCachePath,
   enum_LOAD_SYMBOLS_FLAGS   Flags
);
```

## <a name="parameters"></a>パラメーター

`szSymbolSearchPath`\
[in]シンボル検索パスを含む文字列。 詳細は「解説」を参照してください。 null にすることはできません。

`szSymbolCachePath`\
[in]シンボルをキャッシュできるローカル パスを含む文字列。 null にすることはできません。

`Flags`\
[in]使用されません。常に 0 に設定されます。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 文字列`szSymbolSearchPath`は、シンボルを検索するための 1 つ以上のパスのリストで、セミコロンで区切られています。 これらのパスには、ローカル パス、UNC 形式のパス、または URL を指定できます。 これらのパスは、異なるタイプの組み合わせにもなります。 パスが UNC (たとえば\Symserver\Symbols) の場合、デバッグ エンジンは、パスがシンボル サーバーへのパスであり、\\そのサーバーからシンボルを読み込むことができるかどうかを判断し、で指定された`szSymbolCachePath`パスにシンボルをキャッシュする必要があります。

 シンボル パスには、1 つ以上のキャッシュの場所を含めることもできます。 キャッシュは、優先順位の最も高いキャッシュを最初に、優先順位の高い順にリストされ、* 記号で区切られます。 次に例を示します。

```
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*https://msdl.microsoft.com
```

 [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)メソッドは、シンボルの実際の読み込みを実行します。

## <a name="see-also"></a>関連項目
- [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
