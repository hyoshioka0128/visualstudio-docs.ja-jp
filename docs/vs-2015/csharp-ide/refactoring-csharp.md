---
title: リファクタリング (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.csharp.refactoring.preview
- vs.csharp.refactoring.issues
- vs.csharp.refactoring.buildwarning
- VS.PreviewChanges
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#]
ms.assetid: a39e656a-f81f-4c87-b484-a23168ff1dfc
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0415222645dce2f65e91b5b1c55a5a118cc26697
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667500"
---
# <a name="refactoring-c"></a>リファクタリング (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リファクタリングとは、コードの外部の動作を変更せずにコードの内部構造を変更することによって、コードが記述された後にコードを改善するプロセスです。

 Visual C# では、 **リファクタリング** メニューに次のリファクタリングコマンドが用意されています。

- [メソッドの抽出リファクタリング (C#)](../csharp-ide/extract-method-refactoring-csharp.md)

- [名前の変更リファクタリング (C#)](../csharp-ide/rename-refactoring-csharp.md)

- [フィールドのカプセル化リファクタリング (C#)](../csharp-ide/encapsulate-field-refactoring-csharp.md)

- [インターフェイスの抽出リファクタリング (C#)](../csharp-ide/extract-interface-refactoring-csharp.md)

- [パラメーターの削除リファクタリング (C#)](../csharp-ide/remove-parameters-refactoring-csharp.md)

- [パラメーター順序の再変更リファクタリング (C#)](../csharp-ide/reorder-parameters-refactoring-csharp.md)

## <a name="multi-project-refactoring"></a>複数プロジェクトのリファクタリング
 Visual Studio では、同じソリューション内のプロジェクトに対する複数プロジェクトのリファクタリングがサポートされています。 ファイル間の参照を修正するリファクタリング操作はすべて、同じ言語のすべてのプロジェクトで、これらの参照を修正します。 これは、プロジェクト間参照に使用できます。 たとえば、クラスライブラリを参照するコンソールアプリケーションがある場合、クラスライブラリ型の名前を変更すると ( `Rename` リファクタリング操作を使用)、コンソールアプリケーションのクラスライブラリ型への参照も更新されます。

## <a name="changes-preview"></a>変更のプレビュー
 多くのリファクタリング操作は、リファクタリング操作がコードに対して実行するすべての参照の変更をレビューしてから、変更をコミットする機会を提供します。 これらのリファクタリング操作の場合、[ **参照の変更のプレビュー** ] オプションが [リファクタリング] ダイアログボックスに表示されます。 このオプションを選択し、リファクタリング操作を受け入れると、[ **変更のプレビュー] ダイアログボックス** が表示されます。 [変更の **プレビュー** ] ダイアログボックスに2つのビューが表示されていることに注意してください。 下部のビューには、リファクタリング操作によって、すべての参照の更新を含むコードが表示されます。 [**変更のプレビュー** ] ダイアログボックスで **[キャンセル**] を押すと、リファクタリング操作が停止され、コードに変更は加えられません。

## <a name="refactoring-warnings"></a>リファクタリングの警告
 コンパイラがプログラムを完全に理解していない場合、またはリファクタリングエンジンが適切なすべての参照を更新できない可能性がある場合は、警告ダイアログボックスが表示されます。 この警告ダイアログボックスでは、変更をコミットする前に [変更の **プレビュー** ] ダイアログボックスでコードをプレビューすることもできます。

> [!NOTE]
> メソッドに構文エラーが含まれている場合 (IDE では赤い波線が表示されます)、リファクタリングエンジンは、そのメソッド内の要素への参照を更新しません。 次の例は、この動作を示しています。

 既定では、参照の変更をプレビューせずにリファクタリング操作を実行すると、プログラムでコンパイルエラーが検出された場合、開発環境ではこの警告ダイアログボックスが表示されます。

 **プレビュー参照の変更**が有効になっているリファクタリング操作を実行し、プログラムでコンパイルエラーが検出された場合、開発環境では、**リファクタリングの警告**ダイアログボックスを表示する代わりに、[変更の**プレビュー** ] ダイアログボックスの下部に次の警告メッセージが表示されます。

 **プロジェクトまたはその依存関係の1つが、現在ビルドされていません。参照を更新することはできません。**

 このリファクタリングの警告は、[ **参照の変更のプレビュー** ] オプションを提供するリファクタリング操作でのみ使用できます。

## <a name="error-tolerant-refactoring-and-verification-results"></a>エラートレラントなリファクタリングと検証の結果
 リファクタリングはエラートレラントです。 つまり、ビルドできないプロジェクトでリファクタリングを実行できます。 ただし、このような場合、リファクタリングプロセスではあいまいな参照が正しく更新されない可能性があります。

 リファクタリングエンジンによってコンパイルエラーが検出された場合、またはリファクタリング操作によってコード参照が意図したものとは異なるものにバインドされている場合は、[ **検証結果** ] ダイアログボックスで通知を受け取ることができます (再バインドの問題)。

 検証結果機能を有効にするには、[ **ツール** ] メニューの [ **オプション**] をクリックします。 [ **オプション** ] ダイアログボックスで、[ **テキストエディター**]、[ **C#**] の順に展開します。 [ **詳細設定** ] をクリックし、[ **リファクタリングの結果を確認** する] チェックボックスをオンにします。

 [ **検証結果** ] ダイアログボックスでは、2種類の再バインドの問題の違いを区別します。

### <a name="references-whose-definition-will-no-longer-be-the-renamed-symbol"></a>定義名が変更されたシンボルではなくなった参照
 この種の再バインドの問題は、参照によって名前が変更されたシンボルが参照されなくなった場合に発生します。 次に例を示します。

```csharp
class Example
{
    private int a;
    public Example(int b)
    {
        a = b;
    }
}
```

 リファクタリングを使用して名前 `a` をに変更すると `b` 、このダイアログボックスが表示されます。 名前が変更された変数への参照が、 `a` フィールドにバインドするのではなく、コンストラクターに渡されるパラメーターにバインドされるようになりました。

### <a name="references-whose-definition-will-now-become-the-renamed-symbol"></a>定義が名前変更されたシンボルになる参照
 この種の再バインドの問題は、名前を変更したシンボルを参照していない参照が、名前が変更されたシンボルを参照している場合に発生します。 次に例を示します。

```csharp
class Example
{
    private static void Method(object a) { }
    private static void OtherMethod(int a) { }
    static void Main(string[] args)
    {
        Method(5);
    }
}
```

 リファクタリングを使用して名前 `OtherMethod` をに変更すると `Method` 、このダイアログボックスが表示されます。 では、パラメーターを受け取るオーバーロードされたメソッドではなく、パラメーターを受け取るオーバーロードされたメソッドを参照して `Main` `int` `object` います。

## <a name="see-also"></a>参照
 [C# 用 Visual Studio 開発環境の使用](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)[方法: C# リファクタリングスニペットを復元する](../ide/how-to-restore-csharp-refactoring-snippets.md)