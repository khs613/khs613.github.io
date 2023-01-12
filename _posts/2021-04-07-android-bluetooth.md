---
date: 2021-04-07
title: "[Android] Bluetooth Device 목록 가져오기"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
## 🔮 Bluetooth Device 목록 가져오기 🔫

안드로이드 기기에서 Bluetooth device 목록을 가져오고자 한다. 안드로이드에서는 Bluetooth 정보와 기기 검색 및 연결 등의 기능들을 수행할 수 있다. 오늘은 bluetooth 기기 목록을 가져오는 동작을 살펴보려 한다.  
&nbsp;  

---

### 🟣 권한 설정  
- 매니페스트 파일에 블루투스 권한 추가  

```
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
```
{: .notice--primary}  

&nbsp;  

### 🟣 BluetoothAdapter  
- [BluetoothAdapter](https://developer.android.com/reference/android/bluetooth/BluetoothAdapter) 를 통해 장치 검색, 페어링 된 목록 확인, 연결 요청 등 기본적인 Bluetooth 작업을 수행할 수 있다.  
- getBondedDevices() : BluetoothDevice의 모든 페어링 된 장치를 가져온다.  
- 장치의 이름, MAC 주소 등을 가져올 수 있다.  

``` java
BluetoothAdapter bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();
Set<BluetoothDevice> pairedDevices = bluetoothAdapter.getBondedDevices();

if (pairedDevices.size() > 0) {
    for (BluetoothDevice device : pairedDevices) {
        Log.d(TAG, device.getName());
        Log.d(TAG, device.getAddress());
    }
}
```
{: .notice--primary}  

&nbsp;  

위 소스코드를 통해 현재 기기와 블루투스 페어링 된 장치의 정보를 얻을 수 있다. BluetoothAdapter 를 통해 다양한 기능을 제공할 수 있으므로 추가 사항은 다음에 더 사용하고자 한다.  

&nbsp;  
&nbsp;  
[참고]  
<https://m.blog.naver.com/PostView.nhn?blogId=awesomedev&logNo=220679754787&proxyReferer=https:%2F%2Fwww.google.com%2F>
