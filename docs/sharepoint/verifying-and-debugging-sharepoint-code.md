---
title: SharePoint コードの検証とデバッグ |Microsoft Docs
description: SharePoint コードを確認し、デバッグします。 IntelliTrace を使用して、ソリューション内の過去のイベントと現在の状態を確認します。 単体テストを使用して、メソッドが正しく動作することを確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- unit testing [SharePoint development in Visual Studio]
- IntelliTrace [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, IntelliTrace
- SharePoint development in Visual Studio, unit testing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ce891e40552c0f8927bfd4ce006b750b6e5f8a54
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914505"
---
# <a name="verify-and-debug-sharepoint-code"></a>SharePoint コードの検証とデバッグ
IntelliTrace と単体テストを使用すると、SharePoint ソリューションを簡単にデバッグして、ソリューション内の各メソッドが正常に動作することを確認できます。 Visual Studio の SharePoint プロジェクトに対してこれらの機能を使用するには、他の種類のプロジェクトの場合と同じ手順に従います。

## <a name="intellitrace"></a>収集
IntelliTrace を使用して、SharePoint ソリューションの現在の状態だけでなく、過去に発生したイベントおよび発生時のコンテキストも調べることができます。 SharePoint ソリューション内の目的のイベントが記録されたさまざまな時点に移動し、各時点の状態と変数値を確認することができます。 この動的ナビゲーションを使用すると、多数のブレークポイントを設定しなくても、すばやく簡単に SharePoint ソリューションをデバッグできます。 また、デバッグセッションを IntelliTrace ログ (*itrace*) ファイルに保存し、後で Visual Studio Enterprise で開いて、クラッシュ後のデバッグを実行することもできます。 *Itrace* ファイルには、特定の SharePoint エラーが発生したタイミングと場所に関する詳細情報が含まれているので、エラーの原因を簡単に把握できます。 *Itrace* ファイル内の情報は、SharePoint の統合ログシステム (ULS) によって作成される完全なエラーログのサブセットです。 この情報には、ユーザー プロファイルがいつ開かれたか、閉じられたか、SharePoint プロジェクト内のプロパティがいつ読み込まれたか、読み取られたか、変更されたかなど、SharePoint 固有のイベントが含まれています。 IntelliTrace でどのイベントを記録するか、構成することもできます。 詳細については、「[保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)」を参照してください。

SharePoint でエラーが発生した場合、エラー ダイアログ ボックスには、そのエラーの "相関 ID" 識別子が表示されます。 また、 *itrace* ファイルに記載されているイベントから関連付け id を取得することもできます。 特定の相関 ID で発生したすべてのイベントの一覧を表示するには、[IntelliTrace の概要] ページの [ **分析** ] セクションに id を入力します。 このセクションでは、発生したイベントの名前のみを表示するか、イベントの名前と共に、関数名、終了/エントリ ポイント、パラメーター、戻り値などの呼び出し情報を表示するかを選択できます。

F5 キーを **押す** と、IntelliTrace で Visual Studio イベントを取得できます。 ただし、SharePoint 固有のイベントを取得するには、Microsoft Monitoring Agent を使用して、SharePoint ソリューションの IntelliTrace データを収集する必要があります。 このツールは、IntelliTrace データを収集し、Visual Studio の外部に配置されたアプリケーション用の *itrace* ファイルを作成します。 詳細については、「 [intellitrace の機能](../debugger/intellitrace-features.md) 」および「 [intellitrace スタンドアロンコレクターの使用](../debugger/using-the-intellitrace-stand-alone-collector.md)」を参照してください。

## <a name="unit-test"></a>単体テスト
単体テストを使用すると、コード内のエラーを検出しやすくなります。単体テストでは、テスト メソッドの内部にテスト コードを記述して、それを実行します。 これらのメソッドには、SharePoint オブジェクト モデルに基づいてプロジェクトのロジックと機能を検証するために使用できる、空の変数と Assert ステートメントが含まれます。 詳しくは、「[コードの単体テストUnit Test Your Code](../test/unit-test-your-code.md)」をご覧ください。

### <a name="support-for-microsoft-fakes-framework"></a>Microsoft のフェイクフレームワークのサポート
SharePoint プロジェクトは Microsoft Fakes をサポートしています。これは、.NET Framework に基づいたアプリケーションでデリゲート ベースのテスト スタブと shim を作成できる分離フレームワークです。 Fakes フレームワークを使用することにより、単体テスト内でダミー実装を作成、管理、および挿入できます。 これらのスタブと shim は環境から単体テストを分離します。 スタブを作成すると、オーバーライド可能なメソッドを持つインターフェイスまたは非シール クラスを使用するコードをテストできます。 shim を作成すると、静的またはオーバーライド可能なメソッドを持つシール クラスへの、ハードコーディングされた呼び出しを代替 shim 実装にリダイレクトすることができます。 また、スタブ型および shim 型のデリゲートを使用して、個々のスタブ メンバーの動作を動的にカスタマイズすることもできます。 詳細については、「 [Microsoft フェイクを使用したテストのコードの分離](../test/isolating-code-under-test-with-microsoft-fakes.md)」を参照してください。

## <a name="related-articles"></a>関連記事

|Title|説明|
|-----------|-----------------|
|[IntelliTrace](../debugger/intellitrace.md)|IntelliTrace を使用して Visual Studio ソリューションをより簡単にデバッグする方法について説明します。|
|[チュートリアル: IntelliTrace を使用した SharePoint アプリケーションのデバッグ](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)|IntelliTrace を使用して SharePoint プロジェクトのコード エラーを検出する方法について説明します。|
|[コードの単体テスト](../test/unit-test-your-code.md)|単体テストを使用してコードの論理エラーを検出する方法について説明します。|

## <a name="see-also"></a>関連項目

- [コード品質の向上](../test/improve-code-quality.md)