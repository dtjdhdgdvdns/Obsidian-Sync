<% await tp.file.rename(tp.date.now("YYYY.MM.DD") + " " + await tp.system.prompt("오늘 꿈의 제목을 한 줄로 적어주세요")) -%>
---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - daily
condition: "<% await tp.system.suggester(["😄 최고", "😐 보통", "🤒 피곤함"], ["최고", "보통", "피곤함"]) %>"
---

## 🎯 오늘의 목표
- [ ] 기상: 7시 전에 일어나기!
- [ ] 운동: 새벽운동
- [ ] 공부: 12 hours over, 계획표 지키기

## 💬 오늘의 일상
* 

## 📖 오늘의 학습
*