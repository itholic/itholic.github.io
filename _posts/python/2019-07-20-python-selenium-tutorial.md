---
title: "[python] 셀레니움(selenium) 사용법: 설치부터 네이버 자동 로그인까지"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 셀레니움으로 자동 로그인 기능 만들기

<br/>

이번에 QA 시스템을 구축하면서 E2E 테스트에 적당한 솔루션을 찾다가 셀레니움이라는 것을 알게되었다.

셀레니움은 웹 애플리케이션을 간단히 테스트할 수 있게 도와주는 프레임워크이다.

항상 그랬듯이 이게 대체 무슨 말인지는 코드로 알아보자.

<br/>

## 1. 셀레니움 설치

당연한 말이지만 셀레니움을 사용하려면 셀레니움 패키지를 설치해야한다.

오늘도 핍느님(pip)의 도움을 받아 간단히 설치해보자.

조금 복잡하니 잘 따라와야한다.

```shell
$ pip install selenium
```

우여곡절끝에 설치가 끝났다.

<br/>

## 2. 셀레니움 드라이버 다운로드 

셀레니움만 설치한다고 끝이 아니다.

셀레니움을 통해 웹브라우저를 컨트롤하기 위해서는 각 브라우저에 맞는 드라이버가 필요하다.

지원하는 브라우저는 많지만, 우선 브라우저 3대장(?)만 친절히 링크를 달아놓도록 하겠다.

- <a href="https://sites.google.com/a/chromium.org/chromedriver/downloads" target="_blank">Chrome web driver</a>
- <a href="https://github.com/mozilla/geckodriver/releases" target="_blank">Firefox web driver</a>
- <a href="http://selenium-release.storage.googleapis.com/index.html" target="_blank">IE web driver</a>

본 튜토리얼에서는 크롬 브라우저를 예제로 사용하므로, 크롬 버전에 맞는 드라이버를 받으면 된다.

<br/>

## 3. 네이버 창 띄우기

이제 파이썬 셀레니움을 사용할 모든 준비가 끝났다.

네이버 창을 띄워보자.

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5
  6 browser = webdriver.Chrome(chrome_driver_path)
  7 browser.get(naver_url)
```

(3) `chrome_driver_path`에 앞서 다운받은 크롬 드라이버의 실제 경로를 넣어주면 된다.

(6) 크롬 웹드라이버 객체를 얻고,

(7) get 메소드에 원하는 url 경로를 넣어주면 된다.

실행하면, 다음과 같이 간단하게 네이버 창이 오픈된다.

![naver_main](/assets/images/2019/07/20/python-selenium-tutorial/naver_main.png)

상단에 'Chrome이 자동화된 테스트 소프트웨어에 의해 제어되고 있습니다' 라고 떠있는 것을 볼 수 있다.

'자동화된 테스트 소프트웨어'가 바로 셀레니움을 의미하는 것이다.

<br/>

## 4. 자동 로그인하기

이제 창도 띄웠겠다, 본격적으로 로그인을 해보자.

로그인을 하려면 우선 'NAVER 로그인' 이라고 적힌 요녀석을 '클릭' 해주어야한다.

![login_button](/assets/images/2019/07/20/python-selenium-tutorial/login_button.png)

그럼 두 가지를 알아야 하는데,

첫째, 'NAVER 로그인' 이라고 적힌 창의 위치와

둘째, 클릭하는 방법 이다.

<br/>

먼저 창의 위치를 알아보자.

크롬 개발자 도구에서 해당 위치에 마우스를 올리면 경로를 알 수 있는데,

윈도우 기준 `ctrl + shift + c` 버튼을 누르면 되고,

맥 기준 `command + option + c` 버튼을 누르면 된다.

![login_button_location](/assets/images/2019/07/20/python-selenium-tutorial/login_button_location.png)

찾고자 하는 element(해당 예제의 경우 로그인 버튼) 위에 마우스를 올리면 위 화면과 같이 해당 element의 위치를 알려주는데,

해당 위치에서 우클릭을하면 다음과 같이 해당 경로를 여러가지 방식으로 복사할 수 있는 기능을 제공한다.

![login_button_location_copy](/assets/images/2019/07/20/python-selenium-tutorial/login_button_location_copy.png)

(element란 검색창, 웹툰, 뉴스, 실시간 검색어 등, 웹 페이지를 구성하는 눈에 보이는 모든 요소를 의미한다고 생각하면 된다)

<br/>

어쨌든 우선 이번 예제에서는 selector (CSS selector를 의미한다) 경로를 사용하도록 하겠다.

다음과 같이 Copy selector 버튼을 눌러 경로를 복사하고, 해당 경로를 사용해 코드를 작성해보자.

![copy_css](/assets/images/2019/07/20/python-selenium-tutorial/copy_css.png)

경로를 복사했으면 다시 코드로 돌아오자.

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5 naver_id = "내 아이디"
  6 naver_pw = "내 비밀번호"
  7
  8 browser = webdriver.Chrome(chrome_driver_path)
  9 browser.get(naver_url)
 10  
 11 login_button = browser.find_element_by_css_selector("#account > div > a > i")
 12 login_button.click()
```

