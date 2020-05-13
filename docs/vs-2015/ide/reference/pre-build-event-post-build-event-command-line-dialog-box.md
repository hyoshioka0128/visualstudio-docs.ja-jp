---
title: '[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
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
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b42c219620a669a8fa27a7ce847dc571a4075288
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662167"
---
# <a name="pre-build-eventpost-build-event-command-line-dialog-box"></a>[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

エディット ボックスに [[ビルド イベント] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-events-page-project-designer-csharp.md) のビルド前またはビルド後イベントを直接入力したり、使用できるマクロの一覧からビルド前およびビルド後のマクロを選択したりできます。

> [!NOTE]
> プロジェクトが最新の状態で、ビルドがトリガーされない場合、ビルド前イベントは実行されません。

## <a name="ui-element-list"></a>UI 要素の一覧
 **コマンドラインエディットボックス**ビルド前またはビルド後に実行するイベントを格納します。

> [!NOTE]
> .bat ファイルを実行するすべてのビルド後コマンドの前に `call` ステートメントを追加します。 たとえば、`call C:\MyFile.bat` または `call C:\MyFile.bat call C:\MyFile2.bat` のようにします。

 **マクロ**エディットボックスを展開して、[コマンドライン] ボックスに挿入するマクロの一覧を表示します。

 **マクロテーブル**使用できるマクロとその値を一覧表示します。 それぞれの詳細については、以下の「マクロ」を参照してください。 コマンド ライン エディット ボックスに挿入するマクロは、一度に 1 つだけ選択できます。

 **挿入**マクロテーブルで選択されたマクロをコマンドラインエディットボックスに挿入します。

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

## <a name="see-also"></a>参照
 [Visual Studio の [ビルドイベント] ページでカスタムビルドイベントを指定](../../ide/specifying-custom-build-events-in-visual-studio.md)する[(プロジェクトデザイナー) (C#)](../../ide/reference/build-events-page-project-designer-csharp.md) [方法: ビルドイベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md) [方法: ビルドイベントを指定する (C#)](../../ide/how-to-specify-build-events-csharp.md)
