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


## **DDD Nasıl Yapılır**

Bir an için yoğun implementasyon tartışmalarından uzaklaşalım ve DDD'nin en güçlendirici özelliklerinden birini, **Ubiquitos Language** (Evrensel Dil)'i gözden geçirelim. Bu, DDD'nin iki temel dayanağından biridir, diğer dayanak ise Bounded Context Sınırlı Bağlam (2) olup, biri diğerinin doğru bir şekilde var olabilmesi için gereklidir.

> **Bir Bağlamdaki Terimler**
> 
> Şimdilik, Sınırlı Bağlam'ı, bir uygulama veya belirli bir sistem etrafında bir kavramsal sınır olarak düşünün. Bu sınırın amacı, verilen bir domain terimi, ifadesi veya cümlesinin—Evrensel Dil—sınır içindeki her kullanımının belirli bir bağlamsal anlamı olduğuna dikkat çekmektir. O terimin sınır dışında kullanımı, farklı bir anlam taşıyor olabilir ve muhtemelen öyledir. Bölüm 2, Sınırlı Bağlam'ı derinlemesine açıklar.

**_Ubiquitos Language_**

**Evrensel Dil**, paylaşılan bir takım dilidir. Hem domain uzmanları hem de geliştiriciler tarafından kullanılır. Aslında, proje ekibindeki herkes tarafından paylaşılır. Takımda hangi rolde olursanız olun, proje ekibinde yer alıyorsanız, projeye ait **Evrensel Dil**i kullanırsınız.  
  
**Peki, Evrensel Dilin Ne Olduğunu Düşünüyorsunuz?**

Açıkça söylemek gerekirse, bir işin dili olmalıdır. Kesinlikle endüstri standart terminolojisini benimsemek olmalı. **Hayır, aslında öyle değil.** Tabii ki, domain uzmanlarının kullandığı jargon olmalı. **Üzgünüm, ama hayır.**

**Evrensel Dil**, takım tarafından geliştirilen paylaşılan bir dildir—hem domain uzmanları hem de yazılım geliştiricilerden oluşan bir takım tarafından. İşte bu kadar. Şimdi anladınız!

Doğal olarak, domain uzmanları dil üzerinde güçlü bir etkiye sahiptir çünkü işin o kısmını en iyi onlar bilir ve endüstri standartlarından etkilenmiş olabilirler. Ancak, Dil, daha çok işin kendisinin nasıl düşündüğü ve nasıl işlediği üzerine odaklanır. Ayrıca, çoğu zaman iki veya daha fazla domain uzmanı kavramlar ve terimler üzerinde anlaşmazlık yaşar, ve bazıları aslında her durumu düşünmedikleri için yanılabilir. Bu yüzden uzmanlar ve geliştiriciler birlikte çalışarak domainin bir modelini oluştururken, hem fikir olma ve uzlaşma yoluyla projeye en uygun **Dil**i ortaya koyarlar. Takım, **Dil**in kalitesinden asla ödün vermez, sadece en iyi kavramlar, terimler ve anlamlar konusunda uzlaşır. İlk uzlaşı, son nokta değildir. **Dil**, küçük ve büyük keşifler yapıldıkça zamanla büyür ve değişir, tıpkı başka herhangi bir yaşayan dil gibi.

Bu, geliştiricilerin domain uzmanlarıyla aynı sayfada olmalarını sağlamak için bir numara değildir. Bu, geliştiricilere zorla iş jargonunu dayatmak da değildir. Gerçekten, tüm ekip tarafından oluşturulan bir dildir—domain uzmanları, geliştiriciler, iş analistleri ve sistemi üretmeye dahil olan herkes tarafından. **Dil**, başlangıçta domain uzmanlarının doğal jargonuyla başlayabilir, ancak bununla sınırlı değildir çünkü **Dil** zamanla büyümelidir. Şunu söylemek yeterlidir ki, birden fazla domain uzmanı **Dil**i oluştururken yer yer terimler ve anlamlar hakkında hafif anlaşmazlıklar yaşayabilir.

Aşağıdaki tabloda, sadece grip aşılarının yönetimini kodla modellemekle kalmaz, ekip aynı zamanda **Dil**i açıkça konuşmalıdır. Ekip bu modelin bu yönünü tartışırken, "Hemşireler, hastalara standart dozlarda grip aşısı yapar" gibi ifadeler kullanırlar.

Uzmanların zihnindeki mevcut **Dil**le oradan gelişen **Dil** arasında bazı pazarlıklar ve çekişmeler olacaktır. Bu, uzun süre önemli olacak en iyi **Dil**i geliştirme sürecinin doğal bir parçasıdır. Bu, açık tartışmalar, mevcut belgeleri gözden geçirme, nihayet gün yüzüne çıkan iş bilgisi ve ayrıca standartlar, sözlükler ve eşanlamlılar kullanarak yapılır. Bir noktada, bazı kelimelerin ve ifadelerin iş bağlamına eskisi kadar uygun olmadığını kabul ederiz ve başka bazı kelimelerin çok daha iyi uyduğunu fark ederiz.

**İş için hangisi daha iyidir?  
İkinci ve üçüncü ifadeler benzer olsa da, kod nasıl tasarlanmalıdır?**

| Olası Görüşler | Ortaya Çıkan Kod  |
| -------------- |-------------------|
| "Kim umursar? Sadece yazalım." <br> Ehh, bu hiç de yakın değil. | `patient.setShotType(ShotTypes.TYPE_FLU);` `patient.setDose(dose);` <br>`patient.setNurse(nurse);` |
| "Biz, hastalara grip aşıları yapıyoruz." <br> Daha iyi, ancak bazı önemli kavramları kaçırıyor. | `patient.giveFluShot();` |
| "Hemşireler, hastalara standart dozlarda grip aşıları yapar." <br> Bu, şu anda ilerlemek isteyeceğimiz şey gibi görünüyor, en azından daha fazla şey öğrenene kadar. | `Vaccine vaccine = vaccines.standardAdultFluDose();` <br> `nurse.administerFluVaccine(patient, vaccine);` |

Peki, bu çok önemli Ubiquitous Language'ı nasıl yakalarsınız? İşte deneyimlerin ilerledikçe gelişmeye yol açan bazı yollar:

* Fiziksel ve kavramsal alanın resimlerini çizin ve bunları adlar ve eylemlerle etiketleyin. Bu çizimler çoğunlukla gayri resmi olacaktır, ancak bazı yönleri formel yazılım modellemeyi içerebilir. Takımınız Unified Modeling Language (UML) gibi bazı formel modellemeler yapsa da, tartışmaları engelleyecek ve nihai dilin yaratıcılığını kısıtlayacak herhangi bir seremoniden kaçınmak istersiniz.

* Basit tanımlarla bir terimler sözlüğü oluşturun. Alternatif terimleri listeleyin, işe yarayanları ve işe yaramayanları dahil edin ve nedenlerini belirtin. Tanımlar ekledikçe, alan dilinde yazmak zorunda olduğunuz için dilin yeniden kullanılabilir ifadelerini geliştirmekten kaçamazsınız.

* Eğer bir sözlük fikrini sevmediyseniz, yine de önemli yazılım kavramlarının gayri resmi çizimlerini içeren bir tür dokümantasyon oluşturun. Buradaki amaç, ek dil terimlerinin ve ifadelerinin yüzeye çıkmasını sağlamaktır.

* Sözlük veya diğer yazılı belgeleri sadece bir veya birkaç takım üyesi yakalayabilir, bu yüzden sonucu gözden geçirmek için geri dönün ve takımın geri kalanıyla tartışın. Yakaladığınız tüm dilsel terimler üzerinde her zaman, hatta hiç anlaşamayabilirsiniz, bu yüzden çevik olun ve düzenlemeye hazır olun.

