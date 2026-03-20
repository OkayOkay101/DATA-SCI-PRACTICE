ทำนายว่าติดโทรศัพท์มือถึอไหม โดยใช้ knn
มีตัวแปรทั้งหมด 7,500 ตัวแปร ติดโทรศัพท์ 5308 คน ไม่ติด 2192 คน แต่จะดึงมาแค่ 2000 คนที่ติดกับไม่ติด เพี่อให้ข้อมูลสมดุล
ใช้ cross validation
นำมา train 80% test 20%

ตัวแปรที่นำมาคำนวณมีดังนี้ 
age,gender,daily_screen_time_hours,social_media_hours,gaming_hours,work_study_hours,sleep_hours,notifications_per_day,
app_opens_per_day,weekend_screen_time,stress_level,academic_work_impact

เป้าหมาย
addicted_label
1=ติดโทรศัพท์ 0=ไม่ติด

https://www.kaggle.com/datasets/jayjoshi37/smartphone-usage-and-addiction-prediction 
