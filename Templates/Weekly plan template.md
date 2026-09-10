<%*
// 파일 제목에서 연도 추출 (없으면 현재 연도 2026 자동 지정)
const yearMatch = tp.file.title.match(/\d{4}/);
const year = yearMatch ? yearMatch[0] : tp.date.now("YYYY");
tR += `# 📌 ${year} 주간 목표\n\n`;

// 1주차부터 52주차까지 자동 반복 생성
for (let w = 1; w <= 52; w++) {
    tR += `## ${w}주차\n\n`;
    tR += `**🎯 주간 집중 과제**\n`;
    tR += `- [ ] \n\n`;
    tR += `**📚 공부 & 입시**\n`;
    tR += `- [ ] \n`;
    tR += `- [ ] \n\n`;
    tR += `**🛠️ 프로젝트 & 개인**\n`;
    tR += `- [ ] \n\n`;
    tR += `---\n\n`;
}
_%>