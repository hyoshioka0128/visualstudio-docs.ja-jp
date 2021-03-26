---
description: この関数は、ファイルまたはプロジェクトのソース管理プロパティを表示します。
title: SccProperties 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 56306bb7c248ea500e16964c0929f34a27187298
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056520"
---
# <a name="sccproperties-function"></a>SccProperties 関数
この関数は、ファイルまたはプロジェクトのソース管理プロパティを表示します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccProperties (
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpFileName

からファイルまたはプロジェクトの完全修飾パス名。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロパティが正常に表示されました。|
|SCC_I_RELOADFILE|バージョンコントロールシステムによってファイルのプロパティが変更されたため、IDE がこのファイルを再読み込みする必要があります。|
|SCC_E_PROJNOTOPEN|指定されたプロジェクトは、ソース管理で開かれていません。|
|SCC_E_NOTAUTHORIZED|このファイルまたはプロジェクトのプロパティを表示する権限がユーザーにありません。|
|SCC_E_FILENOTCONTROLLED|指定されたファイルまたはプロジェクトは、ソース管理下にありません。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不明または一般的なエラーが発生しました。|

## <a name="remarks"></a>注釈
 ソース管理プラグインによって、独自のダイアログボックスにプロパティが表示されます。

 プロパティはソース管理プラグインによって定義され、プラグインにプラグインとは異なる場合があります。 プラグインでファイルのソース管理プロパティを変更できる場合、 `SCC_I_RELOAD` このファイルまたはプロジェクトを再読み込みする必要があることを IDE に通知するために、が返されます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
