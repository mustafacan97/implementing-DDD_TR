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

## Service-Oriented (Hizmet Odaklı Mimari - SOA)

Service-Oriented Architecture (SOA), farklı kişiler için farklı anlamlara gelebilir. Bu durum, SOA hakkında tartışmaları biraz zorlaştırabilir. Bu yüzden, ortak bir zemin bulmak ya da en azından bu tartışma için belirli bir çerçeve tanımlamak en iyisidir. _Thomas Erl'in_ tanımladığı **SOA prensiplerini** göz önünde bulunduralım. Hizmetlerin daima birlikte çalışabilir olmasının yanı sıra, aşağıda Tablo 4.1'de belirtilen sekiz tasarım prensibine sahip olması gerekir:

***Tablo 4.1: Hizmetlerin Tasarım Prensipleri***
| Hizmet Tasarım Prensibi | Açıklama |
| ----------------------- | -------- |
| 1. Service Contract | Hizmetler, amaçlarını ve yeteneklerini bir veya daha fazla açıklama belgesi ile ifade eder. |
| 2. Service Loose Coupling | Hizmetler, bağımlılıklarını en aza indirir ve yalnızca birbirlerinden haberdar olurlar. |
| 3. Service Abstraction | Hizmetler, yalnızca sözleşmelerini yayınlar ve iç mantıklarını istemcilerden gizler. |
| 4. Service Reusability | Hizmetler, daha büyük ve karmaşık hizmetler oluşturmak için başkaları tarafından tekrar kullanılabilir. | 
| 5. Service Autonomy | Hizmetler, bağımsız kalabilmek için kendi ortamlarını ve kaynaklarını kontrol eder. Bu sayede tutarlılık ve güvenilirlik sağlanır. |
| 6. Service Statelessness | Hizmetler, durum yönetimini mümkün olduğunca istemcilere bırakır. Ancak bu, Hizmet Özerkliği ile çelişmemelidir. |
| 7. Service Discoverability | Hizmetler, metadata ile tanımlanır ve bu sayede keşfedilebilir. Bu, hizmet sözleşmelerinin anlaşılmasını sağlar ve tekrar kullanılabilirliği artırır. |
| 8. Service Composability | Hizmetler, büyüklükleri ve karmaşıklıkları ne olursa olsun, daha geniş kapsamlı hizmetler içinde bir araya getirilebilir. |

![Figure 4.5](./images/chapter4/figure-4-5.png)

**Figure 4.5:** REST, SOAP ve mesajlaşma hizmetleri ile SOA'yı destekleyen Hexagonal Architecture

Hizmet sınırının en solda ve alan modeli (domain model)'nin merkezde olduğu bir Hexagonal Mimari ile yukarıda bahsedilen prensipleri birleştirebiliriz. Şekil 4.5, temel mimariyi göstermektedir. Bu yapıda, tüketiciler (consumers) hizmetlere REST, SOAP ve mesajlaşma (messaging) yoluyla erişir. Dikkat edilmesi gereken önemli bir nokta, Hexagonal tabanlı bir sistemin birden fazla teknik hizmet uç noktasını destekleyebilmesidir. Bu da SOA içinde DDD'nin nasıl kullanıldığına doğrudan etki eder.

SOA'nın ne olduğu ve ne tür bir değer sunduğu konusunda görüşler oldukça farklıdır, bu yüzden burada anlatılanlara katılmamanız şaşırtıcı olmaz. **Martin Fowler** bu durumu _"hizmet odaklı belirsizlik" (service-oriented ambiguity)_ olarak adlandırmaktadır. Bu yüzden, burada SOA’yı kesin bir şekilde tanımlamaya çalışmak yerine, ***SOA Manifestosu'nda belirtilen öncelikler ile DDD'nin nasıl uyum sağladığına dair bir bakış açısı sunacağım***.

İlk olarak, Manifesto'ya katkıda bulunanlardan biri tarafından ifade edilen pragmatik bakış açılarını dikkate almak önemli bir bağlam sağlamaktadır. Manifesto üzerine yorum yapan Tilkov, bizi SOA hizmetlerinin ne olabileceğini anlamaya en azından bir ya da iki adım daha yaklaştırıyor:

> _"[Manifesto] bana bir hizmeti (service) ya bir SOAP/WSDL arayüzleri seti ya da bir RESTful kaynak koleksiyonu olarak görme seçeneği sunuyor... Bu bir tanımlama girişimi değil—hepimizin üzerinde uzlaşabileceği değerleri ve prensipleri bulma çabasıdır."_

