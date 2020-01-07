---
title: '[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEventsBuilder
- vb.ProjectPropertiesBuildEventsBuilder
helpviewer_keywords:
- $(SolutionExt)
- $(ProjectDir)
- $(TargetPath)
- $(ProjectExt)
- $(TargetFileName)
- $(PlatformName)
- $(SolutionName)
- macros, build events
- $(SolutionPath)
- $(ProjectPath)
- $(ProjectFileName)
- $(DevEnvDir)
- $(TargetName)
- $(TargetDir)
- $(SolutionDir)
- $(TargetExt)
- $(OutDir)
- $(ConfigurationName)
- $(SolutionFileName)
- $(ProjectName)
- build events, macros
ms.assetid: d49b2c57-24bf-4fb2-8351-5c4b6cca938f
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d5671a75a847d81caedeffc17ea436eade060f3e
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461320"
---
# <a name="pre-build-eventpost-build-event-command-line-dialog-box"></a>[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス

エディット ボックスに [[ビルド イベント] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-events-page-project-designer-csharp.md) のビルド前またはビルド後イベントを直接入力したり、使用できるマクロの一覧からビルド前およびビルド後のマクロを選択したりできます。

> [!NOTE]
> プロジェクトが最新の状態で、ビルドがトリガーされない場合、ビルド前イベントは実行されません。

## <a name="ui-element-list"></a>UI 要素の一覧

**コマンド ライン エディット ボックス**

ビルド前またはビルド後に実行するイベントが含まれます。

> [!NOTE]
> .bat ファイルを実行するすべてのビルド後コマンドの前に `call` ステートメントを追加します。 たとえば、`call C:\MyFile.bat` または `call C:\MyFile.bat call C:\MyFile2.bat` のようにします。

**[マクロ]**

エディット ボックスを展開して、コマンド ライン エディット ボックスに挿入するマクロの一覧を表示します。

**[マクロ テーブル]**

使用可能なマクロとその値を一覧表示します。 それぞれの詳細については、以下の「マクロ」を参照してください。 コマンド ライン エディット ボックスに挿入するマクロは、一度に 1 つだけ選択できます。

**[挿入]**

マクロ テーブルで選択したマクロをコマンド ライン エディット ボックスに挿入します。

### <a name="macros"></a>[マクロ]

次のマクロのいずれかを使用して、ファイルの位置を指定したり、複数の選択肢がある場合に入力ファイルの実際の名前を取得したりできます。 これらのマクロの大文字と小文字は区別されません。

|マクロ|説明|
|-----------|-----------------|
|`$(ConfigurationName)`|現在のプロジェクト構成の名前 ("Debug" など)。|
|`$(OutDir)`|プロジェクト ディレクトリに対して相対的な、出力ファイル ディレクトリへのパス。 これは、Output Directory プロパティの値に解決されます。 最後に円記号 (\\) が含まれます。|
|`$(DevEnvDir)`|Visual Studio のインストール ディレクトリ (ドライブとパスで定義)。最後に円記号 (\\) が含まれます。|
|`$(PlatformName)`|現在対象となっているプラットフォームの名前。 たとえば、"AnyCPU" です。|
|`$(ProjectDir)`|プロジェクトのディレクトリ (ドライブとパスで定義)。最後に円記号 (\\) が含まれます。|
|`$(ProjectPath)`|プロジェクトの絶対パス名 (ドライブ、パス、基本名、およびファイル拡張子で定義)。|
|`$(ProjectName)`|プロジェクトの基本名です。|
|`$(ProjectFileName)`|プロジェクトのファイル名 (基本名とファイル拡張子で定義)。|
|`$(ProjectExt)`|プロジェクトのファイル拡張子。 ファイル拡張子の前にピリオド '.' が付きます。|
|`$(SolutionDir)`|ソリューションのディレクトリ (ドライブとパスで定義)。最後に円記号 (\\) が含まれます。|
|`$(SolutionPath)`|ソリューションの絶対パス名 (ドライブ、パス、基本名、およびファイル拡張子で定義)。|
|`$(SolutionName)`|ソリューションの基本名です。|
|`$(SolutionFileName)`|ソリューションのファイル名 (基本名とファイル拡張子で定義)。|
|`$(SolutionExt)`|ソリューションのファイル拡張子です。 ファイル拡張子の前にピリオド '.' が付きます。|
|`$(TargetDir)`|ビルドのプライマリ出力ファイルのディレクトリ (ドライブとパスで定義)。 最後に円記号 (\\) が含まれます。|
|`$(TargetPath)`|ビルドのプライマリ出力ファイルの絶対パス名 (ドライブ、パス、基本名、およびファイル拡張子で定義)。|
|`$(TargetName)`|ビルドのプライマリ出力ファイルの基本名です。|
|`$(TargetFileName)`|ビルドのプライマリ出力ファイルのファイル名 (基本名とファイル拡張子で定義)。|
|`$(TargetExt)`|ビルドのプライマリ出力ファイルのファイル拡張子。 ファイル拡張子の前にピリオド '.' が付きます。|

## <a name="see-also"></a>関連項目

- [Visual Studio でのカスタム ビルド イベントの指定](../../ide/specifying-custom-build-events-in-visual-studio.md)
- [[ビルド イベント] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-events-page-project-designer-csharp.md)
- [方法: ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [方法: ビルド イベントを指定する (C#)](../../ide/how-to-specify-build-events-csharp.md)
