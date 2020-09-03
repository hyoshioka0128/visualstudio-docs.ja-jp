---
author: dotpaul
ms.author: paulming
ms.date: 04/05/2019
ms.topic: include
ms.openlocfilehash: 054198eff46c0983a5610b29dee5e29e5ac67a70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89325035"
---
安全でないデシリアライザーは、信頼できないデータを逆シリアル化するときに脆弱です。 攻撃者は、悪意のある副作用を持つオブジェクトを挿入するために、シリアル化されたデータを変更し、予期しない型を含めることができます。 セキュリティで保護されていないデシリアライザーに対する攻撃は、たとえば、基になるオペレーティングシステムでコマンドを実行したり、ネットワークを介して通信したり、ファイルを削除したりすることができます。