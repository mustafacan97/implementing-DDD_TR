# CHAPTER 1 – Getting Started With DDD

> “Tasarım sadece nasıl göründüğü ve hissettirdiği değildir. Tasarım, nasıl çalıştığıdır.”
>
> — Steve Jobs

Geliştirdiğimiz yazılımda kalite üretmeye çalışıyoruz. Yazılımın çok fazla hatayla teslim edilmesini önlemek için testler kullanarak belirli bir kalite seviyesi elde edebiliriz. Ancak, tamamen hatasız bir yazılım üretsek bile, bu tek başına kaliteli bir yazılım modeli tasarlandığı anlamına gelmez. Yazılım modeli—yani yazılımın, ulaşılmak istenen iş hedefinin çözümünü nasıl ifade ettiği—yine de ciddi şekilde sorunlu olabilir. Az hata içeren bir yazılım teslim etmek elbette iyidir. Yine de, iş hedefini açıkça yansıtan iyi tasarlanmış bir yazılım modeli için daha yükseğe ulaşabiliriz ve hatta çalışmamız mükemmel bir seviyeye erişebilir.

**Domain-Driven Design** veya kısaca DDD olarak adlandırılan yazılım geliştirme yaklaşımı, yüksek kaliteli yazılım modelleri tasarlamada daha başarılı olmamıza yardımcı olmak için vardır. Düzgün bir şekilde uygulandığında, DDD tasarımımızın tam olarak yazılımın nasıl çalıştığını yansıtmasını sağlar. Bu kitap, DDD’yi doğru şekilde uygulamanıza yardımcı olmayı amaçlamaktadır.

DDD’ye tamamen yeni olabilir, daha önce denemiş ama zorlanmış ya da başarılı bir şekilde uygulamış olabilirsiniz. Sebebiniz ne olursa olsun, şüphesiz bu kitabı okuyorsunuz çünkü DDD’yi uygulama yeteneğinizi geliştirmek istiyorsunuz ve bunu yapabilirsiniz. Kitapta sunulan bölüm yol haritası, özel ihtiyaçlarınıza odaklanmanıza yardımcı olacaktır.

> **Bu Bölümün Yol Haritası**
> 1.	DDD’nin projelerinize ve ekiplerinize, karmaşıklıkla mücadele ederken nasıl katkı sağlayabileceğini keşfedin.  
> 2. Projenizin DDD yatırımı yapmaya değer olup olmadığını değerlendirmek için nasıl puanlandırılacağını öğrenin.  
> 3.	DDD’ye yaygın alternatifleri ve neden genellikle sorunlara yol açtıklarını inceleyin.  
> 4.	Projenizde ilk adımları nasıl atacağınızı öğrenerek DDD’nin temellerini kavrayın.  
> 5.	DDD’yi yönetime, alan uzmanlarına ve teknik ekip üyelerine nasıl anlatıp benimsetebileceğinizi öğrenin.  
> 6.	DDD kullanmanın zorluklarıyla yüzleşin ve başarılı olmanızı sağlayacak bilgileri edinin.  
> 7.	DDD’yi uygulamayı öğrenen bir ekibin sürecini gözlemleyin.  

DDD’den Ne Beklemelisiniz? DDD, ilerlemenizi engelleyen ağır, karmaşık ve törensel bir süreç sunmaz. Bunun yerine, muhtemelen halihazırda güvendiğiniz çevik (agile) geliştirme tekniklerini kullanmanızı bekleyin. Çevikliğin ötesinde, iş alanınızı (domain) derinlemesine anlamanıza yardımcı olacak yöntemleri öğrenmeyi ve bunun sonucunda test edilebilir, esnek, düzenli, özenle tasarlanmış, yüksek kaliteli yazılım modelleri üretme fırsatını yakalamayı hedefleyin.

DDD, temel iş hedeflerini karşılayan yüksek kaliteli yazılım tasarlamak için gerekli olan hem stratejik hem de taktiksel modelleme araçlarını size sunar.


## DDD Uygulayabilir Miyim?

Eğer aşağıdaki özelliklere sahipseniz, DDD’yi uygulayabilirsiniz:
* Her gün mükemmel yazılımlar geliştirme tutkusuna ve bu hedefe ulaşma azmine sahipseniz,
* Öğrenmeye ve kendinizi geliştirmeye istekliyseniz ve gerektiğinde eksiklerinizi kabul edebiliyorsanız,
* Yazılım desenlerini (patterns) anlayıp doğru şekilde uygulama yeteneğiniz varsa,
* Kanıtlanmış çevik yöntemleri kullanarak tasarım alternatiflerini keşfetme becerisine ve sabrına sahipseniz,
* Mevcut durumu sorgulama cesaretiniz varsa,
* Detaylara dikkat etme, deneme-yanılma yöntemiyle keşfetme arzunuz ve yeteneğiniz varsa,
* Daha akıllı ve daha iyi kod yazmanın yollarını aramaya yönelik bir motivasyonunuz varsa.

Size öğrenme eğrisinin olmadığını söylemeyeceğim. Açık konuşmak gerekirse, bu eğri dik olabilir. Ancak, bu kitap, öğrenme sürecinizi mümkün olduğunca kolaylaştırmak için hazırlandı. Amacım, sizin ve ekibinizin DDD’yi en yüksek başarı potansiyeliyle uygulamanıza yardımcı olmaktır.

DDD, öncelikli olarak bir teknoloji konusu değildir. En temel ilkeleri açısından, DDD; tartışma, dinleme, anlama, keşfetme ve iş değeri ile ilgilidir. Tüm bunlar, bilgiyi merkezileştirme çabasının bir parçasıdır. Eğer şirketinizin faaliyet gösterdiği iş alanını anlayabiliyorsanız, en azından yazılım modeli keşif sürecine katılarak **Ortak Dil (Ubiquitous Language)** oluşturabilirsiniz. Elbette iş hakkında çok daha fazla şey öğrenmeniz gerekecek. Ancak, işletmenizin kavramlarını anlayabiliyor ve harika yazılımlar geliştirmekten keyif alıyorsanız, DDD’yi başarılı bir şekilde uygulamaya şimdiden hazırsınız demektir.

Peki, uzun yıllar—hatta on yıllarca—yazılım geliştirme deneyimine sahip olmak fayda sağlar mı? Belki. Ancak, yazılım geliştirme deneyimi size **alan uzmanlarından (domain experts)** öğrenme ve onların görüşlerini dikkate alma yeteneğini doğrudan kazandırmaz. İşin en kritik yönlerini en iyi bilen bu kişiler genellikle teknik terimlerle konuşmaz. Onlarla etkili bir şekilde iletişim kurabilmeniz büyük bir avantajdır. Bu süreçte dikkatle dinlemeli, onların bakış açılarına saygı göstermeli ve sizden çok daha fazla bilgiye sahip olduklarını kabul etmelisiniz.

> **Alan Uzmanlarıyla Etkileşime Geçmenin Büyük Avantajları**
Teknik terimler kullanmayan veya nadiren kullanan alan uzmanlarıyla etkili bir şekilde iletişim kurabilmek sizin için büyük bir avantajdır. Onlardan öğreneceğiniz çok şey olduğu gibi, büyük olasılıkla onlar da sizden öğrenecektir. Bu karşılıklı bilgi alışverişi, hem iş alanını daha iyi anlamanızı hem de yazılım modelinizi iş hedefleriyle daha uyumlu hale getirmenizi sağlar.

