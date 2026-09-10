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


---
obsidianUIMode: preview
---

# 📊 통합 기록 대시보드

```dataviewjs
// 현재 선택 상태 기억
window.currentTrackerType = window.currentTrackerType || "daily";
window.currentYear = window.currentYear || new Date().getFullYear();

// 상단 선택 UI
const topBar = document.createElement("div");
topBar.style.marginBottom = "20px";

topBar.innerHTML = `
<div style="
display:flex;
align-items:center;
gap:10px;
margin-bottom:10px;
">

<button id="prev-year" style=" padding:4px 10px; border-radius:6px; cursor:pointer; ">❮</button>

<span id="year-label"
style="
font-size:18px;
font-weight:bold;
min-width:60px;
text-align:center;
">
${window.currentYear}
</span>

<button id="next-year" style=" padding:4px 10px; border-radius:6px; cursor:pointer; ">❯</button>

</div>

<label style="font-weight:bold; margin-right:10px;">
🔍 보기 선택:
</label>

<select id="tracker-select"
style="padding:5px 10px; border-radius:5px;">
    <option value="daily"
        ${window.currentTrackerType === "daily" ? "selected" : ""}>
        📝 일상 기록 달력
    </option>
    <option value="dream"
        ${window.currentTrackerType === "dream" ? "selected" : ""}>
        💭 꿈 기록 달력
    </option>
</select>
`;

this.container.appendChild(topBar);

// 달력 표시 영역
const calendarWrapper = document.createElement("div");
calendarWrapper.style.width = "100%";
this.container.appendChild(calendarWrapper);

// 현재 선택된 달력 렌더링

async function renderCurrentCalendar() {

    // 기존 달력 제거
    calendarWrapper.innerHTML = "";

    let data = {
        entries: []
    };

    if (window.currentTrackerType === "daily") {

        data.colors = {
            green: [
                "#b5f5ec",
                "#87e8de",
                "#5cdbd3",
                "#36cfc9",
                "#13c2c2"
            ]
        };

        for (let page of dv.pages("#daily")) {

            let dateVal =
                page.file.frontmatter?.date ||
                page.date;

            if (
            dateVal &&
                window.moment(dateVal).year() === window.currentYear
                ) {
            data.entries.push({
                date: window.moment(dateVal).format("YYYY-MM-DD"),
                intensity: 1,
                });
            }
        }

    } else {

        data.colors = {
            purple: [
                "#efdbff",
                "#d3adf7",
                "#b37feb",
                "#9254de",
                "#722ed1"
            ]
        };

        for (let page of dv.pages("#dream")) {

            let dateVal =
                page.file.frontmatter?.date ||
                page.date

            if (
            dateVal &&
                window.moment(dateVal).year() === window.currentYear
                ) {
                data.entries.push({
                   date: window.moment(dateVal).format("YYYY-MM-DD"),
                    intensity: 1
                    });
            }
        }
    }

    renderHeatmapCalendar(calendarWrapper, data);
}

// 최초 렌더링
await renderCurrentCalendar();

// 토글 변경
const selectBox = topBar.querySelector("#tracker-select");

selectBox.addEventListener("change", async (e) => {

    window.currentTrackerType = e.target.value;

    await renderCurrentCalendar();
});



const yearLabel = topBar.querySelector("#year-label");

topBar.querySelector("#prev-year")
.addEventListener("click", async () => {

    window.currentYear--;

    yearLabel.textContent = window.currentYear;

    await renderCurrentCalendar();
});

topBar.querySelector("#next-year")
.addEventListener("click", async () => {

    window.currentYear++;

    yearLabel.textContent = window.currentYear;

    await renderCurrentCalendar();
});






