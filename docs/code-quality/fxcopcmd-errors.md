---
title: FxCopCmd エラー
ms.date: 10/19/2016
description: FxCopCmd コマンドが返すエラーコードについて説明します。 各コードが表すエラーの種類を確認し、致命的なエラーを認識する方法を確認します。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
ms.author: mikejo
author: mikejo5000
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: efeabd85bbf2753dd3f5e37a43e0918b7f95d7fe
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860218"
---
# <a name="fxcopcmd-tool-errors"></a>FxCopCmd ツールのエラー

FxCopCmd では、すべてのエラーが致命的であるとは見なされません。 部分分析を実行するための十分な情報が FxCopCmd にある場合は、分析が実行され、発生したエラーが報告されます。 エラーコード (32 ビット整数) には、エラーに対応する数値のビットごとの組み合わせが含まれています。

次の表では、FxCopCmd によって返されるエラーコードについて説明します。

|エラー|数値|
|-----------|-------------------|
|エラーなし|0x0|
|分析エラー|0x1|
|規則の例外|0x2|
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

致命的なエラーの **分析エラー** が返されます。 これは、分析を完了できなかったことを示します。 該当する場合、エラーコードには、致命的なエラーの根底にある原因も含まれます。 次の状況では、致命的なエラーが発生します。

- 入力が不十分なため、分析を実行できませんでした。

- 分析によって、FxCopCmd で処理されない例外がスローされました。

- 指定されたプロジェクトファイルが見つからないか、または破損しています。

- Output オプションが指定されていないか、ファイルを書き込めませんでした。

> [!NOTE]
> FxCopCmd のリターンコード **アセンブリ** は、エラー0x200 自体を参照しますが、エラーではなく警告です。 このリターンコードは、間接参照が不足していて、FxCopCmd がそれらを処理できたことを示します。 警告は、一部の分析結果が侵害された可能性があることを意味します。 他のリターンコードと組み合わせると、 **アセンブリ参照エラー** をエラーとして扱うことができます。

## <a name="see-also"></a>関連項目

- [コード分析のアプリケーション エラー](../code-quality/code-analysis-application-errors.md)