Stefan’ın yorumları dikkate değerdir. Bir fikir birliği sağlamak her zaman faydalıdır ve büyük ihtimalle bir iş hizmetinin (business service), çeşitli teknik hizmetler tarafından sağlanabileceği konusunda hemfikir olabiliriz.

Teknik hizmetler RESTful kaynakları, SOAP arayüzleri, Mesaj türleri olabilir. Business service, bir _business stratejisini_ temsil eder ve iş ile teknolojiyi birleştiren bir yaklaşımdır. Bununla birlikte, tek bir iş hizmeti, tek bir Alt Alan (Subdomain) veya Sınırlandırılmış Bağlam (Bounded Context) ile birebir eşleşmez. Şüphesiz, hem sorun alanı hem de çözüm alanı değerlendirmelerini gerçekleştirirken, bir business service'in her birinden bir dizi içerdiğini göreceğiz.  Bununla beraber Şekil 4.5, yalnızca tek bir Sınırlandırılmış Bağlamın mimarisini gösterir. Bu bağlam içinde bir dizi RESTful kaynak, SOAP arayüzleri ve Mesaj türleri tarafından sağlanan teknik hizmetler bulunur. Ancak geniş bir SOA çözümünde, birden fazla Sınırlandırılmış Bağlam (Bounded Context) yer almalıdır. Bu bağlamlardan her biri Hexagonal Mimariyi kullanabilir veya farklı bir mimari tercih edebilir. SOA veya DDD, teknik hizmetlerin nasıl tasarlanması ve dağıtılması gerektiğini kesin olarak belirlemez, çünkü birçok farklı seçenek mevcuttur.

DDD kullanırken amacımız, iyi tanımlanmış ve kapsamlı bir Sınırlandırılmış Bağlam (Bounded Context) oluşturmaktır. Mimari tercihlerimiz, alan modelinin (domain model) büyüklüğünü belirlememelidir. Eğer bir veya birkaç teknik hizmet uç noktası (örneğin, tek bir REST kaynağı, tek bir SOAP arayüzü veya tek bir mesaj türü), Bounded Context tanımlayan ana faktör haline gelirse, çok sayıda küçük Bounded Context'ler oluşturmak zorunda kalırız ve her biri yalnızca bir Entity ve küçük bir Aggregate içerebilir. Bu durumda, bir kurumsal sistem içinde yüzlerce küçük Sınırlandırılmış Bağlam oluşabilir.

Bazıları bu yaklaşımın teknik avantajları olduğunu düşünebilir, ancak bu durum stratejik DDD'nin temel hedeflerine aykırıdır. Eksiksiz ve kapsamlı Ortak Dil (Ubiquitous Language) oluşturmayı zorlaştırır. SOA Manifestosu'nun prensipleriyle de çelişebilir. Özellikle SOA Manifestosu'nun aşağıdaki iki temel ilkesi, DDD’nin stratejik yaklaşımıyla doğrudan örtüşmektedir:

1.  İş değeri, teknik stratejinin önünde gelir.
2.  Stratejik hedefler, projeye özgü faydalardan daha önemlidir.

Eğer bu ilkeleri benimsersek, *teknik bileşen mimarisi kararları (örneğin, REST mi SOAP mı kullanılacağı), DDD’nin model bölümlendirme (partitioning) sürecinde ana faktör olmamalıdır*.

---

SaaSOvation ekipleri zor ama önemli bir ders öğrenmek zorunda kaldı: *Dilsel faktörlere (linguistic drivers) odaklanmanın, DDD ile daha iyi uyum sağladığını fark ettiler.* Sahip oldukları üç Bounded Context, hem iş süreçleri hem de teknik hizmetler açısından SOA'nın hedefleriyle uyumludur.

---

Bounded Contexts (2), Context Maps (3) ve Integrating Bounded Contexts (13) bölümlerinde tartışılan üç örnek modelin her biri, tek bir dilsel olarak iyi tanımlanmış domain model'i temsil eder. Bu domain modellerinin her biri, iş hedeflerini karşılayan bir SOA'yı uygulayan açık hizmetler (open services) kümesiyle çevrelenmiştir.

## Temsili Durum Transferi—REST

***Stefan Tilkov tarafından katkıda bulunulmuştur***

