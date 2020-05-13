---
title: Visual Studio for Mac Tools for Unity を使用する
description: このガイドでは、Visual Studio for Mac Tools for Unity 拡張機能を使用する方法について説明します
author: therealjohn
ms.author: johmil
ms.date: 07/17/2017
ms.assetid: 83FDD7A3-5D16-4B4B-9080-078E3FB5C623
ms.openlocfilehash: d4df59273db1fab8492b36e87e48e0e770072f17
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "79306705"
---
# <a name="using-visual-studio-for-mac-tools-for-unity"></a>Visual Studio for Mac Tools for Unity を使用する

このセクションでは、Visual Studio for Mac Tools for Unity の統合と生産性の機能の使い方、および Unity 開発での Visual Studio for Mac デバッガーの使い方について説明します。

## <a name="opening-unity-scripts-in-visual-studio-for-mac"></a>Visual Studio for Mac で Unity スクリプトを開く

Visual Studio for Mac を [Unity の外部スクリプト エディターとして設定](setup-vsmac-tools-unity.md#configure-unity-for-use-with-visual-studio-for-mac)した後は、Unity エディターからスクリプトを開くと、自動的に Visual Studio for Mac が起動するか、または Visual Studio for Mac に切り替わり、選んだスクリプトが開かれます。

または、Unity の **[Assets]\(アセット\)** メニューから **[Open C# Project]\(C# プロジェクトを開く\)** を選ぶことで、ソース エディターでスクリプトを開かずに Visual Studio for Mac を起動できます。

![C# プロジェクトを開く](media/using-vsmac-tools-unity-image1.png)

## <a name="unity-documentation-access"></a>Unity のドキュメントへのアクセス

Visual Studio for Mac Tools for Unity には、Unity API のドキュメントにアクセスするためのショートカットが含まれています。 Visual Studio for Mac から Unity API のドキュメントにアクセスするには、説明を見たい Unity API をポイントし、**⌘ コマンド + ‘** キーを押します。

## <a name="intellisense-for-unity-messages"></a>Unity メッセージ用の IntelliSense
Unity エンジンは MonoBehaviour スクリプトにメッセージをブロードキャストするので、OnMouseDown や OnTriggerEnter などのメッセージに応答するコードを記述できます。MonoBehaviour の基底クラスではこれらは仮想メソッドではないので、MonoDevelop などの一部の IDE には Unity メッセージ用のコード補完機能がありません。

ただし、Visual Studio for Mac Tools for Unity では、Unity メッセージ対応に IntelliSense 機能が拡張されています。 これにより、MonoBehaviour スクリプトに Unity メッセージを簡単に実装でき、Unity API の学習に役立ちます。 Unity メッセージ用の IntelliSense を使うには:

1. MonoBehaviour から派生するクラスの本体内部の新しい行にカーソルを置きます。

2. Unity メッセージの名前 (`OnTriggerEnter` など) の入力を始めます。

3. 「**ont**」まで入力すると、intellisense による候補の一覧が表示されます。

   ![Using IntelliSense](media/using-vsmac-tools-unity-image2.png)

4. 一覧での選択は、次の 3 つの方法で変更できます。

   * **上**および**下**方向キーを使います。

   * 目的の項目をマウスでクリックします。

   * 目的の項目の名前の入力を続けます。

5. IntelliSense で選んだ Unity メッセージと必要なパラメーターを挿入するには、次のようにします。

   * **Tab** キーを押します。

   * **Return** キーを押します。

   * 選んだ項目をダブルクリックします。

   ![IntelliSense から Unity メッセージを挿入する](media/using-vsmac-tools-unity-image3.png)

## <a name="adding-new-unity-files-and-folders"></a>Unity の新しいファイルおよびフォルダーを追加する

いつでも Unity エディターで Unity プロジェクトに新しいファイルを追加できますが、Visual Studio for Mac を使うと、新しい Unity スクリプト、シェーダー、フォルダーを Visual Studio 内から簡単に作成できます。

### <a name="add-a-new-c-monobehaviour-script"></a>新しい C# MonoBehaviour スクリプトを追加する

新しい C# MonoBehaviour スクリプトを追加するには、 **[Assets]\(アセット\) フォルダーを右クリックする**か、または [Solution]\(ソリューション\) パッドでそのサブディレクトリの 1 つを右クリックして、 **[Add]\(追加\) > [New MonoBehaviour]\(新しい MonoBehaviour\)** を選びます。

![新しい MonoBehaviour を追加する](media/using-vsmac-tools-unity-image4.png)

### <a name="add-a-new-unity-shader"></a>新しい Unity シェーダーを追加する

新しい Unity シェーダーを追加するには、 **[アセット] フォルダーを右クリックする**か、または [ソリューション] パッドでサブディレクトリを右クリックして、 **[追加]、[新しいシェーダー]** の順に選びます。

### <a name="add-a-new-folder"></a>新しいフォルダーを追加する

新しいフォルダーを追加するには、 **[Assets]\(アセット\) フォルダーを右クリックする**か、または [Solution]\(ソリューション\) パッドでサブディレクトリを右クリックして、 **[Add]\(追加\) > [New Folder]\(新しいフォルダー\)** を選びます。

これらの追加は、Unity エディターの [Project]\(プロジェクト\) ウィンドウに反映されます。

### <a name="to-rename-a-file-or-folder"></a>ファイルまたはフォルダーの名前を変更するには
[Solution]\(ソリューション\) パッドで名前を変更する項目を**右クリック**し、 **[Rename]\(名前の変更\)** を選びます。

> [!NOTE]
> 新しい Unity プロジェクトにスクリプトが含まれず、[Assets]\(アセット\) フォルダーが Visual Studio for Mac の [Solution]\(ソリューション\) パッドに表示されない場合は、Unity エディター内から最初の C# スクリプトを追加します。

## <a name="unity-debugging"></a>Unity のデバッグ

Unity プロジェクトは Visual Studio for Mac でデバッグすることができます。

### <a name="start-debugging"></a>[デバッグ開始]

デバッグを開始するには:

1. **[再生]** ボタンをクリックするか、**Command + Return** キーまたは **F5** キーを押して、Visual Studio を Unity に接続します。

   ![Visual Studio で [再生] をクリックする](media/using-vsmac-tools-unity-image5.png)

2. Unity に切り替えた後、 **[Play]\(再生\)** ボタンをクリックしてエディターでゲームを実行します。

   ![Unity で [Play]\(再生\) をクリックする](media/using-vsmac-tools-unity-image6.png)

3. Visual Studio に接続しながら Unity エディターでゲームを実行しているときに、ブレークポイントに達すると、ゲームの実行は一時停止し、ゲームがブレークポイントにヒットしたコード行が Visual Studio for Mac に表示されます。

### <a name="stop-debugging"></a>デバッグの停止

デバッグを停止するには:

1. Visual Studio for Mac で **[停止]** ボタンをクリックするか、**Shift + Command + Return** キーを押します。

   ![Visual Studio で [停止] をクリックする](media/using-vsmac-tools-unity-image7.png)

Visual Studio for Mac でのデバッグについて詳しくは、「[Using the debugger](debugging.md)」(デバッガーの使用) をご覧ください。
