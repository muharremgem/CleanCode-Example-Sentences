# CleanCode-Example-Sentences

Burada CleanCode çalışması yapılacaktır.

- CleanCode örnek cümleleri burada toplayacagım.





Kodlama Kuralları
Önce neyin temiz kod olmadığını sorarak başlayalım. Örneklerimiz JavaScript’i temel alarak hazırlanacaktır.

Peki, sizin ve ekibinizin işini kolaylaştırmak için yapmaya başlayabileceğiniz bazı şeyler nelerdir? Basit adlandırma kurallarıyla başlayalım.

Tüm JavaScript projeleriniz için her zaman aynı kodlama kurallarını kullanın.

Gizemli sayılar
Açık bir anlamı olmayan bir sayı atamak. Bu koda ilk kez bakarsanız, 86400 sayısının neyi temsil etmesi gerektiği konusunda hiçbir fikriniz olmaz.

for(let i = 0; i < 86400; i += 1) {
    // ...
  }
Bunu adlandırılmış bir sabitle değiştirmek daha iyidir:

const SECOND_IN_A_DAY = 86400;

for(let i = 0; i < SECOND_IN_A_DAY; i += 1) {
  // ...
}
Makalenin ilerleyen kısımlarında bu örnek için neden upper case snake case kullandığımızı da öğreneceksiniz.

Deep Nesting
Kodunuz çok sayıda iç içe geçmiş döngü veya koşullu ifade içeriyorsa, bu muhtemelen ayrı bir fonksiyona çıkarılmalıdır.

const exampleArray = [ [ [ 'value' ] ] ];

exampleArray.forEach((arr1) => {
  arr1.forEach((arr2) => {
    arr2.forEach((el) => {
      console.log(el)
    })
  })
})

// output: 'value'
Bu özel örnek için, tüm dizilerde döngü oluşturacak ve son bir değer döndürecek bir fonksiyon oluşturabiliriz:

const exampleArray = [ [ [ 'value' ] ] ];

const retrieveFinalValue = (element) => {
  if(Array.isArray(element)) {
    return fetchValue(element[0]);
  }

  return element;
}

// output: 'value'
Yorum yazmayı bırak
Öznel olmasına rağmen, kodunuzda yorumların kullanılması yardımcı olabilir. Ancak bu, kodunuzun kendi kendini açıklayıcı olmadığının bir işareti de olabilir.

Yorumlar doğası gereği iyi ya da kötü olmasa da, sıklıkla koltuk değneği olarak kullanılırlar. Kodunuzu her zaman yorumlar yokmuş gibi yazmalısınız. Bu, kodunuzu en basit, en yalın, en kendi kendini belgeleyen şekilde yazmaya zorlar.

Büyük Foknsiyonlardan kaçının
Boyut olarak büyük bir fonksiyon veya hatta bir sınıf, olması gerekenden fazlasını yaptığını gösterir. Bu örnek basit görünebilir ancak bir noktayı kanıtlıyor. Bu fonksiyon olması gerekenden çok daha fazlasını yapar.

const addMultiplySubtract = (a, b, c) => {
    const addition = a + b + c;
    const multiplication = a * b * c;
    const subtraction = a - b - c;
  
    return `${addition} ${multiplication} ${subtraction}`;
  }  
Mantığı ayırmak için farklı fonksiyonlar oluşturmak daha iyidir:

const add = (a, b, c) => a + b + c;
const multiply = (a, b, c) => a * b * c;
const subtract = (a, b, c) => a - b - c;
Kod tekrarı
Bir kod bloğunu kopyalayıp yapıştırmanız gerekiyorsa bu, tekrarlanan bloğun kendi fonksiyonuna çıkarılması gerekebileceğinin bir işaretidir.

Bunun en güzel örneği deep nesting örneğidir:

const exampleArray = [ [ [ 'value' ] ] ];

exampleArray.forEach((arr1) => {
  arr1.forEach((arr2) => {
    arr2.forEach((el) => {
      console.log(el)
    })
  })
})
Burada çok sayıda tekrarlanan kodumuz var. Onu farklı bir fonksiyona ayırmak ve mantığı daha az tekrarla farklı şekilde ele almak çok daha iyidir:

const exampleArray = [ [ [ 'value' ] ] ];

const retrieveFinalValue = (element) => {
  if(Array.isArray(element)) {
    return fetchValue(element[0]);
  }

  return element;
}
Kod tekrarının bir başka örneği de parametrelerden veri almaktır:

const getUserCredentials = (user) => {
    const name = user.name;
    const surname = user.surname;
    const password = user.password;
  }
ES6 nesne ayrıştırmayı kullanarak aşağıdakileri basitçe yapabiliriz:

const getUserCredentials = (user) => {
    const { name, surname, password } = user;
  }
Değişken İsimleri
JavaScript’teki hemen her şey için camel case kullanılır. Camel case tanımlayıcı isimleri (değişkenler ve fonksiyonlar) için kullandığımız bir adlandırma standardıdır.

Bir adın küçük harfle başlaması gerektiğini ve ardından bir sonraki kelimenin her ilk harfinin büyük harf olduğunu belirtir. İşte bazı örnekler:

thisIsARandomCamelCaseName, camelCase, exampleFunctionName

Anlamlı isimler kullanın
getUserData ve getUserInfo belirsizdir. Hangi verileri veya bilgileri alıyorsunuz?

İşlevlerimizin, yöntemlerimizin ve değişken adlarımızın tam anlamlarını ifade etmesi önemlidir.

getUserPost çok daha iyi; tam olarak ne elde ettiğimizi anlayabiliriz.

