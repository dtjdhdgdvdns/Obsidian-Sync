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







// 1. 전환 버튼(드롭다운) HTML 생성 컨테이너
const container = dv.container;
const div = container.createDiv();
div.style.marginBottom = "15px";
div.style.display = "flex";
div.style.alignItems = "center";
div.style.gap = "10px";

div.innerHTML = `
    <label style="font-weight: bold; font-size: 14px;">📊 보기 전환:</label>
    <select id="heatmap-selector" style="padding: 5px 10px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal); cursor: pointer;">
        <option value="study_hours">공부 시간 (시간)</option>
        <option value="todo_count">할 일 완료 개수 (개)</option>
        <option value="math_score">수학 모의고사 점수 (점)</option>
    </select>
`;

const select = div.querySelector("#heatmap-selector");
const renderArea = container.createDiv();

// 2. 히트맵을 그려주는 함수
function renderSelectedHeatmap(metricKey) {
    renderArea.innerHTML = ""; // 기존에 그려진 히트맵 초기화
    
    const calendarData = {
        year: 2026,
        pages: dv.pages('""'),
        step: 1,
        entries: dv.pages('""').map(day => {
            let val = day.file.frontmatter[metricKey] || 0;
            return {
                date: day.file.day,
                intensity: val,
                content: `날짜: ${day.file.name}\n기록 (${metricKey}): ${val}`,
            }
        }),
        theme: metricKey === "study_hours" ? "green" : (metricKey === "todo_count" ? "blue" : "orange"), 
    }

    window.renderHeatmapCalendar(renderArea, calendarData);
}

// 3. 처음 켤 때 기본값으로 렌더링
renderSelectedHeatmap(select.value);

// 4. 드롭다운을 바꿀 때마다 실시간으로 히트맵 변경
select.addEventListener("change", (e) => {
    renderSelectedHeatmap(e.target.value);
});