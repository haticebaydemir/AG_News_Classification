# AG_News_Classification
Projenin kodlarına [buraya tıklayarak](https://colab.research.google.com/drive/1HBkst5ELRJN93jEJ9AQ8s7L4WODyXshB) ulaşabilirsiniz.

# AG News Sınıflandırma Projesi
## Proje Tanımı
Bu proje, AG News veri setini kullanarak haber metinlerini dört ana kategoriye (Dünya, Spor, İş Dünyası, Bilim/Teknoloji) sınıflandırmayı amaçlamaktadır. Doğal dil işleme (NLP) alanında güncel yöntemler ve derin öğrenme teknikleri kullanılarak, kullanıcıların ilgi alanlarına göre içerikleri daha hızlı bir şekilde erişebilmesi sağlanmaktadır.
## Hedef
Projenin amacı, haber içeriklerinin otomatik olarak sınıflandırılmasıdır. Bu, kullanıcı deneyimini iyileştirmek ve içerik öneri sistemleri için veri sağlamaktadır.
## Kullanılan Kütüphaneler
Projenin gerçekleştirilmesinde aşağıdaki kütüphaneler kullanılmıştır:

- **Transformers**: Hugging Face tarafından sağlanan, doğal dil işleme görevleri için önceden eğitilmiş modeller sunan bir kütüphane.
- **Torch**: PyTorch, derin öğrenme uygulamaları için yaygın olarak kullanılan bir framework.
- **Datasets**: Hugging Face’in veri setlerini yüklemek ve yönetmek için kullandığı bir kütüphane.

## Veri Seti
Proje, AG News veri setini kullanmaktadır. Bu veri seti, haber metinlerini ve etiketlerini içermektedir. İlk 1000 örnek alınarak analiz ve model eğitimi gerçekleştirilmiştir.

## Tokenizasyon ve Model Eğitimi
Metin verileri, modelin anlayacağı forma dönüştürülmek üzere tokenizasyon işlemi yapılmıştır. Daha sonra, DistilBERT modeline dayalı bir sınıflandırma modeli eğitilmiştir. Eğitim sürecinde çeşitli parametreler belirlenmiş ve modelin performansı artırılmıştır.

## Model Değerlendirme
Eğitim tamamlandıktan sonra modelin başarımı, doğruluk oranı gibi metriklerle değerlendirilmiştir. Bu aşama, modelin gerçek dünya verileri üzerindeki etkinliğini ölçmeyi amaçlamaktadır.

## Tahmin Yapma
Eğitilmiş model kullanılarak yeni metinler üzerinde tahminler yapılmaktadır. Örnek metinler kullanılarak, modelin sınıflandırma yeteneği test edilmiştir.

## Sonuç
Bu proje, doğal dil işleme ve makine öğrenimi uygulamalarının nasıl entegre edilebileceğine dair önemli bir örnek teşkil etmektedir. AG News veri seti üzerinde yapılan bu çalışma, içerik öneri sistemleri ve kullanıcı deneyimini geliştirme konusunda önemli bir kaynak sunmaktadır.


# İletişim
Sorularınız veya önerileriniz için aşağıdaki iletişim bilgilerini kullanabilirsiniz:

E-posta: baydemirhatice@hotmail.com

Linkedln: https://www.linkedin.com/in/haticebaydemir/

