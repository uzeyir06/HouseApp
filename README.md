# HouseApp

ML .Net, .NET geliştiricileri için tasarlanmış, açık kaynaklı, platformlar arası bir makine öğrenimi çerçevesidir. Python (rutinler C++ ile yazılır) genellikle birçok ML kitaplığı geliştirmek için kullanılır, örneğin TensorFlow ve bu, ML bileşenlerini .Net platformuna sıkı bir şekilde entegre etmeniz gerektiğinde ekstra adımlar ve engeller ekleyebilir.

ML .NET kullanarak bir ev fiyatını tahmin etme
ML .Net, makine öğrenimi uygulamalarını .NET kullanarak entegre etmenize olanak tanıyan harika bir araç seti sağlar - ML .NET hakkında daha fazla bilgiyi burada bulabilirsiniz

ML .NET, bir dizi ML sistemi geliştirmenize olanak tanır

Tahmin/Regresyon

Sorun Sınıflandırma

Öngörücü bakım

Görüntü sınıflandırması

Duygu Analizi

Öneri Sistemleri

kümeleme sistemleri

ML .NET, tipik ML iş akışını destekleyen, makine öğrenimi için geliştirici dostu bir API sağlar:

Farklı veri türleri yükleme (Test, IEnumerable, Binary, Parquet, File Sets)

Verileri Dönüştür Özellik seçimi, normalleştirme, şemayı değiştirme, kategori kodlama, eksik verileri işleme

Probleminize uygun algoritma seçimi (Linear, Boosted tree, SVM, K-Means).

Eğitim (Eğitim ve değerlendirme modelleri)

Modelin Değerlendirilmesi

Dağıtım ve Çalıştırma (eğitilmiş modeli kullanarak)

ML .NET çerçevesini kullanmanın önemli bir avantajı, kullanıcının sorunları için en iyi sonuçları elde etmek için özellik kümesini, eğitim boyutlarını ve test veri kümelerini değiştirerek farklı öğrenme algoritmalarıyla hızlı bir şekilde deneme yapmasına olanak sağlamasıdır. Deney, ekiplerin gereksiz verileri toplamak için çok zaman harcadığı ve iyi performans göstermeyen modeller ürettiği yaygın bir sorunu önler.

Pipelines Öğrenme
ML .NET, veri hazırlama ve model eğitimi için dönüşümleri tek bir ardışık düzende birleştirir, bunlar daha sonra eğitim verilerine ve modelinizde tahminler yapmak için kullanılan girdi verilerine uygulanır.

ML .NET'i tartışırken, aşağıdakilerin kullanımını tanımak önemlidir:

Transformatörler - bunlar verileri dönüştürür ve işler ve çıktı olarak veri üretir.

Tahminciler - bunlar veri alır ve örneğin eğitim sırasında bir transformatör veya model sağlar

Tahmin - bu, tek bir özellik satırı kullanır ve tek bir sonuç satırını tahmin eder.



Basit regresyon örneğinde bunların nasıl devreye girdiğini göreceğiz.

Ev fiyat örneği
İşlevselliğin tipik veri hazırlama iş akışına nasıl uyduğunu anlamak, modeli eğitmek ve test veri kümelerini ve modeli kullanarak uygunluğu değerlendirmek. Yaklaşık 800'den fazla ev satışından oluşan basit bir dizi özellik verilen bir evin satış fiyatını tahmin etmek için basit bir regresyon uygulaması uygulamaya bir göz attım. Örnekte, çok değişkenli doğrusal regresyonun denetimli bir öğrenme problemine bakacağız. Bir etiketin değerini bir dizi özellikten tahmin etmek için denetimli bir öğrenme görevi kullanılır. Bu durumda, bir evin satış fiyatını (etiketi) tahmin etmek için bir veya daha fazla özellik kullanmak istiyoruz.

Odak noktası, daha sonra özellik seçimi ve eğitim algoritmaları ile deneme yapmak için kullanılabilecek küçük bir numuneyi hazır hale getirmek ve çalıştırmaktı. Bu makalenin kodunu GitHub'da burada bulabilirsiniz .

Yaklaşık 800 ev satışının üzerinde bir dizi özellik verilen bir evin satış fiyatını tahmin etmek için bir dizi satış verisini kullanarak modeli eğiteceğiz. Örnek veriler çok çeşitli özelliklere sahip olsa da, kullanışlı bir sistem geliştirmenin önemli bir yönü, kullanılan özelliklerin seçiminin modeli etkilediğini anlamak olacaktır.

Başlamadan önce

Kurulum ve ön gereklilikler konusunda size yol gösterecek 10 dakikalık bir eğitim bulabilir veya sadece aşağıdaki adımları kullanabilirsiniz.

.NET Core'un yüklü olduğu Visual Studio 16.6 veya sonraki bir sürümüne sahip olmanız gerekecek, buradan ulaşabilirsiniz.

.NET uygulamaları oluşturmaya başlamak için .NET SDK'yı indirip yüklemeniz yeterlidir .

Bir komut isteminde aşağıdakileri çalıştırarak ML.Net Paketini yükleyin

dotnet add package Microsoft.ML --version 0.10.0


