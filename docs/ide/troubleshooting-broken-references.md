---
title: 壊れた参照のトラブルシューティング
ms.date: 03/21/2017
ms.topic: troubleshooting
helpviewer_keywords:
- C# projects, references
- Visual Basic projects, references
- troubleshooting references
- referencing files from projects
- referencing components, troubleshooting
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5116d2487ca9f53c460e1cae8f362f3ff1bcdf8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75565917"
---
# <a name="troubleshoot-broken-references"></a>壊れた参照のトラブルシューティング

アプリケーションが、壊れている参照を使用しようとすると例外エラーが生成されます。 エラーの主なトリガーは参照先のコンポーネントを見つけられないことですが、参照が壊れていると考えられるいくつかの状況があります。 これらの例を次のリストに示します。

- プロジェクトの参照パスが不正確または不完全な場合。

- 参照されているファイルが削除されている場合。

- 参照されているファイルの名前が変更されている場合。

- ネットワーク接続または認証に失敗した場合。

- 参照先が、コンピューターにインストールされていない COM コンポーネントになっている場合。

これらの問題に対する解決策を次に示します。

> [!NOTE]
> アセンブリ内のファイルは、プロジェクト ファイルの絶対パスで参照されます。 したがって、複数の開発者がいる環境で作業しているユーザーには、ローカル環境で参照されるアセンブリがなくなる可能性があります。 これらのエラーを避けるためには、このような場合にプロジェクト間参照を追加することをお勧めします。 詳細については、「[アセンブリを使用したプログラミング](/dotnet/framework/app-domains/programming-with-assemblies)」を参照してください。

## <a name="reference-path-is-incorrect"></a>参照パスが正しくない

異なるコンピューターでプロジェクトを共有している場合、コンポーネントが各コンピューターで異なるディレクトリに配置されていると、一部の参照が見つからない場合があります。 参照は、コンポーネント ファイルの名前 (*MyComponent* など) で格納されます。 参照がプロジェクトに追加されると、コンポーネント ファイルのフォルダーの場所 (*C:\MyComponents* など) が **ReferencePath** プロジェクト プロパティに追加されます。

プロジェクトを開くと、参照パスで指定したディレクトリ内を検索して、これらの参照先のコンポーネント ファイルを検索しようとします。 コンポーネントを *D:\MyComponents* などの別のディレクトリに格納しているコンピューターでプロジェクトを開くと、参照が見つらず、 **[タスク一覧]** にエラーが表示されます。

この問題を解決するには、壊れている参照を削除し、 **[参照の追加]** ダイアログ ボックスを使用してこれを置き換えます。 別の解決策は、プロジェクトのプロパティ ページで **[参照パス]** 項目を使用して、一覧内のフォルダーを適切な場所を指すように変更することです。 **[参照パス]** プロパティは、各コンピューターのユーザーごとに保持されます。 したがって、参照パスを変更しても、プロジェクトの他のユーザーには影響しません。

> [!TIP]
> プロジェクト間参照には、これらの問題はありません。 このため、可能であれば、ファイル参照の代わりにプロジェクト間参照を使用します。

### <a name="to-fix-a-broken-project-reference-by-correcting-the-reference-path"></a>参照パスを修正して壊れたプロジェクト参照を修正するには

1. **ソリューション エクスプローラー**で、プロジェクト ノードを右クリックし、 **[プロパティ]** をクリックします。

   **プロジェクト デザイナー**が表示されます。

1. Visual Basic を使用している場合は、 **[参照]** ページを選択し、 **[参照パス]** ボタンをクリックします。 **[参照パス]** ダイアログ ボックスで、参照する項目を含むフォルダーのパスを **[フォルダー]** フィールドに入力し、 **[フォルダーの追加]** ボタンをクリックします。

    C# を使用している場合は、 **[参照パス]** ページを選択します。 参照する項目を含むフォルダーのパスを **[フォルダー]** フィールドに入力し、 **[フォルダーの追加]** ボタンをクリックします。

## <a name="referenced-file-has-been-deleted"></a>参照先ファイルが削除されている

参照されているファイルが削除されたため、ドライブに存在しません。

### <a name="to-fix-a-broken-project-reference-for-a-file-that-no-longer-exists-on-your-drive"></a>ドライブに存在しなくなったファイルの破損したプロジェクト参照を修正するには

- 参照を削除します。

- 参照がコンピューター上の別の場所にある場合は、その場所から読み取ります。

## <a name="referenced-file-has-been-renamed"></a>参照先のファイル名が変更されている

参照されているファイルの名前が変更されている可能性があります。

### <a name="to-fix-a-broken-reference-for-a-file-that-has-been-renamed"></a>名前が変更されたファイルの壊れた参照を解決するには

- 参照を削除し、名前を変更したファイルへの参照を追加します。

- 参照がコンピューター上の別の場所にある場合は、その場所から読み込む必要があります。

## <a name="network-connection-or-authentication-has-failed"></a>ネットワーク接続または認証に失敗した

ファイルにアクセスできないということには、多くの考えられる原因があります。たとえば、ネットワーク接続の障害や認証の失敗などです。 これらの原因には、たとえば、必須リソースへのアクセスについては、ローカル管理者に連絡する必要があるなど、それぞれ独自の回復方法があります。 ただし、参照を削除して使用したコードを修正することは、常に選択肢の 1 つです。

## <a name="com-component-is-not-installed-on-computer"></a>COM コンポーネントがコンピューターにインストールされていない

ユーザーが COM コンポーネントに参照を追加し、2 番目のユーザーが、このコンポーネントがインストールされていないコンピューターでコードを実行しようとすると、2 番目のユーザーは、参照が壊れているというエラーを受信します。 2 番目のコンピューターにコンポーネントをインストールすると、エラーが修正されます。 プロジェクトで COM コンポーネントへの参照を使用する方法の詳細については、「[.NET Framework アプリケーションにおける COM 相互運用性](/dotnet/visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications)」を参照してください。

## <a name="see-also"></a>参照

- [[参照設定] ページ (プロジェクト デザイナー) (Visual Basic)](../ide/reference/references-page-project-designer-visual-basic.md)
