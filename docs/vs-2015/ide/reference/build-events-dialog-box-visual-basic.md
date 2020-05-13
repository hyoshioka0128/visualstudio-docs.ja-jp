---
title: '[ビルド イベント] ダイアログ ボックス (Visual Basic) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- build events, specifying
- pre-build events
- Build Events dialog box
- post-build events
ms.assetid: 3a81a7c7-39f9-47a8-ba5a-b351227f380e
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9fa3b4365f49d172e077ca132b26a49580228c25
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660957"
---
# <a name="build-events-dialog-box-visual-basic"></a>[ビルド イベント] ダイアログ ボックス (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[ビルド イベント]** ダイアログ ボックスを使用して、ビルド構成の手順を指定します。 また、ビルド前またはビルド後の任意のイベントを実行する条件を指定することもできます。 詳細については、「[方法 : ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)」を参照してください。

 **ビルド前に実行するコマンド ライン** ビルド開始前に実行する任意のコマンドを指定します。 長いコマンドを入力するには、 **[ビルド前の編集]** をクリックして [[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)を表示します。

> [!NOTE]
> プロジェクトが最新の状態で、ビルドがトリガーされない場合、ビルド前イベントは実行されません。

 **ビルド後に実行するコマンド ライン** ビルド終了後に実行する任意のコマンドを指定します。 長いコマンドを入力するには、 **[ビルド後の編集]** をクリックして **[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス**を表示します。

> [!NOTE]
> .bat ファイルを実行するすべてのビルド後コマンドの前に `call` ステートメントを追加します。 たとえば、`call C:\MyFile.bat` または `call C:\MyFile.bat call C:\MyFile2.bat` のようにします。

 **ビルド後イベントの実行** 次の表に示すように、実行するビルド後イベントの条件を指定します。

|オプション|結果|
|------------|------------|
|**常時**|ビルド後イベントは、ビルドが成功したかどうかに関係なく実行されます。|
|**ビルドが成功したとき**|ビルド後イベントは、ビルドが成功した場合に実行されます。 このため、ビルドが成功した場合は、最新のプロジェクトについてもイベントが実行されます。 これは、既定の設定です。|
|**ビルドがプロジェクト出力を更新したとき**|ビルド後イベントは、コンパイラの出力ファイル (.exe または .dll) が以前のコンパイラの出力ファイルと異なる場合にだけ実行されます。 ビルド後イベントは、プロジェクトが最新の場合は実行されません。|

## <a name="see-also"></a>参照
 [[コンパイル] ページ (プロジェクトデザイナー) (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) [方法: ビルドイベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)ビルド[前のイベント/ビルド後に実行するコマンドラインダイアログボックス](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
