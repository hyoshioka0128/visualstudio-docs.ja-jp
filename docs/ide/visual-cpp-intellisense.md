---
title: C++ IntelliSense
ms.date: 10/08/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: c0d1be12f733a858bf223fb1dce6a091c0dc6c50
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594215"
---
# <a name="visual-c-intellisense-features"></a>Visual C++ IntelliSense の機能

IntelliSense は、コード作成をより便利にするための一連の機能に与えられた名前です。 C++ 用の IntelliSense は、スタンドアロン ファイルおよび C++ プロジェクトの一部を成すファイルで使用することができます。 クロスプラットフォーム プロジェクトでは、いくつかの IntelliSense 機能が、Android や iOS のコンテキスト内にいるときでも共有コード プロジェクト内の *.cpp* および *.c* ファイルで使用できます。

この記事では、C++ IntelliSense 機能の概要について説明します。 IntelliSense 用にプロジェクトを構成する方法、および問題をトラブルシューティングする方法については、「[IntelliSense の C++ プロジェクトを構成する](visual-cpp-intellisense-configuration.md)」をご覧ください。

## <a name="intellisense-features-in-c"></a>C++ の IntelliSense 機能

IntelliSense は、コード作成をより便利にするための一連の機能に与えられた名前です。 便利さについては、人によって考え方が違うので、ほぼすべての IntelliSense 機能を **[テキスト エディター]**  >  **[C/C++]**  >  **[詳細]** の **[オプション]** ダイアログボックスで有効または無効にできます。 **[オプション]** ダイアログ ボックスは、メニュー バーの **[ツール]** メニューから使用できます。

![[オプション] ダイアログ ボックス](../ide/media/sintellisensecpptoolsoptions.PNG)

次の画像のメニュー項目とキーボード ショートカットを使用すると、IntelliSense にアクセスできます。

![IntelliSense メニュー](../ide/media/vs2015_cpp_intellisense_menu.png)

## <a name="statement-completion-and-member-list"></a>ステートメント入力候補およびメンバーの一覧

キーワード、型、関数、変数名、またはコンパイラが認識するその他のプログラム要素の入力を開始すると、エディターがワードの入力候補を提供します。

