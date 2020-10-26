---
title: Sccenumの関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b1826a87b20d6bc92254fc4a86b8e0b756400ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700904"
---
# <a name="sccenumchangedfiles-function"></a>Sccenumのすべてのファイル関数
ローカルファイルの一覧を指定すると、ソースコード管理データベースの対応するバージョンとは異なるファイルがこの関数によって判断されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccEnumChangedFiles(
   LPVOID  pContext,
   HWND    hWnd,
   LONG    cFiles,
   LPCSTR* lpFileNames,
   LONG*   plIsFileDifferent
);
```

### <a name="parameters"></a>パラメーター
 pContext

からソース管理プラグインのコンテキストポインター。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 cFiles

から配列に指定されたファイル名の数 `lpFileNames` 。 配列のサイズも指定し `plIsFileDifferent` ます。

 lpFileNames 名

から確認するローカルファイル名の配列。

 plIsFileDifferent

[入力、出力]各ファイルの相違ステータスを示す値の配列 (配列には少なくともエントリが必要 `cFiles` です)。 0以外の場合は、ファイルが異なることを意味します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_UNSPECIFIEDERROR|一般的なエラー。|

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
