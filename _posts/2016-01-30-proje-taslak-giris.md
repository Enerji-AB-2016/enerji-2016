---
layout: post
title: Proje Sayfası 
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
  
mydata3=mydata %>%
  select(Toplam,Yil)

testdata=melt(mydata2,id="Yil")
ggplot(data=testdata,aes(x=Yil,y=value,colour=variable))+geom_line()+ ylab('Üretilen Elektrik Miktarı(GWh)')+ggtitle('Türkiyede Yıllara Göre Üretilen Elektrik Miktarının Sektörel Dağılımı')

testdata2=melt(mydata3,id="Yil")
ggplot(data=testdata2,aes(x=Yil,y=value,colour=variable))+geom_bar(stat = "identity")+ ylab('Üretilen Elektrik Miktarı(GWh)')+ggtitle('Türkiyede Yıllara Göre Üretilen Elektrik Miktarı')+scale_fill_discrete(name="Title")

mydata4=mydata2 %>%
  mutate(Toplam_Komur=sum(Toplam_komur))%>%
  mutate(Toplam_Sivi=sum(Toplam_sivi))%>%
  mutate(Toplam_Gaz=sum(Toplam_gaz))%>%
  mutate(Toplam_Hidrolik=sum(Toplam_hidrolik))%>%
  mutate(Toplam_Alterenerji=sum(Toplam_alterenerji))%>%
  select(Toplam_Komur,Toplam_Sivi,Toplam_Gaz,Toplam_Hidrolik,Toplam_Alterenerji)
mydata5=mydata3 %>%
  select(Yil)