DDD’de en çok hoşunuza gidebilecek şeylerden biri, alan uzmanlarının da sizi dinlemek zorunda olmasıdır. Onlar gibi siz de ekibin bir parçasısınız. Garip gelebilir, ancak alan uzmanları kendi işlerini tamamen bildiklerini sanabilirler, fakat gerçekte her şeyi bilmiyorlar. DDD sürecinde onlar da iş hakkında daha fazla şey öğrenecekler.

Siz onlardan öğrenirken, büyük olasılıkla onlar da sizden öğrenecek. Onlara yönelteceğiniz sorular, sadece onların bildiklerini değil, aynı zamanda bilmediklerini de ortaya çıkaracaktır. Böylece ekibin her üyesi, iş alanını daha derinlemesine keşfetme ve hatta işin şeklini belirleme sürecine dahil olur.

Bir ekibin birlikte öğrenmesi ve gelişmesi harika bir deneyimdir. Eğer ona bir şans verirseniz, DDD bunu mümkün kılar.

>**Ama Bizim Alan Uzmanlarımız Yok**
Alan uzmanı olmak, bir iş unvanı değildir. Alan uzmanları, üzerinde çalıştığınız iş alanını gerçekten iyi bilen kişilerdir. Genellikle iş alanında geniş bir geçmişe sahiptirler ve ürün tasarımcıları ya da satış ekibinizin bir parçası olabilirler.  
Unvanlara takılmayın. Aradığınız kişiler, üzerinde çalıştığınız konu hakkında herkesten, hatta sizden çok daha fazla bilgiye sahiptir. Onları bulun. Dinleyin. Öğrenin. Ve öğrendiklerinizi kod ile tasarlayın.

Şu ana kadar oldukça güven verici bir başlangıç yaptık. Ancak, teknik yetkinliğin önemli olmadığını ya da bir şekilde onsuz idare edebileceğinizi söylemeyeceğim. **İleri seviye yazılım alan modeli (domain modeling) kavramlarını kavramanız gerekecek.**

