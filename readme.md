### Calculator-Project-soapui-project.xml

- Test Case 1 
  * Run Add Service & Set Variable & Validate Response











------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Soap UI

### Soap UI
Soap UI bir web servisi çağırmak ya da test etmek için kullanılan açık kaynaklı araçlardan birisidir. 
Soap UI ile API Testi, Yük Testi ve Güvenlik Testi yapılabilir.

### Soap ( Simple Object Access Protocol )
Soap HTTP ve ya TCP/IP üzerinden web servislerine ulaşmak için kullanılan XML tabanlı bir protokoldür.\
4 ana bölümden oluşur.
- Soap Envelope
    * Soap mesajlarında Root ögesidir ve kullanılması zorunludur.2 alt ögesi vardır.
    * Soap Header
        - Authentication, SOAP ile ilgili işlemlerin yapıldığı alandır. Bu alan zorunlu değildir.
    * Soap Body
        - Bu alanda metotun içerisindeki bilgi ve metotun sonuçlarıyla ilgili bilgi tutulur ve zorunludur.
- Soap Fault
    * SOAP içerisinde oluşabilecek hataların yönetildiği alandır. Bu alanda hata mesajları, hata bilgileri bulunur.
        - SOAP fault kodları:
           * Sender: Sorun gönderenden gelen yanlış veya eksik verilerden kaynaklanmıştır.
            * Receiver: Sorun, alıcı tarafında meydana gelen bir problemden kaynaklanmıştır.
            * VersionMismatch: Düğümün (node) kullanılan SOAP sürümünü tanımadığını gösterir.
            * MustUnderstand: Düğümün mustUnderstand ile işaretlenmiş bir bloğu tanımadığını belirtir.
            * Subcodes: 3 seviyeye kadar iç içe yerleştirlebilen hata kodlarını belirtir.
            * Reason: İnsan tarafından okunabilir (açıklayıcı, anlaşılır) açıklama içerir.

- Soap Elementleri
    - SOAP Request :  Soap ileti yapısını kullanarak bir Wsdl’i import ettikten sonra istek yollayabileceğimiz istek tipidir.
    - REST Request : RESTful mimarisi kaynaklarında fonksiyonel testleri yapmamıza olanak sağlayan rest istekleridir.
    - HTTP Request : Herhangi bir Http hizmetini çağırmak için kullanılabilecek bağımsız http istekleridir.
    - AMF Request : Http üzerinden AMF uzaktan çağrıları göndermek için kullanılabilir.(AMF, bir sunucu arka tarafıyla etkileşimde bulunmak için Flash/Flex uygulamaları tarafından kullanılan Adobes ActionScript mesajlaşma formatıdır.)
    - JDBC Request : Bir veri tabanından veri almak için kullanılan request yapısıdır. Sql sorgusu ile tetiklenen veri tabanından dönen sonucu xml olarak gösteren bir yapısı vardır. Bu işlemi yapabilmek için veritabanı sürücüsü ile soap ui bağlantınızı tamamlamanız gerekmektedir.
    - Properties : Fonksiyonel test özellikleriyle ilgili olarak testlerin yürütme ve işlevselliğini parametrelemek için kullanılır.
    - Property Transfer : Response içerisindeki değeri bir sonraki request içerisine eklemek istediğimizde kullanabileceğimiz test adımıdır.
    - Conditional Go to : Birden çok test step içeren Test Case’lerimizde bir sonraki test stepe devam edip etmemesini belli bir koşula bağlamak istediğimizde kullandığımız test adımıdır.
    - Run Test Case : Bir örnekleme ile açıklamaya çalışırsak ; 5 Test Step’imizin olduğunu düşünün ve 3. Test Step “Run Test Case” olsun. Biz kendi Test Case’imizi run ettiğimizde ilk 2 adımdan sonra 3. adıma yani “Run Test Case” adımına geldiğinde bu stepi oluştururken seçtiğimiz Test Case koşulmaya başlar ve o koşum tamamlandıktan sonra ilk başlattığımız Test Case 4.step ile koşuma devam eder. Bu özelliği kullanmak istediğimizde kullanmamız gereken Test Step “Run Test Case” dir.
    - Groovy Script : Testlerde groovy yada Java script kodunu çalıştırmak için bu test adımını kullanabiliriz.
    - Delay : Bir sonraki Test Step’in koşumuna başlamadan önce belli bir delay koymak istiyorsak kullanabileceğimiz test adımıdır.
    - Soap Mock Response : Bu adım ile kendi localimizde istediğimiz bir servisi sanallaştırıp istediğimiz response’un dönmesini sağlayabiliriz.
    - Manuel Test Step : Kullanıcının manuel olarak ilerletmesini istediğimiz durumlarda kullanabileceğimiz test adımıdır.  




