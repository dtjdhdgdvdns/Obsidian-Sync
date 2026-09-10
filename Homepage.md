---
obsidianUIMode: preview
---
# 👋 환영합니다, 내 공간

> "오늘도 목표를 향해 한 걸음씩 나아가는 중!"

---

## 📌 1. 핵심 바로가기 (Quick Access)
> 자주 열어보는 가장 중요한 페이지들을 모아두는 공간입니다.
* [[대입 전형 분석]] *(아까 그 복잡한 표가 있는 노트)*
* [[수학 공부 노트]]
* [[오늘의 할 일 / 스케줄]]

---

## 📊 2. 주요 데이터 요약 (Quick View)
> 자주 찾아보는 대입 전형 표나 핵심 데이터를 첫 화면에서 바로 확인합니다.

![[대입전형.xlsx]] 

2357*(엑셀 뷰어나 시트 플러그인으로 연동해 둔 표의 링크를 여기에 쏙 집어넣으면 첫 화면에서 바로 보입니다!)*

---

## 🎯 3. 오늘의 집중 과제
- [ ] 입시 자료 최종 검토하기
- [ ] 수학 모의고사 오답 노트 정리
- [ ] 1일 1커밋 또는 공부 계획 체크





```dataviewjs
// 1. 일상 기록 잔디 달력
dv.span("**📝 일상 기록 달력**")

const dailyData = {
    year: 2026, // 연도 (필요시 수정)
    colors: {
        green: ["#b5f5ec", "#87e8de", "#5cdbd3", "#36cfc9", "#13c2c2"]
    },
    entries: []
}

// #daily 태그가 있는 노트를 찾아 잔디 데이터에 추가
for(let page of dv.pages('#daily')){
    let dateStr = page.file.name.substring(0, 10); // 파일 이름에서 날짜 추출
    dailyData.entries.push({
        date: dateStr,
        intensity: 1,
        content: await dv.span(`[](${page.file.name})`), // 마우스 올리면 미리보기 표시
    })       
}

renderHeatmapCalendar(this.container, dailyData)


// 2. 꿈 기록 잔디 달력
dv.span("<br><br>**💭 꿈 기록 달력**")

const dreamData = {
    year: 2026, // 연도 (필요시 수정)
    colors: {
        purple: ["#efdbff", "#d3adf7", "#b37feb", "#9254de", "#722ed1"]
    },
    entries: []
}

// #dream 태그가 있는 노트를 찾아 잔디 데이터에 추가
for(let page of dv.pages('#dream')){
    let dateStr = page.file.name.substring(0, 10); // 파일 이름에서 날짜 추출
    dreamData.entries.push({
        date: dateStr,
        intensity: 1,
        content: await dv.span(`[](${page.file.name})`), // 마우스 올리면 미리보기 표시
    })       
}

renderHeatmapCalendar(this.container, dreamData)