(5~6) 로그인시 입력할 아이디와 비밀번호를 위한 변수를 추가했다.

(11) find_element_by_css_selector 함수의 인자로 방금 복사한 css selector 경로를 붙여넣기 해주고,

찾아낸 element를 login_button 이라는 객체로 반환한다.

(12) login_button 객체가 클릭 가능한 element라면, click() 메소드를 이용해 간단하게 클릭이 가능하다.

참고로, 다음과 같이 굳이 login_button 이라는 변수를 만들지 않고 바로 위치를 찾아 클릭할수도 있다.

 `browser.find_element_by_css_selector("#account > div > a > i").click()` 

<br/>

프로그램을 실행하면 이번에는 다음과 같은 화면까지 진행되는 것을 볼 수 있다.

![naver_login](/assets/images/2019/07/20/python-selenium-tutorial/naver_login.png)

<br/>

사실 코드를 다음과 같이 짜서, 처음부터 로그인 화면을 띄울수도 있다.

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_login_url = "https://nid.naver.com/nidlogin.login?mode=form&url=https%3A%2F%2Fwww.naver.com"
  5
  6 browser = webdriver.Chrome(chrome_driver_path)
  7 browser.get(naver_login_url)
```

그냥 처음부터 로그인 화면 url을 사용해 바로 로그인 화면을 띄워준다.

<br/>

하지만 크롬에서 개발자 도구를 활용해 element의 위치를 찾아내는 방법을 알아보기 위함도 있었고,

무엇보다 우리가 일반적으로 네이버에 로그인을 할때 바로 로그인 화면 url을 띄우지는 않으므로,

실제 사람이 로그인 하는 절차를 가장 비슷하게 따라가기 위해 이런식으로 예제를 구성했다.

<br/>

결국 셀레니움을 활용하는 가장 중점적인 목적이 E2E 테스트를 위함인데,

E2E 테스트란 대개 사용자가 일반적으로 웹에 접근하는 시나리오를 테스트하는것이기 때문이다.

<br/>

말이 잠깐 딴데로 샜다.

이제 마지막으로 아이디와 비밀번호를 입력한 후, '로그인' 버튼을 눌러 코딩을 마무리해보자.

<br/>

먼저 아이디,

![input_id](/assets/images/2019/07/20/python-selenium-tutorial/input_id.png)

복사해서, 코드에 붙여넣자

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5 naver_id = "내 아이디"
  6 naver_pw = "내 비밀번호"
  7
  8 browser = webdriver.Chrome(chrome_driver_path)
  9 browser.get(naver_url)
 10  
 11 login_button = browser.find_element_by_css_selector("#account > div > a > i")
 12 login_button.click()
 13
 14 input_id = browser.find_element_by_css_selector("#id")
```

14번째 라인에 예쁘게 추가됐다.

<br/>

그다음 패스워드,

![input_passwd](/assets/images/2019/07/20/python-selenium-tutorial/input_passwd.png)

마찬가지로 복사해서, 코드에 붙여넣자

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5 naver_id = "내 아이디"
  6 naver_pw = "내 비밀번호"
  7
  8 browser = webdriver.Chrome(chrome_driver_path)
  9 browser.get(naver_url)
 10  
 11 login_button = browser.find_element_by_css_selector("#account > div > a > i")
 12 login_button.click()
 13
 14 input_id = browser.find_element_by_css_selector("#id")
 15 input_pw = browser.find_element_by_css_selector("#pw")
```

<br/>

위치를 모두 찾았으니, 이제 아이디와 패스워드를 입력해보자!

input_id 에는 아이디를 입력할 수 있는 텍스트 창이 들어있고,

input_pw 에는 패스워드를 입력할 수 있는 텍스트 창이 들어있다고 생각하면 된다.

그리고 그 창에 무언가를 입력하려면 다음과 같이 `send_keys` 메소드를 사용하면 된다.

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5 naver_id = "내 아이디"
  6 naver_pw = "내 비밀번호"
  7
  8 browser = webdriver.Chrome(chrome_driver_path)
  9 browser.get(naver_url)
 10  
 11 login_button = browser.find_element_by_css_selector("#account > div > a > i")
 12 login_button.click()
 13
 14 input_id = browser.find_element_by_css_selector("#id")
 15 input_pw = browser.find_element_by_css_selector("#pw")
 16 
 17 input_id.send_keys(naver_id)
 18 input_pw.send_keys(naver_pw)
```

실행해보자!

