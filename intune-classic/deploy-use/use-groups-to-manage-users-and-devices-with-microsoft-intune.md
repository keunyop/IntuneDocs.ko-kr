---
title: "그룹을 사용하여 사용자 및 장치 관리 | Microsoft 문서"
description: "그룹 작업 영역을 사용하여 그룹을 만들고 관리합니다."
keywords: 
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.date: 12/15/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: eb9b01ce-9b9b-4c2a-bf99-3879c0bdaba5
ms.reviewer: lpatha
ms.suite: ems
ms.custom: intune-classic
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 095b8db0cb5097edca98d138edccafbe8e55b9ba
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017


---
# <a name="use-groups-to-manage-users-and-devices-in-microsoft-intune"></a>Microsoft Intune에서 그룹을 사용하여 사용자 및 장치 관리

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

이 항목에서는 Intune에서 그룹을 만드는 방법을 설명합니다. 몇 개월 후에 그룹 관리 방법이 어떻게 변경되는지에 대한 정보도 제공합니다. 

>[!IMPORTANT]
>
>Intune 포털에서 그룹 작업 영역을 열 때 Azure AD(Azure Active Directory) 포털 링크가 보이면 Intune의 그룹 관리에 대한 *새* Azure AD 보안 그룹 접근 방식([Azure Active Directory로 그룹 마이그레이션](migrating-groups-to-azure-active-directory.md)에 설명되어 있음)을 이미 사용하고 있는 것입니다. Azure AD 포털에 대한 링크를 클릭하여 그룹을 만들고 관리합니다.
>
>![Azure 그룹 관리에 대한 링크의 스크린샷](../media/groups-link-azure.png) 
>
>Azure AD 포털 링크가 보이지 않으면 지금도 그룹 관리에 대한 *기존* 접근 방식(이 항목의 [Microsoft Intune에서 그룹을 만들어 사용자와 장치 관리](#Create-groups-to-manage-users-and-devices-with-Microsoft-Intune)에 설명되어 있음)을 사용하고 있는 것입니다.

이 항목에서는 Intune 관리 콘솔에서 Intune 그룹을 만드는 방법을 설명합니다.

Microsoft Intune 관리 콘솔의 **그룹** 작업 영역에서 그룹을 만들고 관리할 수 있습니다. **그룹 개요** 페이지에는 주의가 필요한 문제를 식별하고 우선 순위를 정하는 데 유용한 상태 요약이 나와 있습니다. 상태 요약에서는 다음 영역을 다룹니다.

-   경고
-   소프트웨어 업데이트
-   Endpoint Protection
-   정책
-   소프트웨어 관리

그룹 계층 구조에 상태 요약이 표시되기 때문에 선택된 그룹의 구성원에 대한 문제를 식별하고 해결하는 데 유용합니다.

## <a name="create-groups"></a>그룹 만들기

> [!TIP]
> 그룹을 만들 때 정책 적용 방법을 생각해야 합니다. 예를 들어 장치 운영 체제와 관련된 정책과 조직의 서로 다른 역할이나 Active Directory에 이미 정의된 조직 단위와 관련된 정책이 있을 수 있습니다. iOS, Android 및 Windows용의 개별 장치 그룹과 함께 각 조직 역할에 대한 사용자 그룹이 있으면 유용합니다.
>
> 또한 모든 그룹 및 장치에 적용되는 기본 정책을 만들어 조직의 기본 규정 준수 요구 사항을 설정해도 좋을 것입니다. 그러면 가장 넓은 범주의 사용자와 장치에 대해 더 구체적인 정책을 만들 수 있습니다. 예를 들어 각 장치 운영 체제에 대한 메일 정책을 만들 수 있습니다.
>
> 나중에 쉽게 식별할 수 있도록 정책의 이름을 주의 깊게 지정합니다. 예를 들어 **전체 회사에 대한 WP 메일 정책**은 설명이 포함된 좋은 정책 이름입니다.
>
> 제한적인 정책을 만들 때마다 사용자에게 알려야 합니다. 일반적인 그룹과 정책을 만든 후에 작은 그룹을 만들면 불필요한 소통을 줄일 수 있습니다.

## <a name="to-create-a-device-group"></a>장치 그룹을 만들려면

1.  Intune 관리 콘솔에서 **그룹** &gt; **개요** &gt; **그룹 만들기**를 선택합니다.

2.  그룹의 이름 및 설명(선택 항목)을 입력하고, 장치 그룹을 부모 그룹으로 선택합니다. **다음**을 선택합니다.

3.  **회원 기준 정의** 페이지에서 그룹에 포함할 장치 유형을 선택합니다. 포함하도록 선택하는 장치 유형에 따라 그룹 구성 옵션이 더 있습니다.

    -   **컴퓨터**. 부모 그룹의 모든 구성원을 포함할지 여부, 포함하거나 제외할 조직 구성 단위, 포함하거나 제외할 도메인을 선택합니다. 인벤토리에서 컴퓨터에 대한 조직 구성 단위 및 도메인 정보를 얻을 수 있습니다.

    -   **모바일**. Intune을 통해 관리되는 모바일 장치를 포함할지, Exchange ActiveSync를 통해 관리되는 모바일 장치를 포함할지, 아니면 두 개를 모두 포함할지 선택합니다.

    -   **모든 장치**. 이 옵션은 기준에 따른 제외 없이 모든 장치를 포함합니다.

4.  **직접 회원 관리 정의** 페이지에서 **찾아보기**를 선택하여 포함하거나 제외할 각 장치를 선택합니다. 지정한 부모 그룹에 없는 장치를 선택할 경우 Intune에서 이러한 장치를 부모 그룹에 자동으로 추가합니다.

5.  **요약** 페이지에서 선택 내용을 검토하고 **마침**을 클릭합니다.

새로 만든 그룹은 부모 그룹 아래에 있는 **그룹** 작업 영역의 **그룹** 목록에 표시됩니다. 여기서 그룹을 편집하거나 삭제할 수도 있습니다.

## <a name="to-create-a-user-group"></a>사용자 그룹을 만들려면

1.  Intune 관리 콘솔에서 **그룹** &gt; **개요** &gt; **그룹 만들기**를 선택합니다.

2.  그룹의 이름 및 설명(선택 항목)을 입력하고, 사용자 그룹을 부모 그룹으로 선택합니다. **다음**을 선택합니다.

3.  **회원 기준 정의** 페이지에서 부모 그룹의 모든 구성원을 포함할지 아니면 빈 그룹으로 시작할지 선택합니다. [Office 365 관리 센터](http://go.microsoft.com/fwlink/?LinkId=698854)에서 수동으로 구성하거나 Active Directory에서 동기화하는 사용자의 보안 그룹을 기준으로 구성원을 포함하거나 제외합니다. 보안 그룹의 구성원이 변경되면 해당 보안 그룹을 기준으로 한 사용자 그룹의 구성원도 변경될 수 있습니다.

    > [!IMPORTANT]
    > 현재 그룹에 특정 보안 그룹 또는 관리자 그룹의 구성원이 포함되어 있는데 일부 그룹에서 구성원을 제외하는 경우 처음에 포함한 구성원이 제거됩니다. 포함한 구성원과 제외한 구성원이 모두 있는 그룹을 만들려면 포함한 구성원을 넣어 부모 그룹을 먼저 만드는 것이 좋습니다. 그런 다음 해당 부모 그룹의 자식 그룹을 만듭니다. 제외된 멤버를 새 자식 그룹에 나열합니다. 그런 다음 해당 자식 그룹을 사용하여 Intune 정책, 프로필 및 앱 배포를 관리합니다.

    > [!NOTE]
    > Azure Portal에서 사용자에게서 보고를 받는 관리자를 기준으로 그룹을 만들 수 있습니다. 이 유형의 그룹은 동적이기 때문에, 직원이 Azure Active Directory에서 관리자 팀에 추가되거나 관리자 팀에서 제거되면 그에 따라 변경됩니다. 관리자 이름에 따라 Azure 그룹을 만드는 방법은 **"관리자" 그룹으로 그룹을 구성하려면** 섹션의 [특성을 사용하여 고급 규칙 만들기](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)에 설명되어 있습니다.

4.  **직접 회원 관리 정의** 페이지에서 **찾아보기**를 선택하여 포함하거나 제외할 각 사용자를 선택합니다. 지정된 부모 그룹에 없는 사용자를 선택하는 경우 해당 장치는 부모 그룹에 자동으로 추가됩니다. 사용자를 수동으로 추가하는 옵션이 **구성원 선택** 대화 상자의 맨 아래에 있습니다. 아직 등록된 장치가 없는 사용자를 추가하려는 경우에 유용합니다.

5.  **요약** 페이지에서 선택 내용을 검토하고 **마침**을 클릭합니다.

새로 만든 그룹은 부모 그룹 아래에 있는 **그룹** 작업 영역의 **그룹** 목록에 표시됩니다. 여기서 그룹을 편집하거나 삭제할 수도 있습니다.

> [!TIP]
> 보안 그룹은 사용자 그룹을 구성할 때 유용하게 사용할 수 있는 리소스입니다. 보안 그룹은 누가 어떤 리소스에 액세스할 수 있는지 정의하기 때문에 Intune 사용자 그룹으로 쉽게 변환 가능합니다. Active Directory에서 Azure Active Directory로 동기화되는 보안 그룹 또는 Office 365 관리 센터 또는 Azure Portal을 통해 Azure Active Directory에서 직접 만든 보안 그룹은 모두 Intune에서 사용자 그룹을 만드는 데 사용할 수 있습니다.

## <a name="filter-admin-views-by-role"></a>역할별로 관리자 보기 필터링
필터링된 그룹 보기에서 IT 관리자 역할에 따라 해당 관리자가 볼 수 있는 항목을 조정할 수 있습니다. 또한 각 IT 관리자가 관리할 수 있는 그룹도 제한할 수 있습니다. 이러한 기능은 다음과 같은 경우에 유용할 수 있습니다.

-   IT 관리자가 특정 사용자와 장치에만 항목을 배포할 수 있도록 합니다.
-   IT 관리자가 해당 관리자와 관련한 그룹만 볼 수 있도록 합니다.

Intune 관리 콘솔에서 서비스 관리자를 위한 필터링된 그룹 보기를 구성할 수 있습니다. 자세한 내용은 [Microsoft Intune을 시작하기 전에 알아두어야 할 사항](/intune-classic/get-started/what-to-know-before-you-start-microsoft-intune)을 참조하세요.

서비스 관리자를 위한 필터링된 그룹 보기를 설정하면 관리자는 소프트웨어 또는 정책을 배포하거나 보고서를 실행할 때 지정된 그룹만 선택하여 볼 수 있습니다. 또한 관리자에게는 다음 관리 콘솔 페이지의 상태 정보가 보이지 않습니다.

-   **시스템 개요**
-   **그룹 개요**
-   **끝점 보호 개요**
-   **경고 개요**
-   **소프트웨어 개요**
-   **정책 개요**

### <a name="to-create-a-filtered-group-view"></a>필터링된 그룹 보기를 만들려면

1.  Intune 관리 콘솔에서 **관리** &gt; **관리자 관리** &gt; **서비스 관리자**를 선택합니다.

2.  필터링된 그룹 보기를 만들어 사용하게 할 서비스 관리자를 선택한 다음, **그룹 관리**를 선택합니다.

3.  **이 서비스 관리자가 볼 수 있는 그룹 선택** 대화 상자에서 서비스 관리자가 액세스할 수 있는 그룹을 추가한 다음 **확인**을 선택합니다.

필터링된 그룹 보기를 설정하면 IT 관리자는 나타난 그룹만 보고 선택할 수 있습니다.

## <a name="manage-your-groups"></a>그룹 관리
그룹을 만든 후에, 조직의 필요에 따라 해당 그룹을 계속 관리할 수 있습니다.

그룹을 편집하여 이름이나 설명 또는 해당 그룹에 속한 사용자를 변경할 수 있습니다.

더 이상 조직에 필요하지 않은 그룹을 삭제할 수 있습니다. 그룹을 삭제해도 해당 그룹에 속한 사용자는 삭제되지 않습니다.

## <a name="next-steps"></a>다음 단계
그룹 및 정책을 설정한 후에는 **원하는 값**과 **상태**를 검토하여 디자인의 실질적인 영향을 확인합니다.

### <a name="to-check-your-design"></a>디자인을 확인하려면

1. 장치 그룹에서 아무 장치나 선택하고 페이지 위쪽에 있는 정보의 범주를 탐색합니다.
2. **정책**을 선택합니다. Android 장치 정책 설정의 스크린샷 같은 화면이 표시됩니다.

![예: Android 설정 정책](../media/Intune-Device-Policy-v.2.jpg)

각 정책에는 **의도한 값** 및 **상태**가 있습니다. 의도한 값은 정책을 할당한 목적입니다. 상태는 장치에 적용되는 모든 정책 및 하드웨어와 운영 체제의 제한 사항과 요구 사항을 함께 고려할 때 달성하는 상태를 말합니다. 이 스크린샷에서 선택을 취소한 두 가지 예를 확인할 수 있습니다.

-   **단순 암호 허용** 을 **의도한 값**열에 나타난 것처럼 **예** 로 설정했지만 해당 **상태** 가 **해당 없음**인 경우. 이는 Android 장치의 경우 단순한 암호가 지원되지 않기 때문입니다.
-   마찬가지로 이는 Android 장치이므로 확장된 정책 항목 즉, **iOS 장치에 대한 메일 설정**은 이 장치에 적용되지 않습니다.

> [!NOTE]
> 제한 수준이 다른 두 정책을 같은 장치나 사용자에 적용하면 보다 제한적인 정책이 실제로 적용됩니다.