**Bunlar, özel alanınıza uygun bir Ubiquitous Language (Ortak Dil) oluşturmak için ideal ilk adımlardır.** Ancak, bu tam olarak geliştirdiğiniz model değildir. Bu sadece Ubiquitous Language'in başlangıcıdır ve çok geçmeden sisteminizin kaynak kodunda ifade edilecektir. Java, C#, Scala veya başka bir programlama diliyle ilgiliyiz. Bu çizimler ve belgeler, Ubiquitous Language'in zamanla genişleyeceğini ve şekil değiştireceğini de dikkate almaz. Başlangıçta bizi doğru bir şekilde yönlendiren, uzmanlaşmış alanımıza uygun bir Ubiquitous Language geliştiren artefaktlar zamanla geçersiz hale gelebilir. Bu yüzden nihayetinde en kalıcı olan ve kesin anlamları sağlayan şey, takım konuşması ve koddaki modeldir.

Takım konuşması ve kod, Ubiquitous Language'in kalıcı ifadesi olacağı için, çizimlerin, sözlüklerin ve diğer belgelerin, hızla geliştirilen konuşma diline ve kaynak koda ayak uydurmanın zor olacağını kabul etmeye hazırlıklı olun. Bu, DDD kullanmanın bir gerekliliği değildir, ancak pragmatiktir çünkü tüm belgeleri sistemle senkronize tutmak pratik olmaz.

Bu bilgilerle, **saveCustomer()** örneğini yeniden tasarlayabiliriz. Ya Customer sınıfını, desteklemesi gereken her bir iş hedefini yansıtacak şekilde tasarlasaydık?

```
public interface Customer {
	public void changePersonalName(String firstName, String lastName);
	public void postalAddress(PostalAddress postalAddress);
	public void relocateTo(PostalAddress changedPostalAddress);
	public void changeHomeTelephone(Telephone telephone);
	public void disconnectHomeTelephone();
	public void changeMobileTelephone(Telephone telephone);
	public void disconnectMobileTelephone();
	public void primaryEmailAddress(EmailAddress emailAddress);
	public void secondaryEmailAddress(EmailAddress emailAddress);
}
```

Bu modelin Customer için en iyi model olmadığını tartışabiliriz, ancak DDD uygularken tasarımı sorgulamak beklenen bir şeydir. Bir takım olarak, en iyi modelin ne olduğunu tartışabiliriz ve yalnızca kabul edilen Ubiquitous Language'i keşfettikten sonra karar verebiliriz. Yine de, yukarıdaki arayüz, bir Customer’ın desteklemesi gereken çeşitli iş hedeflerini açıkça yansıtmaktadır, ancak dilin sürekli olarak iyileştirilebileceği doğrudur.

Ayrıca, Application Service'in de iş hedeflerinin açık niyetlerini yansıtacak şekilde yeniden yapılandırılacağına dikkat etmek önemlidir. Her Application Service yöntemi, tek bir kullanım durumu akışını veya kullanıcı hikayesini ele almak için değiştirilir.

```
@Transactional
public void changeCustomerPersonalName( 
	String customerId,
	String customerFirstName,
	String customerLastName) { 
	Customer customer = customerRepository.customerOfId(customerId); 
	if (customer == null) {
		throw new IllegalStateException("Customer does not exist."); 
	}

	customer.changePersonalName(customerFirstName, customerLastName);
}
```

Bu yeni tasarım, orijinal örnekten farklıdır çünkü o kodda tek bir metod birçok farklı kullanım durumu akışını veya kullanıcı hikayesini ele alıyordu. Yeni örnekte ise tek bir **Application Service** metodu, yalnızca **Customer**'ın kişisel ismini değiştirmek için sınırlandırılmıştır ve başka hiçbir şey yapmaz. Bu yüzden **DDD** kullanırken, **Application Services**'ı buna göre geliştirmek bizim görevimizdir. Bu, kullanıcı arayüzünün de daha dar bir kullanıcı amacını yansıtması gerektiği anlamına gelir, ki bu daha önce doğruydu. Ancak şimdi, bu özel **Application Service** metodu, istemcisinin ilk ve soyadı parametrelerinin ardından on null göndermesini gerektirmez.

Bu yeni tasarım, zihninizi rahatlatmıyor mu? Kodu okuyabilir ve ne yaptığını kolayca anlayabilirsiniz. Ayrıca bunu test edebilir ve tam olarak ne yapması gerekiyorsa onu yaptığını, yapmaması gereken hiçbir şeyi yapmadığını doğrulayabilirsiniz.

Böylece **Ubiquitous Language**, bir **takımın** belirli bir iş alanı için kullandığı kavram ve terimleri yazılım modeline yakalamak için kullanılan bir takım desenidir. Yazılım modeli, **isimler**, **sıfatlar**, **fiiller** ve **zengin ifadeler** gibi, yakın ilişkili takım tarafından resmi olarak formüle edilen ve konuşulan dili içerir. Hem yazılım hem de modelin **alanın ilkelerine** uygunluğunu doğrulayan testler, bu dili yakalar ve buna uyar, aynı dili takımın konuştuğu dil gibi.

**_Her Yerde Olan, Ama Evrensel Olmayan (Ubiquitous, but Not Universal)_**

Ubiquitous Language'ın kapsamını netleştirmek için bazı temel kavramları dikkatle akılda tutmalıyız:

* **Ubiquitous** kelimesi, "her yerde bulunan" veya "yaygın" anlamına gelir ve bu dil, ****takım içinde konuşulan**** ve **tek bir alan modeliyle ifade edilen** dildir**.**

* **Ubiquitous Language, şirket çapında, hatta dünya çapında geçerli olacak evrensel bir alan dili yaratma girişimi değildir.**

* **Her Bounded Context** için yalnızca **bir tane Ubiquitous Language** vardır.

* **Bounded Context'ler düşündüğümüzden daha küçüktür.** Bir **Bounded Context**, yalnızca **belirli bir iş alanının tam Ubiquitous Language'ını** kapsayacak kadar büyük olmalı, fazlasını içermemelidir.

* **Bu dil yalnızca, izole edilmiş bir Bounded Context içinde geliştirme yapan takım için geçerlidir.**

* **Tek bir proje içinde bile, her biri kendi Ubiquitous Language’ına sahip birden fazla izole edilmiş Bounded Context bulunur** ve bunlar **Context Maps** aracılığıyla entegre edilir. **Bazı terimler örtüşebilir, ancak her Bounded Context’in kendine özgü bir dili vardır.**

* **Eğer tek bir Ubiquitous Language'ı tüm kuruluşa veya daha kötüsü, birden fazla kuruluşa uygulamaya çalışırsanız, başarısız olursunuz.**

**DDD’yi doğru bir şekilde uyguladığınız yeni bir projeye başlarken, öncelikle geliştirilen Bounded Context’i belirleyin.** Bu, alan modelinizin etrafına açık bir sınır çizer. **Bu sınırlar içinde Ubiquitous Language'ı geliştirin ve kullanın.** ****Bu dilin bir parçası olmayan tüm kavramları reddedin.****


## **DDD Kullanmanın İş Değerine Katkısı**

Eğer benim deneyimlerime benzer bir deneyiminiz varsa, yazılım geliştiricilerin artık **sadece "havalı" veya ilgi çekici olduğu için** teknolojileri ve teknikleri uygulayamayacağını biliyorsunuzdur. **Yaptığımız her şeyi gerekçelendirmek zorundayız.**

Eskiden bu her zaman böyle değildi, ancak **şimdi böyle olması iyi bir şey.** Çünkü **bir teknolojiyi veya tekniği kullanmanın en iyi gerekçesi, iş dünyasına gerçek ve somut bir değer sağlamasıdır.**

Eğer **önerdiğimiz yaklaşımın iş açısından daha yüksek değer sunduğunu**  kanıtlayabilirsek, **işletme neden bunu reddetsin?** Özellikle de **alternatiflere kıyasla daha fazla iş değeri sağladığımızı gösterebilirsek, DDD gibi yaklaşımlar çok daha güçlü bir iş gerekçesine sahip olur.**

