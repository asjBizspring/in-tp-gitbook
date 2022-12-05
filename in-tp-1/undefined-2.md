# 분석 스크립트 적용 가이드

{% hint style="info" %}
CTS(CTS 전환 데이터가 포함된 일부 메), LOGGER, TAM, ADM(순위 입찰) 앱 사용을 위해 설치되어야 하는 분석스크립트 적용 가이드입니다.&#x20;

기본 스크립트는 분석할 사이트내 필수로 설치하여야 하며, 환경변수 스크립트는 분석이 필요한 항목을 선별하여 설치할 수 있습니다.
{% endhint %}

## **1. (필수) 기본 스크립트** <a href="#1e9a3092-4e6b-4844-ac4f-88589e8cc2c2" id="1e9a3092-4e6b-4844-ac4f-88589e8cc2c2"></a>

기본 스크립트는 웹사이트 분석을 위해 <mark style="color:red;">**전체 페이지에 필수적으로 삽입**</mark>해야 합니다.

프로그래밍 언어로 구현된 대부분의 웹사이트들은 공통 레이아웃을 가지고 있습니다. 공통 레이아웃에는 일반적으로 헤더(탐색 및 메뉴 부분) 또는 푸터(회사 정보, 저작권 정보 등 공통적인 HTML 코드를 포함하고 있는 부분) 같은 공통적인 UI(사용자 인터페이스) 요소들이 포함됩니다.

모든 페이지에 개별적으로 삽입하면 유지 보수에 어려움이 있을 수 있기 때문에, 한 번의 작업으로 전체 페이지에 적용될 수 있도록 <mark style="color:red;">**푸터 파일 내의 \</body> 태그 위쪽에 삽입**</mark>합니다.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

```javascript
<script type="text/javascript">
  (function(b,s,t,c,k){b[k]=s;b[s]=b[s]||function(){(b[s].q=b[s].q||[]).push(arguments)}; var f=t.getElementsByTagName(c)[0],j=t.createElement(c);j.async=true;j.src='//fs.bizspring.net/gp/gp.v.1.0.js';f.parentNode.insertBefore(j,f);})(window,'_gp',document,'script','BSGPObj');
  _gp('프로파일 번호','land');
</script>
```

***

## **2. (선별) 환경변수 스크립트** <a href="#293c9d2c-6a1a-4d23-aac1-ad6c99971af7" id="293c9d2c-6a1a-4d23-aac1-ad6c99971af7"></a>

환경변수 스크립트는 전체 페이지에 적용하지 않으며 <mark style="color:red;">**해당 환경변수의 설정이 필요한 페이지에만 선별적으로 적용**</mark>합니다.

예를 들어, 주문완료에 대한 전환추적을 하고 싶은 경우에는 사용자가 결제를 완료하면 이동되는 페이지(일반적으로 '주문이 완료되었습니다.'라고 결과를 표시하는 페이지)에 삽입합니다.

<mark style="color:red;">**HTML 코드 내에서 (필수)기본 스크립트보다 반드시 위쪽에 위치해야 합니다**</mark><mark style="color:red;">.</mark>

제공되는 환경변수 전체를 적용할 필요는 없으며 <mark style="color:red;">**필요한 환경변수만을 선별적으로 적용하는 것이 가능**</mark>합니다.

환경변수 값에 쌍따옴표(“) 또는 작은따옴표(‘)가 들어갈 수 없습니다.

****

### **2.1 환경변수 간략 요약표** <a href="#7a132172-94b0-46c4-b6f4-98e4162a4dc2" id="7a132172-94b0-46c4-b6f4-98e4162a4dc2"></a>

| \_TRK\_PND | 상품명        |
| ---------- | ---------- |
| \_TRK\_MF  | 상품 카테고리    |
| \_TRK\_OP  | 주문상품명      |
| \_TRK\_OPC | 주문상품코드     |
| \_TRK\_OE  | 주문수량       |
| \_TRK\_OA  | 주문금액       |
| \_TRK\_OAP | 할인전 금액     |
| \_TRK\_SX  | 회원 성별      |
| \_TRK\_AG  | 회원 나이      |
| \_TRK\_IK  | 내부 검색어 전달  |
| \_TRK\_RK  | 고객 ID/고객번호 |
| \_TRK\_CC  | 외부캠페인코드    |
| \_TRK\_IC  | 내부캠페인코드    |

****

### **2.2 상품 조회** <a href="#b8ec68f8-bcf1-4a27-a496-7c20afe8214a" id="b8ec68f8-bcf1-4a27-a496-7c20afe8214a"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분    | 적용 위치     | 환경 변수                                                        |
| ----- | --------- | ------------------------------------------------------------ |
| 상품 조회 | 상품 상세 페이지 | <p>_TRK_PI </p><p>_TRK_PN </p><p>_TRK_PND </p><p>_TRK_MF</p> |

```javascript
<script type="text/javascript">
  _TRK_PI = "PDV";
  _TRK_PN = "상품코드";
  _TRK_PND = "상품명";
  _TRK_MF = "브랜드명";
</script>
```

****

