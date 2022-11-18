<img width="689" alt="스크린샷 2022-08-12 오후 12 34 06" src="https://user-images.githubusercontent.com/83544570/184546628-78accbd5-dc81-4f0f-9276-f19eabdba1d3.png">

# ✈️ 프로젝트 소개

> [유튜브 데모 영상](https://youtu.be/S5ElqSBUMzM)

### 🐥 프론트, 백엔드 깃허브

> [팀 프로젝트 프론트엔드 GitHub](https://github.com/wecode-bootcamp-korea/35-2nd-FREEPASS-frontend)<br/> 
> [팀 프로젝트 백엔드 GitHub](https://github.com/wecode-bootcamp-korea/35-2nd-FREEPASS-backend)

#

### ✈️ JEJUPASS 웹 싸이트를 모티브한 팀 프로젝트

- 제주패스는 제주 여행의 슈퍼 앱으로 전세계 실시간 최저가 항공, 제주 맛집까지 제주도 여행의 모든 것을 확인할 수 있는 웹 사이트 입니다.
- 저희는 그 중에서도 '항공 페이지'에 집중하여 구현하였습니다.
- 또한 '깨깨오항공', '코팡항공' 등으로 정해놓고 이 기업들을 향해 날아가는 컨셉으로 재미있게 구성해보았습니다!

#

### 📅 작업기간

2022년 8월 1일(월) ~ 2022년 8월 12일(금) : 총 10일

#

### 👥 우리 팀 일원!

Front-End : 🐥 노정은, 🐶 엄성훈, 🐱 이현주, 🦆 이혜진</br>
Back-end : ⚽️ 손찬규, 🦅 박정용

#

### 📅 Front-End 사용한 기술 스택

<img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white"/> <img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white"> <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"> <img src="https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=black"> <img src="https://img.shields.io/badge/amazonaws-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white"><br />

#

### 👩🏻‍💻 본인 담당페이지<br/>

- ESG 페이지 🐶 / Ant Design(Pull Page) <br />
- 항공 메인 페이지 🐶 / Swiper(Carousel), Ant Design(Carousel) <br />
- 항공권 예약 페이지 🐶  

#

### 📅 구현 View

- react swiper, anti design 라이브러리를 사용해서 mock data로 화면 렌더링 <br />

#

##### <2차 프로젝트는 맡은 역할에서 백엔드와 통신 처리하는 과정이 없었다... ㅠㅠ 모두 직접 목데이터를 만들어서 구현하였다.>

## React Swiper PullPage 형태

- 웹페이지를 보다보면 회사소개서 같은 페이지에서 한번쯤 보게되는 풀페이지
- `Siwper 라이브러리의 사용방법과 styled component에서의 단순 적용하는 방법에 대해 학습을 하였다.`
- 필요한 컴포넌트를 상단에 임포트 하고, useEffect로 비동기로 목데이터를 호출하였고, `const StyledSwiper = styled(Swiper)` 확장기능을 사용하여 다른 className을 부여하였다.
- 이미지는 `<CarouselImg imgUrl={imgUrl} />` style props 내려주어, `background-image: url(${props => props.imgUrl})` 처리하였다.
- 화면만 작동되게 처리하였기 때문에, 좋은 코드가 전혀 아니다. 많이쓰이는 slick, swiper에 대해 더 따로 공부해 둬야겠다.

![PullPage](https://user-images.githubusercontent.com/83544570/202486756-1f086d72-8708-471b-8d62-0d75b53874bd.gif)

```jsx
단순한 목데이터들.... 현업에 가면 수십개가 달려있겠지?

[
  {
    "id": 1,
    "mtitle": "MAKE JEJU BETTER",
    "title": "그린 앰버서더는 제주를 지키기 위한 MAKE JEJU BETTER 캠페인의 멤버십입니다",
    "video": "esg_main_video.mp4"
  },
  {
    "id": 2,
    "title": "우리는 제주 여행을 통해 새로운 경험과 즐거움 그리고 힐링을 하고 떠납니다",
    "imgUrl": "bg_img01.jpg"
  },
  ...
]

import { Swiper, SwiperSlide } from 'swiper/react';
import { Pagination, Keyboard, Mousewheel } from 'swiper';
import 'swiper/css';
import 'swiper/css/pagination';

const [slidesData, setSlidesData] = useState([]);

useEffect(() => {
  fetch('/data/esgdata/esgData.json', {
    method: 'GET',
  })
    .then((res) => res.json())
    .then((data) => {
      setSlidesData(data);
    });
}, []);

return (
  <SwiperContainer>
    <StyledSwiper
      direction='vertical'
      pagination={{
        clickable: true,
      }}
      modules={[Pagination, Keyboard, Mousewheel]}
      mousewheel={true}
      keyboard={true}
    >
      {slidesData.map(({ id, video, imgUrl, mtitle, title }) => (
        <SwiperSlide key={id}>
          {video && <video src={video} type='video/mp4' autoPlay loop muted />}
          <CarouselImg imgUrl={imgUrl} />
          <CarouseTitWrap>
            <CarouseMainTit>{mtitle}</CarouseMainTit>
            <CarouseTit>{title}</CarouseTit>
          </CarouseTitWrap>
        </SwiperSlide>
      ))}
    </StyledSwiper>
  </SwiperContainer>
);

const StyledSwiper = styled(Swiper)`
  width: 100%;
  height: 100%;
  .swiper-pagination-bullets {
    right: 50px;
  }
`;
const CarouselImg = styled.div`
  position: relative;
  width: 100vw;
  height: 100vh;
  background-image: url(${(props) => props.imgUrl});
  background-repeat: no-repeat;
  background-size: cover;
  border-radius: 2px;
`;
```

#

## React Antd Carousel

- Siwper 라이브러리를 사용 후 다른 라이브러리에서도 Carousel 을 만들 수 있음을 알게 되었다. 다른 라이브러리도 사용해 보고자 antd의 캐러샐을 사용 하였다.
- 좌우 화살표를 커스텀을 해보고자 간단한 예제들을 찾아보았고, 아래와 같이 작성하였다. 그러하자 아래와 같이 오류가 뜨는 것 이였다.

![antd](https://user-images.githubusercontent.com/83544570/202520203-6e4f092b-c43c-41fe-b612-b88808288d7a.gif)

```jsx
import 'antd/dist/antd.min.css';
import { Carousel } from 'antd';

const SlickArrowLeft = (props) => <button {...props} className='slick-prev' />;
const SlickArrowRight = (props) => <button {...props} className='slick-next' />;

const settings = {
  infinite: true,
  speed: 800,
  slidesToShow: 2,
  slidesToScroll: 2,
  autoplay: true,
  draggable: true,
  arrows: true,
  prevArrow: <SlickArrowLeft />,
  nextArrow: <SlickArrowRight />,
};

<Carousel {...settings}></Carousel>;
```

### 해당오류 메세지

![error](https://user-images.githubusercontent.com/83544570/202509922-4112b6a4-91d0-4870-b298-bd62e36eacec.jpg)
원인?

```jsx
[stack overFlow]
Don't pass down all the props that you receive for custom arrows.

nextArrow: ({ firstProp, secondProps, ...otherProps }) => (
  <element {...props that you want} />
)

Something like this should work.
```

한번에 Props으로 모두 내리지 말라는것...

```jsx
const SlickArrowLeft = ({ currentSlide, slideCount, ...props }) => (
  <button {...props} className='slick-prev' />
);
const SlickArrowRight = ({ currentSlide, slideCount, ...props }) => (
  <button {...props} className='slick-next ' />
);
```

```jsx
The unknown-prop warning will fire if you attempt to render a DOM element with a prop that is not recognized by React as a legal DOM attribute/property. You should ensure that your DOM elements do not have spurious props floating around.
```

이유에 대한 설명과 해결법은 위와 같이 해결 할 수 있었다.

#

## React Swiper 카드 배너형태

- 이번엔 다시 React Swiper 라이브러리로 카드 배너를 만들어 보았다.
- 필요한 요소들을 import하고, 옵션들을 설정하고, styled를 확장하여, 기존에 설정된 클래스들의 color을 blue -> White로 설정만 해주었다.
- 처음 다뤄보는 라이브러리 캐러샐 기능들인데, 커스텀하기가 생각보다 어려웠다.
- 좋은 코드를 위해 더 만들어보며, git도 많이 살펴봐야겠다...

![swiper](https://user-images.githubusercontent.com/83544570/202529967-2723956d-926a-454c-a1e4-6129986ce26c.gif)

```jsx
import { Swiper, SwiperSlide } from 'swiper/react';
import { Navigation, Pagination, Autoplay } from 'swiper';
import 'swiper/css';
import 'swiper/css/navigation';
import 'swiper/css/pagination';

<StyledSwiper
  modules={[Navigation, Pagination, Autoplay]}
  pagination={{
    clickable: true,
    dynamicBullets: true,
  }}
  navigation
  spaceBetween={30}
  slidesPerView={3}
  loop='true'
  autoplay={{
    delay: 4000,
    disableOnInteraction: true,
  }}
>
  {carouselData.map((imgData) => {
    return (
      <SwiperSlide key={imgData.id}>
        <CarouselImg imgUrl={imgData.imgUrl} />
      </SwiperSlide>
    );
  })}
</StyledSwiper>;

const StyledSwiper = styled(Swiper)`
  .swiper-button-next {
    color: white;
    --swiper-navigation-size: 30px;
  }

  .swiper-button-prev {
    color: white;
    --swiper-navigation-size: 30px;
  }

  .swiper-pagination-bullet {
    background: white;
  }
`;
```

#

## 화면랜더를 위한 Mockup Data 만들어보기

- 2차 프로젝트에서는 내가 맡은 부분은 백엔드와 통신 부분이 없었고, 재사용이 많은 카드형태의 컴포넌트 작업이 많았다.
- 백엔드에서 작업이 완료되기전에 목데이터로 미리 작업을 한다고도 하여, 간단히 필요한 부분만 만들어서 컴포넌트를 만들어서 재활용 하였다.
- 실제 예약싸이트들은 수많은 데이터들이 들어갈텐데...

![UI](https://user-images.githubusercontent.com/83544570/202533272-bc7bfaf8-f088-4bb0-a886-21a12d38e321.gif)

```jsx
const AirMain = () => {
  const [jejuData, setJejuData] = useState([]);
  const [japanData, setJapanData] = useState([]);
  const [popularData, setPopularData] = useState([]);

  useEffect(() => {
    fetch('/data/tripdata/jejuData.json', {
      method: 'GET',
    })
      .then((res) => res.json())
      .then((data) => {
        setJejuData(data);
      });

    fetch('/data/tripdata/japanData.json', {
      method: 'GET',
    })
      .then((res) => res.json())
      .then((data) => {
        setJapanData(data);
      });

    fetch('/data/tripdata/PopularData.json', {
      method: 'GET',
    })
      .then((res) => res.json())
      .then((data) => {
        setPopularData(data);
      });
  }, []);

  return (
    <>
      <ModalComponent />
      <AirMainContainer>
        <MainBox>
          <AirTripCard
            title='🍊 제주 여행은 언제나 즐거워 🌴'
            data={jejuData}
          />
          <AirTripCard title='🎏 간만에 일본에 가볼까? 🏯' data={japanData} />
          <AirTripCard title='✈️ 인기 노선별 최저가 🚗' data={popularData} />
        </MainBox>
      </AirMainContainer>
    </>
  );
};
```

#

## input 값을 저장하는 방법과 가공하는 방법??

- 이제 input 값들은 const { name, value } = e.target의 속성들을 꺼내어, [name]: value 로 처리해서 넘겨주는 방법은 처리할 수 있게 되었다.
- 목데이터가 저런식으로 있다면, person 3명의 가상의 배열을 만들어서 컴포넌트와 데이터들을 전달을 해야하는데, 불변을 유지하며, 어떤 메서드를 사용하며 할 줄 몰랐다.
- 혼자 해결 못하는 문제에 직면하면서, 동기들에게 도움을 얻어 가상의 배열을 만들 수있었고, 어떻게 찾았으며 공부해가면 알 수 있는지에 대해서도 많이 물어봤던 것같다.
- `new Array를 이용해서 새로운 배열을 만들어, 불변을 유지하며 person 수만큼의 컴포포넌트와 input 입력값을 가공해서 넣어줄 수 있었다.`

![정보](https://user-images.githubusercontent.com/83544570/202711656-d0e396a3-796c-404f-872a-8d2d2995257d.jpg)

```jsx
{
  "originResults": {
    "code": "01023451212",
    "airline": "대한항공",
    "en_airline": "BOEING 789-9",
    "flight_time": "1시간 05분",
    "user_information": {
      "user_name": "홍길동",
      "user_email": "ghdrlfehd@naver.com"
    },
    "person": 3,
    "total_price": 118000,
  }
}

<TabLi>
  {[...new Array(originResults.person)].map((_, idx) => {
    const handlePassengerData = e => {
      const { name, value } = e.target;
       setPassengerData({
        ...passengerData,
          [idx]: { ...passengerData[idx], [name]: value },
      });
    };
  return (
    <TabContentAdult
      key={idx}
      onChange={handlePassengerData}
    >
.....
```

### 🎥 각 페이지별 View

<table>
  <thead>
    <tr>
      <th>
        메인페이지
      </th>
      <th>
        ESG페이지
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546658-d0c71996-a9b8-442d-9f75-5b6d8e1f181a.png">
      </td>
      <td align="center">
          <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546668-7a340397-a975-4c72-814a-fc2712aa13ce.jpg">
      </td>
    </tr>
  </tbody>
</table>
<table>
  <thead>
    <tr>
      <th>
        항공페이지
      </th>
      <th>
        로그인
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546670-cbb90d9f-48aa-4314-afe6-416e5ecb2c75.png">
      </td>
      <td align="center">
          <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546648-cc5bb318-8140-42f6-9b6e-a89846432c57.png">
      </td>
    </tr>
  </tbody>
</table>
<table>
  <thead>
    <tr>
      <th>
        모달페이지
      </th>
      <th>
        로딩페이지
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546674-a3361803-8c5d-4f0c-9a17-221d7bb3fc1d.jpg">
      </td>
      <td align="center">
          <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546671-c30e9cc7-c935-4c2b-9437-86395d88c62c.jpg">
      </td>
    </tr>
  </tbody>
</table>
<table>
  <thead>
    <tr>
      <th>
        리스트페이지
      </th>
      <th>
        예약결제페이지
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
     <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546675-8d41aa39-efb4-4730-96ca-98072b710934.png">
      </td>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184546676-34799bdc-3032-49cd-a688-dfa1f13e7ad0.png">
      </td>
    </tr>
  </tbody>
</table>

#

### 💫 프로젝트 협업 Tool

- GitHub : 각 페이지별 branch 관리.

- Slack : 팀원간의 실시간 소통 창구.

- Trello : 기능 단위로 카드를 생성, Sprint 단위로 진행했는지와 Stand up 미팅 툴로 활용.

- Notion : 회의정리 기록, 오늘의 공유/질문 사항, 현재 진행 사항, blocker 공유, 기능 단위 페이지 셍성 후 공유 및 기록.

<table>
  <thead>
    <tr>
      <th>
        트렐로
      </th>
      <th>
        노션
      </th>
    </tr>
       <tr>
      <th>
        깃허브
      </th>
      <th>
        슬랙
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184545309-14792748-ce97-449d-a619-dc1f60c80590.jpg">      
        </td>
      <td align="center">
        <img width="789" alt=image" src="https://user-images.githubusercontent.com/83544570/184545339-9336d126-243e-4daa-85b1-fb4044844dbd.jpg">      
        </td>
    </tr>
      <tr>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184545347-3833d8a5-a195-49a1-8b1a-d83af5fb4db7.jpg">      
        </td>
      <td align="center">
        <img width="789" alt="image" src="https://user-images.githubusercontent.com/83544570/184545358-21bbb0dc-754b-4b96-b8d3-1acd53719fcb.png">      
        </td>
    </tr>
  </tbody>
</table>

#

### Reference

- 이 프로젝트는 제주패스를 참조하여 학습목적으로 만들었습니다.
- 학습용으로 만들었기 때문에 이 코드를 활용하여 이득을 취하거나 무단 배포할 경우 법적으로 문제될 수 있습니다.
