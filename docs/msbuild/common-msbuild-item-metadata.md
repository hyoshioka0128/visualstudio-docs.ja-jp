---
title: 一般的な MSBuild 項目メタデータ | Microsoft Docs
description: 一部の MSBuild SDK またはターゲットに対して意味を持ちますが、すべての項目に既定で設定されるわけではない、省略可能な項目メタデータについて説明します。
ms.custom: SEO-VS-2020
ms.date: 07/13/2020
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- msbuild, common item metadata
- item metadata (MSBuild)
ms.assetid: 9857505d-ae15-42f1-936d-6cd7fb9dd276
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 152967fb99442b58d96016e10d8899b57ef35bf6
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796591"
---
# <a name="common-msbuild-item-metadata"></a>一般的な MSBuild 項目メタデータ

次の表では、一部の MSBuild SDK またはターゲットに対して意味を持つ省略可能な項目メタデータについて説明しますが、これはすべての項目に既定で設定されるわけではありません。 これらを設定してビルドの動作に影響を及ぼすことができますが、使用している SDK またはターゲット ファイルによってそれが認識される場合に限ります。

| 項目メタデータ | SDK | 説明 |
|---------------| ------- | -------------|
|%(Link)| すべて |Visual Studio プロジェクト システムでは、`Link` メタデータ (存在する場合) を使用して、プロジェクト ツリーに表示される内容を変更します。 **ソリューション エクスプローラー** で、別の論理フォルダー構造にファイルを置くことができます。<br />さらに、それがコピーされる項目の 1 つである場合、`AssignTargetPath` タスクでは、出力ディレクトリ内のどこにファイルをコピーするか決定するために `Link` が参照されます。|
|%(LinkBase)| .NET Core SDK | 項目のグループに対する `Link` メタデータ用に使うフォルダーを設定するために使用されます。 |

## <a name="see-also"></a>関連項目

- [MSBuild プロジェクトの共通プロパティ](../msbuild/common-msbuild-project-properties.md)
- [MSBuild プロジェクトの共通項目](../msbuild/common-msbuild-project-items.md)
- [MSBuild の既知の項目メタデータ](msbuild-well-known-item-metadata.md)