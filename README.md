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

   ```python
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
   print("Data berhasil diunggah ke Supabase")
   ```
   
2. **Menjalankan Metabase Menggunakan Docker (Local Machine)**

   ```Bash
   docker run -d -p 3000:3000 --name metabase metabase/metabase
   ```
   
3. **Koneksi dan Analisis Data di Metabase Dapat Diakses Melalui Browser di http://localhost:3000**

## Business Dashboard

Jelaskan tentang business dashboard yang telah dibuat. Jika ada, sertakan juga link untuk mengakses dashboard tersebut.

## Conclusion

Jelaskan konklusi dari proyek yang dikerjakan.

### Rekomendasi Action Items (Optional)

Berikan beberapa rekomendasi action items yang harus dilakukan perusahaan guna menyelesaikan permasalahan atau mencapai target mereka.

- action item 1
- action item 2

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
