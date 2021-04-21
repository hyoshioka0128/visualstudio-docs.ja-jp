---
title: Office でのスレッドのサポート
description: スレッド処理は、Microsoft Office オブジェクトモデルでサポートされています。 Office オブジェクトモデルはスレッドセーフではありませんが、Office ソリューションで複数のスレッドで作業できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- multiple threads [Office development in Visual Studio]
- threading [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], threading support
- object models [Office development in Visual Studio], threading support
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dce8bb0667cecbe073c734595d341f9c7b7ccac9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826084"
---
# <a name="threading-support-in-office"></a>Office でのスレッドのサポート
  この記事では、Microsoft Office オブジェクトモデルでのスレッド処理のサポートについて説明します。 Office オブジェクトモデルはスレッドセーフではありませんが、Office ソリューションで複数のスレッドを使用することができます。 Office アプリケーションは、コンポーネントオブジェクトモデル (COM) サーバーです。 COM を使用すると、クライアントは任意のスレッドで COM サーバーを呼び出すことができます。 スレッドセーフでない COM サーバーの場合、COM は同時呼び出しをシリアル化して、サーバー上で一度に1つの論理スレッドだけが実行されるようにするメカニズムを提供します。 このメカニズムは、シングルスレッドアパートメント (STA) モデルと呼ばれています。 呼び出しはシリアル化されるため、サーバーがビジー状態であるかバックグラウンドスレッドで他の呼び出しを処理しているときに、呼び出し元が一定期間ブロックされることがあります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="knowledge-required-when-using-multiple-threads"></a>複数のスレッドを使用する場合に必要な知識
 複数のスレッドを操作するには、マルチスレッドの次の側面について、少なくとも基本的な知識を持っている必要があります。

- Windows API

- COM マルチスレッドの概念

- コンカレンシー

- Synchronization

- マーシャリング

  マルチスレッドに関する一般的な情報については、「 [マネージスレッド処理](/dotnet/standard/threading/)」を参照してください。

  Office はメインの STA で実行されます。 このような影響を理解することで、Office で複数のスレッドを使用する方法を理解することができます。

## <a name="basic-multithreading-scenario"></a>基本的なマルチスレッドのシナリオ
 Office ソリューションのコードは、常にメイン UI スレッド上で実行されます。 バックグラウンドスレッドで別のタスクを実行すると、アプリケーションのパフォーマンスを向上させることができます。 目標は、1つのタスクの後に2つのタスクを続けて実行することです。これにより、実行がスムーズになります (複数のスレッドを使用する主な理由)。 たとえば、メインの Excel UI スレッドにイベントコードがあるとします。バックグラウンドスレッドでは、サーバーからデータを収集し、サーバーからのデータを使用して Excel UI のセルを更新するタスクを実行することができます。

## <a name="background-threads-that-call-into-the-office-object-model"></a>Office オブジェクトモデルを呼び出すバックグラウンドスレッド
 バックグラウンドスレッドが Office アプリケーションの呼び出しを行うと、その呼び出しは STA の境界を越えて自動的にマーシャリングされます。 ただし、バックグラウンドスレッドによって行われた呼び出しを Office アプリケーションが処理できることは保証されません。 いくつかの可能性があります。

1. Office アプリケーションでは、を呼び出すためにメッセージをポンプする必要があります。 これを行わずに大量の処理を実行している場合は、時間がかかることがあります。

2. 別の論理スレッドがアパートメント内に既に存在する場合、新しいスレッドはを入力できません。 これは多くの場合、論理スレッドが Office アプリケーションに入ってから、再入可能な呼び出しを呼び出し元のアパートメントに戻すときに発生します。 アプリケーションがブロックされ、その呼び出しが返されるのを待機しています。

3. Excel は、着信呼び出しをすぐに処理できない状態になっている可能性があります。 たとえば、Office アプリケーションにモーダルダイアログが表示されている場合があります。

   可能性が2および3の場合、COM には [の imessagefilter.prefiltermessage](/windows/desktop/api/objidl/nn-objidl-imessagefilter) インターフェイスが用意されています。 サーバーがそれを実装している場合、すべての呼び出しは [HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall) メソッドを介して入力されます。 可能性が2の場合、呼び出しは自動的に拒否されます。 可能性3の場合、サーバーは状況に応じて呼び出しを拒否できます。 呼び出しが拒否された場合、呼び出し元は何を行うかを決定する必要があります。 通常、呼び出し元は [の imessagefilter.prefiltermessage](/windows/desktop/api/objidl/nn-objidl-imessagefilter)を実装します。この場合、 [RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall) メソッドによって拒否が通知されます。

   ただし、Visual Studio の Office 開発ツールを使用して作成されたソリューションの場合、COM 相互運用機能は、拒否されたすべての呼び出しをに変換し <xref:System.Runtime.InteropServices.COMException> ます ("メッセージフィルターはアプリケーションがビジー状態であることを示しています")。 バックグラウンドスレッドでオブジェクトモデルを呼び出す場合は常に、この例外を処理できるように準備する必要があります。 通常は、一定の時間が経過してからダイアログが表示されます。 ただし、バックグラウンドスレッドを STA として作成し、そのスレッドに対してメッセージフィルターを登録してこのケースを処理することもできます。

## <a name="start-the-thread-correctly"></a>スレッドを正しく開始します
 新しい STA スレッドを作成するときは、スレッドを開始する前にアパートメント状態を STA に設定します。 これを実行する方法を次のコード例に示します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs" id="Snippet5":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb" id="Snippet5":::

 詳細については、「[マネージド スレッド処理のベスト プラクティス](/dotnet/standard/threading/managed-threading-best-practices)」を参照してください。

## <a name="modeless-forms"></a>モードレスフォーム
 モードレスフォームを使用すると、フォームの表示中にアプリケーションとの間で何らかの種類の操作を行うことができます。 ユーザーはフォームと対話し、フォームはを閉じずにアプリケーションと対話します。 Office オブジェクトモデルでは、マネージドモードレスフォームがサポートされています。ただし、バックグラウンドスレッドでは使用しないでください。

## <a name="see-also"></a>関連項目
- [スレッド処理 (C#)](/dotnet/csharp/programming-guide/concepts/threading/index)
- [スレッド処理 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)
- [スレッドとスレッド処理の使用](/dotnet/standard/threading/using-threads-and-threading)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
