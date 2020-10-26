---
title: SccRunScc 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d012908e59be8b82e34ff68cdab1945c5bd2de8b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700405"
---
# <a name="sccrunscc-function"></a>SccRunScc 関数
この関数は、ソース管理の管理ツールを呼び出します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccRunScc(
   LPVOID  pvContext,
   HWND    hWnd,
   LONG    nFiles,
   LPCSTR* lpFileNames
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

から配列に指定されたファイルの数 `lpFileNames` 。

 lpFileNames 名

から選択されたファイル名の配列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ソース管理の管理ツールが正常に呼び出されました。|
|SCC_I_OPERATIONCANCELED|操作が取り消されました。|
|SCC_E_INITIALIZEFAILED|ソース管理システムを初期化できませんでした。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。|
|SCC_E_CONNECTIONFAILURE|ソース管理システムに接続できませんでした。|
|SCC_E_FILENOTCONTROLLED|選択されたファイルはソース管理下にありません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>注釈
 この関数を使用すると、呼び出し元は、外部管理ツールを使用して、ソース管理システムのすべての機能にアクセスできます。 ソース管理システムにユーザーインターフェイスがない場合、ソース管理プラグインは、必要な管理機能を実行するためのインターフェイスを実装できます。

 この関数は、現在選択されているファイルのカウントとファイル名の配列を使用して呼び出されます。 管理ツールでサポートされている場合は、ファイルの一覧を使用して、管理インターフェイスでファイルを事前に指定できます。それ以外の場合、リストは無視してかまいません。

 通常、この関数は、ユーザーが [**ファイル** ** \<Source Control Server> **  ->  **ソース管理**] メニューから [起動] を選択したときに呼び出されます。 この **起動** メニューオプションは、レジストリエントリを設定することによって、常に無効にしたり、非表示にしたりすることができます。 詳細については [、「方法: ソース管理プラグインをインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md) する」を参照してください。 この関数は、 [Sccinitialize](../extensibility/sccinitialize-function.md) が機能ビットを返す場合にのみ呼び出され `SCC_CAP_RUNSCC` ます (この機能の詳細については、「 [機能フラグ](../extensibility/capability-flags.md) 」を参照してください)。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [方法: ソース管理プラグインのインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [機能フラグ](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
