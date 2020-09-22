---
title: '方法: エディターのコンテキストを指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - provide context
ms.assetid: 12df4d06-df6b-4eaf-a7bf-c83655a0c683
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 11a98599a9812cd00650d113170ff55c01ac44db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841680"
---
# <a name="how-to-provide-context-for-editors"></a>方法: エディター用のコンテキストを提供する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターの場合、コンテキストは、エディターにフォーカスがあるとき、またはフォーカスがツールウィンドウに移動する直前にフォーカスがあったときにのみアクティブになります。 エディターのコンテキストを指定するには、次の手順を実行します。  
  
1. コンテキストバッグを作成します。  
  
2. コンテキストバッグを選択要素識別子 (SEID) に発行します。  
  
3. バッグ内のコンテキストを維持します。  
  
   これらのタスクについては、次の手順で説明します。 コンテキストの提供の詳細については、このトピックで後述する「 **堅牢なプログラミング** 」を参照してください。  
  
### <a name="to-create-a-context-bag-for-an-editor-or-a-designer"></a>エディターまたはデザイナーのコンテキストバッグを作成するには  
  
1. `QueryService` <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> サービスのインターフェイスでを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> ます。  
  
     インターフェイスへのポインター <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> が返されます。  
  
2. メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext.CreateEmptyContext%2A> 新しいコンテキストまたは subcontext バッグを作成します。  
  
     インターフェイスへのポインター <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext> が返されます。  
  
3. メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A> コンテキストまたは subcontext バッグに属性、検索キーワード、または F1 キーワードを追加します。  
  
4. Subcontext バッグを作成する場合は、メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddSubcontext%2A> subcontext バッグを親コンテキストバッグにリンクします。  
  
5. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>を呼び出して、[**ダイナミックヘルプ**] ウィンドウが更新されようとしているときに通知を受信します。  
  
     [ **ダイナミックヘルプ** ] ウィンドウを更新する準備ができたらエディターを呼び出すと、更新が行われるまでコンテキストの変更を遅らせることができます。 これにより、システムのアイドル時間が使用可能になるまで、実行時間の長いアルゴリズムを遅延させることができるため、パフォーマンスが向上します。  
  
### <a name="to-publish-the-context-bag-to-the-seid"></a>コンテキストバッグを SEID に発行するには  
  
1. サービスでを呼び出して、 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> インターフェイスへのポインターを返し <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> ます。  
  
2. を呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A> 、SEID_UserContext の要素識別子 (パラメーター) 値を指定して、 `elementid` グローバルレベルにコンテキストを渡すことを示します。  
  
3. エディターまたはデザイナーがアクティブになると、そのオブジェクト内の値 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> がグローバル選択に反映されます。 このプロセスは、セッションごとに1回だけ完了し、を呼び出したときに作成されたグローバルコンテキストへのポインターを格納するだけで済み <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A> ます。  
  
### <a name="to-maintain-the-context-bag"></a>コンテキストバッグを維持するには  
  
1. を実装して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext> 、 **動的ヘルプ** ウィンドウが更新前にエディターまたはデザイナーを呼び出すようにします。  
  
     コンテキストバッグが作成され、実装された後に呼び出されたコンテキストバッグごとに、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate> を呼び出してコンテキストバッグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> 更新されることをコンテキストプロバイダーに通知します。 この呼び出しを使用して、コンテキストバッグ内の属性とキーワード、および subcontext バッグを変更してから、 **ダイナミックヘルプ** ウィンドウを更新することができます。  
  
2. コンテキストバッグでを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A> エディターまたはデザイナーに新しいコンテキストがあることを示します。  
  
     [ **ダイナミックヘルプ** ] ウィンドウが更新中であることを <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> 示すためにを呼び出すと、エディターまたはデザイナーは、その時点で親コンテキストバッグと subcontext バッグの両方に対してコンテキストを適切に更新できます。  
  
    > [!NOTE]
    > コンテキスト `SetDirty` `true` がコンテキストバッグから追加または削除されるたびに、フラグは自動的にに設定されます。 [ **ダイナミックヘルプ** ] ウィンドウは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> `SetDirty` フラグがに設定されている場合にのみ、コンテキストバッグでを呼び出し `true` ます。 更新後ににリセットされ `false` ます。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>を呼び出して、アクティブなコンテキストコレクションにコンテキストを追加するか、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A> コンテキストを削除します。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 独自のエディターを作成する場合は、エディターのコンテキストを提供するために、このトピックの3つの手順をすべて完了する必要があります。  
  
> [!NOTE]
> エディターまたはデザイナーウィンドウを適切にアクティブにし、コマンドルーティングが適切に更新されるようにするには、コンポーネントでを呼び出してフォーカスを設定する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> ます。  
  
 SEID は、選択内容に基づいて変更されるプロパティのコレクションです。 SEID 情報は、グローバル選択で利用できます。 グローバル選択は、インターフェイスによってトリガーされるイベントに接続され、選択されて <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> いるすべてのもの (現在のエディター、現在のツールウィンドウ、現在の階層など) の一覧があります。  
  
 エディターとデザイナーでは、カーソルが単語内で移動するたびにコンテキストが変更される可能性があるため、コンテキストバッグを絶えず更新するのは効率的ではありません。 エディターまたはデザイナーウィンドウ内でカーソルを移動するたびに、更新をより効率的に行うには、を呼び出すことができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A> ます。 これにより、アイドル時間が経過するまでコンテキストの変更を保持することができ、IDE のコンテキストサービスは、 **ダイナミックヘルプ** ウィンドウが更新中のエディターまたはデザイナーに通知を送信します。 この方法は、このトピックの「コンテキストバッグを維持するには」の手順で使用します。  
  
 エディターまたはデザイナー内でアクティビティのコンテキストを指定した後、ユーザーがエディターまたはデザイナー自体のヘルプを取得できるように、特定の F1 キーワードを指定する必要があります。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>
