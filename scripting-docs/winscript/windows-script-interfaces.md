---
title: Microsoft スクリプト インターフェイス | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 4c750627-6797-4857-9f5e-e5f54371f83c
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 141f3f0e60e797a4104c3e276775631f6e9196c5
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835408"
---
# <a name="windows-script-interfaces"></a>Windows スクリプト インターフェイス

Microsoft Windows スクリプト インターフェイスでは、アプリケーションにスクリプトと OLE オートメーションを追加する手段を提供します。 Windows スクリプトに依存しているスクリプト ホストは、複数のソースおよびベンダーからのスクリプト エンジンを使用して、コンポーネント間のスクリプトを管理することができます。 スクリプト自体の実装 (言語、構文、永続的な形式、実行モデルなど) はスクリプト ベンダーに任されます。

Windows スクリプト ドキュメントは、次のセクションに分かれています。

[Windows スクリプト ホスト](../winscript/windows-script-hosts.md)

[Windows スクリプト エンジン](../winscript/windows-script-engines.md)

[アクティブ スクリプトのデバッグの概要](../winscript/active-script-debugging-overview.md)

[アクティブ スクリプト プロファイリングの概要](../winscript/active-script-profiling-overview.md)

[Windows スクリプト インターフェイスのリファレンス](../winscript/reference/windows-script-interfaces-reference.md)

## <a name="windows-script-background"></a>Windows スクリプトの背景

Windows スクリプト インターフェイスは、Windows スクリプト ホストと Windows スクリプト エンジンという 2 つのカテゴリに分類されます。 ホストは、スクリプト エンジンを作成し、スクリプトを実行するためにエンジンで呼び出します。 Windows スクリプト ホストの例は次のとおりです。

- Microsoft Internet Explorer

- インターネット オーサリング ツール

- Shell

Windows スクリプト エンジンは、次のものを含む任意の言語またはランタイム環境向けに開発できます。

- Microsoft Visual Basic Scripting Edition (VBScript)

- Perl

- Lisp

ホストの実装をできる限り柔軟にするために、Windows スクリプト用の OLE オートメーション ラッパーが提供されています。 ただし、このラッパー オブジェクトを使用してスクリプト エンジンをインスタンス化するホストは、Windows スクリプトを直接使用する場合とは異なり、ランタイム名前空間、永続化モデルなどを細かく制御できません。

Windows スクリプトのデザインは、オーサリング環境でのみ必要なインターフェイス要素を分離するので、非オーサリング ホスト (ブラウザーやビューアーなど) とスクリプト エンジン (たとえば、VBScript) の軽量さを維持することができます。

## <a name="windows-script-basic-architecture"></a>Windows スクリプトの基本的なアーキテクチャ

次の図は、Windows スクリプト ホストと Windows スクリプト エンジン間の相互作用を示しています。

ホストとエンジン間の相互作用に必要な手順が次の一覧に示されています。

1. プロジェクトを作成します。 プロジェクトがプロジェクトまたはドキュメントを読み込みます。 (この手順は、Windows スクリプトに固有ではありませんが、完全を期すために含まれています)。

2. Windows スクリプト エンジンを作成します。 ホストが `CoCreateInstance` を呼び出して新しい Windows スクリプト エンジンを作成し、使用する特定のスクリプト エンジンのクラス ID (CLSID) を指定します。 たとえば、Internet Explorer の HTML ブラウザーは、HTML タグの CLSID = 属性を使用して、スクリプトエンジンのクラス識別子を受け取り \<OBJECT> ます。

3. スクリプトを読み込みます。 スクリプトの内容が永続化されている場合、ホストは、スクリプト エンジンの `IPersist*::Load` メソッドを呼び出して、スクリプト ストレージ、ストリーム、またはプロパティ バッグにフィードします。 それ以外の場合、ホストは、`IPersist*::InitNew` または [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) メソッドを使用して、null スクリプトを作成します。 スクリプトをテキストとして保持するホストは、[IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) を使用して、`IActiveScriptParse::InitNew` を呼び出した後で、スクリプトのテキストをスクリプト エンジンにフィードすることができます。