REST, son birkaç yılın en çok kullanılan ve en çok yanlış anlaşılan mimari terimlerinden biri haline geldi. Her zamanki gibi, farklı insanlar REST kısaltmasını kullanırken farklı şeyleri kasteder.

- Bazıları, REST'in SOAP kullanmadan XML’i HTTP üzerinden göndermek anlamına geldiğini düşünür.
- Bazıları, REST'i HTTP ve JSON kullanmakla eşdeğer görür.
- Diğerleri, REST yapmak için metot argümanlarını URI sorgu parametreleri olarak göndermek gerektiğine inanır.

Tüm bu yorumlar yanlıştır. Ancak şanslıyız ki, birçok diğer kavramın (örneğin, "components" veya "SOA") aksine, REST’in ne anlama geldiğine dair otoriter bir kaynak vardır:  
- **Roy T. Fielding'in doktora tezi**, bu terimi ortaya atan ve çok net bir şekilde tanımlayan çalışmadır.

### REST Bir Mimari Stil Olarak

REST’i anlamanın ilk adımı, ***mimari stil*** kavramını kavramaktır. Mimari stil, mimari için neyse, tasarım deseni de belirli bir tasarım için odur. **Farklı somut uygulamalar arasında ortak olan yönleri soyutlayan bir yaklaşımdır** ve teknik detaylarda kaybolmadan avantajlarını tartışmaya olanak tanır. Dağıtık sistemler mimarisinde pek çok farklı mimari stil vardır. Örneğin, *İstemci-sunucu (client-server) mimarisi*, *Dağıtılmış nesne tabanlı mimari*. Fielding’in doktora tezinin ilk bölümleri, farklı mimari stilleri ve bunlara uyan bir mimarinin yerine getirmesi gereken **kısıtlamaları** açıklar. Bu mimari stiller ve kısıtlamalar teorik görünebilir ve bu doğrudur. Ancak bunlar, Fielding’in tanımladığı (o zamanlar) yeni bir mimari stilin temelini oluşturur. REST, yani Web’in mimarisinin uyum sağlaması gereken mimari stildir.

Elbette Web, yani onun en önemli standartları olan URI, HTTP ve HTML, Fielding’in doktora tezinden önce vardı. Ancak Fielding, HTTP 1.1’in standartlaştırılmasında önemli bir rol oynadı ve Web’in bugün bildiğimiz haliyle oluşmasını sağlayan tasarım kararlarında büyük bir etkiye sahipti.

Bu açıdan bakıldığında, **REST**, Web’in mimarisinin sonradan çıkarılan teorik bir genellemesidir.

REST Neden Web Servisleri ile Eş Anlamlı Hale Geldi? Peki neden bugün REST’i belirli bir sistem geliştirme yöntemiyle veya özellikle Web servisleri inşa etme biçimiyle özdeşleştiriyoruz? Bunun sebebi, **Web protokollerinin** farklı şekillerde kullanılabilmesidir. Bazı kullanım şekilleri, bu protokollerin orijinal tasarım hedeflerine uygundur. Bazıları ise bu hedeflerle uyumlu değildir. Bu durumu açıklamak için veritabanı yönetim sistemleri (RDBMS) dünyasından bir benzetme yapabiliriz:

✅ **Doğru kullanım**:  
Bir ilişkisel veritabanını (RDBMS), tablo, sütun, yabancı anahtar ilişkileri, görünümler, kısıtlamalar gibi kavramlara uygun olarak kullanırsınız.

❌ **Yanlış kullanım**:  
Tek bir tablo oluşturup, içinde yalnızca "key" ve "value" adında iki sütun tanımlarsınız. Sonra da tüm veriyi serialized nesneler halinde "value" sütununa koyarsınız. Böyle yaptığınızda hâlâ bir RDBMS kullanıyor olursunuz, ancak sistemin sunduğu sorgulama, join, sıralama ve gruplama gibi birçok avantajı kaybedersiniz.

Aynı durum Web protokolleri için de geçerlidir. Web protokolleri, onları oluşturan temel fikirlere uygun olarak REST mimari stiline uygun kullanılabilir. Ya da bu prensiplere uyulmadan, **REST olmayan bir şekilde kullanılabilir.
 
💡 Eğer **HTTP’yi "RESTful" bir şekilde kullanmayacaksak**, Web tabanlı dağıtık sistemler yerine **başka bir mimari model** tercih etmek daha mantıklı olabilir.  

