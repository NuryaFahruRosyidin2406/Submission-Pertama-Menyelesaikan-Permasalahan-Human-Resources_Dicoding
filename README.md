# Proyek Akhir: Menyelesaikan Permasalahan Perusahaan Edutech

## Business Understanding

Jaya Jaya Maju merupakan salah satu perusahaan multinasional yang telah berdiri sejak tahun 2000 dan telah berkembang pesat hingga memiliki lebih dari 1000 karyawan di seluruh penjuru negeri. Namun, seiring bertambah besarnya skala organisasi, perusahaan tersebut menghadapi tantangan besar dalam manajemen sumber daya manusia (HR). Perusahaan mengalami tingginya attrition rate (rasio jumlah karyawan yang keluar dengan total karyawan keseluruhan) yang menembus angka diatas 10%. Untuk mencegah hal ini semakin parah, manajer departemen HR meminta bantuan dalam mengidentifikasi berbagai faktor yang mempengaruhi tingginya attrition rate tersebut dan menyusun strategi retensi yang efektif.

### Permasalahan Bisnis

Berdasarkan latar belakang di atas, berikut adalah permasalahan bisnis utama yang terkait apa saja faktor utama yang membuat karyawan keluar dari perusahaan (attrition), dan bagaimana profil karyawan yang paling rentan untuk keluar agar HR bisa menyusun strategi pencegahan yang tepat?

### Cakupan Proyek

Untuk menjawab permasalahan bisnis tersebut, proyek ini berfokus pada analisis data karyawan dan pembuatan business dashboard guna memonitori faktor-faktor yang memengaruhi tingkat keluar-masuk karyawan (attrition) di perusahaan.
Berikut ini ada beberapa pertanyaan utama yang akan dicari jawabannya dalam proyek ini:

1.    Berapa total tingkat attrition karyawan saat ini di perusahaan?
2.    Apakah beban kerja dan lembur (OverTime) menjadi pemicu utama karyawan keluar?
3.    Bagaimana pengaruh finansial (seperti gaji dan tingkat kenaikan gaji) terhadap attrition?
4.    Bagaimana hubungan antara tingkat kepuasan kerja dan work-life balance dengan keputusan karyawan untuk resign?
5.    Departemen, posisi kerja, atau kelompok demografi mana yang memiliki risiko attrition paling tinggi?

### Persiapan

**Sumber data:** Dataset internal karyawan Jaya Jaya Maju ('employee_data.csv') yang mencakup variabel demografi, kepuasan kerja, kompensasi, jam kerja, dan status attrition.

**Setup environment:**

1. **Upload Dataset dari Google Colab ke Supabase (PostgreSQL)**

   ```
   # 1. Instalasi library yang dibutuhkan
   !pip install pandas sqlalchemy

   # 2. Import library
   import pandas as pd
   from sqlalchemy import create_engine
   from getpass import getpass

   # 3. Membaca dataset dari penyimpanan GitHub
   df = pd.read_csv(
    "https://raw.githubusercontent.com/NuryaFahruRosyidin2406/Submission-Pertama-Menyelesaikan-Permasalahan-Human-Resources_Dicoding/refs/heads/main/Dataset/employee_data.csv",
    encoding='windows-1252'
   )

   # 4. Koneksi ke Database Supabase menggunakan URI Connection PostgreSQL
   password = getpass("Masukkan Password Supabase: ")
   # Format URI: postgresql://[user]:[password]@[host]:[port]/[dbname]
   URL = f"postgresql://postgres.lhdwpwanyxgcdphjwzji:{password}@aws-0-ap-northeast-1.pooler.supabase.com:6543/postgres"
   engine = create_engine(URL)

   # 5. Mengirimkan dataset ke tabel di Supabase
   df.to_sql('employee_data', engine)

   # Data berhasil diunggah ke Supabase
   ```

2. **Pengecekan dataset kembali di Supabase dan tambahkan query untuk clean dataset yang perlu ditambahkan**

   Query
   ```
   UPDATE employee_data
   SET "Attrition" = 0
   WHERE "Attrition" IS NULL
   ```  

