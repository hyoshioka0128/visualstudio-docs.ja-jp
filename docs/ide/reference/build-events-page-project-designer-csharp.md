---
title: '[ビルド イベント] ページ (プロジェクト デザイナー) (C#)'
ms.date: 10/17/2019
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 4842a5a08de96cd40a45d0765d427cc74cbf5432
ms.sourcegitcommit: ba0fef4f5dca576104db9a5b702670a54a0fcced
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73714383"
---
# <a name="build-events-page-project-designer-c"></a>[ビルド イベント] ページ (プロジェクト デザイナー) (C#)

**プロジェクト デザイナー**の **[ビルド イベント]** ページを使用して、ビルド構成の手順を指定します。 また、あらゆるビルド後イベントを実行する条件を指定することもできます。 詳細については、[ビルド イベントを指定する (C#)](../../ide/how-to-specify-build-events-csharp.md)」および「[方法: ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)」を参照してください。

## <a name="uielement-list"></a>UIElement の一覧

**構成**

このコントロールは、このページでは編集できません。 このコントロールの詳細については、「[[ビルド] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-page-project-designer-csharp.md)」を参照してください。

**プラットフォーム**

このコントロールは、このページでは編集できません。 このコントロールの詳細については、「[[ビルド] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-page-project-designer-csharp.md)」を参照してください。

**ビルド前に実行するコマンド ライン**

ビルド開始前に実行する任意のコマンドを指定します。 長いコマンドを入力するには、 **[ビルド前の編集]** をクリックして [[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)を表示します。

> [!NOTE]
> プロジェクトが最新の状態で、ビルドがトリガーされない場合、ビルド前イベントは実行されません。

**ビルド後に実行するコマンド ライン**

ビルド終了後に実行する任意のコマンドを指定します。 長いコマンドを入力するには、 **[ビルド後の編集]** をクリックして **[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス**を表示します。

> [!NOTE]
> .bat ファイルを実行するすべてのビルド後コマンドの前に `call` ステートメントを追加します。 たとえば、`call C:\MyFile.bat` または `call C:\MyFile.bat call C:\MyFile2.bat` のようにします。

**ビルド後イベントの実行**

次の表に示すように、実行するビルド後イベントの条件を指定します。

|オプション|結果|
|------------|------------|
|**常時**|ビルド後イベントは、ビルドが成功したかどうかに関係なく実行されます。|
|**ビルドが成功したとき**|ビルド後イベントは、ビルドが成功した場合に実行されます。 したがって、ビルドが成功した場合は、最新のプロジェクトについてもイベントが実行されます。|
|**ビルドがプロジェクト出力を更新したとき**|ビルド後イベントは、コンパイラの出力ファイル (.exe または .dll) が以前のコンパイラの出力ファイルと異なる場合にのみ実行されます。 したがって、ビルド後イベントは、プロジェクトが最新の場合は実行されません。|

## <a name="in-the-project-file"></a>プロジェクト ファイルで

以前のバージョンの Visual Studio では、IDE で **PreBuildEvent** または **PostBuildEvent** の設定を変更すると、Visual Studio によってプロジェクト ファイルに `PreBuildEvent` または `PostBuildEvent` プロパティが追加されます。 たとえば、IDE で **PreBuildEvent** のコマンド ラインの設定が次のようになっているとします。

```input
"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)"
```

この場合、プロジェクト ファイルの設定は次のようになります。

```xml
<PropertyGroup>
    <PreBuildEvent>"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)" />
</PropertyGroup>
```

.NET Core プロジェクトでは、Visual Studio 2019 (および最近の更新プログラムでの Visual Studio 2017) では、**PreBuildEvent** および **PostBuildEvent** の設定に対して、`PreBuild` または `PostBuild` という名前の MSBuild ターゲットが追加されます。 これらのターゲットは、MSBuild によって認識される、**BeforeTargets** と **AfterTargets** の属性を使用します。 たとえば、前の例では、Visual Studio によって次のコードが生成されるようになりました。

```xml
<Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="&quot;$(ProjectDir)PreBuildEvent.bat&quot; &quot;$(ProjectDir)..\&quot; &quot;$(ProjectDir)&quot; &quot;$(TargetDir)&quot;" />
</Target>
```

ビルド後のイベントの場合は、`PostBuild` の名前を使用して、属性 `AfterTargets` を `PostBuildEvent` に設定します。

```xml
<Target Name="PostBuild" AfterTargets="PostBuildEvent">
   <Exec Command="echo Output written to $(TargetDir)" />
</Target>
```

> [!NOTE]
> これらのプロジェクト ファイルの変更は、SDK スタイルのプロジェクトをサポートするために行われました。 プロジェクト ファイルを古い形式から SDK スタイルの形式に手動で移行する場合は、`PreBuildEvent` および `PostBuildEvent` プロパティを削除し、前のコードで示されているように `PreBuild` および `PostBuild` ターゲットで置き換える必要があります。 プロジェクトが SDK スタイルのプロジェクトであるかどうかを確認する方法については、[プロジェクトの形式の確認](/nuget/resources/check-project-format)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [方法: ビルド イベントを指定する (C#)](../../ide/how-to-specify-build-events-csharp.md)
- [プロジェクトのプロパティのリファレンス](../../ide/reference/project-properties-reference.md)
- [コードのコンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)
