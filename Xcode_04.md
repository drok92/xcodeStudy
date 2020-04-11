# 화면 제어

---

- #### 화면 제어 방식

  1. 프로그래밍적 화면 전환 : 동적 화면 전환
  2. GUI(스토리보드) 방식 화면 전환 : 정적 화면 전환

- #### Container View Controller

  콘텐츠를 직접 배치하여 화면을 보여주는 대신 다른 뷰 컨트롤러를 구조화하는 역할을 하는 뷰 컨트롤러

  컨테이너 뷰 컨트롤러를 이용하여 뷰만 교체하는 식으로 화면 전환 가능

- #### 뷰를 이용한 화면 전환

  하나의 뷰 컨트롤러 안에 두 개의 루트 뷰를 준비하고 상태에 따라 교체

  하나의 뷰 컨트롤러 아래에 하나의 루트 뷰를 관리하는 MVC 패턴을 거스르는 방식

- #### 뷰 컨트롤러를 직접 호출하여 화면 전환

  직접 표시한다는 의미로 **프레젠테이션 방식**이라고도 함

  > present(_:animated:)

  - 입력받은 인스턴스를 이용해 새로운 화면을 나타내고 화면 전환 시 애니메이션 효과 여부도 설정 가능

  > present(_:animated:completion:)

  - 실행 구문을 클로저나 함수 형식으로 입력받아 화면 전환이 끝난 후에 호출 해주는 역할을 함
  - 화면 전환 처리가 끝나기를 기다리지않고 다음 작업을 이어서 수행하는 방식인 **비동기 방식**을 사용

  > dismiss(animated:)

  - 이전 화면으로 돌아가는 기능이기 때문에 뷰 컨트롤러의 인스턴스를 인자값으로 받지 않음

  > dismiss(animated:completion:)

  - 화면 복귀가 완전히 처리되었을 때 실행할 구문을 인자값으로 입력받아 실행 시킴

- #### UIStoryboard 초기화 과정

  > // UIStoryboard 초기화 과정에서 파일을 직접 지정
  >
  > let storyboard = UIStoryboard(name: "Main", bundle: Bundle.main)
  >
  > let uvc = storyboard.instantiateViewController(withIndentifier:"SecondVC")
  
  - 첫번째 인자값은 파일명으로 확장자는 생략, 두번째 인자값은 스토리보드 파일을 읽어들일 위치
  
- #### instantiateViewController(withIdentifier:)

  인자값으로 입력받은 아이디를 이용하여 스토리보드에서 뷰 컨트롤러를 찾고 연결된 클래스를 읽어와

  뷰 컨트롤러에 대한 인스턴스를 생성

- #### uvc.modalTransitionStyle = UIModalTransitionStyle.coverVertical

  화면 전환 스타일을 정의하는 코드로 4개의 기본 전환 효과가 있다

  - .coverVertical : 아래에서 위쪽으로 새로운 화면이 올라감
  - .crossDissolve : 디졸브 효과로 두 화면이 서로 교차하면서 전환됨
  - .flipHorizontal : 화면 중앙의 축을 기준으로 화면이 돌아가면서 전환됨
  - .partialCurl : 화면 오른쪽 아래 모서리부터 페이지가 말려 올라가는 효과를 주며 전환됨

- #### self.present(uvc, animated: true)

  최종적으로 화면 전환을 처리는 메소드

  위 메소드의 호출 대상은 뷰 컨트롤러 자신이다

  뷰 컨트롤러 인스턴스를 저장한 상수를 입력받아 넘기고, 애니메이션 효과 여부를 Bool 타입으로 설정함

- #### ViewController와 클래스 연결

  새로 만든 뷰 컨트롤러의 인스펙터 창에서 Identity Inspector를 열어 Class 항목을 바꿔줌

- #### Unwind

  iOS에서 이전 화면으로 돌아가는 것을 의미, 별도의 메소드가 제공됨

  화면 전환 방식이 바뀌면 Unwind 메소드도 바뀜

- #### 네비게이션 컨트롤러를 이용한 화면 전환

  네비게이션 바를 이용해 계층적인 성격을 띠는 뷰 컨트롤러의 구조 관리

  뷰 컨트롤러의 포인터를 네비게이션 스택(Stack)으로 관리

  시작점인 루트 뷰 컨트롤러가 네비게이션 컨트롤러에 직접 연결되고 네비게이션 바는 유지

- #### 네비게이션 컨트롤러 추가 방법

  - 오브젝트 라이브러리에서 네비게이션 컨트롤러를 직접 추가 : 루트 뷰 컨트롤러인 테이블 뷰 컨트롤러가 같이 추가됨
  - Embed In 기능으로 추가 : 뷰 컨트롤러 활성화 후 Xcode 메뉴의 [Editor]-[Embed In] 에서 추가
  - 기본적으로 다른 뷰 컨트롤러에도 네비게이션 바 생성, 왼쪽 상단에 뒤로가기 버튼이 자동생성

- #### pushViewController(_:animated:)

  네비게이션 스택 최상위에 뷰 컨트롤러 객체를 추가하는 메소드

  이 메소드가 호출하는 대상이 네비게이션 컨트롤러이다

