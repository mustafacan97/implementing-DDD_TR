# Bölüm 2 - Domains, Subdomains and Bounded Contexts

Üç temel kavramı çok net bir şekilde anlamanız gerekecek:

-   Alanınızın (Domain) ne olduğunu,
-   Alt alanlarınızın (Subdomains) neler olduğunu,
-   Sınırlandırılmış bağlamlarınızın (Bounded Contexts) nasıl çalıştığını.

Bu kavramların [Evans] kitabının ikinci yarısında detaylı bir şekilde ele alınmış olması, onların ikinci planda olduğu anlamına gelmez. **DDD’yi başarılı bir şekilde uygulamak istiyorsanız, bu kavramları doğru bir şekilde anlamanız şarttır.**

---

> **Bu Bölümdeki Yol Haritası**
>
> - DDD’nin büyük resmini kavrayarak Alanlar, Alt Alanlar ve Sınırlandırılmış Bağlamları anlayın.
> - Stratejik tasarımın neden bu kadar önemli olduğunu ve onsuz yapılan tasarımın neden sorunlara yol açtığını öğrenin.
> - Gerçek dünyadan, birden fazla Alt Alana sahip pratik bir Alan inceleyin.
> - Bounded Context'leri hem kavramsal hem de teknik olarak anlamlandırın.
> - SaaSOvation ekibinin stratejik tasarımı keşfederken yaşadığı "aha!" anlarını görün.

## Büyük Resim

**Alan (Domain)** geniş anlamda, bir organizasyonun yaptığı işi ve bunu gerçekleştirdiği dünyayı ifade eder. İşletmeler bir pazar belirler ve ürünler veya hizmetler satar. Her organizasyonun kendine özgü bir bilgi birikimi ve iş yapma yöntemi vardır. Bu bilgi birikimi ve operasyonlarını yürütme yöntemleri, organizasyonun **alanıdır (Domain).**

Bir organizasyon için yazılım geliştirdiğinizde, **o organizasyonun alanında çalışıyorsunuz demektir.** Alanınızın ne olduğu sizin için oldukça açık olmalıdır; çünkü zaten içinde çalışıyorsunuz.

Ancak dikkat edilmesi gereken bir nokta var: "Alan" terimi bazen farklı anlamlarda kullanılabilir. Alan, hem işletmenin tamamını ifade edebilir hem de sadece belirli bir çekirdek veya destekleyici bölümü gösterebilir. Bu kitap boyunca, terimi hangi anlamda kullandığımı netleştirmeye özen göstereceğim. Eğer yalnızca işletmenin belirli bir bölümünden bahsediyorsam, genellikle **"Çekirdek Alan (Core Domain)", "Alt Alan (Subdomain)"** gibi ifadeler kullanacağım.

**Alan Modeli (Domain Model)** teriminde "alan" kelimesi geçtiği için, organizasyonun tüm iş alanını kapsayan büyük, tek bir model oluşturmamız gerektiği gibi bir izlenim edinebiliriz. Yani, bir kurumsal model (Enterprise Model) gibi düşünebiliriz. Ancak DDD'de amaç kesinlikle bu değildir. Tam tersine, DDD **büyük resmi daha küçük, yönetilebilir parçalara bölmeye odaklanır.**

Bir organizasyonun tamamı birden fazla Alt Alandan (Subdomains) oluşur. DDD ile yazılım geliştirirken, modellerimizi belirli Sınırlandırılmış Bağlamlar (Bounded Contexts) içinde oluştururuz. Aslında, Alan Modeli oluşturmak, işletmenin tamamına değil, yalnızca belirli bir kısmına odaklanmamıza yardımcı olan bir yöntemdir.

Orta veya büyük ölçekli bir işletmenin tüm iş süreçlerini tek bir modelde tanımlamaya çalışmak aşırı derecede zor olacak ve büyük olasılıkla başarısızlıkla sonuçlanacaktır. Bu bölümde de açıkça göreceğiniz gibi, **iş alanının farklı bölümlerini kesin çizgilerle ayırmak, başarıya ulaşmamız için kritik öneme sahiptir.**

***Peki, bir Alan Modeli (Domain Model) tam olarak ne olmalıdır?***