💡 Tıpkı **anahtar-değer (key-value) bazlı veri saklama** işlemlerinin, **NoSQL** gibi alternatif çözümlerle daha verimli yapılabileceği gibi.

Evet, çeviriye ek olarak açıklamalar da ekledim. Sadece çeviri istiyorsan, doğrudan çeviri yapabilirim:

### RESTful HTTP Sunucusunun Temel Unsurları

Peki, “RESTful HTTP” kullanan bir dağıtım mimarisinin temel unsurları nelerdir? Öncelikle, sunucu tarafına bakalım. Burada, bir insanın bir web tarayıcısı aracılığıyla bir sunucuyu kullanması (bir “Web uygulaması”) ile başka bir istemcinin, örneğin seçtiğiniz bir programlama diliyle yazılmış bir istemcinin (bir “Web servisi”) kullanması arasında herhangi bir fark olmadığını unutmamalıyız.

⚠️ Öncelikle, **kaynaklar (resources)** temel bir kavramdır. Peki nasıl? Bir sistem tasarımcısı olarak, dış dünyaya erişilebilir hale getirmek istediğiniz **anlamlı varlıkları** belirlersiniz ve her birine **benzersiz bir kimlik** atarsınız. Genel olarak, **her kaynak bir URI'ye sahiptir ve daha da önemlisi, her URI bir kaynağa işaret etmelidir**—yani dış dünyaya açtığınız varlıklar bireysel olarak adreslenebilir olmalıdır.

Örneğin, her müşteri, her ürün, her ürün listesi, her arama sonucu ve belki de ürün kataloğundaki her değişiklik başlı başına bir kaynak olabilir. Kaynakların, bir veya daha fazla formatta temsilleri bulunur. İstemciler, bir XML veya JSON belgesi, bir HTML form post verisi ya da ikili bir format gibi temsiller aracılığıyla kaynaklarla etkileşime girerler.

Bir sonraki önemli unsur, **durumsuz iletişim (stateless communication) ve kendini tanımlayan mesajlar (self-descriptive messages)** fikridir. Bir HTTP isteği, sunucunun işlemi gerçekleştirmesi için gereken tüm bilgileri taşır. Elbette sunucu kendi kalıcı durumunu kullanabilir, ancak istemci ve sunucu, ayrı taleplerin bir bağlam (oturum) oluşturmasını gerektiren bir sisteme dayanamaz. Bu, her kaynağa diğer taleplerden bağımsız olarak erişilebilmesini sağlar ve büyük ölçeklenebilirlik avantajı getirir.

Kaynakları **nesneler** olarak düşünmek de mümkündür—ve aslında bu mantıklı bir yaklaşımdır. Ancak bu nesnelerin nasıl bir arayüze sahip olması gerektiği sorusu, REST’in diğer dağıtılmış sistem mimarilerinden ayrıştığı önemli bir noktadır. Burada, çağırılabilecek metotların kümesi sabittir ve tüm nesneler aynı arayüzü destekler. RESTful HTTP'de bu metotlar **HTTP fiilleridir—özellikle `GET, PUT, POST ve DELETE`.**

İlk bakışta bu metodlar **CRUD (Create, Read, Update, Delete) işlemleriyle birebir aynı gibi görünebilir**, ancak aslında durum böyle değildir. Kalıcı bir varlığı temsil etmeyen ve belirli bir işlem uygulayan kaynaklar oluşturmak oldukça yaygındır. HTTP metodlarının her biri, HTTP spesifikasyonunda oldukça net bir şekilde tanımlanmıştır. Örneğin:
- **GET metodu** yalnızca “güvenli” (safe) işlemler için kullanılmalıdır, 
	- (1) İstemcinin açıkça talep etmediği bir etki yaratmamalıdır,  
	- (2) Her zaman veri okuma işlemidir,  
	- (3) Önbelleğe alınabilir (sunucu uygun yanıt başlıklarıyla bunu belirttiğinde).

**Don Box** (SOAP Web servislerinin önde gelen isimlerinden biri), **HTTP’nin GET metodunun dünyadaki en optimize edilmiş dağıtılmış sistem altyapılarından biri olduğunu** söylemiştir. Bu da, Web’in ölçeklenebilirliği ve performansının büyük ölçüde HTTP’nin bu optimizasyonlarına dayandığını gösterir.

Bazı HTTP metodları ⓘ ***idempotent***'tir, yani **bir hatayla karşılaşıldığında veya sonucu belirsiz olduğunda tekrar güvenle çağrılabilirler.** Bu `GET`, `PUT` ve `DELETE` için geçerlidir.

