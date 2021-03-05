---
description: DCOM を使用して、ファイアウォールがリモートデバッグをブロックしないようにするために、デバッグエンジンが Visual Studio UI に要求できるようにします。
title: IDebugFirewallConfigurationCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFirewallConfigurationCallback2 interface
ms.assetid: 0827361c-b97c-4851-9898-ab6d88c81811
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf8659a1bc4af55a9809a3c85548b971a7193b26
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166529"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
DCOM を使用して、 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ファイアウォールがリモートデバッグをブロックしないように UI に要求するデバッグエンジンを有効にします。

## <a name="syntax"></a>構文

```
IDebugFirewallConfigurationCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 セッションデバッグマネージャーのポートオブジェクトによって実装されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugFirewallConfigurationCallback2` ます。

|メソッド|説明|
|------------|-----------------|
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|ファイアウォールがリモートデバッグをブロックしないように要求します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
