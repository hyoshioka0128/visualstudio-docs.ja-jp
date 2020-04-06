---
title: プログラムプロバイダ2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2
helpviewer_keywords:
- IDebugProgramProvider2 interface
ms.assetid: a9ec7b3e-a59c-4069-b2ee-6f45916eeb78
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 43557e5d81e5140967a1189e57a350595d0f7220
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721697"
---
# <a name="idebugprogramprovider2"></a>IDebugProgramProvider2
この登録済みインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) は[、IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)インターフェイスを通じて "公開" されたプログラムに関する情報を取得できます。

## <a name="syntax"></a>構文

```
IDebugProgramProvider2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
デバッグ エンジン (DE) は、デバッグ中のプログラムに関する情報を提供するには、このインターフェイスを実装します。 このインターフェイスは、レジストリの DE セクションで、メトリック`metricProgramProvider`を使用して登録[されます](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。

## <a name="notes-for-callers"></a>発信者向けのメモ
レジストリから取得した`CoCreateInstance`プログラム プロバイダ`CLSID`の COM 関数を呼び出します。 例を参照してください。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド

|Method|説明|
|------------|-----------------|
|[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)|さまざまな方法でフィルタ処理された、実行中のプログラムに関する情報を取得します。|
|[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)|特定のプロセス ID を指定して、プログラム ノードを取得します。|
|[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)|特定の種類のプロセスに関連付けられたプロバイダー イベントを監視するコールバックを確立します。|
|[SetLocale](../../../extensibility/debugger/reference/idebugprogramprovider2-setlocale.md)|DE で必要な言語固有のリソースのロケールを設定します。|

## <a name="remarks"></a>Remarks
通常、プロセスはこのインタフェースを使用して、そのプロセスで実行されているプログラムを調べる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="example"></a>例

```cpp
IDebugProgramProvider2 *GetProgramProvider(GUID *pDebugEngineGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugProgramProvider2 *pProvider = NULL;
    if (pDebugEngineGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetMetric(NULL,
                    metrictypeEngine,
                    *pDebugEngineGuid,
                    metricProgramProvider,
                    &clsidProvider,
                    strRegistrationRoot);
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugProgramProvider2> spProgramProvider;
            spProgramProvider.CoCreateInstance(clsidProvider);
            if (spProgramProvider != NULL) {
                pProvider = spProgramProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
