---
title: FxCopCmd エラー
ms.date: 10/19/2016
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
ms.author: mikejo
author: jillre
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5916121a555531672cf70280051f02a889f611ac
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091770"
---
# <a name="fxcopcmd-tool-errors"></a>FxCopCmd ツールのエラー

FxCopCmd では、すべてのエラーが致命的であるとは見なされません。 部分分析を実行するための十分な情報が FxCopCmd にある場合は、分析が実行され、発生したエラーが報告されます。 エラーコード (32 ビット整数) には、エラーに対応する数値のビットごとの組み合わせが含まれています。

次の表では、FxCopCmd によって返されるエラーコードについて説明します。

|エラー|数値|
|-----------|-------------------|
|エラーなし|0x0|
|分析エラー|0x1|
|ルールの例外|0x2|
|プロジェクトの読み込みエラー|0x4|
|アセンブリの読み込みエラー|0x8|
|ルールライブラリの読み込みエラー|0x10|
|インポートレポートの読み込みエラー|0x20|
|出力エラー|0x40|
|コマンドラインスイッチエラー|0x80|
|初期化エラー|0x100|
|アセンブリ参照エラー|0x200|
|BuildBreakingMessage|0x400|
|不明なエラー|0x1000000|

致命的なエラーの**分析エラー**が返されます。 これは、分析を完了できなかったことを示します。 該当する場合、エラーコードには、致命的なエラーの根底にある原因も含まれます。 次の状況では、致命的なエラーが発生します。

- 入力が不十分なため、分析を実行できませんでした。

- 分析によって、FxCopCmd で処理されない例外がスローされました。

- 指定されたプロジェクトファイルが見つからないか、または破損しています。

- Output オプションが指定されていないか、ファイルを書き込めませんでした。

> [!NOTE]
> FxCopCmd のリターンコード**アセンブリ**は、エラー0x200 自体を参照しますが、エラーではなく警告です。 このリターンコードは、間接参照が不足していて、FxCopCmd がそれらを処理できたことを示します。 警告は、一部の分析結果が侵害された可能性があることを意味します。 他のリターンコードと組み合わせると、**アセンブリ参照エラー**をエラーとして扱うことができます。

## <a name="see-also"></a>参照

- [コード分析のアプリケーション エラー](../code-quality/code-analysis-application-errors.md)
