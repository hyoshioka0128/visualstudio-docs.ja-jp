---
title: カスタムのカラー設定可能アイテム |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: feecd9e8f8178045f66999b775e2d0792f50b288
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708995"
---
# <a name="custom-colorable-items"></a>カスタムのカラー設定可能なアイテム
カスタムの色付け可能な項目を言語サービスの一部として実装することで、キーワードやコメントなどの色分けの型のリストをオーバーライドできます。

## <a name="user-settings-of-colorable-items"></a>カラー設定可能なアイテムのユーザー設定
 [ツール **]** メニューの **[オプション]** をクリックし、[**環境**] の [**フォントと色**] をクリックすると、[**フォントと色**] ダイアログ ボックスを表示できます。 **[テキスト エディタ]** や **[コマンド ウィンドウ**] などの表示を選択すると、[**アイテムの表示**] リスト ボックスにその表示に使用されるすべての色付け可能なアイテムが表示されます。 色分け可能な項目ごとに、フォント、サイズ、前景色、背景色を表示および変更できます。 選択した項目は、レジストリのキャッシュに格納され、色付きの項目名によってアクセスされます。

## <a name="presentation-of-colorable-items"></a>カラーアイテムのプレゼンテーション
 IDE は **[フォントと色**]ダイアログ ボックスでユーザーが色付け可能な項目を上書きする処理を行うため、各カスタムの色付け可能な項目に名前を付けるだけで済みます。 この名前は、[**表示項目**] ボックスの一覧に表示されます。 色付け可能な項目は、アルファベット順に表示されます。 言語サービスのカスタムの色指定可能な項目をグループ化するには、各名前を言語名で始**めることができます**。 **NewLanguage - Comment**

> [!CAUTION]
> 既存の色付け可能な項目名との競合を避けるために、色付け可能な項目名に言語名を含める必要があります。 開発中にいずれかのカラー付け可能な項目の名前を変更した場合は、最初にカラーアイテムにアクセスするときに作成されたキャッシュをリセットする必要があります。 通常はディレクトリに Visual Studio SDK と共にインストールされる**CreateExpInstance**ツールを使用して、実験用キャッシュをリセットできます。
>
> *C:\プログラム ファイル (x86)\マイクロソフト ビジュアル スタジオ 14.0\VSSDK\VisualStudio 統合\ツール\ビン*
>
> キャッシュをリセットするには、**次のように**入力します。 **CreateExpInstance**の詳細については[、「CreateExpInstance ユーティリティ](../../extensibility/internals/createexpinstance-utility.md)」を参照してください。

 カラー設定可能な項目のリストの最初の項目は参照できません。 最初の項目は、0 のカラー化可能な項目インデックスに[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]対応し、常にその項目の既定のテキストの色と属性を提供します。 この参照されていない項目を処理する最も簡単な方法は、最初の項目として、リスト内のプレースホルダーの色指定可能な項目を提供することです。

## <a name="implement-custom-colorable-items"></a>カスタムのカラー対応アイテムを実装する

1. キーワード、演算子、識別子など、言語で色分けする必要があるものを定義します。

2. これらの色付け可能な項目の列挙体を作成します。

3. パーサーまたはスキャナーから返されるトークンの種類を列挙値に関連付けます。

    たとえば、トークンの種類を表す値は、カスタムの色付け可能な項目の列挙体の値と同じである可能性があります。

4. オブジェクト内のメソッドの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>実装で、パーサーまたはスキャナーから返されるトークンの種類に対応するカスタムの色付け可能な項目の列挙値を属性リストに入力します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>

5. インターフェイスを実装する同じクラスで<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>インターフェイスとその 2 つのメソッドを実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>し<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>、 .

6. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> インターフェイスを実装します。

7. 24 ビットまたは高色の値をサポートする場合は、インターフェイスも<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>実装します。

8. 言語サービス オブジェクトで、オブジェクトを含むリストを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>作成します。

    カスタムの色付け可能な項目の列挙体の対応する値を使用して、リスト内の各項目にアクセスできます。 列挙値をリストのインデックスとして使用します。 リストの最初の項目は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]常に処理される既定のテキスト スタイルに対応するため、アクセスされることはありません。 これを補うためには、リストの先頭にプレースホルダの色付け可能な項目を挿入します。

9. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>メソッドの実装で、カスタムの色付け可能な項目リスト内の項目の数を返します。

10. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>メソッドの実装で、要求された色付け可能な項目をリストから返します。

    <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>インターフェイスと<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>インターフェイスの実装方法の例については、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>を参照してください。

## <a name="see-also"></a>関連項目
- [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)
- [カスタム エディターでの構文の色分け](../../extensibility/syntax-coloring-in-custom-editors.md)
- [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [構文の色分けを実装する](../../extensibility/internals/implementing-syntax-coloring.md)
- [方法: 組み込みのカラー化可能なアイテムを使用する](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
