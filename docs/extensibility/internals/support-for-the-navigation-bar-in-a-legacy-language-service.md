---
title: 従来の言語サービスでのナビゲーション バーのサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f86dabb0594b1e33c45808efb387fcbe313e3de3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704857"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>従来の言語サービスでのナビゲーション バーのサポート
エディター ビューの上部にあるナビゲーション バーには、ファイル内の型とメンバーが表示されます。 左側のドロップダウンに型が表示され、メンバーが右のドロップダウンに表示されます。 ユーザーがタイプを選択すると、キャレットはタイプの最初の行に配置されます。 ユーザーがメンバーを選択すると、キャレットはメンバーの定義に配置されます。 ドロップダウン ボックスが更新され、キャレットの現在の位置が反映されます。

## <a name="displaying-and-updating-the-navigation-bar"></a>ナビゲーション バーの表示と更新
 ナビゲーション バーをサポートするには、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>クラスからクラスを派生させ、メソッドを実装<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>する必要があります。 言語サービスにコード ウィンドウが与えられると、基本<xref:Microsoft.VisualStudio.Package.LanguageService>クラスは、コード<xref:Microsoft.VisualStudio.Package.CodeWindowManager>ウィンドウを表<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>すオブジェクトを含む をインスタンス化します。 オブジェクト<xref:Microsoft.VisualStudio.Package.CodeWindowManager>には新しい<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>オブジェクトが与えられます。 メソッド<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>はオブジェクトを<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>取得します。 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>クラスのインスタンスを返す場合は、メソッド<xref:Microsoft.VisualStudio.Package.CodeWindowManager>を<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>呼び出して内部リストにデータを入力し<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>、オブジェクトを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ドロップダウン バー マネージャーに渡します。 ドロップダウン バー マネージャーは、オブジェクトのメソッドを<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A>呼び出して<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>、2 つの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>ドロップダウン バーを保持するオブジェクトを確立します。

 キャレットが移動すると、メソッド<xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A>はメソッドを<xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A>呼び出します。 基本<xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A>メソッドは、クラス<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>内のメソッド<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>を呼び出して、ナビゲーション バーの状態を更新します。 このメソッドにオブジェクトの<xref:Microsoft.VisualStudio.Package.DropDownMember>セットを渡します。 各オブジェクトは、ドロップダウンのエントリを表します。

## <a name="the-contents-of-the-navigation-bar"></a>ナビゲーション バーの内容
 通常、ナビゲーション バーには型のリストとメンバーのリストが含まれます。 型のリストには、現在のソース ファイルで使用できるすべての型が含まれます。 型名には、完全な名前空間情報が含まれます。 次に、2 つの型を持つ C# コードの例を示します。

```csharp
namespace TestLanguagePackage
{
    public class TestLanguageService
    {
        internal struct Token
        {
            int tokenID;
        }
        private Tokens[] tokens;
        private string serviceName;
    }
}
```

 型リストに と`TestLanguagePackage.TestLanguageService``TestLanguagePackage.TestLanguageService.Tokens`が表示されます。

 メンバー リストには、型リストで選択されている型の使用可能なメンバーが表示されます。 上記のコード例を使用して`TestLanguagePackage.TestLanguageService`、選択されている型の場合、メンバ リストにはプライベート メンバ`tokens`と`serviceName`. 内部構造`Token`は表示されません。

 メンバー リストを実装すると、キャレットがメンバーの内部に配置されたときにメンバーの名前を太字にすることができます。 メンバーは、現在キャレットが配置されているスコープ内にないことを示す、淡色表示されたテキストで表示することもできます。

## <a name="enabling-support-for-the-navigation-bar"></a>ナビゲーション バーのサポートの有効化
 ナビゲーション バーのサポートを有効にするには、属性のパラメーター`ShowDropdownBarOption`を<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>に設定する`true`必要があります。 このパラメーターは、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> プロパティを設定します。 ナビゲーション バーをサポートするには、クラスの<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>メソッドにオブジェクトを<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>実装する<xref:Microsoft.VisualStudio.Package.LanguageService>必要があります。

 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>メソッドの実装で、プロパティが<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A>に`true`設定されている場合は、オブジェクトを<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>返すことができます。 オブジェクトを返さない場合、ナビゲーション バーは表示されません。

 ナビゲーション バーを表示するオプションはユーザーが設定できるため、エディター ビューを開いている間にこのコントロールをリセットできます。 変更を行う前に、ユーザーはエディタ ウィンドウを閉じて再度開く必要があります。

## <a name="implementing-support-for-the-navigation-bar"></a>ナビゲーション バーのサポートの実装
 この<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>メソッドは、ドロップダウンリストごとに 2 つのリストと、各リストの現在の選択を表す 2 つの値を取ります。 リストと選択値を更新<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>`true`できます。

 型ドロップダウンで選択が変更されると、新しい型を反映するようにメンバ リストを更新する必要があります。 メンバ リストに表示される内容は、次のいずれかです。

- 現在の型のメンバーのリスト。

- ソース ファイルで使用できるメンバーのうち、現在のタイプに含まれていないメンバーがすべて淡色表示のテキストで表示されます。 ユーザーは、グレー表示されたメンバーを選択できるため、クイック ナビゲーションに使用できますが、色は現在選択されている型の一部ではないことを示します。

  通常、メソッドの<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>実装では、次の手順を実行します。

1. ソース ファイルの現在の宣言の一覧を取得します。

     リストを作成する方法はいくつかあります。 1 つの方法は、すべての宣言のリストを返す<xref:Microsoft.VisualStudio.Package.LanguageService>カスタム解析理由を<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>使用してメソッドを呼び出すクラスのバージョンにカスタム メソッドを作成することです。 別の方法として、メソッドを<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>カスタム解析の理由<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>でメソッドから直接呼び出す方法もあります。 3 番目の方法として、<xref:Microsoft.VisualStudio.Package.AuthoringScope>クラスの最後の完全解析操作によって返されたクラスの宣言を<xref:Microsoft.VisualStudio.Package.LanguageService>キャッシュし、メソッドから取得する<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>方法があります。

2. 型のリストを設定または更新します。

     ソースが変更された場合、または現在のキャレット位置に基づいて型のテキストスタイルを変更することを選択した場合、タイプリストの内容が更新されることがあります。 この位置はメソッドに<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>渡されることに注意してください。

3. 現在のキャレット位置に基づいて、タイプリストで選択するタイプを決定します。

     手順 1 で取得した宣言を検索して、現在のキャレット位置を囲む型を検索し、その型の型リストを検索して、型リストのインデックスを決定できます。

4. 選択した型に基づいてメンバーの一覧を設定または更新します。

     メンバー リストには、[メンバー] ドロップダウンに現在表示されている**内容**が反映されます。 ソースが変更された場合、または選択した型のメンバーのみを表示していて、選択した型が変更されている場合は、メンバー リストの内容を更新する必要があります。 ソース ファイル内のすべてのメンバーを表示するように選択した場合、現在選択されている型が変更された場合は、リスト内の各メンバーのテキストスタイルを更新する必要があります。

5. 現在のキャレット位置に基づいて、メンバーリストで選択するメンバーを決定します。

     ステップ 1 で取得した宣言で、現在のキャレット位置を含むメンバーを検索し、メンバーリストを検索してメンバー・リストの索引を判別します。

6. リスト`true`に変更が加えられた場合、またはいずれかのリストで選択が行われた場合に戻ります。
