---
title: 'IDebugBreakpointChecksumRequest2:: GetChecksum |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2::GetChecksum
ms.assetid: ec434882-e5c0-4d76-a58b-22c260d8626e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6fe1d2828f15b295f42c7fd756f2ffc407a632c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80735175"
---
# <a name="idebugbreakpointchecksumrequest2getchecksum"></a>IDebugBreakpointChecksumRequest2::GetChecksum
使用するチェックサムアルゴリズムの一意の識別子を指定して、ブレークポイント要求のドキュメントチェックサムを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetChecksum(
    REFGUID        guidAlgorithm,
    CHECKSUM_DATA *pChecksumData
);
```

```csharp
public int GetChecksum(
    ref Guid               guidAlgorithm,
    out enum_CHECKSUM_DATA pChecksumData
);
```

## <a name="parameters"></a>パラメーター
`guidAlgorithm`\
からチェックサムアルゴリズムの一意識別子。

`pChecksumData`\
入出力ブレークポイント要求のドキュメントチェックサム。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="example"></a>例
次の例は、バインドされるドキュメントのチェックサムが UI と一致するかどうかをチェックする関数を示しています。

```cpp
bool CDebugProgram::DoChecksumsMatch(CDebugPendingBreakpoint *pPending, CDebugCodeContext *pContext)
{
    bool fRet = false;
    HRESULT hRes;

    // Get the checksum for the document we are about to bind to from the pdb side
    GUID guidAlgorithmId;
    BYTE *pChecksum = NULL;
    ULONG cNumBytes = 0;

    hRes = pContext->GetDocumentChecksumAndAlgorithmId(&guidAlgorithmId, &pChecksum, &cNumBytes);

    if ( S_OK == hRes )
    {
        // Get checksum data for the document from the UI (request) side
        CComPtr<IDebugBreakpointChecksumRequest2> pChecksumRequest;

        hRes = pPending->GetChecksumRequest(&pChecksumRequest);

        if ( S_OK == hRes )
        {
            CHECKSUM_DATA data;

            hRes = pChecksumRequest->GetChecksum(guidAlgorithmId, &data);

            if ( S_OK == hRes )
            {
                if ( data.ByteCount == cNumBytes && memcmp(data.pBytes, pChecksum, cNumBytes) == 0 )
                    fRet = true;
                else
                    fRet = false;

                // Free up data allocated for checksum data
                CoTaskMemFree(data.pBytes);
            }
            else
                fRet = true; // checksums not available - user disabed checksums
        }
        else
            fRet = true; // we couldn't get checksum from UI - default to past behavior

        // free up space allocated for checksum from pdb
        CoTaskMemFree(pChecksum);
    }
    else
        fRet = true; // we don't have a checksum to compare with.

    return ( fRet );
}
```

## <a name="see-also"></a>関連項目
- [IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)