DDD uygulamanın **gerçekçi iş değerini** düşünelim. Bunu **yönetiminizle, alan uzmanlarınızla ve teknik ekip üyelerinizle** açıkça paylaşmanız önemli. İşte DDD'nin sunduğu değer ve faydaların kısa bir özeti:

1. Organizasyon, alanına dair kullanışlı bir model kazanır.
2. İş süreçleri daha rafine ve net bir şekilde tanımlanır ve anlaşılır.
3. Alan uzmanları yazılım tasarımına katkıda bulunur.
4. Daha iyi bir kullanıcı deneyimi sağlanır.
5. Saf modeller etrafında temiz sınırlar oluşturulur.
6. Kurumsal mimari daha düzenli hale gelir.
7. Çevik, yinelemeli ve sürekli modelleme uygulanır.
8. Hem stratejik hem de taktiksel yeni araçlar kullanılır.


### Organizasyon Kendİ AlanınDa Kullanışlı Bir Model Kazanır

DDD’nin odağı, **iş için en önemli olan noktaya yatırım yapmaktır.** Gereğinden fazla modelleme yapmayız; **temel alanımıza (Core Domain)** odaklanırız. **Destekleyici modeller de önemlidir**, ancak öncelik her zaman temel alan modeline verilir.

Eğer işimizi diğerlerinden ayıran noktaya odaklanırsak, **misyonumuz daha iyi anlaşılır** ve süreci doğru yönlendirecek net çerçeveler oluştururuz. Bu sayede, **tam olarak rekabet avantajı sağlayacak çözümler geliştiririz.**



### İşin Daha Rafine ve Kesin Bir Tanımı ile Anlayışı Gelişir

DDD sürecinde **işin kendisi ve misyonu daha iyi anlaşılır.** Öyle ki, **Core Domain için geliştirilen Ubiquitous Language, pazarlama materyallerine bile yansıyabilir.** Hatta **vizyon dokümanlarında ve misyon bildirimlerinde** kullanılabilir.

Model **zamanla geliştirildikçe**, işletme daha derin bir analiz kabiliyeti kazanır. Alan uzmanları, teknik ekiple birlikte **karşılıklı olarak fikirlerini zorladıkça** ve birbirlerini etkiledikçe **önemli detaylar açığa çıkar.** Bu detaylar, **işletmenin hem mevcut hem de gelecekteki stratejik ve taktiksel kararlarını daha iyi değerlendirmesine** yardımcı olur.


### Alan Uzmanları Yazılım Tasarımına Katkıda Bulunur

DDD'nin **büyük bir iş değeri**, organizasyonun **ana iş alanına dair daha derin bir anlayış geliştirmesidir.**

Alan uzmanları her zaman **kavramlar ve terminoloji konusunda hemfikir olmayabilir.** Bu farklılıklar, bazen organizasyona **dışarıdan gelen farklı deneyimlerden**, bazen de **aynı organizasyon içindeki farklılaşmış süreçlerden** kaynaklanır.

Ancak DDD yaklaşımı sayesinde, **alan uzmanları ortak bir noktada buluşur ve mutabakat sağlar.** Bu, sadece yazılım geliştirme sürecini değil, **tüm organizasyonu daha güçlü hale getirir.**

**Geliştiriciler ve alan uzmanları ortak bir dil kullanmaya başlar. Bilgi transferi kolaylaşır. Ekip içinde ortak bilgi paylaşımı sağlanır. Yeni gelenler için eğitim ve süreç devri daha basit hale gelir. Sadece belirli kişilerde saklı kalan “gizli bilgi” (tribal knowledge) problemi ortadan kalkar.**

Bu avantajlar, **ekibin daima domain dili ile konuşmasını sağlamak için belirlenen hedef doğrultusunda devam eder.**


### **Daha İyi Bir Kullanıcı Deneyimi Sağlanır**

**Kullanıcı deneyimi**, **domain modeline daha iyi uyum sağlayacak şekilde geliştirilebilir.** DDD sayesinde, **kavramsal model doğrudan yazılıma entegre edilir** ve kullanıcı etkileşimini şekillendirir.

Eğer yazılım **çok fazla kararı kullanıcıya bırakırsa**, kullanıcıların **karmaşık kararlar vermesi ve eğitilmesi**  gerekir. **Yanlış veri girişi, verimsizlik ve deneme-yanılma süreci kullanıcı performansını düşürebilir.**

Ancak, **kullanıcı deneyimi domain modeline göre tasarlandığında, kullanıcılar doğru sonuçlara yönlendirilir. Yazılım kullanıcıları eğitir**, bu da işletme için eğitim maliyetlerini azaltır. **Daha az eğitimle daha hızlı üretkenlik sağlanır.** Bu **doğrudan iş değeri yaratır.**


### Saf Modeller Etrafında Temiz Sınırlar Oluşturulur

**Teknik ekip**, **kendi mühendislik ilgileri yerine işin gerekliliklerine odaklanmaya teşvik edilir. Modelin saflığını korumak**, çözümün etkinliğini artırır. **Kaynakların en çok değer yaratacak alanlara yönlendirilmesini sağlar. Projenin Bounded Context’ini anlamak, bu sürecin merkezindedir.**


### Kurumsal Mimari Daha İyi Organize Edilir

Bounded Context’ler doğru anlaşılıp bölümlendiğinde, tüm ekipler hangi entegrasyonların neden gerekli olduğunu  net bir şekilde görebilir. **Sınırlar ve ilişkiler açık hale gelir.** Bağımlılıkları olan modeller arasında Context Map’ler kullanılarak entegrasyonlar sağlanır. Bu süreç, tüm kurumsal mimarinin daha iyi anlaşılmasını sağlar.


### Çevik, Yinelenebilir ve Sürekli Modelleme Kullanılır

DDD, **ağır ve bürokratik bir tasarım süreci değildir.** Önemli olan, domain uzmanlarının zihnindeki modeli iş için kullanılabilir hale getirmektir. Gerçek dünyayı birebir kopyalamak değil, iş problemlerine uygun çözümler üretmek esastır. Ekipler, çevik ve artımlı bir yaklaşım benimseyerek sürekli modelleme yapar. Oluşturulan model, doğrudan çalışan yazılımın kendisidir ve işletme ihtiyaç duyduğu sürece rafine edilir.


### Stratejik ve Taktiksel Yeni Araçlar Kullanılır

Bounded Context, ekibin belirli bir iş problemi için modelleme yapabileceği sınırları belirler. Bu bağlam içinde, Ubiquitous Language geliştirilir ve yazılım modeline entegre edilir. Bağımsız ekipler, Bounded Context’leri Context Map’ler ile yöneterek entegrasyonları stratejik olarak planlar. _Taktiksel modelleme araçları kullanılır:_ **Aggregates, Entities, Value Objects, Services, Domain Events** ve diğerleri. Bu araçlar, **DDD’nin güçlü ve esnek bir yazılım mimarisi oluşturmasını sağlar.**


## DDD Uygulamanın Zorlukları

DDD’yi uygularken zorluklarla karşılaşacaksınız. Bunu başaran herkes bu zorluklarla yüzleşmiştir. **Peki, yaygın zorluklar nelerdir ve bunlarla karşılaştığımızda DDD'yi nasıl savunabiliriz?** İşte en yaygın olanları:

* **Ubiquitous Language oluşturmak için gerekli zaman ve çaba**

* **Domain uzmanlarını en baştan ve sürekli olarak projeye dahil etmek**

* **Geliştiricilerin, kendi domainlerindeki çözümlere bakış açılarını değiştirmesi**

**DDD’yi tam anlamıyla uygulamak ve iş için en yüksek değeri elde etmek istiyorsanız, bu süreç daha fazla düşünmeyi, çaba harcamayı ve zaman ayırmayı gerektirir.**

