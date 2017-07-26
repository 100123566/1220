# 2017. 07. 13
## nRF52832 보드에 Bluetooth 통신 테스트
1. 테스트 버전은 SDK 12.1 버전으로 진행
2. 여러가지 예제 중에 Bluetooth 통신으로 LED 제어를 테스트
3. 소스 디렉토리: \nRF5_SDK_12.1.0_0d23e2a\examples\ble_peripheral\experimental_ble_app_blinky\pca10040\s132\arm5_no_packs
4. 프로젝트 파일을 열어서 기본 설정을 해줌(07.12에서 언급한 내용 참조)
5. 통신 대상은 스마트폰(Nordic 제품 테스트를 위해 예제 테스트용 App을 지원해 줌)
![project file image](images/01.png)

# 컴파일 및 다운로딩
## 예제 소스를 컴파일한 다음 보드에 다운 로딩
1. 별도로 라이브러리나 API를 추가 할 필요 없이 바로 컴파일 가능
2. 본 SDK는 여러 버전의 보드를 지원해 줌으로서 프로젝트 파일을 반드시 정확하게 확인해야 됨
3. 현재까지 확인 된 내용은 모든 예제 소스는 pca10040\s132\arm5_no_packs에 있는 프로젝트 버진이 현재 사용중인 nRF52832에 해당 됨
4. 문제 없이 보드에 다운로딩은 완료 하면 보드에 LED1이 켜져 있음

# 앱 설치
## Nordic 에서 이미 완성된 앱을 설치(Android 기반)
1. 구글 마켓에 들어가서 nrf를 검색
2. 테스트에 필요한 앱은 다음과 같음:
    - nRF Blinky(LED 제어용 앱)
    - nRF Connect(Bluetooth 연결 확인 앱)
    - nRF Toolbox(기타 기능들을 모움 앱)
3. 세 개의 앱을 찾아서 다운로드 및 설치

# Bluetooth 페이링 테스트
## 보드와 스마트폰 간의 Bluetooth 통신을 확인
1. 설치된 nRF Connect 실행
2. 앱 실행되면 바로 디바이스 스캔으로 되어 있음
3. 스캔된 목록에서 개발 보드를 찾아 Connect를 클릭(통상적으로 프로젝트 이름으로 디바이스 이름이 나타나게 됨. 예:Nordic_Blinky)
4. Connect 된 상태라면 화면에서 보드에 기본적인 내용을 확인할 수 있음(이때 보드에서 기존 LED1이 LED2로 변경됨, 연결 성공 상태를 나타냄)
![project file image](images/02.png)

# Bluetooth 통신 기반 LED 제어 테스트
## 엡에서 보드에 있는 LED를 제어 테스트, 보드에 있는 버튼으로 앱에 신호 송신 테스트를 진행
1. 보드에 다운로딩된 Firmware 소스는 변경 하지 않음
2. 설치된 nRF Blinky 실행
3. 앱 화면 하단에 Connect 버튼 클릭 하여 디바이스와 Bluetooth 통신을 시작
4. 성공적으로 Conncet 되었으면 On 버튼을 클릭하면 보드에 LED3가 켜짐(앱에 전구 이미지가 노랑색으로 변경하여 LED가 켜졌음을 알려줌)
![LED ON](images/03.png)
5. 다시 OFF 버튼 클릭하면 LED3가 껴지게 되고 화면에 전구 이미지도 다시 원래데로 됨
6. 보드에 Button1을 클릭하면 앱 화면 배경색이 노랑색으로 변경(보드에 버튼으로 스마트폰에게 신호를 보내 줌)
![BUTTON CLICK](images/04.png)

# 문제점 및 미확인 된 내용
1. SDK 버전의 정확성을 확인 필요
2. Bluetooth 예제 소스 중 기타 기능들 테스트 안되는 원인 파악이 필요
3. 소스 코드에 설정 된 메소드들을 보드의 데이터 시트와 매핑이 필요
4. 예제 소스 변형 하여 작동 및 테스트가 필요

## -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-

