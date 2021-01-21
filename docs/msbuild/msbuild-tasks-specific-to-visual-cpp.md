---
title: C++ に固有の MSBuild タスク | Microsoft Docs
description: C++ がインストールされている場合、MSBuild で C++ コードをビルドするときに使用できる MSBuild タスクを確認します。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks specific to C++
ms.assetid: 05410f0c-7356-4692-bc00-20664421c9ff
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: b1d1a40c9e173ec6dd7cf07e0af0ca68f58efbb0
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93049038"
---
# <a name="msbuild-tasks-specific-to-c"></a>C++ に固有の MSBuild タスク

タスクでは、ビルド プロセスの間に実行するコードを指定します。 C++ がインストールされている場合、MSBuild と共にインストールされるタスクに加えて、以下のタスクを使用できます。 詳細については、「[MSBuild (C++) の概要](/cpp/build/msbuild-visual-cpp-overview)」を参照してください。

 タスクごとのパラメーターのほか、すべてのタスクに以下のパラメーターがあります。

| パラメーター | 説明 |
|-------------------| - |
| `Condition` | 省略可能な `String` 型のパラメーターです。<br /><br /> このタスクが実行されるかどうかを MSBuild エンジンが決定するために使用する `Boolean` 式です。 MSBuild でサポートされている条件について詳しくは、[条件](../msbuild/msbuild-conditions.md)に関する記事をご覧ください。 |
| `ContinueOnError` | 省略可能なパラメーター。 次の値のいずれかを含めることができます。<br /><br /> -   **WarnAndContinue** または **true** 。 タスクが失敗すると、[Target](../msbuild/target-element-msbuild.md) 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーが警告として扱われます。<br />-   **ErrorAndContinue** 。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。<br />-   **ErrorAndStop** または **false** (既定)。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。<br /><br /> バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。<br /><br /> 詳細については、「[方法:タスクで発生したエラーを無視する](../msbuild/how-to-ignore-errors-in-tasks.md)」を参照してください。 |

### <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[BscMake タスク](../msbuild/bscmake-task.md)|Microsoft Browse Information Maintenance Utility ツール ( *bscmake.exe* ) をラップします。|
|[CL タスク](../msbuild/cl-task.md)|C++ コンパイラ ツール ( *cl.exe* ) をラップします。|
|[CPPClean タスク](../msbuild/cppclean-task.md)|C++ プロジェクトのビルド時に MSBuild によって作成される一時ファイルを削除します。|
|[ClangCompile タスク](../msbuild/clangcompile-task.md)|C++ コンパイラ ツール ( *clang.exe* ) をラップします。|
|[CustomBuild タスク](../msbuild/custombuild-task.md)|C++ コンパイラ ツール ( *cmd.exe* ) をラップします。|
|[FXC タスク](../msbuild/fxc-task.md)|ビルド プロセスで HLSL シェーダー コンパイラを使用します。|
|[GetOutOfDateItems](../msbuild/getoutofdateitems-task.md)|古い tlog を読み取り、新しい tlog 書き込んで、最新ではない項目のセットを返します。 (ヘルパー タスク)|
|[GetOutputFileName](../msbuild/getoutputfilename-task.md)|cl や他のツールの出力ファイル名を取得します。これにより、出力ディレクトリのみを指定する、完全なファイル名を指定する、または何も指定しないことが可能になります。 (ヘルパー タスク)|
|[LIB タスク](../msbuild/lib-task.md)|Microsoft 32-Bit Library Manager ツール ( *lib.exe* ) をラップします。|
|[Link タスク](../msbuild/link-task.md)|C++ リンカー ツール ( *link.exe* ) をラップします。|
|[MIDL タスク](../msbuild/midl-task.md)|Microsoft インターフェイス定義言語 (MIDL: Microsoft Interface Definition Language) コンパイラ ツール ( *midl.exe* ) をラップします。|
|[MT タスク](../msbuild/mt-task.md)|Microsoft マニフェスト ツール ( *mt.exe* ) をラップします。|
|[MultiToolTask タスク](../msbuild/multitooltask-task.md)|説明なし。|
|[ParallelCustomBuild タスク](../msbuild/parallelcustombuild-task.md)|[CustomBuild タスク](../msbuild/custombuild-task.md)の並列インスタンスを実行します。|
|[RC タスク](../msbuild/rc-task.md)|Microsoft Windows リソース コンパイラ ツール ( *rc.exe* ) をラップします。|
|[SetEnv タスク](../msbuild/setenv-task.md)|指定された環境変数の値を設定または削除します。|
|[TrackedVCToolTask 基底クラス](../msbuild/trackedvctooltask-base-class.md)|[VCToolTask](../msbuild/vctooltask-base-class.md) から継承します。|
|[VCMessage タスク](../msbuild/vcmessage-task.md)|ビルド時の警告メッセージおよびエラー メッセージをログに記録します。 (拡張できません。 内部使用のみ。)|
|[VCToolTask 基底クラス](../msbuild/vctooltask-base-class.md)|[ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) から継承します。|
|[XDCMake タスク](../msbuild/xdcmake-task.md)|XML ドキュメント ツール ( *xdcmake.exe* ) をラップします。このツールは、XML ドキュメント コメント ( *.xdc* ) ファイルを *.xml* ファイルにマージします。|
|[XSD タスク](../msbuild/xsd-task.md)|ソースからスキーマまたはクラス ファイルを生成する XML スキーマ定義ツール ( *xsd.exe* ) をラップします。 *下記の「注意」を参照。*|
|[MSBuild リファレンス](../msbuild/msbuild-reference.md)|MSBuild システムの要素について説明します。|
|[タスク](../msbuild/msbuild-tasks.md)|タスクについて説明します。タスクはコードの単位であり、組み合わせることでビルドを生成できます。|
|[タスクの作成](../msbuild/task-writing.md)|タスクを作成する方法を説明します。|

> [!NOTE]
> Visual Studio 2017 以降では、C++ プロジェクトでの *xsd.exe* のサポートは非推奨です。 *CppCodeProvider.dll* を手動で GAC に追加して、 **Microsoft.VisualC.CppCodeProvider** API を引き続き使用することができます。