DDD’nin en büyük zorluklarından biri, iş domaini hakkında düşünmek, kavramları ve terminolojiyi araştırmak ve domain uzmanlarıyla sürekli diyalog kurarak **Ubiquitous Language’i keşfetmek, geliştirmek ve iyileştirmektir.** Bu, kod yazmaya hemen başlamaktansa **daha fazla analiz yapmayı gerektirir.** Ancak, **teknolojik jargon kullanarak doğrudan kodlamaya geçmek yerine** işin kendisini anlamak **uzun vadede daha büyük değer sağlar.**

Domain uzmanlarını projeye dahil etmek her zaman kolay değildir. Ancak **bunu mutlaka yapmalısınız.** **Eğer en az bir gerçek uzmanı sürece dahil edemezseniz, domainin derin bilgisini keşfetmeniz mümkün olmayacaktır.** Uzmanları sürece dahil ettiğinizde ise **sorumluluk artık geliştiricilere düşer.** Geliştiriciler, **domain uzmanlarıyla konuşmalı, dikkatle dinlemeli ve onların konuştuğu dili yazılıma yansıtmalıdır.**  Ancak bu her zaman kolay olmaz. Gerçek domain uzmanları **sürekli müsait olmayabilir, seyahat edebilir ve toplantılara katılmaları haftalar sürebilir, küçük işletmelerde, CEO veya üst düzey yöneticiler domain uzmanı olabilir, ancak onların öncelikleri farklı olabilir.**

Çoğu geliştirici, DDD'yi düzgün bir şekilde uygulayabilmek için düşünme biçimlerini değiştirmek zorunda kalmıştır. **Geliştiriciler olarak biz teknik düşünürüz.** Teknik çözümler bizim için kolaydır. **Bu, teknik düşünmenin kötü olduğu anlamına gelmez,** sadece bazen daha az teknik düşünmenin daha iyi olabileceği zamanlar vardır. **Eğer yıllardır sadece teknik yollarla yazılım geliştirmeyi alışkanlık haline getirdiysek, belki de şimdi yeni bir düşünme biçimi üzerinde düşünmenin tam zamanıdır.** Domain'inizin Ubiquitous Language'ini geliştirmek, **başlamak için en iyi yerdir.**

DDD ile gereken başka bir düşünce seviyesi, kavram isimlendirmesinin ötesindedir. **Bir domaini yazılım aracılığıyla modellediğimizde, hangi model nesnelerinin ne yaptığına dikkatlice düşünmemiz gerekir.** Bu, nesnelerin davranışlarını tasarlamakla ilgilidir. Evet, davranışların, **Ubiquitous Language'i** iletmek için doğru şekilde isimlendirilmesini istiyoruz. Ancak, bir nesnenin belirli bir davranış aracılığıyla ne yaptığına da dikkat edilmelidir. Bu, bir sınıf üzerinde sadece nitelikler oluşturup, getter ve setter'ları modelin istemcilerine halka açık hale getirmekten öte bir çaba gerektirir.

Şimdi daha ilginç bir domain modeline bakalım, daha önce ele aldığımız basit domain'lerden daha zorlu bir model. **Amacım önceki yönlendirmelerimi burada yinelemek ve fikirleri pekiştirmektir.**

Tekrar vurgulamak gerekirse, model nesnelerimiz için yalnızca veri erişimcilerini sağlarsak, sonuçlar **bir veri modeline** benzeyecektir. Aşağıdaki iki örneği inceleyin ve hangisinin daha derinlemesine bir tasarım düşüncesi gerektirdiğine ve hangisinin istemcilerine daha fazla fayda sağladığına karar verin. Gereksinim, Scrum modelindeki bir sprint'e bir backlog öğesini taahhüt etmekle ilgilidir. Muhtemelen bunu sürekli yapıyorsunuzdur, dolayısıyla bu domain çoğunlukla tanıdık bir domain'dir.

İlk örnekte, genellikle günümüzde yapılan, öznitelik erişimcileri kullanılır:

```
public class BacklogItem extends Entity {
	private SprintId sprintId;
	private BacklogItemStatusType status;
	... 

	public void setSprintId(SprintId sprintId) {
		this.sprintId = sprintId; 
	}

	public void setStatus(BacklogItemStatusType status) {
		this.status = status; 
	}
	...
}
```

Bu modelin müşterisine gelince:

```
// client commits the backlog item to a sprint
// by setting its sprintId and status 

backlogItem.setSprintId(sprintId);
backlogItem.setStatus(BacklogItemStatusType.COMMITTED);
```

İkinci örnek, domain nesnesi davranışı kullanarak domain'in Ubiquitous Language'ini ifade eder:

```
public class BacklogItem extends Entity {
	private SprintId sprintId;
	private BacklogItemStatusType status;
	... 

	public void commitTo(Sprint aSprint) {
		if (!this.isScheduledForRelease()) {
			throw new IllegalStateException("Must be scheduled for release to commit to sprint."); 
		}

		if (this.isCommittedToSprint()) {
			if (!aSprint.sprintId().equals(this.sprintId())) { 
				this.uncommitFromSprint();
			}
		}
        
        this.elevateStatusWith(BacklogItemStatus.COMMITTED);
        this.setSprintId(aSprint.sprintId()); 
		DomainEventPublisher
			.instance()
			.publish(new BacklogItemCommitted(
				this.tenant(),
				this.backlogItemId(),
				this.sprintId()));
	}
	...
}
```

Bu açık modelin müşterisi daha güvenli bir zeminde faaliyet gösteriyor gibi görünmektedir:

```
// client commits the backlog item to a sprint
// by using a domain-specific behavior 

backlogItem.commitTo(sprint);
```

İlk örnek, tamamen **veri odaklı** bir yaklaşım kullanır. **Sorumluluk tamamen istemciye** aittir; istemci, backlog öğesini doğru şekilde bir sprint'e nasıl dahil edeceğini bilmelidir. Gerçekten bir domain modeli olmayan bu model, hiçbir şekilde yardımcı olmaz. Ya istemci yanlışlıkla yalnızca **sprintId'yi değiştirirse** ama durumu değiştirmezse, ya da tam tersini yaparsa? Ya da gelecekte başka bir özelliğin ayarlanması gerekirse? İstemci kodu, verilerin doğru attribute'lara nasıl haritalandığını analiz etmelidir.

Bu yaklaşım aynı zamanda **BacklogItem nesnesinin şeklini** açığa çıkarır ve dikkatini tamamen **veri attribute'ları** üzerinde toplar, **davranışlar üzerinde değil**. **setSprintId()** ve **setStatus()** işlevlerinin davranışlar olduğunu savunsanız da, burada önemli olan nokta, bu “davranışların” gerçek bir iş domaini değeri taşımamasıdır. Bu “davranışlar”, domain yazılımının modellemesi gereken senaryoların, yani bir backlog öğesini bir sprint'e dahil etme amacının niyetlerini açıkça belirtmez. Ayrıca, istemci geliştiricisinin, bir backlog öğesini bir sprint'e dahil etmek için hangi **BacklogItem attribute'larını** seçeceğini düşünmesi gerektiği için bilişsel yük yaratır. Çünkü bu, veri odaklı bir modeldir.

Şimdi ikinci örneği ele alalım. Veri attribute'larını istemcilere sunmak yerine, açıkça ve net bir şekilde istemcinin bir backlog öğesini bir sprint'e dahil edebileceğini belirten bir **davranış** sunar. Bu belirli domain uzmanları, modelin aşağıdaki gereksinimini tartışır:

> Her backlog öğesinin bir sprint'e dahil edilmesine izin verin. Ancak yalnızca zaten bir sürüm için planlanmışsa dahil edilebilir. Eğer başka bir sprint'e dahil edilmişse, önce o sprint'ten çıkarılmalıdır. Dahil etme işlemi tamamlandığında, ilgili taraflara bildirimde bulunun.

