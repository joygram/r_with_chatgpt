# 통계를 만난 chatGPT

chatGPT를 이용하여 통계 분석을 시도해본다.

프롬프트 엔지니어링

프롬프트 엔지니어링은 구체적이고 명확하게 `프롬프트`를 만들어 인공지능이 높은 품질의 결과물을 만들어내게 하는 방법론입니다.

특히 대규모 언어모델일 경우 고품질 결과물을 생성할 수 있도록 `프롬프트`를 설계하고 제작하는 과정이 필요합니다.

우리는 R을 이용한 통계 분석을 chatGPT를 이용해 R의 깊은 지식이 없는 상황에서도 사용할 수 있는 가능성을 확인할 수 있습니다.

내가 하고 싶은 통계 분석의 범위와 목표만 정확하게 `프롬프팅`한다면 원하는 결과를 잘 얻어낼 수 있을 것입니다.

## 도구의 선택

chatGPT를 활용하는 다양한 절차가 있겠지만

오늘은 콘솔기반의 chatGPT 패키지인 `shell_gpt` 와 `R Studio`를 활용하여 보도록 하겠습니다.

## 활용의 고려

 `shell_gpt`를 활용한다면 간단한 스크립트로 여러가지 유형의 `프롬프트`를 만들고 필요한 보고서나 분석코드를 작성하여 활용할 수 있을 것입니다.

## shell_gpt의 설치

chatGPT를 사용하기 위해서는 여타api 사용과 동일하게 openAI에서 `api-key`를 발급받아야 합니다.

### OpenAI에서 api-key발급받기

openAI에서 api키를 발급받는 절차는 다음과 같습니다.

ChatGPT가 만들어준 가이드입니다.

```
OpenAI API key 발급 방법은 다음과 같습니다.

1. OpenAI 웹 사이트에 접속합니다. (https://openai.com/)
2. 오른쪽 상단에 있는 "Login" 버튼을 클릭합니다.
3. 계정을 생성하거나 로그인합니다.
4. "API Keys" 메뉴로 이동합니다.
5. "Create new API key" 버튼을 클릭합니다.
6. 이름을 입력하고 "Create"를 클릭합니다.
7. API key가 생성되면 화면에 표시됩니다.
8. 이 API key를 사용하여 OpenAI API를 사용할 수 있습니다.

참고로 API key는 노출되지 않도록 보안에 주의해야 합니다.
```

api-key는 발급 당시에만 노출이 되고 다시 확인 할 수 없으니 복사해서 잘 보관 합니다.


## 통계분석코드 작성해보기
RStudio또는 Quarto를 이용한 디지털 글쓰기 형태의 출력물을 만들어 실행하고 분석하는 단계까지 진행하는 것을 목표로 해보도록 합니다. 

샘플 데이터를 간단하게 만들고 데이터를 기준으로 몇가지 통계 분석 진행하여보도록 합니다.
R코드 작성에 익숙하지 않은 사람이라도 바로 결과를 내어보는 것이 되는지 확인하여 봅니다. 


셈플데이터  
```csv
Surv,N,Class,isChild,Sex,Age
20,23,Crew,Adult,2,20
192,862,Crew,Adult,1,30
1,1,First,Child,2,10
5,5,First,Child,1,12
13,13,Second,Child,2,5
```

### case 1  
```bash
# sgpt "my_data.csv를 읽어서 Sex필드의 분산그래프 R을 이용해 그려줘"
Rscript -e "data <- read.csv('my_data.csv'); plot(data$Sex, var(data$Sex))"
```


### case 2
```bash
$ sgpt "my_data.csv를 읽어서 Sex필드의 분산그래프를 그리는 R코드
는?"
```
```{r}
# 라이브러리 로드
library(ggplot2)

# 데이터 불러오기
my_data <- read.csv("my_data.csv")

# Sex 필드의 분산 그래프 그리기
ggplot(my_data, aes(x=Sex, y=value)) +
  geom_point(size=3, alpha=0.5) +
  labs(title="Sex 분산 그래프", x="Sex", y="Value")
```
```
Error in `geom_point()`:
! Problem while computing aesthetics.
ℹ Error occurred in the 1st layer.
Caused by error in `FUN()`:
! object 'value' not found
Run `rlang::last_trace()` to see where the error occurred.
```
표를 그리기 위한 파라메터를 정확하게 지정해주어야 됨을 알게 됩니다. 

### case 3
```{r}
# sgpt "my_data.csv를 읽어서 Sex필드의 분산그래프를 R코드로 작성해줘"


data <- read.csv("my_data.csv")
hist(data$Sex)

```


## chatGPT를 활용 후 변화 
### 활용전 
통계 분석을 위한 코드 작성을 하기 위한 
샘플코드가 있는 블로그나 stackoverflow등을 검색 

샘플코드를 현재 데이터셋에 맞도록 수정반복 

### 활용후 
통계 분석의 목표를 명확하게 정리하여 chatGPT에 프롬프팅 
몇변의 명령을 보완하여 얻어진 결과물을 반영 

## 정리하며
chatGPT가 모든 것을 아우르는 정보를 제공해줄 수 없고 편향된 지식을 제공해줄 수 있다는 한계를 가지고 있지만 지식의 보편화와 실제 인간이 업무를 수행하는데 도움을 주는 비서의 역할을 수행하는데 그 가능성이 있다고 보여집니다. 

이후는 어떻게 변화할지 모르지만 여전히 필요한 것은 사용자가 어떤 목표를 가지고 있느냐 그리고 그것을 어떻게 활용하느냐에 따라 그 결과물의 퀄리티는 판이하게 달라지는 것이 사실입니다. 

즉, 통계분석을 위한 통찰력이 더 요구되는 세상으로 변해가고 있다는 것입니다. 단순 데이터 전처리, 수집등의 업무 위치가 많이 위태로워질 것입니다. 
