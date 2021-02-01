---
title: インストルメントされたバイナリを再配置する | Microsoft Docs
description: プローブをバイナリに挿入して、インストルメンテーション中にアプリケーションのパフォーマンスを測定する方法について学習します。
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: ee94737f59f5c29aac47d686f68ade06131d0379
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720619"
---
# <a name="how-to-relocate-instrumented-binaries"></a>方法: インストルメント化されたバイナリの再配置

インストルメンテーション中、プローブはバイナリに挿入され、アプリケーションのパフォーマンスを測定します。 インストルメントされたバイナリの再配置を選ぶと、元のバイナリのコピーがインストルメント化され、指定した場所に配置されます。 このオプションは、プロファイラーによって元のバイナリの名前を変更したくない場合に役立ちます。 バイナリが再配置されない場合は、バイナリの元のバージョンが上書きされます。

## <a name="to-relocate-instrumented-binary"></a>インストルメント化されたバイナリを再配置するには

1. **パフォーマンス エクスプローラー** で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. **[プロパティ ページ]** で、 **[バイナリ]** プロパティをクリックします。

3. **[インストルメントされたバイナリを再配置]** チェック ボックスを選びます。

4. インストルメントされたバイナリの場所を指定します。

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[VSInstr](../profiling/vsinstr.md)
