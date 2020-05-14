---
title: 依存関係図の拡張
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, creating extensions
- layer models
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 305c562c7600dc6955ce0307db92f4e257fc1c21
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301489"
---
# <a name="extend-dependency-diagrams"></a>依存関係図の拡張

コードを記述して、依存関係図を作成および更新したり、Visual Studio の依存関係ダイアグラムに対してプログラム コードの構造を検証したりできます。 図のショートカット (コンテキスト) メニューに表示するコマンドを追加し、ドラッグ アンド ドロップ ジェスチャをカスタマイズし、テキスト テンプレートからレイヤー モデルにアクセスすることができます。 これらの拡張機能を VSIX (Visual Studio Integration Extension) にパッケージ化し、他の Visual Studio ユーザーに配布することができます。

## <a name="requirements"></a>必要条件

レイヤー拡張機能を開発するコンピューターに以下の項目がインストールされている必要があります。

- Visual Studio

- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)

- モデリング SDK のビジュアル スタジオ

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

レイヤー拡張機能を実行するコンピューターに、適切なエディションの Visual Studio がインストールされている必要があります。 Visual Studio のどのエディションが依存関係図をサポートしているかを確認するには、「[アーキテクチャツールとモデリングツールのエディションサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="see-also"></a>関連項目

- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [依存関係図: ガイドライン](../modeling/layer-diagrams-guidelines.md)
- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)
- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)
