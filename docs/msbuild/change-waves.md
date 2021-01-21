---
title: 流れの変化
description: 破壊的な可能性のある MSBuild の機能を有効または無効にする方法について説明します。
ms.date: 11/10/2020
ms.topic: conceptual
helpviewer_keywords:
- Change waves [MSBuild]
- MSBuildDisableFeaturesFromVersion environment variable
author: ghogen
ms.author: ghogen
manager: jillfra
monikerRange: '>=vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 68aafd8ebb97b4bf649cc41eb7739e1700c9cb1a
ms.sourcegitcommit: 83a39d48b00c6c351e5c1707942633b7f73aaad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2020
ms.locfileid: "94545665"
---
# <a name="change-waves"></a>流れの変化

"*変更ウェーブ*" は、特定のフラグを環境変数として指定することによってオプトアウトできる、MSBuild の動作変更のセットです。 その目的は、破壊的な可能性のある変更について警告し、それらの変更が標準機能になる前に、柔軟に適用できるようにすることです。 特定の変更ウェーブに含まれるすべての機能は、個別にではなくまとめて有効または無効にすることのみが可能です。

新しいバージョンの MSBuild にアップグレードすると、破壊的な可能性のある変更が既定で有効になりますが、機能がビルドに悪影響を与える場合は、その変更のウェーブを簡単に無効にできます。 各変更ウェーブは MSBuild のバージョン番号 (16.8 など) によって識別されますが、変更ウェーブを設定することによって制御されるのはビルド プロセスに影響を与える可能性のある特定の機能のみであり、その MSBuild バージョンに含まれるすべての変更ではありません。 各変更ウェーブに含まれる機能の一覧は、[この記事の後半](#change-waves-and-associated-features)に記載されています。 ある変更ウェーブを無効にすると、上位バージョンの変更ウェーブも無効になります。

## <a name="opt-out-of-change-wave-features"></a>変更ウェーブ機能のオプトアウト

変更ウェーブに含まれる機能を無効にするには、環境変数 `MSBuildDisableFeaturesFromVersion` を、**無効** にしたい機能が含まれている変更ウェーブ (または MSBuild バージョン) に設定します。 これは、その機能が開発された MSBuild のバージョンです。 以下の変更ウェーブから機能へのマッピングを参照してください。

### <a name="msbuilddisablefeaturesfromversion-values"></a>MSBuildDisableFeaturesFromVersion の値

`MSBuildDisableFeaturesFromVersion` を有効な変更ウェーブに設定していない場合は、警告が表示されたり、既定で特定のウェーブに設定されたりします。 次の表に、可能な設定を示します。

| `MSBuildDisableFeaturesFromVersion` 値                         | 結果        | 警告が表示されるか |
| :-------------                                                    | :----------   | :----------: |
| 未設定                                                             | すべての変更ウェーブが有効になります。つまり、各変更ウェーブの背後にあるすべての機能が有効になります。               | いいえ   |
| 任意の有効かつ現在の変更ウェーブ (たとえば、`16.8`)                      | 変更ウェーブ `16.8` **およびそれ以降** のすべての機能が無効になります。                                           | いいえ   |
| 無効な値 (たとえば、有効なウェーブが `16.8` と `16.10` である場合に `16.9` など)| 既定で最も近い有効な値 (上位) に設定されます。 たとえば、`16.9` に設定すると、既定で `16.10` に設定されます。               | いいえ   |
| ローテーション外 (たとえば、最上位のウェーブが `17.0` の場合に `17.1`)      | 最も近い有効な値にとどまります。 たとえば、`17.1` は `17.0` に、`16.5` は `16.8` にとどまります                    | はい  |
| 無効な形式 (たとえば `16x8`、`17_0`、`garbage` など)                    | すべての変更ウェーブが有効になります。つまり、各変更ウェーブの背後にあるすべての機能が有効になります。               | はい  |

## <a name="change-waves-and-associated-features"></a>変更ウェーブと関連する機能

以下の一覧のリンクから、その機能の GitHub PR にアクセスできます。

### <a name="168"></a>16.8

- [NoWarn を有効にする](https://github.com/dotnet/msbuild/pull/5671)
- [ターゲット/タスクのスキップされたログ メッセージを 1024 文字に切り詰める](https://github.com/dotnet/msbuild/pull/5553)
- [false の条件でドライブ全体の glob を展開しない](https://github.com/dotnet/msbuild/pull/5669)

### <a name="1610"></a>16.10

- [条件のプロパティ展開に空白が含まれている場合のエラー](https://github.com/dotnet/msbuild/pull/5672)

### <a name="170"></a>17.0

この変更ウェーブにはまだエントリがありません。

## <a name="change-waves-that-are-out-of-rotation"></a>ローテーション外の変更ウェーブ

現時点では、ローテーション外の変更ウェーブはありません。

## <a name="faq"></a>よく寄せられる質問

**変更ウェーブをローテーションから外す場合に他のすべてのリリースを対象とするのはなぜですか?**

それらの影響を受ける機能について議論し、変更への適応をサポートするために、これが十分な時間であると考えています。

**環境変数がプロジェクトのプロパティではないのはなぜですか?**

MSBuild によってプロジェクトが読み込まれる前に、変更ウェーブの下に機能を配置したいシナリオが存在します。 そのため、変更ウェーブでは環境変数を使用する必要があります。

**オプトインではなくオプトアウトする理由はなんですか?**

私たちにとってオプトアウトはより優れたアプローチです。そうでないと、機能がお客様のビルドに影響を与える場合にフィードバックが制限される可能性があります。

## <a name="see-also"></a>関連項目

- [MSBuild](msbuild.md)
- [MSBuild 16 の新機能](whats-new-msbuild-16-0.md)
