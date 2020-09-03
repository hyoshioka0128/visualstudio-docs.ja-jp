---
title: XML コマンドテーブルの設計 (.Vsct) Files |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 987536af051de4a66b3eccadb105fd98455ddf06
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196849"
---
# <a name="designing-xml-command-table-vsct-files"></a>XML コマンド テーブル (.Vsct) ファイルの設計
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

XML コマンドテーブル (vsct) ファイルには、VSPackage のコマンド項目のレイアウトと外観が記述されています。 コマンド項目には、ボタン、コンボボックス、メニュー、ツールバー、およびコマンド項目のグループが含まれます。 このトピックでは、XML コマンドテーブルファイル、コマンド項目とメニューに与える影響、およびそれらを作成する方法について説明します。  
  
## <a name="commands-menus-groups-and-the-vsct-file"></a>コマンド、メニュー、グループ、および. vsct ファイル  
 vsct ファイルは、コマンド、メニュー、およびコマンドグループを中心に構成されています。 Vsct ファイル内の XML タグは、これらの各項目を、コマンドボタン、コマンドの配置、ビットマップなど、関連する他の項目と共に表します。  
  
 パッケージテンプレートを実行して新しい VSPackage を作成すると [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、選択内容に応じて、テンプレートによって、メニューコマンド、ツールウィンドウ、またはカスタムエディターに必要な要素を含む、vsct ファイルが生成されます。 この vsct ファイルは、特定の VSPackage の要件を満たすように変更できます。 Vsct ファイルを変更する方法の例については、「 [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」の例を参照してください。  
  
 新しい空の vsct ファイルを作成するには、「 [方法: を作成する」を参照してください。Vsct ファイル](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。 作成したら、XML 要素、属性、および値をファイルに追加して、コマンド項目のレイアウトを記述します。 詳細な XML スキーマについては、「 [Vsct Xml スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)」を参照してください。  
  
## <a name="differences-between-ctc-and-vsct-files"></a>Ctc ファイルと vsct ファイルの相違点  
 . Vsct ファイルの XML タグの背後にある意味は、現在は非推奨の ctc ファイル形式のものと同じですが、実装は少し異なります。  
  
- 新しい **\<extern>** タグは、ツールバーの場合など、コンパイルする他の .h ファイルを参照する場所です。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]  
  
- の vsct ファイルでは **/include** ステートメントがサポートされますが、ctc ファイルでは新しい \<**import> * * 要素も機能します。 違いは、 **/include** によって **すべて** の情報が表示されますが、 \<**import> * * では名前だけが取り込まれます。  
  
- Ctc ファイルには、プリプロセッサディレクティブを定義するヘッダーファイルが必要ですが、vsct ファイルには必要ありません。 代わりに、 **\<Symbol>** ファイルの末尾にある要素に配置されているシンボルテーブルにディレクティブを配置します。  
  
- vsct ファイル **\<Annotation>** はタグを機能させます。これにより、メモや画像のような情報を埋め込むことができます。  
  
- 値は、項目に属性として格納されます。  
  
- コマンドフラグは、個別に保存することも、スタックに格納することもできます。  ただし、スタックされたコマンドフラグでは、Intellisense は機能しません。 コマンドフラグの詳細については、「 [Command Flag 要素](../../extensibility/command-flag-element.md)」を参照してください。  
  
- Split ドロップダウン、combos など、複数の型を指定できます。  
  
- Guid は検証されません。  
  
- 各 UI 要素には、それと共に表示されるテキストを表す文字列があります。  
  
- 親は省略可能です。 省略した場合、値 "Group Unknown" が使用されます。  
  
- Icon 引数は省略可能です。  
  
- ビットマップセクション--ctc ファイルと同じですが、コンパイル時に vsct.exe コンパイラによってプルされるファイル名を href で指定できる点が異なります。  
  
- ResID--古いビットマップリソース ID を使用できますが、ctc ファイルの場合と同様に動作します。  
  
- HRef--ビットマップリソースのファイル名を指定できる新しいメソッド。 この例では、all が使用されていることを前提としているため、使用するセクションを省略できます。 コンパイラはまず、ファイルのローカルリソース、次に、任意の net 共有、および/I スイッチによって定義されているすべてのリソースを検索します。  
  
- キーバインド--エミュレーターを指定する必要がなくなりました。 1つを指定した場合、コンパイラは、エディターとエミュレーターが同じであると見なします。  
  
- Keychord--が削除されました。 新しい形式は、Key1、Mod1、Key2、Mod2 です。  文字、16進数、または VK 定数のいずれかを指定できます。  
  
  新しいコンパイラである vsct.exe は、ctc ファイルと vsct ファイルの両方をコンパイルします。 ただし、古い ctc.exe コンパイラは、vsct ファイルを認識したりコンパイルしたりすることはありません。  
  
  vsct.exe コンパイラを使用して、既存の cto ファイルを vsct ファイルに変換できます。 詳細については、「 [方法: を作成する」を参照してください。既存のからの vsct ファイル。Cto ファイル](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)。  
  
## <a name="the-vsct-file-elements"></a>Vsct ファイルの要素  
 コマンドテーブルには、次の階層と要素があります。  
  
 [Commandtable 要素](../../extensibility/commandtable-element.md) — VSPackage に関連付けられているすべてのコマンド、メニューグループ、およびメニューを表します。  
  
 [Extern 要素](../../extensibility/extern-element.md) —は、vsct ファイルとマージするすべての外部 .h ファイルを参照します。  
  
 [Include 要素](../../extensibility/include-element.md) : コンパイルする追加のヘッダー (.h) ファイルを、使用する vsct ファイルと共に参照します。 Vsct ファイルには、IDE または別の VSPackage が提供するコマンド、メニューグループ、およびメニューを定義する定数を含む .h ファイルを含めることができます。  
  
 [Commands 要素](../../extensibility/commands-element.md) —実行可能な個々のコマンドをすべて表します。 各コマンドには、次の4つの子要素があります。  
  
 [Menus 要素](../../extensibility/menus-element.md) — VSPackage のすべてのメニューとツールバーを表します。 メニューは、コマンドのグループのコンテナーです。  
  
 [Groups 要素](../../extensibility/groups-element.md) — VSPackage 内のすべてのグループを表します。 グループは、個々のコマンドのコレクションです。  
  
 [Buttons 要素](../../extensibility/buttons-element.md) — VSPackage 内のすべてのコマンドボタンとメニュー項目を表します。 ボタンは、コマンドに関連付けることができるビジュアルコントロールです。  
  
 [ビットマップ要素](../../extensibility/bitmaps-element.md) — VSPackage 内のすべてのボタンのすべてのビットマップを表します。 ビットマップは、コンテキストに応じて、コマンドボタンの横に表示される画像です。  
  
 [Commandplacements 要素](../../extensibility/commandplacements-element.md) — VSPackage のメニューに個々のコマンドを配置する追加の場所を示します。  
  
 [VisibilityConstraints 要素](../../extensibility/visibilityconstraints-element.md) : コマンドを常に表示するかどうか、または特定のダイアログボックスまたはウィンドウが表示されるときなど、特定のコンテキストでのみ表示するかどうかを指定します。 この要素の値を持つメニューとコマンドは、指定されたコンテキストがアクティブな場合にのみ表示されます。 既定の動作では、コマンドは常に表示されます。  
  
 [KeyBindings 要素](../../extensibility/keybindings-element.md) : コマンドのキーバインドを指定します。 つまり、 **CTRL + S**などのコマンドを実行するために押す必要がある1つ以上のキーの組み合わせです。  
  
 使用されている[コマンド要素](../../extensibility/usedcommands-element.md)— [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 指定したコマンドが他のコードによって実装されているが、現在の VSPackage がアクティブになっている場合は、コマンドの実装を提供することを環境に通知します。  
  
 `Symbols Element` -パッケージ内のすべてのコマンドのシンボル名と GUID Id を格納します。  
  
## <a name="vsct-file-design-guidelines"></a>.Vsct ファイルのデザインガイドライン  
 Vsct ファイルを正常にデザインするには、次のガイドラインに従ってください。  
  
- コマンドはグループにのみ配置できます。グループはメニューだけに配置でき、メニューはグループにのみ配置できます。 実際には、IDE にはメニューのみが表示され、グループおよびコマンドは表示されません。  
  
- サブメニューをメニューに直接割り当てることはできませんが、グループに割り当てられている必要があります。これは、メニューに割り当てられています。  
  
- コマンド、サブメニュー、およびグループは、定義するディレクティブの親フィールドを使用して、1つの親グループまたはメニューに割り当てることができます。  
  
- ディレクティブ内の親フィールドだけを使用してコマンドテーブルを整理すると、大きな制限があります。 オブジェクトを定義するディレクティブは、1つの親引数のみを受け取ることができます。  
  
- コマンド、グループ、またはサブメニューを再利用するには、新しいディレクティブを使用して、オブジェクトの新しいインスタンスを独自のペアで作成する必要があり `GUID:ID` ます。  
  
- 各 `GUID:ID` ペアは一意である必要があります。 たとえば、メニュー、ツールバー、またはコンテキストメニューに配置されたコマンドを再利用すると、インターフェイスによって処理され <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。  
  
- コマンドとサブメニューを複数のグループに割り当てることもできます。また、複数のメニューには、 [コマンド要素](../../extensibility/commands-element.md)を使用してグループを割り当てることができます。  
  
## <a name="vsct-file-notes"></a>.Vsct ファイルのメモ  
 両方のファイルをコンパイルしてネイティブサテライト DLL に配置した後に、そのファイルに対して変更を加えた場合は、 **devenv.exe/nosetupvstemplates**を実行する必要があります。 これにより、実験的なレジストリに指定されている VSPackage リソースが再読み込みされ、が記述されている内部データベースが [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 再構築されます。  
  
 開発時には、複数の VSPackage プロジェクトを実験用レジストリハイブに作成して登録することができます。これにより、IDE で混乱を招く可能性があります。 この問題を解決するには、実験的なハイブを既定の設定にリセットして、登録されているすべての Vspackage と IDE に加えられたすべての変更を削除します。 実験用ハイブをリセットするには、Visual Studio SDK に付属の CreateExpInstance.exe ツールを使用します。 確認するには  
  
 **% PROGRAMFILES (x86)% \ Visual Studio \<version> SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe**  
  
 コマンドラインの **Createexpinstance/Reset**を使用して、ツールを実行します。 このツールは、通常インストールされていない、登録済みのすべての Vspackage を実験的なハイブから削除することに注意してください [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="see-also"></a>参照  
 [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)
