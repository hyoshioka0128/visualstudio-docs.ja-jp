---
title: Symbol Path コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.symbolpath
helpviewer_keywords:
- symbol path command
- Debug.SymbolPath command
- SymbolPath command
ms.assetid: b697ef2d-3f5d-40df-b113-7068a5bec0d4
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ed8ec8e7f990a4a2c5d943a15a105faa5ab23572
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589384"
---
# <a name="symbol-path-command"></a>Symbol Path コマンド
デバッガーによってシンボルが検索されるディレクトリの一覧を設定します。

## <a name="syntax"></a>構文

```
Debug.SymbolPath pathname1;pathname2;... pathnameN
```

## <a name="arguments"></a>引数
`pathname`

任意。 デバッガーによってシンボルが検索されるパスを、セミコロンで区切った一覧です。

## <a name="remarks"></a>解説
`pathname` を指定しない場合、シンボル用の現在のパスがコマンドによって一覧表示されます。

## <a name="example"></a>例
次の例では、シンボル ディレクトリの一覧に 2 つのパスを追加します。

```
Debug.SymbolPath C:\Symbol Path 1;C:\Symbol Path 2
```

## <a name="example"></a>例
次の例では、シンボル用の現在のパスをセミコロンで区切った一覧が表示されます。

```
Debug.SymbolPath
```

## <a name="see-also"></a>参照

- [[コマンド] ウィンドウ](../../ide/reference/command-window.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
