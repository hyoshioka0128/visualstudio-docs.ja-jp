---
title: MSBuild に関する問題のトラブルシューティングとログ記録
description: Visual Studio プロジェクトのビルドに関する問題を診断し、必要に応じて、調査のために Microsoft に送信するログを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/27/2019
ms.technology: vs-ide-compile
ms.topic: troubleshooting
helpviewer_keywords:
- msbuild logs"
author: corob-msft
ms.author: corob
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Generate build logs for msbuild projects to collect helpful information when troubleshooting issues.
ms.openlocfilehash: c6b08b243a5b4eec3119ceedbaf2177670aa3e83
ms.sourcegitcommit: c9a84e6c01e12ccda9ec7072dd524830007e02a3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92136577"
---
# <a name="troubleshoot-and-create-logs-for-msbuild-problems"></a>MSBuild に関する問題のトラブルシューティングとログ記録

以下の手順によって、Visual Studio プロジェクトのビルドに関する問題を診断し、必要に応じて、調査のために Microsoft に送信するログを作成することができます。

## <a name="a-property-value-is-ignored"></a>プロパティの値が無視される

プロジェクトのプロパティが特定の値に設定されているように見えるのに、ビルドに影響がない場合は、次の手順に従います。

1. ご自身の Visual Studio のバージョンに対応する Visual Studio 開発者コマンド プロンプトを開きます。
1. 使用するソリューション パス、構成、プロジェクト名の値を代入した後、次のコマンドを実行します。

    ```cmd
    msbuild /p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /pp:out.xml MyProject.vcxproj
    ```

    このコマンドにより、"前処理済み" の msbuild プロジェクト ファイル (out.xml) が生成されます。 そのファイルから特定のプロパティを検索すれば、それが定義されている場所を確認できます。

プロパティの最後の定義が、ビルドによって使用されます。 プロパティが 2 回設定されている場合は、2 つ目の値により 1 つ目が上書きされます。 また、MSBuild では、いくつかのパスでプロジェクトが評価されます。

- PropertyGroups と Imports
- ItemDefinitionGroups
- ItemGroups
- ターゲット

そのため、次の順序を考えてみます。

```xml
<PropertyGroup>
   <MyProperty>A</MyProperty>
</PropertyGroup>
<ItemGroup>
   <MyItems Include="MyFile.txt"/>
</ItemGroup>
<ItemDefinitionGroup>
  <MyItems>
      <MyMetadata>$(MyProperty)</MyMetadata>
  </MyItems>
</ItemDefinitionGroup>
<PropertyGroup>
   <MyProperty>B</MyProperty>
</PropertyGroup>
```

"MyFile.txt" 項目の "MyMetadata" の値は、ビルド中に "B" と評価されます ("A" や空ではありません)

## <a name="incremental-build-is-building-more-than-it-should"></a>インクリメンタル ビルドで必要以上にビルドされる

MSBuild によってプロジェクトまたはプロジェクト項目が不必要にリビルドされる場合は、詳細またはバイナリ ビルド ログを作成します。 そのログから、不必要にビルドまたはコンパイルされていたファイルを検索できます。 出力は次のようになります。

```output
  Task "CL"

  Using cached input dependency table built from:

  F:\test\Project1\Project1\Debug\Project1.tlog\CL.read.1.tlog

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ
  Project1.cpp will be compiled because F:\TEST\PROJECT1\PROJECT1\PROJECT1.H was modified at 6/5/2019 12:37:09 PM.

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ

  Write Tracking Logs:
  Debug\Project1.tlog\CL.write.1.tlog
```

Visual Studio IDE 内で (詳細な出力ウィンドウを使って) ビルドしている場合、 **[出力ウィンドウ]** に各プロジェクトが最新の状態でない理由が表示されます。

```output
1>------ Up-To-Date check: Project: Project1, Configuration: Debug Win32 ------

1>Project is not up-to-date: build input 'f:\test\project1\project1\project1.h' was modified after the last build finished.
```

## <a name="create-a-binary-msbuild-log"></a>msbuild のバイナリ ログを作成する

1. ご自分のバージョンの Visual Studio の [開発者コマンド プロンプト] を開きます。
1. コマンド プロンプトから、次のコマンドのいずれかを実行します。 (実際のプロジェクトと構成値を使うことを忘れないでください。):

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /bl MySolution.sln
    ```

    or

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /bl MyProject.vcxproj
    ```

MSBuild を実行したディレクトリに、Msbuild.binlog ファイルが作成されます。 [Msbuild Structured Log Viewer](http://www.msbuildlog.com/) を使って、これを表示および検索できます。

## <a name="create-a-detailed-log"></a>詳細なログを作成する

1. Visual Studio のメイン メニューから、 **[ツール]**  >  **[オプション]**  >  **[プロジェクトおよびソリューション]**  > **[ビルド/実行]** に移動します。
1. **[Msbuild project build verbosity]\(Msbuild プロジェクトのビルドの詳細度\)** を両方のコンボ ボックスで **[詳細]** に設定します。 先頭のものを使うと **[出力ウィンドウ]** でのビルドの詳細度を制御でき、2 番目を使うと、ビルド中に各プロジェクトの中間ディレクトリに作成される \<projectname\>.log ファイルでのビルドの詳細度を制御できます。
2. Visual Studio 開発者コマンド プロンプトで、使用する実際のパスと構成値を代入して次のコマンドのいずれかを入力します。

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /fl MySolution.sln
    ```

    or

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /fl MyProject.vcxproj
    ```

    msbuild を実行したディレクトリに、Msbuild.log ファイルが作成されます。

## <a name="see-also"></a>関連項目

- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
