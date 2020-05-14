---
title: インクリメンタル ビルド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, incremental builds
ms.assetid: 325e28c7-4838-4e3f-b672-4586adc7500c
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eb11467d8d59e7af11741d7719da2858ac1a784c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192880"
---
# <a name="incremental-builds"></a>インクリメンタル ビルド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

インクリメンタル ビルドは、対応する入力ファイルに対して最新の状態の出力ファイルを含むターゲットが実行されないように最適化されたビルドです。 ターゲット要素には、ターゲットが入力として受け取る項目を示す `Inputs` 属性と、ターゲットが出力として生成する項目を示す `Outputs` 属性の両方を指定できます。 MSBuild は、これらの属性の値間に一対一の対応関係があるかどうかを確認します。 一対一の対応関係が存在する場合、MSBuild は、すべての入力項目のタイム スタンプをそれぞれ対応する出力項目のタイム スタンプと比較します。 一対一の対応関係が存在しない出力ファイルは、すべての入力ファイルと比較されます。 項目が最新の状態であると見なされるのは、その出力ファイルが入力ファイルと同じタイム スタンプであるかそれよりも新しい場合です。  
  
 すべての出力項目が最新の状態である場合、MSBuild はターゲットをスキップします。 このターゲットの*インクリメンタル ビルド*により、ビルド速度が大幅に向上します。 一部のファイルだけが最新の状態である場合、MSBuild は最新の項目をスキップしてターゲットを実行するので、すべての項目が最新の状態になります。 これは、*部分インクリメンタル ビルド*と呼ばれます。  
  
 一対一の対応関係は、通常は項目の変換によって生成されます。 詳細については、「[MSBuild 変換](../msbuild/msbuild-transforms.md)」をご覧ください。  
  
 次にターゲットの例を示します。  
  
```  
<Target Name="Backup" Inputs="@(Compile)"   
    Outputs="@(Compile->'$(BackupFolder)%(Identity).bak')">  
    <Copy SourceFiles="@(Compile)" DestinationFiles=  
        "@(Compile->'$(BackupFolder)%(Identity).bak')" />  
</Target>  
```  
  
 `Compile` 項目の種類によって表されるファイル セットは、バックアップ ディレクトリにコピーされます。 バックアップ ファイル名の拡張子は .bak です。 `Compile` 項目の種類によって表されるファイル (対応するバックアップ ファイル) が Backup ターゲットの実行後に削除または変更されない場合、Backup ターゲットは以降のビルドでスキップされます。  
  
## <a name="output-inference"></a>出力の推論  
 MSBuild は、ターゲットの `Inputs` 属性と `Outputs` 属性を比較して、ターゲットを実行する必要があるかどうかを判断します。 インクリメンタル ビルドが完了した後に存在するファイル セットが、関連するターゲットが実行されるかどうかにかかわらず、同じままであることが理想的です。 タスクによって作成または変更されるプロパティと項目はビルドに影響する可能性があるため、プロパティと項目に影響するターゲットがスキップされる場合でも MSBuild はそれらの値を推論する必要があります。 これは、*出力の推論*と呼ばれます。  
  
 次の 3 つの場合があります。  
  
- ターゲットに `Condition` と評価される `false` 属性が指定されている場合。 この場合、ターゲットは実行されず、ビルドには影響しません。  
  
- ターゲットに古い出力があり、ターゲットを実行して最新の状態にする場合。  
  
- ターゲットに古い出力がなく、ターゲットがスキップされる場合。 MSBuild はターゲットを評価し、ターゲットが実行された場合と同じように項目とプロパティを変更します。  
  
  インクリメンタル コンパイルをサポートするために、タスクでは `TaskParameter` 要素の `Output` 属性値がタスク入力パラメーターと等しいことを確認する必要があります。 次にいくつかの例を示します。  
  
```  
<CreateProperty Value="123">  
    <Output PropertyName="Easy" TaskParameter="Value" />  
</CreateProperty>  
```  
  
 これにより、ターゲットが実行またはスキップされるかどうかにかかわらず、値が "123" の Easy プロパティが作成されます。  
  
```  
<CreateItem Include="a.cs;b.cs">  
    <Output ItemName="Simple" TaskParameter="Include" />  
</CreateItem>  
```  
  
 これにより、ターゲットが実行またはスキップされるかどうかにかかわらず、"a.cs" と "b.cs" の 2 つの項目を持つ、項目の種類 Simple が作成されます。  
  
 MSBuild 3.5 以降では、ターゲットの項目グループとプロパティ グループに対して、出力の推論が自動的に実行されます。 `CreateItem` タスクはターゲットでは必要でないため、使用しないようにしてください。 また、`CreateProperty` タスクは、ターゲットが実行されたかどうかを確認する場合にのみターゲットで使用するようにしてください。  
  
## <a name="determining-whether-a-target-has-been-run"></a>ターゲットが実行されたかどうかの確認  
 出力の推論のため、ターゲットが実行されたかどうかを確認できるように、`CreateProperty` タスクをターゲットに追加してプロパティと項目を調べる必要があります。 `CreateProperty` タスクをターゲットに追加し、`Output` が "ValueSetByTask" である `TaskParameter` 要素を指定します。  
  
```  
<CreateProperty Value="true">  
    <Output TaskParameter="ValueSetByTask" PropertyName="CompileRan" />  
</CreateProperty>  
```  
  
 これにより、ターゲットが実行された場合にのみ、CompileRan プロパティが作成され、値 `true` が指定されます。 ターゲットがスキップされた場合、CompileRan は作成されません。  
  
## <a name="see-also"></a>関連項目
 [ターゲット](../msbuild/msbuild-targets.md)
