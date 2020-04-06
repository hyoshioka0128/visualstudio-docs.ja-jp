---
title: プログラムプログラム2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2
helpviewer_keywords:
- IDebugProgramPublisher2 interface
ms.assetid: b1d17f63-7146-4076-a588-034cfc6858b9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b17f5bab02e49951eb1647af95641af807c44863
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721525"
---
# <a name="idebugprogrampublisher2"></a>IDebugProgramPublisher2
このインターフェイスを使用すると、デバッグ エンジン (DE) またはカスタム ポート サプライヤーは、デバッグ用のプログラムを登録できます。

## <a name="syntax"></a>構文

```
IDebugProgramPublisher2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
Visual Studio では、デバッグ中のプログラムを登録して、複数のプロセス間でデバッグを行うために、デバッグ中のプログラムを登録するためにこのインターフェイスを実装しています。

## <a name="notes-for-callers"></a>発信者向けのメモ
COM の`CoCreateInstance`関数`CLSID_ProgramPublisher`を呼び出してこのインターフェイスを取得します (例を参照)。 DE またはカスタム ポート サプライヤーは、このインターフェイスを使用して、デバッグ中のプログラムを表すプログラム ノードを登録します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)|DEs とセッション デバッグ マネージャー (SDM) でプログラム ノードを使用できるようにします。|
|[UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)|プログラム ノードを削除して、使用できなくなった状態にします。|
|[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)|プログラムを DEs および SDM で使用できるようにします。|
|[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)|プログラムを削除して、使用できなくなった。|
|[SetDebuggerPresent](../../../extensibility/debugger/reference/idebugprogrampublisher2-setdebuggerpresent.md)|デバッガーが存在することを示すフラグを設定します。|

## <a name="remarks"></a>Remarks
このインターフェイスは、DEs とセッション デバッグ マネージャー (SDM) で使用するために、プログラムとプログラム ノードを利用できるようにします (つまり、それらを"公開" します)。 公開されたプログラムおよびプログラム ノードにアクセスするには[、IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)インターフェイスを使用します。 これは、Visual Studio がプログラムがデバッグ中であることを認識できる唯一の方法です。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="example"></a>例
この例では、プログラムの発行元をインスタンス化し、プログラム ノードを登録する方法を示します。 これは、チュートリアル「[プログラム ノードの公開」から取得します](https://msdn.microsoft.com/library/d0100e02-4e2b-4e72-9e90-f7bc11777bae)。

```cpp
// This is how m_srpProgramPublisher is defined in the class definition:
// CComPtr<IDebugProgramPublisher2> m_srpProgramPublisher.

void CProgram::Start(IDebugEngine2 * pEngine)
{
    m_spEngine = pEngine;

    HRESULT hr = m_srpProgramPublisher.CoCreateInstance(CLSID_ProgramPublisher);
    if ( FAILED(hr) )
    {
        ATLTRACE("Failed to create the program publisher: 0x%x.", hr);
        return;
    }

    // Register ourselves with the program publisher. Note that
    // CProgram implements the IDebgProgramNode2 interface, hence
    // the static cast on "this".
    hr = m_srpProgramPublisher->PublishProgramNode(
        static_cast<IDebugProgramNode2*>(this));
    if ( FAILED(hr) )
    {
        ATLTRACE("Failed to publish the program node: 0x%x.", hr);
        m_srpProgramPublisher.Release();
        return;
    }

    ATLTRACE("Added program node.\n");
}
```

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
