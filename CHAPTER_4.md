# Mimari (Architecture)

> Mimari, kendi zamanını ve yerini anlatmalı, ancak zamansızlığa özlem duymalıdır.
>
>— Frank Gehry

DDD'nin en büyük avantajlarından biri, belirli bir mimariyi zorunlu kılmamasıdır.
Özenle oluşturduğumuz Core Domain (Çekirdek Alan) (2), Bounded Context (Sınırlı Bağlam) (2) içinde yer aldığı için, bir veya daha fazla mimari yaklaşımın tüm uygulama veya sistem üzerinde etkili olmasını sağlar. Bazı **mimari etkiler** doğrudan alan modelinin etrafında şekillenir ve genel bir etkiye sahiptir,  bazıları ise belirli ihtiyaçlara odaklanır. Buradaki _amaç, doğru mimari seçimleri ve desenleri bir araya getirmektir._

Gerçek yazılım kalite gereksinimleri, hangi mimari stillerin ve desenlerin kullanılacağını belirlemelidir.  
Seçilen mimari ve desenler, bu kalite gereksinimlerini karşıladığından veya aştığından emin olmalıdır.

-   Gereğinden fazla mimari karmaşıklık getirmek, doğru seçim yapmak kadar tehlikelidir.    
-   Mimariyi, yalnızca başarısızlık riskini azaltmak için kullanmalıyız.
-   Gereksiz bir mimari yaklaşımı haklı çıkaramıyorsak, onu sistemimizden çıkarmalıyız.
    

Bir mimari stil veya deseni seçme yeteneğimiz, kullanılabilir işlevsel gereksinimlerle (ör. kullanım senaryoları, kullanıcı hikayeleri, alan modeline özgü senaryolar) sınırlıdır. Bu nedenle, işlevsel gereksinimler olmadan doğru mimari seçimleri yapamayız. Bu da, kullanım senaryolarına dayalı bir mimari yaklaşımın günümüzde hâlâ geçerli olduğunu gösterir.

> ***Bu Bölümde Ele Alınacak Konular***
>
> - SaaSOvation’ın CIO’su ile yapılan retrospektif bir röportajı inceleyin.
> - Katmanlı Mimari’nin (Layered Architecture) Bağımlılık Tersine Çevirme Prensibi (DIP) ve Altıgen Mimari (Hexagonal) ile nasıl geliştirildiğini görün.
> - Hexagonal mimarinin, Servis Odaklı (SOA) ve REST tabanlı sistemleri nasıl desteklediğini keşfedin. 
> - Data Fabric veya Grid Tabanlı Dağıtık Önbellek ve Event-Driven Mimariyi değerlendirin.
> - CQRS’in DDD ile nasıl fayda sağladığını anlayın.
> - SaaSOvation ekiplerinin kullandığı mimari yaklaşımlardan ders çıkarın.

> ***Mimari, Sadece "Havalı" Görünmek İçin Kullanılmaz!***
>
> Aşağıdaki mimari stiller ve desenler, her projeye uygulanabilecek "havalı araçlar" değildir. Bunları yalnızca gerçek bir ihtiyacı karşıladığında ve proje başarısızlık riskini azalttığında kullanmalıyız.

---

[Evans], Katmanlı Mimariyi (Layers Architecture) merkeze aldı. Bu nedenle, SaaSOvation ekibi başlangıçta DDD’nin yalnızca bu iyi bilinen desenle etkili olabileceği sonucuna vardı. Ancak zamanla, DDD’nin bundan çok daha esnek olduğunu anladılar. [Evans] yazıldığında dönemde Katmanlı Mimari en popüler yaklaşım olsa da, DDD’nin yalnızca bununla sınırlı olmadığı fark edildi.

----------

Katmanlı Mimari prensipleri, hâlâ iyi kararlar almayı yönlendiren bir rehber olarak kullanılabilir.   Ancak burada durmamıza gerek yok! Gerektiğinde daha modern mimarileri ve desenleri ele alacağız. Bu da DDD’nin ne kadar esnek ve geniş çapta uygulanabilir olduğunu kanıtlayacak.

Elbette, SaaSOvation ekibi tüm mimari yaklaşımları aynı anda uygulamak zorunda değildi.  
Ancak ellerindeki seçeneklerden en doğru olanlarını seçmeleri gerekiyordu.

## Başarılı Bir CIO (Chef Information Officer) ile Röportaj

Bu bölümde, ele alınan mimari yaklaşımların neden kullanıldığına dair bir perspektif sunmak için on yıl sonrasına bir yolculuk yapacağız ve SaaSOvation’ın CIO’su ile konuşacağız. Şirketin başlangıçları mütevazıydı, ancak ***mimari kararlar her adımda başarının anahtarı oldu.*** Hadi, TechMoney programının sunucusu Maria Finance-Ilmundo ile birlikte bu röportaja kulak verelim...

**Maria:** Bu akşamki özel konuğum, büyük bir başarı hikayesine imza atan SaaSOvation’ın CIO’su Mitchell Williams. Şu an devam eden _"Mimari Tarzlarınızı Tanıyın"_ serimizde, ***doğru mimari seçimlerin nasıl kalıcı bir başarı getirdiğini*** tartışacağız. Mitchell, programımıza hoş geldiniz ve katıldığınız için teşekkürler.

**Mitchell:** Burada olmak çok güzel, Maria. Her zaman keyif alıyorum.

**Maria:** Bize erken dönemde aldığınız mimari kararları ve bunları neden tercih ettiğinizi anlatabilir misiniz?

