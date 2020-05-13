---
title: Python コードの単体テスト
description: Visual Studio で Python コードの単体テストを設定し、テスト エクスプローラーの機能を最大限に活用してテストを検出、実行、デバッグします。
ms.date: 09/18/2019
ms.topic: include
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 09c67ace9db36cb8ee3d94296d339b62849e3c94
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "71254194"
---
# <a name="set-up-unit-testing-for-python-code"></a>Python コードの単体テストの設定

単体テストは、アプリケーションの他のコード単位 (通常は分離された関数、クラスなど) をテストするコードの断片です。 アプリケーションがそのすべての単体テストに合格すると、少なくとも低レベルの機能が正しいことを信頼できます。

Python は、プログラムの設計時にシナリオを検証するために単体テストを幅広く使用します。 Visual Studio の Python サポートには、別々にテストを実行する必要のない、開発プロセスのコンテキスト内での単体テストの検出、実行、デバッグのサポートが含まれています。

この記事では、Python での Visual Studio の単体テスト機能の概要を説明します。 一般的な単体テストについて詳しくは、「[コードの単体テスト](../test/unit-test-your-code.md)」をご覧ください。

::: moniker range="vs-2017"

[!include[Testing Python code](includes/vs-2017/unit-testing-python.md)]

::: moniker-end

::: moniker range=">= vs-2019"

[!include[Testing Python code](includes/vs-2019/unit-testing-python.md)]

::: moniker-end