4. 名前付きの項目の追加 スクリプト エンジンの名前空間にインポートされる各最上位レベルの名前付き項目 (ページやフォームなど) について、ホストは、[IActiveScript::AddNamedItem](../winscript/reference/iactivescript-addnameditem.md) メソッドを呼び出して、エンジンの名前空間内にエントリを作成します。 最上位レベルの名前付き項目が、既に手順 3. で読み込まれたスクリプトの永続的な状態の一部になっている場合は、この手順は必要ではありません。 ホストが `IActiveScript::AddNamedItem` を使用してサブレベルの名前付き項目 (HTML ページ上のコントロールなど) を追加するのではなく、エンジンが、ホストの `ITypeInfo` および `IDispatch` インターフェイスを使用して最上位レベルの項目からサブレベルの項目を間接的に取得します。

5. スクリプトを実行します。 ホストは、[IActiveScript::SetScriptState](../winscript/reference/iactivescript-setscriptstate.md) メソッドで SCRIPTSTATE_CONNECTED フラグを設定することによってエンジンでスクリプトの実行を開始させます。 この呼び出しが、静的バインド、イベントのフック (以下参照)、コードの実行などのスクリプト エンジンの構築作業を行う場合があります。これはスクリプト化された `main()` 関数の方法と似ています。

6. 項目情報を取得します。 スクリプトエンジンは、シンボルと最上位レベルの項目を関連付ける必要があるたびに、[IActiveScriptSite::GetItemInfo](../winscript/reference/iactivescriptsite-getiteminfo.md) メソッドを呼び出し、このメソッドは指定された項目に関する情報を返します。

7. イベントをフックします。 実際のスクリプトを開始する前に、スクリプト エンジンは、`IConnectionPoint`インターフェイスを介してすべての関連するオブジェクトのイベントに接続します。

8. プロパティとメソッドを呼び出します。 スクリプトが実行されるときには、スクリプト エンジンが `IDispatch::Invoke` またはその他の標準の OLE バインディング メカニズムを使用して、名前付きのオブジェクトのメソッドとプロパティへの接続を実現します。

## <a name="windows-script-terms"></a>Windows スクリプトの用語

この一覧には、このドキュメントで使用されるスクリプトに関連する用語の定義が含まれています。

|用語|定義|
|----------|----------------|
|コード オブジェクト|Visual Basic でのフォームの背後にあるモジュール、名前付きの項目に関連付けられている C++ クラスなどの、名前付きの項目に関連付けられているスクリプト エンジンによって作成されたインスタンス。 これは、ホストまたはその他のスクリプト以外のエンティティがコード オブジェクトを操作できるように、OLE オートメーションをサポートする OLE コンポーネント オブジェクト モデル (COM) オブジェクトであることが望ましいと言えます。|
|名前付き項目|ホストがスクリプトに関連すると考える OLE COM オブジェクト (できれば OLE オートメーションをサポートするオブジェクト)。 たとえば、Web ブラウザーの HTML ページとブラウザー、Microsoft Word 文書の文書とダイアログ ボックスなどがあります。|
|スクリプト|スクリプト エンジンが実行するプログラムを構成するデータ。 スクリプトは、任意の連続する実行可能なデータであり、テキストの集まり、`pcode` のブロック、コンピューター固有の実行可能バイト コードなどが含まれます。 ホストは、`IPersist*`インターフェイスまたは [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) インターフェイスのいずれかで、スクリプト エンジンにスクリプトを読み込みます。|
|スクリプト エンジン|スクリプトを処理する OLE オブジェクト。 スクリプト エンジンは、[IActiveScript](../winscript/reference/iactivescript.md) を実装し、必要に応じて [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) インターフェイスを実装します。|
|スクリプティング ホスト|Windows スクリプト エンジンを所有しているアプリケーションまたはプログラム。 ホストは、[IActiveScriptSite](../winscript/reference/iactivescriptsite.md) を実装し、必要に応じて [IActiveScriptSiteWindow](../winscript/reference/iactivescriptsitewindow.md) インターフェイスを実装します。|
|スクリプトレット|[IActiveScriptParse](../winscript/reference/iactivescriptparse.md) インターフェイスを介してオブジェクトにアタッチされるスクリプトの一部。 スクリプトレットを集めたものがスクリプトです。|
|スクリプト言語|スクリプトの記述言語 (たとえば VBScript) とその言語のセマンティクスです。|