**Mitchell:** Tabii ki! Belki inanmayacaksınız ama ilk başta projelerimizi masaüstü dağıtımı etrafında planlıyorduk. Ekibimiz, masaüstü uygulamasının merkezi bir veritabanına kaydetmek üzere tasarlanmasını sağladı. Bu yaklaşım için Katmanlı Mimariyi (Layers Architecture) seçtik.

**Maria:** Peki, bu mantıklı mıydı?

**Mitchell:** Bizce öyleydi. Çünkü yalnızca tek bir uygulama katmanı ve merkezi bir veritabanı ile çalışıyorduk. Bu yapı, basit bir istemci-sunucu (client-server) modelinde bizim için yeterliydi.

**Maria:** Ama çok geçmeden işler değişti, değil mi?

**Mitchell:** Kesinlikle! Bir iş ortağıyla güçlerimizi birleştirdik ve SaaS abonelik modeli ile ilerlemeye karar verdik. Bunu desteklemek için önemli bir finansman arayışına girdik ve bunu başardık.  
Öncelikle bir dizi iş birliği aracı geliştirmeye odaklanarak _çevik proje yönetimi uygulamamızı_ bir süreliğine arka planda tuttuk. Bunun iki temel faydası oldu:

1. Hızla büyüyen iş birliği pazarına (collaboration market) girdik. 
2. Proje yönetimi uygulamamıza doğal bir eklenti olarak bir iş birliği modülü oluşturduk.

Bildiğiniz gibi, yazılım geliştirme projelerinde iş birliği yapmak çok kritik bir konudur.

**Maria:** Oldukça ilginç. Kararlarınızın sizi nereye götürdüğünü anlatır mısınız?

**Mitchell:** Yazılım karmaşıklığı arttıkça, kaliteyi yönetmek için birim (unit) ve özellik (feature) test araçları kullanmamız gerekti. Bunu yapmak için Katmanlı Mimaride tersine mühendislik yaparak Dependency Inversion Prensibini (DIP) uyguladık. Bu çok önemliydi çünkü ekip, UI ve Altyapı Katmanlarını (Infrastructure Layer) devre dışı bırakarak Application ve Domain Katmanlarını bağımsız olarak test edebiliyordu. Aslında, UI'yi izole olarak geliştirebilir ve veritabanı teknolojisine karar vermeyi erteleyebilirdik. Bu, Katmanlı Mimariyi (Layers) tamamen terk etmekten ziyade onun doğal bir evrimiydi ve ekibimiz için rahat bir geçiş oldu.

**Maria:** Vay canına! Kullanıcı arayüzünü ve veritabanını değiştirebilmek oldukça riskli görünüyor. Bunu yapmak zor oldu mu?

**Mitchell:** Aslında hiç de zor olmadı. DDD'nin taktik desenlerini (tactical patterns) kullanmamız bu süreci çok kolaylaştırdı. Örneğin, _Aggregate Pattern_ ve _Repositories_ sayesinde öncelikle bellek içi (in-memory) veri saklama çözümleri ile geliştirme yapabilir ve veritabanı teknolojisini daha sonra entegre edebilirdik.

**Maria:** Vay.

**Mitchell:** Kesinlikle.

**Maria:** Ve sonra?

**Mitchell:** Boom! İşler yolunda gitti. _CollabOvation ve ProjectOvation_ ürünlerini çıkardık ve ardışık kârlı çeyrek dönemler yaşadık.

**Maria:** Ka-ching!

**Mitchell:** Kesinlikle! Daha sonra, masaüstü tarayıcılar için geliştirdiğimiz uygulamayı mobil cihazları da destekleyecek hale getirmek istedik. Bunun için REST mimarisini benimsedik.   Bu sırada abone olan şirketler, kimlik yönetimi, güvenlik ve gelişmiş proje yönetimi araçları talep etmeye başladı. Ayrıca, yeni yatırımcılar, iş zekası panellerinden (BI-Business Intelligence dashboards) gelen raporları görmek istiyorlardı.

**Maria:** Harika! Yani sadece mobil değil, birçok yeni ihtiyaç ortaya çıktı. Bunları nasıl yönettiniz?

**Mitchell:** Ekibimiz, _Hexagonal Mimariyi (Ports and Adapters)_ kullanmanın en iyi seçenek olduğunu düşündü. Bu yaklaşım sayesinde, yeni istemci türlerini neredeyse bir defaya mahsus şekilde ekleyebiliyorduk. Aynı şekilde, NoSQL ve mesajlaşma (messaging) gibi yeni çıkış noktalarını (output ports) da kolayca entegre edebildik. Ve bütün bunlar bizi ***cloud***'a buluta taşıdı.

**Maria:** Peki, bu değişiklikler konusunda kendinize güvendiniz mi?

**Mitchell:** Kesinlikle.

**Maria:** Bu büyük bir olay! Eğer tüm bu değişikliklerden zarar görmediyseniz, demek ki doğru seçimleri yapmışsınızdır.

**Mitchell:** Aynen öyle! Her ay yüzlerce yeni müşteri ekliyorduk. Eski sistemlerden veri taşımak için bir servis geliştirdik ve SOA mimarisini kullanarak bu süreçleri daha iyi yönetmeyi başardık.

**Maria:** Harika. Yani SOA’yı sadece "havalı" olduğu için değil, gerçekten ihtiyaç duyduğunuzda uyguladınız.

