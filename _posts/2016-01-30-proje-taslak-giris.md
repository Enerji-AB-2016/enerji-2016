---
layout: post
title: Proje Sayfası Oluşturmaya Giriş
date: 2016-01-30 12:00:00 +02:00
---

mydata=read_excel('enerjiuretimi.xls')
ggplot(data=mydata)+geom_line(aes(x=Yil,y=Komur))
mydata2=mydata %>%
  mutate(Toplam_komur=((Toplam*Komur)/100))%>%
  mutate(Toplam_sivi=((Toplam*Sivi_yakitler)/100))%>%
  mutate(Toplam_gaz=((Toplam*Dogalgaz)/100))%>%
  mutate(Toplam_hidrolik=((Toplam*Hidrolik)/100))%>%
  mutate(Toplam_alterenerji=((Toplam*Alter_Enerji)/100))%>%
  select(Yil,Toplam_komur,Toplam_sivi,Toplam_gaz,Toplam_hidrolik,Toplam_alterenerji)%>%
  print(n=Inf)
ggplot(data=mydata2,aes(x=Yil))+geom_line(aes(y=Toplam_komur),color=1)
+ylab('Üretilen Elektrik Miktarı(GWh)')+ geom_line(aes(y=Toplam_sivi),color=2)
+geom_line(aes(y=Toplam_gaz),color=3)+geom_line(aes(y=Toplam_hidrolik),color=4)
+geom_line(aes(y=Toplam_alterenerji),color=5)

```{r}
print("R ile Veri Analizi Proje Sayfası")
```