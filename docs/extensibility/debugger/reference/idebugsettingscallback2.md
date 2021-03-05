---
description: デバッグエンジンがメトリック設定をリモートで読み取ることができるようにします。
title: IDebugSettingsCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7053c45ba86f4bea54befc3bde67d831cc9c822e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168661"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
デバッグエンジンがメトリック設定をリモートで読み取ることができるようにします。

## <a name="syntax"></a>構文

```
IDebugSettingsCallback2D : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
このインターフェイスは、セッションデバッグマネージャーのイベントコールバックによって実装され、デバッグエンジンによって使用されます。 また、Dbgmetric [d] .lib ではなくローカルで使用することもできます。

## <a name="methods"></a>メソッド
次の表に、のメソッドを示し `IDebugSettingsCallback2` ます。

|メソッド|説明|
|------------|-----------------|
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|言語およびベンダー識別子を指定して、使用可能な式エバリュエーターを列挙します。|
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|メトリックを指定して、式エバリュエーターローカルオブジェクトを取得します。|
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|指定した式エバリュエーターのメトリックに対応する値を取得します。|
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|名前またはメトリックを指定して、式エバリュエーターのメトリックファイルを取得します。|
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|名前を指定して、式エバリュエーターメトリックの一意の識別子を取得します。|
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|名前を指定して、式エバリュエーターのメトリックの値の文字列を取得します。|
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|名前を指定して、メトリックの値を取得します。|
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|名前を指定して、メトリックの一意の識別子を取得します。|
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|名前を指定して、メトリックの値の文字列を取得します。|

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
次の例は、パラメーターとして **IDebugSettingsCallback2** オブジェクトを受け取る関数を示しています。

```cpp
HRESULT GetDebugSettingsCallback (IDebugSettingsCallback2 **ppCallback)
{
    HRESULT hRes = E_FAIL;

    if ( ppCallback )
    {
        if ( EVAL(m_pdec) )
            hRes = m_pdec->QueryInterface(IID_IDebugSettingsCallback2, (void **)ppCallback);
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```
