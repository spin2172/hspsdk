.. _overview:


HSP가 제공하는 기능
===============
 
이 페이지에서는 HSP가 제공하는 여러 기능들에 대해 소개해드립니다.
 
HSP를 사용하시면 게임에서 독자적으로 구현하기 어려운 기능이나 데이터를 제공받아 사용 하실 수 있습니다. 이러한 기능들은 게임에서 공통적으로 필요한 기능들을 모아 놓은 것으로 효율적인 게임 개발을 가능하게 합니다. 뿐만 아니라 많은 사용자들로부터 이미 안정성과 성능이 검증되어 있으므로 안정적인 게임 서비스 제공이 가능합니다.
 



Auth & Login
 
HSP는 한게임뿐만 아니라 여러 IdP(Identity provider)의 계정을 이용한 ID/PASSWORD 기반의 OAuth로그인과 단말기의 ClientUUID를 이용한 게스트 로그인을 지원합니다.
 
게스트 로그인을 이용하면 사용자는 아무것도 입력하지 않아도 바로 게임에 로그인하여 간편하게 게임을 시작 할 수 있습니다. 게임은 OAuth 로그인 사용자와 게스트 로그인 사용자의 구분 없이 동일하게 사용자의 게임데이터를 관리 할 수 있습니다. 또한 사용자의 편의성을 위해 자동 로그인 기능을 제공합니다.
HSP Login을 이용해 인증하게 되면 어떤 IDP로 로그인하더라도 자동으로 고유한 회원번호를 발급받게 됩니다. HSP 인증을 이용하면 이 회원번호를 기준으로 사용자를 구별하게 되므로 어떠한 IDP를 통해 로그인했더라도 동일한 방식으로 구현이 가능합니다.
 
이와 같은 인증기능은 API 함수 하나로 쉽게 사용 할 수 있습니다. 따라서 개발자는 복잡한 인증 절차나 법적 문제, 정책적 문제 등을 고려하지 않고 쉽게 인증 기능을 구현할 수 있습니다. 또한 여러IDP의 다양한 인증방식 역시 하나의 API 함수로 쉽게 연동할 수 있습니다.
 

Profile
 
HSP는 다음과 같이 간단한 사용자 정보를 제공합니다.
 
-       고유 회원번호(sNo), 별명, 성별, 나이, 사진 URL, 오늘의 한마디, 처벌 여부 등
 
HSP Login을 이용해서 받은 고유한 회원번호를 통해 사용자 정보를 쉽게 관리할 수 있습니다.
 
위 회원정보는 인증 방식과 관계 없이 모든 회원에 대해서 제공되며, API 함수를 호출하면 간단히 얻을 수 있습니다.
 

앱 초기정보 관리 - Launching
 
서비스되고 있는 게임 앱은 기동시 여러 정보가 필요합니다. 게임 클라이언트(앱)이 업데이트가 필요하지는 않은지, 현재 서버가 서비스가 가능한 상태인지, 그 외에도 공지해야 할 내용도 있을겁니다.
HSP는 그런 각종 데이터를 게임 초기에 게임 앱에게 제공하고, 이것을 HSP에서는 Launching또는 LNC라고 부릅니다.
 
이 초기정보는 HSP Admin으로부터 운영자가 설정이 가능하며, 제공되는 정보는 다음과 같습니다.
-       게임 점검 정보, 긴급 공지정보
-       게임 클라이언트의 업데이트 필요여부, 다운로드 URL
-       게임안내페이지 URL
-       그 외의 각종 데이터
 
 

HSP 설정 관리 – HSA(HSP Admin)
 
HSP를 사용하기 위해서는 HSP에 각종 게임의 정보를 제공할 필요가 있습니다. 또한, 게임 운영시 HSP의 기능을 사용할 필요도 있습니다.
예를 들면, 운영자가 자기 게임이용자들에게 이벤트메시지를 발송할 수도 있�지요. 또는, 게임클라이언트 업데이트가 필요하면, 게임업데이트가 필요하니 게임 실행시 설치페이지로 이동하라고 HSP에게 명령을 줄 수도 있을겁니다.
 
HSP는 이런 HSP기능사용을 위한 Admin Page를 제공합니다. 웹 페이지에서 간단히 HSP의 각종 기능을 설정, 사용하실 수 있습니다.
 

Social Relation(친구) - Amigo
 
HSP는 스마트폰 게임에 적합한 Social 기능을 성능과 확장성 그리고 유연성을 고려하여 제공합니다.
 
HSP는 상대방에게 친구를 요청하고 수락을 받아서 친구가 되는 양방향 친구와 트위터와 같이 상대방의 동의 없이 친구 관계를 맺을 수 있는 단방향 친구를 맺는 기능을 모두 지원하고 있습니다.
또한 나를 기준으로 관계에 있는 친구의 친분도를 나타내는 Social Point와 HSP에서 제공하는 정보 외에 추가로 게임에서 정의하여 사용할 수 있는 확장 정보인 Extra data를 제공합니다.
 
