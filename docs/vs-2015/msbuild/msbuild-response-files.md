---
title: MSBuild 応答ファイル | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
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
manager: ghogen
ms.openlocfilehash: 09271f90eb0b065df6c6f28bc318509d7141a252
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49242295"
---
# <a name="msbuild-response-files"></a>MSBuild 応答ファイル
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
応答 (.rsp) ファイルは、MSBuild.exe のコマンド ライン スイッチを含むテキスト ファイルです。 各スイッチを個別の行に記述することも、すべてのスイッチを 1 つの行に記述することもできます。 コメント行は **#** 記号で始まります。 **@** スイッチは、MSBuild.exe に別の応答ファイルを渡すために使用されます。  
  
 自動応答ファイルは、プロジェクトをビルドする際に MSBuild.exe が自動的に使用する特別な .rsp ファイルです。 この MSBuild.rsp ファイルは、MSBuild.exe と同じディレクトリに配置する必要があります。それ以外の場合は検出されません。 このファイルを編集して、MSBuild.exe に既定のコマンド ライン スイッチを指定できます。 たとえば、プロジェクトをビルドする際に毎回同じロガーを使用する場合は、**/logger** スイッチを MSBuild.rsp に追加することで、プロジェクトがビルドされるたびに MSBuild.exe がそのロガーを使用するようになります。  
  
## <a name="see-also"></a>関連項目  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [Command-Line Reference (コマンド ライン リファレンス)](../msbuild/msbuild-command-line-reference.md)



