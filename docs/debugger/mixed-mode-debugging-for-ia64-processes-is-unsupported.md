---
title: IA64 プロセスの混合モードのデバッグはサポートされていません。
description: Visual Studio では、IA64 (Itanium) プロセスにおけるマネージド コードとネイティブ コードの混合モードのデバッグはサポートされていません。 回避策については、こちらの記事を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_ia64
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 20bc1e38-049b-4388-87c4-936815d85b46
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 19232155a802e0e883b6169fe71fe5005711031c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930266"
---
# <a name="mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>IA64 プロセスの混合モードのデバッグはサポートされていません。
Visual Studio では、IA64 プロセスでマネージド コードとネイティブ コードの混合モードのデバッグはサポートされていません。 つまり、デバッグ中にマネージド コードからネイティブ コードにステップ インすることや、ネイティブ コードからマネージド コードにステップ インすることはできません。

### <a name="workarounds"></a>問題回避

- マネージド コードとネイティブ コードを個別のデバッガー セッション内でデバッグする。

     \- または -

     次の手順に示すように、混合コードを 32 ビット プロセスとしてデバッグする。

### <a name="to-change-the-platform-to-32-bit-visual-basic-or-c"></a>プラットフォームを 32 ビットに変更するには (Visual Basic または C#)

1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。

2. プロパティ ページで、 **[コンパイル]** タブまたは **[デバッグ]** タブをクリックします。

3. **[プラットフォーム]** をクリックし、プラットフォームの一覧から [x86] を選択します。

     Visual Basic コンパイラおよび C# コンパイラの既定では、どの CPU 上でも実行されるコードが生成されます。 64 ビット コンピューター上では、これらのバイナリは 64 ビット プロセスとして実行されます。 32 ビット プロセスとして実行するには、 **[Any CPU]** でなく **[Win32]** を選択する必要があります。

### <a name="to-change-the-platform-to-32-bit-cc"></a>プラットフォームを 32 ビットに変更するには (C/C++)

1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。

2. プロパティ ページで **[プラットフォーム]** をクリックし、プラットフォームの一覧の [Win32] をクリックします。

## <a name="see-also"></a>関連項目
- [64 ビット アプリケーションをデバッグする](../debugger/debug-64-bit-applications.md)