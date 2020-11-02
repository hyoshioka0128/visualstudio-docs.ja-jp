---
title: '方法: タスクで発生したエラーを無視する | Microsoft Docs'
description: MSBuild タスクで発生したエラーを無視し、タスクが失敗したときにビルドを停止するか続行するかを制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, ignoring errors
- ContinueOnError attribute [MSBuild]
ms.assetid: e2f1ca4f-787b-44bd-bc64-81a036025e96
author: ghogen
ms.author: ghogen
manager: jillfra
ms.openlocfilehash: 97a2666b32ad7e6bc93865fa36529377652b6453
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436250"
---
# <a name="how-to-ignore-errors-in-tasks"></a>方法: タスクで発生したエラーを無視する

ビルド時に一部のタスクのエラーを許容するとよい場合があります。 そのような重要でないタスクが失敗しても必要な出力は生成できるため、ビルドを続行させる場合です。 たとえば、各コンポーネントのビルド後にプロジェクトで `SendMail` タスクを使ってメール メッセージを送信する場合、メール サーバーが利用できず、ステータス メッセージを送信できなくても、完了までビルドを続行させるのは許容範囲と見なせる場合があります。 別の例として、通常、ビルド中に中間ファイルが削除される場合、それらのファイルを削除できなくても、完了までビルドを続行させるのは許容範囲と見なせる場合があります。

## <a name="use-the-continueonerror-attribute"></a>ContinueOnError 属性を使用する

`Task` 要素の `ContinueOnError` 属性は、タスク エラーの発生時にビルドを停止するか続行するかを制御します。 この属性は、ビルドを続行するときに、エラーをエラーとして扱うか、それとも警告として扱うかも制御します。

`ContinueOnError` 属性には、次の値のいずれかを含めることができます。

- **WarnAndContinue** または **true** 。 タスクが失敗すると、[Target](../msbuild/target-element-msbuild.md) 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーが警告として扱われます。

- **ErrorAndContinue** 。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。

- **ErrorAndStop** または **false** (既定値)。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。

バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。

`ContinueOnError` の既定値は `ErrorAndStop`です。 属性を `ErrorAndStop` に設定すると、プロジェクト ファイルを読むユーザーにとって動作は明確になります。

#### <a name="to-ignore-an-error-in-a-task"></a>タスクのエラーを無視するには

タスクの `ContinueOnError` 属性を使用します。 次に例を示します。

```xml
<Delete Files="@(Files)" ContinueOnError="WarnAndContinue"/>
```

## <a name="example"></a>例

次のコード例は、`Delete` タスクが失敗した場合でも `Build` ターゲットが実行され続け、ビルドが成功したと見なされることを示します。

```xml
<Project DefaultTargets="FakeBuild"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <Files Include="*.obj"/>
    </ItemGroup>
    <Target Name="Clean">
        <Delete Files="@(Files)" ContinueOnError="WarnAndContinue"/>
    </Target>

    <Target Name="FakeBuild" DependsOnTargets="Clean">
        <Message Text="Building after cleaning..."/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [MSBuild](../msbuild/msbuild.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [タスク](../msbuild/msbuild-tasks.md)
