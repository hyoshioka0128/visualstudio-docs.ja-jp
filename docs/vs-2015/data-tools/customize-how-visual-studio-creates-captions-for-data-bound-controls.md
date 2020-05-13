---
title: Visual Studio 2015 がデータバインドコントロールのキャプションを作成する方法をカスタマイズするMicrosoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c0e54f68ab7e34f1cfb6abb228f552cc3792a8b7
ms.sourcegitcommit: 374f5ec9a5fa18a6d4533fa2b797aa211f186755
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476918"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>Visual Studio がデータ バインド コントロールのキャプションを作成する方法をカスタマイズする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[[データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)から Windows フォームデザイナーに項目をドラッグすると、特別な考慮事項が表示されます。2つ以上の単語が連結されていることがわかった場合、キャプションラベル内の列名は、より読みやすい文字列に再フォーマットされます。 **HKEY_CURRENT_USER \Software\microsoft\visualstudio\10.0\data designer**レジストリキーの**SmartCaptionExpression**、 **SmartCaptionReplacement**、および**SmartCaptionSuffix**の値を設定することによって、これらのラベルの作成方法をカスタマイズできます。

> [!NOTE]
> このレジストリキーは、作成するまで存在しません。

 スマートキャプションは、 **SmartCaptionExpression**値の値に入力された正規表現によって制御されます。 **データデザイナー**のレジストリキーを追加すると、キャプションラベルを制御する既定の正規表現がオーバーライドされます。 正規表現の詳細については、「 [Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

 次の表では、キャプションラベルを制御するレジストリ値について説明します。

|レジストリ項目|説明|
|-------------------|-----------------|
|**SmartCaptionExpression**|パターンに一致するために使用される正規表現。|
|**SmartCaptionReplacement**|**SmartCaptionExpression**に一致したすべてのグループを表示する形式。|
|**SmartCaptionSuffix**|キャプションの末尾に追加する省略可能な文字列。|

 次の表は、これらのレジストリ値の内部既定の設定を示しています。

|レジストリ項目|既定値|説明|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|(\\\p{Ll})(\\\p{Lu})&#124;_+|小文字の後に大文字またはアンダースコアが続くパターンに一致します。|
|**SmartCaptionReplacement**|$1 $2|$1 は、式の最初のかっこに一致したすべての文字を表し、$2 は2番目のかっこで囲まれた任意の文字を表します。 置換は、最初の一致、空白、および2番目の一致です。|
|**SmartCaptionSuffix**|:|返される文字列に付加された文字を表します。 たとえば、キャプションが `Company Name`場合、サフィックスによって `Company Name:`|

> [!CAUTION]
> レジストリエディターで何かを実行する場合は注意が必要です。 編集する前にレジストリをバックアップしてください。 レジストリエディターを誤って使用すると、重大な問題が発生し、オペレーティングシステムの再インストールが必要になることがあります。 Microsoft では、レジストリエディターを誤って使用した場合に発生する問題を解決できないことを保証していません。 レジストリ エディターは、ご自身の責任において使用してください。

### <a name="to-modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>[データソース] ウィンドウのスマートキャプションの動作を変更するには

1. [**開始**] をクリックしてコマンドウィンドウを開き、を**実行**します。

2. [**実行**] ダイアログボックスで「`regedit`」と入力し、[ **OK**] をクリックします。

3. [ **HKEY_CURRENT_USER** ] ノードを展開します。

4. [**ソフトウェア**] ノードを展開します。

5. **Microsoft**ノードを展開します。

6. [ **VisualStudio** ] ノードを展開します。

7. [ **10.0** ] ノードを右クリックし、`Data Designers`という名前の新しい**キー**を作成します。

8. [**データデザイナー** ] ノードを右クリックし、`SmartCaptionExpression`という名前の新しい**文字列値**を作成します。

9. [**データデザイナー** ] ノードを右クリックし、`SmartCaptionReplacement`という名前の新しい**文字列値**を作成します。

10. [**データデザイナー** ] ノードを右クリックし、`SmartCaptionSuffix`という名前の新しい**文字列値**を作成します。

11. **SmartCaptionExpression**アイテムを右クリックし、[**変更**] を選択します。

12. [**データソース**] ウィンドウで使用する正規表現を入力します。

13. **SmartCaptionReplacement**アイテムを右クリックし、[**変更**] を選択します。

14. 正規表現で一致したパターンを表示する方法で書式設定された置換文字列を入力します。

15. **SmartCaptionSuffix**アイテムを右クリックし、[**変更**] を選択します。

16. キャプションの末尾に表示する任意の文字を入力します。

     次に [**データソース**] ウィンドウから項目をドラッグすると、指定された新しいレジストリ値を使用してキャプションラベルが作成されます。

### <a name="to-turn-off-the-smart-captioning-feature"></a>スマートキャプション機能を無効にするには

1. [**開始**] をクリックしてコマンドウィンドウを開き、を**実行**します。

2. [**実行**] ダイアログボックスで「`regedit`」と入力し、[ **OK**] をクリックします。

3. [ **HKEY_CURRENT_USER** ] ノードを展開します。

4. [**ソフトウェア**] ノードを展開します。

5. **Microsoft**ノードを展開します。

6. [ **VisualStudio** ] ノードを展開します。

7. [ **10.0** ] ノードを右クリックし、`Data Designers`という名前の新しい**キー**を作成します。

8. [**データデザイナー** ] ノードを右クリックし、`SmartCaptionExpression`という名前の新しい**文字列値**を作成します。

9. [**データデザイナー** ] ノードを右クリックし、`SmartCaptionReplacement`という名前の新しい**文字列値**を作成します。

10. [**データデザイナー** ] ノードを右クリックし、`SmartCaptionSuffix`という名前の新しい**文字列値**を作成します。

11. **SmartCaptionExpression**アイテムを右クリックし、[**変更**] を選択します。

12. 値として `(.*)` を入力します。 これは、文字列全体に一致します。

13. **SmartCaptionReplacement**アイテムを右クリックし、[**変更**] を選択します。

14. 値として `$1` を入力します。 これにより、文字列が一致した値に置き換えられます。文字列全体が変更されずに保持されます。

     次に [**データソース**] ウィンドウから項目をドラッグすると、キャプションラベルが、変更されていないキャプションで作成されます。

## <a name="see-also"></a>参照
 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