# 2017. 07. 14
## MDK를 이용한 Bluetooth 통신 데이터 송신
1. MDK를 사용하기 위해 먼저 화경 Setup를 진행
2. Nordic 홈페이지에서 nRFgoStudio 다운 및 설치
3. 주소: https://www.nordicsemi.com/eng
4. 상단 메뉴 Products 클릭  
![going to products menu](images/0714_01.png)
5. 왼쪽 메뉴에서 BLUETOOTH LOW ENERGY 클릭  
![going to BLE menu](images/0714_02.png)
6. 진입한 후 첫번째 표(nRF52 Series)에서 nRF52832 클릭  
![select nRF52832](images/0714_03.png)
7. 진입한 화면에 텝에서 DOWNLOADS 클릭  
![select donwloads](images/0714_04.png)
8. 내용 중에서 하단부분에 있는 nRFgo Studio를 선택하여 다운 및 설치(본인 OS 환경에 따라 선택)  
![select donwloads](images/0714_05.png)

## nRFgo Studio 환경 설정 및 Softdevice HEX 파일 다운로딩
1. 설치된 nRFgo Studio를 실행
2. 개발 보드를 USB로 PC와 연결
3. 연결된 상태라면 nRFgo Studio에 왼쪽 Device Manager에서 디바이스를 확인할 수 있음  
![select device](images/0714_06.png)
4. 해당 보드를 클릭하면 오른쪽에서 기본 내용을 확인할 수 있음  
![select device2](images/0714_07.png)
5. Erase all를 클릭하면 기존에 있는 Firmware를 지울 수 있음
6. 오른쪽 화면에서 Program SoftDevice 탭을 선택  
![select program softdevice tab](images/0714_08.png)
7. Browse를 클릭하여 SDK에 제공한 softdevice의 HEX 파일을 선택
8. 해당 HEX 파일 경로: \SDK폴더\components\softdevice\s132\hex
- 주의사항: 현재 테스트된 SDK 버전은 12.1이며, 보드 종류는 s132이고, firmware 프로젝트도 반드시 같은 버전으로 선택
9. SoftDevice의 HEX 파일을 다운로딩 되면 이제 firmware를 다시 보드에 다운로딩
10. 본 예제는 nRF Toolbox에서 제공한 HRM 및 RSC 두개를 테스트
11. 예제 소스는 SDK폴더 중 \examples\ble_peripheral\ble_app_hrs\pca10040\s132\arm5_no_packs 에서 프로젝트 파일 선택
12. 프로젝트에 main.c 파일을 열어서 컴파일한 뒤 다운로딩을 진행 하면 됨(소스 다운로딩은 07.12에서 언급된 내용 참조)

## 프로그램 테스트
1. 스마트폰에서 기존 설치된 nRF Connect를 실행
2. 개발 보드를 선택하여 Connect를 진행(디바이스 이름은 기본적으로 해당 프로젝트 이름과 동일, 예:Nordic_HRM)
3. Conncet가 성공적으로 이루어 지면 해당 보드에 기본 정보를 확인할 수 있음
4. 다시 nRF Toolbox로 진입 후 HRM 기능을 선택
5. 화면 밑에 Connect를 클릭하여 해당보드와 연결을 진행
6. 연결 성공되면 SoftDevice에 미리 만들어진 데이터가 보드로부터 스마트폰까지 Bluetooth로 전송 진행  
![Connected device and sending data](images/0714_09.png)
7. 화면에서 전송된 데이터를 확인할 수 있고, 같은 방법으로 RSC 기능을 테스트
8. SoftDevice의 HEX 파일은 미이 다운로딩이 되어 있어 다른 기능 테스트할 때는 다시 다운로딩할 필요 없음
9. RSC 프로젝트 위치는 SDK에 \examples\ble_peripheral\ble_app_rscs\pca10040\s132\arm5_no_packs 있음
10. main.c 파일을 열어서 컴파일한 뒤 다운로딩을 진행
11. 기존 방식과 같게 먼저 nRF Connect에서 연결 확인한 뒤 다시 nRF Toolbox 기능중 RSC를 선택
12. 화면 밑에서 Connect를 클릭하여 보드와 연결
13. 연결 성공한 뒤 SoftDevice에서 미이 만들어진 데이터가 Bluetooth 기반으로 스마트폰에게 전송 하는 것을 확인  
![Connected device and sending data](images/0714_10.png)

## 문제점 및 의문 사항
1. 앱 실행중 간혹 응답없음으로 되버리는 현상(Bluetooth 서비스에서 문제 있다고 예상)
2. SoftDevice의 데이터를 수정 가능 여부