HSP Amigo는 Layered Architecture를 적용하여 HSP SDK 없이 HTTP통신을 통해 게임 클라이언트 단독으로 사용 하실 수도 있습니다.
 

 

Ranking
 
HSP는 사용자들의 순위를 보여주는 랭킹 리스트(리더 보드) 기능을 제공합니다. 많은 데이터에 대해 빠른 응답과 안정적인 성능을 보장하며, 다양한 종류의 랭킹 리스트를 산출 할 수 있습니다. HSP가 제공하는 랭킹 리스트는 다음과 같습니다.
 
- 랭킹 산출 기간 : 일간/주간/월간/평생
- 랭킹 순위 산출 방법 : 오름차순/내림차순, 최초 기록자 우선/최근 기록자 우선
 
랭킹 리스트는 기본적으로 10만 등까지 제공하며, 그 이상의 랭킹 정보가 필요하면 기술 PM과 협의를 통해 제공해드립니다.
 
HSP는 모든 게임 사용자 중에서의 랭킹뿐 아니라 사용자의 친구들 중에서의 랭킹도 산출할 수 있으므로 친구 랭킹 기능을 쉽게 개발할 수 있습니다.
 
Ranking 정보는 RAT(Ranking Admin Tool)를 통해 쉽게 관리할 수 있습니다.
 

 

Push
 
HSP는 iOS와 Android 두 OS 사용자에게 실시간 알림 서비스(Push)를 제공합니다.
 
개발자는 Apple이나 Google이 제공하는 Push 플랫폼에 대해 잘 알지 못하더라도 동일한 API를 이용하여 쉽게 Push 메시지를 게임 클라이언트로 전달할 수 있습니다.
 
비개발자라도 HSP의 운영도구인 HSA를 이용하면, 게임의 모든 사용자에게 쉽게 Push 메시지를 발송할 수 있습니다.
 

 

CGP – Cross Game Promotion
 
HSP는 일방적인 배너광고 형태를 벗어나, 게임 사용자에게 보상을 제공하고 새로운 게임을 체험해 보도록 하는 등의 프로모션 기능을 제공합니다.
 
HSP의 프로모션 기능을 이용하면 다른 게임 사용자가 해당 게임으로 유입되거나 해당 게임 사용자가 다른 게임에 유입되도록 할 수 있습니다. 또한 HSP는 게임 내부에서도 콘텐츠 활성화를 위한 In-game promotion 기능도 지원합니다.
 
HSP는 개발자에게 프로모션 이벤트를 소개할 수 있는 웹 페이지와 이벤트 관련 제반 기능을 제공합니다.
 
개발자는API를 통해 간단하게 프로모션 기능을 사용할 수 있으며, 프로모션 기능 사용 중에 프로모션의 내용이 변경되어도 게임 수정 없이 HSA를 통해 관리 할 수 있으며, 변경 내용은 자동으로 각 게임에 반영됩니다.
 

 

Payment & Item
 
HSP의 결제 기능은 Apple의 IAP와 Android 마켓, 통신사 마켓 등 여러 마켓을 지원하고 있습니다.
 
개발자는 동일한 API로 모든 마켓의 결제 서비스를 이용할 수 있으며, HSP는 결제 처리시에 발생한 로그를 제공하고 오류 발생시 트랜잭션 처리를 보장합니다.
 
HSP의 결제 기능은 게임 서버 없이 독립 실행되는 게임뿐만 아니라 클라이언트-서버 구조의 게임도 지원하고 있습니다.
 

 

HSA – Hangame Smartphone Admin
 
HSP는 자체 운영도구인 HSA를 제공하고 있습니다.
 
HSA를 통해 게임 등록, 회원 정보 조회, 마켓 관리, 공지 등록, 랭킹, 도전과제, 점검, 그리고 Push 메시지 발송 등의 여러 게임 운영 도구를 사용 할 수 있습니다.
 

 

Others
 
HSP는 그 밖에도 게임 이용자 동접 지표 집계를 위한 Presence와 HOG, 사용자의 프로필 이미지 관리를 위한 Photo, 커넥션 관리 및 접속정보를 위한 Lighthouse를 제공합니다.
 
또한 위 컴포넌트의 모든 정보는 Mashup을 통해 유기적으로 연결되어 여러 컴포넌트가 따로 관리하고 있는 정보를 하나의 조합된 형태로 제공 받아 사용 할 수 있습니다.
 
 
마지막으로 HSP는 개발자를 위해 최신의 온라인 가이드 문서를 웹으로 제공하고 있습니다. ( http://pubsdk.hangame.com )
 

