---
title: プロパティと項目の比較 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, msbuild properties
ms.assetid: b9da45ae-d6a6-4399-8628-397deed31486
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 66fc8065e81b8b93e73ec034a166e3d5645d4b6b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184089"
---
# <a name="comparing-properties-and-items"></a>プロパティと項目の比較
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild のプロパティと項目は、いずれもタスクに情報を渡し、条件を評価し、プロジェクト ファイルで参照する値を格納しておくために使用されます。  
  
- プロパティは名前と値のペアです。 詳細については、「[MSBuild プロパティ](msbuild-properties1.md)」を参照してください。  
  
- 項目は、一般的にファイルを示すオブジェクトです。 項目オブジェクトには、メタデータ コレクションを関連付けることができます。 メタデータは名前と値のペアです。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。  
  
## <a name="scalars-and-vectors"></a>スカラーとベクター  
 MSBuild プロパティは 1 つの文字列値のみを持つ名前と値のペアなので、多くの場合は*スカラー*と説明されます。 MSBuild 項目の種類は項目のリストなので、多くの場合は*ベクター*と説明されます。 ただし実際には、プロパティで複数の値を表すことがあり、項目の種類の項目数が 0 個または 1 個の場合があります。  
  
### <a name="target-dependency-injection"></a>ターゲットの依存関係の挿入  
 プロパティが複数の値を表す方法については、ターゲットをターゲットの一覧に追加して一覧を作成する場合の一般的な使用パターンを考えます。 この一覧は、一般的に、プロパティ値とターゲット名をセミコロン (;) で区切って表します。  
  
```  
<PropertyGroup>  
    <BuildDependsOn>  
        BeforeBuild;  
        CoreBuild;  
        AfterBuild  
    </BuildDependsOn>  
</PropertyGroup>  
```  
  
 通常、`BuildDependsOn` プロパティは、ターゲットの `DependsOnTargets` 属性の引数として使用され、項目一覧に変換されます。 このプロパティをオーバーライドして、ターゲットを追加したり、ターゲットの実行順を変更したりすることができます。 たとえば、オブジェクトに適用された  
  
```  
<PropertyGroup>  
    <BuildDependsOn>  
        $(BuildDependsOn);  
        CustomBuild;  
    </BuildDependsOn>  
</PropertyGroup>  
```  
  
 CustomBuild ターゲットをターゲット一覧に追加し、`BuildDependsOn` に値 `BeforeBuild;CoreBuild;AfterBuild;CustomBuild` を付与します。  
  
 MSBuild 4.0 以降、ターゲットの依存関係の挿入は非推奨とされます。 代わりに `AfterTargets` 属性と `BeforeTargets` 属性を使用してください。 詳細については、「[ターゲットのビルド順序](../msbuild/target-build-order.md)」を参照してください。  
  
### <a name="conversions-between-strings-and-item-lists"></a>文字列と項目一覧との変換  
 MSBuild は、項目の種類と文字列値の変換を必要に応じて実行します。 項目一覧を文字列値にする方法については、MSBuild プロパティの値として項目の種類を使用すると何が起こるかを考えます。  
  
```  
<ItemGroup>  
    <OutputDir Include="KeyFiles\;Certificates\" />  
  </ItemGroup>  
<PropertyGroup>  
    <OutputDirList>@(OutputDir)</OutputDirList>  
</PropertyGroup>  
```  
  
 項目の種類 OutputDir には、"KeyFiles\\;Certificates\\" という値の `Include` 属性があります。 MSBuild は、この文字列を 2 つの項目 KeyFiles\ と Certificates\\ に解析します。 項目の種類 OutputDir を OutputDirList プロパティの値として使用している場合、MSBuild は、項目の種類をセミコロン区切りの文字列 "KeyFiles\\;Certificates\\" に変換または "平坦化" します。  
  
## <a name="properties-and-items-in-tasks"></a>タスクのプロパティと項目  
 プロパティと項目は、MSBuild タスクの入力と出力として使用されます。 詳細については、[タスク](../msbuild/msbuild-tasks.md)に関する記事を参照してください。  
  
 プロパティは属性としてタスクに渡されます。 タスク内の MSBuild プロパティは、値を文字列との間で変換できるプロパティの種類で表されます。 サポートされるプロパティの種類には、`bool`、`char`、`DateTime`、`Decimal`、`Double`、`int`、`string` に加え、<xref:System.Convert.ChangeType%2A> が処理できるあらゆる種類が含まれます。  
  
 項目は <xref:Microsoft.Build.Framework.ITaskItem> オブジェクトとしてタスクに渡されます。 タスク内では、<xref:Microsoft.Build.Framework.ITaskItem.ItemSpec%2A> は項目の値を表し、<xref:Microsoft.Build.Framework.ITaskItem.GetMetadata%2A> はそのメタデータを取得します。  
  
 項目の種類の項目一覧は、`ITaskItem` オブジェクトの配列として渡すことができます。 .NET Framework 3.5 以降、`Remove` 属性を使用してターゲットの項目一覧から項目を削除できるようになりました。 項目は項目一覧から削除できるため、アイテムの種類の項目数が 0 個になる可能性があります。 項目一覧をタスクに渡す場合、タスクのコードでこの可能性をチェックする必要があります。  
  