Şüphe duyduğunuzda tanımlayıcı isimlendirmeyi tercih edin
Mümkün olduğunca kısa ve öz olun, ancak isminiz için iki veya üç kelimelik bir açıklama bulmakta güçlük çekiyorsanız, açıklayıcı olma tarafında kalmak daha iyidir.

findUserByNameOrEmail ve setUserLoggedInTrue findUser  ‘dan daha iyidir.

Daha kısa bir versiyon olduğunda onu kullanın
getUserFromDatabase çok açıklayıcı olsa da, aynı anlama gelen daha kısa bir versiyonu var. Kendinize sormanız gereken en önemli soru “fromDatabase programınıza herhangi bir anlam katıyor mu?”

Cevap, büyük olasılıkla olmamasıdır. Kullanıcıyı veri tabanından getirdiğimizi varsayabiliriz.

Her kavram için tutarlı fiiller kullanın
Fonksiyonlar genellikle bir şeyler oluşturur, okur, günceller veya siler. Hatta biraz daha açıklayıcı olabilir ve bunları yazabilirsiniz: get, set, add, remove, reset, delete.

Bir fonksiyon, bir fiil veya fiil cümlesi olmalı ve amacını iletmelidir.

Fiillerimizle tutarlı olmalıyız. Almak için her zaman get, retrieve, return ve on bin farklı isim yerine sadece get kullanabiliriz:

getQuestions getUserPosts getUsers ‘dan ziyade:

getQuestions returnUsers retrieveUsers.

Açıkçası bu kelimelerin farklı varyasyonları vardır, ancak hangisini seçerseniz seçin, tutarlı kalın. Örneğin bir şeyi sildiğinizde tüm programınız boyunca “delete” veya “remove” kullanın (ikisini birden değil).

if-then ifadelerinde iyi okunan boolean ‘ler yapın
Boolean değişken adları için iyi bir test; vereceğiniz ismi bir if-then ifadesine koymak ve yüksek sesle okumaktır. Doğal bir cümle gibi okunuyorsa bu daha iyi bir durumdur.

Örneğin, bir arabanın özelliklerini kontrol ediyorsak hangi isimlendirmeyi daha uygun bulursunuz?

sedan, sold, green, airbag, veya;

isSedan, isSold, isGreen, hasAirbag.

Ve şimdi property’leri kontrol ediyorsak şöyle bir şey yapabiliriz:

car.isSedan, car.isSold, car.hasAirbag (car.airbags’ den  çok daha iyi) ve boolean değerleriyle karşı karşıya olduğumuzu hemen anlıyoruz.

Bunlar kulağa daha doğal geliyor ve programın anlaşılmasını kolaylaştırıyor.

Sınıflar için isimler kullanın
Sınıflar bir şeyleri almaz, bunlar nesnedir.

Daha spesifik olarak, bir şeyin planıdırlar. Bir sınıfı örneklemek, bir şeyi yapan şeydir.

class Car = {…} class MakeCar {…} değil.

Yeni bir araba yapacak olsaydın “yeni bir yeni araba yap” demezdin, “yeni bir araba yap” derdin.

Sınıf isimlendirmeleri için PascalCase kullanın
Pascal case hangi öğelerin sınıf olduğunu ve hangilerinin olmadığını görmeyi kolaylaştırır.

class task {…} yerine class Task {…}.

Sabit değerleri büyük harfle yaz
Bir günde saniyeleri belirttiğimizi hatırlıyor musunuz? (SECOND_IN_A_DAY = 86400)

Sabit bir değer değişmeyecek bir şeydir. Bu kuralın C dilinde kökleri vardır ve her zaman JavaScript’te görülmez.

Const bildirimi değerin yeniden atama yoluyla değiştirilemeyeceği anlamına gelir.

Örneğin:

const HOURS_IN_DAY = 24;   const TODAY = new Date (); gibi.

Tek harfli değişken adlarından kaçının
Kısaltılmış adlar uzun vadede kaydettiğiniz tuş vuruşlarından daha fazla güçlük çıkarır.

İsimler kısa ve açıklayıcı olmalıdır. Genel kapsamda (Global scope) başlatılan bir değişken yüz satır sonra kullanıma girebilir. Yalnızca tek bir harf olursa ne olduğunu unutmak kolaylaşır.

const dueDate = new Date() şundan çok daha iyi const d = new Date();

const query = () => { … }; şundan çok daha iyi q = () => { … };

Tek harfli değişken adları kullanıyorsanız, bunları küçük fonksiyonlarla veya döngülerde dizin değişkenleri olarak sınırlayın (bu sorun değil):

for(let i = 0; i < 10>; i ++) { // ... }
Gelecekteki akıl sağlığınız için bu kuralları hatırlayın.

Özetlemek gerekirse, uzun vadede bu kurallara uymanın çok büyük faydaları var. Diğerleri yazdığınız kodu kısa bir süre içerisinde, yukarıdan aşağıya tarayabilir ve rahat bir nefes alabilir veya hayal kırıklığı yaşayabilir. Hangisini tercih edersiniz?

Temiz kod, kodlamaya başlamayı ve devam etmeyi kolaylaştırır; hem birey hem de ekip için daha iyidir ve okunması çok daha kolaydır.

Temiz bir kodun özellikleri:

“Zarif olmalı – Temiz kod okumak “hoş” olmalıdır. Okumak, sizi iyi hazırlanmış bir müzik kutusu veya iyi tasarlanmış bir arabanın yapacağı gibi gülümsetmelidir.”
“Temiz kod odaklıdır —Her fonksiyon, her sınıf, her modül, çevredeki ayrıntılar tarafından tamamen bozulmadan ve kirletilmeden kalan tek fikirli bir tutum sergiler.”
“Temiz kodla ilgilenildi. Birileri onu basit ve düzenli tutmak için zaman ayırdı. Ayrıntılara gereken önemi verdiler. Önemsediler.”


