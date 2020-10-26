---
title: DslTextTransform コマンド
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 32c01401eda8fb1bbe2bdcfc2950a51b968e98b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "76114903"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform コマンド
DslTextTransform は TextTransform.exe を呼び出し、共通オプションを使用して実行するスクリプトです。 DslTextTransformation を使用すると、プロジェクトの夜間ビルドを自動化でき [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] ます。 詳細については、「 [TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md)」を参照してください。

 DslTextTransform は、次のディレクトリにあります。

 **\<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin**

 DslTextTransform への入力として、次の引数を指定できます。

- ドメインモデルプロジェクトの出力ディレクトリ。

- デザイナー定義プロジェクトの出力ディレクトリ。

- テキストテンプレートファイルの場所。

  DslTextTransform は、既定のディレクティブプロセッサとアセンブリを使用して、指定されたテキストテンプレートファイルを処理します。 カスタムディレクティブプロセッサを作成する場合は、TextTransform.exe を呼び出す独自のバッチファイルを作成できます。 このバッチファイルでは、アセンブリおよび関連付けられているカスタムディレクティブプロセッサを指定できます。
