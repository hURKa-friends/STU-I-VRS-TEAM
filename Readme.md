# Malý dron ovládaný pomocou IMU jednotky
Cieľom tímového zadania je vytvorenie systému na ovládanie malého drona Tello pomocou príkazov získaných z IMU jednotky. Dron má reagovať na pohyby, respektíve náklony ovládacej jednotky (napríklad pri náklone doprava sa bude pohybovať doprava).

IMU jednotka pozostáva zo senzorov, ktoré sú prítomné na senzorickej doske X-NUCLEO-IKS01A1, kokrétne zo:
- Senzora LSM6DS0 (MEMS 3D akcelerometer + 3D gyroskop)
- Senzora LIS3MDL (MEMS 3D magnetometer)

Pre vypracovanie zadania budeme potrebovať:
- IMU jednotku (Senzorickú dosku IKS01A1) (aspoň 2ks)
- Doplnkové vstupy (tlačítka, potenciometre, ...)
  (Kolískový spínač pre ARM/DISARM, Active/Deactivate riadenia(aspoň 2ks), možno potenciometer pre ovládanie výšky)
- STM32 F303K8 (aspoň 2ks)
- Tello dron (máme už 2ks)
- Náhradné vrtuľky pre Tello dron (1 už zlomil hlavný dronista Filip Kuruc)

## Štruktúra projektu
IMU dáta ako napríklad náklony v jednotlivých osiach budú snímané senzormi IMU jednotky. Nasnímané dáta budú periodicky vyčítavané cez I2C zbernicu do STM32. STM32 bude ďalej spracúvať doplnkové vstupy pre ovládanie ostatných funkcií drona ako napríklad ARM, DISARM, výška letu drona a iné. Výstupom spracovania dát budú konkrétne príkazy a hodnoty pre ovládanie drona. Tieto dáta budú cez USART komunikáciu posielané do počítača, kde cez Tello Python API budú preposielané cez bezdrôtové WiFi spojenie do drona.
<p align="center">
    <img src="https://github.com/hURKa-friends/STU-I-VRS-TEAM/blob/master/docs/drawio/StrukturaZadania.drawio.png" width="850" title="Project layout scheme">
</p>

## Deľba práce - Hlavné zodpovednosti
Prakticky budeme na úlohách rozdelený podľa potreby, ale za jednotlivé segmenty zadania bude zodpovednosť pripadať nasledovným spôsobom:

- HW komunikačné knižnice I2C, SPI, USART - Marek Sýkorka, Tomáš Čvirik
- Spracovanie príjmaných senzorových dát - Denis Práznovský
- Implementácia Python API - Filip Kuruc