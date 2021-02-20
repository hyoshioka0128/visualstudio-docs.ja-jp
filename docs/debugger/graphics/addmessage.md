---
title: AddMessage | Microsoft Docs
description: VsgDbg クラスの AddMessage メソッドを使用し、グラフィックス診断 HUD (ヘッドアップ ディスプレイ) にカスタム メッセージを追加します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 102a0404-a00c-4566-93f3-01bc8df63280
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d9d51e4415d9707b2df4bb0912290d4f5aa7825f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874640"
---
# <a name="addmessage"></a>AddMessage
グラフィックス診断の *HUD* (ヘッドアップ ディスプレイ) にカスタム メッセージを追加します。

## <a name="syntax"></a>構文

```C++
void AddMessage(
  wchar_t const * szMessage
);
```

#### <a name="parameters"></a>パラメーター
 `szMessage` HUD に追加するメッセージ。

## <a name="remarks"></a>Remarks
 グラフィックス診断の HUD は、グラフィック診断で実行されているアプリケーションの左上隅に表示されます。 これには、アプリケーションとグラフィックス情報キャプチャのランタイム情報、およびこの関数の呼び出しによって追加されたメッセージが表示されます。

 HUD にメッセージを追加するには、アクティブにグラフィックス情報をキャプチャする必要はありません。メッセージは、`VsgDbg` クラスのインスタンスを使用して追加できますが、[Init](init.md) メンバー関数は最初に呼び出されません。 メッセージは HUD に表示されるだけで、グラフィックのログ ファイルには記録されません。