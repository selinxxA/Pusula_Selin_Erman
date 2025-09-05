# Pusula_Selin_Erman
Selin Erman ermanselin771@gmail.com

This project was prepared as part of the Pusula Talent Academy program.
The main goal is to perform Exploratory Data Analysis (EDA) on the provided dataset, clean and preprocess the data, and visualize key findings.

The steps include:

Handling missing values

Encoding categorical variables (e.g., gender, allergy information)

Standardizing and normalizing numerical variables if necessary

Creating visualizations such as histograms, bar charts, and correlation heatmaps

Running the Code:
Clone this repository or download the project files.

Place the dataset file Talent_Academy_Case_DT_2025.xlsx in the same directory as the code.


EDA & Preprocessing — Bulgular Özeti
Veri seti genel bilgileri
Toplam gözlem: 2235 satır
Sütun sayısı: 13 sütun
Değişken tipleri
Unique ID: HastaNo
Sayısal (numeric): Yas, TedaviSuresi, UygulamaSuresi
Kategorik: Cinsiyet, KanGrubu, Uyruk, KronikHastalik, Bolum, Alerji, TedaviAdi, UygulamaYerleri, Tanilar

Ekisk Veri (missing value) özeti:
HastaNo              0
Yas                  0
Cinsiyet           169
KanGrubu           675
Uyruk                0
KronikHastalik     611
Bolum               11
Alerji             944
Tanilar             75
TedaviAdi            0
TedaviSuresi         0
UygulamaYerleri    221
UygulamaSuresi       0

Gözlem: Eksik veriye sahip sütunlar temel olarak Cinsiyet, KanGrubu, KronikHastalik, Bolum, Alerji, Tanilar, UygulamaYerleri şeklindedir. Kronik Hastalık ve Alerji  sınıflarında olan verilerin eksikliği normaldir çünkü bu sonuçtan insanların hastalığa ya da alerjiye sahip olmadığı sonucuna varılmıştır. 
Eksik veri düzeltme (Imputation) — uygulanan yöntemler ve sonuçlar
Cinsiyet kategorisindeki eksik veriler için ; aynı hastanın (HastaNo) farklı satırlarda yer alan kayıtlarında bilgi varsa, aynı hastanın diğer satırlarındaki değerler kullanılarak eksikler dolduruldu. Teknik olarak uygulanan yöntem: groupby("HastaNo") ile grup oluşturup ffill() / bfill() veya benzeri işlemlerle doldurma yapıldı.Bu adım, gerçek hasta bilgilerini tahmin etmek yerine mevcut olanı kullanarak daha güvenilir bir imputation sağlar.
KanGrubu: Başlangıçta 1560 mevcut, 675 eksik. Hasta bazlı doldurma uygulandıktan sonra: 1591 mevcut, 644 eksik olarak raporlanmıştır (eksik sayısında azalma).
Cinsiyet: Başlangıçta 2066 mevcut, 169 eksik. Aynı hasta-bazlı doldurma sonrası: 2090 mevcut, 145 eksik olarak raporlanmıştır.


Kan grubuna value_count uygulanmıştır ve 8 farklı kategoriden 4 farklı kategoriye indirilerek değişken daraltılmıştır. 
Eksik Data Düzeltme
Analize dahil edilmeyen veriler vardır bunlar Tanilar ve TedaviAdi sınıflarıdır. Totalde 294 farklı Tanı sınıfı ortaya çıkmıştır bunlardan bazıları boş veri bazıları tanımsız karakter içermektedir ve bu verinin incelenmesini zorlaştırmaktadır. Sonuç olarak  anlaşılabilir bir analiz çıkmayacağı kanısına varılmıştır ve  verinin silinmesine karar verilmiştir.
Aynı şekilde TedaviAdi verisi 244 farklı sonuç vermiştir ve bu sonucun yorumlanmasından sağlıklı bir sonuç çıkmayacağına karar verilip veri silinmiştir.  
Duplication (çift kayıtlar): Veride aynı hastaya ait tekrarlı satırlar mı yoksa  tekrarlı ziyaret mi olduğu net olmadığı için duplikeler silinmedi. Bu karar modelleme aşamasında dikkat edilmesi gerektiğini işaret eder; tekrar kayıtların nasıl ele alınacağına göre (ör. yalnızca ilk kayıt alınması, tüm kayıtların tutulması vb.) ek kararlar verilmeli.
   
BoxPlot Grafik Yorumları
Sayısal verilerimden olan yaş , tedavi süresi ve uygulama sürelerinin Boxplot grafikleri oluşturuldu  fakat hedef değişken olan  Tedavi  süresi verilerinde 25%, 50% ve 75%  değerlerinin hepsi 15 olduğu için Boxplot grafiğinde anlamlı bir grafik oluşturulamamıştır bu yüzden farklı grafik oluşturma yöntemleri denenip verinin nasıl dağıldığı daha ayrıntılı incelenmiştir.
Tedavi süresi için histogram ve barplot denenmiş ve dağılımın en iyi barplot da görselleştirildiği sonucuna varılmıştır burada hangi değerin frekansının yüksek olduğu açık bir şekilde gözükmektedir. Aynı şekilde ECDF plot kullanılmış ve verinin hangi noktadan sonra nasıl biriktiğini görebiliyoruz. 
Kategorik/metin sütunlarında value_counts() ile frekans analizleri yapıldı; öne çıkan kategoriler belirlendi. Daha sonrasında Cinsiyet ve Uyruk sınıflarına kategorik dönüşüm uygulandı.
Modelin doğru şekilde beslenebilmesi adına kan grubu ve alerji kategorilerine de One-Hot Encoding yöntemi uygulanmıştır.       
Öneriler
Duplicate kayıtların incelenmesi: Aynı hastanın birden fazla kaydı araştırılmalı; eğer farklı ziyaretler ise korunmalı, aynı kayıtların tekrar olduğu tespit edilirse silinmelidir. Bu karar model sonuçlarını etkiler.
Kalan eksikler için gelişmiş imputation: Kalan missing değerler için KNNImputer, model-tabanlı tahmin (ör. RandomForest ile sınıflandırma) veya mantıksal atama yöntemleri değerlendirilebilir.





