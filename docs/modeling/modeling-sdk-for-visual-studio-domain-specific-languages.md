---
title: Modeling SDK for Visual Studio - ドメイン固有言語
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools
- Domain-Specific Language
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2abb209943ff14969f71ebdca6982020f30a5d47
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75590203"
---
# <a name="modeling-sdk-for-visual-studio---domain-specific-languages"></a>Modeling SDK for Visual Studio - ドメイン固有言語

モデリング SDK for Visual Studio を使用すると、Visual Studio に統合できる強力なモデルベースの開発ツールを作成できます。 同様に、1 つ以上のモデル定義を作成して、一連のツールと統合できます。

MSDK の中核は、業務分野の概念を表すために作成するモデルの定義です。 図式ビュー、コードとその他の成果物を生成する機能、モデルを変換するためのコマンド、Visual Studio のコードやその他のオブジェクトと対話する機能など、さまざまなツールを使用してモデルを囲むことができます。 モデルを開発するとき、他のモデルやツールと組み合わせて、開発の中央に配置される強力なツール セットを形成することができます。

MSDK では、ドメイン固有言語 (DSL) の形式でモデルを迅速に開発できます。 グラフィカルな表記と共にスキーマまたは抽象構文を定義する専用のエディターを使用することから始めます。 この定義から、VMSDK は次を生成します。

- トランザクション ベースのストアで実行する厳密に型指定された API によるモデル実装。

- ツリー ベースのエクスプローラー。

- 定義するモデルまたは一部をユーザーが表示できるグラフィカル エディター。

- 読み取り可能な XML にモデルを保存するシリアル化メソッド。

- テキスト テンプレートを使用して、プログラム コードとその他の成果物を生成するための機能。

これらのすべての機能をカスタマイズおよび拡張できます。 拡張した機能は、統合後も DSL 定義を更新でき、拡張した機能を失うことなく機能を再生成できるように統合されています。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

[関連するブログ記事](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
