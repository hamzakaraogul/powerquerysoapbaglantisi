# powerquerysoapbaglantisi
Power Query'e Web Servis üzerinden soap yardımı ile veri almak.

Excel Power Query Link = https://www.microsoft.com/tr-TR/download/details.aspx?id=39379
<br>
SoapUI Open Source Link = https://www.soapui.org/downloads/soapui

Soap'ı açınız.

Sarı ile işaretlenmiş yere webservis linki olan wsdl linkini yapıştırıyoruz. ( https://www.w3schools.com/xml/tempconvert.asmx?wsdl )
![image](https://user-images.githubusercontent.com/62428397/183509813-a9991ab3-f35d-4bb9-aefa-1f4bf40f6018.png)

Sonrasında 'OK' tuşuna basıyoruz.

Aşağıdaki resimdeki gibi CelsiusToFahrenheit seçebiliriz.
![image](https://user-images.githubusercontent.com/62428397/183510117-30400af2-16f6-4a24-a948-69282e11ec42.png)

Soru işareti yazan yere 30 yazabiliriz.
![image](https://user-images.githubusercontent.com/62428397/183510296-3e45f1c0-ced0-4c1c-9fa6-bdcec5384ff5.png)

![image](https://user-images.githubusercontent.com/62428397/183510374-97d91be3-a28a-48f1-ad8f-bd6bb13adbfe.png) Tuşuyla sorguyu çalıştırıyoruz.
<br>
Sonuç görüldüğü üzere geliyor.
![image](https://user-images.githubusercontent.com/62428397/183510538-3bbf66a7-623c-4276-bde4-aa2036486d63.png)

Soap sorgumuzda bir problem olmadığını gördüğümüz üzere programı kapatmadan excele geçiyoruz.


Aşağıda görüldüğü üzere Excel Power Query yüklediyseniz sekmesi gelecektir.
![image](https://user-images.githubusercontent.com/62428397/183510776-b32cc996-6c18-4457-ac2b-61bea29d2e9f.png)

Fakat daha önceden yüklemişseniz ve gelmiyorsa;

![image](https://user-images.githubusercontent.com/62428397/183510936-a4783169-6652-4b05-9bd4-81f6489ff122.png) alanına tıklayınız.
<br>

![image](https://user-images.githubusercontent.com/62428397/183511000-e86c69b3-3c24-4917-8505-b9ddd2ac32e7.png)

Seçenekler alanına basınız.

Eklentiler alanına 'com eklentileri' seçeneğini seçerek 'git' butonuna basınız.
![image](https://user-images.githubusercontent.com/62428397/183511374-3f2b6e4c-2d93-43ab-95ba-496d207c9282.png)

<br>
Excel için Microsoft Power Query alanında tik atarak tamam'a bastığınızda powerquery gelecektir.
<br>
<img src="https://user-images.githubusercontent.com/62428397/183511734-33271a5c-af8b-4552-983f-8090b7e4af6b.png">
<br>

Düzenleyici başlata basarak power query'i başlatıyoruz.

![image](https://user-images.githubusercontent.com/62428397/183514436-a29ac970-7562-4f3f-a9a2-263129cdb4e2.png)

<br>

Sorgular alanında sağ tıklayarak, Yeni Sorgu -> Diğer Kaynaklar -> Boş Sorgu'ya tıklıyoruz.
![1](https://user-images.githubusercontent.com/62428397/183514815-d3426629-a2c8-441c-bb51-6661b4023ae3.png)

<br>
. koyarak enter tuşuna basıyoruz.
![image](https://user-images.githubusercontent.com/62428397/183515062-e57b8280-e724-4521-8124-883a180d9ee3.png)

<br>
Görünüm sekmesinde Gelişmiş Düzenleyici'ye basıyoruz.

![image](https://user-images.githubusercontent.com/62428397/183515161-437a5f01-fabd-4211-af4c-d56734897f27.png)

<br>
Soap sorgusunu buraya yapıştırabilirsiniz.
<br>
<img src="https://user-images.githubusercontent.com/62428397/183515448-8067778e-0fcd-4845-8fb6-8e5f1989613b.png">
<br>
SourceURL = "Webservis linki"
<br>
options = [ 
            #"Accept-Encoding"= "gzip,deflate",
            SOAPAction="Resimde Gösterilen Alan", 
            #"Content-Type"="text/xml;charset=UTF-8",
            #"Connection"="Keep-Alive"
          ],
<br>          
<img src="https://user-images.githubusercontent.com/62428397/183515683-b5f4dfb1-a93b-4e65-813b-bf9c43c63577.png">
      
<br>

WebContent = Web.Contents(SourceURL, 
// Content options in Web.Contents() 
    [Content=Text.ToBinary("

<br>
Yazısından sonra ' (" ' şeklinde iki tırnak başladığı için
<br>

<img src="https://user-images.githubusercontent.com/62428397/183515940-d7d02ef6-2594-496e-b461-072bbaced8bc.png">

Yukarıda resimde sarı alanda gösterilen alanı girerken her tirnaktan sonra &Character.FromNumber(34) şeklinde yazmamiz gerekiyor.
<br>
<soapenv:Envelope xmlns:soapenv="&Character.FromNumber(34)&"http://schemas.xmlsoap.org/soap/envelope/"&Character.FromNumber(34)&" xmlns:ns="&Character.FromNumber(34)&"https://www.w3schools.com/xml/"&Character.FromNumber(34)&" >

<br>
Sonraki alanda tirnak olmadığı için;
<br>
<img src="https://user-images.githubusercontent.com/62428397/183516097-3b3e7cbb-4fc7-43c7-a816-dc474ef90a1e.png">
<br>
direk bu şekilde yazabiliriz.
<br>
 <soapenv:Header/>
   <soapenv:Body>
      <ns:CelsiusToFahrenheit>
         <!--Optional:-->
         <ns:Celsius>30</ns:Celsius>
      </ns:CelsiusToFahrenheit>
   </soapenv:Body>
</soapenv:Envelope>

<br>
Sonrasında 
<br>

"), 
Headers=options]) ,
XmlContent = Xml.Tables(WebContent)
in
    XmlContent
    
<br>
şeklinde yazılmaktadır.
<br>

Bitti butonuna bastıktan sonra sorgu gelecektir.
<br>
![image](https://user-images.githubusercontent.com/62428397/183516487-38afc9c6-cd89-4aad-875f-39b440b74990.png)
<br>
şeklinde gelen yerdeki butona basınız.
<br>
![image](https://user-images.githubusercontent.com/62428397/183516550-5a9591c4-4c4d-4e3a-b125-e101e31c4d6e.png)
<br>
Anonim olarak bağlanınız.
<br>
![image](https://user-images.githubusercontent.com/62428397/183516602-7a9b4c47-65a9-43dd-b278-56652a4ff048.png)
<br>

Table yazısına tıklayınız. Sonra tekrardan 2 defa daha da çıkacak onlarada tıklayın.
<br>
Sonuç olarak sorgu aşağıdaki gibi gelecek ve webservis sorgunu powerqueryde almış olacaksınız.
<br>
![image](https://user-images.githubusercontent.com/62428397/183516769-e885ad02-0a4a-4311-8f8e-d2a7ac5498c1.png)

















