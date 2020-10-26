---
title: MSBuild 応答ファイル | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- response files, MSBuild
- MSBuild, response files
- MSBuild, .rsp files
- .rsp files
ms.assetid: 9f53987b-20ee-470a-ab62-fce997bb5e15
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a1ce11edac37368b9c4993a87a8c2b3e734b7862
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189380"
---
# <a name="msbuild-response-files"></a>MSBuild 応答ファイル
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

応答 (.rsp) ファイルは、MSBuild.exe のコマンド ライン スイッチを含むテキスト ファイルです。 各スイッチを個別の行に記述することも、すべてのスイッチを 1 つの行に記述することもできます。 コメント行は **#** 記号で始まります。 スイッチは、 **@** 別の応答ファイルを MSBuild.exe に渡すために使用されます。  
  
 自動応答ファイルは、プロジェクトをビルドする際に MSBuild.exe が自動的に使用する特別な .rsp ファイルです。 この MSBuild.rsp ファイルは、MSBuild.exe と同じディレクトリに配置する必要があります。それ以外の場合は検出されません。 このファイルを編集して、MSBuild.exe に既定のコマンド ライン スイッチを指定できます。 たとえば、プロジェクトをビルドするたびに同じ logger を使用する場合、 **/logger** スイッチを msbuild.exe に追加する MSBuild.exe と、プロジェクトがビルドされるたびに logger が使用されます。  
  
## <a name="see-also"></a>参照  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [コマンドラインリファレンス](../msbuild/msbuild-command-line-reference.md)
