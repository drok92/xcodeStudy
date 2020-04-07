# Xcode 기초

---

- #### Include Unit Tests

  선택 후 프로젝트를 생성하면 'XXXTests'라는 폴더와 기능 단위별 케이스를 직접 정의할 수 있도록 XCTestCase를 상속받은 클래스가 추가됨

- #### Include UI Tests

  Unit Tests와 비슷한 목적의 테스트 옵션이지만 Unit Tests는 기능 단위 테스트이고 UI Tests는 화면 요소에 대한 자동 테스트임. 선택 후 프로젝트를 생성하면 XXXUITests라는 폴더와 화면 요소를 테스트하는 스크립트를 작성할 수 있도록 XCTestCase를 상속받은 클래스가 추가됨

- #### AppDelegate.swift

  앱 전체의 생명 주기 관리를 위임받은 객체인 AppDelegate를 구현한 클래스이다. 다양한 상태 변화(앱 실행,종료,활성화,비활성화,백그라운드 상태 등등)를 감지하고 이에 대한 처리를 해야할 때 이용하는 클래스

- #### ViewController.swift

  뷰 컨트롤러를 구현한 클래스. 일반적으로 화면의 개수만큼 ViewController가 필요

- #### *.storyboard

  Main.storyboard는 앱의 UI 설계를 담당하고 LaunchScreen.storyboard는 앱을 실행하면 시작 화면을 구성하는데 사용 (시작화면을 **"Splash"**라고도 함)

- #### Split-View Controller

  일반적으로 ViewController의 화면이 한 번에 하나씩 보이지만 Split-View Controller는 한 번에 여러 개의 화면이 동시에 보임

- #### Segue

  일반적으로 화면 전환에 쓰이는 방법으로 출발지와 목적지를 직접 지정하여 사용하는 방법. 두 개의 ViewController 사이에 연결된 화면 전환 객체를 세그웨이라고 함

- #### ViewController와 클래스 연결

  ViewController를 추가하면 소스 코드를 작성할 클래스를 정의하고 연결해 주어야 함 

- #### Assistant Editor

  보조 에디터를 사용할 때 현재 스토리보드에 활성화된 객체에 연결된 클래스를 열어줌

- #### func viewDidLoad()

  리소스를 초기화하거나 초기 화면을 구성하는 등, 처음 한 번만 실행해야 하는 초기화 코드는 대부분 이 메소드 내부에 작성하면 됨

- #### override

  이미 부모 메소드에 정의된 같은 메소드가 존재하여 다시 구현하기 위한 키워드로서 메소드의 이름과 파라미터, 반환 형식은 같게 유지하고 내용만 새롭게 덮어씀

- #### super.viewDidLoad()

  부모 클래스에 정의된 viewDidLoad() 메소드의 내용도 모두 실행함을 의미

- #### CallBack Method

  적절한 시점에서 시스템에 의해 자동으로 호출되는 메소드

- #### 아울렛 변수(Outlet var)

  인터페이스 빌더를 스위프트의 클래스가 참조할 수 있도록 연결된 멤버 변수

- #### Launch Screen

  **"Splash"**라고도 하며 첫 번째 ViewController로 넘어가기전 잠깐 표시되는 화면

- #### application(_:didFinishLaunchingWithOptions:)

  AppDelegate.swift에 있는 메소드로 앱이 처음 실행될 때, 필요한 시스템적 처리를 모두 끝내고 메인 화면을 표시하기 직전에 호출됨

- #### sleep(UInt32)

  앱 잠들게 하는 뜻으로, application(_:didFinishLaunchingWithOptions:) 메소드에 넣어서 앱 실행을 지연시킴

