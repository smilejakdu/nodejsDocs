# 카카오 map

[https://apis.map.kakao.com/web/documentation/#drawing](https://apis.map.kakao.com/web/documentation/#drawing)

위의 문서를 참고하면 됩니다.

src/\_app.tsx

```sql
import type { AppProps } from "next/app";
import axios from "axios";
import Layout from "@/layouts/Layout";
import {ThemeProvider} from "@mui/system";
import theme from "@/styles/theme";
import {RecoilRoot} from "recoil";
import Script from "next/script";

function App({ Component, pageProps }: AppProps) {
  axios.defaults.withCredentials = true

  return(
      <div>
        <ThemeProvider theme={theme}>
          <Script src="<https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js>" strategy="beforeInteractive"/>
          <Script src={`//dapi.kakao.com/v2/maps/sdk.js?appkey=${process.env.REACT_KAKAO_JS_KEY}&autoload=false`}
                  strategy="beforeInteractive"/>
          <Script src="<https://t1.kakaocdn.net/kakao_js_sdk/2.7.1/kakao.min.js>"
                  integrity="sha384-kDljxUXHaJ9xAb2AzRd59KxjrFjzHa5TAoFQ6GbYTCAG0bjM55XohjjDT7tDDC01"
                  crossOrigin="anonymous"/>
          <Script src="<https://developers.kakao.com/sdk/js/kakao.js>" strategy="beforeInteractive"/>
          <RecoilRoot>
            <Layout>
              <Component {...pageProps} />
            </Layout>
          </RecoilRoot>
        </ThemeProvider>
      </div>
  )
}

export default App;

```

src/pages/index.tsx

```sql
import React from 'react';
import KakaoMap from '../components/KakaoMap'; // 경로는 실제 위치에 따라 조정해야 합니다.

const MainPage = () => {
  const locations = [
    { lat: 37.514575, lng: 127.0495556 },
    { lat: 37.507374, lng: 127.057203 },
    { lat: 37.512021, lng: 127.058941 }
  ];
  return (
    <div>
      <KakaoMap locations={locations} />
    </div>
  );
};

export default MainPage;

```

src/components/KakaoMap.tsx

```sql
import React, { useEffect } from "react";
import "react-kakao-maps-sdk";

const KakaoMap = ({ locations }: { locations: Array<{lat: number, lng: number}> }) => {
  useEffect(() => {
    kakao.maps.load(() => {
      if (!locations.length) return; // 위치 데이터가 없으면 종료

      const container = document.getElementById("map");
      const options = {
        center: new kakao.maps.LatLng(locations[0].lat, locations[0].lng), // 첫 번째 위치를 중심으로 설정
        level: 3,
      };
      const map = new kakao.maps.Map(container as HTMLElement, options);

      // 여러 위치에 대한 마커 생성
      locations.forEach(location => {
        const position = new kakao.maps.LatLng(location.lat, location.lng);
        const marker = new kakao.maps.Marker({
          map: map,
          position: position,
        });
        marker.setMap(map);
      });
    });
  }, [locations]); // locations 배열이 변경될 때마다 효과 실행

  return (
    <div style={{ position: "relative", width: "100%", height: "100vh" }}>
      <div id="map" style={{ width: "100%", height: "100%" }}></div>
    </div>
  );
};

export default KakaoMap;

```