**Mitchell:** Evet, Maria, aslında en başından beri benimsediğimiz yaklaşım buydu. Bu bizim başarı için yol haritamızdı. Örneğin, zaman içinde ***TrackOvation*** adlı hata takip yazılımını ekledik ve bu, ProjectOvation ile entegre çalıştı. ProjectOvation’ın özellikleri arttıkça, kullanıcı arayüzü de giderek daha sofistike hale geldi. Scrum ürünleri ve sistemlerindeki hataların tamamını gösteren Ürün Sahibi panosu, her uygulama komutu ve ilgili olay gerçekleştiğinde anlık olarak güncellendi. Abone olan farklı kiracılardaki Ürün Sahipleri, panoları farklı şekillerde görüntülemeyi tercih ettiğinden, arayüz daha da karmaşık hale geldi. Ve elbette, mobil cihazları da desteklememiz gerekti. Ekip, ***CQRS mimari desenini dahil etmenin avantajlarını*** değerlendirdi.

**Maria:** CQRS mi? Hadi ama Mitch, bu bayağı karmaşık bir konu. Bunun nasıl sonuçlanacağını bilemediğimiz belirsizliklerden biri miydi? Yoksa uçurumdan aşağı adım atmak gibi bir risk mi taşıyordu?

**Mitchell:** Hayır, pek sayılmaz. Ekip, command ve query dünyaları arasındaki sürtünmeyi azaltmak için CQRS kullanmak adına geçerli bir neden bulduğunda, tam gaz ilerledi ve bir daha asla geriye bakmadı.

**Maria:** Aynen öyle. Bu, abonelerinizin dağıtık işlem gerektiren özellikler istemeye başladığı zaman değil miydi?

**Mitchell:** Evet; bunu doğru yapmasaydık kısa sürede karmaşıklık içinde boğulabilirdik. Bazı özellikler, bir sonuca ulaşmadan önce bir dizi dağıtılmış süreçten geçmeyi gerektiriyordu. ProjectOvation ekibi, kullanıcıyı bu potansiyel olarak uzun sürebilecek işlemler için bekletmek ve zaman aşımı riskiyle karşı karşıya bırakmak istemedi. Bu yüzden, tamamen Event-Driven bir Mimariyi hayata geçirdiler ve bu süreci yönetmek için ***klasik "Pipes and Filters" desenini*** kullandılar.

**Maria:** Ama bu, Karmaşıklık Yolu'ndaki yolculuğunuzun sonu değildi, değil mi? Ne kadar zorluydu?

**Mitchell:** Haha, hayır, hayır. Öyle bir şey asla olmadı gibi görünüyor. Ancak, zeki bir ekibiniz varsa, Karmaşıklık Yolu parkta yürüyüş yapmak gibi gelir. Aslında, Olay Tabanlı Mimari, genişleyen sistem paketinin birçok alanını basitleştirdi.

**Maria:** Doğru, bu. Devam et. Bu belli bir fırsattı. Hikayenin en sevdiğim kısmına geliyoruz. Biliyorsun... [gözleri parlıyor $$$]

**Mitchell:** Mimari yapımız, o kadar hızlı ölçeklenmemizi ve değişimi o kadar iyi yönetmemizi sağladı ki, RoaringCloud, SaaSOvation'ı satın aldı ... yani, bunun hepsi kamuya açık bir kayıt meselesi.

**Maria:** Derim ki, çok da kamuya açık bir durumdu. Hisse başına 50 dolardan, yaklaşık 3 milyar dolarlık bir kamu kaydıydı.

**Mitchell:** Finansal veriler konusunda gerçekten iyi bir hafızan var! Ve bu, entegrasyonu doğru yapabilmek için ciddi bir teşvikti. Yeni abonelerle birlikte kullanıcı tabanı, ProjectOvation altyapısını zorlamaya başladı. Artık Pipes and Filters'ı dağıtmak ve paralel hale getirme zamanıydı. Bu da uzun süreli işlemler eklemeyi gerektiriyordu, ki bunlara bazen ***Sagas*** denir.

**Maria:** Harika. Kesinlikle eğlenceli diyebilir misiniz?

**Mitchell:** Eğlenceliydi, ancak daha da önemlisi gereklilikti.

**Maria:** Ve eğlence sona ermemiş gibi görünüyor. Başarı hikayenizde belki de en beklenmedik ve şok edici bölüm bir sonraki adım oldu, değil mi?

**Mitchell:** Bunu biliyorsun. Artık RoaringCloud, pazarda abonelik uygulamalarının ve milyonlarca kullanıcının çokluğu nedeniyle bir tekel haline gelmişti ve hükümet bu durumu fark etti ve sektörü düzenlemeye başladı. Yeni bir yasa çıkarıldı ve RoaringCloud'dan her proje değişikliğini takip etmesi istenmeye başlandı. Aslında, bu uyumluluk durumunu domain modelinin doğal bir parçası olarak en iyi şekilde ele almanın yolu ***Event Sourcing*** kullanmaktı.

**Maria:** Vay, tam hazırlıklısınız! Gerçekten de deli bir durum.

**Mitchell:** Evet, aslında **çılgınca iyi bir problem bu**.

**Maria:** Beni en çok etkileyen şey şu ki, tüm bu yıllar boyunca uygulamalarınızın temeli DDD yazılım modellerine dayanıyordu. Ama kesinlikle DDD size zarar vermedi. Bu süreç boyunca herhangi bir zorluk yaşamadınız gibi görünüyor.

**Mitchell:** Aslında tam tersi oldu. DDD’yi erken seçip onu tamamen anlamak için zaman ayırdığımız için, kaçamayacağımız ve istemediğimiz iş durumları bile kolayca yönetildi.

