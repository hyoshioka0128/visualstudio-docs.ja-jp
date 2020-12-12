---
title: DslTextTransform コマンド
description: DslTextTransform は TextTransform.exe を呼び出すスクリプトであり、共通のオプションを使用して実行されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 74f87f735f5ad6864082046327bc852d5d43fdb6
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97362718"
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