ⓘ Son olarak, RESTful bir sunucu, istemcinin uygulamanın olası durum geçişlerini keşfetmesini sağlamak için hipermedyayı kullanır. Bu, Fielding'in tezinde **“Uygulama Durumunun Motoru Olarak Hipermedya (HATEOAS)”** olarak adlandırılır. Daha basit bir ifadeyle, **bireysel kaynaklar bağımsız değildir; birbirine bağlıdır.** Bu şaşırtıcı bir durum değildir—sonuçta Web’in adı da buradan gelir. Bir RESTful sunucu, yanıtlarına bağlantılar ekleyerek istemcinin bağlı kaynaklarla etkileşime girmesine olanak tanır.

### RESTful HTTP İstemcisinin Temel Unsurları

Bir RESTful HTTP istemcisi, bir kaynaktan diğerine geçiş yaparken ya kaynak temsillerinde bulunan bağlantıları takip eder ya da sunucuya veri göndererek işlem yaptığında yönlendirilir. Sunucu ve istemci, istemcinin dağıtım davranışını dinamik olarak etkilemek için iş birliği yapar. Bir URI, bir adresi çözümlemek için gerekli tüm bilgileri içerir—ana bilgisayar adı (host name) ve port dahil—. Hipermedya ilkesini takip eden bir istemci, sonunda farklı bir uygulama, farklı bir ana bilgisayar veya hatta farklı bir şirket tarafından barındırılan bir kaynağa erişebilir.

<ins>*İdeal bir REST yapısında*</ins>, istemci **önceden belirlenmiş tek bir URI ile başlar** ve ardından **hipermedya kontrollerini takip ederek işlem yapar**. **Bu model, tarayıcıların HTML içeriklerini işleyerek ve kullanıcıya bağlantılar ve formlar sunarak çalıştığı modelin aynısıdır.** Tarayıcı, kullanıcının girdilerini alarak birçok farklı Web uygulamasıyla etkileşime girer—üstelik bu uygulamaların arayüzü veya iç uygulama detayları hakkında önceden bilgi sahibi olmadan.

Elbette, bir tarayıcı tamamen bağımsız bir ajan değildir**—kararları almak için bir insana ihtiyaç duyar. Ancak, programlanmış bir istemci de aynı ilkeleri benimseyebilir. **Bazı mantıklar doğrudan kodlanmış olsa bile, istemci belirli URI yapılarını varsaymak veya tüm kaynakların aynı sunucuda bulunacağını düşünmek yerine bağlantıları takip eder ve bir ya da daha fazla medya türü hakkındaki bilgisini kullanır.

### REST ve DDD

Cazip görünse de, **bir domain modelini doğrudan RESTful HTTP üzerinden açığa çıkarmak önerilmez.** Bu yaklaşım genellikle sistem arayüzlerinin gereğinden daha kırılgan olmasına neden olur, çünkü domain modelindeki her değişiklik doğrudan sistem arayüzüne yansır. DDD ve RESTful HTTP’yi birleştirmek için iki alternatif yaklaşım bulunmaktadır.

<ins>*İlk yaklaşım*</ins>, sistemin arayüz katmanı için ayrı bir Bounded Context oluşturmaktır ve bu arayüz modeli üzerinden gerçek Core Domain’e erişmek için uygun stratejiler kullanılır. Bu klasik bir yaklaşımdır çünkü sistemin arayüzünü, uzak servisler veya remote interface’ler yerine kaynak soyutlamaları kullanarak açığa çıkan bütünleşik bir yapı olarak görür.

Bu yaklaşımı somut bir örnekle ele alalım. Bir çalışma grubunu yöneten bir sistem inşa ediyoruz. Bu sistem, görevleri, programları/randevuları, alt grupları ve bunların yönetimi için gerekli tüm süreçleri kapsıyor. Infrastructure detaylarından bağımsız saf bir domain modeli tasarlıyoruz. Bu model, Ubiquitous Language’i yakalar ve gerekli iş mantığını uygular. Bu titizlikle tasarlanmış domain modeline bir arayüz sağlamak için RESTful kaynaklardan oluşan bir uzak arayüz sunarız. Bu kaynaklar, istemcinin ihtiyaç duyduğu kullanım senaryolarını yansıtır—ki bu, saf domain modelinden oldukça farklı olabilir. Ancak, her kaynak Core Domain’e ait bir veya daha fazla Aggregate kullanılarak oluşturulur.