### **2.3 장바구니 담기** <a href="#ceadfe18-8908-4750-bc05-2518f9b9b701" id="ceadfe18-8908-4750-bc05-2518f9b9b701"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분      | 적용 위치     | 환경 변수                                                     |
| ------- | --------- | --------------------------------------------------------- |
| 장바구니 담기 | 상품 상세 페이지 | <p>_TRK_PI <br>_TRK_PN </p><p>_TRK_PND </p><p>_TRK_MF</p> |

\
클릭 이벤트는 PC 버전의 경우에는 mousedown으로 Mobile 버전의 경우에는 touchstart로 적용합니다.

```javascript
<script type="text/javascript">
  document.querySelectorAll("장바구니담기 버튼 선택자").forEach(function(element) {
    element.addEventListener("mousedown 또는 touchstart", function() {
      _TRK_PI = "SCI";
      _TRK_PN = "상품코드";
      _TRK_PND = "상품명";
      _TRK_MF = "브랜드명";
      _gp("프로파일 번호","conv");
    });
  });
</script>
```

\
상품조회 스크립트를 적용하여 해당 페이지에 \_TRK\_PN, \_TRK\_PND, \_TRK\_MF 변수가 이미 설정되어 있는 경우에는 \_TRK\_PI 변수만 설정합니다.

```javascript
<script type="text/javascript">
  document.querySelectorAll("장바구니담기 버튼 선택자").forEach(function(element) {
    element.addEventListener("mousedown 또는 touchstart", function() {
      _TRK_PI = "SCI";
      _gp("프로파일 번호","conv");
    });
  });
</script>
```

****

### **2.4 주문 완료** <a href="#490e86ea-6cb4-4bd9-8e2f-5c15b6889c20" id="490e86ea-6cb4-4bd9-8e2f-5c15b6889c20"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분 | 적용 위치     | 환경 변수                                                                                                      |
| -- | --------- | ---------------------------------------------------------------------------------------------------------- |
| 주문 | 주문 완료 페이지 | <p>_TRK_PI _</p><p>TRK_ODN </p><p>_TRK_OA </p><p>_TRK_OE </p><p>_TRK_OP </p><p>_TRK_OPC</p><p>_TRK_OAP</p> |

\
주문수량, 주문금액의 변수는 숫자만 호출합니다.

```javascript
<script type="text/javascript">
  _TRK_PI = "ODR";
  _TRK_ODN = "주문번호";
  _TRK_OA = "주문금액";
  _TRK_OE = "주문수량";
  _TRK_OP = "주문상품명";
  _TRK_OPC = "주문상품코드";
  _TRK_OAP = "할인전금액";
</script>
```

\
2개 이상 상품을 구매할 경우 세미콜론으로 구분하여 변수를 호출합니다.

**예시) 동시에 A 상품 300원 \* 10개 + B 상품 200원 \* 4개 + C 상품 500원 \* 1개를 주문한 경우**

```
<script type="text/javascript">
  _TRK_PI = "ODR";
  _TRK_ODN = "주문번호";
  _TRK_OA = "3000;800;500";
  _TRK_OE = "10;4;1";
  _TRK_OP = "A의 상품명;B의 상품명;C의 상품명";
  _TRK_OP = "A의 상품코드;B의 상품코드;C의 상품코드";
  _TRK_OAP = "2000;400;300";
</script>
```

****

### **2.5 특정 카테고리** <a href="#d2fc39e4-a067-4e09-a9da-0e877808c714" id="d2fc39e4-a067-4e09-a9da-0e877808c714"></a>

| 구분      | 적용 위치       | 환경 변수     |
| ------- | ----------- | --------- |
| 특정 카테고리 | 카테고리 분석 페이지 | \_TRK\_CP |

```javascript
<script type="text/javascript">
  _TRK_CP = "소속 카테고리명 변수";
</script>
```

****

### **2.6 회원 가입** <a href="#a55bd6b0-301a-4438-b9e7-2f1c9f9363bc" id="a55bd6b0-301a-4438-b9e7-2f1c9f9363bc"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분    | 적용 위치        | 환경 변수                                      |
| ----- | ------------ | ------------------------------------------ |
| 회원 가입 | 회원 가입 완료 페이지 | <p>_TRK_PI</p><p>_TRK_SX</p><p>_TRK_AG</p> |

```javascript
<script type="text/javascript">
  _TRK_PI = "RGR";
  _TRK_SX = "";
  _TRK_AG = "";
</script>
```

****

### **2.7 로그인** <a href="#07d74fa1-da50-4732-9025-94663ad22299" id="07d74fa1-da50-4732-9025-94663ad22299"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분  | 적용 위치      | 환경 변수                                       |
| --- | ---------- | ------------------------------------------- |
| 로그인 | 로그인 완료 페이지 | <p>_TRK_PI </p><p>_TRK_SX</p><p>_TRK_AG</p> |

```javascript
<script type="text/javascript">
  _TRK_PI = "LIR";
  _TRK_SX = “”;
  _TRK_AG = “”;
</script>
```

****