## <a name="property-and-item-evaluation-order"></a>プロパティと項目の評価順序  
 ビルドの評価フェーズでは、インポート対象のファイルは出現順にビルドに組み込まれます。 プロパティと項目は、次の順に 3 つのパスで定義されます。  
  
- プロパティが出現順に定義および修正されます。  
  
- 項目定義が出現順に定義および修正されます。  
  
- 項目が出現順に定義および修正されます。  
  
  ビルドの実行フェーズでは、ターゲット内で定義されるプロパティおよび項目は、出現順に、1 つの段階でまとめて評価されます。  
  
  ただし、これだけでは済みません。 プロパティ、項目定義、または項目を定義するときに、その値も評価されます。 式エバリュエーターで、値を指定する文字列が展開されます。 文字列の展開はビルド フェーズによって変わります。 プロパティと項目の詳細な評価順は次のとおりです。  
  
- ビルドの評価フェーズ:  
  
  - プロパティが出現順に定義および修正されます。 プロパティ関数が実行されます。 式内のフォーム $(PropertyName) のプロパティ値が展開されます。 プロパティ値が展開された式に設定されます。  
  
  - 項目定義が出現順に定義および修正されます。 式内のプロパティ関数は既に展開されています。 メタデータ値が展開された式に設定されます。  
  
  - 項目の種類が出現順に定義および修正されます。 フォーム @(ItemType) の項目値が展開されます。 項目の変換も展開されます。 式内のプロパティ関数と値は既に展開されています。 項目一覧とメタデータ値が展開された式に設定されます。  
  
- ビルドの実行フェーズ:  
  
  - ターゲット内に定義されているプロパティと項目は、出現順にまとめて評価されます。 プロパティ関数が実行され、式内のプロパティ値が展開されます。 項目値と項目の変換も展開されます。 プロパティ値、項目の種類値、およびメタデータ値が、展開された式に設定されます。  
  
### <a name="subtle-effects-of-the-evaluation-order"></a>評価順のわかりにくい効果  
 ビルドの評価フェーズでは、プロパティの評価が項目の評価よりも先に実行されます。 それでも、プロパティ値が項目値に依存しているように見えることがあります。 次のスクリプトがあるとします。  
  
```  
<ItemGroup>  
    <KeyFile Include="KeyFile.cs">  
        <Version>1.0.0.3</Version>  
    </KeyFile>  
</ItemGroup>  
<PropertyGroup>  
    <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>  
</PropertyGroup>  
<Target Name="AfterBuild">  
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />  
</Target>  
```  
  
 Message タスクを実行すると、次のメッセージが表示されます。  
  
```  
KeyFileVersion: 1.0.0.3  
```  
  
 これは、`KeyFileVersion` の値が実際には文字列 "@(KeyFile->'%(Version)')" であるためです。 プロパティが最初に定義されたときに項目と項目の変換が展開されなかったため、`KeyFileVersion` プロパティには展開されていない文字列値が割り当てられました。  
  
 ビルドの実行フェーズで Message タスクを処理するときに、MSBuild は文字列 "@(KeyFile->'%(Version)')" を展開して "1.0.0.3" を生成します。  
  
 プロパティと項目グループの順序が変わった場合でも、同じメッセージが表示されます。  
  
 2 つ目の例として、プロパティと項目グループがターゲット内にあるときに生じる状況を考えてみましょう。  
  
```  
<Target Name="AfterBuild">  
    <PropertyGroup>  
        <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>  
    </PropertyGroup>  
    <ItemGroup>  
        <KeyFile Include="KeyFile.cs">  
            <Version>1.0.0.3</Version>  
        </KeyFile>  
    </ItemGroup>  
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />  
</Target>  
```  
  
 Message タスクを実行すると、次のメッセージが表示されます。  
  
```  
KeyFileVersion:   
```  
  
 これは、ビルドの実行フェーズ中に、ターゲット内で定義されているプロパティと項目グループが上から下の順にまとめて評価されるためです。 `KeyFileVersion` の定義時に `KeyFile` は不明です。 そのため、項目の変換によって空の文字列に展開されます。  
  
 この場合、プロパティと項目グループの順序を逆にすることで、元のメッセージが復元されます。  
  
```  
<Target Name="AfterBuild">  
    <ItemGroup>  
        <KeyFile Include="KeyFile.cs">  
            <Version>1.0.0.3</Version>  
        </KeyFile>  
    </ItemGroup>  
    <PropertyGroup>  
        <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>  
    </PropertyGroup>  
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />  
</Target>  
```  
  
 `KeyFileVersion` の値は "@(KeyFile->'%(Version)')" ではなく "1.0.0.3" に設定されます。 Message タスクを実行すると、次のメッセージが表示されます。  
  
```  
KeyFileVersion: 1.0.0.3  
```  
  
## <a name="see-also"></a>関連項目
 [詳細な概念](../msbuild/msbuild-advanced-concepts.md)