Elbette, JAX-RS kaynak metodlarına domain nesnelerini doğrudan parametre olarak verebiliriz. Örneğin, `/:user/:task` URI’si `getTask()` metoduna eşlenerek bir `Task` nesnesi döndürebilir. **Bu basit gibi görünebilir, ancak büyük bir sorun içerir**. `Task` nesnesinin yapısında yapılan herhangi bir değişiklik, remote interface'e anında yansır ve birçok istemciyi bozabilir—üstelik değişiklik dış dünyayla tamamen ilgisiz olsa bile. Bu iyi bir durum değildir.

Bu nedenle ilk yaklaşım tercih edilir: Core Domain ile sistem arayüz modelini birbirinden ayırmak. Böylece, Core Domain’de değişiklik yapıldığında bu değişikliğin sistem arayüz modeline yansıtılması gerekip gerekmediğine ve nasıl bir eşleme kullanılacağına ayrı ayrı karar verebiliriz. Bu yaklaşımda, sistem arayüz modeli için tasarlanan sınıflar genellikle Core Domain tarafından yönlendirilse de, kullanım senaryoları esas belirleyici faktördür. ***Not: Bu yaklaşımda bile özel bir medya türü (custom media type) tanımlayabiliriz.***

<ins>*İkinci yaklaşım*</ins>, standart medya türlerine daha fazla önem verildiğinde uygundur. Eğer geliştirilen medya türleri sadece tek bir sistem arayüzünü değil, belirli bir kategoriye ait istemci-sunucu etkileşimlerini desteklemek için tasarlanıyorsa, her standart medya türünü temsil eden bir domain modeli oluşturulabilir. Bu domain modeli istemciler ve sunucular arasında yeniden kullanılabilir, ancak bazı REST ve SOA savunucuları bunu **anti-pattern** olarak görmektedir.   ***Not: Bu yaklaşım DDD terminolojisinde bir Shared Kernel veya Published Language olarak değerlendirilebilir.***

Bu yaklaşım daha çok dıştan içe doğru ilerleyen, yatay kesitli bir yaklaşımdır. Önceki çalışma grubu ve görev yönetimi örneğinde, birçok yaygın format bulunur. Örneğin, *ical (iCalendar)* formatını ele alalım. Bu pek çok farklı uygulama tarafından kullanılabilen genel bir formattır. Bu durumda, önce bir medya türü (ical) seçeriz, ardından bu format için bir domain modeli oluştururuz. Bu model, yalnızca sunucu uygulamamız için değil, aynı formatı anlaması gereken diğer sistemler (örneğin bir Android istemcisi) için de kullanılabilir. Ancak, bu yaklaşımda sunucunun birçok farklı medya türüyle uğraşması gerekebilir ve aynı medya türü birden fazla sunucu tarafından kullanılabilir.

Hangi yaklaşımın seçileceği büyük ölçüde sistem tasarımcısının yeniden kullanılabilirlik hedeflerine bağlıdır. Çözüm ne kadar özelleşmişse, ilk yaklaşım (Bounded Context kullanımı) o kadar faydalı olur. Çözüm ne kadar genel ve standartlaşmışsa, ikinci medya türü odaklı yaklaşım o kadar mantıklı hale gelir—bu yaklaşımın en uç noktası ise resmi bir standart kuruluşu tarafından kabul edilen bir format olmaktır.

### Neden REST?

Deneyimlerime göre, **REST prensiplerine uygun olarak tasarlanmış bir sistem, loose coupling vaadini yerine getirir**. Genel olarak, yeni kaynaklar eklemek ve mevcut kaynak temsillerine bağlantılar eklemek oldukça kolaydır. Ayrıca, gerektiğinde yeni formatlara destek eklemek de basittir**, bu da **sistemdeki bağlantıları çok daha az kırılgan hale getirir.

**REST tabanlı bir sistem çok daha anlaşılırdır**, çünkü daha küçük parçalara—kaynaklara—bölünmüştür. Her kaynak ayrı ayrı test edilebilir, hata ayıklanabilir ve bağımsız bir giriş noktası olarak kullanılabilir.

HTTP’nin tasarımı ve URI yeniden yazma ile önbellekleme gibi özellikleri destekleyen araçların olgunluğu, RESTful HTTP’yi hem gevşek bağlanırlık hem de yüksek ölçeklenebilirlik gerektiren mimariler için harika bir seçenek haline getirir.