3. **Menjalankan Metabase Menggunakan Docker (Local Machine)**

   Command Prompt
   ```
   docker run -p 3000:3000 --name metabase metabase/metabase
   ```

   Jika nama container sudah ada, maka jalankan kembali container Metabase

   Command Prompt
   ```
   docker start metabase
   ```
   
4. **Koneksi dan Analisis Data di Metabase Dapat Diakses Melalui Browser di http://localhost:3000/setup**

## Business Dashboard

Dashboard HR Analytics ini dikembangkan menggunakan **Metabase** untuk memantau tingkat *attrition* (karyawan keluar) dan mengidentifikasi faktor-faktor risiko utama di dalam perusahaan. Desain visual menggunakan pendekatan *dark theme* dengan skema warna bergradasi (biru untuk metrik netral dan merah untuk metrik risiko) agar *data storytelling* tersampaikan dengan jelas.

Dashboard ini terbagi menjadi empat area analisis utama, yaitu:
1. **Metrik Utama Attrition:** Ini menampilkan KPI fundamental perusahaan yang meliputi Total Employees, Total Attrition, dan Attrition Rate (&).
2. **Analisis Beban Kerja & Risiko Jabatan:** Ini menguraikan korelasi antara status lembur (*OverTime*) dengan *attrition*, serta rincian distribusi *attrition* berdasarkan departemen dan posisi/jabatan (*Job Role*).
3. **Analisis Pengaruh Finansial & Kompensasi:** Ini mengidentifikasi hubungan antara rata-rata pendapatan bulanan (*Average Monthly Income*) per departemen serta persentase kenaikan gaji (*Percent Salary Hike*) terhadap keputusan karyawan untuk keluar.
4. **Kepuasan Kerja, Work-Life Balance, & Demografi Karyawan:** Ini menganalisis dampak tingkat kepuasan kerja (*Job Satisfaction*) yang dikombinasikan dengan *Work-Life Balance*, serta sebaran *attrition* berdasarkan kelompok usia (*Age Group*).

**Link Dashboard:** [Masukkan Link Dashboard Metabase Kamu Di Sini]

## Conclusion

Proyek **HR Analytics** ini bertujuan untuk mengidentifikasi faktor-faktor utama yang mendorong tingkat keluar-masuk karyawan (*attrition*) di perusahaan serta memberikan landasan berbasis data (*data-driven*) bagi pihak HR dalam mengambil langkah preventif. Berdasarkan pengolahan dan visualisasi data yang telah dilakukan pada seluruh metrik utama, dapat ditarik beberapa kesimpulan penting, seperti:

1. **Tingkat Attrition Berada di Tingkat Kritis:**
   Dari total **1.470 karyawan**, sebanyak **179 karyawan** yang telah meninggalkan perusahaan. Hal ini menghasilkan *attrition rate* sebesar **12,5%**. Angka ini mengindikasikan adanya isu retensi yang perlu segera ditangani.

2. **Faktor Beban Kerja & Lembur (OverTime):**
   Dari total 416 karyawan yang melakukan kerja lembur (*OverTime = Yes*), sebanyak 98 karyawan mengalami *attrition*. Angka ini jauh lebih tinggi dibandingkan kelompok karyawan yang tidak lembur. Hal ini mengindikasikan bahwa beban kerja berlebih berkontribusi langsung pada tingkat kepuasan dan retensi karyawan.

3. **Konsentrasi Risiko pada Departemen & Jabatan Spesifik:**
   Tingkat *attrition* terkonsentrasi pada dua departemen utama, yaitu **Research & Development** (107 karyawan) dan **Sales** (66 karyawan). Posisi teknis dan lapangan seperti *Research Scientist*, *Laboratory Technician*, serta *Sales Executive* merupakan peran dengan tingkat kehilangan talenta paling signifikan.

4. **Kompensasi & Insentif Finansial:**
   Analisis terhadap persentase kenaikan gaji (*Percent Salary Hike*) menunjukkan bahwa karyawan yang menerima kenaikan gaji berkala di rentang **12%–16%** menyumbang angka *attrition* terbesar. Sebaliknya, ketika kenaikan gaji berada di atas **20%**, tingkat *attrition* turun drastis. Hal ini menandakan bahwa struktur kompensasi saat ini belum cukup kompetitif untuk menahan talenta terbaik.

