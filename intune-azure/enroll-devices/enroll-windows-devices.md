---
title: "Windows 장치 등록"
titleSuffix: Intune Azure preview
description: "Intune Azure 미리 보기: Windows 장치에 대한 Intune MDM(모바일 장치 관리)을 사용하도록 설정합니다."
keywords: 
author: nathbarn
manager: nathbarn
ms.date: 03/15/17
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d
ms.reviewer: damionw
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: a95aca706a4996d40e268a80c7c334ebb9854df5
ms.openlocfilehash: 6cbaf8414452f11f0aa97616bbed2cf164b49ac0
ms.lasthandoff: 03/15/2017


---

# <a name="enroll-windows-devices"></a>Windows 장치 등록

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

다음 방법 중 하나를 사용하여 Windows 장치에 대한 등록을 설정할 수 있습니다.

- [**Azure Active Directory Premium에 Windows 10 및 Windows 10 Mobile 자동 등록**](#set-up-windows-10-and-windows-10-mobile-automatic-enrollment-with-azure-active-directory-premium)
 -  이 방법은 Windows 10 및 Windows 10 Mobile 장치에만 적용됩니다.
 -  이 방법을 사용하려면 Azure Active Directory Premium이 있어야 합니다. 그렇지 않은 경우 Windows 8.1 및 Windows Phone 8.1에 대한 등록 방법을 사용하세요.
 -  자동 등록을 사용하도록 설정하지 않은 경우 Windows 8.1 및 Windows Phone 8.1에 대한 등록 방법을 사용합니다.

- [**CNAME을 구성하여 Windows 8.1 및 Windows Phone 8.1 등록**](#simplify-enrollment-by-configuring-cname)
 - Windows 8.1 및 Windows Phone 8.1 장치를 등록하려면 이 방법을 사용해야 합니다.
 - Azure AD(Active Directory) Premium이 없는 경우에도 이 방법을 사용할 수 있습니다.


## <a name="prerequisites"></a>전제 조건

다음 구성 요소 중 일부가 Intune Azure 미리 보기에 아직 없는 경우 클래식 Intune 관리 콘솔에서 수행해야 합니다.

- [사용자 지정 도메인 이름 구성](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-2)
- [MDM(모바일 장치 관리) 기관](set-mdm-authority.md)을 **Microsoft Intune**으로 설정
- [회사 포털 앱 구성](/intune-azure/manage-apps/company-portal-app.md)
- 사용자에게 라이선스 할당

[!INCLUDE[AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## <a name="enable-windows-workplace-enrollment"></a>Windows 작업 공간 등록 사용

사용자로 하여금 Azure AD Premium 자동 등록 없이도 장치를 설치 및 등록하도록 할 수 있습니다. DNS CNAME 리소스 레코드를 만들면 사용자가 서버 이름을 입력하지 않고도 Intune에서 연결 및 등록합니다.

1. **CNAME 만들기**(선택 사항)<br>
 회사의 도메인에 대한 **CNAME** DNS 리소스 레코드를 만들어야 합니다. 예를 들어, 회사의 웹 사이트가 contoso.com인 경우 DNS에 EnterpriseEnrollment.contoso.com을 enterpriseenrollment-s.manage.microsoft.com으로 리디렉션하는 CNAME을 만듭니다.

    CNAME DNS 항목을 만드는 것은 선택 사항이지만 CNAME 레코드를 사용하면 사용자가 보다 쉽게 등록할 수 있습니다. 등록 CNAME 레코드가 없으면 사용자에게 MDM 서버 이름인 enrollment.manage.microsoft.com을 수동으로 입력하라는 메시지가 표시됩니다.

    확인된 도메인이 둘 이상 있는 경우 각 도메인에 대해 CNAME 레코드를 만듭니다. CNAME 리소스 레코드에는 다음 정보가 포함되어야 합니다.

    CNAME 리소스 레코드에는 다음 정보가 포함되어야 합니다.

  |유형|호스트 이름|지시 대상|TTL|
  |--------|-------------|-------------|-------|
  |CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com |1시간|
  |CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1시간|

  `EnterpriseEnrollment-s.manage.microsoft.com` – 메일의 도메인 이름에서 도메인을 인식하여 Intune 서비스로 리디렉션을 지원합니다.

  회사에서 사용자 자격 증명에 여러 도메인을 사용하는 경우 각 도메인용으로 CNAME 레코드를 만듭니다.

  예를 들어, 회사의 웹 사이트가 contoso.com인 경우 DNS에 EnterpriseEnrollment.contoso.com을 EnterpriseEnrollment-s.manage.microsoft.com으로 리디렉션하는 CNAME을 만듭니다. DNS 레코드 변경 내용이 전파되는 데는 최대 72시간이 걸릴 수 있습니다. DNS 레코드가 전파될 때까지 Intune의 DNS 변경 내용을 확인할 수 없습니다.

2.  **CNAME 확인**<br>Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다. Intune 블레이드에서 **장치 등록** > **Windows Enrollment**(Windows 등록)를 선택합니다. 회사 웹 사이트의 확인된 도메인 URL을 **확인된 도메인 이름 지정** 상자에 입력하고 **자동 검색 테스트**를 선택합니다.

3.  **장치를 등록하는 방법과 장치가 관리될 때 발생하는 상황에 대한 정보를 사용자에게 제공해야 합니다.**

    최종 사용자 등록 지침은 [Intune에서 Windows 장치 등록](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows)을 참조하세요. [IT 관리자가 내 장치에서 볼 수 있는 항목](https://docs.microsoft.com/intune/enduser/what-can-your-it-administrator-see-when-you-enroll-your-device-in-intune-windows)으로 사용자를 보낼 수도 있습니다.

    최종 사용자 작업에 대한 자세한 내용은 [Microsoft Intune에서 최종 사용자 환경 관련 리소스](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)를 참조하세요.

회사 포털을 장치에 배포하지 않는다면 추가 작업이 필요하지 않습니다.  관리 콘솔에서 2단계 및 3단계는 무시해도 됩니다.
