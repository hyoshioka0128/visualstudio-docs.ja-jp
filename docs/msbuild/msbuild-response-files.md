---
title: MSBuild 応答ファイル | Microsoft Docs
ms.date: 11/04/2016
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44d6e3c77fee53b15ec8d18cb74fd7355ee101a8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89315149"
---
# <a name="msbuild-response-files"></a>MSBuild 応答ファイル

応答 ( *.rsp*) ファイルは、*MSBuild.exe* のコマンド ライン スイッチを含むテキスト ファイルです。 各スイッチを個別の行に記述することも、すべてのスイッチを 1 つの行に記述することもできます。 コメント行は **#** 記号で始まります。 **@** スイッチは、*MSBuild.exe* に別の応答ファイルを渡すために使用されます。

## <a name="msbuildrsp"></a>MSBuild.rsp

自動応答ファイルは、プロジェクトをビルドする際に *MSBuild.exe* によって自動的に使用される特別な *.rsp* ファイルです。 この *MSBuild.rsp* ファイルは、*MSBuild.exe* と同じディレクトリに配置する必要があります。それ以外の場合は検出されません。 このファイルを編集して、既定のコマンド ライン スイッチを *MSBuild.exe* に指定できます。 たとえば、プロジェクトをビルドする際に毎回同じロガーを使用する場合は、 **-logger** スイッチを *MSBuild.rsp* に追加することで、プロジェクトをビルドするたびに *MSBuild.exe* でそのロガーが使用されるようになります。

## <a name="directorybuildrsp"></a>Directory.Build.rsp

バージョン 15.6 以降では、MSBuild は、プロジェクトの親ディレクトリで *Directory.Build.rsp* という名前のファイルを検索します。  これは、ソース コード リポジトリでコマンド ライン ビルド中に既定の引数を指定する場合に役立つことがあります。  ホスト型ビルドのコマンド ライン引数を指定する場合にも使用できます。

## <a name="see-also"></a>参照

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)
