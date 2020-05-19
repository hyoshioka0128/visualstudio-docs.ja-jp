---
title: Visual C/C++ カスタム ビジュアライザーの互換性
ms.date: 01/28/2019
ms.prod: visual-studio-dev16
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging assertions
- assertions, debugging
- assertions, assertion failures
- Assertion Failed dialog box
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: 9fdd44be89fde2fbc26038c8b88fff405876264f
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430619"
---
# <a name="visual-cc-custom-visualizer-compatibility"></a>Visual C/C++ カスタム ビジュアライザーの互換性

Visual Studio 2019 以降、C++ には、メモリ集中型のコンポーネントをホストするために外部 64 ビット プロセスを使用する、強化されたデバッガーが含まれています。 この更新プログラムの一部として、C/C++ 式エバリュエーターに対する特定の拡張機能を、新しいデバッガーと互換性を持たせるように更新する必要があります。

現在、レガシ C/C++ EE アドインまたは C/C++ カスタム ビジュアライザーを使用している場合、 **[ツール]**  >  **[オプション]**  >  **[デバッグ]** に移動し、 **[外部プロセスでのデバッグ シンボルの読み込み (ネイティブのみ)]** をオフにすることで、この外部プロセスの使用をオフにすることができます。 このオプションの選択を解除すると、IDE (devenv.exe) プロセス内のメモリ使用量が大幅に増加します。 そのため、大規模なプロジェクトをデバッグする場合は、拡張機能の所有者と協力して、このデバッグ オプションとの互換性を確保することをお勧めします。

レガシ C/C++ EE アドインまたは C/C++ カスタム ビジュアライザーの所有者は、[Concord 拡張サンプルの Wiki](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Worker-Process-Remoting) で、ワーカー プロセスにおける拡張機能の読み込みのオプトインに関する詳細を参照できます。 [C/C++ カスタム ビジュアライザーのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/tree/master/CppCustomVisualizer)も見つけることができます。