Böylece, ikinci örnekteki metot, modelin Ubiquitous Language'ini bağlamda, yani **BacklogItem türünün izole edildiği Bounded Context'te** yakalar. Bu senaryoyu incelediğimizde, ilk çözümün eksik ve hatalar içerdiğini keşfederiz.

İkinci implementasyonla istemcilerin, işlemi gerçekleştirmek için gerekenleri bilmesine gerek yoktur; işlem ne kadar basit veya karmaşık olursa olsun, bu metodun implementasyonu gerektiği kadar mantık içerir. Henüz sürüm için planlanmamış bir backlog öğesinin dahil edilmesini engellemek için kolayca bir **koruma** ekledik. Gerçekten de ilk implementasyondaki setter'lar içine korumalar ekleyebilirsiniz, ancak bu durumda setter, sprintId ve status için gereksinimleri anlamaktan ziyade nesnenin tam bağlamını anlamaktan sorumlu olur.

Burada başka bir ince fark daha vardır. Eğer backlog öğesi başka bir sprint'e dahil edilmişse, önce mevcut sprint'ten çıkarılır. Bu önemli bir ayrıntıdır çünkü bir backlog öğesi bir sprint'ten çıkarıldığında, istemcilere bildirilmesi gereken bir **Domain Event** yayınlanır:

> Her backlog öğesinin bir sprint'ten çıkarılmasına izin verin. Backlog öğesi çıkarıldığında, ilgili taraflara bildirimde bulunun.

**Sprint'ten çıkarma bildirimini yayınlamak, yalnızca `uncommitFrom()` domain davranışını kullanarak otomatik olarak elde edilir.** `commitTo()` metodunun, bir bildirim yayınladığını bilmesine bile gerek yoktur. Tek bilmesi gereken, yeni bir sprint'e dahil olmadan önce mevcut sprint'ten çıkması gerektiğidir. **Ek olarak, `commitTo()` domain davranışı da son adım olarak ilgili taraflara bir Event ile bildirim gönderir.** Eğer bu zengin davranışı `BacklogItem` içine yerleştirmeseydik, Event'leri istemciden yayınlamamız gerekirdi. Bu da domain mantığının modelden sızmasına neden olurdu. Bu kötü bir yaklaşımdır.

Açıkça görülüyor ki, ikinci örnekteki `BacklogItem`'ı oluşturmak, birinciye kıyasla daha fazla düşünmeyi gerektiriyor. Ancak gereken ekstra çaba çok daha fazla fayda sağlıyor. Bu şekilde tasarım yapmayı öğrendikçe, süreç daha kolay hale gelir. Sonuç olarak, kesinlikle **daha fazla düşünme, daha fazla çaba, daha fazla iş birliği ve ekip çalışmalarının daha iyi koordine edilmesi** gerekiyor. Ancak bu ekstra çaba, DDD'yi ağır hale getirecek kadar büyük değildir. **Bu yeni düşünme şekli, harcanan çabaya fazlasıyla değer.**

**Düşünme Zamanı**

-   Şu anda çalıştığınız **belirli domain’i** kullanarak, modelin yaygın terimlerini ve eylemlerini düşünün.
-   Terimleri tahtaya yazın.
-   Daha sonra, ekibinizin proje hakkında konuşurken kullanması gereken ifadeleri yazın.
-   Bunları gerçek bir domain uzmanı ile tartışarak nasıl geliştirilebileceğini değerlendirin (kahve getirmeyi unutmayın!).


**_Alan Modelleme İçin Gerekçe_**

Taktiksel modelleme genellikle stratejik modellemeden daha karmaşıktır. Bu nedenle, **DDD'nin taktiksel desenlerini** (Kümeler, Servisler, Değer Nesneleri, Events vb.) kullanarak bir alan modeli geliştirmeyi planlıyorsanız, **daha fazla düşünme ve daha büyük bir yatırım** gerekecektir. Peki, bir organizasyon **taktiksel alan modellemesini nasıl haklı çıkarabilir?** DDD'nin baştan sona doğru bir şekilde uygulanabilmesi için ekstra yatırım gerektiren bir projeyi nasıl nitelendirebiliriz?

Kendinizi bilinmeyen bir bölgeden geçen bir keşif ekibine liderlik ederken hayal edin. Çevredeki toprakları ve sınırları anlamak istersiniz. Ekibiniz haritaları inceler, belki de kendi haritalarını çizer ve **stratejik yaklaşımlarını** belirler. Arazinin belirli yönlerini değerlendirir ve bunların avantajlarını nasıl kullanabileceğinizi düşünürsünüz. Ancak **ne kadar planlama yaparsanız yapın, bazı unsurlar gerçekten zor olacaktır.**

Eğer stratejiniz dik bir kaya yüzeyini tırmanmanız gerektiğini gösteriyorsa, buna uygun taktiksel araçlar ve manevralar kullanmanız gerekecektir. Aşağıdan yukarıya bakarken belirli zorlukları ve tehlikeli bölgeleri görebilirsiniz. Ancak **her detayı ancak kaya yüzeyine ulaştığınızda fark edersiniz.** Belki kaygan bir kayaya **kazık çakmanız gerekir**, belki de **doğal çatlaklara farklı boyutlarda kamalar sıkıştırarak** ilerleyebilirsiniz. Bu tırmanış desteklerine tutunmak için karabinalarınızı kullanırsınız. **Mümkün olduğunca düz bir rota çizmeye çalışırsınız** ancak **nokta nokta karar vermeniz gerekir.** Bazen **geri dönüp rotayı yeniden belirlemeniz bile gerekebilir**, çünkü **kaya yüzeyinin sunduğu koşullara göre hareket etmek zorundasınız.**

Birçok insan tırmanışı tehlikeli bir macera sporu olarak görse de, deneyimli tırmanıcılar bunun araba kullanmaktan veya uçakla seyahat etmekten daha güvenli olduğunu söyler. Tabii ki, bunun doğru olabilmesi için tırmanıcıların araçları ve teknikleri çok iyi anlamaları ve kayayı doğru değerlendirmeleri gerekir.

Eğer belirli bir Alt Alanın **(Subdomain)** geliştirilmesi böylesine zorlu ve hatta riskli bir tırmanışı gerektiriyorsa, **DDD'nin taktiksel desenlerini** yanımıza alarak bu tırmanışı gerçekleştirmeliyiz. Çekirdek Alan **(Core Domain)** kriterlerine uyan bir iş girişimi, taktiksel desenlerin kullanımını hızla göz ardı etmemelidir. **Çekirdek Alan bilinmeyen ve karmaşık bir bölgedir**. Takımın, sürecin ortasında **felaket niteliğinde bir düşüş yaşamaktan** korunması için doğru taktikleri kullanması en iyi yöntemdir.

İşte bazı pratik rehberler. Öncelikle genel düzeyde başlıyor, ardından detaylara iniyoruz:  

- Eğer bir Sınırlandırılmış Bağlam **(Bounded Context)**, Çekirdek Alan olarak geliştiriliyorsa, bu iş açısından stratejik olarak kritik öneme sahiptir. Çekirdek model henüz tam olarak anlaşılmamıştır ve çok sayıda deney ve yeniden düzenleme (refactoring) gerektirecektir. Uzun vadeli bir taahhüt ve sürekli iyileştirme gerektiriyor olabilir. Bu alan her zaman Çekirdek Alanınız olmayabilir. Ancak, eğer Sınırlandırılmış Bağlam karmaşıksa, yenilikçi bir yapıya sahipse ve uzun vadede değişime uğrayarak varlığını sürdürmesi gerekiyorsa, taktiksel desenleri kullanmayı ciddi şekilde düşünmelisiniz. Bu aynı zamanda, Çekirdek Alanın en yetenekli geliştirici kaynaklarını ve yüksek bir beceri seviyesini hak ettiği anlamına gelir.