### WSDL ( Web Service Description Language )
Soap içinde kullanılan ve servis içindeki fonksiyon, parametre, servis adresi vb. bilgilerini sağlayan bir standarttır.WSDL, web servislerinin fonksiyonlarını, istek ve cevap yapılarını, olası hataların ne olduğunu, iletişim ve güvenlik gereksinimleri gibi öğelerin ne olduğunu tanımlar. Bundan dolayı tanımlama dili olarak geçer.\
```
<definitions>
    Genel web servis arayüz yapısını tanımlar. Bu bölüm, servis tarafından desteklenen işlemleri, bu işlemlerle ilgili parametreleri ve soyut veri türlerini içerir.

<types>
  Veri tipi tanımlar........
</types>

<message>
  İletilecek olan verileri (mesajları) tanımlar....
</message>

<portType>
  Web servis işlevlerini tanımlar......
</portType>

<binding>
  Web servise ait protokol ve çıktı biçimini tanımlar....
</binding>

</definitions>
```


### SoapUI Web Servis Test Örneği

Sample WSDL : http://webservices.oorsprong.org/websamples.countryinfo/CountryInfoService.wso?WSDL

- Property Tanımlama ve Kullanma
  * Tanımlama
    - propertyler workspace, project ya da servis düzeyinde tanımlanabilir. \
  Project seviyesinde örnek property tanımlama ;\
  * Kullanma
    - ${#Project#PropertyName} – For Project Level
    - ${#TestSuite#PropertyName} – For Test Suite level
    - ${#TestCase#PropertyName} – For Test Case level
    - ${TestStepName#PropertyName} – For Test Step level
    - ${#MockService#PropertyName} – For MockService property
    - ${#Global#PropertyName} – For Global properties, found in File → Preference → - Global properties tab. This property can be used across all projects
    - ${#System#PropertyName} – For System Property, found in Help → System properties
    - ${#Env#PropertyName} – For environment variable\
    ![Alt text](SoapUI-Notes/image-1.png)

- Property Transfer
  * Test Suite oluştyurduktan sonra CountryISOCode servisi ile bir ülkenin ISO kodunu alıp, Property Transfer ile ISO kodunu CapitalCity servisine aktaracağız.\
  ![Alt text](SoapUI-Notes/image-3.png)


### SOAP Load Test


    - Threads: Number of concurrent users simulated. While there is no optimal number suggested, the open source SOAPUI version is known to perform well for up to 100 Threads.
    - Test Delay: The delay (milliseconds) between each TestCase run.
    - Random: The factor multiplied by Test Delay to randomly assign the delay between each case.
    - Limit: Available options are Total Runs, Seconds, and Runs per Thread. We set this parameter to 60s of the complete load test run.
    min: minimum time for the load step (millisecond).
    max: maximum time for the load step (millisecond).
    avg: average time for the load step (millisecond).
    last: time for the final load step in the test (millisecond).
    cnt: number of executions per load step.
    tps: transactions per second.
    bytes: header data volume processed in the load step (bytes).
    bps: header data volume processed as bytes per second in the load step (bytes per second).
    err: number of assertions occurred in the load step.
    rat: percent of requests failed (percent).


    Eş zamanlı 20 req , 1 dakika boyunca , toplam 467 sn sürmüş

  ![Alt text](SoapUI-Notes/image-4.png)

### SOAP UI Groovy Script Örnekler
    - groovy script random değer atama
    def test_prameters= testRunner.testCase.testSuite.project.getTestSuiteByName("deneme").getTestCaseByName("TestCase 1")
    test_prameters.setPropertyValue("Ad","Emine")
    def sn_degeri = context.expand('${#TestCase#ad}')
    log.info("ad değeri: " + sn_degeri)

    - groovy script dönen değeri kontrol etme
    def groovyUtils = new com.eviware.soapui.support.GroovyUtils(context)
    def holder = groovyUtils.getXmlHolder( "Request#Response" )
    holder.namespaces["ns1"] = "http://tckimlik.nvi.gov.tr/WS"
    def Result = holder.getNodeValue("//ns1:TCKimlikNoDogrulaResult")
    log.info "Service Response Message : " + Result\
    if(Result=="true")
    { log.info "Pass" }
    else
    { log.info "fail"}  

    - groovy script dönen değeri dosyaya yazma
    def groovyUtils = new com.eviware.soapui.support.GroovyUtils(context)
    def holder = groovyUtils.getXmlHolder( "Request#Response" )
    holder.namespaces["ns1"] = "http://tckimlik.nvi.gov.tr/WS"
    def addResult = holder.getNodeValue("//ns1:TCKimlikNoDogrulaResult")
    log.info "Service Response Message : " + addResult
    if(addResult=="true")
    { log.info "Pass" }
    else
    { log.info "fail"}
    def date = new Date()
    def dts = date.format("yyyy-MM-dd-HH-mm-ss")
    def fileName = "C:\Users\sedat\Desktop\test.txt"
    new File(fileName).write(dts +" Tarihli Servis Response Mesaji : "+addResult)

