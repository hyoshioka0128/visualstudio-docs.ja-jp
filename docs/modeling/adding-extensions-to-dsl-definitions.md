---
title: DSL 定義への拡張機能の追加
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2500fc8d9e09d95d7972a4b151b01937a5570a08
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544236"
---
# <a name="add-extensions-to-dsl-definitions"></a>DSL 定義に拡張機能を追加する

DSL 定義の拡張機能を使用すると、ドメイン固有言語 (DSL) に対する拡張機能のパッケージを作成できます。 DSL 拡張機能は、Visual Studio Integration Extension (VSIX) に含まれており、DSL と同じ方法でユーザーのコンピューターにインストールできます。 その他の機能は、実行時に動的に有効にしたり無効にしたりすることができます。 Dsl は拡張用に明示的に設計する必要はなく、拡張 DSL を変更することなく、後で、またはサードパーティが拡張できます。

DSL 拡張には、次の機能を含めることができます。

- モデル要素とプレゼンテーション要素のプロパティ

- 図形とコネクタのデコレーター

- クラス、リレーションシップ、図形、およびコネクタ

- 検証制約

- ツールボックスの項目とタブ

拡張 DSL のユーザーは、追加機能のインスタンスを含むモデルを作成して保存できます。 モデルは、適切な拡張機能をインストールした他のユーザーが読み取ることができます。 拡張機能をインストールしていないユーザーは、追加機能を使用できませんが、追加の機能を失うことなく、モデルを更新して保存することができます。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>関連項目

- [関連するブログ記事](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