- Tüketicileri açısından **Genel Alt Alan (Generic Subdomain)** veya **Destekleyici Alt Alan (Supporting Subdomain)** olabilecek bir alan, aslında sizin işiniz için bir Çekirdek Alan olabilir. Alanı her zaman **nihai tüketicilerin bakış açısından** değerlendirmezsiniz. Eğer bir Sınırlandırılmış Bağlam, ana iş girişiminizin bir parçası olarak geliştiriliyorsa, dış müşterilerin nasıl gördüğünden bağımsız olarak bu alan sizin için bir Çekirdek Alandır. Bu durumda **taktiksel desenleri kullanmayı ciddi şekilde düşünmelisiniz.**  

- Eğer bir Destekleyici Alt Alan (Supporting Subdomain) geliştiriyorsanız ve bunu bir üçüncü taraf Genel Alt Alan (Generic Subdomain) olarak temin edemiyorsanız, taktiksel desenler bu alandaki çabalarınıza fayda sağlayabilir. Bu durumda takımın yetkinlik seviyesini ve modelin ne kadar yeni ve yenilikçi olduğunu göz önünde bulundurmalısınız. Eğer model, özel bir iş değeri katıyor, belirli bir uzmanlığı içeriyor ve sadece teknik olarak ilginç olmanın ötesine geçiyorsa, yenilikçidir. Eğer takım, taktiksel tasarımı doğru şekilde uygulayacak yetkinliğe sahipse ve Destekleyici Alt Alan yenilikçi olup uzun yıllar boyunca varlığını sürdürecekse, bu alan için taktiksel tasarıma yatırım yapmak iyi bir fırsattır. Ancak,bu durum bu modeli Çekirdek Alan yapmaz, çünkü iş açısından sadece destekleyici bir roldedir.

Eğer işinizde alan modelleme konusunda geniş deneyime sahip ve bu konuda kendini rahat hisseden birçok geliştirici çalışıyorsa, bu yönergeler biraz kısıtlayıcı görünebilir. Eğer deneyim seviyesi çok yüksekse ve mühendisler taktiksel desenlerin en iyi seçim olacağını düşünüyorlarsa, onların görüşüne güvenmek mantıklıdır. Deneyimli geliştiriciler bile dürüst bir şekilde, belirli bir durumda bir alan modeli geliştirmenin en iyi seçim olup olmadığını belirteceklerdir.

**İş alanının türü, otomatik olarak geliştirme yaklaşımının nasıl seçileceğini belirlemez.** Takımınız, nihai kararı vermek için bazı **önemli soruları** göz önünde bulundurmalıdır. İşte önceki üst düzey yönergelerle uyumlu ve onları genişleten **daha ayrıntılı karar parametrelerinden oluşan kısa bir liste**:  

- Alan uzmanları mevcut mu ve onlarla bir ekip oluşturma konusunda kararlı mısınız?
- Belirli iş alanı şu anda nispeten basit olsa da zamanla daha karmaşık hale gelecek mi? **Transaction Script**, karmaşık uygulamalar için risklidir. Eğer şimdi Transaction Script kullanılırsa, bağlam (Context) daha karmaşık hale geldiğinde, daha sonra davranış odaklı bir alan modeline geçiş yapmak pratik olacak mı?
- DDD’nin taktiksel desenlerinin kullanımı, ister üçüncü taraf ister özel olarak geliştirilmiş olsun, diğer Sınırlandırılmış Bağlamlarla (Bounded Context) entegrasyonu kolaylaştıracak mı?
- Transaction Script kullanılırsa geliştirme gerçekten daha basit olacak mı ve daha az kod gerektirecek mi? (Her iki yaklaşımla deneyim gösteriyor ki, çoğu zaman Transaction Script en az aynı miktarda veya daha fazla kod gerektiriyor. Bunun nedeni büyük olasılıkla, alanın karmaşıklığının ve modelin yenilikçi yapısının proje planlamasında tam olarak anlaşılamamasıdır. **Alan karmaşıklığını ve yeniliği küçümsemek sık görülen bir hatadır.**)
- Kritik yol ve zaman çizelgesi, taktiksel yatırım için gereken ek yükü kaldırabilecek mi?
- Çekirdek Alan’a yapılan taktiksel yatırım, sistemi değişen mimari etkilerden koruyacak mı? (Transaction Script, sistemi bu etkilere karşı savunmasız bırakabilir. Alan modelleri genellikle uzun ömürlüdür, ancak mimari değişimler diğer katmanları daha fazla etkileyebilir.)
- Müşteriler/dış kullanıcılar, daha temiz, uzun ömürlü bir tasarım ve geliştirme yaklaşımından fayda sağlayacak mı, yoksa yarın bu uygulamanın yerini hazır bir çözüm alabilir mi? Başka bir deyişle, **bu uygulama/hizmeti neden özel olarak geliştirmemiz gerektiğini sorgulamalıyız.**  
- Taktiksel DDD kullanarak bir uygulama/hizmet geliştirmek, Transaction Script gibi diğer yaklaşımlardan daha zor olacak mı? (Bu sorunun yanıtında takımın yetkinlik seviyesi ve alan uzmanlarının erişilebilirliği kritik öneme sahiptir.)  
- Eğer takımın araç seti DDD’yi destekleyen unsurlarla eksiksiz olsaydı, yine de başka bir yaklaşımı seçer miydik? (Bazı unsurlar **modelin kalıcılığını (persistence) daha pratik hale getirir**, örneğin: **nesne-ilişkisel haritalama (ORM), tam Aggregate serileştirme ve kalıcılık, bir Olay Mağazası (Event Store) veya taktiksel DDD’yi destekleyen bir framework**. Bunların dışında başka yardımcı unsurlar da olabilir.)  

Bu liste, alanınıza özel bir önceliklendirme içermemektedir ve muhtemelen ek kriterler belirleyebilirsiniz. İşiniz için en güçlü ve avantajlı yöntemleri kullanmanın ikna edici nedenlerini anlıyorsunuz. Aynı zamanda iş ve teknoloji ortamınızı da en iyi siz biliyorsunuz. **Sonuçta, tatmin edilmesi gereken kişiler nesne yönelimli geliştiriciler veya teknoloji uzmanları değil, iş müşterileridir. Bu yüzden akıllıca seçim yapın.**

**_DDD Ağır Bir Yük Değildir_**

DDD’nin doğru şekilde uygulanmasının, ağır ve törensel bir süreç gerektirdiğini, desteklenmesi gereken gereksiz dokümantasyon çıktıları oluşturduğunu ima etmek istemiyorum. DDD bununla ilgili değildir. Scrum gibi herhangi bir çevik proje çerçevesine kolayca entegre olacak şekilde tasarlanmıştır. **Tasarım ilkeleri, gerçek bir yazılım modelinin test-öncelikli ve hızlı şekilde iyileştirilmesini teşvik eder.**  

Eğer yeni bir alan nesnesi (Entity veya Value Object gibi) geliştirmeniz gerekirse, **test-öncelikli** yaklaşım şu şekilde işler:  

1. Yeni alan nesnesinin, alan modelinin bir istemcisi tarafından nasıl kullanılacağını gösteren bir test yazın.
2. Testin derlenmesini sağlayacak kadar kod içeren yeni alan nesnesini oluşturun.
3. Hem testi hem de alan nesnesini, testin istemcinin nesneyi nasıl kullanacağını doğru şekilde temsil ettiğinden emin olana kadar iyileştirin. Ayrıca alan nesnesinin uygun davranışsal metot imzalarına sahip olmasını sağlayın.
4. Her alan nesnesinin davranışlarını uygulayın ve test geçene kadar alan nesnesini iyileştirin. Gereksiz kod tekrarlarını ortadan kaldırın.  
5. Kodunuzu takım üyelerine ve alan uzmanlarına göstererek, testin yaygın Dil (Ubiquitous Language) çerçevesinde alan nesnesini doğru şekilde kullandığından emin olun.

