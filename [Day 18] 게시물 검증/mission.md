#### 1. @Mock, @MockBean, @Spy, @SpyBean, @InjectMocks 의 차이를 한번 정리해 봅시다.

Mocking: 테스트에서 실제 객체 대신 **가짜 객체(mock object)**를 만들어 사용하는 기법입니다.

@Mock : 테스트에 사용할 Mock 객체를 생성하기 위해 사용하는 어노테이션입니다.

@MockBean : Spring 에서 Mock 객체에 대한 의존성을 주입하는 어노테이션입니다.

@Spy : 실제 객체를 부분적으로 Mocking 할 수 있게 합니다. 

@SpyBean : Spring의 Bean에 대해 Spy를 적용합니다. 테스트 중 일부 메서드만 Mocking 하거나 실제로 호출할 수 있습니다.

@InjectMocks : Mock 객체로 선언된 클레스에 의존성을 주입하는 어노테이션입니다. 테스트 대상 객체에 Mock 객체들이 주입됩니다.

#### 2. 아래 3개의 테스트가 있습니다.
내용을 살펴보고, 각 항목을 @BeforeEach, given절, when절에 배치한다면 어떻게 배치하고 싶으신가요?
(@BeforeEach에 올라간 내용은 공통 항목으로 합칠 수 있습니다. ex. 1-1과 2-1을 하나로 합쳐서 @BeforeEach에 배치)

@BeforeEach: 공통적으로 준비되는 데이터나 객체들을 메서드로 묶어서 처리합니다.

given: 테스트에서 설정해야 할 초기 상태나 데이터 준비를 포함합니다.

when: 테스트할 동작을 실행합니다.

then: 결과를 검증하는 부분으로, 예외 처리나 결과 값 등을 확인합니다.

```
@BeforeEach

void setUp() {
    // ?
}

@DisplayName("사용자가 댓글을 작성할 수 있다.")
@Test
void writeComment(){
    1-1 사용자 생성에 필요한 내용 준비
    1-2 사용자 생성
    1-3 게시물 생성에 필요한 내용 준비
    1-4 게시물 생성
    1-5 댓글 생성에 필요한 내용 준비
    1-6 댓글 생성
    
    // given
    
    // when
    
    // then
    
    검증
            
}

@DisplayName("사용자가 댓글을 수정할 수 있다.")
@Test
void writeComment(){
    2-1 사용자 생성에 필요한 내용 준비
    2-2 사용자 생성
    2-3 게시물 생성에 필요한 내용 준비
    2-4 게시물 생성
    2-5 댓글 생성에 필요한 내용 준비
    2-6 댓글 생성
    2-7 댓글 수정
    
    // given
    
    // when
    
    // then
    
    검증
            
}

@DisplayName("자신이 작성한 댓글이 아니면 수정할 수 없다.")
@Test
void writeComment(){
    3-1 사용자 1 생성에 필요한 내용 준비
    3-2 사용자 1 생성
    3-3 사용자 2 생성에 필요한 내용 준비
    3-4 사용자 2 생성
    3-5 사용자 1의 게시물 생성에 필요한 내용 준비
    3-6 사용자 1의 게시물 생성
    3-7 사용자 1의 댓글 생성에 필요한 내용 준비
    3-8 사용자 1의 댓글을 생성
    3-9 사용자 2가 사용자 1의 댓글 수정 시도
    
    // given
    
    // when
    
    // then
    
    검증
            
}


```

#### 제출 답변

1. 사전 준비
```
@BeforeEach : 공통 데이터

사용자 1 생성에 필요한 내용 준비

사용자 2 생성에 필요한 내용 준비

사용자의 게시물 생성에 필요한 내용 준비

게시물의 댓글 생성에 필요한 내용 준비

```

2. 사용자가 댓글을 작성할 수 있다.
````
// given

사용자 1 생성

게시물 1 생성

댓글 생성

   
// when

댓글 작성
    
// then

댓글이 작성되었는지 검증

````

3. 사용자가 댓글을 수정할 수 있다.

````
// given

사용자 1 생성

게시물 1 생성

댓글 생성

댓글 작성

   
// when

댓글 수정
    
// then

댓글 내용이 수정되었는지 검증

````

4. 자신이 작성한 댓글이 아니면 수정할 수 없다.

````
// given

사용자 1 생성

사용자 2 생성

게시물 1 생성

댓글 생성 준비

사용자 1이 댓글 작성

   
// when

사용자 2가 사용자 1의 댓글 수정 시도
    
// then

예외 메세지가 출력되었는지 확인

````
