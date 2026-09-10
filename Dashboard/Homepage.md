---
cssclasses:
  - notion-dashboard
obsidianUIMode: preview
---

# 👋 환영합니다, 내 공간

> "오늘도 목표를 향해 한 걸음씩 나아가는 중!"

---

```dataviewjs
const { MarkdownRenderer, Component } = require("obsidian");
const comp = new Component();
comp.load();

// 1. 날짜 및 주/월 자동 계산
const todayStr = moment().format("YYYY.MM.DD");
const year = moment().format("YYYY");
const week = moment().format("W[주차]");
const month = moment().format("M[월]");

// 2. 오늘 일기장 찾기
const dailyPage = dv.pages().find(p => p.file.name.startsWith(todayStr));
const dailyFileName = dailyPage ? dailyPage.file.name : `${todayStr} 일기`;

// 3. quick links 전용 노션 스타일 자동 주입 (점 제거, 세리프 폰트, 텍스트 밑줄)


// 4. 4:6 비율 그리드 생성
const grid = this.container.createEl("div", {
    attr: { style: "display: grid; grid-template-columns: 4fr 6fr; gap: 40px; align-items: start;" }
});

const leftCol = grid.createEl("div", { cls: "notion-quick-links" });
const rightCol = grid.createEl("div");

// iframe 위젯 코드 (필요 시 src 안에 링크 입력)
// iframe 위젯 코드 (필요 시 src 안에 링크 입력)
const myIframe = `<iframe src="https://indify.co/widgets/live/progressBar/e68wM1pKhHVkIxx3Y4qF" width="100%" height="400" style="border: 0;"></iframe>`;

// 5. 좌측 40% 영역 (quick links 스타일 적용)
const leftContent = [
    "### quick links",
    "- 📄 [[2028 입시 계획]]",
    "- 📑 [[2028 커리큘럼]]",
    "- 📐 [[수학 노트]]",
    "- 🎵 [[플레이리스트]]",
    "",
    "![[Waguri kaoruko.jpg|1000]]",
    
    
    
    
'<div style="margin-top: 40px; text-align: center;">', 
'<img src="' + app.vault.adapter.getResourcePath('Waguri kaoruko.jpg') + 
'" style="width: 100%; max-width: 250px; border-radius: 8px;" />', '</div>', 
    
    "",
    myIframe
].join("\n");

// 6. 우측 60% 영역 (제목을 클릭 가능한 링크로 변경)
const rightContent = [
    `### [[${dailyFileName}|today]]`,
    `![[${dailyFileName}#🎯 오늘의 목표]]`,
    "",
    "---",
    "",
    `### [[${year} 주간 목표|this week]]`,
    `![[${year} 주간 목표#${week}]]`,
    "",
    "---",
    "",
    `### [[${year} 월간 목표|this month]]`,
    `![[${year} 월간 목표#${month}]]`
].join("\n");
// 7. 화면 렌더링
await MarkdownRenderer.render(app, leftContent, leftCol, dv.current().file.path, comp);
await MarkdownRenderer.render(app, rightContent, rightCol, dv.current().file.path, comp);
```

# 📊 통합 기록 
```dataviewjs

window.currentTrackerType =
    window.currentTrackerType || "daily";

const topBar = document.createElement("div");

topBar.innerHTML = `
<label style="font-weight:bold;margin-right:10px;">
🔍 보기 선택:
</label>

<select id="tracker-select"
style="padding:5px 10px;border-radius:5px;">
    <option value="daily"
        ${window.currentTrackerType === "daily" ? "selected" : ""}>
        📝 일상 기록
    </option>

    <option value="dream"
        ${window.currentTrackerType === "dream" ? "selected" : ""}>
        💭 꿈 기록
    </option>
</select>
`;

this.container.appendChild(topBar);

const trackerContainer =
    document.createElement("div");

trackerContainer.style.marginTop = "15px";

this.container.appendChild(trackerContainer);

async function renderTracker() {

    trackerContainer.innerHTML = "";

    let trackerData = {
        entries: []
    };

    if (window.currentTrackerType === "daily") {

        trackerData.heatmapTitle =
            "📝 일상 기록";

        for (let page of dv.pages("#daily")) {

            let dateVal =
                page.file.frontmatter?.date ||
                page.date;

            if (dateVal) {

                trackerData.entries.push({
                    date: window
                        .moment(dateVal)
                        .format("YYYY-MM-DD"),

                    intensity: 1,

                    filePath:
                        page.file.path
                });
            }
        }

    } else {

        trackerData.heatmapTitle =
            "💭 꿈 기록";

        for (let page of dv.pages("#dream")) {

            let dateVal =
                page.file.frontmatter?.date ||
                page.date;

            if (dateVal) {

                trackerData.entries.push({
                    date: window
                        .moment(dateVal)
                        .format("YYYY-MM-DD"),

                    intensity: 1,

                    filePath:
                        page.file.path
                });
            }
        }
    }

    renderHeatmapTracker(
        trackerContainer,
        trackerData
    );
}

await renderTracker();

topBar
.querySelector("#tracker-select")
.addEventListener(
    "change",
    async (e) => {

        window.currentTrackerType =
            e.target.value;

        await renderTracker();
    }
);

```