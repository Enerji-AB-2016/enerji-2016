---
layout: post
title: Proje Sayfası 
date: 2016-01-30 12:00:00 +02:00
---

  1970-2013 Yılları Arası Üretilen Sektörel Elektrik Miktarının Amalizi
  
  
  mydata=read_excel('enerjiuretimi.xls')
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
  
  phidata=mydata %>%
  mutate(ortalama_komur=sum(Komur)/44)%>%
  mutate(ortalama_sivi=sum(Sivi_yakitler)/44)%>%
  mutate(ortalama_gaz=sum(Dogalgaz)/44)%>%
  mutate(ortalama_hidrolik=sum(Hidrolik)/44)%>%
  mutate(ortalama_alter=sum(Alter_Enerji)/44)%>%
  select(ortalama_alter,ortalama_hidrolik,ortalama_gaz,ortalama_sivi,ortalama_komur)

  dataT1=t(phidata[1,])

  B <- c(0.7373802,34.2926453,19.4764683,15.3377781,30.1557281) 
  pie(B, main="1970-2013 yılları arası Ortalama Üretilen Sektörel Elektrik Miktarı", col=rainbow(length(B)),
  labels=c("ortalama_alter","ortalama_hidrolik","ortalama_gaz","ortalama_sivi","ortalama_komur"))
  
  data2=mydata %>%
  filter(Yil>=2003)
  
  phidata2=data2 %>%
  mutate(ortalama_komur=sum(Komur)/11)%>%
  mutate(ortalama_sivi=sum(Sivi_yakitler)/11)%>%
  mutate(ortalama_gaz=sum(Dogalgaz)/11)%>%
  mutate(ortalama_hidrolik=sum(Hidrolik)/11)%>%
  mutate(ortalama_alter=sum(Alter_Enerji)/11)%>%
  select(ortalama_alter,ortalama_hidrolik,ortalama_gaz,ortalama_sivi,ortalama_komur)

  B <- c(1.334982,23.21947,45.95544,2.724251,26.76586) 
  pie(B, main="2003-2013 yılları arası Ortalama Üretilen Sektörel Elektrik Miktarı", col=rainbow(length(B)),
  labels=c("ortalama_alter","ortalama_hidrolik","ortalama_gaz","ortalama_sivi","ortalama_komur"))
  percentlabels = round(100*B/sum(B), 1)
  pielabels =paste(percentlabels, "%", sep="")



