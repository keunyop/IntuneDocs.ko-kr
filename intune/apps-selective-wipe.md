---
title: "앱에서 회사 데이터만 초기화하는 방법"
titleSuffix: Intune Azure preview
description: "Intune Azure 미리 보기: Microsoft Intune을 사용하여 앱을 선택적으로 초기화하는 방법을 알아봅니다."
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 02/07/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 42605e6e-5b84-44ff-b86e-346ea123b53e
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: affe7323b8572aa17122011b293cb6a3a2fd7747
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017

---

# <a name="how-to-wipe-only-corporate-data-from-intune-managed-apps"></a>Intune 관리 앱에서 회사 데이터만 초기화하는 방법

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

장치를 분실하거나 도난당한 경우, 또는 직원이 퇴사하는 경우, 장치에서 업무용 앱 데이터가 확실히 제거되도록 해야 합니다. 하지만 장치에서 개인 데이터(특히, 직원 소유의 장치인 경우)를 제거하지 말아야 하는 경우가 있습니다.

회사 앱 데이터를 선택적으로 제거하려면 이 항목의 단계를 사용하여 초기화 요청을 만듭니다. 요청이 완료되고 나면, 다음 번에 장치에서 앱을 실행할 때 회사 데이터가 앱에서 제거됩니다.

>[!IMPORTANT]
> 앱에서 기본 주소록에 직접 동기화된 연락처가 제거됩니다. 기본 주소록에서 다른 외부 소스에 동기화된 연락처는 초기화할 수 없습니다. 현재 Microsoft Outlook 앱에만 적용됩니다.

## <a name="create-a-wipe-request"></a>초기화 요청 만들기

1.  [Azure 포털](https://portal.azure.com)에 로그인합니다.

2.  **추가 서비스**를 선택하고 필터 텍스트 상자에 **Intune**을 입력한 후 **Intune**을 선택합니다. Intune 미리 보기 블레이드가 열리면 **앱 관리** 블레이드를 선택합니다.

    ![새 초기화 요청 블레이드의 스크린샷](./media/intune-azure-preview-blade.png)

3.  **모바일 앱 블레이드**에서 **새 초기화 요청**을 선택합니다. **새 초기화 요청** 블레이드가 열립니다.

4.  **새 초기화 요청**을 선택합니다. **새 초기화 요청** 블레이드가 열립니다.

    ![새 초기화 요청 블레이드의 스크린샷](./media/AzurePortal_MAM_NewWipeRequest.png)

5.  **사용자**를 선택하여 **사용자** 블레이드를 열고 초기화하려는 앱 데이터의 사용자를 선택합니다.

6.  **장치**를 선택합니다. 선택한 사용자와 연결된 모든 장치를 나열하고, 두 개의 열, 장치 이름(사용자가 정의한 식별 이름), 장치 유형 및 장치 플랫폼을 제공하는 **장치** 블레이드가 열립니다. 초기화하려는 장치를 선택합니다.

7.  이제 **새 초기화 요청** 블레이드로 전환됩니다. 초기화 요청을 수행하려면 **확인**을 클릭합니다. 

서비스에서 장치의 각 보호된 앱 및 초기화 요청과 연결된 사용자에 대해 별도의 초기화 요청을 만들고 추적합니다.

## <a name="monitor-your-wipe-requests"></a>초기화 요청 모니터링

초기화 요청의 전반적인 상태를 표시하고, 보류 중인 요청 및 오류의 수가 포함된 요약된 보고서를 생성할 수 있습니다. 세부 정보를 확인하려면 다음 단계를 따릅니다.

1.  **모바일 앱 - 앱 선택 초기화** 블레이드에서 사용자별로 그룹화된 요청 목록을 확인할 수 있습니다. 시스템에서는 장치에서 실행 중인 각각의 보호된 앱에 대해 초기화 요청을 생성하므로 한 사용자에 대해 여러 요청이 표시될 수 있습니다. 상태를 통해 초기화 요청이 **보류 중**인지, **실패**했는지 아니면 **성공**했는지 확인할 수 있습니다.

    ![새 초기화 요청 블레이드의 스크린샷](./media/wipe-request-status-1.png)

또한 장치 이름과 장치 유형을 볼 수 있습니다. 이는 보고서를 읽을 때 유용합니다.

>[!IMPORTANT]
> 초기화하려면 사용자가 앱을 열어야 하며 초기화에는 요청 후 최대 30분 걸릴 수 있습니다.

## <a name="delete-a-wipe-request"></a>초기화 요청 삭제

보류 중 상태의 초기화는 수동으로 삭제할 때까지 표시됩니다.  초기화 요청을 수동으로 삭제하려면

1.  **초기와 요청** 블레이드에서 **초기화 요청** 타일을 선택하여 **초기화 요청** 블레이드를 엽니다.

2.  삭제하려는 초기화 요청을 마우스 오른쪽 단추로 클릭하고 **초기화 요청 삭제**를 선택합니다.

    ![새 초기화 요청 블레이드의 스크린샷](./media/delete-wipe-request.png)

3.  삭제를 확인하라는 메시지가 표시되면 **예** 또는 **아니요**를 선택하고 **확인**을 클릭합니다.

### <a name="see-also"></a>참고 항목
[앱 보호 정책이란?](app-protection-policy.md)

[앱 관리란?](app-management.md)