**Bu sürecin, zaten uygulamakta olduğunuz test-öncelikli yaklaşımdan farklı olmadığını düşünebilirsiniz.** Aslında biraz farklı olabilir, ancak temelde **aynı prensiplere dayanır.** Bu test aşaması, modelin kusursuz olduğunu kanıtlamaya çalışmaz. Bunun yerine, öncelikle **modelin nasıl kullanılacağını belirlemeye ve bu kullanımı yönlendiren testlerle tasarımı şekillendirmeye odaklanırız.** İyi haber şu ki bu gerçekten çevik bir yaklaşımdır. **DDD, törensel ve ağır bir tasarım sürecini teşvik etmez; aksine hafif ve esnek bir geliştirme süreci sunar.**  

Daha sonraki aşamalarda, yeni alan nesnesinin her açıdan (ve pratik olarak mümkün olan her senaryoda) doğruluğunu test eden ek testler yazarsınız. Bu noktada, alan nesnesinin içindeki alan kavramının doğru ifade edilip edilmediğiyle ilgilenirsiniz. İstemci benzeri test kodunu okumak, Yaygın Dil’i (Ubiquitous Language) doğru bir şekilde yansıttığını göstermelidir. Teknik bilgisi olmayan alan uzmanları bile bir geliştiricinin yardımıyla **bu kodu yeterince iyi okuyabilmeli ve modelin takımın hedeflerine ulaşıp ulaşmadığını değerlendirebilmelidir.**  

Bu durum, test verilerinin gerçekçi olması gerektiği anlamına gelir. **Testler, modelin ifadesini desteklemeli ve güçlendirmelidir.** Aksi takdirde, **alan uzmanları uygulamanın doğruluğu hakkında tam bir yargıya varamaz.**  

Bu test-öncelikli çevik metodoloji, mevcut iterasyon kapsamında belirlenen görevler tamamlanana kadar tekrar eder. Bu yaklaşım, çevik prensiplerle uyumludur ve Extreme Programming (XP) tarafından başlangıçta önerilen uygulamaları yansıtır. Çevik geliştirme, DDD’nin temel desen ve uygulamalarını ortadan kaldırmaz; aksine, bu iki yaklaşım bir arada oldukça iyi çalışır. Elbette, test-öncelikli geliştirme yapmadan da tam kapsamlı DDD uygulayabilirsiniz. Mevcut model nesneleri için her zaman sonradan testler yazabilirsiniz. Ancak, modelin istemci perspektifinden tasarlanması, ek bir avantaj sunar.


## **Gerçeklik Dolu Bir Kurgu**  

Modern DDD uygulamaları için en iyi uygulama rehberini nasıl sunabileceğimi düşünürken, önerdiğim her şeyin neden yapılması gerektiğini de açıklamak istedim. Yani sadece **"nasıl"** değil, **"neden"** sorusuna da yanıt vermeliydim. Birkaç projeyi vaka çalışması olarak ele almak, belirli bir öneride bulunmamın nedenlerini göstermek ve DDD’nin yaygın karşılaşılan zorlukları nasıl çözdüğünü ortaya koymak açısından doğru bir yöntem gibi geldi.

Bazen **diğer proje ekiplerinin karşılaştığı sorunları incelemek ve onların DDD’yi yanlış kullanımlarından ders çıkarmak, kendi hatalarımıza bakmaktan daha kolaydır.** Başkalarının çalışmalarındaki eksiklikleri fark ettiğinizde, siz de benzer bir çıkmaza sürüklenip sürüklenmediğinizi veya aynı bataklıkta olup olmadığınızı değerlendirebilirsiniz. Böylece, bulunduğunuz noktayı anladıktan sonra, hataları düzeltmek ve gelecekte aynı sorunları yaşamamak için gerekli değişiklikleri yapabilirsiniz.

Ancak, üzerinde çalıştığım gerçek projeleri anlatmak yerine —zaten bunları açıkça paylaşmam mümkün değil— gerçek dünyadaki durumlara dayanan kurgusal senaryolar kullanmaya karar verdim. Böylece, belli bir uygulama yaklaşımının neden en iyi ya da en azından daha iyi çalıştığını göstermek için ideal koşulları yaratabilirim.

Dolayısıyla burada yalnızca bir kurgu oluşturmuyorum. **Gerçek dünyada faaliyet gösteren bir şirketin iş modeline sahip kurgusal bir firma, gerçek yazılımlar geliştiren ve dağıtan kurgusal ekipler ve gerçek dünyadaki DDD zorlukları ile çözümleri yer alıyor.** Ben buna **"gerçeklik dolu kurgu"** diyorum. Bu yöntemin oldukça etkili olduğunu gördüm ve umarım sizin için de faydalı olur.

Herhangi bir dizi örnek sunarken, konunun öğretilebilir ve öğrenilebilir olmasını sağlamak için kapsamı belirli bir çerçevede tutmalıyız. Aksi takdirde aşırı detaylar içinde boğulabiliriz. Aynı zamanda, örneklerin fazla basit olması da kritik dersleri kaçırmamıza neden olabilir. Bu dengeyi sağlamak için seçtiğim iş senaryosu, büyük ölçüde sıfırdan (greenfield) geliştirme projelerine dayanıyor.

Projeleri farklı zaman dilimlerinde inceledikçe, **ekiplerin yaşadığı çeşitli sorunları ve başarıları göreceğiz.** Örneklerdeki Core Domain, DDD’yi farklı açılardan ele alabilecek kadar karmaşık olacak. Bounded Context’lerimizin bazıları **diğer bağlamlarla etkileşim içinde olacak, böylece DDD’nin entegrasyon süreçlerini de inceleyebileceğiz.** Ancak, bu üç örnek model, her türlü stratejik tasarım sürecini kapsayamaz. Özellikle, çok sayıda eski (legacy) sistemin bulunduğu "brownfield" ortamlardaki zorlukları tam anlamıyla göstermek mümkün değil. Yine de bu gibi karmaşık durumları tamamen göz ardı etmeyeceğim. Uygun olduğu durumlarda, ana örneklerden saparak DDD’nin daha geniş bir perspektifte nasıl avantajlar sunduğunu da inceleyeceğiz.

Şimdi sizi **şirketle tanıştırayım ve ekipleri ile üzerinde çalıştıkları projeler hakkında biraz bilgi vereyim.**

**_SaaSOvation, Ürünleri ve DDD Kullanımı_**

Şirketin adı **SaaSOvation.** Adından da anlaşılacağı gibi, SaaSOvation’ın misyonu, bir dizi hizmet olarak yazılım **(SaaS)** ürünü geliştirmek. Bu SaaS ürünleri **SaaSOvation tarafından barındırılacak** ve **abone olan şirketler tarafından erişilip kullanılacak.** Şirketin iş planı, biri diğerinin öncüsü olacak şekilde iki ürün geliştirmeyi içeriyor.

1. _Amiral Gemisi Ürün: CollabOvation_

SaaSOvation’ın amiral gemisi ürünü **CollabOvation.** Bu ürün, **kurumsal iş birliği için tasarlanmış bir platform** olup, önde gelen sosyal ağların sunduğu özellikleri içeriyor. Forumlar, paylaşılan takvimler, bloglar, anlık mesajlaşma, wiki, mesaj panoları, doküman yönetimi, duyurular ve uyarılar, aktivite takibi ve RSS beslemeleri gibi araçlar bu pakette yer alıyor.  

Tüm bu iş birliği araçları, şirketlerin hem küçük projelerde hem büyük programlarda hem de iş birimleri genelinde verimliliği artırmasına yardımcı olmak için tasarlanmış. Günümüzün hızla değişen ve belirsizliklerle dolu ekonomik ortamında, şirket içi iş birliği bilgi transferini hızlandırmak, fikir paylaşımını teşvik etmek ve yaratıcı süreci etkili bir şekilde yönetmek için kritik öneme sahip. **CollabOvation, yüksek değerli bir çözüm sunarken, geliştiriciler için de önemli bir meydan okuma olacak.**  

