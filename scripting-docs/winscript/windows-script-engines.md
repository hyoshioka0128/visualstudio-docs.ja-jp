---
title: Windows スクリプト エンジン | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows script engines
ms.assetid: e576853d-7252-4eb9-81eb-9d5bb7626ab4
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 94fca3befc13e32e6e2859c7b1ef6330af7b812f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72568946"
---
# <a name="windows-script-engines"></a>Windows スクリプト エンジン
Microsoft Windows スクリプト エンジンを実装するには、次のインターフェイスをサポートする OLE COM オブジェクトを作成します。  
  
|||  
|-|-|  
|Interface|説明|  
|[IActiveScript](../winscript/reference/iactivescript.md)|基本的なスクリプト機能を提供します。 このインターフェイスの実装は必須です。|  
|[IActiveScriptParse](../winscript/reference/iactivescriptparse.md)|スクリプト テキストの追加や式の評価などの機能を提供します。 このインターフェイスの実装は省略可能です。ただし、実装されていない場合、スクリプト エンジンはスクリプトを読み込むために IPersist* インターフェイスのいずれかを実装する必要があります。|  
|IPersist*|永続性のサポートを提供します。 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) が実装されていない場合は、次のインターフェイスの 1 つ以上の実装が必要になります。<br /><br /> IPersistStorage: OBJECT タグの DATA={url} 属性のサポートを提供します。<br /><br /> IPersistStreamInit: OBJECT タグの DATA="string-encoded byte stream" 属性および `IPersistStorage` と同じサポートを提供します。<br /><br /> IPersistPropertyBag: OBJECT タグの PARAM 属性のサポートを提供します。|  
  
> [!NOTE]
> `IPersist*` でスクリプト状態を保存または復元する際にスクリプト エンジンが呼び出されなくなる可能性があります。 代わりに、[IActiveScriptParse](../winscript/reference/iactivescriptparse.md) が使用されます。その場合、空のスクリプトを作成するために [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) が呼び出され、[IActiveScriptParse::AddScriptlet](../winscript/reference/iactivescriptparse-addscriptlet.md) でスクリプトレットがイベントに追加されて接続され、[IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) で一般的なコードが追加されます。 それでも、スクリプト エンジンは 1 つ以上の `IPersist*` インターフェイス (可能であれば `IPersistStreamInit`) を完全に実装する必要があります。他のホスト アプリケーションがそれらを利用しようとする場合があるためです。  
  
 次のセクションでは、Windows スクリプト エンジンの実装について、さらに詳しく説明します。  
  
 詳細については、「[Windows スクリプト インターフェイスのリファレンス](../winscript/reference/windows-script-interfaces-reference.md)」を参照してください。  
  
## <a name="registry-standard"></a>レジストリ標準  
 Windows スクリプト エンジンは、カテゴリ識別子を使用して自身を識別できます。 現在、Windows スクリプトでは 2 つのカテゴリ識別子を定義します。  
  
|||  
|-|-|  
|カテゴリ|説明|  
|CATID_ActiveScript|クラス識別子 (CLSID) は、少なくとも [IActiveScript](../winscript/reference/iactivescript.md) インターフェイスと永続化メカニズム (`IPersistStorage`、`IPersistStreamInit`、または IPersistPropertyBag インターフェイス) をサポートする Windows スクリプト エンジンであることを示します。|  
|CATID_ActiveScriptParse|CLSID は、少なくとも [IActiveScript](../winscript/reference/iactivescript.md) と [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) インターフェイスをサポートする Windows スクリプト エンジンであることを示します。|  
  
 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) が該当する永続化メカニズムでない場合、`IPersist*::InitNew` と機能的に同等の [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) メソッドがサポートされます。  
  
## <a name="script-engine-states"></a>スクリプト エンジンの状態  
 任意の時点で、Windows スクリプト エンジンは次のいずれかの状態になります。  
  
