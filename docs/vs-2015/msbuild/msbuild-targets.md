---
title: MSBuild ターゲット | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- MSBuild, targets
ms.assetid: 8060b4d2-e4a9-48cf-a437-852649ceb417
caps.latest.revision: 29
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c4cc8d9654fc2d277f0b7c69483ab46aa3209983
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157605"
---
# <a name="msbuild-targets"></a>MSBuild ターゲット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ターゲットはタスクを特定の順序でグループ化し、ビルド プロセスを小さな単位に分割することを可能にします。 たとえば、あるターゲットは、ビルドの準備として、出力ディレクトリに含まれるすべてのファイルを削除し、別のターゲットは、プロジェクトに対する入力をコンパイルし、空のディレクトリに配置します。 タスクについて詳しくは、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。  
  
## <a name="declaring-targets-in-the-project-file"></a>プロジェクト ファイルでターゲットを宣言する  
 ターゲットは、プロジェクト ファイル内で、[Target](../msbuild/target-element-msbuild.md) 要素を使用して宣言します。 たとえば、次の XML は Construct という名前のターゲットを作成し、Compile というアイテムの種類で Csc タスクを呼び出します。  
  
```  
<Target Name="Construct">  
    <Csc Sources="@(Compile)" />  
</Target>  
```  
  
 MSBuild プロパティと同様に、ターゲットは再定義できます。 たとえば、オブジェクトに適用された  
  
```  
<Target Name="AfterBuild" >  
    <Message Text="First occurrence" />  
</Target>  
<Target Name="AfterBuild" >  
    <Message Text="Second occurrence" />  
</Target>  
```  
  
 AfterBuild を実行すると、"Second occurrence" (2 番目の出現) のみが表示されます。  
  
## <a name="target-build-order"></a>ターゲットのビルド順序  
 あるターゲットへの入力が別のターゲットの出力に依存する場合、ターゲットの順序を指定する必要があります。 ターゲットの実行順序はいくつかの方法で指定できます。  
  
- 初期ターゲット  
  
- 既定のターゲット  
  
- 最初のターゲット  
  
- ターゲットの依存関係  
  
- `BeforeTargets` と `AfterTargets` (MSBuild 4.0)  
  
  1 つのビルドでターゲットが 2 回実行されることはありません。そのビルド内の後続のターゲットが先行するターゲットに依存している場合でも同じです。 ターゲットは一度実行されると、それ以上ビルドに影響しません。  
  
  ターゲットのビルド順序の詳細と詳細については、「 [ターゲットのビルド順序](../msbuild/target-build-order.md)」を参照してください。  
  
## <a name="target-batching"></a>ターゲットのバッチ  
 あるターゲット要素に、%(メタデータ) 形式でメタデータを指定する `Outputs` 属性が含まれている場合があります。 その場合、MSBuild は一意のメタデータ値ごとにターゲットを 1 回実行し、そのメタデータ値を含むアイテムをグループ化または "バッチ処理" します。 たとえば、オブジェクトに適用された  
  
```  
<ItemGroup>  
    <Reference Include="System.Core">  
      <RequiredTargetFramework>3.5</RequiredTargetFramework>  
    </Reference>  
    <Reference Include="System.Xml.Linq">  
      <RequiredTargetFramework>3.5</RequiredTargetFramework>  
    </Reference>  
    <Reference Include="Microsoft.CSharp">  
      <RequiredTargetFramework>4.0</RequiredTargetFramework>  
    </Reference>  
</ItemGroup>  
<Target Name="AfterBuild"  
    Outputs="%(Reference.RequiredTargetFramework)">  
    <Message Text="Reference:  
      @(Reference->'%(RequiredTargetFramework)')" />  
</Target>  
```  
  
 RequiredTargetFramework メタデータによって参照項目をバッチ処理します。 このターゲットの出力は次のようになります。  
  
```  
Reference: 3.5;3.5  
Reference: 4.0  
```  
  
 ターゲット バッチ処理が実際のビルドで利用されることはほとんどありません。 タスクのバッチが一般的です。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。  
  
## <a name="incremental-builds"></a>インクリメンタル ビルド  
 インクリメンタル ビルドは、対応する入力ファイルに対して最新の状態の出力ファイルを含むターゲットが実行されないように最適化されたビルドです。 ターゲット要素には、`Inputs` 属性と `Outputs` 属性の両方を含めることができます。ターゲットが入力として受け取る項目と出力として生成する項目をそれぞれ示します。  
  
 すべての出力項目が最新の状態になっている場合、MSBuild はターゲットをスキップします。これがビルドのスピードを大幅に上げます。 これはターゲットのインクリメンタル ビルドと呼ばれています。 一部のファイルだけが最新の状態になっている場合、MSBuild は最新の項目なしでターゲットを実行します。 これはターゲットの部分的インクリメンタル ビルドと呼ばれています。 詳しくは、「[インクリメンタル ビルド](../msbuild/incremental-builds.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [方法: 複数のプロジェクトファイルで同じターゲットを使用する](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)
