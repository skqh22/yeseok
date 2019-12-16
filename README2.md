# 와디즈 펀딩 리워드(%)랭킹 및 크롤링 및 분석


### 와디즈 펀딩 사이트의 실시간 리워드 랭킹, 급상승 펀딩 상승률 랭킹, 하루 중 가장 좋아요를 많이 받은 랭킹에 대해 크롤링하고 분석했습니다

```
install.packages('rvest')
install.packages('RSelenium')
library('rvest')
library('RSelenium')
```
### ->필요한 패키지 'rvest','RSelenium'을 불러왔습니다

```
remDr <- remoteDriver(
remoteServerAddr = "localhost",
port = 4446L,
browserName = "chrome")
remDr$open()
remDr$navigate("https://www.wadiz.kr/web/main")
remDr$navigate('https://www.wadiz.kr/web/main/trend') 
```
### ->메인 홈페이지 url을 불러왔습니다

![와디즈 펀딩 메인](https://user-images.githubusercontent.com/58077375/70862277-8d498480-1f7d-11ea-8a8d-f28705c4801e.PNG)

```
percenty <- remDr$getPageSource()[[1]] #첫 화면 페이지 소스 추출
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

### -> 홈페이지 실시간 리워드 랭킹 1위~4위를 크롤링 해왔습니다
### remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
### 이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
### 불필요한 부분을 gsub로 정제하고 xdata에 넣습니다


```
percenty2 <- remDr$getPageSource()[[1]]
main2 <- read_html(percenty2)
mainfo2=html_nodes(main2,css='.commons_achievementRate__2J-KL') 

급상승 펀딩 (24시간을 기준으로 전날 대비 펀딩 달성 상승률이 높은 프로젝트)
percent11 <- gsub('<span class="commons_achievementRate__2J-KL">','',mainfo2[1:4]);percent11
percent22 <- gsub('%</span>','',percent11);percent22
ydata <- as.numeric(percent22)
ydata
```
![급상승 펀딩](https://user-images.githubusercontent.com/58077375/70862314-27113180-1f7e-11ea-9c0b-792ba659c3bb.PNG) 

### -> 홈페이지/트렌드 페이지에서 일정 기간동안 펀딩 상승률 1~4위를 크롤링 했습니다
### remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
### 이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
### 불필요한 부분을 gsub로 정제하고 ydata에 넣습니다


```
percenty3 <- remDr$getPageSource()[[1]] 
main3 <- read_html(percenty3)
mainfo3=html_nodes(main3,css='.commons_achievementRate__2J-KL') 
percent111 <- gsub('<span class="commons_achievementRate__2J-KL">','',mainfo3[5:8]);percent11
percent222 <- gsub('%</span>','',percent111);percent222
zdata <- as.numeric(percent222)
zdata 
```
![좋아요 펀딩](https://user-images.githubusercontent.com/58077375/70862316-30020300-1f7e-11ea-9efc-c94a8240c113.PNG)

### -> ydata와 같이 트렌드 페이지에서 오늘 하루 좋아요를 가장 많이 받은 펀딩 1~4위를 크롤링 했습니다
### remDr$getPageSource를 사용해 페이지 소스 첫 화면을 모두 불러옵니다
### 이 소스를 read_html로 읽은 후 css 분을 크롤링 합니다
### 불필요한 부분을 gsub로 정제하고 zdata에 넣습니다.

```
xdata121410 <- c(3567,8057,394,380)
xdata121411 <- c(3567,8099,398,377)
xdata121412 <- c(3592,8117,397,381)
xdata121501 <- c(3640,8195,382,237)
xdata121517 <- c(8846,3986,1758,389)
xdata121518 <- c(8878,1817,3996,389)
xdata121519 <- c(1865,8917,4011,390)
xdata121520 <- c(1982,8959,4029,390)
total1 <- c(xdata121410,xdata121411,xdata121412,xdata121501,xdata121517,
            xdata121518,xdata121519,xdata121520)

ydata121410 <- c(10731,27419,117,750)
ydata121411 <- c(10746,27562,117,750)
ydata121412 <- c(10774,27630,117,750)
ydata121501 <- c(10799,27639,117,750)
ydata121517 <- c(10897,28148,117,758)
ydata121518 <- c(10897,28151,117,760)
ydata121519 <- c(10913,28183,117,760)
ydata121520 <- c(10928,28268,117,760)
total2 <- c(ydata121410,ydata121411,ydata121412,
            ydata121501,ydata121517,ydata121518,ydata121519,ydata121520)


zdata121410 <- c(1440,1153,16,17)
zdata121411 <- c(1422,2484,750,44)
zdata121412 <- c(381,397,16,84)
zdata121501 <- c(3640,3106,16,42)
zdata121517 <- c(300,28148,55,44)
zdata121518 <- c(389,432,0,55)
zdata121519 <- c(1754,8090,0,31)
zdata121520 <- c(1754,8090,0,31)
total3 <- c(zdata121410,zdata121411,zdata121412,zdata121501,
            zdata121517,zdata121518,zdata121519,zdata121520)
```
### ->xdata,ydata,zdata 자료들을 total1,total2,total3에 시간별로 %값을 수집했습니다

``` 
par(mfrow=c(1,3))
plot(total1,xlab='시간',ylab='리워드%')
plot(total2,xlab='시간',ylab='리워드%')
plot(total3,xlab='시간',ylab='리워드%')
```
![plot total2](https://user-images.githubusercontent.com/58077375/70861937-558c0e00-1f78-11ea-9fb1-2f6a913668be.PNG)

### -> 시간별 실시간 랭킹, 급상승 랭킹, 좋아요 순 랭킹의 리워드(%) 추이를 산점도로 분석해 보았습니다
###    결과 세 자료 모두 1등과 2등의 격차, 2등과 3등의 격차가 일정함을 보여주고있습니다
###    (단, 좋아요 순 자료의 기준은 매일매일 갱신되기때문에 자정이 넘어가는 시각에 큰 격차가 나타나고있습니다)    


![상관분석2](https://user-images.githubusercontent.com/58077375/70863105-f2a27300-1f87-11ea-9bcc-4c979bdff2fb.PNG)

### -> total1,total2,total3 각 각 자료의 상관관계를 회귀직선으로 나타내 두 자료의 회귀관계를 알아보았습니다 