|||  
|-|-|  
|状態|説明|  
|未初期化|スクリプトが IPersist* インターフェイスを使用して初期化されていないか読み込まれていない、または [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) インターフェイスが設定されていません。 通常、スクリプトが読み込まれるまで、この状態からスクリプト エンジンを使用することはできません。|  
|初期化済み|スクリプトが `IPersist*` インターフェイスで初期化されており、[IActiveScriptSite](../winscript/reference/iactivescriptsite.md) インターフェイスが設定されていますが、ホスト オブジェクトとシンク イベントに接続されません。 この状態は単に、`IPersist*::Load`、`IPersist*::InitNew`、または [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) メソッドが完了しており、[IActiveScript::SetScriptSite](../winscript/reference/iactivescript-setscriptsite.md) メソッドが呼び出されたことを意味することに注意してください。 エンジンはこのモードでコードを実行することはできません。 エンジンは、[IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) メソッドでホストが渡すコードをキューに入れ、開始状態に遷移した後でコードを実行します。<br /><br /> セマンティクスにおいて言語が大きく異なる場合があるため、スクリプト エンジンがこの状態遷移をサポートする必要はありません。 ただし、[IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) メソッドをサポートするエンジンはこの状態遷移をサポートする必要があります。 ホストはこの遷移に備え、適切なアクションを実行する必要があります。つまり、現在のスクリプト エンジンをリリースし、新しいスクリプト エンジンを作成し、`IPersist*::Load`、`IPersist*::InitNew`、または [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) を (場合によっては [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) も) 呼び出す必要があります。 この遷移の使用は上記の手順の最適化と見なされます。 スクリプト エンジンが名前付きアイテムの名前と名前付きアイテムを記述する型情報について取得する情報は有効のままであることに注意してください。<br /><br /> 言語は大きく異なるため、この遷移の正確なセマンティクスを定義するのは困難です。 少なくとも、スクリプト エンジンはすべてのイベントから切断し、[IActiveScriptSite::GetItemInfo](../winscript/reference/iactivescriptsite-getiteminfo.md) メソッドを呼び出して取得される SCRIPTINFO_IUNKNOWN ポインターをすべてリリースする必要があります。 スクリプトの再実行後に、エンジンはこれらのポインターを再取得する必要があります。 また、スクリプト エンジンはスクリプトをリセットし、言語に適した初期状態に戻す必要もあります。 たとえば、VBScript ではすべての変数をリセットし、SCRIPTTEXT_ISPERSISTENT フラグを設定して [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) を呼び出して動的に追加されたコードを保持します。 その他の言語では現在の値 (コード/データは分離されないため、Lisp など) を保持するか、既知の状態にリセットする必要がある場合があります (これには変数が静的に初期化された言語を含む)。<br /><br /> 開始状態への遷移には `IPersist*::Save` を呼び出してスクリプト エンジンを保存してから `IPersist*::Load` を呼び出して新しいスクリプト エンジンを読み込む場合と同じセマンティクスが必要であることに注意してください。これらのアクションには [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) と同じセマンティックが必要です。 `IActiveScript::Clone` や `IPersist*` をまだサポートしていないスクリプト エンジンでは、`IActiveScript::Clone` または `IPersist*` のサポートが後で追加された場合に開始状態への遷移で上記の条件に違反しないように、遷移の動作方法を慎重に検討する必要があります。<br /><br /> この開始状態への遷移時に、スクリプト エンジンは適切なデストラクターなどがスクリプトで実行された後にイベント シンクから切断されます。 これらのデストラクターが実行されないようにするために、ホストは開始状態に移行する前に最初にスクリプトを切断状態に移行できます。<br /><br /> 現在のイベントなどの実行が完了するまで待機せずに実行中のスクリプト スレッドをキャンセルするには、[IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) を使用します。|  
|開始|初期化済み状態から開始状態に遷移すると、初期化済み状態でキューに入れられたコードをエンジンが実行します。 エンジンは開始状態の間、コードを実行できますが、[IActiveScript::AddNamedItem](../winscript/reference/iactivescript-addnameditem.md) メソッドで追加されたイベントには接続されません。 エンジンは [IActiveScript::GetScriptDispatch](../winscript/reference/iactivescript-getscriptdispatch.md) メソッドから取得した IDispatch インターフェイスを呼び出すか、[IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) を呼び出すことでコードを実行できます。 さらにバックグラウンド初期化 (プログレッシブ読み込み) がまだ進行中である可能性があります。また、SCRIPTSTATE_CONNECTED フラグを設定して [IActiveScript::SetScriptState](../winscript/reference/iactivescript-setscriptstate.md) メソッドを呼び出すと、初期化が完了するまでスクリプトがブロックされる可能性があります。|  
|接続済み|スクリプトが読み込まれ、ホスト オブジェクトからのシンク イベントのために接続されます。 これが初期化済み状態からの遷移である場合、スクリプト エンジンは開始状態を経て遷移し、接続済み状態に入ってイベントに接続する前に必要なアクションを実行する必要があります。|  
|切断|スクリプトが読み込まれ、実行時の状態ですが、ホスト オブジェクトからのシンク イベントからは一時的に切断されています。 これは (受信したイベントを無視して) 論理的または (適切な接続ポイントで IConnectionPoint::Unadvise を呼び出して) 物理的に行われる場合があります。 これが初期化済み状態からの遷移の場合、スクリプト エンジンは開始状態を経て遷移し、切断状態に入る前に必要なアクションを実行する必要があります。 進行中のイベント シンクは、状態が変わる前に完了します ([IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) を使用して、実行中のスクリプト スレッドをキャンセルする)。 この状態は初期化済み状態とは区別されます。初期化状態では、この状態への遷移によってスクリプトがリセットされなくなり、スクリプトの実行時の状態はリセットされず、スクリプトの初期化手順は実行されません。|  
|終了|スクリプトは終了しています。 スクリプト エンジンは動作しなくなり、ほとんどのメソッドに対してエラーを返します。|  
  
 次の図は、さまざまなスクリプト エンジンの状態の関係と、ある状態から別の状態への遷移を引き起こすメソッドを示しています。  
  
 次の図は、さまざまな状態遷移中にスクリプト エンジンが実行するアクションを示しています。  
  
