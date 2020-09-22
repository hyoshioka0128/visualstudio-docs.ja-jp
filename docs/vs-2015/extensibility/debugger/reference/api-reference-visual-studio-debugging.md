---
title: API リファレンス (Visual Studio デバッグ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], API reference
ms.assetid: e4e429da-3667-41f7-9158-a8207d13e91a
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f3e95200cf29c8561798c858635c3864d635fb40
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841589"
---
# <a name="api-reference-visual-studio-debugging"></a>API 参照 (Visual Studio のデバッグ)
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このリファレンスセクションでは、API の概念の概要、すべての API 要素の構文と使用法、および一連のコード例を紹介するガイドを紹介します。 すべての参照は、カテゴリ別にアルファベット順に一覧表示されます。  
  
 次の表は、 `HRESULT` メソッドによって返される共通の値を示しています。  
  
|Name|説明|値|  
|----------|-----------------|-----------|  
|S_OK|成功しました。|0x00000000|  
|E_UNEXPECTED|予期しないエラーです。|0x8000FFFF|  
|E_NOTIMPL|実装されていません。|0x80004001|  
|E_OUTOFMEMORY|操作を完了するために必要なメモリが不足しています。|0x8007000E|  
|E_INVALIDARG|1 つ以上の引数が無効です。|0x80070057|  
|E_NOINTERFACE|そのようなインターフェイスはサポートされていません。|0x80004002|  
|E_POINTER|ポインターが無効です。|0x80004003|  
|E_HANDLE|ハンドルが無効です。|0x80070006|  
|E_ABORT|操作は中止されました。|0x80004004|  
|E_FAIL|予期しないエラーです。|0x80004005|  
|E_ACCESSDENIED|一般アクセス拒否エラーです。|0x80070005|  
  
> [!NOTE]
> デバッグメソッドから制御が戻ったときに、すべての out パラメーターポインターが有効であることを前提としてい [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] `S_OK` ます。つまり、が返されたときに、パラメーターポインターに対して検証は実行されません `S_OK` 。  
  
> [!NOTE]
> 無効または `NULL` [out] パラメーターがあると、IDE がクラッシュする可能性があります。  
  
## <a name="see-also"></a>参照  
 [インターフェイス](../../../extensibility/debugger/reference/interfaces-visual-studio-debugging.md)   
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [Visual Studio デバッガーの拡張性](../../../extensibility/debugger/visual-studio-debugger-extensibility.md)
