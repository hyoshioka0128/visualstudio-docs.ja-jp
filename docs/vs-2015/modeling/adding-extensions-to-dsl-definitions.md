---
title: DSL 定義への拡張機能の追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 07e133be-92ab-4936-a02b-45d2012bd0a6
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5fab56a7738ed7b52760cf20a5bfcc8542ee5a23
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75919056"
---
# <a name="adding-extensions-to-dsl-definitions"></a>DSL 定義への拡張機能の追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL 定義の拡張機能を使用すると、ドメイン固有言語 (DSL) に対する拡張機能のパッケージを作成できます。 DSL 拡張機能は、Visual Studio Integration Extension (VSIX) に含まれており、DSL と同じ方法でユーザーのコンピューターにインストールできます。 その他の機能は、実行時に動的に有効にしたり無効にしたりすることができます。 Dsl は拡張用に明示的に設計する必要はなく、拡張 DSL を変更することなく、後またはサードパーティが拡張することができます。

 追加機能には、次のものが含まれます。

- モデル要素とプレゼンテーション要素のプロパティ

- 図形とコネクタのデコレーター

- クラス、リレーションシップ、図形、およびコネクタ

- 検証制約

- ツールボックスの項目とタブ

  拡張 DSL のユーザーは、追加機能のインスタンスを含むモデルを作成して保存できます。また、適切な拡張機能をインストールした他のユーザーがそれらを読み取ることができます。 拡張機能をインストールしていないユーザーは、追加機能を使用できませんが、追加の機能を失うことなく、モデルを更新して保存することができます。

  サンプルコードとこの機能の詳細については、「 [Visual Studio の視覚化とモデリング SDK](https://www.microsoft.com/en-us/download/details.aspx?id=48148) 」 Web サイトを参照してください。

## <a name="see-also"></a>参照
 [Visual Studio Visualization and Modeling SDK](https://www.microsoft.com/en-us/download/details.aspx?id=48148)
