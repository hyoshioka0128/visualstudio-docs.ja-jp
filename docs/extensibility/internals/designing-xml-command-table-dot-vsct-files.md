---
title: XML コマンド テーブルの設計 (.Vsct) ファイル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fcd29aee98139bb151c87590b256df6b8370abff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708753"
---
# <a name="design-xml-command-table-vsct-files"></a>XML コマンド テーブル (.vsct) ファイルを設計する
XML コマンド テーブル (*.vsct*) ファイルは、VSPackage のコマンド項目のレイアウトと外観を記述します。 コマンド項目には、ボタン、コンボ ボックス、メニュー、ツールバー、コマンド項目のグループなどがあります。 この資料では、XML コマンド テーブル ファイル、コマンド項目とメニューに与える影響、およびそれらの作成方法について説明します。

## <a name="commands-menus-groups-and-the-vsct-file"></a>コマンド、メニュー、グループ、および .vsct ファイル
 *vsct*ファイルは、コマンド、メニュー、およびコマンド グループを中心に編成されています。 *.vsct*ファイル内の XML タグは、コマンド ボタン、コマンド配置、ビットマップなどの関連項目と共に、これらの各項目を表します。

 パッケージ テンプレートを実行して新しい VSPackage を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]作成すると、選択内容に応じて、メニュー コマンド、ツール ウィンドウ、またはカスタム エディターに必要な要素を含む *.vsct*ファイルがテンプレートによって生成されます。 この *.vsct*ファイルは、特定の VSPackage の要件を満たすように変更できます。 *vsct*ファイルを変更する方法の例については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 新しい空の *.vsct*ファイルを作成するには、「[方法 : *.vsct*ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)」を参照してください。 作成したら、XML 要素、属性、および値をファイルに追加して、コマンド項目のレイアウトを記述します。 詳細な XML スキーマについては、 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)を参照してください。

## <a name="differences-between-ctc-and-vsct-files"></a>ctc ファイルと .vsct ファイルの違い
 *vsct*ファイルの XML タグの意味は、現在は廃止された *.ctc*ファイル形式のタグと同じですが、実装は少し異なります。

