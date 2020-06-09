---
title: DONT_SAVE_VSGLOG_TO_TEMP | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f27ab0e6-9575-4ca0-9901-37d3e5c3a2f5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40f3c3c22de6b4b0ebdbdf2dfc953f4cb1c9b5e6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736078"
---
# <a name="dont_save_vsglog_to_temp"></a>DONT_SAVE_VSGLOG_TO_TEMP
その存在によって、グラフィックス ログ ファイルがユーザーの一時ファイル ディレクトリに保存されるかどうかを定義します。

## <a name="syntax"></a>構文

```C++
#define DONT_SAVE_VSGLOG_TO_TEMP
```

## <a name="value"></a>[値]
 その有無によって、グラフィックス ログ ファイルがユーザーの一時ファイル ディレクトリに保存されるかどうかが決まるプリプロセッサ シンボル。 このシンボルが定義されている場合、`VSG_DEFAULT_RUN_FILENAME` で定義されるファイル名は、キャプチャされるアプリケーションの現在のディレクトリに対する相対パスになるか、または絶対パスです。それ以外の場合、`VSG_DEFAULT_RUN_FILENAME` で定義されるファイル名は、ユーザーの一時ファイル ディレクトリに対する相対パスになり、絶対パスにすることはできません。

## <a name="remarks"></a>Remarks
 ユーザーの特権によっては、グラフィック ログ ファイルを任意の場所に保存できないことがあります。 選択した場所にユーザーが書き込むことができるかどうかがわからない場合は、ユーザーの一時ファイル ディレクトリ、または別の既知の場所にグラフィックス ログを保存することをお勧めします。

 グラフィックス ログ ファイルを一時ファイル ディレクトリに保存することを防ぐには、`vsgcapture.h` をインクルードする前に `DONT_SAVE_VSGLOG_TO_TEMP` を定義する必要があります。

## <a name="example"></a>例
 次の例に、グラフィックス ログ ファイルをホスト コンピューターの絶対パスに保存する方法を示します。

```cpp
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h
#define DONT_SAVE_VSGLOG_TO_TEMP
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"

#include <vsgcapture.h>
```

## <a name="see-also"></a>関連項目
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
