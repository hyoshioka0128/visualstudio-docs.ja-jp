---
title: x64 プロセスの混合モード デバッグは、4 より前の Microsoft .NET Framework バージョンを使用している場合にはサポートされません。
description: バージョンが 4 より前の .NET Framework では、x64 プロセスの混合モード デバッグはサポートされません。 回避策については、こちらの記事を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: b7495655-54c0-4315-8422-43bf63b8c22e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 039f97fc102e98ba0b6809c4aae402c0f26c5cc1
ms.sourcegitcommit: c67dece5ded82a5867148e1f94396954c1ec4398
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "97975226"
---
# <a name="mixed-mode-debugging-for-x64-processes-is-only-supported-when-using-microsoftnet-framework-4-or-greater"></a>x64 プロセスの混合モード デバッグは、4 より前の Microsoft .NET Framework バージョンを使用している場合にはサポートされません。
バージョンが 4 より前の .NET Framework では、x64 プロセスの混合モード デバッグはサポートされません。 つまり、デバッグ中にマネージド コードからネイティブ コードにステップ インすることや、ネイティブ コードからマネージド コードにステップ インすることはできません。

### <a name="workarounds"></a>問題回避

- Microsoft .NET Framework 4 以降を使用するようにプロジェクトを更新する。

     \- または -

     マネージド コードとネイティブ コードを個別のデバッガー セッション内でデバッグする。

     \- または -

     次の手順に示すように、混合コードを 32 ビット プロセスとしてデバッグする。

### <a name="to-change-the-platform-to-32-bit-visual-basic-or-c"></a>プラットフォームを 32 ビットに変更するには (Visual Basic または C#)

1. **ソリューション エクスプローラー** で、プロジェクトを右クリックして、 **[プロパティ]** をクリックします。

2. プロパティ ページで、 **[コンパイル]** タブまたは **[デバッグ]** タブをクリックします。

3. **[プラットフォーム]** をクリックし、プラットフォームの一覧から [x86] を選択します。

     Visual Basic コンパイラおよび C# コンパイラの既定では、どの CPU 上でも実行されるコードが生成されます。 64 ビット コンピューター上では、これらのバイナリは 64 ビット プロセスとして実行されます。 32 ビット プロセスとして実行するには、 **[Any CPU]** でなく **[Win32]** を選択する必要があります。

### <a name="to-change-the-platform-to-32-bit-cc"></a>プラットフォームを 32 ビットに変更するには (C/C++)

1. **ソリューション エクスプローラー** で、プロジェクトを右クリックして、 **[プロパティ]** をクリックします。

2. プロパティ ページで **[プラットフォーム]** をクリックし、プラットフォームの一覧の [Win32] をクリックします。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- [SQL デバッグの設定](/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100))に関する記事を参照してください。

## <a name="see-also"></a>関連項目
- [64 ビット アプリケーションをデバッグする](../debugger/debug-64-bit-applications.md)