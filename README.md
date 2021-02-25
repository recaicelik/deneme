# Kingtech LCD için HX8394F Sürücü Kodu Yaması
## Amaç

Bu belge, Quectel SC66 modülünün Android platformunda hx8394f sürücüsü ile Kingtech ekran panelini çalıştırmak için Ekran Seri Arayüzünün (DSI) nasıl kullanılacağını açıklamaktadır.  

- Aşağıda daha önceden hazırlanmış Kingtech LCD'sini süren hx8394f sürücü kodlarının sisteme entegresi açıklanmıştır.
- Yama dosyalarının nasıl yapılacağını açıklamamaktadır. Bunun için patch içindeki ekran driver geliştirme kılavuzuna bakınız.
- ## Patch Dosyaları

- dsi-panel-hx8394f-720p-video.dtsi
- mdss_dsi.c
- sdm660-mdss-panels.dtsi
- sdm660-mtp.dtsi

## Dosyaların Yama Aşaması

Aşağıda verilen kopyalama işlemleri sırasıyla yapıldıktan sonra Kingtech ekran panelini süren hx8394f sisteme entegre olacaktır.

1. sdm660-mdss-panels.dtsi dosyasını aşağıdaki dizinde aynı isimle olan dosyayla değiştirin.

```sh
kernel/msm-4.4/arch/arm64/boot/dts/qcom/
```

2. sdm660-mtp.dtsi dosyasını aşağıdaki dizinde aynı isimle olan dosyayla değiştirin.

```sh
kernel/msm-4.4/arch/arm/boot/dts/qcom/
```

3. dsi-panel-hx8394f-720p-video.dtsi dosyasını aşağıdaki dizinde aynı isimle olan dosyayla değiştirin.

```sh
kernel/msm-4.4/arch/arm/boot/dts/qcom/
```

4. mdss_dsi.c dosyasını aşağıdaki dizinde aynı isimle olan dosyayla değiştirin.

```sh
kernel/msm-4.4/drivers/video/fbdev/msm/
```

## Derleme Aşaması

Dosyaları var olan dosyalarla değiştirdikten sonra boot.img dosyasının tekrar derlenmesi gerekmektedir. Aşağıda verilen 
komutları sırasıyla çalıştırdıktan sonra yeni boot.img dosyası oluşacaktır.

```sh
source build/envsetup.sh
lunch sdm660_64-userdebug
make bootimage
```

## Boot.img Dosyasını Yükleme Aşaması

Yukarıdaki işlemler yapıldıktan sonra oluşan yeni boot.img dosyasının Quectel SC66 Modülüne atılması gerekmektedir. Bunun için aşağıdaki komutlar sırasıyla çalıştırılmalıdır.

```sh
adb reboot bootloader
fastboot flash boot_a <path to boot.img>
fastboot flash boot_b <path to boot.img>
fastboot reboot
```

