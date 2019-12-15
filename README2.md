와디즈 펀딩 사이트 리워드율(%) 분석



와디즈 펀딩 사이트의 실시간 리워드 랭킹, 급상승 펀딩 상승률 랭킹, 하루 중 가장 좋아요를 많이 받은 랭킹에 대해 크롤링하고 분석했습니다

![패키지](https://user-images.githubusercontent.com/58077375/70862046-3aba9900-1f7a-11ea-90a7-1515b45d41fa.PNG)

->필요한 패키지 'rvest','RSelenium'을 불러왔습니다

![url 불러오기](https://user-images.githubusercontent.com/58077375/70862088-ea900680-1f7a-11ea-8f5d-cec06c3e6f6d.PNG)

->한 사이트 url을 불러왔습니다


![페이지 소스1](https://user-images.githubusercontent.com/58077375/70862167-13fd6200-1f7c-11ea-9569-af8520c39fa5.PNG)

-> 홈페이지 실시간 리워드 랭킹 1위~4위를 크롤링 해왔습니다
remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
불필요한 부분을 gsub로 정제하고 xdata에 넣습니다.


![페이지 소스2](https://user-images.githubusercontent.com/58077375/70862224-eb299c80-1f7c-11ea-9399-c266f39e0b6b.PNG)

-> 홈페이지/트렌드 페이지에서 일정 기간동안 펀딩 상승률 1~4위를 크롤링 했습니다
remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
불필요한 부분을 gsub로 정제하고 data에 넣습니다.




![plot total2](https://user-images.githubusercontent.com/58077375/70861937-558c0e00-1f78-11ea-9fb1-2f6a913668be.PNG)
