---
title: SccAddFromScc 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e35ae460d6ceb505bc7ad64a0e522bf2841260f2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99886614"
---
# <a name="sccaddfromscc-function"></a>SccAddFromScc 関数
この関数を使用すると、ユーザーは既にソース管理システムにあるファイルを参照し、そのファイルを現在のプロジェクトの一部にすることができます。 たとえば、この関数では、ファイルをコピーせずに、現在のプロジェクトに共通のヘッダーファイルを取得できます。 ファイルの戻り値の配列には、 `lplpFileNames` ユーザーが IDE プロジェクトに追加するファイルの一覧が含まれています。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAddFromScc (
   LPVOID   pvContext,
   HWND     hWnd,
   LPLONG   lpnFiles,
   LPCSTR** lplpFileNames
);
```

### <a name="parameters"></a>パラメーター
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpnFiles

[入力、出力]に追加されるファイルの数のバッファー。 (が `NULL` 指すメモリが `lplpFileNames` 解放される場合はです。 詳細については、「解説」を参照してください。)

 lplpFileNames 名

[入力、出力]ディレクトリパスのないすべてのファイル名へのポインターの配列。 この配列は、ソース管理プラグインによって割り当てられ解放されます。 `lpnFiles`= 1 で、 `lplpFileNames` がではない場合 `NULL` 、が指す配列内の最初の名前には `lplpFileNames` コピー先のフォルダーが格納されます。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ファイルが正常に配置され、プロジェクトに追加されました。|
|SCC_I_OPERATIONCANCELED|操作はキャンセルされましたが、無効です。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|

## <a name="remarks"></a>解説
 IDE はこの関数を呼び出します。 ソース管理プラグインがローカルの出力先フォルダーの指定をサポートしている場合、IDE は `lpnFiles` = 1 を渡し、ローカルフォルダー名をに渡し `lplpFileNames` ます。

 関数の呼び出しによってが返された場合 `SccAddFromScc` 、プラグインはとに値を割り当て `lpnFiles` `lplpFileNames` 、必要に応じてファイル名配列のメモリを割り当てます (この割り当てはのポインターに置き換わることに注意して `lplpFileNames` ください)。 ソース管理プラグインは、すべてのファイルをユーザーのディレクトリまたは指定されたフォルダーに配置する役割を担います。 IDE は、IDE プロジェクトにファイルを追加します。

 最後に、IDE はこの関数を2回呼び出し、にを渡し `NULL` `lpnFiles` ます。 これは、のファイル名配列に割り当てられたメモリを解放するために、ソース管理プラグインによって特別なシグナルとして解釈されます。 `lplpFileNames``.`

 `lplpFileNames` は `char ***` ポインターです。 ソース管理プラグインは、ファイル名へのポインターの配列へのポインターを配置するため、この API の標準的な方法でリストを渡します。

> [!NOTE]
> VSSCI API の初期バージョンでは、追加されたファイルのターゲットプロジェクトを示す方法が提供されていませんでした。 これに対応するために、パラメーターのセマンティクス `lplpFIleNames` が拡張され、出力パラメーターではなく in/out パラメーターになるようになりました。 1つのファイルのみが指定されている場合 (つまり、が = 1 である値)、 `lpnFiles` の最初の要素には `lplpFileNames` ターゲットフォルダーが含まれます。 これらの新しいセマンティクスを使用するために、IDE は `SccSetOption` `nOption` パラメーターをに設定して関数を呼び出し `SCC_OPT_SHARESUBPROJ` ます。 ソース管理プラグインがセマンティクスをサポートしていない場合は、を返し `SCC_E_OPTNOTSUPPORTED` ます。 これにより、 **ソース管理からの追加** 機能の使用が無効になります。 プラグインが **ソース管理からの追加** 機能 () をサポートしている場合は、 `SCC_CAP_ADDFROMSCC` 新しいセマンティクスをサポートし、を返す必要があり `SCC_I_SHARESUBPROJOK` ます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