**Maria:** Benim de dediğim gibi, "Ka-ching!" Bir kez daha teşekkürler Mitchell. Burada, _"Doğru mimariyi seçmenin nasıl kalıcı bir başarı getirdiğini"_ öğrendik.  _"Know Your Architectural $tyles"_ programında tekrar görüşmek üzere.

**Mitchell:** Benim için de bir zevkti, Maria. Davet ettiğiniz için teşekkür ederim.

Bu röportaj, **mimari etkilerin nasıl DDD ile entegre edilebileceğini** ve **her bir yaklaşımın en uygun zamanda nasıl devreye alınabileceğini** gösteren harika bir örnek sunuyor. 🚀

## Katmanlar (Layers)

Layered Architecture [Buschmann et al.] deseni, birçok kişi tarafından tüm mimarilerin atası olarak kabul edilir. N-tiers (çok katmanlı) sistemleri destekler ve bu nedenle genellikle Web, kurumsal ve masaüstü uygulamalarında kullanılır. Burada, uygulamamızın veya sistemimizin çeşitli endişelerini iyi tanımlanmış katmanlara ayırırız.

> **Domain modelinin** ve **iş mantığının** ifadesini izole eder ve altyapı, kullanıcı arayüzü ya da iş mantığı olmayan herhangi bir uygulama mantığına olan bağımlılığı ortadan kaldırırız. Karmaşık bir programı katmanlara böleriz. Her katmanda, yalnızca alt katmanlara bağımlı olan, uyumlu bir tasarım geliştiririz. [Evans, Ref, p. 16]

Şekil 4.1, geleneksel Katmanlar Mimarisi kullanan bir DDD uygulamasında yaygın olan katmanları gösterir. Burada, izole edilmiş **Core Domain**, mimarideki bir katmanda yer alır. Üstünde **UI** ve **Uygulama Katmanları**, altında ise **Altyapı Katmanı** bulunur.

![Figure 4.1](./images/chapter4/figure-4-1.png)

**Figure 4.1:** DDD'nin uygulandığı geleneksel Katmanlar Mimarisi

Bu mimarinin temel kuralı, her katmanın yalnızca kendisine ve altındaki katmanlara bağımlı olmasıdır. Bu tarz içinde bazı farklılıklar bulunmaktadır. **Sıkı Katmanlar Mimarisi**, yalnızca doğrudan altındaki katmana bağlanmaya izin veren bir yaklaşımdır. **Gevşek Katmanlar Mimarisi** ise, herhangi bir üst düzey katmanın altındaki herhangi bir katmana bağlanmasına izin verir. Çünkü, _Kullanıcı Arayüzü_ ve _Uygulama Servisleri_ genellikle altyapıyı kullanması gerektiğinden, çoğu sistem Gevşek Katmanlar Mimarisi üzerine kuruludur.

Alt katmanlar, üst katmanlarla doğrudan bağlantıya sahip olmasa da, **Observer** veya **Mediator** gibi bir mekanizma kullanarak gevşek bir şekilde üst katmanlara bağlanabilirler [Gamma et al.]. Alt katmandan üst katmana doğrudan bir referans bulunmaz. Örneğin, Mediator kullanıldığında, üst katman, alt katman tarafından tanımlanan bir arayüzü uygular, ardından uygulayan nesneyi alt katmana argüman olarak gönderir. Alt katman, uygulayan nesneyi, nerede yer aldığı konusunda herhangi bir bilgi sahibi olmadan kullanır.

Kullanıcı Arayüzü, yalnızca kullanıcı görünümü ve istekleriyle ilgili endişeleri ele alan kodları içermelidir. Domain/iş mantığı içermemelidir. Bazıları, Kullanıcı Arayüzü'nün doğrulama gerektirdiği için iş mantığını içermesi gerektiğini düşünebilir. Ancak, Kullanıcı Arayüzü'nde bulunan doğrulamalar, yalnızca domain modelinde bulunması gereken doğrulamalarla aynı türden değildir (yalnızca). **Entities (5)** bölümünde de tartışıldığı gibi, yalnızca domain modelinde derin iş bilgilerini ifade eden kaba doğrulamaları sınırlamak istiyoruz.

Eğer UI bileşenleri domain modelinden nesneler kullanıyorsa, bu genellikle yalnızca verilerini ekranda render etmekle sınırlıdır. Bu yaklaşımı kullanırken, **Presentation Model (14)** kullanılarak görünümün domain nesneleri hakkında bilgi sahibi olmasının önüne geçilebilir.

Bir kullanıcı insan olabileceği gibi başka sistemler de olabilir, bu nedenle bazen bu katman, **Open Host Service (13)** şeklinde bir API servislerinin uzaktan çağrılmasını sağlamak için olanaklar sunar.

UI bileşenleri, **Application Layer**'nın doğrudan istemcileridir.

**Application Services (14)**, Application Layer'da bulunur. **Domain Servisleri (7)**'nden farklıdırlar ve bu nedenle domain mantığından yoksundur. Persistence transaction ve security gibi konuları kontrol edebilirler. Ayrıca, diğer sistemlere yönelik Event tabanlı bildirimler göndermek veya kullanıcılara e-posta mesajları göndermek gibi işlemlerden sorumlu olabilirler. Domain modelinin doğrudan istemcileridir ancak kendileri iş mantığı içermez. Son derece hafif olurlar ve **Aggregate (10)** gibi domain nesneleri üzerinde gerçekleştirilen işlemleri koordine ederler. Uygulama Servislerinin birincil işlevi, model üzerindeki kullanım senaryolarını veya kullanıcı hikayelerini ifade etmektir. Dolayısıyla, bir Application Service'in ortak işlevi, Kullanıcı Arayüzü'nden parametreler alıp, bir **Repository (12)** kullanarak bir Aggregate örneği elde etmek ve ardından bu örnek üzerinde bazı komut işlemleri gerçekleştirmektir:

```
@Transactional
public void commitBacklogItemToSprint(String aTenantId, String aBacklogItemId, String aSprintId) {
	TenantId tenantId = new TenantId(aTenantId); 
	
	BacklogItem backlogItem = backlogItemRepository.backlogItemOfId( 
		tenantId,
		new BacklogItemId(aBacklogItemId)); 

	Sprint sprint = sprintRepository.sprintOfId(tenantId, new SprintId(aSprintId)); 

	backlogItem.commitTo(sprint);
}
```

Eğer Application Service, bundan çok daha karmaşık hale gelirse, bu muhtemelen domain mantığının servis içine sızdığının ve modelin anemik hale geldiğinin bir göstergesidir. Bu nedenle, bu model istemcilerini çok ince tutmak en iyi uygulamadır. Yeni bir Aggregate oluşturulması gerektiğinde, Application Service, **Factory (11)** veya Aggregate'in constructor'ını kullanarak onu başlatır ve ardından ilgili Repository'yi kullanarak kalıcı hale getirir. Application Service, ayrıca bazı domain-specific görevlerini yerine getirmek için bir **Domain Servisi**'lerini kullanabilir; bu, stateless bir işlem olarak tasarlanmıştır.

Eğer domain modeli **Domain Events (8)** yayınlamak üzere tasarlandıysa, Application Layer herhangi bir sayıda **Event**'e abone olmak için aboneler kaydedebilir. Bu, **Events**'lerin saklanmasını, iletilmesini ve başka şekilde uygulamanın görevlerinden biri olarak ele alınmasını sağlar. Bu, domain modelinin yalnızca kendi temel endişelerini bilmesini sağlar ve **Domain Event Publisher (8)**'ın hafif kalmasını ve mesajlaşma altyapısı bağımlılıklarından kurtulmasını sağlar.

⚠️ Domain modeli, tüm iş mantığını içerdiği için diğer bölümlerde uzun uzadıya tartışılmaktadır, burada tekrar edilmemektedir. Bununla birlikte, domain ve geleneksel Layers kullanımı ile ilgili bazı zorluklar bulunmaktadır. Layers kullanmak, Domain Katmanının Infrastructure'ı sınırlı bir şekilde kullanmasını gerektirebilir. Bununla, temel domain nesnelerinin bunu yapmasını kastetmiyorum; bu kesinlikle tamamen kaçınılması gereken bir şeydir. Ancak, Layers tanımına sadık kalmak, Domain Katmanında Infrastructure tarafından sağlanan teknolojilere dayanan bazı arabirimlerin implementasyonlarını gerektirebilir.

Örneğin, Repository interface'leri, Infrastructure içinde barındırılan kalıcılık mekanizmaları gibi bileşenleri kullanan implementasyonlar gerektirir. Peki ya Repository interface'leri sadece Infrastructure içinde implement etsek? Çünkü Infrastructure Katmanı, Domain Katmanının altındadır, bu durumda Infrastructure'dan Domain'e yapılan referanslar Layers Architecture kurallarını ihlal eder. Yine de, bunun önlenmesi, temel domain nesnelerinin Infrastructure'a bağlanacağı anlamına gelmez. Bunu önlemek için, teknik sınıfları gizlemek için **implementation Modules (9)** kullanabiliriz:

`com.saasovation.agilepm.domain.model.product.impl`

Modüller (9) bölümünde belirtildiği gibi, `MongoProductRepository` bu paket içinde barındırılabilir. Ancak, bu sorunu ele almanın tek yolu bu değildir. Bunun yerine, bu tür arabirimleri Application Layer içinde implement etmeyi tercih edebiliriz, böylece Layers kurallarını korumuş oluruz. Şekil 4.2, bu yaklaşımın bir örneğini sunmaktadır. Ancak, bunu yapmak biraz hoş olmayan bir çözüm gibi görünebilir.

Daha iyi bir yol vardır, bu ***Dependency Inversion Principle*** başlıklı bölümde tartışılmıştır. 
 
Geleneksel bir Katmanlı Mimaride, Infrastructure en alttadır. Kalıcılık ve mesajlaşma mekanizmaları gibi şeyler burada yer alır. Mesajlar, kurumsal mesajlaşma ara katmanları veya daha temel e-postalar (SMTP) veya metin mesajları (SMS) gibi şeyleri içerebilir. Uygulamaya düşük seviyede hizmetler sağlayan tüm teknik bileşenleri ve çerçeveleri düşünün. Bunlar genellikle Infrastructure'ın bir parçası olarak kabul edilir. Daha yüksek seviyedeki katmanlar, daha alt seviyedeki bileşenlere bağlanarak sağlanan teknik imkanları yeniden kullanır. Bu durumda, tekrar belirtmek gerekirse, core domain model nesnelerinin Infrastructur*'a bağlanması fikrini reddetmek istiyoruz.

![Figure 4.2](./images/chapter4/figure-4-2.png)

**Figure 4.2:** Application Layer, Domain Layer tarafından tanımlanan interface'lerin bazı teknik uygulamalarını barındırabilir.

---

SaaSOvation takımları, Infrastructure Layer'ın en altta olmasının bazı dezavantajlar sunduğunu fark etti. Birincisi, Domain Layer tarafından gereken teknik yönlerin implementasyonunun, Layers kurallarının ihlal edilmesi gerektiği için biraz tatsız hale gelmesiydi. Ayrıca, kodları test etmek oldukça zor oluyordu. Bu dezavantajı nasıl aşabilirlerdi?

