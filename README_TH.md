# DATA-SCI-PRACTICE

ไทม์แคปซูลเก็บผลงานฝึกทำ Data Science ชิ้นแรก สำหรับทำนายการติดสมาร์ตโฟนด้วยอัลกอริทึม K-Nearest Neighbors (คงโค้ดใน `FirstOFMany.ipynb` และข้อมูล `Smartphone.csv` ไว้ตามเดิม)

[English](README.md) | [ชุดข้อมูลบน Kaggle](https://www.kaggle.com/datasets/jayjoshi37/smartphone-usage-and-addiction-prediction)

## สิ่งที่ต้องใช้

โน้ตบุ๊กใช้ Python 3 ร่วมกับ `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn` และ `mlxtend`

## การติดตั้ง

สร้าง virtual environment แล้วติดตั้งแพ็กเกจตามที่ `FirstOFMany.ipynb` เรียกใช้:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install pandas numpy matplotlib seaborn scikit-learn mlxtend jupyter
```

## การรันโน้ตบุ๊ก

เปิด Jupyter จากโฟลเดอร์หลักของโปรเจกต์ เพื่อให้ `FirstOFMany.ipynb` อ่านไฟล์ `Smartphone.csv` ได้ตรงตำแหน่ง:

```bash
jupyter notebook FirstOFMany.ipynb
```

## ขั้นตอนการทำงานของโค้ด

1. อ่านไฟล์ `Smartphone.csv` (7,500 แถว, 16 คอลัมน์) และตรวจสัดส่วน `addicted_label` (ติด 5,308 แถว, ไม่ติด 2,192 แถว)
2. เติมค่าว่างด้วย `0`, แปลงค่าข้อความใน `gender`, `stress_level`, `academic_work_impact` และ `addiction_level` เป็นตัวเลข แล้วตัด `transaction_id` กับ `user_id` ออก
3. สุ่มตัวอย่างฝั่งละ 2,000 แถว (`random_state=42`) รวมเป็นชุดข้อมูลสมดุล 4,000 แถว
4. ตัด `addicted_label` และ `addiction_level` (ซึ่งมีค่าสหสัมพันธ์กับเป้าหมายสูงถึง `0.9017`) ออก เหลือตัวแปรต้น 12 ตัว จากนั้นปรับสเกลด้วย `MinMaxScaler`
5. แบ่งข้อมูล Train 80% / Test 20% (`test_size=0.2`, `random_state=42`), เทรน `KNeighborsClassifier(n_neighbors=41)` และวนทดสอบค่า `k` ตั้งแต่ 1 ถึง 110 เพื่อดูกราฟ Error Rate

## ผลลัพธ์

ที่ค่า `k=41` โมเดลได้ค่า Accuracy `0.8662` บนชุดทดสอบ 800 แถว

| ผลลัพธ์ | คำอธิบาย |
|---|---|
| [กราฟจำนวนตามเพศ](docs/images/01_gender_count.png) | การกระจายตัวของ `gender` จากข้อมูลทั้งหมด 7,500 แถว |
| [ตารางสหสัมพันธ์](docs/images/02_correlation_heatmap.png) | ค่าสหสัมพันธ์ระหว่างคอลัมน์ตัวเลขทั้งหมด |
| [Confusion Matrix](docs/images/03_confusion_matrix_knn41.png) | ผลการทำนายบนชุดทดสอบของ `KNeighborsClassifier(n_neighbors=41)` |
| [กราฟ Error Rate ตามค่า K](docs/images/04_error_rate_vs_k.png) | อัตราความคลาดเคลื่อนบนชุดทดสอบสำหรับ `k=1..110` |

## โครงสร้างไฟล์

- `FirstOFMany.ipynb` โน้ตบุ๊กต้นฉบับที่เก็บไว้โดยไม่แก้ไข
- `Smartphone.csv` ชุดข้อมูลจำนวน 7,500 แถว
- `docs/images/` รูปกราฟที่ได้จากการรัน `FirstOFMany.ipynb`
- `README.md` และ `README_TH.md` เอกสารอธิบายโปรเจกต์ภาษาอังกฤษและภาษาไทย