5. **Rentannya Talenta Usia Produktif:**
   Berdasarkan demografi usia, akumulasi *attrition* terbesar berasal dari kelompok usia muda, yaitu **< 30 tahun (39,11%)** dan **30–40 tahun (38,55%)**. Secara total, lebih dari **77%** karyawan yang keluar berada di bawah usia 40 tahun. Ini menunjukkan tantangan besar bagi perusahaan dalam menjaga *engagement* dan memberikan jenjang karir yang jelas bagi talenta usia produktif.

Secara keseluruhan, *attrition* di perusahaan ini didorong oleh kombinasi **beban kerja yang tinggi (lembur), penyesuaian gaji berkala yang kurang memuaskan pada rentang menengah, serta ketidakseimbangan kehidupan kerja pada talenta usia muda**.

### Rekomendasi Action Items (Optional)

Berdasarkan hasil analisis dan temuan pada dashboard, berikut beberapa langkah strategis yang dapat direkomendasikan bagi perusahaan untuk menekan angka *attrition*, seperti: 

- **Evaluasi & Penyesuaian Kebijakan Gaji (Salary Hike Strategy):**
  Tinjau ulang standar kenaikan gaji berkala, terutama bagi karyawan berkinerja tinggi.
- **Pengendalian Jam Lembur & Audit Beban Kerja:**
  Terapkan batas maksimal jam lembur mingguan serta lakukan audit pembagian beban kerja, khususnya di departemen **Research & Development** dan **Sales**. Dan juga bisa berikan insentif lembur yang lebih adil atau opsi *flexible working hours* untuk menjaga *Work-Life Balance*.
- **Program Retensi & Pengembangan Karir Usia Muda:**
  Mengingat lebih dari 77% *attrition* didominasi oleh karyawan berusia di bawah 40 tahun, perusahaan perlu menyusun *clear career pathing*, program *mentorship*, serta skema apresiasi performa rutin untuk dapat meningkatkan *employee engagement* dan rasa kepemilikan oleh para karyawan.

## Employee Data

The data contains demographic details, work-related metrics and attrition flag.

* **EmployeeId** - Employee Identifier
* **Attrition** - Did the employee attrition? (0=no, 1=yes)
* **Age** - Age of the employee
* **BusinessTravel** - Travel commitments for the job
* **DailyRate** - Daily salary
* **Department** - Employee Department
* **DistanceFromHome** - Distance from work to home (in km)
* **Education** - 1-Below College, 2-College, 3-Bachelor, 4-Master,5-Doctor
* **EducationField** - Field of Education
* **EnvironmentSatisfaction** - 1-Low, 2-Medium, 3-High, 4-Very High
* **Gender** - Employee's gender
* **HourlyRate** - Hourly salary
* **JobInvolvement** - 1-Low, 2-Medium, 3-High, 4-Very High
* **JobLevel** - Level of job (1 to 5)
* **JobRole** - Job Roles
* **JobSatisfaction** - 1-Low, 2-Medium, 3-High, 4-Very High
* **MaritalStatus** - Marital Status
* **MonthlyIncome** - Monthly salary
* **MonthlyRate** - Mounthly rate
* **NumCompaniesWorked** - Number of companies worked at
* **Over18** - Over 18 years of age?
* **OverTime** - Overtime?
* **PercentSalaryHike** - The percentage increase in salary last year
* **PerformanceRating** - 1-Low, 2-Good, 3-Excellent, 4-Outstanding
* **RelationshipSatisfaction** - 1-Low, 2-Medium, 3-High, 4-Very High
* **StandardHours** - Standard Hours
* **StockOptionLevel** - Stock Option Level
* **TotalWorkingYears** - Total years worked
* **TrainingTimesLastYear** - Number of training attended last year
* **WorkLifeBalance** - 1-Low, 2-Good, 3-Excellent, 4-Outstanding
* **YearsAtCompany** - Years at Company
* **YearsInCurrentRole** - Years in the current role
* **YearsSinceLastPromotion** - Years since the last promotion
* **YearsWithCurrManager** - Years with the current manager

## Acknowledgements
https://www.ibm.com/communities/analytics/watson-analytics-blog/watson-analytics-use-case-for-hr-retaining-valuable-employees/
