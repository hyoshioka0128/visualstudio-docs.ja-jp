---
title: IDebugPortEx2::起動中断 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::LaunchSuspended
helpviewer_keywords:
- IDebugPortEx2::LaunchSuspended
ms.assetid: 34b2cf99-2e52-4757-8969-1d12ac517ec0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28ff6065bbe83852b5acc3ffe253a0bdabcc67ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725105"
---
# <a name="idebugportex2launchsuspended"></a>IDebugPortEx2::LaunchSuspended
実行可能ファイルを起動します。

## <a name="syntax"></a>構文

```cpp
HRESULT LaunchSuspended( 
   LPCOLESTR        pszExe,
   LPCOLESTR        pszArgs,
   LPCOLESTR        pszDir,
   BSTR             bstrEnv,
   DWORD            hStdInput,
   DWORD            hStdOutput,
   DWORD            hStdError,
   IDebugProcess2** ppPortProcess
);
```

```csharp
int LaunchSuspended( 
   string             pszExe,
   string             pszArgs,
   string             pszDir,
   string             bstrEnv,
   uint               hStdInput,
   uint               hStdOutput,
   uint               hStdError,
   out IDebugProcess2 ppPortProcess
);
```

## <a name="parameters"></a>パラメーター
`pszExe`\
[in]起動する実行可能ファイルの名前。 これは、パラメーターで指定された作業ディレクトリへの絶対パスまたは相対パスを`pszDir`指定できます。

`pszArgs`\
[in]実行可能ファイルに渡す引数。 引数がない場合は、null 値になることがあります。

`pszDir`\
[in]実行可能ファイルで使用される作業ディレクトリの名前。 作業ディレクトリが不要な場合は、NULL 値になることがあります。

`bstrEnv`\
[in]NULL で終わる文字列の環境ブロック、その後に追加の NULL 終端文字が続きます。

`hStdInput`\
[in]代替入力ストリームへのハンドル。 リダイレクトが不要な場合は 0 になることがあります。

`hStdOutput`\
[in]代替出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 になることがあります。

`hStdError`\
[in]代替エラー出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 になることがあります。

`ppPortProcess`\
[アウト]起動されたプロセスを表す[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、プロセスを起動して、中断され、コードを実行しないようにする必要があります。 プロセスを再開するために[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)メソッドが呼び出されます。

 プログラムは、デバッグ エンジンから起動することもできます。 詳細については、[プログラムの起動を](../../../extensibility/debugger/launching-a-program.md)参照してください。

## <a name="see-also"></a>関連項目
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)
- [プログラムの起動](../../../extensibility/debugger/launching-a-program.md)