<br/>

![send_id_pw](/assets/images/2019/07/20/python-selenium-tutorial/send_id_pw.png)

<br/>

아이디와 비밀번호까지 입력이 되었다.

이제 "로그인" 버튼의 위치를 알아내 클릭을 하면 끝이다.

요태까지 그래왔던 것처럼 자연스럽게 경로를 카피해주자.

![real_login_button](/assets/images/2019/07/20/python-selenium-tutorial/real_login_button.png)

이제 마지막 코드를 추가하자!

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5 naver_id = "내 아이디"
  6 naver_pw = "내 비밀번호"
  7
  8 browser = webdriver.Chrome(chrome_driver_path)
  9 browser.get(naver_url)
 10  
 11 login_button = browser.find_element_by_css_selector("#account > div > a > i")
 12 login_button.click()
 13
 14 input_id = browser.find_element_by_css_selector("#id")
 15 input_pw = browser.find_element_by_css_selector("#pw")
 16 
 17 input_id.send_keys(naver_id)
 18 input_pw.send_keys(naver_pw)
 19
 20 browser.find_element_by_css_selector("#frmNIDLogin > fieldset > input").click()
```

(20) 이번에는 element의 경로를 통해 객체를 얻어냄과 동시에 바로 click() 을 해주었다.

11~12 번 라인처럼 login_button 이라는 변수를 따로 쓰지 않고 말이다

<br/>

이제 다 끝났다!

실행해보자. 

당연한 말이지만, 실제 실행시에는 실제 본인의 네이버 아이디와 패스워드를 입력했다.

<br/>

![auto_login_fail](/assets/images/2019/07/20/python-selenium-tutorial/auto_login_fail.png)

모든것이 행복하게 끝날 줄 알았는데, 이런 창이 뜨면서 로그인을 방해한다.

코드를 다음과 같이 수정해보자.

```python
  1 from selenium import webdriver
  2
  3 chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
  4 naver_url = "http://naver.com"
  5 naver_id = "내 아이디"
  6 naver_pw = "내 비밀번호"
  7
  8 browser = webdriver.Chrome(chrome_driver_path)
  9 browser.get(naver_url)
 10
 11 login_button = browser.find_element_by_css_selector("#account > div > a > i")
 12 login_button.click()
 13
 14 browser.execute_script(f"document.getElementsByName('id')[0].value='{naver_id}'")
 15 browser.execute_script(f"document.getElementsByName('pw')[0].value='{naver_pw}'")
 16
 17 browser.find_element_by_css_selector("#frmNIDLogin > fieldset > input").click()
```

(14~15) 기존에 input_id, input_pw 를 받아와 send_keys로 내용을 입력하던 부분을 execute_script 라는 메소드로 대체하였다.

잘 보면 value를 설정해주는 부분에 naver_id와 naver_pw가 들어가 있는 것을 볼 수있다.

<br/>

이번엔 정말 끝이다! 

실행해보자.

![login_success](/assets/images/2019/07/20/python-selenium-tutorial/login_success.png)

깔끔하게(?) 로그인에 성공했다.

(읽지 않은 메일 개수가 18개인것은 절대 의도한 부분이 아니다)

<br/>

자, 그럼 최종적으로 완성된 코드를 보자.

주석을 추가했고, 바로 복사해서 쓸 수 있도록 라인수는 제거했다.

(단, chrome_driver_path 는 본인의 실제 드라이버 경로를 넣어주어야한다)

```python
from selenium import webdriver

chrome_driver_path = "다운받은 크롬 드라이버의 경로를 넣어주세요"
naver_url = "http://naver.com"
naver_id = "내 아이디"
naver_pw = "내 패스워드"

browser = webdriver.Chrome(chrome_driver_path)
browser.get(naver_url)  # 네이버 메인 화면 띄우기

browser.find_element_by_css_selector("#account > div > a > i").click()  # "NAVER 로그인" 버튼 클릭해서 로그인 화면으로 넘어가기

browser.execute_script(f"document.getElementsByName('id')[0].value='{naver_id}'")  # id 입력
browser.execute_script(f"document.getElementsByName('pw')[0].value='{naver_pw}'")  # pw 입력

browser.find_element_by_css_selector("#frmNIDLogin > fieldset > input").click()  # "로그인" 버튼 클릭해서 최종 로그인
```

<br/>

## 기타

### 예제 환경

```
OS: macOS Mojave (10.14.2)

Language: Python 3.7.2

Selenium: 3.141.0

Chrome: 75.0.3770.100 (64bit)
```

<br/>

`*` 2019년 07월 20일 기준, 정상 동작하는것을 확인하였다

`*` 네이버에서 셀레니움을 통한 자동 로그인 방지를 위해 추후 execute_script를 통한 접근도 막는다면 동작하지 않을 수 있다
