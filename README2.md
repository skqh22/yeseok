와디즈 펀딩 사이트 리워드율(%) 분석



와디즈 펀딩 사이트의 실시간 리워드 랭킹, 급상승 펀딩 상승률 랭킹, 하루 중 가장 좋아요를 많이 받은 랭킹에 대해 크롤링하고 분석했습니다

```
install.packages('rvest')
     install.packages('RSelenium')
     library('rvest')
     library('RSelenium')
```

->필요한 패키지 'rvest','RSelenium'을 불러왔습니다

```remDr <- remoteDriver(
  remoteServerAddr = "localhost",
  port = 4446L,
  browserName = "chrome")
remDr$open()
remDr$navigate("https://www.wadiz.kr/web/main")
remDr$navigate('https://www.wadiz.kr/web/main/trend') 
```

->한 사이트 url을 불러왔습니다

![와디즈 펀딩 메인](https://user-images.githubusercontent.com/58077375/70862277-8d498480-1f7d-11ea-8a8d-f28705c4801e.PNG)

```percenty <- remDr$getPageSource()[[1]] #첫 화면 페이지 소스 추출
main <- read_html(percenty) #html 형식으로 불러오기
mainfo=html_nodes(main,css='.commons_achievementRate__2J-KL') 
percent1 <- gsub('<span class="commons_achievementRate__2J-KL">','',mainfo);percent1
percent2 <- gsub('%</span>','',percent1);percent2
percent3 <- gsub(',','',percent2);percent3
percent4 <- percent3[5:8];percent4 #중복된 css값들로 인해 필요한 버튼만 순서맞춰 정리
xdata <- as.numeric(percent4)
xdata
```


![실시간 랭킹](https://user-images.githubusercontent.com/58077375/70862295-dbf71e80-1f7d-11ea-9e88-9cd147c1f9a8.PNG)
-> 홈페이지 실시간 리워드 랭킹 1위~4위를 크롤링 해왔습니다
remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
불필요한 부분을 gsub로 정제하고 xdata에 넣습니다.


```#화면 페이지 소스 복사 통해 데이터 추출
percenty2 <- remDr$getPageSource()[[1]] #화면 데이터 소스 얻기 
main2 <- read_html(percenty2) #html 형식으로 읽기
mainfo2=html_nodes(main2,css='.commons_achievementRate__2J-KL') 

#급상승 펀딩 (24시간을 기준으로 전날 대비 펀딩 달성 상승률이 높은 프로젝트)
percent11 <- gsub('<span class="commons_achievementRate__2J-KL">','',mainfo2[1:4]);percent11
percent22 <- gsub('%</span>','',percent11);percent22
ydata <- as.numeric(percent22)

#급상승 펀딩 '%값' 데이터 추출값
ydata
```

![급상승 펀딩](https://user-images.githubusercontent.com/58077375/70862314-27113180-1f7e-11ea-9c0b-792ba659c3bb.PNG) 

-> 홈페이지/트렌드 페이지에서 일정 기간동안 펀딩 상승률 1~4위를 크롤링 했습니다
remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
불필요한 부분을 gsub로 정제하고 data에 넣습니다.

```#화면 페이지 소스 복사 통해 데이터 추출
percenty3 <- remDr$getPageSource()[[1]] #화면 데이터 소스 얻기 
main3 <- read_html(percenty3) #html 형식으로 읽기
mainfo3=html_nodes(main3,css='.commons_achievementRate__2J-KL') 

#오늘 가장 많은 사람들이 좋아한 펀딩 (진행중인 펀딩 중 24시간 내 좋아요를 가장 많이 받은 프로젝트)
percent111 <- gsub('<span class="commons_achievementRate__2J-KL">','',mainfo3[5:8]);percent11
percent222 <- gsub('%</span>','',percent111);percent222
zdata <- as.numeric(percent222)

#오늘 가장 많은 사람들이 좋아한 펀딩 '%값' 데이터 추출값
zdata 
```

 ![좋아요 펀딩](https://user-images.githubusercontent.com/58077375/70862316-30020300-1f7e-11ea-9efc-c94a8240c113.PNG)


-> ydata와 같이 트렌드 페이지에서 오늘 하루 좋아요를 가장 많이 받은 펀딩 1~4위를 크롤링 했습니다
remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
불필요한 부분을 gsub로 정제하고 zata에 넣습니다.





 ```![plot total2](https://user-images.githubusercontent.com/58077375/70861937-558c0e00-1f78-11ea-9fb1-2f6a913668be.PNG) ```