Yine de bu, sizi aşırı zorlayacak anlamına gelmiyor. **Eğer** [**Head First Design Patterns (Freeman ve diğerleri)**](https://www.amazon.com/Head-First-Design-Patterns-Brain-Friendly/dp/0596007124) **kitabını anlayabiliyor ve orijinal** [**Design Patterns (Gamma ve diğerleri)**](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612) **metnini kavrayabiliyorsanız**—hatta daha ileri düzeyde desenlerle ilgileniyorsanız—DDD’de başarılı olma şansınız oldukça yüksek.

Buna güvenebilirsiniz: **Deneyim seviyeniz ne olursa olsun, bu süreci sizin için olabildiğince kolaylaştırmak adına elimden gelen her şeyi yapacağım.**

> **Domain Model Nedir?**
Domain model, üzerinde çalıştığınız belirli iş alanının yazılım modelidir. Genellikle bir nesne modeli olarak uygulanır; bu nesneler hem veri hem de doğrudan ve doğru bir iş anlamına sahip davranışlar içerir.
DDD uygularken, çekirdek ve stratejik bir uygulamanın veya alt sistemin merkezinde, özenle tasarlanmış, benzersiz bir domain modeli oluşturmak kritik öneme sahiptir. DDD ile oluşturulan domain modelleri genellikle küçük, odaklanmış ve spesifik olur. Asla tüm işletmeyi tek bir büyük domain modeliyle kapsama çalışmazsınız. Oh, ne güzel! 😌

**DDD'den faydalanabilecek kişilerin aşağıdaki perspektiflerini göz önünde bulundurun. Burada bir yere uyduğunuzu biliyorum:**

* **Yeni başlayan, junior geliştirici**: “Gençim, taze fikirlere sahibim, kod yazmaya olan enerjim tavan yaptı ve bir fark yaratacağım. Beni sinirlendiren şey, üzerinde çalıştığım projelerden biri. Kampüsten ilk işime başlamayı beklememiştim ama burada sadece birbirine neredeyse tamamen aynı ama gereksiz 'objeler' kullanarak verileri ileri geri taşımak var. Neden bu mimari bu kadar karmaşık? Bu neyin nesi? Kodu değiştirmeye çalıştığımda sıkça bozuluyor. Gerçekten ne yapması gerektiğini kimse anlıyor mu? Şimdi yeni karmaşık özellikler eklemem gerekiyor. Genellikle eski sınıfların etrafına bir adaptör sarıyorum, böylece o pislikten korunuyorum. Hiç keyif almıyorum. Bütün gün boyunca kod yazmak ve hata ayıklamak dışında yapabileceğim bir şey olduğuna eminim. Ne olursa olsun, bunu bulup sahip olacağım. Bazı kişiler DDD hakkında konuşuyordu. Gang of Four gibi ama domain modeli için uyarlanmış. Güzel.”

* **Orta seviye geliştirici**: “Son birkaç aydır yeni sisteme dâhil oldum. Şimdi fark yaratma sıram geldi. Anlıyorum ama kıdemli geliştiricilerle toplantı yaparken derinlemesine bilgi eksikliği hissediyorum. Bazen her şey garip görünüyor ama nedenini bilmiyorum. Buradaki iş yapış şeklimizi değiştirmeme yardımcı olacağım. Teknolojiyle bir probleme yaklaşmanın sadece bir noktaya kadar işe yaradığını biliyorum ve bu da temelde yeterli olmuyor. İhtiyacım olan şey, beni **akıllı** ve **deneyimli** bir yazılım pratiği uzmanı yapacak sağlam bir yazılım geliştirme tekniği. Bir kıdemli mimar, yeni gelen birisi, DDD adlı bir şeyden bahsetti. Dinliyorum.” **Zaten kıdemli gibi ses çıkartıyorsunuz. Devam edin. Geleceğe yönelik tutumunuz karşılık bulacak.**

* **Kıdemli geliştirici, mimar**: “DDD’yi birkaç projede kullandım, ama bu yeni pozisyona geçtikten sonra kullanmadım. Taktiksel desenlerin gücünü seviyorum, ama uygulayabileceğim daha pek çok şey var, stratejik tasarım bunlardan biri. [Evans]’ı okurken en çok etkileyici bulduğum şey **Ortak Dil** oldu. Bu gerçekten güçlü bir şey. Takım arkadaşlarım ve yönetimle birkaç kez DDD’nin burada benimsenmesi için konuşmalar yaptım. Yeni gelenlerden ve bazı orta seviye ile kıdemli kişilerden bazıları heyecanlı. Yönetim pek heyecanlı değil. Bu şirkete yeni katıldım ve aslında liderlik etmek için geldim ama organizasyonun düşündüğümden daha az **yıkıcı gelişmelere** ilgi gösterdiğini görüyorum. Neyse. Vazgeçmeyeceğim. Diğer geliştiriciler bu konuda heyecanlı, biliyorum ki bunu başarabiliriz. Beklediğimizden çok daha büyük kazançlar elde edeceğiz. **İş alanı uzmanlarını**—yani **domain expert**—teknik ekiplerimize daha yakın hale getireceğiz ve gerçekten çözümlerimize yatırım yapacağız, sadece onları her iterasyonda yeniden yapmayacağız.” **İşte liderin yaptığı şey budur. Bu kitap, stratejik tasarımla başarıya nasıl ulaşacağınızı gösteren çok fazla rehberlik sunuyor.**

* **Alan Uzmanı**: “Bir süredir işimize yönelik IT çözümlerini tanımlamakta yer alıyorum. Belki de fazla şey bekliyorum ama keşke geliştiriciler, burada ne yaptığımızı daha iyi anlayabilseler. Sürekli olarak sanki biz aptalmışız gibi bizimle konuşuyorlar. Anlamadıkları şey şu ki, eğer biz olmasaydık, burada bilgisayarlarla vakit geçirecek işler de olmazdı. Geliştiriciler sürekli yazılımımızın ne yaptığı hakkında garip bir şekilde konuşuyor. A hakkında konuştuğumuzda, bunun aslında B olduğunu söylüyorlar. Sanki her seferinde ihtiyacımız olanı anlatmaya çalışırken yanımızda bir sözlük ve yol haritası bulundurmamız gerekiyor. B’yi bildiğimiz şekilde A olarak adlandırmalarına izin vermediğimizde ise işbirliği yapmıyorlar. Bu modda çok fazla zaman kaybediyoruz. Neden yazılım, gerçek uzmanların iş hakkında düşündüğü şekilde çalışmak zorunda?”

* **Bu doğru.** İş dünyası insanları ile teknoloji uzmanları arasında yanlış bir **çeviri ihtiyacı** en büyük problemlerden biridir. Bu bölüm tam size göre. Gördüğünüz gibi, DDD sizi ve geliştiricileri eşit seviyeye getirecek. Ve sürpriz! Zaten bazı geliştiriciler sizin tarafınızda. Burada onlara yardımcı olun.

* **Yönetici**: “Yazılım gönderiyoruz. Her zaman en iyi sonuçlarla değil, değişiklikler de olması gerekenden daha uzun sürüyor. Geliştiriciler sürekli olarak bir şeyler ‘domain’ hakkında konuşuyorlar. Bir başka teknik ya da metodolojinin peşinden gitmek bizim için gerekli mi, bilmiyorum. Her seferinde böyle bir şeyin bir ‘gümüş mermi’ olduğunu söylerler, ama binlerce kez duyduğum bir şey. Deneriz, moda geçer ve sonra eskiye döneriz. Sürekli olarak kursumuzu korumamız gerektiğini söylüyorum, ama takım beni sürekli zorluyor. Çok çalıştılar, bu yüzden onları dinlemeliyim. Akıllı insanlar ve değişiklik yapmaları için onlara şans vermek lazım, yoksa sinirlenip ayrılacaklar. Eğer üst yönetimden onay alabilirsem, onlara öğrenmeleri ve uyum sağlamaları için biraz zaman tanıyabilirim. Eğer patronumu takımın yazılım yatırımlarını ve iş bilgisinin merkezileştirilmesini başarmaya dair iddialarına ikna edebilirsem, bu onayı alabileceğimi düşünüyorum. Gerçek şu ki, takımlarım ile iş uzmanları arasında güven ve işbirliğini teşvik edebilecek bir şey yaparsam işimi kolaylaştıracak. Her neyse, duyduğum bu.” **İyi bir yönetici!**

**Hangi pozisyonda olursanız olun, işte önemli bir uyarı.** DDD ile başarılı olmak için bir şeyler öğrenmeniz gerekecek, aslında bir sürü şey öğrenmeniz gerekecek. Ancak bu büyük bir mesele olmamalı. Akıllısınız ve sürekli öğrenmeniz gerektiğini biliyorsunuz. Yine de hepimizin karşılaştığı bu zorluk:

> “Kişisel olarak her zaman öğrenmeye hazırım, ancak her zaman öğretilmekten hoşlanmam.“
>
> — Sir Winston Churchill

İşte bu noktada bu kitap devreye giriyor. Öğretmeyi mümkün olduğunca keyifli hale getirmeye çalıştım, aynı zamanda DDD'yi başarılı bir şekilde uygulamanız için gereken kritik anlayışı da sundum.

Ancak sorunuz şu: **"Neden DDD yapmalıyım?"** Bu gayet geçerli bir soru.


## **Neden DDD Yapmalısınız?**

Aslında, DDD'nin pratik anlamda ne kadar mantıklı olduğuna dair size birkaç iyi neden verdim. **DRY prensibini (tekrar etme)** ihlal etme riskiyle, burada bunları tekrar ediyorum ve önceki sebeplere eklemeler yapıyorum. Herkes bir yankı duyuyor mu?

* **Alan uzmanlarını ve geliştiricileri eşit bir seviyeye koymak**, bu da yazılımın sadece kodlayıcılar için değil, iş için de tamamen anlamlı olmasını sağlar. Bu, yalnızca karşı tarafı tolere etmek anlamına gelmez. Bu, bir bütün haline gelmiş, sıkı bir takım oluşturmak anlamına gelir.

* “İş için anlamlı olmak” meselesi, **iş liderlerinin ve uzmanlarının yazılım geliştiriciler olsaydı oluşturabilecekleri yazılıma mümkün olduğunca yakın yazılım yaparak işe yatırım yapmaktır.**

* **İş hakkında daha fazla şey öğretebilirsiniz.** Hiçbir alan uzmanı, C seviyesindeki bir yönetici, ya da kimse, işin her bir detayını bilmez. Bu sürekli bir keşif sürecidir ve zamanla daha anlamlı hale gelir. DDD ile herkes öğrenir çünkü herkes keşif tartışmalarına katkı sağlar.

* **Bilgiyi merkezileştirmek önemlidir**, çünkü bununla birlikte iş, yazılımı anlamanın “kabile bilgisi” haline gelmediğinden emin olabilir. Bu bilgi yalnızca seçkin bir azınlığa, genellikle yalnızca geliştiricilere ait olur.

* **Alan uzmanları, yazılım geliştiriciler ve yazılım arasında hiçbir çeviri yoktur.** Bu, belki de birkaç çeviri anlamına gelmez. Sıfır çeviri demek, çünkü takımınız herkesin konuştuğu ortak, paylaşılan bir dil geliştirir.

* **Tasarım kodu yansıtır ve kod tasarımı yansıtır.** Tasarım nasıl çalıştığıdır. En iyi kod tasarımını bilmek, çevik bir keşif süreci kullanarak hızlı deneysel modeller aracılığıyla gelir.

* DDD, **stratejik ve taktiksel tasarımı ele alan sağlam yazılım geliştirme teknikleri** sağlar. Stratejik tasarım, en önemli yazılım yatırımlarının neler olduğunu, en hızlı ve güvenli şekilde nasıl varılacağını belirlerken mevcut yazılım varlıklarının nasıl kullanılacağını ve kimlerin dahil olması gerektiğini anlamamıza yardımcı olur. Taktiksel tasarım, çözümün tek bir zarif modelini, zamanla test edilmiş ve kanıtlanmış yazılım yapı taşlarını kullanarak oluşturmak için yardımcı olur.

Herhangi bir iyi, yüksek getirili yatırım gibi, DDD'nin de takım için zaman ve çaba gerektiren başlangıç maliyeti vardır. Her yazılım geliştirme çabasında karşılaşılan tipik zorlukları göz önünde bulundurmak, sağlam bir yazılım geliştirme yaklaşımına yatırım yapma ihtiyacını pekiştirecektir.

**_İş Değeri Sunmak Zor Olabilir_**

Gerçek iş değeri sağlayan yazılım geliştirmek, sıradan iş yazılımı geliştirmekle aynı şey değildir. Gerçek iş değeri sağlayan yazılım, **iş stratejik girişimleri** ile uyumlu olup, **açıkça tanımlanabilir bir rekabet avantajı** sağlayan çözümler sunar — bu yazılım teknolojiyle değil, **işle ilgili** olmalıdır.

**İş bilgisi** asla merkezileştirilmez. Geliştirme ekipleri, birçok paydaşın ihtiyaçları ve talepleri arasında denge kurmak ve önceliklendirme yapmak zorundadır ve yazılımın **fonksiyonel ve fonksiyonel olmayan gereksinimlerini** ortaya çıkarmak amacıyla farklı becerilere sahip birçok kişiyle etkileşimde bulunurlar. Tüm bu bilgileri topladıktan sonra, ekipler, herhangi bir gereksinimin gerçek iş değeri sağladığından nasıl emin olabilirler? Aslında, hangi **iş değerleri** aranıyor ve bunları nasıl ortaya çıkarabilir, önceliklendirebilir ve gerçekleştirebiliriz?

İş yazılımı geliştirmede yaşanan en büyük kopukluklardan biri, **alan uzmanları ile yazılım geliştiriciler arasındaki boşluktur**. Genellikle, gerçek alan uzmanları iş değerini sağlamaya odaklanmışken, yazılım geliştiriciler genellikle iş problemlerine **teknolojik ve teknik çözümler** getirmeye çekilirler. Yazılım geliştiricilerinin yanlış motivasyonları olduğu söylenemez; bu, sadece dikkatlerini çeken şeydir. Yazılım geliştiricileri alan uzmanlarıyla etkileşime girdiğinde bile, işin nasıl düşündüğü ve nasıl işlediği ile yazılım geliştiricilerinin bunu nasıl yorumladığı arasındaki **çeviri/haritalama** çoğu zaman yüzeysel kalır. Ortaya çıkan yazılım, genellikle alan uzmanlarının zihinsel modelini **tanınabilir bir şekilde yansıtmaz** ya da belki kısmen yansıtır. Zamanla, bu kopukluk maliyetli hale gelir çünkü **alan bilgisinin yazılıma çevrilmesi**, geliştiriciler diğer projelere geçtikçe veya şirketten ayrıldıkça kaybolur.

Başka bir sorun, bir veya daha fazla alan uzmanının **birbirleriyle anlaşamamasıdır**. Bu, her uzmanın modellediği belirli alandaki deneyimine göre değişir ya da basitçe, daha çok **ilişkili ancak farklı alanlarda uzmanlaşmış** olabilirler. Ayrıca, birçok "alan uzmanı" aslında belirli bir alanda uzmanlığa sahip olmayıp daha çok iş analisti olabilir ve bu nedenle **öngörücü bir yönlendirme** sağlamaları beklenir. Bu durum kontrolsüz bir şekilde devam ettiğinde, **bulanık** değil, **keskin** zihinsel modellere yol açar ve bu da çelişkili yazılım modellerine yol açar.

**Daha da kötü** olanı, yazılım geliştirme teknik yaklaşımının işin işleyişini **yanlış bir şekilde değiştirmesidir**. Bu farklı bir senaryo olabilir, ancak **ERP yazılımının** genellikle bir organizasyonun genel iş operasyonlarını ERP'nin işleyişine uyacak şekilde değiştirdiği iyi bilinir. ERP'nin sahip olma maliyeti, lisans ve bakım ücretleriyle tam olarak hesaplanamaz. İşte bu yeniden organizasyon ve işteki kesinti, bu iki somut faktörden çok daha pahalı olabilir. Benzer bir dinamik, yazılım geliştirme ekiplerinin işin ihtiyaçlarını **yeni geliştirilen yazılımın** ne yaptığına dönüştürme çabasında da geçerlidir. Bu, iş için, müşteriler için ve iş ortakları için **hem maliyetli** hem de **yıkıcı** olabilir. Dahası, bu teknik yorumlama, **gereksizdir** ve **önlenebilir** doğru yazılım geliştirme teknikleri kullanılarak. **Çözüm, önemli bir yatırımdır**.

**_DDD Nasıl Yardımcı Olur?_**

DDD, yazılım geliştirme için üç ana yönü hedefleyen bir yaklaşımdır:

1. **DDD, alan uzmanlarını ve yazılım geliştiricilerini bir araya getirir** ve yazılımı, iş uzmanlarının zihinsel modelini yansıtacak şekilde geliştirir. Bu, "gerçek dünyayı" modellemeye harcanan bir çaba olduğu anlamına gelmez. Bunun yerine, DDD, iş için en faydalı olan modeli sunar. Bazen faydalı ve gerçekçi modeller kesişir, ancak birbirlerinden sapmaya başladıklarında, DDD **faydalı** olanı tercih eder.
Bu yönle birlikte, alan uzmanlarının ve yazılım geliştiricilerinin çabaları, odaklandıkları iş alanlarının modelini geliştirmek için ortak bir **Evrensel Dil** oluşturmak üzere yönlendirilir. Evrensel Dil, tam takım anlaşmasıyla geliştirilir, konuşulur ve yazılım modeline doğrudan yansıtılır. Takımın hem alan uzmanları hem de yazılım geliştiricilerinden oluştuğunu tekrar hatırlatmakta fayda var. Hiçbir zaman "biz ve onlar" değil, her zaman **biz**. Bu, iş bilgisinin yazılım geliştirme süreçlerinin ilk birkaç sürümünü teslim eden ekiplerin ve bu yazılımın üretilmesinin ötesinde, devamlılığını sağlayan temel bir iş değeridir. Bu, yazılım geliştirme maliyetinin sadece bir maliyet merkezi değil, **haklı bir iş yatırımı** olmasını sağlamak için önemli bir noktadır.
Bu çaba, başlangıçta birbirleriyle anlaşmazlık yaşayan veya sadece alan hakkında temel bilgiye sahip olmayan alan uzmanlarını birleştirir. Ayrıca, bu durum, derin alan bilgisini tüm ekip üyeleri arasında yayarak sıkı işbirlikçi takımı güçlendirir, yazılım geliştiriciler de dahil. Bunu, her şirketin bilgi çalışanlarına yapması gereken **pratik eğitim** olarak düşünebilirsiniz.

2. **DDD, işin stratejik girişimlerini ele alır**. Bu stratejik tasarım yaklaşımı doğal olarak teknik analizleri içerir, ancak daha çok işin stratejik yönüyle ilgilidir. En iyi ekipler arası organizasyonel ilişkilerin tanımlanmasına yardımcı olur ve bir ilişkinin yazılım ya da proje başarısızlığına yol açabilecek bir durum olduğunu erken uyarı sistemleriyle fark etme imkanı sağlar. Stratejik tasarımın teknik yönleri, sistemleri ve işlevsel endişeleri temiz bir şekilde sınırlandırma hedefi taşır, bu da her iş düzeyindeki hizmeti korur. Bu, genel bir hizmet odaklı mimari ya da iş odaklı mimarinin nasıl elde edileceğine dair anlamlı motivasyonlar sunar.

3. **DDD, yazılımın gerçek teknik taleplerini karşılar**. **Taktiksel tasarım modelleme araçlarını** kullanarak yazılımı analiz eder ve geliştirir. Bu taktiksel tasarım araçları, geliştiricilerin, alan uzmanlarının zihinsel modelinin doğru bir şekilde kodifikasyonunu yapmalarını, yazılımın yüksek test edilebilirliğe sahip olmasını, hata yapma olasılığını azaltmasını (kanıtlanabilir bir ifade), hizmet düzeyinde anlaşmalara (SLA'lar) uygun performans sergilemesini, ölçeklenebilir olmasını ve dağılmış bilgi işlem olanaklarını desteklemesini sağlar. DDD’nin en iyi uygulamaları genellikle, **doğru iş kuralları ve veri tutarlılıklarını** tanımaya odaklanarak, daha yüksek düzeydeki mimari ve daha düşük düzeydeki yazılım tasarımı endişelerini ele alır ve kuralları hata durumlarından korur.

Bu yazılım geliştirme yaklaşımını kullanarak, siz ve ekibiniz gerçek iş değeri sağlamada başarılı olabilirsiniz.

**_Alanınızın Karmaşıklığıyla Başa Çıkmak_**

DDD'yi öncelikle iş açısından en önemli alanlarda kullanmak istiyoruz. Kolayca değiştirilebilecek şeylere yatırım yapmazsınız. **Yatırımınızı, karmaşık, kritik ve en yüksek getiriyi vaat eden konulara yaparsınız.** İşte bu yüzden bu modele **"Çekirdek Alan" (Core Domain)** denir.

Bu çekirdek alanlar ve **önemli Destekleyici Alt Alanlar (Supporting Subdomains)** öncelikli yatırım yapılması gereken alanlardır. O halde, doğru bir şekilde, "karmaşık" kavramının ne anlama geldiğini iyi kavramamız gerekir.

> **DDD'yi Karmaşıklığı Artırmak İçin Değil, Basitleştirmek İçin Kullanın**
DDD'yi, karmaşık bir alanı en basit şekilde modellemek için kullanın. Çözümünüzü daha karmaşık hale getirmek için asla DDD'yi kullanmayın.

Neyin karmaşık olduğu işletmeden işletmeye farklılık gösterecektir. Farklı şirketler farklı zorluklarla, farklı olgunluk seviyeleriyle ve farklı yazılım geliştirme yetenekleriyle karşı karşıyadır. Bu yüzden, neyin karmaşık olduğunu belirlemek yerine, neyin önemsiz olmadığını belirlemek daha kolay olabilir. Bu nedenle, ekibiniz ve yönetiminiz, üzerinde çalışmayı planladığınız sistemin bir DDD yatırımına değip değmeyeceğine karar vermelidir.

**DDD Puan Kartı**: Projenizin bir DDD yatırımına uygun olup olmadığını belirlemek için aşağıdaki tabloyu kullanın. Eğer puan kartındaki bir satır projenizi tanımlıyorsa, sağ sütundaki ilgili puanı ekleyin. Projeniz için tüm puanları toplayın. Eğer toplam 7 veya daha yüksekse, DDD kullanmayı ciddi şekilde düşünün.

| **If your project…**  | **Points** | **Supporting thoughts** |
| --------------------- |------------|-------------------------|
| Eğer uygulamanız tamamen veri odaklıysa ve gerçekten saf bir CRUD çözümü olarak nitelendiriliyorsa, yani her işlem temelde bir veritabanı sorgusuyla **Oluşturma (Create), Okuma (Read), Güncelleme (Update) veya Silme (Delete)** işleminden ibaretse, DDD’ye ihtiyacınız yoktur. Ekibinizin tek yapması gereken, bir veritabanı tablo düzenleyicisine hoş bir arayüz eklemektir. Başka bir deyişle, kullanıcılarınıza doğrudan bir tabloya veri ekleyebilecekleri, güncelleyebilecekleri ve zaman zaman silebilecekleri kadar güvenebiliyorsanız, bir kullanıcı arayüzüne bile ihtiyacınız olmazdı. Bu gerçekçi bir senaryo olmasa da, kavramsal olarak dikkate değerdir. Eğer basit bir veritabanı geliştirme aracı ile bir çözüm üretebiliyorsanız, şirketinizin zamanını ve parasını DDD’ye harcamayın. | 0 | Bu basit gibi görünebilir, ancak **basit** ile **karmaşık** olanı ayırt etmek genellikle o kadar kolay değildir. Her CRUD olmayan uygulama, DDD kullanmanın zaman ve çabasını hak ediyor diye bir kural yoktur. Bu yüzden, karmaşık olanla olmayanı ayırt etmek için başka ölçütler geliştirebiliriz... |
| Eğer sisteminiz sadece **30 veya daha az iş operasyonu** gerektiriyorsa, muhtemelen oldukça basittir. Bu, uygulamanızın toplamda 30’dan fazla **kullanıcı hikayesi** veya **kullanım senaryosu akışı** içermeyeceği ve her bir akışın yalnızca minimal iş mantığı barındıracağı anlamına gelir. Eğer böyle bir uygulamayı **Ruby on Rails** veya **Groovy ve Grails** kullanarak hızla ve kolayca geliştirebileceğinizi ve karmaşıklık ile değişim üzerindeki kontrol eksikliğinin sizi zorlamayacağını düşünüyorsanız, muhtemelen DDD kullanmanıza gerek yoktur. | 1 | Açık olmak gerekirse, burada **25 ila 30 tekil iş mantığı metodundan** bahsediyorum, **25 ila 30 farklı servis arayüzünden değil**. Eğer her bir servis arayüzü birden fazla metoda sahipse, **bu gerçekten karmaşık olabilir.** |
| Ancak **30 ila 40 kullanıcı hikayesi veya kullanım senaryosu akışına** ulaştıysanız, bu noktada karmaşıklık artıyor olabilir. Sisteminiz artık **DDD kullanım alanına** girmeye başlıyor olabilir. | 2 | **Caveat emptor** (_dikkat edin_): Çoğu zaman **karmaşıklık yeterince erken fark edilmez.** Yazılım geliştiricileri olarak **karmaşıklığı ve gereken çabayı hafife alma konusunda gerçekten iyiyiz.** Sadece bir Rails veya Grails uygulaması kodlamak **istiyoruz diye** bu doğru bir seçim anlamına gelmez. Uzun vadede, **bu tür tercihler faydadan çok zarar getirebilir.** |
| Uygulama şu an karmaşık olmayacak olsa bile, gelecekte karmaşıklığı artacak mı? Gerçek kullanıcılar uygulamayla çalışmaya başlayana kadar bunu kesin olarak bilemeyebilirsiniz, ancak **"Destekleyici Düşünceler"** sütunundaki bir adım, gerçek durumu ortaya çıkarmaya yardımcı olabilir. <br><br> Burada dikkatli olun. Eğer uygulamanın **orta düzeyde bile** karmaşıklığa sahip olacağına dair en ufak bir ipucu varsa—burada paranoyak olmak için iyi bir zaman—bu, aslında **orta düzeyden daha karmaşık** olacağının yeterli bir göstergesi olabilir. **DDD’ye yönelmek mantıklı olacaktır.** | 3 | Burada, **alan uzmanlarıyla daha karmaşık kullanım senaryolarını** gözden geçirmek ve nereye varacağını görmek faydalı olabilir. Alan uzmanları… <br> 1. **…zaten daha karmaşık özellikler mi talep ediyor?** Eğer öyleyse, bu büyük ihtimalle uygulamanın **zaten karmaşık olduğunu** veya yakında CRUD yaklaşımı için **fazla karmaşık hale geleceğini** gösterir. <br> 2. **…özelliklerden o kadar sıkılmışlar mı ki, tartışmaya bile tahammül edemiyorlar?**  
Muhtemelen **karmaşık değildir.** |
| Uygulamanın özellikleri, **birkaç yıl boyunca sık sık değişecek** ve bu değişikliklerin **basit olacağını öngöremiyorsunuz.** | 4 | DDD, **modelinizi zaman içinde yeniden düzenlerken karmaşıklığı yönetmenize yardımcı olabilir.** |
| Domain’i (**Alanı**) anlamıyorsunuz, çünkü **bu sizin için yeni bir konu.** Ekip olarak bildiğiniz kadarıyla, daha önce bunu yapan kimse olmamış. Bu durum, büyük ihtimalle konunun **karmaşık olduğu** anlamına gelir veya en azından **analitik bir incelemeyle gereken titizliğin gösterilmesini** hak eder. | 5 | **Alan uzmanlarıyla birlikte çalışmanız ve doğru modeli bulmak için denemeler yapmanız gerekecek.** Zaten önceki kriterlerden bir veya daha fazlasında puan aldıysanız, **DDD kullanın.** |

Bu puanlama çalışması, ekibinizin şu sonuçlara varmasına yol açmış olabilir:

* Keşfettiğimizde karmaşıklığın yanlış tarafında olduğumuzu fark edersek, ne kadar hızlı ve kolay bir şekilde yön değiştiremiyoruz; yanlış tarafın düşündüğümüzden daha karmaşık veya daha basit olması fark etmiyor.
* Evet, ama bu sadece projeyi planlama aşamasında **basitlik ile karmaşıklığı daha erken tespit etmek** konusunda çok daha iyi olmamız gerektiği anlamına geliyor. Bu, bize çok zaman, masraf ve sıkıntı kazandırabilir.
* Bir büyük mimari karar verdikten ve birkaç kullanım senaryosunda derinlemesine geliştirme yaptıktan sonra, genellikle **buna sıkışıp kalıyoruz.** O yüzden **akıllıca seçmeliyiz.**

Eğer bu gözlemlerden herhangi biri ekibinizle örtüşüyorsa, kritik düşünmeyi iyi bir şekilde kullanıyorsunuz demektir.

**_Anemi ve Hafıza Kaybı_**

Anemi, tehlikeli yan etkileri olan ciddi bir sağlık sorunu olabilir. **"Anemik Domain Model"** terimi ilk kez kullanıldığında, bunun güçlü olmayan, içsel davranışsal niteliklere sahip olmayan bir domain modelinin iyi bir şey olabileceğini söylemek amacıyla kullanılmamıştı. İlginç bir şekilde, Anemik Domain Modelleri, endüstrimizde her yerde karşımıza çıkmaya başladı. Sorun şu ki, çoğu geliştirici bunun oldukça normal olduğunu düşünüyor ve sistemlerinde ciddi bir durum olduğunu bile kabul etmiyor. Bu gerçek bir sorun.

Modelinizin yorgun, halsiz, unutkan, sakar ve biraz destek ihtiyacı olup olmadığını mı merak ediyorsunuz? Eğer aniden teknik hipokondriya yaşıyorsanız, işte kendi kendinize bir muayene yapmanın iyi bir yolu. Kendinizi rahatlatabilir veya en kötü korkularınızı doğrulayabilirsiniz. Kendinizi kontrol etmek için aşağıdaki adımları kullanın.

(Evet / Hayır şeklinde)

* Yazılımınızda "domain modeli" olarak adlandırdığınız şeyin çoğunlukla yalnızca kamuya açık getter'lar ve setter'lar içerip iş mantığı neredeyse hiç bulunmuyor mu—yani, çoğunlukla sadece özellik değeri taşıyan nesneler mi?
* "Domain modeli"nin sıklıkla kullanıldığı yazılım bileşenleri, sisteminizin çoğu iş mantığını barındırıyor ve bu bileşenler "domain modeli" üzerindeki kamuya açık getter'ları ve setter'ları sıkça mı çağırıyor? Bu belirli "domain modeli" istemci katmanına genellikle Service Layer veya Application Layer (4, 14) denir. Eğer bunun kullanıcı arayüzünüzü tanımlıyorsa, bu soruya "Evet" yanıtını verin ve beyaz tahtaya bin kez yazın ki bir daha asla bunu yapmayacağım.

**İpucu: Doğru cevaplar ya her iki soruya da "Evet", ya da her iki soruya da "Hayır" olmalıdır.**

> “Nasıl yaptınız?
>
>Eğer her iki soruya da "Hayır" cevabı verdiyseniz, domain modeliniz iyi durumda demektir.
Her iki soruya da "Evet" cevabı verdiyseniz, "domain modeliniz" çok, çok hasta. **Anemik**. İyi haber şu ki, okudukça ona yardım edebilirsiniz.
>
>Bir soruya "Evet", diğerine "Hayır" cevabı verdiyseniz, ya inkar ediyorsunuz ya da anemi nedeniyle başka bir nörolojik sorunla karşı karşıyasınız. Çelişkili cevaplar verdiyseniz ne yapmalısınız? İlk soruya geri dönün ve **kendinize tekrar bir kontrol yapın**. Zamanınızı ayırın, ama unutmayın ki her iki soruya da kesin bir şekilde "Evet!" demelisiniz.”

[Fowler, Anemic]’in dediği gibi, **Anemik Domain Model** kötü bir şeydir çünkü bir domain modelini geliştirmenin yüksek maliyetinin çoğunu ödersiniz, ancak çok az veya hiç fayda elde etmezsiniz. Örneğin, nesne-ilişkisel empedans uyumsuzluğu (veritabanı modelleri ile uygulama modelleri arasındaki uyumsuzluk) nedeniyle, böyle bir "domain modelinin" geliştiricileri nesneleri persistence deposuna ve oradan geri maplamak için çok zaman ve çaba harcar. Bu, çok az veya hiç fayda sağlamadan ödenen yüksek bir bedeldir. Şunu ekleyeceğim ki, sahip olduğunuz şey aslında bir domain modeli değil, sadece bir **veri modelidir** ve bu modelin bir ilişkisel modelden (veya başka bir veritabanından) nesnelere projeksiyonudur. Bu, aslında **Active Record** [Fowler, P of EAA] tanımına daha yakın bir taklitçidir. Muhtemelen mimarinizi sadeleştirerek **Transaction Script** [Fowler, P of EAA] kullandığınızı kabul edebilir ve pretansiyonlu olmaktan kaçınabilirsiniz.

**Anemi Neden Olur?**

Eğer Anemic Domain Model (Anemik Alan Modeli), kötü bir tasarım çabası sonucu zayıf bir sonuca yol açıyorsa, neden pek çok kişi modelinin sağlıklı olduğunu düşünerek kullanıyor? Elbette, bu **prosedürel programlama** zihniyetini yansıtıyor, ancak bunun ana sebep olduğunu düşünmüyorum. Endüstrimizin büyük bir kısmı, örnek kodları takip edenlerden oluşuyor, bu da kötü değil, yeter ki örnekler kaliteli olsun. Ancak sıklıkla örnek kodlar, yalnızca bir kavramı ya da API özelliğini basit bir şekilde gösterme amacı güder, iyi tasarım ilkeleriyle ilgilenmez. Fakat, çoğunlukla **getter** ve **setter**'larla gösterilen aşırı basitleştirilmiş örnek kodlar, her gün tasarım hakkında ikinci bir düşünceye kapılmadan kopyalanıyor.

Başka bir eski etki daha var. **Microsoft’un Visual Basic**'inin eski tarihi, bugün geldiğimiz noktada büyük bir rol oynamıştır. **Visual Basic**'in kötü bir dil ve entegre geliştirme ortamı (IDE) olduğunu söylemiyorum çünkü her zaman verimli bir ortam olmuştur ve bazı açılardan endüstriyi iyi yönde etkilemiştir. Tabii ki, bazıları onun doğrudan etkisinden tamamen kaçınmış olabilir, ancak **Visual Basic**, neredeyse her yazılım geliştiricisini bir şekilde etkilemiştir.

Bahsettiğim şey, properties ve properties sheet etkisidir, her ikisi de orijinal **Visual Basic** form tasarımcısı tarafından popüler hale getirilen **getter** ve **setter**'lar ile desteklenmiştir. Yapmanız gereken tek şey, bir form üzerine birkaç özel kontrol örneği yerleştirmek, bunların özellik sayfalarını doldurmak ve voilà! Tam işlevsel bir **Windows** uygulamanız olurdu. Bunu yapmak, **C** kullanarak Windows API'sine doğrudan programlama yapmaktan sadece birkaç dakika alırken, o benzer uygulamayı programlamak birkaç gün sürebilirdi.

Peki, bunun **Anemic Domain Models** ile ne ilgisi var? **JavaBean** standardı, Java için görsel programlama araçları yaratmaya yardımcı olmak amacıyla ilk kez belirlenmişti. Amacı, **Microsoft ActiveX** yeteneklerini Java platformuna taşımaktı. Çeşitli türde üçüncü taraf özel kontrolleri, tıpkı **Visual Basic**'teki gibi, yaratma umudu sundu. Kısa süre içinde neredeyse her framework ve kütüphane **JavaBean** modasına katıldı. Bu, **Java SDK/JDK**'nin büyük bir kısmını ve popüler **Hibernate** gibi kütüphaneleri de içeriyordu. DDD endişelerimize özgü olarak, **Hibernate**, alan modellerini kalıcı hale getirmek için tanıtılmıştı. Bu trend, **.NET** platformunun da bizimle buluşmasıyla devam etti.

İlginç bir şekilde, erken dönemlerde **Hibernate** ile kalıcı hale getirilen her domain modelinin, her basit özellik ve karmaşık ilişki için **public** getter ve setter'lar sunması gerekiyordu. Bu, **POJO** (Plain Old Java Object) tasarımınızı, **davranış zengin** bir arayüzle tasarlamak isteseniz bile, **Hibernate**'in domain nesnelerinizi kalıcı hale getirebilmesi ve yeniden oluşturabilmesi için iç yapılarını **public** olarak açmak zorunda olduğunuz anlamına geliyordu. Elbette, **JavaBean** arayüzünü gizlemek için bazı şeyler yapabilirdiniz, ancak büyük ölçüde çoğu geliştirici, bunu neden yapmaları gerektiğini anlamadıkları için uğraşmaz ya da hiç düşünmezdi.

> **DDD ile Object-Relational Mappers (ORM'ler) kullanmak konusunda endişelenmeli miyim?**
>
> Önceki Hibernate eleştirisi, tarihsel bir perspektiften gelmektedir. Bir süredir Hibernate, gizli getter'lar ve setter'lar ile hatta doğrudan alan erişimini desteklemektedir. Sonraki bölümlerde, Hibernate ve diğer kalıcılık mekanizmaları kullanırken modellerinizde anemiyi nasıl önleyeceğinizi gösteriyorum. Yani, endişelenmeyin.

Çoğu, hatta neredeyse tüm Web framework'leri de yalnızca **JavaBean** standardı üzerine çalışmaktadır. Eğer **Java** nesnelerinizin **Web** sayfalarınızı doldurabilmesini istiyorsanız, **Java** nesnelerinizin **JavaBean** spesifikasyonunu desteklemesi gerekmektedir. Eğer **HTML** formlarınız, sunucu tarafına gönderildiğinde bir **Java** nesnesini dolduracaksa, **Java** form nesnenizin de **JavaBean** spesifikasyonunu desteklemesi gerekmektedir.

Piyasadaki neredeyse her framework, ve dolayısıyla **public properties** kullanımını zorunlu kılar. Çoğu geliştirici, tüm işletmelerindeki anemik sınıflardan etkilenmekten kendini alıkoyamaz. Kabul etmelisin, sen de bundan etkilenmedin mi? Sonuç olarak, bu durum en iyi şekilde her yerde anemi olarak adlandırılabilir.

Peki, diyelim ki hemfikir olduk ve bu durum bizi gerçekten zorluyor. Peki, her yerde aneminin modelimize ne gibi etkileri olur? Bir **Anemic Domain Model**'in (örneğin, sahte **Application Service**, **Transaction Script** tarzı) istemci kodunu okurken ne görüyoruz? İşte basit bir örnek:

```
@Transactional
public void saveCustomer( 
	String customerId,
    String customerFirstName, String customerLastName,
    String streetAddress1, String streetAddress2,
    String city, String stateOrProvince,
    String postalCode, String country,
    String homePhone, String mobilePhone,
    String primaryEmailAddress, String secondaryEmailAddress) { 

	Customer customer = customerDao.readCustomer(customerId); 
	if (customer == null) {
	    customer = new Customer();
        customer.setCustomerId(customerId); 
	}

	customer.setCustomerFirstName(customerFirstName);
    customer.setCustomerLastName(customerLastName);
    customer.setStreetAddress1(streetAddress1);
    customer.setStreetAddress2(streetAddress2);
    customer.setCity(city);
    customer.setStateOrProvince(stateOrProvince);
    customer.setPostalCode(postalCode);
    customer.setCountry(country);
    customer.setHomePhone(homePhone);
    customer.setMobilePhone(mobilePhone);
    customer.setPrimaryEmailAddress(primaryEmailAddress);
	customer.setSecondaryEmailAddress (secondaryEmailAddress); 

	customerDao.saveCustomer(customer);
}
```

Bu kod ne yaptı? Aslında, bu oldukça çok yönlü bir kod. Yeni veya mevcut bir müşteri olsa da bir Müşteri kaydeder. Soyadı değişmiş ya da kişi yeni bir eve taşınmış olsa da bir Müşteri kaydeder. Kişi yeni bir ev telefonu numarası almış ya da ev telefonu hizmetini iptal etmişse veya ilk kez mobil telefon almışsa, ya da her ikisini de yapmışsa, bir Müşteri kaydeder. Hatta, Juno'dan Gmail'e geçiş yapmış ya da iş değiştirmiş ve yeni bir iş e-posta adresi almış bir Müşteri'yi bile kaydeder. Vay, bu harika bir yöntem!

Ya da değil mi? Aslında, bu saveCustomer() metodunun hangi iş durumlarında kullanıldığını kesin olarak bilmiyoruz. Bu metod neden ilk başta oluşturuldu? İlk başta ne amaçla yaratıldığını ve farklı iş hedeflerini desteklemesi için nasıl değiştirildiğini hatırlayan var mı? Bu hatıralar muhtemelen metodun oluşturulup sonra değiştirildikten sadece birkaç hafta veya ay sonra kayboldu. Ve daha da kötüleşiyor. Buna inanmadınız mı? O zaman aynı metodun bir sonraki versiyonuna göz atın:

```
@Transactional
public void saveCustomer( 
	String customerId,
    String customerFirstName, String customerLastName,
    String streetAddress1, String streetAddress2,
    String city, String stateOrProvince,
    String postalCode, String country,
    String homePhone, String mobilePhone,
    String primaryEmailAddress, String secondaryEmailAddress) { 

	Customer customer = customerDao.readCustomer(customerId); 
	if (customer == null) {
	    customer = new Customer();
        customer.setCustomerId(customerId); 
	}
	if (customerFirstName != null) {
	    customer.setCustomerFirstName(customerFirstName); 
	}
    if (customerLastName != null) { 
		customer.setCustomerLastName(customerLastName);
    } 
	if (streetAddress1 != null) {
	    customer.setStreetAddress1(streetAddress1); 
	}
    if (streetAddress2 != null) { 
		customer.setStreetAddress2(streetAddress2);
    }
	if (city != null) {
	    customer.setCity(city);
	}
    if (stateOrProvince != null) { 
		customer.setStateOrProvince(stateOrProvince);
    }
	if (postalCode != null) {
		customer.setPostalCode(postalCode); 
	}
    if (country != null) { 
		customer.setCountry(country);
    }
	if (homePhone != null) {
        customer.setHomePhone(homePhone); 
	}
    if (mobilePhone != null) { 
		customer.setMobilePhone(mobilePhone);
    }
	if (primaryEmailAddress != null) {
        customer.setPrimaryEmailAddress(primaryEmailAddress);
	}
    if (secondaryEmailAddress != null) { 
		customer.setSecondaryEmailAddress (secondaryEmailAddress);
    }
	
	customerDao.saveCustomer(customer);
}
```

Burada belirtmem gerekir ki, bu örnek en kötü durumdan daha kötü değil. Çoğu zaman veri eşleştirme kodu oldukça karmaşık hale gelir ve birçok iş mantığı buna gizlenir. Bu örnekte en kötüsünü atlıyorum, ancak muhtemelen kendiniz de buna tanık olmuşsunuzdur.

Şimdi, **müşteriId** dışındaki her parametre isteğe bağlıdır. Artık bu metodu, en azından bir düzine iş durumu altında bir Müşteri kaydetmek için kullanabiliriz ve belki daha fazla! Ama bu gerçekten iyi bir şey mi? Bu metodu yanlış durumlarda bir Müşteri kaydetmediğinden emin olmak için nasıl test edebiliriz?

Ayrıntıya girmeden, bu metodun doğru şekilde çalışmasından çok daha fazla yanlış şekilde çalışabileceğini söyleyebilirim. Belki veritabanı kısıtlamaları, tamamen geçersiz bir durumun kaydedilmesini engelliyordur, ancak şimdi bunu emin olmak için veritabanına bakmanız gerekir. Neredeyse kesinlikle, Java nitelikleri ile sütun adları arasında zihinsel bir eşleme yapmanız biraz zaman alacaktır. Bu kısmı çözdükten sonra, veritabanı kısıtlamalarının eksik veya tamamlanmamış olduğunu görürsünüz.

Birkaç kaynak revizyonunu karşılaştırarak ve kullanıcı arayüzü tamamlandıktan sonra eklenen otomatik uzak istemciler hariç, mümkün olan birçok istemciyi inceleyerek, bu metodun neden şu anda olduğu şekilde çalıştığını anlamaya çalışabilirsiniz. Cevapları ararken, kimse bu metodun neden şu şekilde çalıştığını veya kaç doğru kullanım olduğunu açıklayamıyor. Bunun üzerinde tek başınıza anlamak birkaç saat veya gün sürebilir.

**Domain uzmanları** burada yardımcı olamaz çünkü kodu anlayabilmek için programcı olmaları gerekir. Birkaç domain uzmanı yeterince programlama bilgisine sahip olsa ya da en azından kodu okuyabilse, yine de bu kodun neyi desteklemeye çalıştığı konusunda bir geliştirici kadar kaybolmuş olabilirler. Tüm bu endişeleri göz önünde bulundurursak, bu kodu herhangi bir şekilde değiştirmeye cesaret edebilir miyiz, eğer edersek nasıl?

Burada en az üç büyük problem var:

1. **saveCustomer()** arayüzü tarafından çok az **niyet** ortaya konmuş.

2. **saveCustomer()**’ın kendisinin implementasyonu **gizli karmaşıklık** ekliyor.

3. **Customer** “domain nesnesi” aslında bir nesne değil. Gerçekten sadece aptalca bir veri tutucu.

Bunu **anemiye bağlı bellek kaybı** olarak adlandıralım. Bu, bu tür örtük ve tamamen öznel kod “tasarımı” üreten projelerde sıkça meydana gelir.

> **Bir Dakika Durun!**
> 
> Bu noktada bazılarınız, "Tasarımımız aslında hiçbir zaman beyaz tahtanın dışına çıkmıyor. Sadece bir yapı çizeriz ve buna dair anlaşma sağlandığında, uygulamaya geçmeye serbest bırakılırız. Korkutucu." diye düşünebilir.
> 
> Eğer öyleyse, tasarımı implementasyondan ayırmamaya çalışın. DDD pratiği yaparken tasarım, koddur ve kod, tasarımdır. Diğer bir deyişle, beyaz tahta diyagramları tasarım değildir, sadece modelin zorluklarını tartışmak için bir yoldur.
>
> Takipte kalın, çünkü beyaz tahtadaki fikirleri nasıl alıp sizin için çalışır hale getireceğinizi öğreneceksiniz.

Artık bu tür bir kod hakkında endişelenmeniz gerektiğini ve daha iyi bir tasarım oluşturmak için nasıl bir yol izleyeceğinizi anlamış olmalısınız. İyi haber şu ki, **kodu tasarımı açıkça ve dikkatle oluşturmakta başarılı olabilirsiniz.**