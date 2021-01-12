---
title: コピー (プログラムによるキャプチャ) | Microsoft Docs
description: VsgDbg クラスの Copy メソッドを使用し、アクティブなグラフィックス ログ (.vsglog) ファイルのコンテンツを新しいファイルにコピーします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 30ec235a-0abb-44b9-8852-61bc9e67ce22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 126b1d7a2fa9064a343e7eadbe83dd1eeecccb83
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727845"
---
# <a name="copy-programmatic-capture"></a>コピー (プログラムによるキャプチャ)
アクティブなグラフィックス ログ (.vsglog) ファイルの内容を、新しいファイルにコピーします。

## <a name="syntax"></a>構文

```C++
void Copy(
  wchar_t const * szNewVSGLog
);
```

#### <a name="parameters"></a>パラメーター
 `szNewVSGLog` 新しいグラフィックス ログ ファイルのファイル名。

## <a name="remarks"></a>Remarks
 グラフィックス情報を新しいファイルにコピーするには、グラフィック情報を既にキャプチャしている必要があります。していない場合は、何も実行されません。