- 新しい**\<extern>** タグは、ツール バーのファイルなど、コンパイルする他の *.h*ファイルを参照する場所です[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- *.vsct*ファイルは **/include**ステートメントをサポートしていますが *、.ctc*ファイルのように、新**\<しいインポート>** 要素も備えています。 違いは **、/include** *はすべての*情報を取り込み、**\<インポート>** は名前だけを取り込む点です。

- *.ctc*ファイルにはプリプロセッサ ディレクティブを定義するヘッダー ファイルが必要ですが *、.vsct*ファイルに必要なファイルはありません。 代わりに *、.vsct*ファイルの下部にある**\<シンボル>** 要素にあるシンボル テーブルにディレクティブを配置します。

- *.vsct*ファイルには**\<注釈>** タグがあり、メモや画像など、任意の情報を埋め込むことができます。

- 値は、項目の属性として格納されます。

- コマンド フラグは個別に格納することも、スタックすることもできます。  ただし、IntelliSense は、スタックされたコマンド フラグでは機能しません。 コマンド フラグの詳細については、 [CommandFlag 要素](../../extensibility/command-flag-element.md)を参照してください。

- 分割ドロップダウン、コンボなど、複数のタイプを指定できます。

- GUID は検証しません。

- 各 UI 要素には、UI 要素と共に表示されるテキストを表す文字列があります。

- 親はオプションです。 省略すると、値 *[グループ不明]* が使用されます。

- *Icon*引数は省略可能です。

- ビットマップ セクション: このセクションは *.ctc*ファイルと同じですが、コンパイル時に*vsct.exe*コンパイラによってプルされるファイル名を Href で指定できるようになりました。

- ResID: 古いビットマップリソースIDを使用することができ *、.ctc*ファイルと同じように動作します。

- HRef: ビットマップ リソースのファイル名を指定できる新しいメソッド。 ここでは、すべてが使用されていることを前提としているので、使用するセクションは省略できます。 コンパイラは、まずファイルのローカル リソースを検索し、次に任意のネット共有、**および /I**スイッチで定義されたリソースを検索します。

- キーバインド: エミュレーターを指定する必要がなくなりました。 指定した場合、コンパイラはエディターとエミュレーターが同じであると見なします。

- キーコード: キーコードが削除されました。 新しいフォーマットは *、キー1、Mod1、Key2、Mod2*です。  文字、16 進数、または VK 定数のいずれかを指定できます。

新しいコンパイラ*vsct.exe*は *、.ctc*ファイルと *.vsct*ファイルの両方をコンパイルします。 ただし、古い*ctc.exe*コンパイラは *.vsct*ファイルを認識またはコンパイルしません。

*vsct.exe*コンパイラを使用して、既存の *.cto*ファイルを *.vsct*ファイルに変換できます。 詳細については、「[方法 : 既存の .cto ファイルから .vsct ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)」を参照してください。

## <a name="the-vsct-file-elements"></a>vsct ファイル要素
 コマンド テーブルには、次の階層と要素があります。

- [コマンド テーブル要素](../../extensibility/commandtable-element.md): VSPackage に関連付けられているすべてのコマンド、メニュー グループ、およびメニューを表します。

- [Extern 要素](../../extensibility/extern-element.md): .vsct ファイルとマージする外部*の .h*ファイルを参照します。

- [要素を含める](../../extensibility/include-element.md): *.vsct*ファイルと共にコンパイルする追加のヘッダー (.h) ファイルを参照します。 *.vsct*ファイルには、コマンド、メニュー グループ、および IDE または他の VSPackage が提供するメニューを定義する定数を含む *.h*ファイルを含めることができます。

- [Commands 要素](../../extensibility/commands-element.md): 実行できる個々のコマンドをすべて表します。 各コマンドには、次の 4 つの子要素があります。

- [メニュー要素](../../extensibility/menus-element.md): VSPackage のすべてのメニューとツール バーを表します。 メニューは、コマンドのグループのコンテナです。

- [グループ要素](../../extensibility/groups-element.md): VSPackage 内のすべてのグループを表します。 グループは、個々のコマンドの集合です。

- [ボタン要素](../../extensibility/buttons-element.md): VSPackage のすべてのコマンド ボタンとメニュー項目を表します。 ボタンは、コマンドに関連付けることができるビジュアル コントロールです。

- [ビットマップ要素](../../extensibility/bitmaps-element.md): VSPackage のすべてのボタンのすべてのビットマップを表します。 ビットマップは、コンテキストに応じてコマンド ボタンの横または横に表示される図です。

- [コマンド配置要素](../../extensibility/commandplacements-element.md): VSPackage のメニューに個々のコマンドを配置する必要がある追加の場所を示します。

- [VisibilityConstraints 要素](../../extensibility/visibilityconstraints-element.md): コマンドを常に表示するか、特定のダイアログ ボックスやウィンドウを表示するときなど、特定のコンテキストでのみ表示するかどうかを指定します。 この要素の値を持つメニューとコマンドは、指定したコンテキストがアクティブな場合にのみ表示されます。 既定の動作では、コマンドは常に表示されます。

- [KeyBindings 要素](../../extensibility/keybindings-element.md): コマンドのキー バインドを指定します。 つまり **、Ctrl**+**S**などのコマンドを実行するために押す必要がある 1 つ以上のキーの組み合わせです。

- [UsedCommands 要素](../../extensibility/usedcommands-element.md):[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]指定したコマンドは他のコードによって実装されますが、現在の VSPackage がアクティブな場合は、コマンドの実装を提供することを環境に通知します。

- [シンボル要素](../../extensibility/symbols-element.md): パッケージ内のすべてのコマンドのシンボル名と GUID ID が含まれます。

## <a name="vsct-file-design-guidelines"></a>.vsct ファイルの設計ガイドライン
 *vsct*ファイルを正しくデザインするには、次のガイドラインに従います。

- コマンドはグループ内にのみ配置でき、グループはメニューにのみ配置でき、メニューはグループ内にのみ配置できます。 メニューのみが実際には IDE に表示され、グループやコマンドは表示されません。

- サブメニューはメニューに直接割り当てることはできませんが、グループに割り当てる必要があります。

- コマンド、サブメニュー、およびグループは、その定義ディレクティブの親フィールドを使用して、1 つの親グループまたはメニューに割り当てることができます。

- ディレクティブの親フィールドを使用してコマンド テーブルを編成する場合、大きな制限があります。 オブジェクトを定義するディレクティブは、親引数を 1 つだけ受け取ることができます。

- コマンド、グループ、またはサブメニューを再利用するには、新しいディレクティブを使用して、独自`GUID:ID`のペアを持つオブジェクトの新しいインスタンスを作成する必要があります。

- 各`GUID:ID`ペアは一意である必要があります。 メニュー、ツールバー、コンテキスト メニューなどに配置されたコマンドの再利用は、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイスによって処理されます。

- コマンドとサブメニューは複数のグループに割り当てることができ、グループは[Commands 要素](../../extensibility/commands-element.md)を使用して複数のメニューに割り当てることができます。

## <a name="vsct-file-notes"></a>.vsct ファイルに関する注意事項
 .vsct ファイルをコンパイルしてネイティブのサテライト DLL に格納した後で *.vsct*ファイルに変更を加えた場合は **、devenv.exe /setup /nosetupvstemplates**を実行する必要があります。 これにより、実験用レジストリで指定された VSPackage リソースを強制的に再読み込みし、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]内部データベースを再構築します。

 開発中に、複数の VSPackage プロジェクトを作成し、IDE で混乱を招く可能性がある実験用レジストリ ハイブに登録することができます。 これを修正するには、実験用ハイブをデフォルトの設定にリセットして、登録されているすべての VSPackage と IDE に加えた変更を削除します。 実験用ハイブをリセットするには、Visual Studio SDK に付属している CreateExpInstance.exe ツールを使用します。 あなたはそれを見つけることができます:

 *%プログラムファイル(x86)%\Visual\\\<Studio バージョン> SDK\VisualStudio 統合\ツール\ビン\CreateExpInstance.exe*

 **コマンドを**使用してツールを実行します。 このツールは、通常は と一緒[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]にインストールされていない登録済み VSPackages をすべて実験用ハイブから削除することを忘れないでください。

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)