Neredeyse her yazılım alanı (Domain) birden fazla Alt Alana (Subdomains) sahiptir. Organizasyon devasa ve karmaşık da olsa, küçük ve basit de olsa, işletmenin başarılı olmasını sağlayan farklı işlevler vardır. Bu işlevleri ayrı ayrı düşünmek büyük avantaj sağlar.

### Subdomains ve Bounded Contexts at Work

Alt Alanların (Subdomains) nasıl kullanılabileceğini göstermek için oldukça basit bir örnekle başlayalım. **Çevrimiçi (online) ürün satan bir perakende şirketi düşünelim.** Şirketin sattığı ürünler herhangi bir şey olabilir, bu yüzden ürünler üzerinde çok fazla düşünmemize gerek yok. Bu alanda iş yapabilmek için şirketin yerine getirmesi gereken temel işlevler şunlardır:

- Müşterilere bir ürün kataloğu sunmak,
- Sipariş verilmesine izin vermek,
- Satılan ürünler için ödeme almak,
- Ürünleri alıcılara göndermek (sevkiyat).

Bu çevrimiçi perakendecinin **alanı (Domain)**, dört ana alt alandan (Subdomains) oluşuyor gibi görünüyor:

1.  Ürün Kataloğu (Product Catalog)
2.  Sipariş Yönetimi (Orders)
3.  Faturalandırma (Invoicing)
4.  Sevkiyat (Shipping)

