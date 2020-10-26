---
title: '[XML スキーマ] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 0271fa26-2205-49bd-96e0-ae1441571808
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d637cb3c25772685d5a782eb74bf94878ded36c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669418"
---
# <a name="xml-schemas-dialog-box"></a>[XML スキーマ] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[XML スキーマ]** ダイアログ ボックスは、XML ドキュメントに関連付ける XML スキーマ定義言語 (XSD) スキーマの選択に使用します。 スキーマ キャッシュにあるスキーマを選択することも、キャッシュ内に置かれていないスキーマを指定することもできます。 選択したスキーマは、スキーマ セットの一部と見なされます。 そのスキーマ セットは、IntelliSense と XML ドキュメントの検証に使用されます。

 **[XML スキーマ]** ダイアログ ボックスにアクセスするには、ドキュメントのプロパティ ウィンドウで **[スキーマ]** ボタンをクリックするか、 **[XML]** メニューの **[スキーマ]** をクリックします。

## <a name="uielement-list"></a>UIElement の一覧
 **使用** XML スキーマを使用する方法を選択します。

- **[自動]** 。 このスキーマは現在のドキュメントで使用されていませんが、自動的な関連付けには使用できます。 XML ドキュメントでこのスキーマの `targetNamespace` に一致する名前空間を宣言すると、スキーマが自動的に関連付けられ、スキーマ セットに含まれます。

- **[このスキーマを使用する]** 。 このスキーマは、現在のドキュメントで使用されています。 ユーザーがこの列をクリックしてこのスキーマが使用されることを明示的に要求したか、一致する `targetNamespace` に基づいてスキーマが自動的に関連付けられたかのいずれかです。

- **[選択されているスキーマを使用しない]** 。 スキーマに一致する `targetNamespace` がある場合でも、このスキーマは現在のドキュメントで使用されません。 この設定は、スキーマ キャッシュまたはソリューションに同じスキーマのバージョンが複数存在する場合の競合を解決する際に役立ちます。

  **ターゲットの名前空間** XML スキーマに関連付けられているターゲットの名前空間を表示します。

  **ファイル名** XML スキーマファイル名が表示されます。

  **追加** [ **XSD スキーマを開く** ] ダイアログを開きます。このダイアログボックスでは、スキーマセットに追加する追加のスキーマを選択できます。 スキーマをスキーマ セットに追加すると、 **[使用]** 列の値が **[このスキーマを使用する]** に設定されます。

  **削除** 現在選択されているスキーマをスキーマセットから削除します。 この操作では、メモリ内のスキーマ キャッシュからスキーマが削除されますが、ファイル システムからは削除されません。

## <a name="see-also"></a>参照
 [Xml エディターコンポーネント](../xml-tools/xml-editor-components.md)方法:[スキーマキャッシュ](../xml-tools/schema-cache.md)を[使用する xml スキーマを選択](../xml-tools/how-to-select-the-xml-schemas-to-use.md)する
