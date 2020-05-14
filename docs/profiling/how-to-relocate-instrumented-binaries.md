---
title: '方法 : インストルメントされたバイナリを再配置する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.binaries
helpviewer_keywords:
- binaries, instrumented
- instrumentation, instrumented binaries
- instrumented binaries and relocating
- profiling tools, instrumented binaries
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: cddbb0b3e27b841441937b7256ea32d722e25f5e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74774901"
---
# <a name="how-to-relocate-instrumented-binaries"></a>方法: インストルメント化されたバイナリを再配置する

インストルメンテーション中、プローブはバイナリに挿入され、アプリケーションのパフォーマンスを測定します。 インストルメントされたバイナリの再配置を選ぶと、元のバイナリのコピーがインストルメント化され、指定した場所に配置されます。 このオプションは、プロファイラーによって元のバイナリの名前を変更したくない場合に役立ちます。 バイナリが再配置されない場合は、バイナリの元のバージョンが上書きされます。

## <a name="to-relocate-instrumented-binary"></a>インストルメント化されたバイナリを再配置するには

1. **パフォーマンス エクスプローラー**で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. **[プロパティ ページ]** で、 **[バイナリ]** プロパティをクリックします。

3. **[インストルメントされたバイナリを再配置]** チェック ボックスを選びます。

4. インストルメントされたバイナリの場所を指定します。

## <a name="see-also"></a>参照

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[VSInstr](../profiling/vsinstr.md)
