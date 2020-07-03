---
title: 方法 - プログラムのクラッシュが発生している DLL を確認する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.dll
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, DLL crashes
- Module List dialog box
- errors [debugger], DLL crashes
- Modules window
- debugging [Visual Studio], DLL crashes
- DLLs, load order of
ms.assetid: ecf62568-8b65-4a41-b8a4-e962ff2dfb71
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 155fd74dc6e01f88bf04fe21b77ebdae6b04437f
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349537"
---
# <a name="how-to-find-which-dll-your-program-crashed-in-c-c-visual-basic-f"></a>方法: プログラムのクラッシュが発生している DLL を確認する (C#、C++、Visual Basic、F#)

 システム DLL または他の開発者が作成したコードを呼び出す部分でアプリケーションがクラッシュした場合、クラッシュが発生した DLL を確認する必要があります。 プログラム外の DLL でクラッシュが発生している場合は、 **[モジュール]** ウィンドウを使用してその場所を確認できます。

### <a name="to-find-where-a-crash-occurred-using-the-modules-window"></a>[モジュール] ウィンドウを使ってクラッシュの発生場所を確認するには

1. クラッシュが発生したアドレスをメモします。

    エラー メッセージ内にアドレスが表示されない場合は、別の方法を使用した DLL の識別が必要になることがあります。 疑わしいのは システム DLL だと思う場合は、デバッグ時に Microsoft シンボル サーバーから[シンボルを読み込む](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)ことができます。 それ以外の場合は、代わりにヒープ情報を含む[ダンプ ファイルを作成する](../debugger/using-dump-files.md)必要があります。 さまざまな[ツール](https://blogs.msdn.microsoft.com/andrehal/2009/12/31/what-is-a-dump-and-how-do-i-create-one/)を使用して、ダンプ ファイルを作成できます。

2. **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[モジュール]** をクリックします。

3. **[モジュール]** ウィンドウの **[アドレス]** 列に注目します。 必要に応じて、スクロール バーを使用します。

4. 列の上部にある **[アドレス]** ボタンをクリックして、DLL をアドレス順に並べ替えます。

5. 並べ替えたリストを検索して、アドレス範囲内にクラッシュ場所がある DLL を探します。

6. **[名前]** 列と **[パス]** 列で、DLL の名前とパスを確認します。

## <a name="see-also"></a>関連項目
- [DLL プロジェクトのデバッグ](../debugger/debugging-dll-projects.md)
- [方法: [モジュール] ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)