- #### popViewController(animated:)

  네비게이션 컨트롤러에 의해 화면이 전환되었을 때 이전 화면으로 되돌아가는 메소드

- #### 세그웨이 (Segue)를 이용한 화면 전환

  - 스토리보드에서 뷰 컨트롤러 사이의 연결 관계 및 화면 전환을 관리하는 세그를 이용
  - 출발점이 뷰 컨트롤러 자체인 경우를 **''메뉴얼 세그웨이''**라고 함
  - 출발점이 버튼 등인 경우 **''액션 세그웨이''** 또는 **"트리거 세그웨이"**라고 함

- #### 액션 세그웨이

  - 트리거(버튼, 테이블 셀, 제스처 등)와 세그웨이가 직접 연결된 것을 의미
  - 화면 전환을 위해 코드가 일절 필요하지 않음
  - 스토리보드에 화면 전환 관계가 명료하게 표시되어 직관적으로 파악 가능

  ##### 연결 방법

  - 연결을 해줄 객체를 Ctrl + 마우스 왼쪽 버튼으로 뷰 컨트롤러까지 드래그

- ####  시작 컨트롤러 지정

  스토리보드에서 진입점으로 시작하는 화살표로 시작 컨트롤러 지정 가능

  시작 컨트롤러로 원하는 뷰 컨트롤러를 선택하고 Attribute Inspector에서 [Is Initial View Controller] 항목 체크

- #### 메뉴얼 세그웨이

  액션 세그웨이와 달리 트리거 없이 수동으로 실행해야 하므로 별도의 소스 코드가 필요

  > performSegue(withIdentifier : <세그웨이 식별자>, sender : <세그웨이 실행 객체>)

  - 메뉴얼 세그웨이를 실행하기 위한 메소드이다

  > #### 연결 방법

  1. 뷰 컨트롤러 상단 Dock Bar 에서 첫번째 아이콘(View Controller)를 다른 뷰 컨트롤러에 드래그하여 연결

  2. 세그웨이를 선택하여 Identifier을 입력

  3. 액션 메소드를 만들어주고 위 메소드를 입력

- #### 다양한 화면 전환 효과

  세그웨이를 선택하여 Attribute Inspector에서 [Transition] 항목에서 기본 4가지 선택 가능

- #### Unwind - 화면 복귀

  ##### Unwind Segue

  - 뷰 컨트롤러 상단의 Dock Bar 에서 세번째 Exit를 이용하여 화면 복귀가 가능함

  > @IBAction func <메소드 이름>(_ sender: UIStoryboardSegue) {}

  - 되돌아갈려는 뷰 컨트롤러 클래스에 작성하는 메소드

  > #### 연결 방법

  - 돌아가고자 하는 뷰 컨트롤러 클래스에 Unwind 메소드를 정의하고 돌아갈 버튼이 있는 뷰 컨트롤러 상단 Dock Bar의 Exit에 버튼이나 아이콘을 드래그하여 unwind 메소드 선택 후 연결

- #### 커스텀 세그웨이

  원하는 기능을 구현하기 위해 UIStoryboardSegue 클래스를 서브클래싱하여 새롭게 정의하는 방법

  > #### 구현 방법

  - UIStoryboardSegue 클래스를 상속 받는 커스텀 클래스를 정의할 새로운 스위프트 파일 추가

    > override func perform() {
    >
    > ​	// 세그웨이의 출발지 뷰 컨트롤러
    >
    > ​	let srcUVC = self.source
    >
    > ​	// 세그웨이의 목적지 뷰 컨트롤러
    >
    > ​	let destUVC = self.destination
    >
    > ​	// fromView에서 toView로 뷰를 전환
    >
    > ​	UIView.transition(from: srcUVC.view, to: destUVC.view, duration: 2, options: .transitionCurlDown)
    >
    > }

    - 마지막 transition에서 from은 출발지 뷰, to는 목적지 뷰, duration은 화면 전환에 소요되는 시간, options는 애니메이션 전환 옵션, completion은 화면 전환이 끝난 후 실행할 함수나 클로저 구문이다

  - 세그웨이를 Custom으로 지정해준 뒤, Attribute Inspector 탭에서 [Class] 항목에서 작성한 클래스를 선택

- #### 전처리 메소드(Pre-Process Method)

  코코아 터치 프레임워크는 세그웨이가 실행되기 전에 특정 메소드를 호출하도록 설계되어 있음

  이를 이용하여 화면 전환 전에 필요한 처리를 할 수 있다

  > prepare(for segue: UIStoryboardSegue, sender: Any?) {...}

  - 전처리 메소드는 직접 호출 할수 있는것이 아니라 시스템이 필요한 시점에 호출하도록 설계됨

- #### NSLOG

  파운데이션 프레임워크에서 정의된 클래스로, 입력된 문자열을 Xcode의 디버그 콘솔에 출력함

  주로 값을 확인하거나 실행 과정에서 발생하는 여러 과정을 체크하는 용도로 많이 사용함

