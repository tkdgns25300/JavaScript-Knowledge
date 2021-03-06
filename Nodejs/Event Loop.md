실제 자바스크립트가 구동되는 환경(브라우저, Node.js등)에서는 주로 여러 개의 스레드가 사용되는데, 이러한 구동 환경이 단일 호출 스택을 사용하는 자바 스크립트 엔진과 연동하기 위해 사용되는 장치가 바로 '이벤트 루프' 입니다.

핵심만 말하자면, JavaScript event loop는 call stack이 비어있는 경우, task queue에서 대기하던 callback을 call stack으로 옮겨서 callback을 실행시켜주는 역할을 합니다.

자바스크립트의 함수가 실행되는 방식을 보통 "Run to Completion" 이라고 말합니다. 이는 하나의 함수가 실행되면 이 함수의 실행이 끝날 때까지는 다른 어떤 작업도 중간에 끼어들지 못한다는 의미입니다. 앞서 말했듯이 자바스크립트 엔진은 단일 호출 스택을 사용하며, 현재 스택에 쌓여있는 모든 함수들이 실행을 마치고 스택에서 제거되기 전까지는 다른 어떠한 함수도 실행될 수 없습니다.

자바스크립트에서는 함수 호출을 관리하는 call stack과 비동기 작업 처리를 위한 Web API가 함께 작업을 처리합니다. Web API는 특히 작업 완료에 시간이 오래 걸리는 작업을 처리하게 되는데, 이 결과값을 처리할 수 있는 callback 함수를 task queue에 쌓습니다.

하나의 js파일이 실행되면, 코드가 차례로 실행됩니다. 코드가 실행되는 도중에 함수가 호출이 되는 순간 call stack에 해당 함수 실행을 위한 모든 정보가 실행 컨텍스트에 담깁니다. 이 함수 내에서 또 함수가 호출되면, call stack에 새로운 실행 컨텍스트가 생깁니다. 함수 실행이 마무리 될 때 마다 결과값을 반환하고 해당 실행 컨텍스트는 없어집니다. 마지막 실행 컨텍스트부터 하나씩 빠지기 때문에 Stack 구조라고 부를 수 있는 것입니다.

이 과정 중에 호출되는 함수가 비동기로 작동되는 경우, 이 비동기 작업은 (브라우저는) Web API에서 처리됩니다.  이 작업의 결과를 처리하는 callback 함수는 이후에 call stack에서 따로 실행이 되어야 하는데, call stack에서 실행 컨텍스트가 아직 남아있는 경우 task queue에서 "대기"하게 됩니다.

시간이 오래 걸리는 작업이 call stack에 머물러서 싱글스레드로 작동되는 event loop를 막지 않도록 도와줍니다. 그래서 연산이 많고 시간이 오래 걸리는 작업은 비동기로 처리하는 것이 효율적인 것입니다.