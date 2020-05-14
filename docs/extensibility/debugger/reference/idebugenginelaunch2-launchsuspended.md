---
title: IDebugエンジンの打ち上げ2::起動中断 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730542"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
このメソッドは、デバッグ エンジン (DE) を使用してプロセスを起動します。

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
[in]プロセスを起動するマシンの名前。 ローカル マシンを指定するには、NULL 値を使用します。

`pPort`\
[in]プログラムが実行されるポートを表す[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイス。

`pszExe`\
[in]起動する実行可能ファイルの名前。

`pszArgs`\
[in]実行可能ファイルに渡す引数。 引数がない場合は、null 値になることがあります。

`pszDir`\
[in]実行可能ファイルで使用される作業ディレクトリの名前。 作業ディレクトリが不要な場合は、NULL 値になることがあります。

`bstrEnv`\
[in]NULL で終わる文字列の環境ブロック、続いて追加の NULL 終端文字。

`pszOptions`\
[in]実行可能ファイルのオプション。

`dwLaunchFlags`\
[in]セッションの[LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)を指定します。

`hStdInput`\
[in]代替入力ストリームへのハンドル。 リダイレクトが不要な場合は 0 になることがあります。

`hStdOutput`\
[in]代替出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 になることがあります。

`hStdError`\
[in]代替エラー出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 になることがあります。

`pCallback`\
[in]デバッガー イベントを受け取る[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクト。

`ppDebugProcess`\
[アウト]起動されたプロセスを表す結果の[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 通常[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)][、LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)メソッドを使用してプログラムを起動し、中断されたプログラムにデバッガーをアタッチします。 ただし、デバッグ エンジンがプログラムを起動する必要がある場合 (たとえば、デバッグ エンジンがインタープリターの一部であり、デバッグ中のプログラムがインタープリタ言語である場合)、その場合[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]はメソッドを`IDebugEngineLaunch2::LaunchSuspended`使用します。

 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)メソッドは、プロセスが中断状態で正常に起動した後にプロセスを開始するために呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