## <a name="scripting-engine-threading"></a>スクリプト エンジンのスレッド  
 Windows スクリプト エンジンは多くの環境で使用できるため、その実行モデルを可能な限り柔軟な状態に保つことが重要です。 たとえば、サーバー ベースのホストは、効率的な方法で Windows スクリプトを使用しているときにマルチスレッド デザインを保持する必要がある場合があります。 同時に、一般的なアプリケーションなど、スレッドを使用しないホストにスレッド管理の負荷を与えないようにする必要があります。 Windows スクリプトは、フリー スレッド スクリプト エンジンがホストにコールバックし、この負荷からホストを解放できる方法を制限することで、このバランスを保ちます。  
  
 サーバーで使用されるスクリプト エンジンは、通常、フリー スレッド COM オブジェクトとして実装されます。 これは、[IActiveScript](../winscript/reference/iactivescript.md) インターフェイスとその関連するインターフェイスに対するメソッドを、マーシャリングなしで、プロセスのスレッドから呼び出せることを意味します (残念ながら、これは、スクリプトエンジンをインプロセスサーバーとして実装する必要があることも意味します。これは、現在 OLE ではフリースレッドオブジェクトのプロセス間マーシャリングがサポートされていないためです)。同期は、スクリプトエンジンの役割です。 内部的に再入不可能なスクリプト エンジンの場合や、マルチスレッド化されていない言語モデルの場合、ミューテックスを使用する同期で、スクリプト エンジンへのアクセスを可能な限り簡単にシリアル化できます。 もちろん、[IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) メソッドなどの特定のメソッドはこの方法でシリアル化しないため、スタック スクリプトを別のスレッドから終了することができます。  
  
 [IActiveScript](../winscript/reference/iactivescript.md) が通常、フリー スレッドであるということは、一般に [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) インターフェイスとホストのオブジェクト モデルもフリー スレッドである必要があることを意味します。 これにより、ホストの実装が非常に難しくなります。特に、ホストがそのオブジェクト モデルにシンブル スレッドまたはアパートメント モデルの ActiveX コントロールを持つシングル スレッドの Windows ベース アプリケーションである一般的なケースで難しくなります。 そのため、スクリプト エンジンでの [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) の使用には次の制約があります。  
  
 スクリプト サイトは常にホスト スレッドのコンテキストで呼び出されます。 つまり、スクリプト エンジンは自身で作成したスレッドのコンテキストでスクリプト サイトを呼び出すことはありません。[IActiveScript](../winscript/reference/iactivescript.md) とその派生物、公開されたスクリプト エンジンのディスパッチ オブジェクト、Windows メッセージを介してホストから、あるいはホストのオブジェクト モデル内のイベント ソースから呼び出されたスクリプト エンジン メソッド内からのみ呼び出します。  
  
 スクリプト サイトが単純なスレッド状態制御メソッド ([IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) メソッドなど) のコンテキスト内や [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) メソッドから呼び出されることはありません。  
  
## <a name="see-also"></a>関連項目  
 [Windows スクリプト インターフェイス](../winscript/windows-script-interfaces.md)
