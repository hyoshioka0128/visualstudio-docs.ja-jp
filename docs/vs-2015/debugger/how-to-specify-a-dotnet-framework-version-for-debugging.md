---
title: '方法: デバッグ用に .NET Framework バージョンを指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- .NET Framework, specifying version for debugging
- debugging [Visual Studio], specifying .NET Framework version
ms.assetid: 7a4893ba-4620-4774-893f-378d4ca28893
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4c785c419ead31ad90e2b20ae7f48af778598bb6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176563"
---
# <a name="how-to-specify-a-net-framework-version-for-debugging"></a>方法 : デバッグで .NET Framework のバージョンを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] デバッガーでは、Microsoft [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] の現在のバージョンだけでなく、古いバージョンのデバッグもサポートしています。 Visual Studio からアプリケーションを起動すると、デバッグしているアプリケーションの [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バージョンは正しく識別されます。 アプリケーションが既に実行されていて、[ **アタッチ先**] を使用する場合、デバッガーはの古いバージョンを常に識別できるとは限りません [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。 この場合、次のようなエラー メッセージが出力されます。  
  
 "アプリケーションが使用しようとしている Microsoft [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョンに関してデバッガーが不適切な想定を行っています。"  
  
 このような場合はまれですが、使用するデバッガーのバージョンを指定するには、レジストリ キーを設定します。  
  
### <a name="to-specify-a-net-framework-version-for-debugging"></a>デバッグで .NET Framework のバージョンを指定するには  
  
1. コンピューターにインストールされている .NET Framework のバージョンを確認するには、Windows\Microsoft.NET\Framework ディレクトリを探します。 バージョン番号は次のようになります。  
  
     `V1.1.4322`  
  
     正しいバージョン番号を確認し、メモしておきます。  
  
2. **レジストリ エディター** (regedit) を起動します。  
  
3. **レジストリ エディター**で、[HKEY_LOCAL_MACHINE] フォルダーを開きます。  
  
4. 次に移動します。HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine\\{449EC4CC-30D2-4032-9256-EE18EB41B62B}  
  
     このキーが存在しない場合、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine を右クリックし、 **[新しいキー]** をクリックします。 新しいキーに `{449EC4CC-30D2-4032-9256-EE18EB41B62B}` という名前を付けます。  
  
5. {449EC4CC-30D2-4032-9256-EE18EB41B62B} に移動し、 **[名前]** 列を確認して、CLRVersionForDebugging キーを探します。  
  
    1. このキーが存在しない場合、{449EC4CC-30D2-4032-9256-EE18EB41B62B} を右クリックし、 **[新規] - [文字列値]** をクリックします。 次に、新しい文字列値を右クリックし、 **[名前の変更]** をクリックし、「`CLRVersionForDebugging`」と入力します。  
  
6. **[CLRVersionForDebugging]** をダブルクリックします。  
  
7. **[文字列の編集]** ボックスの **[値]** ボックスに、.NET Framework のバージョン番号を入力します。 次に例を示します。V1.1.4322  
  
8. **[OK]** をクリックします。  
  
9. **レジストリ エディター**を閉じます。  
  
     それでもデバッグの開始時にエラー メッセージが表示される場合は、レジストリに正しいバージョン番号が入力されていることを確認します。 また、Visual Studio でサポートされている [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョンを使用していることを確認します。 デバッガーは、現在のバージョンおよび以前のバージョンの .NET Framework と互換性がありますが、将来のバージョンとの上位互換性はない可能性があります。  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
