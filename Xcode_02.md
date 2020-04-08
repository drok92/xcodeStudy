# iOS 앱 구조와 코코아 터치 프레임워크

---

- #### 시작 진입점(Entry Point)

  운영 체제가 앱 내부에 정의된 main() 함수부터 호출하여 시작하는 것

  iOS에서는 @UIApplicationMain 어노테이션이 엔트리 포인트이다

- #### MVC 패턴

  Model(데이터) - View(화면) - Controller(이벤트) 로 이어지는 세 개의 핵심 구조를 이용한 앱의 설계

  데이터와 비지니스 로직을 시각적인 표현으로부터 분리하여 화면 상관없이 데이터나 비지니스 로직 작성이 가능

- #### 앱의 생명주기 (상태 변화)

  - **Not Running** : 앱이 시작되지 않았거나 실행되었지만 시스템에 의해 종료된 상태
  - **Inactive** : 앱이 전면에서 실행중이지만, 아무런 이벤트를 받지 않고 있는 상태
  - **Active** : 앱이 전면에서 실행중이며, 이벤트를 받고 있는 상태
  - **Background** : 앱이 백그라운드에 있지만 여전히 코드가 실행되고 있는 상태
  - **Suspended** : 앱이 메모리에 유지되지만 실행되는 코드가 없는 상태

- #### AppDelegate

  UIApplication으로부터 권한을 일부 위임받아 커스텀 코드와 상호작용하는 역할을 담당

  기본적으로 앱 내에서 오직 하나의 인스턴스만 생성되도록 시스템적으로 보장받음

- #### application(_:willFinishLaunchingWithOptions:)

  앱이 구동되어 필요한 초기 실행 과정이 완료되기 직전에 호출되는 메소드

- #### application(_:didFinishLaunchingWithOptions:)

  앱이 사용자에게 화면으로 표시되기 직전에 호출되는 메소드

  앱이 실행된 후에 진행할 커스터마이징이나 초기화를 위한 코드를 여기에 작성하면 됨

- #### applicationDidBecomeActive(_:)

  실행된 앱이 화면 전면에 표시될 때 호출되는 메소드

  앱이 Inactive 상태로 바뀌면서 일시 중지된 작업이 있다면 재시작하는 코드를 여기에 작성해야함

- #### applicationDidEnterBackground(_:)

  앱이 백그라운드 상태에 진입했을 때 호출되는 메소드

  종료된 앱이 다시 실행될 때 현재 상태를 복구할 수 있도록 이 메소드에 저장처리하는 것이 좋음

- #### applicationWillTerminate(_:)

  앱이 종료되기 직전에 호출되는 메소드

- #### UIKit Framework

  파운데이션 프레임워크와 더불어 코코아 터치 프레임워크를 이루는 주 프레임워크

  주로 유저 인터페이스를 제공함

- #### Foundation Framework

  기본 데이터 형식, 컬렉션 및 앱의 기본 객체와 기반 기술을 제공

  UIKit이 외부적인 부분을 담당한다고 하면 파운데이션은 내부적인 기능을 처리하기 위함

- #### 코코아 터치 프레임워크(Cocoa Touch Framework)

  애플 환경에서 터치 기반의 어플리케이션을 제작하기 위한 도구들의 모음

  macOS를 제외한 나머지 기기들에서 개발하기 위한 프레임워크

  UIKit, Foundation, WebKit 프레임워크 등을 포함하고 있는 최상위 레벨 프레임워크

- #### NSWindow

  코코아 프레임워크에서 기본적으로 제공하는 윈도우 객체

  윈도우 왼쪽 위 제어 버튼이 대표적

- #### 프레임워크의 계층 관계

  대부분의 상위 프레임워크는 하위 프레임워크에 의존적

  상위 계층일수록 어플리케이션 제작에 쉽게 사용할 수 있는 형태로 됨

  하위 계층일수록 추상적이면서 하드웨어 쪽에 가까워 구현하기 힘듬

