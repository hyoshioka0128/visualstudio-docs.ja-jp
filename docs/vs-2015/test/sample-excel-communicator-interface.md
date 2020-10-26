---
title: Excel Communicator インターフェイスのサンプル | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 1dbf1090-762c-4824-82dd-2d7c2c6f00b6
caps.latest.revision: 13
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e3a9bd037c8886743910af649bf831b11337598
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660486"
---
# <a name="sample-excel-communicator-interface"></a>Excel Communicator インターフェイスのサンプル
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`IExcelUICommunication` インターフェイスのサンプルは `ExcelAddIn` プロジェクト内の `ExcelUICommunicator` オブジェクトで使用されています。

## <a name="iexceluicommunication-interface"></a>IExcelUICommunication インターフェイス
 このインターフェイスは、コード化された UI テスト プロセスで実行される `CodedUIExtension` と [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] プロセスで実行される `ExcelCodedUIAddIn` の間の通信ポイントを定義します。

 `ExcelCodedUIAddinHelper` アセンブリには、このインターフェイスから派生し、Excel オブジェクト モデルを使用してメソッドを処理する `ExcelUICommunicator` クラスがあります。

 一部のメソッドは、要求した情報を Excel から取得した後に `CellInformation` オブジェクトなどの情報オブジェクトの 1 つを作成し、返します。

 また、提供される情報オブジェクトを使用して、Excel 内にある対応するコントロールを見つけ、そのコントロールで処理を実行するメソッドもあります。 たとえば、`ScrollIntoView` メソッドは所定のセルが表示されるまでワークシートをスクロールします。

## <a name="codeduiextensibilitysample-and-excelcodeduiaddinhelper-communication"></a>CodedUIExtensibilitySample と ExcelCodedUIAddinHelper の通信
 `ExcelCodedUIAddinHelper` アセンブリは Excel プロセスで実行されます。このアセンブリには、`IExcelUITestCommunication` インターフェイスを実装して、必要な情報を Excel UI から直接取得または設定する `UICommunicator` クラスがあります。

 `CodedUIExtensibilitySample` アセンブリは Visual Studio のコード化された UI テスト プロセスで実行されます。 このアセンブリには `Communicator` クラスがあります。このクラスは .NET リモート処理チャネルを開き、`Instance` プロパティを提供します。このプロパティは `IExcelUICommunication` インターフェイスを使用して、`ExcelCodedUIAddinHelper` アセンブリ内の `UICommunicator` オブジェクトを使用し、要求および情報オブジェクト (`CellInformation` オブジェクトなど) を 2 つのアセンブリ間で相互にやり取りします。

## <a name="see-also"></a>参照
 コード化された[ui テストと操作の記録を拡張し](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)て、コード化された[ui テスト用の Microsoft Excel サンプル Excel アドイン](../test/sample-excel-add-in-for-coded-ui-testing.md)をサポートする[excel 用のコード化](../test/sample-coded-ui-test-extension-for-excel.md)された ui テスト拡張機能のサンプル
