---
title: コールバック2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2c85b54f92970dca5d712b827019300f850b03cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719946"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
デバッグ エンジンがメトリック設定をリモートで読み取ることを可能にします。

## <a name="syntax"></a>構文

```
IDebugSettingsCallback2D : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
このインターフェイスは、セッション デバッグ マネージャーのイベント コールバックによって実装され、デバッグ エンジンによって使用されます。 また、Dbgmetric[d].lib の代わりにローカルで使用することもできます。

## <a name="methods"></a>メソッド
次の表に`IDebugSettingsCallback2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|言語とベンダ識別子を指定して、使用可能な式エバリュエーターを列挙します。|
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|メトリックを指定して、式エバリュエーターのローカル オブジェクトを取得します。|
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|式エバリュエーターの指定されたメトリックに対応する値を取得します。|
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|名前またはメトリックを指定して、式エバリュエーター メトリック ファイルを取得します。|
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|指定された式エバリュエーター メトリックの一意の識別子を取得します。|
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|指定された式エバリュエーター メトリックの値文字列を取得します。|
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|指定された名前のメトリックの値を取得します。|
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|指定された名前のメトリックの一意の識別子を取得します。|
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|指定された名前のメトリックの値文字列を取得します。|

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="example"></a>例
次の例は、パラメーターとして**IDebugSettingsCallback2**オブジェクトを受け取る関数を示しています。

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