---

Katmanların sırasını biraz ayarlayarak daha tatlı bir çözüm bulabilir miydik?

### Bağımlılık Tersine Çevirme Prensibi (Dependency Inversion Principle)

Geleneksel Layers Architecture üzerinde, bağımlılıkların işleyiş şeklini ayarlayarak iyileştirme yapmanın bir yolu vardır. **Dependency Inversion Principle (DIP)**, Robert C. Martin tarafından öne sürülmüş ve [Martin, DIP]'te açıklanmıştır. Resmi tanım şu şekilde ifade edilmektedir:

> Yüksek seviyedeki modüller, düşük seviyedeki modüllere bağımlı olmamalıdır. Her ikisi de soyutlamalara bağımlı olmalıdır.
>
> Soyutlamalar, detaylara bağımlı olmamalıdır. Detaylar, soyutlamalara bağımlı olmalıdır.

Bu tanımın özünde, düşük seviyeli hizmetleri sağlayan bir bileşenin (bu tartışma için Infrastructure), yüksek seviyeli bileşenler (bu tartışma için UI, Application ve Domain) tarafından tanımlanan arayüzlere bağımlı olması gerektiği ifade edilmektedir. DIP kullanan bir mimarinin birçok farklı şekilde ifade edilmesi mümkün olsa da, bunu Şekil 4.3'te gösterilen yapıya indirgemek mümkündür.

> ***DIP Gerçekten Tüm O Katmanları Destekler mi?***
> 
> Bazıları, DIP'nin sadece iki katmandan oluştuğunu düşünebilir: biri üstte, diğeri altta. Üstteki katman, alttaki katmanda tanımlanan arayüz soyutlamalarını uygular. Şekil 4.3'ü buna uyacak şekilde ayarladığınızda, Infrastructure Layer üstteki katman olurken, User Interface Layer, Application Layer ve Domain Layer alttaki katmanları oluşturur. Bu bakış açısını veya DIP mimarisinin bu şekilde görsel bir sunumunu tercih edip etmeyeceğiniz size bağlıdır. Endişelenmeyin, **Hexagonal Architecture** [Cockburn] veya **Ports and Adapters Architecture** tüm bunların gittiği yön olacaktır.

![Figure 4.3](./images/chapter4/figure-4-3.png)

**Figure 4.3:** Bağımlılık Tersine Çevirme İlkesi kullanıldığında olası Katmanlar. Infrastructure Katmanını diğerlerinin üzerine taşıyarak aşağıdaki tüm Katmanlar için arayüzler uygulamasını sağlıyoruz.

Şekil 4.3'teki mimariye göre, Domain katmanında tanımlanan bir interface için Infrastructure katmanında implementasyonu olan bir Repository'imiz olacaktır:

````
package com.saasovation.agilepm.infrastructure.persistence;

import com.saasovation.agilepm.domain.model.product.*;

public class HibernateBacklogItemRepository implements BacklogItemRepository {
    ...
    @Override
    @SuppressWarnings("unchecked")
    public Collection<BacklogItem> allBacklogItemsCommitedTo(Tenant aTenant, SprintId aSprintId) {
        Query query = this.session().createQuery("from -BaklogItem as _obj_ where _obj_.tenant = ? and _obj_.sprintId = ?");

        query.setParameter(0, aTenant);
        query.setParameter(1, aSprintId);

        return (Collection<BacklogItem>) query.List();
    }
    ...
}
````

Domain katmanına odaklanırsak, DIP kullanmak, Domain ve Infrastructure katmanlarının, domain model tarafından tanımlanan soyutlamalara (interfaces) bağımlı olmasını sağlar. Application Layer doğrudan Domain katmanının istemcisidir ve Domain interface'lerine bağımlıdır. Bu sayede, Repository ve Domain Service gibi teknik implementasyon sınıflarına Infrastructure tarafından dolaylı bir şekilde erişebilir. Implementasyonları edinmenin birkaç yolu olabilir, bunlar arasında **Dependency Injection**, **Service Factory** ve **Plug In** [Fowler, P of EAA] yer alır. Kitap boyunca kullanılan örneklerde, Spring Framework tarafından sağlanan Dependency Injection ve bazen Service Factory sınıfı olan DomainRegistry kullanılmıştır. Aslında, DomainRegistry, Spring'i kullanarak domain modeli tarafından tanımlanan arayüzleri implement eden bean'lere, bunlar arasında Repositories ve Domain Services de dahil olmak üzere referanslar aramak için kullanır.

İlginç bir şekilde, DIP'nin bu mimari üzerindeki etkisini düşündüğümüzde, aslında artık hiç katman olmadığı sonucuna varabiliriz. Hem yüksek seviyeli hem de düşük seviyeli endişeler yalnızca soyutlamalara bağımlıdır, bu da yığılımın (stack) çökeceği anlamına gelir. Peki, bu mimariyi tamamen tersine çevirmeyi ve biraz daha simetri eklemeyi düşündüğümüzde nasıl olur? Şimdi bunun nasıl çalıştığına bakalım.

## Hexagonal veya Ports ve Adapters

