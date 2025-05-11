# Python Clean Code Rehberi (Türkçe)

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![Status](https://img.shields.io/badge/status-active-success)](#)
![version](https://img.shields.io/badge/version-v1.1.0-blue)

> "Kod yalnızca makine için değil, onu okuyacak diğer insanlar için de yazılır."

Bu rehber, Python dilinde temiz, okunabilir ve sürdürülebilir kod yazma alışkanlıklarını geliştirmek amacıyla hazırlanmıştır. Amaç; kodu sadece çalışan bir yapı değil, aynı zamanda ekip içinde anlaşılır, bakımı kolay ve hataya daha az açık hale getirmektir.

Python geliştiricileri için geçerli olan temel prensipleri, örneklerle birlikte sunar. Her bölüm, bir konuyu ele alır ve iyi/kötü uygulama örnekleriyle desteklenir. Geliştiricilerin hem bireysel projelerde hem de ekip çalışmalarında daha temiz kod yazmaları hedeflenmiştir.

---
> 📌 Versiyon: **v1.1.0** – Son güncelleme: 11 Mayıs 2025  
> 🔗 [CHANGELOG.md](./CHANGELOG.md) dosyasından tüm sürüm geçmişine ulaşabilirsiniz.
---

## 📚 İçindekiler

* [1. Giriş ve Temel Felsefe](#1-giriş-ve-temel-felsefe)
* [2. Anlamli Degisken Isimleri](#2-anlamli-degisken-isimleri)
* [3. Fonksiyonlar ve Tek Sorumluluk](#3-fonksiyonlar-ve-tek-sorumluluk)
* [4. Kod Tekrarından Kaçınmak (DRY)](#4-kod-tekrarından-kaçınmak-dry)
* [5. Yorumlar ve Kodun Anlatımı](#5-yorumlar-ve-kodun-anlatımı)
* [6. Exception Handling (Hata Yönetimi)](#6-exception-handling-hata-yönetimi)
* [7. Kod Biçimlendirme ve Linter Kullanımı](#7-kod-biçimlendirme-ve-linter-kullanımı)
* [8. Kötü Pratikler (Anti-Patterns)](#8-kötü-pratikler-anti-patterns)
* [9. OOP ve Kompozisyon Prensipleri](#9-oop-ve-kompozisyon-prensipleri)
* [10. Pythonic Kod Yazımı](#10-pythonic-kod-yazımı)
* [11. Sihirli Sayılardan (Magic Numbers) Kaçının](#11-sihirli-sayılardan-magic-numbers-kaçının)
* [12. Modülerlik ve Sınıf Yapıları (Modularity and Classes)](#12-modülerlik-ve-sınıf-yapıları-modularity-and-classes)

---

## 1. Giriş ve Temel Felsefe

Python dili, belirli bir yazım felsefesine dayanır. Bu felsefe, yalnızca çalışır kod değil, okunabilir, anlaşılabilir ve sürdürülebilir kod üretmeyi öncelikli hale getirir. Bu yaklaşıma "The Zen of Python" adı verilir ve Python içinde doğrudan erişilebilir durumdadır:

```python
>>> import this
```

Zen of Python'dan bazı temel ilkeler:

* Güzel olan çirkinden iyidir.
* Açık olan örtük olandan iyidir.
* Basit olan karmaşıktan iyidir.
* Karmaşık olan anlaşılmazdan iyidir.
* Okunabilirlik önemlidir.

Bu ilkeler, Python ile geliştirme yaparken sadece dilin sözdizimine değil, aynı zamanda yazım tarzına da dikkat etmeniz gerektiğini ifade eder.

Clean Code yaklaşımı yalnızca Python'a özel değildir; evrensel bir yazılım mühendisliği disiplinidir. Ancak Python’un sadeliğe ve açıklığa verdiği önem nedeniyle bu yaklaşım dil ile doğrudan örtüşür.

Bu bölümün amacı, "neden temiz kod yazmalıyız?" sorusuna net bir cevap vermektir:

* Takım çalışmasında başkalarının sizin kodunuzu anlayabilmesi için,
* Gelecekte kendi kodunuzu tekrar okuduğunuzda zorluk yaşamamak için,
* Hataları azaltmak ve test edilebilirliği artırmak için,
* Yeni özellikleri kolayca ekleyebilmek için.

Bu rehberdeki her başlık, Python kodunu daha temiz, anlaşılır ve bakımı kolay hale getirmek için temel yapı taşlarını sunacaktır.

---

## 2. Anlamli Degisken Isimleri

Kodun en temel yapı taşlarından biri olan değişkenler, doğru isimlendirilmediği sürece kodun anlaşılabilirliğini doğrudan olumsuz etkiler. Değişken isimleri, değişkenin neyi temsil ettiğini açıkça göstermelidir. Kısa ama anlamsız, ya da çok uzun ama belirsiz isimlerden kaçınılmalıdır.

### Genel Kurallar:

* Anlamlı, açıklayıcı ve bağlamı ifade eden isimler kullanın.
* Tek harfli değişken isimlerini yalnızca döngü sayaçlarında kullanın (`i`, `j` gibi).
* Boole değişkenlerini `is_`, `has_`, `can_` gibi öneklerle tanımlayın.
* Kısaltmalardan kaçının, gerekirse açık yazın (`temp_user_id` > `tmp_id`).
* Negatif anlamlı isimlerden kaçının (`is_not_empty` yerine `is_empty == False` daha açık olabilir).

### ❌ Kötü Örnek:

```python
d = 100
t = 20
tp = d + t
```

### ✅ İyi Örnek:

```python
product_price = 100
tax_amount = 20
total_price = product_price + tax_amount
```

### Kötü Uygulamalardan Kaçınma:

* `x`, `y`, `z`, `data1`, `temp2` gibi bağlamsız isimler yalnızca kısa süreli değişkenler için kullanılmalıdır.
* `data`, `value`, `info`, `result` gibi aşırı genel isimler yerine daha belirleyici terimler tercih edilmelidir.

### Ekstra Not:

Geliştiricinin kodu yorum satırı olmadan bile anlayabilmesi gerekir. Anlamlı değişken ismi, çoğu zaman yoruma gerek bırakmaz.

---
## 3. Fonksiyonlar ve Tek Sorumluluk

Fonksiyonlar, kodun temel yapı taşlarındandır. Temiz kod yazımında bir fonksiyonun yalnızca **tek bir sorumluluğu** olması gerekir. Bu prensibe *Single Responsibility Principle (SRP)* denir.

Fonksiyonlar kısa, anlaşılır ve test edilebilir olmalıdır. Çok fazla iş yapan, uzun ve iç içe geçmiş fonksiyonlar hem okunabilirliği düşürür hem de bakım maliyetini artırır.

### Genel Kurallar

- Her fonksiyon yalnızca bir iş yapmalıdır.
- Fonksiyon isimleri açık, fiil temelli ve yaptığı işle uyumlu olmalıdır.
- Girdi sayısı mümkün olduğunca azaltılmalıdır (tercihen 3 veya daha az).
- Fonksiyon içindeki kod blokları, başka bir fonksiyonla kolayca ayrıştırılabilecek yapıdaysa bölünmelidir.

---

### ❌ Kötü Örnek

```python
def process_user(user):
    # validate user
    if not user.get("email"):
        raise ValueError("No email")
    # save to db
    db.save(user)
    # send email
    send_welcome_email(user["email"])
```

Bu fonksiyon birden fazla işi aynı anda yapıyor: doğrulama, veri kaydı ve bildirim. Bu, test yazmayı zorlaştırır ve hata ayıklamayı güçleştirir.

---

### ✅ İyi Örnek

```python
def validate_user(user):
    if not user.get("email"):
        raise ValueError("No email")

def save_user(user):
    db.save(user)

def notify_user(email):
    send_welcome_email(email)

def process_user(user):
    validate_user(user)
    save_user(user)
    notify_user(user["email"])
```

Her bir işlem ayrı fonksiyon haline getirilerek kod hem okunur hem de yeniden kullanılabilir hale gelir. Bu yaklaşım hata ayıklamayı da kolaylaştırır.

---

### Ekstra Notlar

- Test yazımı açısından, tek sorumluluk prensibine uygun fonksiyonlar daha kolay test edilir.
- Büyük fonksiyonlar zamanla daha da büyür; küçük fonksiyonlar ise bölünebilir, sadeleştirilebilir.
- Fonksiyon içinde `ve`, `veya`, `ama`, `hem...hem de` gibi ifadeler zihinsel karmaşıklığa yol açıyorsa, fonksiyon bölünmelidir.

---
## 4. Kod Tekrarından Kaçınmak (DRY)

Kod tekrarından kaçınmak yazılım geliştirmede temel bir ilkedir. Bu ilke genellikle "Don't Repeat Yourself (DRY)" şeklinde ifade edilir. Aynı kod veya mantık birden fazla yerde tekrarlandığında, bakım maliyeti ve hata riski artar.

### Genel Kurallar

- Aynı kod blokları birden fazla yerde kullanılıyorsa fonksiyon haline getirin.
- Tekrar eden verileri sabit (constant) olarak tanımlayın.
- Ortak işlem akışları için yardımcı modüller oluşturun.
- Magic number (sihirli sayı) kullanımından kaçının.

---

### ❌ Kötü Örnek

```python
print("User created successfully.")
# ...
print("User created successfully.")
```

Aynı metin iki kez tekrar ediyor. Bu durumda bir sabit ya da fonksiyon kullanmak daha doğrudur.

---

### ✅ İyi Örnek

```python
SUCCESS_MESSAGE = "User created successfully."

print(SUCCESS_MESSAGE)
# ...
print(SUCCESS_MESSAGE)
```

Ya da:

```python
def notify_user_created():
    print("User created successfully.")

notify_user_created()
# ...
notify_user_created()
```

---

### Avantajları

- Bir değişiklik gerektiğinde tek bir noktadan güncelleme yapılır.
- Hatalı kopyalama, unutulan güncellemeler gibi riskler azalır.
- Kod daha sade ve anlaşılır hale gelir.

---

### Nerede Sınır Koymalı?

DRY prensibini uygularken aşırı soyutlamadan kaçının. Her benzerlik soyutlama gerektirmez. Anlamlı tekrarlar bazen okunabilirliği artırabilir. DRY ile birlikte *KISS (Keep It Simple, Stupid)* prensibi de göz önünde bulundurulmalıdır.

---
## 5. Yorumlar ve Kodun Anlatımı

Yorumlar (comments), kodun anlaşılmasını kolaylaştırabilir; ancak kötü yazılmış yorumlar kafa karıştırabilir veya gereksiz yere kodu şişirebilir. Temiz kodda amaç, mümkün olan her durumda yorum ihtiyacını ortadan kaldıracak kadar açık ve okunabilir kod yazmaktır.

### Genel Kurallar

- Kod kendi kendini açıklamalıdır, yorum ihtiyacı en aza indirgenmelidir.
- Ne yapıldığını değil, neden yapıldığını açıklayan yorumlar yazılmalıdır.
- Güncel olmayan veya yanıltıcı yorumlardan kaçınılmalıdır.
- Açıklayıcı değişken ve fonksiyon isimleri tercih edilmelidir.

---

### ❌ Kötü Örnek

```python
# kullanıcıyı siler
def delete(u):
    db.delete(u)
```

Buradaki yorum, fonksiyonun ne yaptığını tekrar etmektedir. Bu hem gereksiz hem de düşük kaliteli bir yorumdur.

---

### ✅ İyi Örnek

```python
def delete_user(user):
    db.delete(user)
```

Yoruma gerek kalmadan fonksiyonun amacı açıktır. Fonksiyon adı yeterince açıklayıcıdır.

---

### Yorum Yazılması Gereken Durumlar

- Karmaşık bir algoritmanın *neden* bu şekilde yazıldığını açıklamak.
- Geçici veya bilinçli bir teknik borç (technical debt) alanını belirtmek.
- Belirli sistemsel sınırlamalar veya dış API kısıtlamalarını belgelemek.
- TODO, FIXME, HACK gibi işaretlerle gelecekte yapılması gerekenleri belirtmek.

---

### Yorumlarda Dikkat Edilmesi Gerekenler

- Yorumlar kodla birlikte güncellenmelidir.
- Kodun ne yaptığını anlatmak yerine, geliştiriciye ek bağlam sağlamalıdır.
- Yorumlar profesyonel ve tarafsız bir dil ile yazılmalıdır.

---

### Ekstra Not

Yorumlara bağımlı olmak yerine, okunabilirliği yüksek kod yazmak daha sürdürülebilir bir yaklaşımdır. Yorum, kodun yetersizliğini telafi eden bir araç değil, destekleyici bir açıklamadır.

---
## 6. Exception Handling (Hata Yönetimi)

Hata yönetimi, uygulamanın kararlı ve güvenli çalışması açısından kritik öneme sahiptir. Python'da `try/except` bloklarıyla istisnalar (exceptions) kontrol altına alınabilir. Temiz kod yaklaşımında, sadece beklenen ve yönetilebilir hatalar yakalanmalı, hatalar sessizce yutulmamalıdır.

### Genel Kurallar

- Sadece beklenen ve anlamlı hataları yakalayın.
- Hata mesajları açık ve anlaşılır olmalı.
- `except Exception:` gibi geniş kapsamlı yakalamalardan kaçının.
- Her `try` bloğu yalnızca gerekli kodu kapsamalı.
- Gerekirse özel exception sınıfları oluşturun.

---

### ❌ Kötü Örnek

```python
try:
    user = db.get_user(id)
    user.do_something()
except:
    pass
```

Bu örnekte tüm hatalar yakalanıp hiçbir işlem yapılmıyor. Bu, hata ayıklamayı imkânsız hale getirir ve sistemin sessizce bozulmasına neden olur.

---

### ✅ İyi Örnek

```python
try:
    user = db.get_user(id)
    user.do_something()
except DatabaseError as e:
    logger.error(f"Database error: {e}")
    raise
```

Hata yalnızca belirli bir durumda yakalanır, loglanır ve tekrar fırlatılır. Böylece hem takip edilebilir olur hem de sistem davranışı kontrol altında kalır.

---

### Özel Exception Sınıfı Kullanımı

```python
class InvalidUserInput(Exception):
    pass

def process_input(data):
    if not isinstance(data, dict):
        raise InvalidUserInput("Input must be a dictionary.")
```

Bu yaklaşım, uygulamanın belirli hatalarını ayırmak ve anlamlı hale getirmek için idealdir.

---

### Ekstra Notlar

- Hataları gizlemek, hata yönetimi değildir.
- `finally:` bloğu her durumda çalışır, kaynak temizliği için kullanılabilir.
- Sık kullanılan hatalar için `ValueError`, `TypeError` gibi standart sınıflar tercih edilmelidir.

---
## 7. Kod Biçimlendirme ve Linter Kullanımı

Kodun biçimi, okunabilirliği ve sürdürülebilirliği doğrudan etkiler. Biçimsel tutarsızlıklar zamanla kodun anlaşılmasını zorlaştırır ve ekip içi iş birliğini engeller. Python için PEP8 standardı, kod stilinin nasıl olması gerektiğini tanımlar.

### Genel Kurallar

- Kodunuzu otomatik olarak biçimlendirmek için araçlar kullanın (örneğin `black`).
- Gereksiz boşluklardan ve hizalama hatalarından kaçının.
- Satır uzunluğu genellikle 79–88 karakteri geçmemelidir.
- Değişken, sınıf ve fonksiyon adlarında tutarlı isimlendirme kuralları izlenmelidir.

---

### Önerilen Araçlar

- **Black** → Otomatik kod biçimlendirici.
- **isort** → `import` sıralamalarını düzenler.
- **Flake8** → PEP8 hatalarını kontrol eder.
- **Pylint** → Kod kalitesi, hata analizi ve öneriler sağlar.
- **mypy** → Tip kontrolü yapar (optional typing desteği).

---

### ❌ Kötü Örnek

```python
def getuser( id ):
 return db.get( id )
```

---

### ✅ İyi Örnek

```python
def get_user(id: int) -> User:
    return db.get(id)
```

---

### Linter Kullanımı

```bash
# Flake8 ile kodu kontrol et
flake8 your_file.py

# Black ile otomatik düzeltme yap
black your_file.py

# isort ile import sıralarını düzelt
isort your_file.py
```

---

### Tip Kontrolü (Opsiyonel)

Statik tip kullanımı, büyük projelerde hataları erken yakalamaya yardımcı olur.

```python
def add(a: int, b: int) -> int:
    return a + b
```

mypy ile kontrol etmek:

```bash
mypy your_file.py
```

---

### Ekstra Not

Biçimsel kurallar zamanla değişebilir, ancak proje genelinde tutarlılık en önemli kriterdir. Linter kurallarının CI/CD sürecine dahil edilmesi önerilir.

---
## 8. Kötü Pratikler (Anti-Patterns)

Anti-pattern'ler, kısa vadede işe yarıyor gibi görünen ancak uzun vadede bakımı zorlaştıran, hataya açık ve yanlış yaklaşımlardır. Kod kalitesini düşüren bu alışkanlıklar fark edilip düzeltilmediği sürece projelerde teknik borç birikir.

### Sık Görülen Kötü Pratikler

---

### 🔸 Kod Tekrarı

```python
def create_user(user):
    db.insert(user)
    logger.info("User created")

def create_admin(admin):
    db.insert(admin)
    logger.info("User created")
```

Yerine:

```python
def create_entity(entity):
    db.insert(entity)
    logger.info("Entity created")
```

---

### 🔸 Yersiz Global Değişken Kullanımı

```python
counter = 0

def increment():
    global counter
    counter += 1
```

Yerine sınıf bazlı yaklaşım tercih edilmelidir.

---

### 🔸 Gereksiz Yorumlar

```python
i = 0  # sayaç
```

Yorum yerine daha iyi değişken adı seçilmeli:

```python
counter = 0
```

---

### 🔸 Anlamsız Fonksiyonlar

```python
def do():
    x = 1
    return x
```

Bu tür yapılar gereksizdir ve kod karmaşıklığını artırır.

---

### 🔸 Exception Gizleme

```python
try:
    risky_operation()
except:
    pass
```

Bu yaklaşım hatayı saklar ve ciddi sorunlara neden olabilir.

---

### Genel Tavsiyeler

- Kodda "iş görsün yeter" yaklaşımından kaçının.
- Kod okunabilirliği, kısa yazmaktan daha önemlidir.
- Anlamlı yapılar oluşturmak, koda değer katar.

---

### Ekstra Not

Anti-pattern’ler zamanla alışkanlığa dönüşebilir. Bu nedenle düzenli kod gözden geçirmeleri (code review) yapılmalı, ekip içinde bu pratikler belirlenip belgelenmelidir.

---
## 9. OOP ve Kompozisyon Prensipleri

Nesne yönelimli programlama (OOP), Python projelerinde sık kullanılan bir yaklaşımdır. Ancak OOP kullanımı doğru uygulanmadığında kodu karmaşıklaştırabilir. Bu nedenle sınıf tasarımı, kalıtım (inheritance) ve kompozisyon (composition) gibi kavramların bilinçli şekilde kullanılması önemlidir.

### Temel OOP İlkeleri

- Her sınıf tek bir sorumluluğa sahip olmalıdır (SRP).
- Kalıtım yerine kompozisyon tercih edilmelidir.
- Gereksiz soyutlamalardan kaçınılmalıdır.
- Sınıflar birbiriyle gevşek bağlı (loosely coupled) olmalıdır.

---

### 🔹 Kalıtım (Inheritance) – Ne Zaman?

Kalıtım, bir üst sınıfın işlevselliğini alt sınıflara aktarmak için kullanılır. Ancak her durumda tercih edilmemelidir.

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Bark"
```

Bu yapılar mantıklı soyutlamalar varsa kullanılabilir. Ancak sık güncellenen yapılar için risklidir.

---

### 🔹 Kompozisyon (Composition) – Tercih Edilmesi Gereken Yaklaşım

Kompozisyon, bir sınıfın başka sınıfları özellik olarak barındırmasıdır. Daha esnek ve test edilebilir yapı sağlar.

```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()

    def drive(self):
        self.engine.start()
        print("Driving")
```

---

### ❌ Kötü Örnek – Anlamsız Kalıtım

```python
class Database:
    pass

class MyDatabase(Database):
    pass
```

Burada alt sınıfın özel bir katkısı yoksa, gereksiz kalıtım yapılmış olur.

---

### ✅ İyi Örnek – Kompozisyon Kullanımı

```python
class Logger:
    def log(self, message):
        print(message)

class Service:
    def __init__(self, logger: Logger):
        self.logger = logger

    def run(self):
        self.logger.log("Service running")
```

---

### Ekstra Not

Python’da `@dataclass`, `abc` (abstract base class) gibi yapılar da OOP projelerinde kodu sadeleştirmek için kullanılabilir. Ancak her yapı, amacına uygun ve gerekliyse tercih edilmelidir.

---
## 10. Pythonic Kod Yazımı

Pythonic kod, dilin sunduğu özellikleri ve felsefesini en verimli, okunabilir ve sade biçimde kullanan koddur. Bu tarz kod yazımı, hem Python’a özgü söz dizimini hem de topluluk tarafından benimsenmiş en iyi uygulamaları içerir.

### Temel Özellikler

- Sadelik, açık ifade ve okunabilirlik ön plandadır.
- Yerleşik fonksiyonlar ve dil yapıları tercih edilir.
- Gereksiz tekrar, karmaşık yapılar ve "Java tarzı" sınıf kullanımlarından kaçınılır.
- List comprehension, unpacking, context manager gibi yapılar aktif olarak kullanılır.

---

### ❌ Kötü Örnek – Python dışı düşünce tarzı

```python
numbers = [1, 2, 3, 4, 5]
squares = []
for n in numbers:
    squares.append(n * n)
```

---

### ✅ İyi Örnek – Pythonic yaklaşım

```python
squares = [n * n for n in [1, 2, 3, 4, 5]]
```

---

### Kullanılabilecek Pythonic Yapılar

- **List Comprehension**
- **Enumerate & Zip**
- **Unpacking (tuple/list)**
- **Context Manager (`with` kullanımı)**
- **Ternary Operator**
- **Walrus Operator (`:=`)**
- **F-string ile formatlama**
- **Any / All kullanımı**

---

### Örnekler

#### `enumerate`

```python
for index, item in enumerate(items):
    print(index, item)
```

#### `zip`

```python
for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

#### `with`

```python
with open("file.txt") as f:
    data = f.read()
```

#### `f-string`

```python
name = "John"
print(f"Hello, {name}!")
```

---

### Ekstra Not

Pythonic düşünce tarzı sadece sözdizimi ile ilgili değildir. Aynı zamanda “işi en anlaşılır ve sade şekilde yapma” zihniyetini de içerir. Bu bakış açısı, temiz kodun doğal bir parçasıdır.

---

## 11. Sihirli Sayılardan (Magic Numbers) Kaçının

Sihirli sayılar (magic numbers), kod içerisinde doğrudan kullanılan, anlamı belirsiz sabit sayılardır. Bu tür değerler, kodun okunabilirliğini ve sürdürülebilirliğini zorlaştırır.

Kodda geçen bir sayının neyi temsil ettiğini anlamak için ek bağlam gerekmesi, kodu okuyan geliştiriciler için zaman kaybına ve hata riskine yol açar.

### ❌ Kötü Örnek:

```python
def calculate_discount(price):
    return price * 0.9  # Bu oran neye göre belirlendi?
```

### ✅ İyi Örnek:

```python
DISCOUNT_RATE = 0.9

def calculate_discount(price):
    return price * DISCOUNT_RATE
```
0.9 değeri burada %10'luk bir indirim oranını temsil eder; ancak bu doğrudan yazıldığında anlamı belirsiz kalır — sabit bir değişkene atanarak oran hem açıklanmış hem de yönetilebilir hale getirilmiş olur.

---

🔖 **İpucu:** Sabitleri büyük harflerle ve `snake_case` formatında adlandırmak, Python topluluk standartlarıyla uyumludur.

---

## 12. Modülerlik ve Sınıf Yapıları (Modularity and Classes)

Kodun yalnızca çalışması yeterli değildir; aynı zamanda sürdürülebilir, anlaşılabilir ve genişletilebilir olması gerekir. Bu hedeflere ulaşmanın yolu, projeyi anlamlı parçalara bölmekten geçer. Modülerlik ve sınıf temelli tasarım, bu bağlamda temiz kodun temel yapı taşlarındandır.

### 🧱 Modüler Tasarım Neden Önemlidir?

- Her modül, belirli bir sorumluluğa sahip olmalıdır.
- Kod bölümleri birbirinden mümkün olduğunca bağımsız olmalıdır.
- Modüller, yeniden kullanılabilir olacak şekilde tasarlanmalıdır.

Python'da modülerliği sağlamak için:
- Fonksiyonlar belirli görevlerle sınırlandırılmalı,
- İlgili fonksiyonlar sınıflar altında gruplanmalı,
- Bu sınıflar, işlevsel gruplara göre farklı dosyalara dağıtılmalıdır.

### 📁 Uygulamalı Yapı Örneği

Gerçek dünyada modüler mimariye örnek olarak Django’nun varsayılan proje yapısı verilebilir:

```
myproject/
├── auth/
│   ├── views.py
│   ├── models.py
│   └── urls.py
├── shop/
│   ├── views.py
│   ├── models.py
│   └── urls.py
└── config/
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

Bu yapıda her "app" kendi iş alanını temsil eder. Bu sayede birimlerin bağımsız olarak gelişmesi ve test edilmesi kolaylaşır.

---

### 🧠 Sınıflar ve Nesne Yönelimli Temizlik

Sınıflar, kodu hem mantıksal hem yapısal olarak gruplamanın etkili bir yoludur. Ancak yalnızca "class" yazmak yeterli değildir. Temiz kod için sınıflar şu ilkeleri gözetmelidir:

- **Single Responsibility (Tek Sorumluluk):** Her sınıf yalnızca tek bir iş yapmalı.
- **Açık Arayüz:** Sınıf dışına açık olan metotlar net ve gerekli olanla sınırlı olmalı.
- **Uygulanabilirlik:** Gereksiz miras veya soyutlamalardan kaçınılmalı.

#### Python Örneği:

```python
class Invoice:
    def __init__(self, amount: float):
        self.amount = amount

    def calculate_tax(self):
        return self.amount * 0.18

class InvoicePrinter:
    def print_invoice(self, invoice: Invoice):
        print(f"Total with tax: {invoice.amount + invoice.calculate_tax()}")
```

Burada `Invoice` sınıfı sadece veriyi ve işlemi taşır, çıktı ise ayrı bir sınıfa aittir. Bu, sorumlulukların ayrılması anlamında temiz kodun idealidir.

---

🔎 **Not:** Kod modülerleştikçe test edilebilirlik artar. Her sınıf ve modül, tek başına çalışabilir olmalıdır.

---

### Ek Kaynaklar

- [Clean Code by Robert C. Martin](https://www.oreilly.com/library/view/clean-code/9780136083238/)
- [PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/)
- [Refactoring Guru](https://refactoring.guru)
