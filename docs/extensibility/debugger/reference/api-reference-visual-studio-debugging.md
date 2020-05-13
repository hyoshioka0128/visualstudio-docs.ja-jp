---
title: API リファレンス (Visual Studio のデバッグ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], API reference
ms.assetid: e4e429da-3667-41f7-9158-a8207d13e91a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a2df6d82099a927664620e19096107f283afada
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738175"
---
# <a name="api-reference-visual-studio-debugging"></a>API 参照 (Visual Studio のデバッグ)
リファレンスセクションには、API の概念的概要、すべての API 要素の構文と使用方法を示すガイド、およびコード例の各種が含まれています。 すべての参照は、カテゴリのアルファベット順に一覧表示されます。

 次の表は、メソッド`HRESULT`によって返される一般的な値を示しています。

|名前|説明|値|
|----------|-----------------|-----------|
|S_OK|正常終了しました。|0x00000000|
|E_UNEXPECTED|予期しないエラーです。|0x8000FFFF|
|E_NOTIMPL|実装されていません。|0x80004001|
|E_OUTOFMEMORY|メモリ不足で操作を完了できません。|0x8007000E|
|E_INVALIDARG|1 つ以上の引数が無効です。|0x80070057|
|E_NOINTERFACE|そのようなインターフェイスはサポートされていません。|0x80004002|
|E_POINTER|無効なポインタです。|0x80004003|
|E_HANDLE|ハンドルが無効です。|0x80070006|
|E_ABORT|操作は中止されました。|0x80004004|
|E_FAIL|予期しないエラーです。|0x80004005|
|E_ACCESSDENIED|一般的なアクセス拒否エラー。|0x80070005|

> [!NOTE]
> [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]デバッグ メソッドが戻`S_OK`るとき、すべての out パラメーター ポインターが有効であると見なされます。 `S_OK`
>
> [!NOTE]
> 無効または`NULL`[out] パラメータにより IDE がクラッシュする可能性があります。

## <a name="see-also"></a>関連項目
- [インターフェイス](../../../extensibility/debugger/reference/interfaces-visual-studio-debugging.md)
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [Visual Studio デバッガーの拡張性](../../../extensibility/debugger/visual-studio-debugger-extensibility.md)
