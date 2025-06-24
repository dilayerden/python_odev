Airline Passenger Satisfaction - Veri Analizi Projesi
Proje Amacı
Bu proje, havayolu yolcu memnuniyet veri seti üzerinde:

İstatistiksel özet çıkarımı

Eksik değer analizi

Aykırı değer (outlier) tespiti

Sayısal ve kategorik değişkenlerin görselleştirilmesi

işlemlerini içeren kapsamlı bir veri analizi çalışmasıdır.

 Veri Seti Hakkında
Kaynak: Kaggle - Airline Passenger Satisfaction

Boyut: ~130,000 gözlem

Özellikler: 24 sütun (müşteri demografik bilgileri, uçuş detayları, memnuniyet anketi)

  Analiz Yaklaşımı
1. İstatistiksel Özet
python
# Temel istatistikler
df.describe().T

# Kategorik değişken frekansları
df.select_dtypes(include='object').describe()
Çıktı Örnekleri:

Sayısal değişkenler için: min/max/ortalama/çeyreklik değerler

Kategorik değişkenler için: mod ve frekans dağılımları

2. Eksik Değer Analizi
python
# Eksik değer yüzdesi
missing = df.isnull().sum()/len(df)*100

# Görselleştirme
sns.heatmap(df.isnull(), cbar=False)
Analiz Sonuçları:

"Arrival Delay" sütununda %0.3 eksik veri

Eksik veri stratejisi: Medyan ile doldurma

3. Aykırı Değer Analizi
python
# Boxplot ile görselleştirme
plt.figure(figsize=(15,5))
sns.boxplot(data=df.select_dtypes(include=['int64','float64']))
plt.xticks(rotation=45)
Tespit Edilen Aykırı Değerler:

"Flight Distance" ve "Departure Delay" değişkenlerinde belirgin aykırı değerler

IQR yöntemi ile tespit ve baskılama uygulanabilir

4. Görsel Analizler
Sayısal Değişkenler
python
# Histogram grid
df.hist(figsize=(20,15), bins=30)
plt.tight_layout()
Kategorik Değişkenler
python
# Memnuniyet dağılımı
plt.figure(figsize=(6,4))
df['satisfaction'].value_counts().plot(kind='pie', autopct='%1.1f%%')
Korelasyon Analizi
python
plt.figure(figsize=(12,8))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
 Önemli Bulgular
Memnuniyet Dağılımı:

%43.5 memnun (satisfied)

%56.5 memnun değil (neutral or dissatisfied)

En Yüksek Korelasyonlar:

Online boarding - Satisfaction (+0.39)

Inflight wifi service - Satisfaction (-0.34)

Aykırı Değerler:

Uçuş gecikmelerinde 1500 dakikayı aşan ekstrem değerler

  Proje Yapısı
text
airline-analysis/
├── data/
│   └── airline_passenger_satisfaction.csv
├── notebooks/
│   └── Airline_Data_Analysis.ipynb
├── reports/
│   └── findings.md
└── README.md
🚀 Çalıştırma
bash
# Gereksinimler
pip install pandas numpy matplotlib seaborn jupyter