![Figure 2.1: A Domain with Subdomains and Bounded Contexts](https://i.sstatic.net/S3KV7l.png)
**Figure 2.1:** A Domain with Subdomains and Bounded Contexts

Şimdiye kadar her şey oldukça basit görünüyor. Ancak tek bir ekstra detay eklersek, örneğimiz biraz daha karmaşık hale gelecek. **Şirketin bir de Stok Yönetimi (Inventory) ile ilgilenmesi gerektiğini düşünelim.** Bu noktada, sistemin fiziksel alt sistemleri ve mantıksal Alt Alanlarını inceleyelim.

Bu perakendecinin alanını (Domain) gerçekleştirmek için kullanılan üç fiziksel sistem mevcut ve bunlardan yalnızca ikisi şirket içinde barındırılıyor. Bu iki iç sistem, iki farklı Sınırlandırılmış Bağlam (Bounded Contexts) olarak düşünülebilir. Ancak, günümüzde çoğu sistem **DDD yaklaşımıyla tasarlanmadığı için**, tek bir sistem birçok farklı işlevden sorumlu hale gelebiliyor. Bu, yaygın ama problemli bir durumdur.

Örneğin, E-Ticaret Sınırlandırılmış Bağlamı (e-Commerce Bounded Context) içinde, birden fazla iç içe geçmiş alan modeli (Domain Model) bulunmaktadır. Ancak bu modeller temiz bir şekilde ayrılmamıştır. Aksine, tek bir yazılım modeli içinde birleştirilmişlerdir, ki bu oldukça kötü bir durumdur.

Eğer perakendeci şirket **bu E-Ticaret sistemini dışarıdan satın almış olsaydı**, bu kadar büyük bir sorun olmayabilirdi. Ancak bu sistemi bakımını üstlenen ekip, zamanla artan karmaşıklığın olumsuz etkilerini hissetmeye başlamıştır. **Ürün Kataloğu, Sipariş Yönetimi, Faturalandırma ve Sevkiyat modellerinin** tek bir büyük e-ticaret modeli içinde birleştirilmesi nedeniyle, her bir işlevin geliştirilmesi diğerlerini engellemeye başlamıştır. Özellikle de yeni bir büyük özellik eklenmek istendiğinde, mevcut modellerin birbirine olan bağımlılıkları büyük bir engel yaratacaktır.

***Neden Tek Bir Büyük Sistem Problem Yaratır?***

Ne yazık ki pek çok yazılım geliştiricisi, her şeyi tek bir sistem içine dahil etmenin akıllıca olduğunu düşünür. Bunun sonucunda "her şeyi bilen, her şeyi yapan" devasa e-ticaret sistemleri ortaya çıkar. Bu yaklaşım, her ihtiyacı karşılayabilecekmiş gibi görünebilir, ancak aslında büyük bir yanılgıdır. **Ne kadar çok işlev tek bir sisteme yığılırsa yığılsın, hiçbir zaman tüm kullanıcıların ihtiyaçlarını tam anlamıyla karşılayamaz.** Ayrıca, farklı Alt Alanlara (Subdomains) ait yazılım modellerinin birbirinden ayrılmaması, sistemin bakımını ve değişiklik yapılmasını aşırı derecede zorlaştırır. Çünkü:

- Her bileşen birbirine bağımlıdır.
- Bir yerde yapılan değişiklik, beklenmedik hatalara yol açabilir.
- Yeni özellikler eklemek giderek zorlaşır.

***DDD ile Karmaşıklığın Üstesinden Gelmek***

DDD’nin stratejik tasarım araçlarını kullanarak, bu iç içe geçmiş modelleri mantıksal olarak ayrılmış Alt Alanlara (Subdomains) bölebiliriz. Şekil 2.1’de görüldüğü gibi, **bu ayrımları kesikli çizgilerle belirtebiliriz.** Bu noktada, üçüncü taraf sistemleri temiz bir şekilde refaktör etmiş değiliz. Ancak bu sistemlerin nasıl ayrılması gerektiğini tanımladık. Böylece, **mantıksal Alt Alanları (Subdomains) belirleyerek iş süreçlerini daha iyi yönetebilir ve hangi alanların hangi fiziksel Sınırlandırılmış Bağlamlara (Bounded Contexts) bağlı olduğunu açıkça görebiliriz.**

***İşletme Açısından Bakıldığında Zorluklar***

Şimdi teknik karmaşıklıklardan **işletmenin karşılaştığı iş zorluklarına** geçelim. Bu küçük şirketin:

-  Sınırlı bütçesi var.
-  Sınırlı depo alanı var.
-  Sürekli bir dengeleme süreci içinde.

Şirket, çok fazla satmayan ürünlere aşırı harcama yapmamalıdır. Çünkü bazı ürünler belirli dönemlerde daha fazla satarken, diğer zamanlarda durgunluk gösterebilir. Eğer bazı ürünler planlandığı gibi satılmazsa, şirketin fonları müşteri talebi olmayan ürünlere bağlanmış olur ve para adeta donmuş hale gelir. Bu da şirketin, o an talep gören ürünleri stoklamak için yeterli alan bulamaması anlamına gelir.

Bu kadarla da bitmiyor. Başka bir sorun daha ortaya çıkıyor. Bazı ürünler beklenenden daha hızlı satıldığında, şirket bu ürünlerden yeterince stok yapamayabilir ve bu da müşteri taleplerini karşılamada yetersiz kalmasına neden olabilir. Yetersiz stok sorunu, müşterilerin acil olarak ihtiyaç duydukları bu ürünleri başka yerlerden temin etmelerine yol açabilir. Evet, bazı ürün toptancıları perakendeci adına doğrudan sevkiyat (drop-shipping) yapmaya isteklidir, ancak bu seçenek daha pahalıdır ve beraberinde istenmeyen başka sonuçlar da getirebilir. Bazı maliyet düşürme stratejileri, bazı ürünleri yerel olarak stoklamayı, uzak bölgelere daha iyi satılan diğer ürünleri ise doğrudan sevk etmeyi gerektirir. Bu yüzden, doğrudan sevkiyat (drop-shipping), yalnızca başarısız olmuş bir satışı kurtarmak için son anda başvurulan bir yöntem olmamalıdır.

Sonuçta, **çok satan ürünler aslında kıt olduğu için değil, perakende şirketi bunları en iyi şekilde stoklayamadığı için müşterilere hızlıca ulaştırılamıyor.** Eğer müşteriler sürekli gecikmeler yaşarsa, bu çevrimiçi satış şirketinin kazandığı rekabet avantajını kaybetmesine yol açabilir.

Ancak şunu da açıkça belirtelim: Stok yönetimiyle ilgili karşılaşılan zorlukların sınırlarını tam olarak araştırmış değiliz. Bu olumsuz durumlar yalnızca küçük ölçekli perakendeciler için geçerli değildir. Bütün perakendeciler, maliyetleri en aza indirirken stoklarını tam olarak ihtiyaçlarına uygun şekilde satın almak ve yönetmek ister. Yine de, küçük ölçekli perakendeciler, düşük performansın getirdiği dezavantajları büyük ölçekli perakendecilere kıyasla çok daha hızlı hisseder.

Herhangi bir çevrimiçi perakendeci için en büyük avantajlardan biri, gelecekteki stok ve satış taleplerini geçmiş eğilimlere göre tahmin edebilmek olurdu. Eğer bir perakendeci, **stok ve satış geçmişi verilerini işleyebilen bir tahmin motoru (forecasting engine) kullanabilseydi**, stoklarını optimize etmek için net tahminler elde edebilirdi:
- Ne zaman sipariş vermeli?
- Hangi üründen ne kadar sipariş etmeli?

Küçük bir perakendecinin böyle bir tahmin sistemini geliştirmesi muhtemelen yeni bir **"Temel Alan (Core Domain)"** oluşturmasını gerektirir. Çünkü bu, çözülmesi kolay bir problem değildir ve başarılı olunursa şirkete büyük bir rekabet avantajı kazandırabilir. Gerçekten de, Şekil 2.1'deki üçüncü fiziksel Sınırlandırılmış Bağlam (Bounded Context), harici bir **Tahminleme Sistemi**’dir **(External Forecasting System)**.

- Orders Subdomain ve Inventory Bounded Context, geçmiş ürün satışları ve iadeleri hakkında veri sağlamak için Tahminleme Sistemi ile entegre olur.
- Ayrıca, Catalog Subdomain, küresel olarak tanınan barkodları (product barcodes) sağlamalıdır.
	- Böylece, Tahminleme Sistemi, küçük ölçekli perakendecinin ürünlerini küresel satış trendleriyle karşılaştırabilir.
    - Bu da, daha geniş bir bakış açısı sunarak, en doğru stoklama miktarlarını hesaplamasına yardımcı olur.

Eğer bu yeni çözüm gerçekten bir "Temel Alan (Core Domain)" olacaksa (ki büyük olasılıkla öyledir), bu alanı geliştiren ekibin iş alanını, Alt Alanları (Subdomains) ve gerekli entegrasyonları iyi anlaması çok önemli olacaktır. Bu yüzden, Şekil 2.1’de gösterilen mevcut entegrasyonların belirlenmesi, projenin başlangıcında durumu net bir şekilde kavramak için kilit rol oynar.

Her zaman Alt Alanların (Subdomains) büyük ve işlevsel olarak kapsamlı modeller içermesi gerekmez. Bazen bir Alt Alan, yalnızca birkaç algoritmadan oluşan küçük bir sistem olabilir. Bu algoritmalar, iş çözümü açısından kritik olabilir, ancak "Temel Alan (Core Domain)" içinde yer almak zorunda değildir. İyi bir DDD yaklaşımı uygulandığında, bu tür basit Alt Alanlar, **Modüller (Modules)** kullanılarak Temel Alan’dan ayrılabilir ve ağır bir mimari bileşen içinde barındırılmak zorunda kalmaz.

DDD uygularken, her Sınırlandırılmış Bağlamın (Bounded Context), kullanılan her terimin anlamının net bir şekilde tanımlandığı yerler olmasını sağlamaya çalışırız. Bu aslında bir dil sınırıdır (linguistic boundary). Bu bağlamsal sınırlar, DDD'nin en önemli uygulama noktalarından biridir.

Tek bir Sınırlandırılmış Bağlam (Bounded Context) her zaman yalnızca tek bir Alt Alan (Subdomain) içinde yer almaz, ancak bazen alabilir. Şekil 2.1'de yalnızca bir Sınırlandırılmış Bağlamın (Inventory - Stok Yönetimi), tek bir Alt Alan içinde bulunduğunu görüyoruz. Bu durum, e-Ticaret Sistemi geliştirilirken doğru bir DDD yaklaşımının kullanılmadığını açıkça gösteriyor. Bu sistemde şu ana kadar dört farklı Alt Alan belirledik ve muhtemelen daha fazlası da var.

Öte yandan, Stok Yönetimi Sistemi (Inventory System), yalnızca ürünlerin stoklanmasını içeren bir alan olarak tek bir Alt Alan içinde sınırlandırılmış gibi görünüyor. Bunun sebebi, gerçekten DDD uygulanmış olması olabilir ya da bu sadece tesadüfi bir durum da olabilir. Kesin bir sonuca varmak için sistemin iç yapısını detaylıca incelememiz gerekir. Ancak ne olursa olsun, **Stok Yönetimi Sistemi'ni yeni Temel Alanımızı (Core Domain) geliştirmek için pratik bir şekilde kullanabiliriz.**

***Dilbilimsel Açıdan Hangi Sınırlandırılmış Bağlam Daha İyi Bir Tasarıma Sahip?***

Şekil 2.1'e baktığımızda hangi Sınırlandırılmış Bağlamın (Bounded Context) daha iyi tasarlandığını dilbilimsel açıdan değerlendirebiliriz. Örneğin, e-Ticaret Sisteminde (e-Commerce System) terimler ve anlamlar muhtemelen birbiriyle çakışmaktadır. Bunu **"Müşteri" (Customer)** terimi üzerinden inceleyelim:

- Bir kullanıcı Katalog tarayıp ürünleri incelerken, Müşteri terimi farklı bir anlam taşır.
- Aynı kullanıcı bir Sipariş oluşturduğunda ise, "Müşteri" kelimesinin anlamı değişir.

**Bunun nedeni şu:**

- Katalog içinde "Müşteri" kavramı; önceki alışverişler, sadakat programı, mevcut ürünler, indirimler ve gönderim seçenekleriyle ilişkilidir.
- Ancak, Sipariş oluştururken "Müşteri" yalnızca şu bilgileri içerir:
    -   İsim
    -   Teslimat adresi
    -   Fatura adresi
    -   Ödenecek toplam tutar
    -   Ödeme koşulları

Bu basit analiz bile, e-Ticaret Sisteminde "Müşteri" kavramının tek ve net bir anlama sahip olmadığını gösteriyor. Bu durumda, sistemi detaylı incelediğimizde benzer şekilde anlamı değişen birçok başka terim de bulmamız olasıdır. Bu, temiz ve net anlamlara sahip olmayan bir Sınırlandırılmış Bağlam örneğidir.

Bununla birlikte, **Stok Yönetimi Sistemi'nin tamamen temiz bir modele sahip olduğunun garantisi de yoktur.** Bu sistemin odaklanmış bir model gibi görünmesine rağmen stoklanan ürünlerin farklı kullanımları arasında kavramsal anlam farklılıkları olabilir. Örneğin:

- Sipariş edilen bir ürün (Ordered Item),
- Teslim alınan bir ürün (Goods Received),
- Stokta bulunan bir ürün (Stock Item),
- Stoktan çıkan bir ürün (Item Leaving Inventory),
- Bozulan veya kırılan bir ürün (Wasted Inventory Item)

bu sistemde **farklı anlamlara gelebilir.**

Şekil 2.1'e bakarak, bu kavramların nasıl modellenmiş olduğunu kesin olarak bilemeyiz. Ancak DDD uygulandığında, hiçbir şeyi varsaymak yerine her kavramın açıkça tanımlandığından emin oluruz. Alan uzmanlarının (domain experts) bu kavramları nasıl tanımladığına bağlı olarak, bazılarını farklı Sınırlandırılmış Bağlamlara ayırmamız gerekebilir.

Dışarıdan bakıldığında, **Stok Yönetimi Sistemi'nin DDD açısından daha sağlıklı bir model sunduğunu söyleyebiliriz.** Muhtemelen, bu sistemin geliştirici ekibi "Bir Ürün" (Item) kavramını, tüm stok durumlarını kapsayacak şekilde zorlamamıştır. Bu kesin olmamakla birlikte, **Stok Yönetimi Sistemi'nin e-Ticaret Sistemi'ne kıyasla entegrasyon açısından daha kolay olabileceğini gösteriyor.**

Şekil 2.1'de bir işletmedeki Sınırlandırılmış Bağlamların (Bounded Contexts) nadiren tek başına çalıştığını görüyoruz. Örneğin:

- Üçüncü taraf e-Ticaret Sistemi (Third-Party e-Commerce System),
- Stok Yönetimi Sistemi (Inventory System),
- Harici Tahminleme Sistemi (External Forecasting System),

arasında **zorunlu entegrasyon ilişkileri bulunmaktadır.** Bu farklı modellerin birlikte çalışmak zorunda olduğunu gösterir. Bütünleşik büyük bir model sunmaya çalışan üçüncü taraf e-Ticaret Sistemi bile, perakendecinin ihtiyaç duyduğu her şeyi tam olarak karşılayamaz. Şekil 2.1’de gösterilen **düz çizgiler (solid straight lines), farklı Alt Alanlar arasındaki entegrasyon ilişkilerini gösterir.**
Bu ilişkiler her zaman belirli bir entegrasyon türünü içerir ve "Bağlam Haritaları" (Context Maps) konsepti ile bu entegrasyon türlerini daha ayrıntılı olarak inceleyeceğiz.

**Bu bölümde, basit bir iş alanının (business domain) yüksek seviyeli bir özetini gördük.** Temel Alan (Core Domain) kavramıyla tanıştık. DDD’nin bu kavramı nasıl ele aldığını gördük. Şimdi, bunu daha iyi anlamamız gerekiyor.

### Çekirdek Alana Odaklanın

Alt Alanlar ve Sınırlandırılmış Bağlamlar hakkında bir anlayış geliştirdikten sonra, Şekil 2.2’de gösterilen farklı bir Alanın soyut bir görünümünü ele alalım. Bu, herhangi bir alanı temsil edebilir. Belki de sizin çalıştığınız alanı ☺. Bu kez, belirli isimleri kaldırdım, böylece boşlukları kendi zihninizde doldurabilirsiniz. Doğal olarak, iş hedeflerimiz sürekli olarak rafine edilmekte ve genişlemektedir. Bu süreç, değişen Alt Alanlara ve içlerindeki modellere yansımaktadır. Bu diyagram, yalnızca belirli bir bakış açısıyla ve belirli bir zaman diliminde iş alanının tamamını yakalıyor. Ancak, bu perspektif kısa ömürlü olabilir ve zamanla değişebilir.

![Figure 2.2: An abstract business Domain that includes Subdomains and Bounded Contexts](https://www.bdabek.pl/wp-content/uploads/2020/09/bc-vs-subdomain.png)
**Figure 2.2:** An abstract business Domain that includes Subdomains and Bounded Contexts

---

> **Alıştırma Zamanı**
>
> - Bir sütunda, günlük işinizde farkında olduğunuz tüm Alt Alanları (Subdomains) listeleyin. Diğer sütunda ise Sınırlandırılmış Bağlamları (Bounded Contexts) listeleyin. Alt Alanlar birden fazla Sınırlandırılmış Bağlam ile kesişiyor mu? Eğer öyleyse, bu çok kötü bir şey değil, kurumsal yazılım dünyasının bir gerçeği.
> -   Şimdi, Şekil 2.2’deki şablonu kullanarak işletmenizde çalışan bazı yazılım isimlerini, Alt Alanlar, Sınırlandırılmış Bağlamlar ve bunlar arasındaki entegrasyon ilişkileriyle birlikte diyagrama ekleyin.
> > Bu zor muydu? Muhtemelen öyle, çünkü Şekil 2.2’deki şablon, Alanınızdaki mevcut sınırlarla tam olarak örtüşmüyor olabilir.
> - Tekrar başlayın. Bu kez, Alanınızı, Alt Alanlarınızı ve Sınırlandırılmış Bağlamlarınızı daha iyi yansıtacak bir diyagram çizin. Şekil 2.2’deki teknikleri kullanın**, ancak bunları kendi iş dünyanıza uygun hale getirin.
> > Elbette, işletmenizdeki tüm Alt Alanlar ve Sınırlandırılmış Bağlamlar hakkında her şeyi biliyor olmayabilirsiniz. Özellikle Alanınız büyük ve karmaşıksa.   Ancak, günlük olarak çalıştığınız bölümleri belirleyebilirsiniz.  Yanılmaktan korkmayın! Bu, “Bağlam Haritalama (Context Mapping)” pratiği yapmanız için iyi bir fırsat. Bu konu bir sonraki bölümde daha ayrıntılı ele alınacak.  Eğer oraya göz atmak isterseniz, bu da gayet iyi. Ancak şimdilik mükemmel olmaya çalışmayın—öncelikle temel fikirleri kavramaya odaklanın.

---

Şimdi Şekil 2.2’deki İş Alanı sınırının üst kısmına bakın; burada **"Çekirdek Alan" (Core Domain)** olarak etiketlenmiş bir **Alt Alan** göreceksiniz. Daha önce tanıtılan bu kavram, DDD’nin en önemli unsurlarından biridir. Çekirdek Alan, iş alanının **kuruluşun başarısı için birincil öneme sahip olan** bölümüdür. **Stratejik açıdan bakıldığında, işletmenin Çekirdek Alanında mükemmelleşmesi gerekir.** Bu alan, işletmenin sürekliliği ve başarısı için en kritik noktadır. Bu yüzden, bu projeye en yüksek öncelik verilir; **derin bilgiye sahip bir veya daha fazla alan uzmanı, en iyi geliştiriciler ve ekip için mümkün olan en fazla özgürlük ve destek sağlanır**. Bu sayede, ekip başarıya ulaşma yolunda herhangi bir engelle karşılaşmadan ilerleyebilir. DDD proje çalışmalarınızın büyük bir kısmı **Çekirdek Alana odaklanacaktır**. 

Şekil 2.2’de ayrıca **iki farklı Alt Alan türü** daha bulunur:

- Destekleyici Alt Alan (Supporting Subdomain)
- Genel Alt Alan (Generic Subdomain)

Bazı durumlarda, işletmeyi desteklemek amacıyla **sınırlı bir bağlam (Bounded Context)** oluşturulur veya dışarıdan temin edilir. Eğer bu bağlam, işletme için temel olmasa da önemli bir süreci modelliyorsa, buna **Destekleyici Alt Alan (Supporting Subdomain)** denir. İşletme, özelleştirilmiş bir ihtiyacı karşılamak için Destekleyici Alt Alan oluşturur. 

Öte yandan, eğer bir Alt Alan işletme için herhangi bir özel katma değer sağlamıyor ancak genel işleyişin bir parçası olarak gereklilik arz ediyorsa, buna **Generic Subdomain** denir.

Bir Alt Alanın **Supporting veya Generic olması, onun önemsiz olduğu anlamına gelmez**. Bu Alt Alanlar da işletmenin başarısı için kritik olabilir. Ancak işletmenin bu alanlarda mükemmelleşmesine gerek yoktur. Asıl mükemmeliyet Çekirdek Alanda sağlanmalıdır, çünkü işletmeye özgü rekabet avantajını sunan alan burasıdır.

---

> **Alıştırma Zamanı**
> - Çekirdek Alan kavramlarının önemini tam olarak kavrayıp kavramadığınızı anlamak için, yeni oluşturduğunuz beyaz tahta çiziminize geri dönün ve organizasyonunuzda hangi alanların Çekirdek Alan olarak geliştirildiğini belirlemeye çalışın.
> - Ardından, iş alanınızda Destekleyici Alt Alanlar ve Genel Alt Alanları belirlemeye çalışın.

---

> **Unutmayın: Alan Uzmanlarına Sorun!**  
İlk seferde tam olarak doğru yapmasanız da, bu alıştırma yazılımınızın işinizi en çok nasıl ayırt ettiğini, ayırt edici yazılımı neyin desteklediğini ve işinizin başarısı için hiçbir şekilde ayırt edici olmayan yazılımı dikkatlice düşünmenize yardımcı olacaktır. Bu süreç üzerinde çalışmaya devam edin, böylece düşünme süreçleri ve teknikler konusunda daha rahat hale gelirsiniz.  
Çiziminizdeki her bir Alt Alan ve Bağlantılı Bağlamı, farklı alanlarda uzmanlaşmış birkaç alan uzmanıyla tartışın.  
Sadece onlardan çok şey öğreneceksiniz, aynı zamanda uzmanları dinleme konusunda değerli deneyimler kazanacaksınız. Bu, DDD’yi iyi bir şekilde uygulamanın bir özelliğidir.

---

Az önce öğrendikleriniz stratejik tasarımın büyük resim temelidir.

** 53. sayfada kaldım