### **2.8 회원특성 분류** <a href="#fd33ad25-7e4a-493e-9984-961241c1a43b" id="fd33ad25-7e4a-493e-9984-961241c1a43b"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분 | 적용 위치 | 환경 변수      |
| -- | ----- | ---------- |
| 성별 |       | \_TRK\_SX  |
| 연령 |       | \_TRK\_AG  |

```
<script type="text/javascript">
  _TRK_SX = “”; // M, F, U
  _TRK_AG = “”; // A ~ G 
</script>
```

{% hint style="warning" %}
**참고**

**\_TRK\_PI의 경우 아래와 같이 코드값으로 정의**

회원 가입 완료 페이지는 RGR, 로그인 성공시 LIR 그외는 2.11 참고

**\_TRK\_SX의 경우 아래와 같이 코드값으로 정의**

남성은 M, 여성은 F, 그 외는 U

**\_TRK\_AG의 경우 A\~Z 알파벳 코드값으로 정의**
{% endhint %}

| 속성 | 속성명    | 데이터 범위  |
| -- | ------ | ------- |
| A  | 10대 이하 | 0\~19   |
| B  | 20대    | 20\~29  |
| C  | 30대    | 30\~39  |
| D  | 40대    | 40\~49  |
| E  | 50대    | 50\~59  |
| F  | 60대    | 60\~69  |
| G  | 70대 이상 | 70\~150 |

****\
**예시) level B(20대) 의 여성이 회원가입 완료하였을 경우**

```javascript
<script type="text/javascript">
  _TRK_PI = “RGR”; 
  _TRK_SX = “F”;
  _TRK_AG = “B”;
</script>
```

****

### **2.9 내부 검색어** <a href="#500e97e1-427d-45c4-abfb-8eae84d4a123" id="500e97e1-427d-45c4-abfb-8eae84d4a123"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

| 구분     | 적용 위치     | 환경 변수     |
| ------ | --------- | --------- |
| 내부 검색어 | 검색 완료 페이지 | \_TRK\_IK |

```javascript
<script type="text/javascript">
  _TRK_IK = "검색어 변수"; 
</script>
```

****

### **2.10 \_TRK\_ENV\_XXX 변수 정의** <a href="#49e26757-2e2b-46f0-842f-f84821efb11e" id="49e26757-2e2b-46f0-842f-f84821efb11e"></a>

> 환경변수 스크립트는 HTML 코드 내에서 (필수) <mark style="color:red;">기본 스크립트보다 반드시 위쪽에 위치</mark>해야 합니다.

****\
****정의되어 있는 환경변수 이외에 사용할 경우 \_TRK\_ENV\_ 뒤에 이름(XXX) 정의해주고 값을 할당

```javascript
<script type="text/javascript">
  _TRK_ENV_XXX = "값";
</script>
```

****\
**예시) 환경변수가 \_TRK\_ENV\_PDA1이고 값이 “1”인 경우**

```javascript
<script type="text/javascript">
  _TRK_ENV_PDA1 = “1”; 
</script>
```

| ENV 변수            | 용도            |
| ----------------- | ------------- |
| \_TRK\_ENV\_PDA1  | 상품 속성 #1      |
| \_TRK\_ENV\_PDA2  | 상품 속성 #2      |
| \_TRK\_ENV\_PDA3  | 상품 속성 #3      |
| \_TRK\_ENV\_PDA4  | 상품 속성 #4      |
| \_TRK\_ENV\_PDA5  | 상품 속성 #5      |
| \_TRK\_ENV\_PDA6  | 상품 속성 #6      |
| \_TRK\_ENV\_PDA7  | 상품 속성 #7      |
| \_TRK\_ENV\_PDA8  | 상품 속성 #8      |
| \_TRK\_ENV\_PDA9  | 상품 속성 #9      |
| \_TRK\_ENV\_PDA10 | 상품 속성 #10     |
| \_TRK\_ENV\_CPN   | 쿠폰 사용         |
| \_TRK\_ENV\_CPND  | 쿠폰 코드         |
| \_TRK\_ENV\_AIC   | 장바구니 추가 금액    |
| \_TRK\_ENV\_ACA   | 장바구니 삭제 금액    |
| \_TRK\_ENV\_IKR   | 내부검색어 검색결과 여부 |
| \_TRK\_ENV\_IKP   | 내부검색어 검색결과수   |

****

### **2.11 \_TRK\_PI 코드값** <a href="#a8ba9179-5db9-4af6-b53d-425a572aa16c" id="a8ba9179-5db9-4af6-b53d-425a572aa16c"></a>

| 코드값  | 용도          |
| ---- | ----------- |
| RGR  | 회원가입        |
| LIR  | 로그인         |
| LGO  | 로그아웃        |
| PLV  | 상품 리스트 페이지  |
| PDV  | 상품 상세 조회    |
| PRV  | 상품 리뷰 조회    |
| ATF  | 관심상품에 추가    |
| SCI  | 장바구니에 추가    |
| SCO  | 장바구니에서 삭제   |
| OCV  | 장바구니 페이지 조회 |
| OCF  | 체크아웃        |
| ODR  | 주문(구매)      |
| WPR  | 리뷰 작성       |
| FOD  | 첫 구매 여부     |
| CODR | 구매 취소       |
