---
title: 'IDebugEngineLaunch2:: LaunchSuspended |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e802c17d0a93aabbe5c6c0a8573abc6a551944ae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730542"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
このメソッドは、デバッグエンジン (DE) を介してプロセスを起動します。

## <a name="syntax"></a>構文

```cpp
HRESULT LaunchSuspended ( 
   LPCOLESTR             pszMachine,
   IDebugPort2*          pPort,
   LPCOLESTR             pszExe,
   LPCOLESTR             pszArgs,
   LPCOLESTR             pszDir,
   BSTR                  bstrEnv,
   LPCOLESTR             pszOptions,
   LAUNCH_FLAGS          dwLaunchFlags,
   DWORD                 hStdInput,
   DWORD                 hStdOutput,
   DWORD                 hStdError,
   IDebugEventCallback2* pCallback,
   IDebugProcess2**      ppDebugProcess
);
```

```csharp
int LaunchSuspended(
   string               pszServer,
   IDebugPort2          pPort,
   string               pszExe,
   string               pszArgs,
   string               pszDir,
   string               bstrEnv,
   string               pszOptions,
   enum_LAUNCH_FLAGS    dwLaunchFlags,
   uint                 hStdInput,
   uint                 hStdOutput,
   uint                 hStdError,
   IDebugEventCallback2 pCallback,
   out IDebugProcess2   ppProcess
);
```

## <a name="parameters"></a>パラメーター
`pszMachine`\
からプロセスを起動するコンピューターの名前。 ローカルコンピューターを指定するには、null 値を使用します。

`pPort`\
からプログラムが実行されるポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイス。

`pszExe`\
から起動する実行可能ファイルの名前。

`pszArgs`\
から実行可能ファイルに渡す引数。 引数がない場合は、null 値を指定できます。

`pszDir`\
から実行可能ファイルによって使用される作業ディレクトリの名前。 作業ディレクトリが不要な場合は、null 値を指定できます。

`bstrEnv`\
からNULL で終わる文字列の環境ブロックの後に、追加の NULL ターミネータが続きます。

`pszOptions`\
から実行可能ファイルのオプションです。

`dwLaunchFlags`\
からセッションの [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md) を指定します。

`hStdInput`\
から代替入力ストリームを処理します。 リダイレクトが不要な場合は0を指定できます。

`hStdOutput`\
から代替出力ストリームへのハンドル。 リダイレクトが不要な場合は0を指定できます。

`hStdError`\
から代替エラー出力ストリームへのハンドル。 リダイレクトが不要な場合は0を指定できます。

`pCallback`\
からデバッガーイベントを受け取る [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`ppDebugProcess`\
入出力起動されたプロセスを表す結果の [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 通常、は、 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] [launchsuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) メソッドを使用してプログラムを起動し、中断されたプログラムにデバッガーをアタッチします。 ただし、デバッグエンジンでプログラムの起動が必要になる状況があります (たとえば、デバッグエンジンがインタープリターの一部であり、デバッグ中のプログラムが解釈された言語である場合など)。この場合は、 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] メソッドを使用し `IDebugEngineLaunch2::LaunchSuspended` ます。

 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)メソッドは、プロセスが中断状態で正常に起動された後にプロセスを開始するために呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
