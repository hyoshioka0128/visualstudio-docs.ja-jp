---
title: XSD タスク | Microsoft Docs
ms.date: 06/27/2018
ms.topic: reference
f1_keywords:
- vc.task.xsd
- VC.Project.VCXMLDataGeneratorTool.Namespace
- VC.Project.VCXMLDataGeneratorTool.GenerateFromSchema
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- XSD task (MSBuild (C++))
- MSBuild (C++), XSD task
ms.assetid: 15c99f5c-7124-4bbc-bc03-70c7bcce8893
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 217e045a731efa1fe3ba1dda63e89eca685d4b75
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77630783"
---
# <a name="xsd-task"></a>XSD タスク

ソースからスキーマまたはクラス ファイルを生成する XML スキーマ定義ツール (*xsd.exe*) をラップします。

> [!NOTE]
> Visual Studio 2017 以降では、C++ プロジェクトでの *xsd.exe* のサポートは非推奨です。 *CppCodeProvider.dll* を手動で GAC に追加して、**Microsoft.VisualC.CppCodeProvider** API を引き続き使用することができます。

## <a name="parameters"></a>パラメーター

 **XSD** タスクのパラメーターの説明を次の表に示します。

- **AdditionalOptions**

     省略可能な **String** 型のパラメーターです。

     コマンド ラインで指定するオプションのリストです。 例: /\<option1> /\<option2> /\<option#> 他の **XSD** タスク パラメーターでは表されないオプションを指定する場合は、このパラメーターを使用します。

- **GenerateFromSchema**

  省略可能な **String** 型のパラメーターです。

  指定したスキーマから生成される種類を指定します。

  次のいずれかの値を指定します。各値は XSD オプションに対応しています。

  - **classes** -  **/classes**

  - **dataset** -  **/dataset**

- **Language**

     省略可能な **String** 型のパラメーターです。

     生成されたコードに使用するプログラミング言語を指定します。

     **CS** (C#、既定)、**VB** (Visual Basic)、または **JS** (JScript) のいずれかを選択します。 `System.CodeDom.Compiler.CodeDomProvider Class` を実装するクラスの完全修飾名を指定することもできます。

- **Namespace**

     省略可能な **String** 型のパラメーターです。

     生成する型のランタイム名前空間を指定します。

- **Sources**

     必須の `ITaskItem[]` 型のパラメーターです。

     タスクで使用および生成できる MSBuild ソース ファイル アイテムの配列を定義します。

- **SuppressStartupBanner**

     省略可能な **Boolean** 型のパラメーターです。

     `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。

- **TrackerLogDirectory**

     省略可能な **String** 型のパラメーターです。

     トラッカー ログのディレクトリを指定します。

## <a name="see-also"></a>参照

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
