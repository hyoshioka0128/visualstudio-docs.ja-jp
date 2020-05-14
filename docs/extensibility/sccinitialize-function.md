---
title: Scc初期化関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 661e0a24fa1d222079fd5ee728c5f42a5386c75b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700642"
---
# <a name="sccinitialize-function"></a>SccInitialize 関数
この関数は、ソース管理プラグインを初期化し、統合開発環境 (IDE) に機能と制限を提供します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccInitialize (
   LPVOID* ppvContext,
   HWND    hWnd,
   LPCSTR  lpCallerName,
   LPSTR   lpSccName,
   LPLONG  lpSccCaps,
   LPSTR   lpAuxPathLabel,
   LPLONG  pnCheckoutCommentLen,
   LPLONG  pnCommentLen
);
```

#### <a name="parameters"></a>パラメーター
 `ppvContext`

[in]ソース管理プラグインは、コンテキスト構造へのポインターをここに配置できます。

 `hWnd`

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 `lpCallerName`

[in]ソース管理プラグインを呼び出すプログラムの名前。

 `lpSccName`

[イン、アウト]ソース管理プラグインが独自の名前を付けるバッファ ( を超`SCC_NAME_LEN`えないようにする ) 。

 `lpSccCaps`

[アウト]ソース管理プラグインの機能フラグを返します。

 `lpAuxPathLabel`

[イン、アウト]ソース管理プラグインが[、SccOpenProject](../extensibility/sccopenproject-function.md)および[SccGetProjPath](../extensibility/sccgetprojpath-function.md)によって返される`SCC_AUXLABEL_LEN``lpAuxProjPath`パラメーターを記述する文字列を格納するバッファーです ( を超えないように ) 。

 `pnCheckoutCommentLen`

[アウト]チェックアウト コメントの最大許容長を返します。

 `pnCommentLen`

[アウト]他のコメントに対して許容される最大長を返します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|ソース管理の初期化に成功しました。|
|SCC_E_INITIALIZEFAILED|システムを初期化できませんでした。|
|SCC_E_NOTAUTHORIZED|ユーザーは、指定された操作を実行できません。|
|SCC_E_NONSPECFICERROR|非特異的な障害;ソース管理システムが初期化されませんでした。|

## <a name="remarks"></a>Remarks
 IDE は、ソース管理プラグインを最初に読み込むときに、この関数を呼び出します。 これにより、IDE は、呼び出し元の名前などの特定の情報をプラグインに渡すことができます。 IDE は、コメントの最大許容長やプラグインの機能など、特定の情報も返します。

 ポインター`ppvContext`へのポインター。 `NULL` ソース管理プラグインは、独自の使用のために構造体を割り当て、その構造体へのポインターを`ppvContext`に格納できます。 IDE は、このポインターを他のすべての VSSCI API 関数に渡し、プラグインがグローバルストレージに頼らずにコンテキスト情報を利用できるようにし、プラグインの複数のインスタンスをサポートできるようにします。 この構造体は[、SccUninitialize](../extensibility/sccuninitialize-function.md)が呼び出されたときに割り当てを解除する必要があります。

 パラメーター`lpCallerName`と`lpSccName`パラメーターを使用すると、IDE とソース管理プラグインで名前を交換できます。 これらの名前は、単に複数のインスタンスを区別するために使用することも、実際にはメニューやダイアログ ボックスに表示することもできます。

 パラメーター`lpAuxPathLabel`は、ソリューション ファイルに格納され[、SccOpenProject](../extensibility/sccopenproject-function.md)への呼び出しでソース管理プラグインに渡される補助プロジェクトパスを識別するためのコメントとして使用される文字列です。 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]文字列 "SourceSafe プロジェクト:" を使用します。他のソース管理プラグインは、この特定の文字列を使用しないようにする必要があります。

 この`lpSccCaps`パラメーターは、ソース管理プラグインに、プラグインの機能を示すビットフラグを格納する場所を提供します。 (機能ビットフラグの完全なリストについては、[機能フラグ](../extensibility/capability-flags.md)を参照してください。 たとえば、プラグインが呼び出し元が提供するコールバック関数に結果を書き込む予定の場合、プラグインは機能ビット SCC_CAP_TEXTOUTを設定します。 これにより、バージョン管理の結果を表示するウィンドウを作成するように IDE に通知されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [機能フラグ](../extensibility/capability-flags.md)
