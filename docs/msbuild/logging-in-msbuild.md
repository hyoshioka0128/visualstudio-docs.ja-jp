---
title: MSBuild でのログ | Microsoft Docs
description: ビルド イベント、メッセージ、警告、エラーをログ ファイルにキャプチャすることによってビルドの進行状況を監視する手段が、MSBuild のログ記録によってどのように提供されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, logging
ms.assetid: 9aea2e76-8f60-4234-913d-598e7bbad808
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9de830003571f1f648cf06be634d9a773b95269f
ms.sourcegitcommit: f1d47655974a2f08e69704a9a0c46cb007e51589
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92904328"
---
# <a name="logging-in-msbuild"></a>MSBuild でのログ

ログを使用すると、ビルドの進行状況を監視できます。 ログは、ログ ファイルにイベント、メッセージ、警告、エラーをキャプチャします。

## <a name="in-this-section"></a>このセクションの内容

- [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)

 MSBuild でのログ記録のさまざまな側面について説明します。

- [ビルド ロガー](../msbuild/build-loggers.md)

 シングル プロセッサ ロガーの作成に必要な手順について説明します。

- [マルチプロセッサ環境でのログ](../msbuild/logging-in-a-multi-processor-environment.md)

 マルチプロセッサ環境でのログの仕組みと、マルチプロセッサ ログの 2 つのモデルについて説明します。

- [マルチプロセッサ対応のロガーの記述](../msbuild/writing-multi-processor-aware-loggers.md)

 マルチプロセッサ対応のロガーの作成方法および ConfigurableForwardingLogger の使用方法について説明します。

- [転送 logger の作成](../msbuild/creating-forwarding-loggers.md)

 カスタム転送ロガーを作成する方法について説明します。

## <a name="see-also"></a>関連項目

- [複数プロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md) 複数のプロジェクトを並列に実行して、これらのプロジェクトをより速くビルドする方法について説明します。
