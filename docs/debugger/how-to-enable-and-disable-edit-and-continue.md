---
title: '方法: エディット コンティニュを有効および無効にする | Microsoft Docs'
ms.custom: seodec18
ms.date: 10/04/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- /INCREMENTAL linker option
- Apply Code Changes command
- Edit and Continue, disabling
- code changes, applying in break mode
- INCREMENTAL linker option
- Edit and Continue, enabling
- break mode, applying code changes
- Edit and Continue, applying code changes
- Step command
- Go command
ms.assetid: fd961a1c-76fa-420d-ad8f-c1a6c003b0db
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 2c8486bdcd7bc737d3851eabd88734df4efd80b7
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430537"
---
# <a name="how-to-enable-and-disable-edit-and-continue-c-vb-c"></a>方法: エディット コンティニュを有効および無効にする (C#、VB、C++)

**[エディット コンティニュ]** は、デザイン時に Visual Studio の **[オプション]** ダイアログ ボックスで無効または有効にすることができます。 **エディット コンティニュ**はデバッグ ビルドでのみ動作します。 詳細については、「[エディット コンティニュ](../debugger/edit-and-continue.md)」を参照してください。

ネイティブ C++ の場合、 **[エディット コンティニュ]** には `/INCREMENTAL` オプションを使用する必要があります。 C++ の機能要件の詳細については、この[ブログ投稿](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)と「[エディット コンティニュ (C++)](../debugger/edit-and-continue-visual-cpp.md)」を参照してください。

**エディット コンティニュを有効または無効にするには:**

1. デバッグ セッション中は、デバッグを停止します ( **[デバッグ]**  >  **[停止]** 、または **Shift**+**F5** キー)。

1. **[ツール]**  >  **[オプション]** > (または **[デバッグ]**  >  **[オプション]** ) > **[デバッグ]**  >  **[全般]** を選択し、右側のペインで **[エディット コンティニュ]** を選択します。

    > [!NOTE]
    > IntelliTrace が有効になっている場合に、IntelliTrace イベントと呼び出し情報の両方を収集すると、エディット コンティニュが無効になります。 詳細については、[IntelliTrace](../debugger/intellitrace.md) に関するページを参照してください。

1. C++ コードの場合は、 **[ネイティブのエディット コンティニュを有効にする]** が選択されていることを確認し、追加のオプションを設定します。
    - **[コンティニュに変更を適用する (ネイティブのみ)]**

      選択した場合は、ブレーク状態からデバッグを続行すると、Visual Studio によって自動的にコンパイルされ、コードの変更が適用されます。 そうしない場合は、 **[デバッグ]**  >  **[コード変更を適用]** を使用して変更の適用を選択できます。

    - **[古いコードの警告を表示する (ネイティブのみ)]**

      選択した場合は、古いコードに関する警告が示されます。

1. **[OK]** をクリックします。
