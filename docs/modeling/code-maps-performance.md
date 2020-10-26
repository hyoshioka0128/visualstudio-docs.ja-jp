---
title: コードマップの速度が遅い
ms.date: 05/16/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28cb2c4fd74716aa876c57517bb440fda513de5d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75590541"
---
# <a name="improve-performance-for-code-maps"></a>コードマップのパフォーマンスを向上させる

マップを初めて生成したときに、Visual Studio は、見つかったすべての依存関係のインデックスを作成します。 このプロセスには、特に大規模なソリューションでは時間がかかることがありますが、それ以降のパフォーマンスは向上します。 コードが変更された場合、Visual Studio では、更新されたコードだけにインデックスが付け直されます。 マップがレンダリングを完了するまでにかかる時間を最小限に抑えるには、次の推奨事項を考慮してください。

- 目的の依存関係のみをマップする。

- ソリューション全体のマップを生成する前に、ソリューションのスコープを縮小する。

- コードマップツールバーの [ **ビルドのスキップ** ] を選択して、ソリューションの自動ビルドをオフにします。

- コードマップツールバーの [ **親を含める** ] を選択して、親項目の自動追加をオフにします。

   ![[ビルドのスキップ] ボタンと [親を含める] ボタン](../modeling/media/codemapsfilterskipbuildicons.png)

- コード マップ ファイルを直接編集し、不要なノードとリンクを削除する。 マップを変更しても、基のコードには影響しません。 「 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

プロジェクト項目の [**出力ディレクトリにコピー** ] プロパティが [**常にコピー**する] に設定されている場合、マップの作成や**ソリューションエクスプローラー**マップへの項目の追加に時間がかかることがあります。 パフォーマンスを向上させるには、このプロパティを **[新しい場合はコピーする]** または `PreserveNewest`に変更します。 「 [インクリメンタルビルド](../msbuild/incremental-builds.md)」を参照してください。

完成したマップには、正常にビルドされたコードの依存関係のみが表示されます。 特定のコンポーネントにビルド エラーが発生すると、そのエラーがマップに表示されます。 マップに基づいてアーキテクチャを決定する前に、コンポーネントが実際にビルドされ、その依存関係がマップ上に表示されていることを確認してください。
