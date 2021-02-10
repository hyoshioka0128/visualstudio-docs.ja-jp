---
title: 従来の言語サービスでのナビゲーションバーのサポート
description: 従来の言語サービスでナビゲーションバーをサポートする方法について説明します。 エディタービューのナビゲーションバーには、ファイル内の型とメンバーが表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d33b8452f727037226a50abe6a9493ce132e9564
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99932580"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>従来の言語サービスでのナビゲーション バーのサポート
エディタービューの上部にあるナビゲーションバーには、ファイル内の型とメンバーが表示されます。 型は左のドロップダウンリストに表示され、メンバーは右のドロップダウンリストに表示されます。 ユーザーが型を選択すると、カレットが型の最初の行に配置されます。 ユーザーがメンバーを選択すると、そのメンバーの定義にカレットが配置されます。 ドロップダウンボックスは、カレットの現在位置を反映して更新されます。

## <a name="displaying-and-updating-the-navigation-bar"></a>ナビゲーションバーの表示と更新
 ナビゲーションバーをサポートするには、クラスからクラスを派生させ、メソッドを実装する必要があり <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> ます。 言語サービスにコードウィンドウが指定されている場合、基本クラスはをインスタンス化します。これには、 <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.CodeWindowManager> コードウィンドウを表すオブジェクトが含まれてい <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> ます。 次に、 <xref:Microsoft.VisualStudio.Package.CodeWindowManager> オブジェクトに新しいオブジェクトを指定し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。 メソッドは、 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> オブジェクトを取得し <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> ます。 クラスのインスタンスを返す場合 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 、はメソッドを <xref:Microsoft.VisualStudio.Package.CodeWindowManager> 呼び出して内部リストに値を <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 設定し、オブジェクトを <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ドロップダウンバーマネージャーに渡します。 次に、ドロップダウンバーマネージャーが <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A> オブジェクトに対してメソッドを呼び出し、 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar> 2 つのドロップダウンバーを保持するオブジェクトを確立します。

 カーソルを移動すると、メソッドは <xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A> メソッドを呼び出し <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> ます。 基本メソッドは、クラスのメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> ナビゲーションバーの状態を更新します。 オブジェクトのセットを <xref:Microsoft.VisualStudio.Package.DropDownMember> このメソッドに渡します。 各オブジェクトは、ドロップダウンのエントリを表します。

## <a name="the-contents-of-the-navigation-bar"></a>ナビゲーションバーの内容
 通常、ナビゲーションバーには、型のリストとメンバーの一覧が含まれています。 型の一覧には、現在のソースファイルで使用できるすべての型が含まれています。 型名には、完全な名前空間情報が含まれます。 2つの型を持つ C# コードの例を次に示します。

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

 型リストにとが表示され `TestLanguagePackage.TestLanguageService` `TestLanguagePackage.TestLanguageService.Tokens` ます。

 [メンバー] 一覧には、[種類] ボックスの一覧で選択した型の使用可能なメンバーが表示されます。 上のコード例を使用して、が選択されている場合は、 `TestLanguagePackage.TestLanguageService` メンバーの一覧にプライベートメンバーとが含まれ `tokens` `serviceName` ます。 内部構造体 `Token` は表示されません。

 メンバーの一覧を実装すると、カレットをその内側に置いたときに、メンバーの名前を太字にすることができます。 また、メンバーを淡色表示で表示することもできます。これは、カレットが現在配置されているスコープ内にないことを示します。

## <a name="enabling-support-for-the-navigation-bar"></a>ナビゲーションバーのサポートを有効にする
 ナビゲーションバーのサポートを有効にするには、 `ShowDropdownBarOption` 属性のパラメーターをに設定する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> `true` ます。 このパラメーターは、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> プロパティを設定します。 ナビゲーションバーをサポートするには、クラスのメソッドにオブジェクトを実装する必要があり <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> ます。

 メソッドの実装で、 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> プロパティがに設定されている場合は、 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> `true` オブジェクトを返すことができ <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> ます。 オブジェクトを返さない場合、ナビゲーションバーは表示されません。

 ナビゲーションバーを表示するオプションは、ユーザーが設定できます。これにより、エディタービューが開いている間にこのコントロールがリセットされる可能性があります。 ユーザーは、変更が行われる前に、エディターウィンドウを閉じて再度開く必要があります。

## <a name="implementing-support-for-the-navigation-bar"></a>ナビゲーションバーのサポートの実装
 メソッドは、 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 2 つのリスト (ドロップダウンごとに1つ) と、各リスト内の現在の選択範囲を表す2つの値を受け取ります。 リストと選択値を更新できます。この場合、メソッドは、 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> リストが `true` 変更されたことを示すためにを返す必要があります。

 [型] ドロップダウンで選択内容が変更されると、メンバーの一覧を更新して新しい型を反映する必要があります。 メンバーの一覧に表示される内容は、次のいずれかになります。

- 現在の型のメンバーの一覧。

- ソースファイルで使用できるすべてのメンバー。ただし、現在の型に含まれていないすべてのメンバーが淡色表示されます。 ユーザーは、グレー表示されたメンバーを選択してクイックナビゲーションに使用することもできますが、色は現在選択されている種類の一部ではないことを示しています。

  メソッドの実装は、 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 通常、次の手順を実行します。

1. ソースファイルの現在の宣言の一覧を取得します。

     リストを設定するには、いくつかの方法があります。 1つの方法は、 <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> すべての宣言の一覧を返すカスタム解析の理由を指定して、メソッドを呼び出すクラスのバージョンにカスタムメソッドを作成することです。 別の方法として、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> カスタム解析の理由を指定してメソッドからメソッドを直接呼び出すこともでき <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> ます。 3番目の方法では、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの最後の完全な解析操作によって返されたクラスの宣言をキャッシュ <xref:Microsoft.VisualStudio.Package.LanguageService> し、メソッドからそれを取得し <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> ます。

2. 型の一覧を設定または更新します。

     型リストの内容は、ソースが変更されたとき、または現在のキャレット位置に基づいて型のテキストスタイルを変更するように選択した場合に更新される可能性があります。 この位置はメソッドに渡されることに注意 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> してください。

3. 現在のキャレット位置に基づいて、[型] ボックスの一覧で選択する型を決定します。

     手順 1. で取得した宣言を検索して、現在のキャレット位置を囲む型を検索し、その型の型リストを検索して、型の一覧にインデックスを決定できます。

4. 選択した型に基づいてメンバーの一覧を作成または更新します。

     メンバーの一覧には、[ **メンバー** ] ボックスの一覧に現在表示されている内容が反映されます。 ソースが変更された場合、または選択した型のメンバーだけを表示し、選択した型が変更されている場合は、メンバーリストの内容を更新する必要があります。 ソースファイル内のすべてのメンバーを表示することを選択した場合は、現在選択されている型が変更されている場合は、リスト内の各メンバーのテキストスタイルを更新する必要があります。

5. 現在のキャレットの位置に基づいてメンバーの一覧で選択するメンバーを決定します。

     手順1で取得した宣言を現在のキャレット位置を含むメンバーに対して検索し、そのメンバーのメンバーリストを検索して、メンバーリストのインデックスを決定します。

6. リストに何らかの `true` 変更が加えられた場合、またはいずれかの一覧で選択した場合は、を返します。
