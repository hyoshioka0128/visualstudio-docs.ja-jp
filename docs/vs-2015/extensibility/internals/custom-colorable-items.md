---
title: カスタム装飾 Items |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 24a4db907ec859c6075c06956f86939047379897
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "91102536"
---
# <a name="custom-colorable-items"></a>カスタムの配色可能な項目
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

言語サービスの一部としてカスタム装飾項目を実装することで、キーワードやコメントなど、色分けの型の一覧をオーバーライドできます。  
  
## <a name="user-settings-of-colorable-items"></a>装飾 Items のユーザー設定  
 [**フォントおよび色**] ダイアログボックスを表示するには、[**ツール**] メニューの [**オプション**] を選択し、[**環境**] の [**フォントおよび色**] を選択します。 **テキストエディター**や**コマンドウィンドウ**などの表示を選択すると、[**表示項目**] ボックスに、その表示のすべての装飾項目が表示されます。 各装飾項目のフォント、サイズ、前景色、および背景色を表示および変更できます。 選択内容は、レジストリのキャッシュに格納され、装飾項目名によってアクセスされます。  
  
## <a name="presentation-of-colorable-items"></a>装飾項目のプレゼンテーション  
 IDE では、[ **フォントおよび色** ] ダイアログボックスの装飾項目のユーザーオーバーライドが処理されるため、各カスタム装飾項目には名前を指定するだけで済みます。 この名前は、[ **表示項目** ] の一覧に表示されます。 装飾項目はアルファベット順に表示されます。 言語サービスのカスタム装飾アイテムをグループ化するには、それぞれの言語名で各名前を開始します ( **Newlanguage-Comment** や **Newlanguage-Keyword**など)。  
  
> [!CAUTION]
> 既存の装飾項目名との競合を避けるために、装飾項目名に言語名を含める必要があります。 開発中にいずれかの装飾項目の名前を変更した場合は、装飾項目に初めてアクセスしたときに作成されたキャッシュをリセットする必要があります。 Visual Studio SDK と共にインストールされる Createのインスタンスツールを使用して試験的なキャッシュをリセットできます。通常はディレクトリにあります。  
>   
> **C:\Program Files (x86) \Microsoft Visual Studio 14.0 \ VSSDK\VisualStudioIntegration\Tools\Bin**  
>   
> キャッシュをリセットするには、を呼び出し `CreateExpInstance /Reset` ます。 Createのインスタンスの詳細については、「 [Createのインスタンスユーティリティ](../../extensibility/internals/createexpinstance-utility.md)」を参照してください。  
  
 装飾項目の一覧の最初の項目は参照されません。 最初の項目は、0の装飾 item インデックスに対応し、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] その項目の既定のテキストの色と属性を常に提供します。 この未参照の項目を処理する最も簡単な方法は、リスト内のプレースホルダー装飾項目を最初の項目として指定することです。  
  
## <a name="implementing-custom-colorable-items"></a>カスタム装飾項目の実装  
  
1. キーワード、演算子、識別子など、お使いの言語で色付けが必要なものを定義します。  
  
2. これらの装飾 items の列挙体を作成します。  
  
3. パーサーまたはスキャナーから返されたトークンの種類を列挙値に関連付けます。  
  
    たとえば、トークン型を表す値は、custom 装飾 items 列挙型の値と同じにすることができます。  
  
4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>オブジェクトのメソッドの実装で、[ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 属性] の一覧に、パーサーまたはスキャナーから返されたトークンの種類に対応するカスタム装飾 items 列挙子の値を入力します。  
  
5. インターフェイスを実装するクラスと同じクラスで、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> インターフェイスと、との2つのメソッドを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> ます。  
  
6. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> インターフェイスを実装します。  
  
7. 24ビットまたは高色の値をサポートする場合は、インターフェイスも実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> ます。  
  
8. 言語サービスオブジェクトで、オブジェクトを含むリストを作成し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> ます。このリストには、パーサーまたはスキャナーが識別できる各装飾項目が含まれます。  
  
    リスト内の各項目には、custom 装飾 items 列挙子の対応する値を使用してアクセスできます。 列挙値は、一覧のインデックスとして使用します。 リスト内の最初の項目は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 常にそれ自体を処理する既定のテキストスタイルに対応しているため、アクセスされません。 このことを補うには、リストの先頭に装飾 item というプレースホルダーを挿入します。  
  
9. メソッドの実装で <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> 、カスタム装飾 items リスト内の項目数を返します。  
  
10. メソッドの実装で <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 、要求された装飾項目をリストから取得します。  
  
    インターフェイスとインターフェイスを実装する方法の例につい <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> ては、「」を参照してください <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 。  
  
## <a name="see-also"></a>参照  
 [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)   
 [カスタムエディターでの構文の色分け](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [実装 (構文の色分けを)](../../extensibility/internals/implementing-syntax-coloring.md)   
 [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
