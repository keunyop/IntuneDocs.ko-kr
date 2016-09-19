---
title: "Microsoft Intune을 사용한 Windows 장치 관리 설정 | Microsoft Intune"
description: "Microsoft Intune으로 Windows 10 장치를 비롯한 Windows Phone PC에 대한 MDM(모바일 장치 관리)을 설정합니다."
keywords: 
author: NathBarn
manager: angrobe
ms.date: 08/29/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 9a18c0fe-9f03-4e84-a4d0-b63821bf5d25
ms.reviewer: damionw
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ebb1648ab13d31a2ba1ab17615814be8dda8a08c
ms.openlocfilehash: 9b063c1e6b1ff5dcab16fce958ede49303284b18


---

# Windows 장치 관리 설정

Intune 관리자는 두 가지 방법으로 Windows PC 등록 및 관리를 수행하도록 설정할 수 있습니다.

- **[Azure AD에 자동으로 등록](#azure-active-directory-enrollment)** - Windows 10 및 Windows 10 Mobile 사용자가 장치에 회사 또는 학교 계정을 추가하여 장치를 등록합니다.
- **[회사 포털 등록](#company-portal-app-enrollment)** - Windows 8.1 이상 장치의 경우 회사 포털 앱을 다운로드 및 설치한 다음 앱에서 회사 또는 학교 계정 자격 증명을 입력하는 방식으로 등록합니다.

[!INCLUDE[AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## 회사 포털 앱 등록 구성
사용자가 Intune 회사 포털 앱을 설치하고 해당 앱에서 장치를 등록하는 방식으로 사용 중인 장치를 등록하도록 할 수 있습니다. DNS CNAME을 만들면 사용자가 서버 이름을 입력하지 않고도 Intune에서 연결 및 등록할 수 있습니다.

1. **Intune 설정**<br>
모바일 장치 관리를 아직 준비하지 않은 경우 [모바일 장치 관리 기관](get-ready-to-enroll-devices-in-microsoft-intune.md#set-mobile-device-management-authority)을 **Microsoft Intune**으로 설정하고 MDM을 설정하여 관리를 준비합니다.

2. **CNAME 만들기**(선택 사항)<br>등록을 쉽게 수행할 수 있도록 회사 도메인용 **CNAME** DNS 리소스 레코드를 만듭니다. CNAME DNS 항목은 선택 사항이지만 CNAME 레코드를 만들면 사용자가 더욱 쉽게 등록을 수행할 수 있습니다. 등록 CNAME 레코드가 없으면 사용자에게 MDM 서버 이름인 `https://manage.microsoft.com`을 수동으로 입력하라는 메시지가 표시됩니다.  CNAME 리소스 레코드에는 다음 정보가 포함되어야 합니다.

  |유형|호스트 이름|지시 대상|TTL|
  |--------|-------------|-------------|-------|
  |CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com |1시간|
  |CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1시간|

  `EnterpriseEnrollment-s.manage.microsoft.com` – 메일의 도메인 이름에서 도메인을 인식하여 Intune 서비스로 리디렉션을 지원합니다.

  `EnterpriseRegistration.windows.net` - 회사 또는 학교 계정을 사용하여 Azure Active Directory에 등록하는 Windows 8.1 및 Windows 10 Mobile 장치를 지원합니다.

  회사에서 사용자 자격 증명에 여러 도메인을 사용하는 경우 각 도메인용으로 CNAME 레코드를 만듭니다.

  예를 들어, 회사의 웹 사이트가 contoso.com인 경우 DNS에 EnterpriseEnrollment.contoso.com을 EnterpriseEnrollment-s.manage.microsoft.com으로 리디렉션하는 CNAME을 만듭니다. DNS 레코드 변경 내용이 전파되는 데는 최대 72시간이 걸릴 수 있습니다. DNS 레코드가 전파될 때까지 Intune의 DNS 변경 내용을 확인할 수 없습니다.

3.  **CNAME 확인**<br>[Intune 관리 콘솔](http://manage.microsoft.com)에서 **관리** &gt; **모바일 장치 관리** &gt; **Windows**를 클릭합니다. 회사 웹 사이트의 확인된 도메인 URL을 **확인된 도메인 이름 지정** 상자에 입력하고 **자동 검색 테스트**를 클릭합니다.

  ![Windows 장치 관리 대화 상자](../media/enroll-intune-winenr.png)

4.  **선택적 단계**<br>Windows 10에서는 **테스트용 로드 키 추가** 단계를 수행할 필요가 없습니다. **코드 서명 인증서 업로드** 단계는 Windows 스토어에서 제공되지 않는 LOB(기간 업무) 앱을 장치에 배포하려는 경우에만 수행하면 됩니다. [자세한 정보](set-up-windows-phone-8.0-management-with-microsoft-intune.md)

6.  **사용자에게 알림**<br>장치를 등록하는 방법과 장치가 관리될 때 발생하는 상황에 대한 정보를 사용자에게 제공해야 합니다.
      - [Microsoft Intune 사용 방법에 대해 최종 사용자에게 알릴 내용](what-to-tell-your-end-users-about-using-microsoft-intune.md)
      - [Windows 장치용 최종 사용자 가이드](../enduser/using-your-windows-device-with-intune.md)

### 참고 항목
[Microsoft Intune에 장치를 등록하도록 준비](get-ready-to-enroll-devices-in-microsoft-intune.md)



<!--HONumber=Aug16_HO5-->

