<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# Team [32] — [เครื่องคัดแยกมะพร้าวด้วย AI]

> Coding Thailand 2026 — Edge AI Workshop
> [Track  B ] — [Basic]

README ของทีมควรทำหน้าที่เป็นหน้าเล่าเรื่องหลัก: คนอ่านควรเข้าใจได้ภายในไม่กี่นาทีว่าทีมกำลังแก้ปัญหาอะไร ใช้ model แบบไหน และ V2 ดีขึ้นจาก V1 ยังไง

---

## 👥 ทีมเรา

| ชื่อ | บทบาท 3H | GitHub |
|---|---|---|
| ธีรกานต์ เอิ่มชา | Hacker | @ThirakanAomecha |
| ณัชฐพงษ์ อารีย์ไทย | Hipster | @XnatsunoX |
| ณัฐธชา วงสา | Hustler | @naththchawngsa-tech |

---

## 🎯 โจทย์

**Problem:** การคัดแยกชนิดของมะพร้าว (Coconut Classification)

**Target user:** เกษตรกร ผู้ประกอบการ

**Edge AI value:** เพื่อแยกมะพร้าวไปยังช่องที่กำหนดโดยอัตโนมัติ เช่น 
AI วิเคราะห์ว่า
- สีเขียวอ่อน
- ขนาดเล็ก
- ผิวเรียบ
จัดเป็น “มะพร้าวน้ำหอม”

---

## 🔬 Approach

### Track เลือก
- [ ] A — Motion (Modulino Movement)
- [x] B — Vision (USB Webcam)
- [ ] C — Environment (Thermo + Light + Distance)
- [ ] D — Audio (USB Microphone)

### Classes

1. CM
2. CO
3. BG          

### Output
- [ ] Modulino Pixels
- [x] Modulino Buzzer
- [ ] Modulino LED Matrix
- [ ] อื่นๆ: ___

---

## 🔗 Links

- **Edge Impulse Project:** https://studio.edgeimpulse.com/studio/1013301
- **Prototype Video (ถ้ามี):** _ใส่ลิงก์เมื่อพร้อม_

---

## 📊 Results

กรอกเฉพาะตัวเลขที่ทีมวัดได้จริงจากการ train และ test ไม่ต้องเดาตัวเลขให้ดูดี

| Metric | V1 | V2 | Δ |
|---|---|---|---|
| Validation accuracy | 72.5% | 73.9% | +1.4% |
| Test accuracy |  66.67% | 68.52% | +1.85% |
| Inference time | 8 ms |  8 ms | 0 ms |
| Model size | 119.2 KB | 119.2 KB | 0 KB |

---

## 📂 Repository Structure

```
.
├── README.md                  ← ตอนนี้อ่านอยู่ที่นี่
├── docs/
│   ├── setup-notes.md        ← บันทึก setup
│   ├── track-selection.md    ← เหตุผลเลือก track
│   ├── v1-vs-v2.md          ← เปรียบเทียบ model
│   └── issues-and-fixes.md   ← ปัญหาที่เจอ
├── worksheets/
│   ├── W1-class-design.md
│   ├── W2-data-collection-log.md
│   ├── W3-prediction-log.md
│   └── W4-idea-canvas.md
├── code/
│   ├── v1/                   ← Code Model V1
│   └── v2/                   ← Code Model V2
├── assets/
│   └── workspace.jpg         ← ภาพ workspace
└── logs/
    └── predictions.csv       ← Prediction log (machine-readable)
```

---

## ✅ เช็กก่อนสรุปรอบแรก

- [x] Worksheet W1-W4 ครบ
- [x] Edge Impulse project link ใน README
- [x] Model V1 + V2 deploy ได้
- [x] Prediction log ≥10 cases
- [x] V1 vs V2 comparison
- [x] Commit ≥10 ครั้ง
- [x] ทุกคนในทีมเป็น Contributor

---

## 🤝 วิธีอัปเดต repo ทีม

```bash
# Clone repo
git clone <url>
cd <repo>

# สร้าง branch ใหม่ก่อนแก้
git checkout -b feat/your-feature

# แก้ไข แล้ว commit
git add .
git commit -m "docs: เพิ่มชื่อทีมและลิงก์โปรเจกต์"
git push -u origin feat/your-feature

# เปิด Pull Request บน GitHub
```

---

## 📜 License

MIT