Hexagonal Mimari (Alistair Cockburn tarafından şekillendirilen), simetri üretmek için bir tarz önerir. Bu hedefi, çok çeşitli istemcilerin sistemi eşit şekilde etkileşimde bulunabilmesini sağlayarak ilerletir. Yeni bir istemci mi gerekiyor? Sorun değil. Sadece, verilen istemcinin girişini, iç uygulamanın API'sinin anlayabileceği bir forma dönüştürmek için bir ***Adapter*** ekleyin. Aynı zamanda, sistemin kullandığı çıktı mekanizmaları, örneğin grafikler, kalıcılık ve mesajlaşma, çeşitli ve değiştirilebilir olabilir. Bu, uygulama sonuçlarını, belirli bir çıktı mekanizmasının kabul edeceği bir forma dönüştüren bir Adapter oluşturularak mümkündür.

Bunu tartışırken, bu mimarinin zamanlar üstü bir potansiyele sahip olduğunu kabul edebilirsiniz. Bugün, Layers Architecture kullandığını söyleyen birçok ekip aslında bunun yerine Hexagonal kullanıyor. Bunun bir nedeni de, şu anda bazı formda Dependency Injection kullanan projelerin sayısının artmış olmasıdır. Dependency Injection'ın otomatik olarak Hexagonal olduğu söylenemez. Sadece, Ports and Adapters tarzı bir mimari geliştirmeye doğal olarak eğilimli bir şekilde bir mimari üretmeyi teşvik eder. Her halükarda, daha kapsamlı bir anlayış bu noktayı netleştirecektir.

Genellikle, istemcilerin sistemle etkileşime girdiği yeri "front end" olarak düşünürüz. Benzer şekilde, uygulamanın kalıcı verileri aldığı, yeni kalıcı verileri depoladığı veya çıktıyı gönderdiği yer, "back end" olarak kabul edilir. Ancak **Hexagonal** mimari, bir sistemin alanlarını farklı bir şekilde ele almayı teşvik eder, bu da Şekil 4.4'te gösterildiği gibi. İki ana alan vardır: ***outside*** ve ***inside***. Dış alan, çeşitli istemcilerin _input_ göndermesine olanak tanırken, aynı zamanda kalıcı verileri almak, uygulamanın çıktısını (örneğin veritabanı) depolamak veya başka bir yere göndermek (örneğin mesajlaşma) için mekanizmalar sağlar.

![Figure 4.4](./images/chapter4/figure-4-4.png)

**Figure 4.4:** Hexagonal Mimari, Ports and Adapters olarak da bilinir. Dış tiplerin her biri için Adaptörler vardır. Dışarısı içeriye uygulamanın API'si aracılığıyla ulaşır.

Şekil 4.4'te her istemci türünün kendi **Adapter**'ı vardır, bu da giriş protokollerini, uygulamanın API'siyle uyumlu hale getiren giriş verilerine dönüştürür—iç kısım. Altıgenin her bir kenarı, giriş veya çıkış için farklı bir **Port** türünü temsil eder. Üç istemci, aynı türdeki giriş Port'u (Adapter A, B ve C) üzerinden istek gönderirken, biri farklı bir Port türünü kullanır (Adapter D). Belki üçü HTTP (tarayıcı, REST, SOAP vb.) kullanırken, diğeri AMQP (örneğin, RabbitMQ) kullanıyordur. Bir Port'un anlamı için çok net bir tanım yoktur, bu yüzden esnek bir kavramdır. Port'lar hangi şekilde bölünürse bölünsün, istemci istekleri gelir ve ilgili Adapter, girişlerini dönüştürür. Ardından, uygulama üzerinde bir işlem çağırır veya uygulamaya bir olay gönderir. Böylece kontrol içeriye aktarılır.

> ***Muhtemelen Port'ları Kendimiz Uygulamıyoruz***
>
> Aslında, Port'ları genellikle kendimiz uygulamayız. Bir Port'u HTTP olarak düşünün ve Adapter'ı Java Servlet veya JAX-RS anotasyonlu bir sınıf olarak kabul edin; bu sınıf, bir konteynerden (JEE) veya bir çerçeveden (RESTEasy veya Jersey) metod çağrılarını alır. Veya NServiceBus veya RabbitMQ için bir mesaj dinleyicisi oluşturabiliriz. Bu durumda, Port daha çok mesajlaşma mekanizmasıdır ve Adapter, mesaj dinleyicisi olacaktır, çünkü mesaj dinleyicisinin sorumluluğu, mesajdan verileri alıp, bunları uygulamanın API'sine (domain modelinin istemcisi) geçmek için uygun parametrelere çevirmektir.

> ***Uygulamayı Fonksiyonel Gereksinimlere Göre Tasarlayın***
> 
> Hexagonal kullanırken, uygulamayı, desteklenen istemci sayısından değil, kullanım senaryolarını (use case) göz önünde bulundurarak tasarlarız. Herhangi bir sayıda ve türde istemci, çeşitli Port'lar aracılığıyla istek gönderebilir, ancak her Adapter, aynı API'yi kullanarak uygulamaya yönlendirme yapar.

Uygulama, istekleri API'si aracılığıyla alır. Uygulama sınırı veya iç hexagon, aynı zamanda kullanım senaryosu (ya da kullanıcı hikayesi) sınırıdır. Diğer bir deyişle, kullanım senaryolarını uygulamanın fonksiyonel gereksinimlerine dayanarak oluşturmalıyız, çeşitli istemcilerin veya çıktı mekanizmalarının sayısına göre değil. Uygulama, API'si aracılığıyla bir istek aldığında, iş mantığının yürütülmesini içeren tüm istekleri yerine getirmek için domain modelini kullanır. Böylece, uygulamanın API'si, Application Services'ın bir seti olarak yayınlanır. Burada tekrar, Application Services, domain modelinin doğrudan istemcisidir, Layers kullanırken olduğu gibi.