## Command-Query Sorumluluğu Ayrımı (CQRS)

Depolar (Repositories) üzerinden kullanıcıların görmek istediği tüm verileri sorgulamak zor olabilir. Bu özellikle, kullanıcı deneyimi tasarımının birden fazla Küme (Aggregate) türü ve örneği arasında bölünmüş veri görünümleri oluşturduğu durumlarda geçerlidir. Domain model ne kadar karmaşıksa, bu durum o kadar sık karşılaşılır.

Sadece Depolar kullanarak bu sorunu çözmek ideal olmayabilir. Tüm gerekli Aggregate örneklerini almak için istemcilerin birden fazla Repository kullanmasını gerektirebiliriz, ardından sadece ihtiyaç duyulan verileri bir **Veri Transfer Nesnesi (DTO - Data Transfer Object)** içinde birleştirebiliriz [Fowler, P of EAA]. Alternatif olarak, farklı Repository'lerde özel arama metotları (finders) tasarlayarak, tek bir sorgu ile parçalı verileri bir araya getirebiliriz. Bu çözümler uygunsuz görünüyorsa, kullanıcı deneyimi tasarımından ödün vermemiz gerekebilir ve görünümleri Aggregate sınırlarına sıkı sıkıya uydurmamız gerekebilir. Ancak, çoğu kişi uzun vadede böyle mekanik ve katı bir kullanıcı arayüzünün yeterli olmayacağı konusunda hemfikirdir.

Peki, domain model'den view'lere veri eşlemeyi tamamen farklı bir şekilde ele alabilir miyiz? **Cevap, CQRS olarak bilinen mimari desende yatıyor**. Bu desen, sıkı bir nesne (veya bileşen) tasarım prensibi olan Command-Query Separation - CQS mimari seviyeye taşımaktan doğmuştur.

<ins>*Bu prensip, Bertrand Meyer tarafından geliştirilmiştir ve şunu iddia eder:*</ins>

> Her metot, ya bir işlem (command) olmalı ve bir eylem gerçekleştirmeli, ya da bir sorgu (query) olmalı ve çağrıyı yapan tarafa veri döndürmelidir, ancak ikisini birden yapmamalıdır. Başka bir deyişle, bir soru sormak cevabı değiştirmemelidir. Daha resmi olarak, bir metot yalnızca referans şeffaflığına sahipse ve yan etkileri yoksa bir değer döndürmelidir.

ⓘ Bir nesne seviyesinde bu şu anlama gelir:

1.  Eğer bir metot nesnenin durumunu değiştiriyorsa, bir komuttur (command) ve herhangi bir değer döndürmemelidir. Java ve C#’ta bu metodun dönüş tipi `void` olmalıdır.
    
2.  Eğer bir metot bir değer döndürüyorsa, bir sorgudur (query) ve doğrudan ya da dolaylı olarak nesnenin durumunu değiştirmemelidir. Java ve C#’ta bu metot, döndürdüğü değerin türüyle tanımlanmalıdır.

Bu oldukça net bir yönergedir ve ona bağlı kalmanın hem teorik hem de pratik faydaları vardır. Ancak, Mimari bir desen olarak bunu DDD'de kullanırken neden ve nasıl uygularız?

Şimdi, Bounded Contexts) içinde yer alan bir domain model'i gözünüzde canlandırın. Normalde Kümeler (Aggregates), hem komut hem de sorgu metotlarına sahip olur. Ayrıca, belirli özelliklere göre filtreleme yapabilen çeşitli bulucu (finder) metotları içeren Depolar (Repositories) bulunur. **CQRS ile, bu "normal" yaklaşımları terk ediyor ve veri sorgulama işini tamamen farklı bir şekilde tasarlıyoruz**.

Öncelikle, **modelde geleneksel olarak bulunan tüm saf query sorumluluklarını, yalnızca commands çalıştıran sorumluluklardan ayırıyoruz. Kümeler (Aggregates), artık query metotları (getter’lar) içermeyecek, yalnızca command metotlarına sahip olacak.** 

