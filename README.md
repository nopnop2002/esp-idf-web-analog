# esp-idf-web-analog
This project is a demonstration of __real-time visualization of data__ via a web browser.   
The purpose of this project is to introduce a library that can __visualize data in real time__.   
Use the ADC value as the data to display.   
   
ESP32 has two ADCs, ADC1 and ADC2.   
You can use ADCs to convert analog values to digital values.   
The analog values change dynamically and are suitable for this demonstration.

![web-meter](https://user-images.githubusercontent.com/6020549/164379601-68aaf0e3-f50c-4776-8de1-216ce94d63df.jpg)
![web-horizontal](https://user-images.githubusercontent.com/6020549/164379617-143ab49b-af77-4cfe-9d65-6f213d724d28.jpg)
![web-vertical](https://user-images.githubusercontent.com/6020549/164379627-dac0078c-0a25-45bb-941f-d5588c87413b.jpg)
![Chartjs](https://user-images.githubusercontent.com/6020549/164872690-abad13da-563f-44a4-b579-b4dd25598c33.jpg)
![Plotly](https://user-images.githubusercontent.com/6020549/164872660-be85b191-c0ed-4f06-b04c-1ba6c020d6d7.jpg)
![Epoch](https://user-images.githubusercontent.com/6020549/164948839-9a6997b3-6c40-441c-841e-be1a32b36890.jpg)

# ADC Attenuation   
This project uses ADC_ATTEN_DB_11(11dB) for attenuation.   
11dB attenuation (ADC_ATTEN_DB_11) gives full-scale voltage 3.9V.   
But the range that can be measured accurately is as follows:   
- Measurable input voltage range for ESP32 is 150 mV ~ 2450 mV.   
- Measurable input voltage range for ESP32S2 is 0 mV ~ 2500 mV.   
- Measurable input voltage range for ESP32S3 is 0 mV ~ 3100 mV.   
- Measurable input voltage range for ESP32C3 is 0 mV ~ 2500 mV.   


# Software requirements
esp-idf v4.4 or later.   
This is because this version supports ESP32-C3.   


# How to Install

- Install websocket component   
I used [this](https://github.com/Molorius/esp32-websocket) component.   
This component can communicate directly with the browser.   
It's a great job.   

```
git clone https://github.com/nopnop2002/esp-idf-web-analog
cd esp-idf-web-analog/RadialGauge/
git clone https://github.com/Molorius/esp32-websocket components/websocket
```


- Configuration of esp-idf
```
idf.py set-target {esp32/esp32s2/esp32s3/esp32c3}
idf.py menuconfig
```
![config-top](https://user-images.githubusercontent.com/6020549/164379960-58350b2d-17d4-48b5-84d1-615ff037242a.jpg)
![config-app](https://user-images.githubusercontent.com/6020549/164379982-149e4044-7889-4755-813e-0185fd082c9b.jpg)



Set the information of your access point.

![config-wifi-1](https://user-images.githubusercontent.com/6020549/164383151-ea783d1c-406b-42d5-9767-2e6911be9b2f.jpg)

You can use mDNS.   
![config-wifi-2](https://user-images.githubusercontent.com/6020549/164380164-8be36ca2-a5c4-402e-b83d-d21513e66c55.jpg)

Set the information of gpio for analog input.
![config-adc-1](https://user-images.githubusercontent.com/6020549/164380386-c6dffeb8-9bdd-46bf-8e55-9c4ecef16090.jpg)

It is possible to monitor 3 channels at the same time.   
![config-adc-2](https://user-images.githubusercontent.com/6020549/164380399-fe125c4f-006d-48cb-9e4e-f104c389b8b5.jpg)

Analog input gpio for ESP32 is GPIO32 ~ GPIO39. 12Bits width.   
Analog input gpio for ESP32S2 is GPIO01 ~ GPIO10. 13Bits width.   
Analog input gpio for ESP32S3 is GPIO01 ~ GPIO10. 12Bits width.   
Analog input gpio for ESP32C3 is GPIO00 ~ GPIO04. 12Bits width.   

- Connect ESP32 and Analog source using wire cable   
I used a variable resistor for testing.
```
ESP32C3 3.3V   -------------------------- Ra of variable resistor


ESP32C3 GPIO00 -----------------------+-- Vout of variable resistor
                                      |
                 R1      R2      R3   |
ESP32C3 GND    --^^^--+--^^^--+--^^^--+
                      |       |
                      |       |
ESP32C3 GPIO01 -------+       |
                              |
                              |
ESP32C3 GPIO02 ---------------+


ESP32C3 GND    -------------------------- Rb of variable resistor
```

- Flash firmware
```
idf.py flash monitor
```

- Launch a web browser   
Enter the following in the address bar of your web browser.   

```
http:://{IP of ESP32}/
or
http://esp32-server.local/
```

# WEB Pages
WEB pages are stored in the html folder.   
You can change it as you like.   