- #### iOS의 프레임워크 계층 구조

  > ##### Core OS 계층

  - 제일 아래 계층으로 커널, 파일 시스템, 네트워크, 보안 등 운영 체제로써 기능을 위한 핵심 영역

  > ##### Core Service 계층

  - 문자열 처리, 데이터 집합 관리, 주소록 관리나 GPS, 자이로스코프 센서 같은 하드웨어 특성에 기반한 서비스 제공

  > ##### Media 계층

  - 코어 서비스 계층에 의존적이며 그래픽, 텍스트, 오디오, 애니메이션 등 비디오 파일같은 미디어 파일 담당

  > ##### Cocoa Touch

  - 어플리케이션 계층으로 직접 지원하며, 이 곳에 UIKit와 GameKit, MapKit 등 프레임워크들이 속함

- #### 프레임워크와 접두어, 주요 객체들

  - Foundation Framework : NS <NSDate, NSData, NSURL, NString, NSLog, NSArray> 등등
  - UIKit Framework : UI <UIApplication, UIViewController, UIView, UIButton> 등등
  - UserNotifications Framework : UN <UNNotification, UNNotificationTrigger> 등등
  - MapKit Framework : MK <MKAnnotationView, MKCircle, MKMapItem> 등등
  - Core Foundation : CF <CFBundle, CFError, CFBoolean, CFRunLoop> 등등
  - Core Graphics : CG <CGColor, CGContext, CGImage, CGLayer, CGRect> 등등
  - AVFoundation : AV <AVAssetReader, AVAudioConverter, AVAudioBuffer> 등등

- #### iOS UI의 표현 구조

  윈도우는 iOS에서 디바이스 스크린을 빈틈없이 채우기 위한 객체로, 항상 UI 표현 계층의 최상위에 위치

  윈도우는 뷰의 일종이지만 직접 콘텐츠를 가지지 않고, 콘텐츠를 가진 뷰를 내부에 배치함

  또한 화면이 전환되더라도 윈도우는 바뀌지않고 내부에 배치된 뷰의 콘텐츠만 변경

  윈도우와 뷰 사이는 ViewController를 통해 연결함

- #### Contents View Controller

  화면(Scene)을 담당하고 콘텐츠를 표시하는 뷰 컨트롤러

- #### Container View Controller

  네비게이션 컨트롤러나 탭 바 컨트롤러, 페이지 컨트롤러 같은 내부에 콘텐츠를 배치하는 대신 다른 뷰 컨트롤러를 배치하고

  서로 유기적인 관계로 엮이도록 만들어줌

- #### 뷰의 계층 구조(View hieracy)

  - **superview** : 계층 구조에서 다른 뷰를 포함
  - **subview** : 슈퍼 뷰에 속하는 뷰

- #### Root View (Contents View)

  각 씬이 가지고 있는 최상위 뷰를 지칭하는 말

  테이블 뷰 컨트롤러에서는 테이블 뷰가 루트 뷰, 컬렉션 뷰 컨트롤러에서는 컬렉션 뷰가 루트 뷰를 담당

- #### View Controller

  화면 구성 요소들 = 뷰를 관리함이 주된 역할

  화면과 데이터 사이의 상호 작용까지 관리하기도 함

  - View Controller : 가장 기본이 되는 컨트롤러로서 내부에 뷰를 포함
  - Navigation Controller : 앱의 화면 이동 관리와 연관된 처리를 담당해주는 컨트롤러, 상단에 네이게이션 바가 추가됨
  - Table View Controller : 내부에 리스트 형식의 테이블 뷰를 포함하는 컨트롤러, 화면 단위 컨트롤러임
  - Tab Bar Controller : 여러 개의 탭이 있고, 탭 터치로 화면 전환을 하는 컨트롤러, 하단에 탭 바가 추가됨
  - Split View Controller : 메인과 서브 화면을 분할하는 컨트롤러, 프로젝트 템플릿 선택 단계에서 선택가능

- #### ViewController의 생명주기 (상태 변화)

  - **Appearing** : 뷰 컨트롤러가 스크린에 등장하면서부터 등장 완료하기 직전까지의 상태, 교차 가능
  - **Appeared** : 뷰 컨트롤러가 스크린에 완전히 등장한 상태
  - **Disappearing** : 뷰 컨트롤러가 스크린에서 가려지기 시작해서 완전히 가려지기 직전까지의 상태, 또는 퇴장하기 시작해서 완전히 퇴장하기 직전까지의 상태
  - **Disappeared** : 뷰 컨트롤러가 스크린에서 완전히 가려졌거나 혹은 퇴장한 상태

  