Repository, sadece bir `add()` veya `save()` metodu içerecek (hem oluşturma hem de güncellemeyi desteklemek için) ve yalnızca tek bir sorgu metoduna sahip olacak: `fromId()`. Bu tek sorgu metodu, bir Küme’nin (Aggregate) benzersiz kimliğini alıp onu döndürecek Repository artık belirli özelliklere göre filtreleme yaparak Küme (Aggregate) bulamayacak. Tüm bu sorgu yetenekleri modelden kaldırıldığında, bu model artık bir ***"command model"*** olarak adlandırılır. Ancak, kullanıcıya veri gösterebilmek için hala bir yol gereklidir. Bu yüzden, tamamen sorgular için optimize edilmiş ikinci bir model oluşturuyoruz: ***"query model"*** .

> ***Bu Fazladan Karmaşıklık mı Getiriyor?***
> 
> Bu yaklaşım fazladan iş gibi görünebilir ve bir dizi sorunu çözerken başka bir dizi problem ekliyormuşuz gibi hissedebilirsiniz. Ancak bu yöntemi hemen göz ardı etmemek gerekir.
> CQRS, yalnızca belirli bir "görünüm karmaşıklığı" sorununu çözmek için tasarlanmıştır. Yeni ve "havalı" bir yaklaşım olarak sırf özgeçmişe eklenmek için uygulanmamalıdır.

> ***Farklı İsimlerle Bilinen Kavramlar***
> 
> CQRS içindeki bazı bileşenlerin farklı isimlerle anıldığını da bilmek önemlidir:
> - ***Query model***, read model olarak da adlandırılır.
> - ***Command model***, write model olarak da bilinir.

Sonuç olarak, geleneksel domain model ikiye bölünecektir. **Command model** bir depoda, **Query model** ise başka bir depoda tutulur. Bunun sonucunda şekil 4.6'da gösterilen bileşenler kümesine benzer bir yapı elde ederiz. Bu deseni daha net anlamak için birkaç ek detay daha gereklidir.

### CQRS’nin Alanlarını İnceleme

Bu desenin ana alanlarını tek tek ele alalım. Öncelikle istemci ve sorgu desteğiyle başlayıp, ardından komut modeline ve sorgu modelinin nasıl güncellendiğine kadar ilerleyelim.

![Figure 4.6](./images/chapter4/figure-4-6.png)

**Figure 4.6:** CQRS ile istemcilerden gelen komutlar komut modeline tek yönlü olarak gider. Sorgular, sunum için optimize edilmiş ayrı bir veri kaynağına karşı çalıştırılır ve kullanıcı arayüzü veya raporlar olarak sunulur.

***İstemci ve Sorgu İşlemcisi***

İstemci (şemada en solda yer alır) bir Web tarayıcısı veya özel bir masaüstü kullanıcı arayüzü olabilir. Bir sunucuda çalışan bir dizi sorgu işlemcisi kullanır. Şema, sunucu(lar)daki katmanlar arasında mimari olarak önemli bölümleri göstermez. Var olan katmanlar ne olursa olsun, sorgu işlemcisi, bir veritabanında temel sorguları çalıştırmayı bilen basit bir bileşeni temsil eder; örneğin bir SQL deposu.

Burada karmaşık katmanlar yoktur. En fazla, bu bileşen sorgu deposu veritabanında bir sorgu çalıştırır ve belki de sorgu sonucunu taşımak için bir formata (belki bir DTO, ama belki de değil) serileştirir, eğer gerekliyse. Eğer istemci Java veya C# ile çalışıyorsa, veritabanını doğrudan sorgulayabilir. Ancak bu, her bağlantı için bir veritabanı istemci lisansı gerektirebilir. Bağlantı havuzu kullanan bir sorgu işlemcisi kullanmak, en iyi seçenektir.

Eğer istemci bir veritabanı sonuç kümesini (örneğin, JDBC türünde) tüketecekse, serileştirme gereksiz olabilir ama yine de istenebilir. Burada iki düşünce okulu vardır. Birincisi, nihai sadeliğin, sonuç kümesinin veya bunun çok temel bir şekilde wireframe (tasarım-UI) uyumlu serileştirilmiş halinin (XML veya JSON) istemci tarafından tüketilmesini gerektirdiğini savunur. Diğerleri ise DTO’ların oluşturulup istemci tarafından tüketilmesi gerektiğini savunur. Bu, bir zevk meselesi olabilir, ancak her zaman DTO’lar ve DTO Derleyicileri [Fowler, P of EAA] eklediğimizde karmaşıklık artar ve gerçekten gerekmedikçe bunlar kazara eklenmiş karmaşıklıklar olur. Her takım, hangi yaklaşımın projeleri için en iyi olduğunu belirler.

*** 184. sayfa