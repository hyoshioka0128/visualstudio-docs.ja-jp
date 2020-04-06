---
title: 関数を作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0694fd6b4ba82faf8b05354765fc5734efe2ef4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700211"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 関数
この関数は、ソース管理プラグインが MSSCCPRJ の作成をサポートするかどうかを決定します。指定された各ファイルの SCC ファイル。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccWillCreateSccFile(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPBOOL  pbSccFiles
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 nファイル

[in]`lpFileNames`配列に含まれるファイル名の数と配列の長さ`pbSccFiles`。

 ファイル名

[in]チェックする完全修飾ファイル名の配列 (配列は呼び出し元によって割り当てられる必要があります)。

 ファイル

[イン、アウト]結果を格納する配列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_E_INVALIDFILEPATH|アレイ内のパスの 1 つが無効です。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 この関数は、ソース管理プラグインが MSSCCPRJ でサポートを提供するかどうかを判断するファイルの一覧を使用して呼び出されます。指定された各ファイルの SCC ファイル (MSSCCPRJ の詳細については。SCC ファイルを参照してください[。SCC ファイル](../extensibility/mssccprj-scc-file.md))。 ソース管理プラグインは、MSSCCPRJ を作成する機能があるかどうかを宣言できます。初期化中に宣言`SCC_CAP_SCCFILE`して SCC ファイルを作成します。 プラグインは、指定された`TRUE``pbSccFiles`ファイル`FALSE`の中に MSSCCPRJ が含まれるファイルを示すために、配列内のファイルごとに戻ります。SCC サポート。 プラグインが関数から成功コードを返す場合、戻り値配列の値が受け入れられます。 失敗した場合、配列は無視されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)
