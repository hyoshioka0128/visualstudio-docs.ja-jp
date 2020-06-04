---
title: '[エディット コンティニュ] エラー メッセージ ダイアログ ボックス | Microsoft Docs'
ms.date: 10/15/2018
ms.topic: reference
f1_keywords:
- vs.debug.ENC.SupportedButNotAvailable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7df95eae689f7c3abbb0d75a7557ce749bdceee5
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188224"
---
# <a name="edit-and-continue-error-message"></a>[エディット コンティニュ] エラー メッセージ

エディット コンティニュをサポートするコード言語でデバッグしている場合、 **[エディット コンティニュ]** エラー メッセージ ボックスが表示されますが、自分が加えたコード変更にはエディット コンティニュを使用できません。 エラー メッセージには、より詳細な説明が表示されます。 ダイアログに応答するには、 **[OK]** を選択してダイアログ ボックスを閉じ、編集を取り消します。

このエラー メッセージには次のような原因が考えられます。

- SQL Server コードを編集しようとしています。
- 最適化されたコードを編集しようとしています。 必要に応じて、リリース ビルドからデバッグ ビルドに切り替える必要があります。
- デバッガーで一時停止しているときではなく、実行中にコードを編集しようとしています。 [ブレークポイントを設定](../debugger/using-breakpoints.md)して、一時停止中にコードを編集してみてください。
- アンマネージド デバッグのみが有効になっているときにマネージド コードを編集しようとしています。 [混合モード デバッグ](../debugger/how-to-debug-in-mixed-mode.md)を実行している場合は、エディット コンティニュを使用できません。
- プログラミング言語にエディット コンティニュでサポートされていないコード変更を加えています。 詳細については、[C# でサポートされているコードの変更](supported-code-changes-csharp.md)、[Visual Basic のエディット コンティニュでサポートされていない編集](supported-code-changes-csharp.md)、[サポートされている C++ コードの変更](supported-code-changes-cpp.md)に関するページを参照してください。
- **[デバッグ]** メニューからデバッグを開始するのではなく、アタッチしているアプリでコードを編集しようとしています。
- ワトソン博士のダンプをデバッグ中にコードを編集しようとしています。デバッグ。
- 未処理の例外が発生した後にコードを編集しようとしています。オプション **[ハンドルされていない例外で呼び出し履歴をアンワインドする]** がオフです。
- 埋め込まれたランタイム アプリケーションをデバッグしているときに、コードを編集しようとしています。
- 64 ビット アプリ ターゲットで、4.5.1 より前のバージョンの .NET Framework を使用してマネージド コードを編集しようとしています。 4\.5.1 より前の .NET Framework にエディット コンティニュを使用するには、 **[コンパイラの詳細設定]** 設定の **[\<プロジェクト名>**  > **のプロパティ]**  >  **[コンパイル]** タブでターゲットを **[x86]** に設定します。
- デバッグ中に変更され、再読み込みされたアセンブリのコードを編集しようとしています。
- 読み込まれていないアセンブリ内のコードを編集しようとしています。
- 最新バージョンにビルド エラーがあるため、以前のバージョンのアプリのデバッグを開始しています。

詳細については次を参照してください:
- [C++ のエディット コンティニュに関するブログ投稿](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)
- [サポートされているコード変更 (C++)](../debugger/supported-code-changes-cpp.md)
- [エディット コンティニュ](../debugger/edit-and-continue.md)