2. _İkinci Ürün: ProjectOvation_

İkinci ürün olan **ProjectOvation**, SaaSOvation’ın **asıl odaklandığı Core Domain.** Bu araç, **çevik proje yönetimini kolaylaştırmayı amaçlıyor** ve **Scrum çerçevesini** temel alıyor. Scrum’ın geleneksel proje yönetim modeliyle tamamen uyumlu olan ProjectOvation, şu bileşenleri içeriyor:  

- Ürün  
- Ürün sahibi  
- Takım  
- Backlog öğeleri  
- Planlanan sürümler  
- Sprintler  

Ayrıca, backlog öğelerinin iş değeri hesaplamalarını yapabilen maliyet-fayda analizi tabanlı hesaplama araçları da mevcut. Eğer Scrum’ın en güçlü halini düşünürsek, ProjectOvation tam olarak buraya yöneliyor. Ancak, SaaSOvation bundan daha fazlasını da hedefliyor.

_CollabOvation ve ProjectOvation Entegre Olacak_

SaaSOvation, bu iki ürünün tamamen ayrı yollar izlemesini istemiyor* Yönetim ekibi, çevik yazılım geliştirme süreçlerine iş birliği araçlarının entegre edilmesi konusunda yenilikçi bir yaklaşım benimsedi. Bu nedenle, **CollabOvation’ın belirli özellikleri, ProjectOvation’a isteğe bağlı bir ek paket olarak sunulacak.**  

Bu entegrasyon sayesinde, proje planlama, özellik ve hikâye tartışmaları, ekip ve ekipler arası iletişim ve destek süreçleri için iş birliği araçları sağlanmış olacak. SaaSOvation’ın tahminlerine göre, ProjectOvation abonelerinin %60’ından fazlası CollabOvation özelliklerini ek paket olarak satın alacak. 

Bunun da ötesinde, **bu tür ek paket satışları genellikle, ilgili ana ürünün de tam sürümüne geçişi teşvik eder.** Bir kez satış kanalı oluşturulduğunda ve yazılım geliştirme ekipleri proje yönetiminde iş birliğinin gücünü gördüğünde, bu heyecan kurumsal seviyede tam iş birliği paketinin benimsenmesine yol açabilir. Bu nedenle, **SaaSOvation, ProjectOvation satışlarının en az %35’inin tam CollabOvation paketine geçişle sonuçlanacağını tahmin ediyor.** Üstelik, bu tahmin muhafazakâr bir yaklaşım olarak değerlendiriliyor ve bu başarının oldukça büyük olacağı öngörülüyor.

CollabOvation geliştirme ekibi, şirkette ilk olarak kurulan ekip oldu. Bu ekipte birkaç kıdemli geliştirici yer alırken, çoğunluk orta seviyedeki geliştiricilerden oluşuyordu. İlk toplantılarda **Domain-Driven Design (DDD)** metodolojisinin benimsenmesine karar verildi. Ekipteki iki kıdemli geliştiriciden biri, önceki iş yerinde DDD’nin bazı taktiksel desenlerini kullanmıştı. Ancak, daha deneyimli bir DDD uygulayıcısı olsaydı, bu yaklaşımın tam anlamıyla DDD olmadığını fark ederdi. Aslında yaptığı şey, genellikle **DDD-Lite** olarak adlandırılan bir yaklaşımdı.

**DDD-Lite**, DDD’nin bazı taktiksel desenlerini seçici bir şekilde kullanmak, ancak:  

- Ubiquitous Language’i (Ortak Dil) keşfetmeye, yakalamaya ve geliştirmeye tam anlamıyla odaklanmamak,
- Bounded Context (Sınırlı Bağlamlar) ve Context Mapping (Bağlam Haritalaması) kavramlarını atlamak anlamına geliyor.  

Bu yöntem **daha çok teknik bir bakış açısıyla, doğrudan teknik problemleri çözmeye odaklanıyor.** Faydaları olabilse de, stratejik modelleme içermediği sürece getirisi sınırlı kalıyor.

SaaSOvation ekibi **bu yöntemi benimsemişti.** Ancak **Bounded Context’leri ve Alt Alanları (Subdomains) tam anlamıyla anlamadıkları için bazı sorunlarla karşılaştılar.**  

Sorunlar yaşansa da, SaaSOvation daha büyük tuzaklardan kaçmayı başardı. Bunun temel sebebi, iki ana ürününün doğal olarak ayrı Bounded Context’ler oluşturmasıydı. Bu durum, CollabOvation ve ProjectOvation modellerinin ayrı tutulmasını sağladı. Ancak bu tamamen bir şans eseri gerçekleşti. Ekibin Bounded Context kavramını bilinçli olarak uygulamamış olması, yaşadıkları bazı sorunların kaynağıydı.

Sonuç olarak: **_Ya öğrenirsiniz, ya da başarısız olursunuz._**

---

SaaSOvation ekibinin DDD'yi eksik bir şekilde kullanmasının incelenebilir olması bizim için faydalı. Ekip, stratejik tasarımı daha iyi kavrayarak hatalarından ders çıkarmayı başardı. **CollabOvation ekibinin yaptığı düzenlemelerden siz de öğreneceksiniz,** tıpkı ProjectOvation ekibinin, kardeş ve iş ortağı projenin ilk aşamalarına dair retrospektiflerden faydalandığı gibi. Tam hikayeyi görmek için şu bölümlere göz atabilirsiniz:  
- Alt Alanlar (Subdomains) (2)
- Sınırlı Bağlamlar (Bounded Contexts) (2)
- Bağlam Haritaları (Context Maps) (3)

---

## Sonuç

Evet, bu bölüm DDD'ye oldukça cesaret verici bir başlangıç oldu. Şimdiye kadar, siz ve ekibinizin aslında gelişmiş bir yazılım geliştirme tekniğinde başarılı olabileceğinizi iyi bir şekilde hissetmiş olmalısınız. Ben de aynı şekilde düşünüyorum. Tabii ki, her şeyi basite indirgemeyeceğiz. **DDD'yi uygulamak gerçek bir çaba gerektirir.** Eğer bu kolay olsaydı, herkes harika kodlar yazıyor olurdu ve bunun olmadığını biliyoruz. O yüzden hazırlıklı olun. Bu çaba değecek çünkü tasarımınız, yazılımınızın nasıl çalıştığına tam olarak uyacak.

Şimdiye kadar öğrendikleriniz:

- DDD'nin projeleriniz ve ekipleriniz için neler yapabileceğini, alan karmaşıklığıyla nasıl başa çıkabileceğinizi keşfettiniz.
- Projelerinizi değerlendirme ve DDD yatırımına değip değmediğini öğrenme yolunu öğrendiniz.
- DDD'ye alternatif olan yaygın yaklaşımları ve bu yaklaşımların neden çoğu zaman problemlere yol açtığını incelediniz.
- DDD'nin temellerini kavradınız ve projelerinizde ilk adımlarınızı atmaya hazırsınız.
- DDD'yi yönetiminize, alan uzmanlarına ve teknik ekip üyelerinize nasıl satacağınızı öğrendiniz.
- DDD'nin zorluklarıyla başa çıkarken nasıl başarılı olacağınızı öğrenmek için gerekli bilgilere sahipsiniz.

Sıradaki adımlarımız şu şekilde: **Sonraki iki bölüm, son derece önemli olan stratejik tasarım üzerine olacak** ve ardından **DDD ile yazılım mimarileri üzerine bir bölüm gelecek.** Bu, **taktiksel modelleme** ile ilgili sonraki bölümlere geçmeden önce kavrayışınızı güçlendirecek çok önemli bir konudur.