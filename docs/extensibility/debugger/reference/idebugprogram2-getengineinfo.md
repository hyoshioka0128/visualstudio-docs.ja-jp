---
title: 'IDebugProgram2:: GetEngineInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetEngineInfo
helpviewer_keywords:
- IDebugProgram2::GetEngineInfo
ms.assetid: 3a4f2dc0-e082-4d8d-aeaf-463ab09d279b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b26d6dcde31d3599c8aa8f8223c1f3cf00a59437
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906255"
---
# <a name="idebugprogram2getengineinfo"></a>IDebugProgram2::GetEngineInfo
このプログラムを実行しているデバッグエンジン (DE) の名前と GUID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEngineInfo( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo( 
   out string pbstrEngine,
   out GUID   pguidEngine
);
```

## <a name="parameters"></a>パラメーター
`pbstrEngine`\
入出力このプログラムを実行している DE の名前を返します。

`pguidEngine`\
入出力このプログラムを実行している DE の GUID を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 各 DE は、id の固有の GUID を定義します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
