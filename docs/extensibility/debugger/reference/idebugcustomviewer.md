---
title: カスタムビューアー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c44d2289180ece35725b9258e9d20abeb3a4cac3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732420"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
このインターフェイスを使用すると、式エバリュエーター (EE) は、必要な形式でプロパティの値を表示できます。

## <a name="syntax"></a>構文

```
IDebugCustomViewer : IUknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
EE は、プロパティの値をカスタム形式で表示するために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
COM の`CoCreateInstance`関数の呼び出しは、このインターフェイスをインスタンス化します。 渡`CLSID`された`CoCreateInstance`のはレジストリから取得されます。 [レジストリ](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)内の場所を取得します。 例と同様に詳細については、解説を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|指定された値を表示するために必要な処理を行います。|

## <a name="remarks"></a>Remarks
このインターフェイスは、データ テーブルや他の複合プロパティ型など、通常の方法でプロパティの値を表示できない場合に使用されます。 `IDebugCustomViewer`インターフェイスによって表されるカスタム ビューアーは、EE に関係なく特定の型のデータを表示するための外部プログラムである型ビジュアライザーとは異なります。 EE は、その EE に固有のカスタム ビューアーを実装します。 ユーザーは、ビジュアライザーの種類を選択します。 このプロセスの詳細については[、データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)を参照してください。

カスタム ビューアーは EE と同じ方法で登録されるため、言語 GUID とベンダ GUID が必要です。 正確なメトリック (またはレジストリ エントリ名) は EE に対してのみ認識されます。 このメトリックは[、DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)構造で返され、次に[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)の呼び出しによって返されます。 メトリックに格納される値は、COM`CLSID`の`CoCreateInstance`関数に渡される値です (例を参照)。

[SDK のデバッグ ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)関数`SetEEMetric`を使用して、カスタム ビューアーを登録できます。 カスタム ビューアーで必要な特定の`Debugging SDK Helpers`レジストリ キーについては、「式エバリュエーター」のレジストリ セクションを参照してください。 カスタム ビューアーは 1 つのメトリック (EE の実装者によって定義されます) のみを必要とするのに対し、式エバリュエーターは、いくつかの定義済みのメトリックを必要とします。

通常、カスタム ビューアーは、[表示値](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)に提供される[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスには、文字列以外のプロパティの値を変更するためのメソッドがないため、データの読み取り専用ビューを提供します。 任意のデータ ブロックの変更をサポートするために、EE はインターフェイスを実装する同じオブジェクトにカスタム インターフェイス`IDebugProperty3`を実装します。 このカスタム インターフェイスは、任意のデータ ブロックを変更するために必要なメソッドを提供します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="example"></a>例
この例では、プロパティにカスタム ビューアーがある場合に、プロパティから最初のカスタム ビューアーを取得する方法を示します。

```cpp
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)
{
    // This string is typically defined globally.  For this example, it
    // is defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugCustomViewer *pViewer = NULL;
    if (pProperty != NULL) {
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);
        if (pProperty3 != NULL) {
            HRESULT hr;
            ULONG viewerCount = 0;
            hr = pProperty3->GetCustomViewerCount(&viewerCount);
            if (viewerCount > 0) {
                ULONG viewersFetched = 0;
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };
                hr = pProperty3->GetCustomViewerList(0,
                                                     1,
                                                     &viewerInfo,
                                                     &viewersFetched);
                if (viewersFetched == 1) {
                    CLSID clsidViewer = { 0 };
                    CComPtr<IDebugCustomViewer> spCustomViewer;
                    // Get the viewer's CLSID from the registry.
                    ::GetEEMetric(viewerInfo.guidLang,
                                  viewerInfo.guidVendor,
                                  viewerInfo.bstrMetric,
                                  &clsidViewer,
                                  strRegistrationRoot);
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {
                        // Instantiate the custom viewer.
                        spCustomViewer.CoCreateInstance(clsidViewer);
                        if (spCustomViewer != NULL) {
                            pViewer = spCustomViewer.Detach();
                        }
                    }
                }
            }
        }
    }
    return(pViewer);
}
```

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