Aşağıdaki, JAX-RS kullanılarak yayımlanan bir RESTful kaynağını temsil etmektedir. Bir istek, HTTP giriş Port'u üzerinden gelir ve işleyici bir Adapter olarak hareket ederek, bir Application Service*e devreder:

```
@Path("/tenants/{tenantId}/products")
public class ProductResource extends Resource { 

	private ProductService productService;
	...

	@GET
	@Path("{productId}")
	@Produces({ "application/vnd.saasovation.projectovation+xml" })
	public Product getProduct( 
		@PathParam("tenantId") String aTenantId,
		@PathParam("productId") String aProductId,
		@Context Request aRequest) { 

		Product product = productService.product(aTenantId, aProductId);
		if (product == null) {
			throw new WebApplicationException(Response.Status.NOT_FOUND);
		}

		return product; // serialized to XML using MessageBodyWriter
	} 
	...
}
```

Çeşitli JAX-RS açıklamaları, Adapter'ın önemli bir kısmını sağlar, kaynak yolunu çözümleyip parametrelerini String örneklerine dönüştürür. ProductService örneği enjekte edilir ve bu istek, uygulamanın iç kısmına yönlendirilir. Product, XML olarak serileştirilir ve bir Response içine yerleştirilir, ardından HTTP çıkış Port'u üzerinden gönderilir.

> ***JAX-RS Burada Odak Noktası Değil***
> Bu, uygulamanın ve domain modelinin iç kısmını kullanmanın sadece bir yoludur. Esasında, JAX-RS önemli değildir. Bunun yerine Restfulie kullanabiliriz ya da restify modülünü çalıştıran bir Node.js sunucusu oluşturabiliriz. Dahası, diğer Ports'tan gelen girdileri ele almak için tasarlanmış Adapters aynı API'ye yönlendirme yapacaktır, bunu göreceksiniz.

Uygulamanın sağ tarafındaki kısmı ne olacak? Repository implementasyonlarını, daha önce depolanan Aggregate örneklerine erişim sağlayan ve yenilerini depolayan **persistence Adapters** olarak düşünebiliriz. Diyagramda gösterildiği gibi (**Adapters E, F, ve G**), ilişkisel veritabanları, belge depoları, dağıtık önbellek ve bellek içi depolar için Repository implementasyonlarımız olabilir. Uygulama **Domain Event** mesajlarını dışarıya gönderiyorsa, mesajlaşma için farklı bir **Adapter (H)** kullanılacaktır. Çıkış mesajlaşma Adapter'ı, AMQP'yi destekleyen giriş Adapter'ının tersidir ve bu nedenle, kalıcılık için kullanılan Port'tan farklı bir Port'tan dışarıya çıkar.

✅ Hexagonal'ın büyük bir avantajı, Adapters'ların test amaçları için kolayca geliştirilebilmesidir. Uygulama ve domain modeli, istemciler ve depolama mekanizmaları var olmadan önce tasarlanabilir ve test edilebilir. Testler, `ProductService`'i HTTP/REST, SOAP ya da mesajlaşma Ports'ını desteklemek için herhangi bir karar verilmeden önce oluşturulabilir. UI wireframe'leri tamamlanmadan önce, her türlü test istemcisi geliştirilebilir. Proje için bir kalıcılık mekanizması seçilmeden çok önce, bellek içi Repositories kullanılabilir ve test amacıyla kalıcılığı taklit edebilir. Repositories (12) bölümünde, bellek içi implementasyonlar geliştirme hakkında daha fazla bilgi bulabilirsiniz. Teknik bileşenler eklenmeden, çekirdek üzerinde önemli ilerlemeler kaydedilebilir.

Eğer gerçek Layers kullanıyorsanız, yapıyı devirmeyi ve Ports ve Adapters tabanlı geliştirme yapmayı düşünün. Doğru tasarlandığında, içindeki hexagon—uygulama ve domain modeli—dış kısımlara sızmaz. Bu, kullanım senaryolarının uygulandığı temiz bir uygulama sınırı oluşturur. Dışarıda, her türlü istemci Adapters'ı sayısız otomatik testi ve gerçek dünyadaki istemcileri destekleyebilir, ayrıca depolama, mesajlaşma ve diğer çıkış mekanizmalarını da destekleyebilir.

---

SaaSOvation takımları, Hexagonal Architecture'ı kullanmanın avantajlarını değerlendirdiklerinde, Layers'dan geçiş yapmaya karar verdiler. Aslında bu zor olmadı. Sadece, Spring Framework'ü kullanırken biraz farklı bir düşünme biçimi benimsemek gerekiyordu.

---

Hexagonal Architecture çok yönlü olduğundan, sistemin ihtiyaç duyduğu diğer mimarileri destekleyen bir temel olabilir. Örneğin, _Service-Oriented_, _REST_ ya da _Event-Driven Architecture_ gibi yapıları dahil edebilir; _CQRS_ kullanabilir; bir _Data Fabric_ ya da _Grid-Based Distributed Cache_ uygulayabilir; ya da _Map-Reduce_ dağıtık ve paralel işlem ekleyebiliriz. Bunların çoğu bu bölümde daha sonra tartışılacak. Hexagonal tarzı, bu ek mimari seçeneklerin her birini desteklemek için güçlü bir temel oluşturur. Başka yollar da vardır, ancak bu bölümün geri kalanında, her bir konuyu geliştirirken Ports ve Adapters'ın kullanılacağını varsayın.

*** 173. sayfada kaldım.