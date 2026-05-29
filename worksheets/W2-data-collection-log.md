<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# 📝 Worksheet W2 — Data Collection Log

> **ทำในช่วง 10:30-12:00**
> บันทึก process ของการเก็บข้อมูล

---

## ข้อมูลทีม + Edge Impulse

- **ชื่อทีม:** Cocobyte
- **Edge Impulse Project URL:**
  ```
  https://studio.edgeimpulse.com/studio/1013301
  ```

---

## 1. Setup Log

ก่อนเริ่มเก็บข้อมูล ทีมทำอะไรบ้าง?

| เวลา | ทำอะไร | ผู้รับผิดชอบ |
|---|---|---|
| 10:30 | เช็คอุปกรณ์ | ณัชฐพงษ์ อารีย์ไทย |
| 10:38 | ศึกษาวิธีใช้ Github | ธีรกานต์ เอิ่มชา |
| 10:42 | ทำความเข้าใจกับ Arduino UNO Q  | ณัฐธชา วงสา |

---

## 2. Data Collection Sessions

บันทึกแต่ละ session การเก็บข้อมูล:

### Session 1

- **เวลา:** 10:45 ถึง 11:00
- **Class:** CO
- **จำนวน samples ที่เก็บ:** 100
- **สภาพแวดล้อม:** โต๊ะที่ไร้สิ่งขีดขวาน
- **ใครเป็น subject?:** กล่องสีส้ม
- **Variation ที่ลอง:** วางจุดที่ต่างกัน
- **ปัญหาที่เจอ:** ภาพ samples ยังน้อยเกินไป

### Session 2

- **เวลา:** 11:00 ถึง 11:15
- **Class:** CM
- **จำนวน samples ที่เก็บ:** 100
- **สภาพแวดล้อม:** โต๊ะที่ไร้สิ่งขีดขวาน
- **ใครเป็น subject?:** กล่องสีฟ้า
- **Variation ที่ลอง:** วางจุดที่ต่างกัน
- **ปัญหาที่เจอ:** ภาพ samples ยังน้อยเกินไป
  
### Session 3

- **เวลา:** 11:15 ถึง 11:30
- **Class:** BG
- **จำนวน samples ที่เก็บ:** 132
- **สภาพแวดล้อม:** พื้นหลังที่ไม่ใช้ CO & CM
- **ใครเป็น subject?:** พื้นหลังที่ไม่ใช้ CO & CM
- **Variation ที่ลอง:** พื้นหลังสี
- **ปัญหาที่เจอ:** นาน

> หาก session มากกว่า 3 ให้ copy template เพิ่ม

---

## 3. Dataset Summary

| Class | จำนวน Train | จำนวน Test | สัดส่วน Train:Test |
|---|---|---|---|
| CO | 79 | 21 | 79 / 21 |
| CM | 83 | 16 | 83 / 16 |
| BG | 78 | 12 | 78 / 12 |
| **รวม** | 240 | 49  | 83 / 17 |

**เป้าหมายตาม W1:** 318 samples × class
**ทำได้จริง:** 289 samples × class
**ห่างจากเป้า:**  -9.12%

---

## 4. Quality Check

ตอบทุกข้อก่อนเริ่ม train:

- [x] ทุก class มี samples ใกล้เคียงกัน (ไม่ต่างกันเกิน 20%)
- [x] เก็บใน ≥2 สภาพแวดล้อม
- [x] เก็บจาก ≥2 subjects (Vision/Audio/Motion ที่มีคน)
- [x] มี variation ใน angle/distance/lighting
- [x] ไม่มี mislabeled data (เช็คตัวอย่างแล้ว)
- [x] Train:Test split = 80:20

---

## 5. Reflection — สิ่งที่เรียนรู้

### a) สิ่งที่ยากที่สุด:
```
การตีกรอบ
```

### b) ถ้าทำใหม่จะปรับอะไร:
```
ถ่ายและตีกรอบให้มากขึ้น
```

### c) คาดการณ์: model จะ confuse class ไหนกับอะไรมากที่สุด?
```
BG เพราะพื้นหลังอาจจะมีสีที่เข้ากับ CO & CM
```

---

## 📤 วิธี submit

```bash
git add worksheets/W2-data-collection-log.md
git commit -m "docs: data collection log เก็บได้ครบ X samples ใน Y session"
git push
```

---

## 💡 Best Practices

1. **อย่าเก็บข้อมูลที่ "สมบูรณ์แบบ" หมด** — โลกจริงไม่สมบูรณ์แบบ
2. **เก็บข้อมูล "เหมือนไม่ใช่ class ใดเลย" เป็นอีก class** = noise/background class
3. **สลับคนเก็บ** — กัน bias ของ subject เดียว
4. **เช็คตัวอย่างทุก 20 samples** — กัน mislabel
