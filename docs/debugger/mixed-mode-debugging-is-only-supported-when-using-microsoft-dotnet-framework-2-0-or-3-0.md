---
title: 混合モード デバッグは Microsoft .NET Framework 2.0 または 3.0 を使用している場合にのみサポートされます | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_to_old
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: f607af6f-57fe-472a-a32e-b6202067aa96
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b20ef6b81e4d7162fd230d9d0c3437fe1b5232c1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72730916"
---
# <a name="mixed-mode-debugging-is-only-supported-when-using-microsoft-net-framework-20-or-30"></a>混合モード デバッグは、Microsoft .NET Framework 2.0 以上を使用している場合にのみサポートされます
2\.0 より前のバージョンの Microsoft .NET Framework では、64 ビット プロセスの混合モード デバッグはサポートされません。 つまり、デバッグ中にマネージド コードからネイティブ コードにステップ インすることや、ネイティブ コードからマネージド コードにステップ インすることはできません。

 この問題を回避するには、次の操作を実行します。

- Microsoft .NET Framework 2.0 または 3.0 のどちらかを使用するようにプロジェクトを更新する。

- マネージド コードとネイティブ コードを個別のデバッガー セッション内でデバッグする。

- 次の手順に示すように、混合コードを 32 ビット プロセスとしてデバッグする。

### <a name="to-change-the-operating-system-to-32-bit-visual-basic-or-c"></a>オペレーティング システムを 32 ビットに変更するには (Visual Basic または C#)

1. **ソリューション エクスプローラー**でプロジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。

2. プロパティ ページで、 **[コンパイル]** タブまたは **[デバッグ]** タブをクリックします。

3. **[プラットフォーム]** をクリックして、プラットフォームの一覧から **[x86]** を選択します。

     Visual Basic コンパイラおよび C# コンパイラの既定では、どの CPU 上でも実行されるコードが生成されます。 64 ビット コンピューター上では、これらのバイナリは 64 ビット プロセスとして実行されます。 32 ビット プロセスとして実行するには、 **[Any CPU]** でなく **[Win32]** を選択する必要があります。

### <a name="to-change-the-operating-system-to-32-bit-cc"></a>オペレーティング システムを 32 ビットに変更するには (C/C++)

1. **ソリューション エクスプローラー**でプロジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。

     プロパティ ページで **[プラットフォーム]** をクリックして、プラットフォームの一覧から **[Win32]** を選択します。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- [SQL デバッグの設定](/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100))に関する記事を参照してください。

## <a name="see-also"></a>関連項目
- [64 ビット アプリケーションをデバッグする](../debugger/debug-64-bit-applications.md)