Veri Sınıfı
İlk işimiz, house data .csv dosyamızı yüklerken kullanabileceğimiz bir data class tanımlamak. Unutulmaması gereken önemli kısım, [LoadColumn()] öznitelikleridir; bunlar, alanları girdideki farklı sütunlarla ilişkilendirmemize izin verir. İşleyebileceğimiz veri kümelerindeki değişikliklere uyum sağlamanın basit bir yolunu sunar. Bir kullanıcı bir evin fiyatını tahmin etmek istediğinde, özellikleri vermek için veri sınıfını kullanır. Modeli eğitirken sınıftaki tüm alanları kullanmamıza gerek olmadığını unutmayın.



Modeli Eğitim ve Kaydetme
CreateHousePriceModelUsingPipeline(…) yöntemi, ev fiyatlarını tahmin etmek için kullanılan modeli oluşturmadaki ilginç çalışmaların çoğunu yapar.

Kod parçacığı, şunları nasıl yapabileceğinizi gösterir:

Bir .csv dosyasındaki verileri okuyun

Eğitim algoritmasını seçin

Antrenman yaparken kullanılacak özellikleri seçin

Dize özelliklerini ele al

Verileri işlemek ve modeli eğitmek için bir işlem hattı oluşturun

Bu tür problemlerde, genellikle gelen verileri normalleştirmeniz gerekir, Odalar ve Yatak Odaları özelliğini göz önünde bulundurun, Odalar değer aralığı genellikle Yatak Odalarından daha büyüktür, bunları uyum üzerinde aynı etkiye sahip olacak ve hızlandırmak için normalleştiririz ( eğitmene bağlı olarak) takma zamanı. Kullandığımız eğitmen, özellikleri otomatik olarak normalleştirir, ancak çerçeve, bunu kendiniz yapmanız gerekiyorsa normalleştirmeyi destekleyen araçlar sağlar.

Benzer şekilde, kullanılan özelliklerin sayısına bağlı olarak (ve model fazla uyuyorsa) eğitmene Düzenlileştirme uygularız - bu aslında tüm özellikleri korur ancak etkiyi azaltmak için özellik parametrelerinin her birine bir ağırlık ekler. Örnekte, eğitmen düzenlemeyi yapacaktır; alternatif olarak, eğitmeni oluştururken düzenleme ayarlamaları yapabilirsiniz.



Değerlendirme
Eğitimden sonra test verilerini kullanarak modelimizi değerlendirmemiz gerekiyor, bu tahmin edilen sonuç ile gerçek sonuçlar arasındaki hatanın boyutunu gösterecektir. Hatayı azaltmak, en iyi özellik karışımını belirlemek için nispeten küçük bir veri kümesi üzerinde yinelemeli bir sürecin parçası olacaktır. ML .NET tarafından desteklenen farklı yaklaşımlar vardır . Model kalitesinin bir çalıştırmadan diğerine varyansını tahmin etmek için çapraz doğrulama kullanıyoruz ve ayrıca değerlendirme için ayrı bir test seti çıkarma ihtiyacını ortadan kaldırıyor. Modelin doğruluk metriklerini değerlendirmek ve almak için kalite metriklerini görüntüleriz



İki metriğe bakacağız:

L1 Kaybı - bunu en aza indirmeniz gerekir, ancak giriş etiketleri normalleştirilmemişse bu oldukça yüksek olabilir.

R-kare - uyumun iyiliğinin bir ölçüsünü sağlar, çünkü doğrusal regresyon modelleri 0 -> 1 arasında olacaktır, 1'e ne kadar yakınsa o kadar iyidir.

Mutlak kayıp L1 = (1/m) * toplam( abs( yi - y'i)) olarak tanımlanır

Mevcut metriklerin bir açıklamasını burada bulabilirsiniz .

Kodu 0.608'lik bir R-Sqaured verdiği gibi çalıştırmak, bunu geliştirmek isteyeceğiz. İlk adım, özellik seçimiyle denemeye başlamak, belki de daha net bir anlayışa sahip olduktan sonra azaltılmış bir özellik listesiyle başlamak ve daha sonra daha geniş bir veri kümesi almayı düşünmek olacaktır.

Modeli daha sonra kullanmak üzere kaydetme
Ev fiyatlarını tahmin etmek için kullanılan modeli saklamak kolaydır

// Modeli, son kullanıcı uygulamalarından daha sonra kullanmak üzere kaydedin
using (var file = File.OpenWrite(outputModelPath))
    model.SaveTo(mlContext, file);


Ev satış fiyatlarını yükleyin ve tahmin edin

Özellikleri değiştirip farklı eğitimi değerlendirdikten sonra, modeli satış fiyatlarını tahmin etmek için kullanabilirsiniz. Bence bu, ML .NET çerçevesinin parladığı yer çünkü daha sonra modeli kullanmanın farklı yollarını desteklemek için .Net'teki harika araçları kullanabiliriz.


Bu tür bir ML uygulaması için tipik bir kullanım, Windows Azure'a dağıtılan bir docker kapsayıcısında çalışan basit bir REST hizmeti oluşturmak olacaktır. Javascript ile yazılmış bir web uygulaması, insanların bir evin ne için satması gerektiğini hızlı bir şekilde görmelerini sağlamak için hizmeti tüketir.

.Net Core kullanarak arka ucu farklı donanım platformlarında çalıştırabiliriz, Visual Studio 2019, 2017 sağlam bir hizmetin oluşturulmasını, dağıtılmasını ve yönetilmesini hızlı ve kolay hale getirir.
