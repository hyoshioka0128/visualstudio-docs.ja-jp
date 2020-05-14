---
title: SccRunScc 関数 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700405"
---
# <a name="sccrunscc-function"></a>SccRunScc 関数
この関数は、ソース管理管理ツールを呼び出します。

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
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nファイル

[in]配列に指定されたファイルの`lpFileNames`数。

 ファイル名

[in]選択したファイル名の配列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|ソース管理管理ツールが正常に呼び出されました。|
|SCC_I_OPERATIONCANCELED|操作はキャンセルされました。|
|SCC_E_INITIALIZEFAILED|ソース管理システムを初期化できませんでした。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。|
|SCC_E_CONNECTIONFAILURE|ソース管理システムに接続できませんでした。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース管理下にありません。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 この関数を使用すると、外部管理ツールを使用して、ソース管理システムの機能の全範囲にアクセスできます。 ソース管理システムにユーザー インターフェイスがない場合、ソース管理プラグインは、必要な管理機能を実行するインターフェイスを実装できます。

 この関数は、現在選択されているファイルのファイル名の数と配列を使用して呼び出されます。 管理ツールがサポートしている場合、ファイルのリストを使用して管理インターフェースのファイルを事前選択できます。それ以外の場合、リストは無視できます。

 この関数は通常、ユーザーが **[ファイル** -> ソース管理]**メニューから** **[ソース管理サーバーの起動\<]>** を選択したときに呼び出されます。 この **[起動]** メニュー オプションは、レジストリ エントリを設定することで、常に無効にしたり、非表示にしたりできます。 詳細については、「[方法 : ソース管理プラグインをインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md)する」を参照してください。 この関数は[、SccInitialize](../extensibility/sccinitialize-function.md)が機能ビット`SCC_CAP_RUNSCC`を返す場合にのみ呼び出されます (機能[フラグ](../extensibility/capability-flags.md)の詳細については、この機能ビットおよびその他の機能ビットを参照してください)。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [方法: ソース管理プラグインのインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [機能フラグ](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
