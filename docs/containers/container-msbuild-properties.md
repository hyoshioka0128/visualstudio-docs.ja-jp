---
title: Visual Studio コンテナー ツールのビルド プロパティ
author: ghogen
description: コンテナー ツールのビルド プロセスの概要
ms.author: ghogen
ms.date: 06/06/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: 987d358abcccadf36d15593722ff55ba4b879d03
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "71950696"
---
# <a name="container-tools-build-properties"></a>コンテナー ツールのビルド プロパティ

プロジェクトのビルドに向けて MSBuild によって使用されるプロパティを設定することによって、Visual Studio でのコンテナー プロジェクトのビルド方法をカスタマイズすることができます。 たとえば、Dockerfile の名前の変更、イメージのタグやラベルの指定、Docker コマンドに渡す追加の引数の指定を行ったり、コンテナー環境の外側のビルドなど、特定のパフォーマンス最適化を Visual Studio で実行するかどうかを管理したりすることができます。 また、起動する実行可能ファイルの名前や、指定するコマンド ライン引数などのデバッグ プロパティを設定することもできます。

プロパティの値を設定するには、プロジェクト ファイルを編集します。 たとえば、Dockerfile に *MyDockerfile* という名前が付けられているとします。 次のように、プロジェクト ファイル内で `DockerfileFile` プロパティを設定することができます。

```xml
<PropertyGroup>
   <DockerfileFile>MyDockerfile</DockerfileFile>
</PropertyGroup>
```

プロパティ設定を、既存の `PropertyGroup` 要素に追加できます。存在しない場合は、新しい `PropertyGroup` 要素を作成できます。

次の表は、コンテナー プロジェクトで使用できる MSBuild プロパティを示しています。 NuGet パッケージ バージョンは、[Microsoft.VisualStudio.Azure.Containers.Tools.Targets](https://www.nuget.org/packages/Microsoft.VisualStudio.Azure.Containers.Tools.Targets/) に適用されます。

| プロパティ名 | 説明 | 既定値  | NuGet パッケージ バージョン|
|---------------|-------------|----------------|----------------------|
| ContainerDevelopmentMode | "ホスト上でビルド" の最適化 ("高速モード" のデバッグ) を有効にするかどうかを制御します。  指定できる値は、**Fast** と **Regular** です。 | Fast |1.0.1872750 以降|
| ContainerVsDbgPath | VSDBG デバッガー用のパス。 | `%USERPROFILE%\vsdbg\vs2017u5` |1.0.1985401 以降|
| DockerDebuggeeArguments | デバッグ時に、デバッガーは、これらの引数を起動した実行可能ファイルに渡すよう指示されます。 | ASP.NET .NET Framework プロジェクトには適用されません |1.7.8 以降|
| DockerDebuggeeProgram | デバッグ時に、デバッガーは、この実行可能ファイルを起動するよう指示されます。 | .NET Core プロジェクトの場合: dotnet、ASP.NET .NET Framework プロジェクトの場合: 該当なし (IIS が常に使用されます) |1.7.8 以降|
| DockerDebuggeeKillProgram | このコマンドは、コンテナー内で実行中のプロセスを終了するために使用されます。 | ASP.NET .NET Framework プロジェクトには適用されません |1.7.8 以降|
| DockerDebuggeeWorkingDirectory | デバッグ時に、デバッガーは、このパスを作業ディレクトリとして使用するよう指示されます。 | C:\app (Windows) または /app (Linux) |1.7.8 以降|
| DockerDefaultTargetOS | Docker イメージをビルドするときに使用される、既定のターゲット オペレーティング システム。 | Visual Studio によって設定されます。 |1.0.1985401 以降|
| DockerImageLabels | Docker イメージに適用される、既定のラベル セット。 | com.microsoft.created-by=visual-studio;com.microsoft.visual-studio.project-name=$(MSBuildProjectName) |1.5.4 以降|
| DockerFastModeProjectMountDirectory|**高速モード**では、このプロパティは、実行中のコンテナーにプロジェクト出力ディレクトリがボリュームマウントされる場所を制御します。|C:\app (Windows) または /app (Linux)|1.9.2 以降|
| DockerfileBuildArguments | Docker ビルド コマンドに渡される追加の引数。 | 該当なし。 |1.0.1872750 以降|
| DockerfileContext | Docker イメージをビルドするときに使用される、既定のコンテキスト。 | Visual Studio によって設定されます。 |1.0.1872750 以降|
| DockerfileFastModeStage | デバッグ モードでイメージをビルドするときに使用される、Dockerfile ステージ (つまり、ターゲット)。 | Dockerfile (ベース) で発見された最初のステージ |
| DockerfileFile | プロジェクトのコンテナーをビルドまたは実行するために使用される、既定の Dockerfile について説明します。 これは、パスに置き換えることもできます。 | Dockerfile |1.0.1872750 以降|
| DockerfileRunArguments | Docker 実行コマンドに渡される追加の引数。 | 該当なし。 |1.0.1872750 以降|
| DockerfileRunEnvironmentFiles | Docker の実行中に適用される、セミコロンで区切られた環境ファイルの一覧。 | 該当なし。 |1.0.1872750 以降|
| DockerfileTag | Docker イメージをビルドするときに使用されるタグ。 デバッグでは、":dev" がタグに追加されます。 | 次の規則に従って英数字以外の文字を削除した後のアセンブリ名。 <br/> 結果のタグがすべて数値の場合、"image" がプレフィックスとして挿入されます (たとえば、image2314)。 <br/> 結果のタグが空の文字列の場合は、"image" がタグとして使用されます。 |1.0.1872750 以降|

## <a name="next-steps"></a>次の手順

MSBuild プロパティの一般情報については、[MSBuild プロパティ](../msbuild/msbuild-properties.md)を参照してください。

## <a name="see-also"></a>関連項目

[Docker Compose のビルド プロパティ](docker-compose-properties.md)

[コンテナー ツールの起動設定](container-launch-settings.md)

[MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)
