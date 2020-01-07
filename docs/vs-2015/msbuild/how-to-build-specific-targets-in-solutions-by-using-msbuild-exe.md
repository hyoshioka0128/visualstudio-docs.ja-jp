---
title: '方法: MSBuild.exe を使用してソリューション内の特定のターゲットをビルドする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, building specific targets in a solution
- msbuild.exe, building specific targets in a solution
- MSBuild, msbuild.exe
ms.assetid: f46feb9b-4c16-4fec-b6e1-36a959692ba3
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8bfef86b8ea82077ba7fe3f753f9835c06c3380a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156662"
---
# <a name="how-to-build-specific-targets-in-solutions-by-using-msbuildexe"></a>方法 : MSBuild.exe を使用してソリューション内の特定のターゲットをビルドする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild.exe 使用して、ソリューション内の特定のプロジェクトの特定のターゲットをビルドできます。  
  
### <a name="to-build-a-specific-target-of-a-specific-project-in-a-solution"></a>ソリューション内の特定のプロジェクトの特定のターゲットをビルドするには  
  
1. コマンド ラインで、`MSBuild.exe <SolutionName>.sln` と入力します。ここで `<SolutionName>` は実行するターゲットを含んでいるソリューションのファイル名に対応します。  
  
2. **/t** スイッチの後ろに、*ProjectName*:*TargetName* という形式でターゲットを指定します。  
  
## <a name="example"></a>例  
 次の例では、`NotInSlnFolder` プロジェクトの `Rebuild` ターゲットを実行してから、`NewFolder` ソリューション フォルダーにある `InSolutionFolder` プロジェクトの`Clean` ターゲットを実行します。  
  
```  
msbuild SlnFolders.sln /t:NotInSlnfolder:Rebuild;NewFolder\InSolutionFolder:Clean  
```  
  
## <a name="see-also"></a>関連項目
 [Command-Line Reference (コマンド ライン リファレンス)](../msbuild/msbuild-command-line-reference.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [MSBuild](msbuild.md)  
 [MSBuild の概念](../msbuild/msbuild-concepts.md)
