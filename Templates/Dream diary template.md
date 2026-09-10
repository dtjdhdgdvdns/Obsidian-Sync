<% await tp.file.rename(tp.date.now("YYYY.MM.DD") + " " + await tp.system.prompt("오늘 꿈의 제목을 한 줄로 적어주세요")) -%>
---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - dream
lucid_dream: false
sleep_quality: "<% await tp.system.suggester(["🟢 아주 푹 잠", "🟡 보통", "🔴 뒤척임/피곤함"], ["푹 잠", "보통", "피곤함"]) %>"
emotion: "<% await tp.system.suggester(["😊 평온/즐거움", "😨 공포/불안", "🤔 이상함/기괴함", "😢 슬픔"], ["평온", "공포", "이상함", "슬픔"]) %>"
keyword: [<% await tp.system.prompt("꿈에 나온 핵심 키워드를 입력하세요 (여러 개일 경우 쉼표로 구분)") %>]
---

## 💭 꿈의 내용
> *어떤 일이 있었나요? 일어난 직후 기억나는 대로 자유롭게 적어보세요.*
* 

## 🔍 특징 및 감상
- [ ] **루시드 드림:** 
- **인상 깊었던 장면:** 
- **나의 해석/느낌:** 

## 🛌 수면 메모
* **취침 시간:** 
* **기상 시간:**