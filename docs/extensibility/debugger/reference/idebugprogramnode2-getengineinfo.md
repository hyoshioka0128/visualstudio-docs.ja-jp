---
title: 'IDebugProgramNode2:: GetEngineInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetEngineInfo
helpviewer_keywords:
- IDebugProgramNode2::GetEngineInfo
ms.assetid: 664e7fe5-9100-4b7d-9dc5-e5a4dd0d0451
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b337d9c6742c1c3b0379a757761955151cc6dc6c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898652"
---
# <a name="idebugprogramnode2getengineinfo"></a>IDebugProgramNode2::GetEngineInfo
プログラムを実行しているデバッグエンジン (DE) の名前と識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEngineInfo ( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo(
   out string pbstrEngine,
   out Guid pguidEngine
);
```

## <a name="parameters"></a>パラメーター
`pbstrEngine`\
入出力プログラムを実行している DE の名前を返します (C++ 固有: 呼び出し元がエンジンの名前を必要としないことを示す null ポインターを指定できます)。

`pguidEngine`\
入出力プログラムの実行を解除するグローバル一意識別子を返します (C++ 固有: 呼び出し元がエンジンの GUID に関係しないことを示す null ポインターにすることができます)。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
