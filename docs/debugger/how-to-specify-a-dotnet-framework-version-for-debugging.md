---
title: デバッグ用の .NET Framework バージョンを指定する |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- .NET Framework, specifying version for debugging
- debugging [Visual Studio], specifying .NET Framework version
ms.assetid: 7a4893ba-4620-4774-893f-378d4ca28893
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1f6107d6396c6228be1d511e81003fbe7faf06c9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732636"
---
# <a name="specify-an-older-net-framework-version-for-debugging-c-visual-basic-f"></a>デバッグ用に古い .NET Framework バージョンを指定C#する (、 F#Visual Basic、)

Visual Studio デバッガーでは、Microsoft .NET Framework の古いバージョンと現在のバージョンのデバッグがサポートされています。 Visual Studio からアプリケーションを起動する場合、デバッガーは、デバッグしているアプリケーションの正しいバージョンの .NET Framework を常に識別できます。 ただし、アプリケーションが既に実行されていて、 **[アタッチ先]** を使用してデバッグを開始した場合、デバッガーは常に古いバージョンの .NET Framework を識別できない可能性があります。 この場合、次のようなエラー メッセージが出力されます。

``` cmd
The debugger has made an incorrect assumption about the .NET Framework version your application is going to use.
```

このエラーが発生するまれなケースとして、レジストリキーを設定して、使用するバージョンをデバッガーに示すことができます。

### <a name="to-specify-a-net-framework-version-for-debugging"></a>デバッグで .NET Framework のバージョンを指定するには

1. コンピューターにインストールされている .NET Framework のバージョンを確認するには、Windows\Microsoft.NET\Framework ディレクトリを探します。 バージョン番号は次のようになります。

    `V1.1.4322`

    正しいバージョン番号を確認し、メモしておきます。

2. **レジストリ エディター** (regedit) を起動します。

3. **レジストリ エディター**で、[HKEY_LOCAL_MACHINE] フォルダーを開きます。

4. HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine\\{449EC4CC-30D2-4032-9256-EE18EB41B62B} に移動します。

    このキーが存在しない場合、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine を右クリックし、 **[新しいキー]** をクリックします。 新しいキーに `{449EC4CC-30D2-4032-9256-EE18EB41B62B}` 名前を指定します。

5. {449EC4CC-30D2-4032-9256-EE18EB41B62B} に移動し、 **[名前]** 列を確認して、CLRVersionForDebugging キーを探します。

   1. このキーが存在しない場合、{449EC4CC-30D2-4032-9256-EE18EB41B62B} を右クリックし、 **[新規] - [文字列値]** をクリックします。 次に、新しい文字列値を右クリックし、 **[名前の変更]** をクリックして、「`CLRVersionForDebugging`」と入力します。

6. **[CLRVersionForDebugging]** をダブルクリックします。

7. **[文字列の編集]** ボックスの **[値]** ボックスに、.NET Framework のバージョン番号を入力します。 たとえば、「V1.1.4322」などです。

8. **[OK]** をクリックします。

9. **レジストリ エディター**を閉じます。

     それでもデバッグの開始時にエラー メッセージが表示される場合は、レジストリに正しいバージョン番号が入力されていることを確認します。 また、Visual Studio でサポートされている .NET Framework のバージョンを使用していることを確認します。 デバッガーは、現在のバージョンおよび以前のバージョンの .NET Framework と互換性がありますが、将来のバージョンとの上位互換性はない可能性があります。

## <a name="see-also"></a>関連項目
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