アイコンとその意味の一覧は、「[[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン](../ide/class-view-and-object-browser-icons.md)」を参照してください。

![Visual C&#43;&#43; の入力候補ウィンドウ](../ide/media/vs2015_cpp_complete_word.png)

メンバーの一覧を最初に起動するときに、現在のコンテキストにアクセス可能であるメンバーだけが表示されます。 その後 **Ctrl**+**J** キーを押すと、アクセシビリティにかかわらず、すべてのメンバーが表示されます。 3 回目に実行すると、プログラム要素のより多くの一覧が表示されます。 **[テキスト エディター]**  >  **[C/C++]**  >  **[ 全般]**  >  **[自動メンバー表示]** の **[オプション]** ダイアログ ボックスでメンバーの一覧をオフに切り替えることができます。

![Visual C&#43;&#43; のメンバー リスト](../ide/media/vs2015_cpp_list_members.png)

## <a name="parameter-help"></a>パラメーターのヘルプ

関数呼び出しで左中かっこを入力するか、クラス テンプレートの変数宣言で山かっこを入力すると、エディターは関数またはコンストラクターの各オーバーロードのパラメーターの型を含む小さいウィンドウを表示します。 &mdash;カーソルの場所&mdash;に基づく「現在」のパラメーターは、太字で表示します。 **[テキスト エディター]**  >  **[C/C++]**  >  **[全般]**  >  **[パラメーター情報]** の **[オプション]** ダイアログ ボックスでパラメーター情報をオフにすることができます。

![Visual C&#43;&#43; パラメーターのヘルプ](../ide/media/vs_2015_cpp_param_help.png)

## <a name="quick-info"></a>クイック ヒント

変数の上にマウス カーソルを移動すると、小さなウィンドウがインラインで表示され、型の情報と型が定義されているヘッダーが表示されます。 関数のシグネチャを表示するには、関数呼び出しの上にカーソルを置きます。 **[テキスト エディター]**  >  **[C/C++]**  >  **[詳細]**  >  **[自動クイック ヒント]** の **[オプション]** ダイアログ ボックスでクイック ヒントをオフにすることができます。

![Visual C&#43;&#43; の QuickInfo](../ide/media/vs2015_cpp_quickinfo.png)

## <a name="error-squiggles"></a>エラーの波線

プログラム要素 (変数、キーワード、中かっこ、型名など) の下の波線は、コード内のエラーや潜在的なエラーに注意を引くためのものです。 まだ実装を記述する必要があることを通知するために、事前宣言を記述するときに、緑の波線が表示されます。 Windows のコンテキストで作業しているものの、Android のコンテキストではエラーになる内容を入力するなど、現在アクティブでないコードにエラーがある場合、共有プロジェクトに紫の波線が表示されます。 赤の波線は、コンパイラ エラーまたは警告が現在のコードにあり、対処する必要があることを示します。

![Visual C&#43;&#43; のエラーの波線](../ide/media/vs2015_cpp_error_quiggles.png)

### <a name="code-colorization-and-fonts"></a>コードの色付けとフォント

**[環境]**  >  **[フォントおよび色]** の **[オプション]** ダイアログ ボックスで既定の色とフォントを変更することができます。 ここでは、エディターだけでなく、多数の UI ウィンドウのフォントを変更することができます。 C++ に固有の設定は "C++" で始まり、その他の設定はすべての言語で利用できます。

## <a name="cross-platform-intellisense"></a>クロスプラットフォームの IntelliSense

共有コード プロジェクトでは、Android のコンテキストを使用している場合でも、波線などのいくつかの IntelliSense 機能を使用できます。 非アクティブなプロジェクトでエラーになるいくつかのコードを記述すると、IntelliSense が波線を表示しますが、現在のコンテキストでのエラーの波線とは色が異なります。

Android や iOS 用にビルドするように構成されている OpenGLES アプリケーションを検討してみましょう。 この図は編集中の共有コードを示します。 この図では、アクティブなプロジェクトは **iOS.StaticLibrary** です。

![アクティブなプロジェクトとして iOS が選択されています。](../ide/media/intellisensecppcrossplatform2.png)

次の点に注意してください。

- `__ANDROID__` が iOS プロジェクトに対して定義されていないため、6 行目の `#ifdef` 分岐は淡色表示で非アクティブ領域として表示されています。

- 11 行目のあいさつの変数は、`HELLO` 識別子で初期化され、赤の波線で表示されています。 これは現在アクティブな iOS プロジェクトに、`HELLO` 識別子が定義されていないためです。

- 12 行目の `BYE` 識別子は、(現在) 非アクティブな **Android.NativeActivity** プロジェクトでは定義されていないため、紫の波線で表示されています。 この行は、iOS がアクティブなプロジェクトの場合にはコンパイルされますが、Android がアクティブなプロジェクトの場合にはコンパイルされません。 これは共有コードのため、現在アクティブな構成でコンパイルする場合でも、コードを修正する必要があります。

アクティブなプロジェクトを Android に変更すると、波線は次のように変化します。

- `__ANDROID__` が Android プロジェクトに対して定義されているため、8 行目の `#else` 分岐は淡色表示で非アクティブ領域として表示されています。

- 11 行目のあいさつの変数は `HELLO` 識別子で初期化され、紫の波線で表示されています。 これは現在アクティブではない iOS プロジェクトに、`HELLO` 識別子が定義されていないためです。

- 12 行目の `BYE` 識別子は、アクティブなプロジェクトで定義されていないため、赤の波線で表示されています。

## <a name="intellisense-for-stand-alone-files"></a>スタンドアロン ファイルの IntelliSense

プロジェクトの外部で 1 つのファイルを開いても、やはり IntelliSense を取得します。 **[テキスト エディター]**  >  **[C/C++]**  >  **[詳細設定]** の **[オプション]** ダイアログ ボックスで特定の IntelliSense 機能を有効または無効にすることができます。 プロジェクトの一部ではない 1 つのファイルに IntelliSense を構成するには、**IntelliSense を表示し、非プロジェクト ファイルのセクション**を確認します。

![Visual C&#43;&#43; の単一ファイルの Intellisense](../ide/media/vs2015_cpp_single_file_intellisense.png)

既定では、単一ファイルの IntelliSense は標準のインクルード ディレクトリだけを使用してヘッダー ファイルを検索します。 他にディレクトリを追加するには、次の図に示すとおり、**ソリューション** ノードのショートカット メニューを開き、 **[デバッグ ソース ファイル]** リストにディレクトリを追加します。

![ヘッダー ファイルまでのパスを追加しています。](../ide/media/intellisensedebugyourcode.jpg)

## <a name="enable-or-disable-features"></a>検索を有効または無効にする

便利さについては、人によって考え方が違うので、ほぼすべての IntelliSense 機能を **[テキスト エディター]**  >  **[C/C++]**  >  **[詳細]** の **[オプション]** ダイアログボックスで有効または無効にできます。 **[オプション]** ダイアログ ボックスは、メニュー バーの **[ツール]** メニューから使用できます。

![[オプション] ダイアログ ボックス](../ide/media/sintellisensecpptoolsoptions.PNG)

## <a name="see-also"></a>関連項目

- [IntelliSense の使用](../ide/using-intellisense.md)
- [IntelliSense の C++ プロジェクトを構成する](visual-cpp-intellisense-configuration.md)
