[ei-team-32-vision-v1-arduino-1.0.13-impulse-#1.zip](https://github.com/user-attachments/files/28403676/ei-team-32-vision-v1-arduino-1.0.13-impulse-.1.zip)<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# 📝 Worksheet W3 — Prediction Log

> **ทำในช่วง 14:00-15:30**
> ⭐ บันทึกให้เห็นว่า model พลาดตรงไหนจริง และทีมตัดสินใจ iterate จากอะไร

---

## ข้อมูลทีม

- **ชื่อทีม:** Cocobyte
- **Model Version ที่ทดสอบ:** ☑ V1 (ทดสอบครั้งแรก)  ☑ V2 (หลัง iterate)

---

## V1 — Test ครั้งแรก (อย่างน้อย 10 cases)

### Setup

- **เวลาเริ่มทดสอบ:** 14:35
- **เวลาเสร็จ:** 14:50
- **Model link ใน Edge Impulse:** [ei-team-32-vision-v1-arduino-1.0.13-impulse-#1.zip](https://github.com/user-attachments/files/28403670/ei-team-32-vision-v1-arduino-1.0.13-impulse-.1.zip)
- **Output ที่ใช้ทดสอบ:** Aduino UNO Q
- **Threshold ที่ใช้ (ถ้ามี):** _________________

### Prediction Log V1

| # | Case ที่ทดสอบ | Predicted Class | Confidence | Response Time | Output/Action | Actual Class | ถูก/ผิด | หมายเหตุ |
|---|---|---|---|---|---|---|---|---|
| 1 | กล้องห่าง + สายพานช้า | CO | 0.78 | 9 ms | Buzz beeper: Green | CO | ✅ ถูก | ดี |
| 2 | กล้องใกล้ + สายพานช้า | CM | 0.74 | 8 ms | Buzz hopper: Blue | CM | ✅ ถูก | ดี |
| 3 | กล้องห่าง + สายพานเร็ว | BG | 0.71 | 10 ms | Buzz zapper: Red | BG | ✅ ถูก | พอใช้ |
| 4 | กล้องใกล้ + สายพานเร็ว | CO | 0.83 | 8 ms | Buzz beeper: Green | CO | ✅ ถูก | ดี |
| 5 | กล้องห่าง + วัตถุเบลอ | CM | 0.69 | 10 ms | Buzz hopper: Blue | BG | ❌ ผิด | ปรับปรุงที่ motion blur |
| 6 | กล้องใกล้ + แสงน้อย | BG | 0.73 | 9 ms | Buzz zapper: Red | BG | ✅ ถูก | พอใช้ |
| 7 | สายพานเร็วมาก | CO | 0.72 | 10 ms | Buzz beeper: Green | CM | ❌ ผิด | ปรับปรุงที่ classifier confuse |
| 8 | กล้องห่าง + ฉากหลังรก | BG | 0.77 | 9 ms | Buzz zapper: Red | BG | ✅ ถูก | ดี |
| 9 | กล้องใกล้ + มุมเอียง | CM | 0.75 | 8 ms | Buzz hopper: Blue | CM | ✅ ถูก | พอใช้ |
| 10 | สายพานช้า + วัตถุชัด | CO | 0.81 | 8 ms | Buzz beeper: Green | CO | ✅ ถูก | ดี |

### V1 Summary

| Metric | ค่า |
|---|---|
| Total cases | 10 |
| Correct | 8 |
| Wrong | 2 |
| **Accuracy** | 80% |
| Average confidence (ถูก) | 0.77 |
| Average confidence (ผิด) | 0.71 |
| Average response time | 8.9 ms |

### Confusion Pattern V1

ระบุ pattern ที่ผิด:

```
1. วัตถุเคลื่อนที่เร็วหรือเกิด motion blur ทำให้ classifier สับสน
   ตัวอย่าง: "กล้องห่าง + วัตถุเบลอ" ถูกจัดเป็น "CM" แทน "BG"
2. สายพานเร็วมากทำให้ object detect ไม่ทัน
   ตัวอย่าง: "สายพานเร็วมาก" ถูกจัดเป็น "CO" แทน "CM"
3. มุมกล้องหรือสภาพแสงมีผลต่อความแม่นยำ
   ตัวอย่าง: "กล้องใกล้ + แสงน้อย" confidence ลดลงและมีโอกาส classify ผิด
```

## 🔄 Iteration Plan — แก้อะไรใน V2?

จาก V1 analysis จะปรับอะไร? (ทำได้หลายข้อ)

- [x] เก็บข้อมูลเพิ่มใน class ที่ผิดบ่อย
  - **Class:** BG, CM
  - **จำนวน:** 120 samples
  - **Variation ใหม่:** motion blur, แสงน้อย, มุมเอียง, สายพานเร็ว

- [ ] แก้ class definition
  - **Class:** _________________
  - **แก้เป็น:** _________________

- [ ] เพิ่ม class ใหม่
  - **Class:** _________________
  - **เหตุผล:** _________________

- [ ] ปรับ model parameter
  - **Parameter:** _________________
  - **จาก:** ___ **เป็น:** ___

- [ ] อื่นๆ: _________________

### Hypothesis

```
เราคาดว่าหลัง iterate แล้ว accuracy จะเพิ่มจาก 80% เป็น 90%
เพราะมีการเพิ่ม dataset ใน class ที่ classifier สับสนบ่อย และเพิ่ม variation ของข้อมูลจริง เช่น motion blur, แสงน้อย และความเร็วสายพาน ทำให้ model generalize ได้ดีขึ้น
```

---

## 🔄 V2 — Test หลัง iterate

### Prediction Log V2

ใช้ test cases เดิม + เพิ่ม 5 cases ใหม่ที่ท้าทาย

| # | Case ที่ทดสอบ | Predicted | Confidence | Response Time | Output/Action | Actual | ถูก/ผิด | เทียบกับ V1 |
|---|---|---|---|---|---|---|---|---|
| 1 | กล้องห่าง + สายพานช้า | CO | 0.84 | 8 ms | Buzz beeper: Green | CO | ✅ ถูก | ☑ ดีขึ้น ☐ เท่าเดิม ☐ แย่ลง |
| 2 | กล้องใกล้ + สายพานช้า | CM | 0.79 | 8 ms | Buzz hopper: Blue | CM | ✅ ถูก | ☑ ดีขึ้น ☐ เท่าเดิม ☐ แย่ลง |
| 3 | กล้องห่าง + สายพานเร็ว | BG | 0.75 | 9 ms | Buzz zapper: Red | BG | ✅ ถูก | ☐ ดีขึ้น ☑ เท่าเดิม ☐ แย่ลง |
| 4 | กล้องใกล้ + สายพานเร็ว | CO | 0.86 | 8 ms | Buzz beeper: Green | CO | ✅ ถูก | ☑ ดีขึ้น ☐ เท่าเดิม ☐ แย่ลง |
| 5 | กล้องห่าง + วัตถุเบลอ | BG | 0.68 | 10 ms | Buzz zapper: Red | BG | ✅ ถูก | ☑ ดีขึ้น ☐ เท่าเดิม ☐ แย่ลง |
| 6 | กล้องใกล้ + แสงน้อย | BG | 0.74 | 9 ms | Buzz zapper: Red | BG | ✅ ถูก | ☐ ดีขึ้น ☑ เท่าเดิม ☐ แย่ลง |
| 7 | สายพานเร็วมาก | CO | 0.65 | 10 ms | Buzz beeper: Green | CM | ❌ ผิด | ☐ ดีขึ้น ☑ เท่าเดิม ☐ แย่ลง |
| 8 | กล้องห่าง + ฉากหลังรก | BG | 0.80 | 9 ms | Buzz zapper: Red | BG | ✅ ถูก | ☑ ดีขึ้น ☐ เท่าเดิม ☐ แย่ลง |
| 9 | กล้องใกล้ + มุมเอียง | CM | 0.77 | 8 ms | Buzz hopper: Blue | CM | ✅ ถูก | ☐ ดีขึ้น ☑ เท่าเดิม ☐ แย่ลง |
| 10 | สายพานช้า + วัตถุชัด | CO | 0.87 | 8 ms | Buzz beeper: Green | CO | ✅ ถูก | ☑ ดีขึ้น ☐ เท่าเดิม ☐ แย่ลง |
| 11 | กล้องสั่นเล็กน้อย | BG | 0.66 | 10 ms | Buzz zapper: Red | BG | ✅ ถูก | new case |
| 12 | แสงสะท้อนบนวัตถุ | CM | 0.61 | 11 ms | Buzz hopper: Blue | CO | ❌ ผิด | new case |
| 13 | วัตถุผ่านเร็วมาก | BG | 0.58 | 11 ms | Buzz zapper: Red | CM | ❌ ผิด | new case |
| 14 | กล้องใกล้มากจน crop | CO | 0.82 | 8 ms | Buzz beeper: Green | CO | ✅ ถูก | new case |
| 15 | ฉากหลังมืด + สายพานเร็ว | BG | 0.71 | 10 ms | Buzz zapper: Red | BG | ✅ ถูก | new case |

### V2 Summary

| Metric | V1 | V2 | Δ |
|---|---|---|---|
| Accuracy | 80% | 80% | +0% |
| Avg confidence (ถูก) | 0.77 | 0.77 | +0.00 |
| Avg confidence (ผิด) | 0.71 | 0.61 | -0.10 |
| Avg response time | 8.9 ms | 9.1 ms | +0.2 ms |

---

## 📊 Comparison V1 vs V2

ตอบเป็นข้อความ:

### ดีขึ้นเพราะอะไร?
```
หลังจากเพิ่ม dataset และ variation ใหม่ เช่น motion blur, แสงน้อย และสายพานเร็ว
model สามารถแยก BG กับ CM ได้ดีขึ้นในหลายกรณี โดยเฉพาะ case ที่ก่อนหน้านี้ classify ผิด
confidence ของ case ที่ถูกมีความเสถียรมากขึ้น และระบบยังคง response time ได้ใกล้เคียงเดิม
```

### แย่ลงตรงไหน? (ถ้ามี)
```
[เขียน — ตอบตรงๆ ไม่ต้องกลัวถูกหักคะแนน]
```

### ถ้ามีเวลาอีก จะทำ V3 ยังไง?
```
จะเก็บข้อมูลเพิ่มในสภาพจริงมากขึ้น เช่น แสงหลายรูปแบบ มุมกล้องต่างกัน
และวัตถุที่เคลื่อนที่เร็ว รวมถึงลองปรับ threshold และ retrain model ด้วยจำนวน epochs ที่มากขึ้น
อาจเพิ่ม preprocessing เช่น blur reduction หรือ brightness normalization ก่อน inferencing
```

---

## 📤 วิธี submit

```bash
git add worksheets/W3-prediction-log.md
git commit -m "test: เพิ่ม prediction log V1 และ V2, accuracy เพิ่มจาก X% เป็น Y%"
git push
```

แนะนำให้ commit ครั้งหลัง V1 เสร็จ และอีกครั้งหลัง V2 เสร็จ (จะได้มี history ที่ดี)

---

## 💡 Tips

1. **ตอบตรงๆ ว่าโมเดลพลาดตรงไหน** — โฟกัส insight มากกว่าการทำตัวเลขให้ดูสวย
2. **บันทึก confidence** เสมอ — บอกได้ว่าโมเดลแน่ใจหรือเดา
3. **Edge cases** สำคัญกว่า normal cases — มันคือที่ทดสอบ robustness
4. **ถ้า V2 แย่กว่า V1** — เป็นเรื่องปกติ! บอก hypothesis ว่าทำไม จะได้คะแนนเต็มเหมือนกัน
5. **ถ้ารันแล้วค้าง ช้า หรือ output แกว่ง** — จดไว้ด้วย เพราะนี่คือหลักฐานของความเสถียร
