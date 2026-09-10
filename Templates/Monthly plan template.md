<%*
const yearMatch = tp.file.title.match(/\d{4}/);
const year = yearMatch ? yearMatch[0] : tp.date.now("YYYY");
tR += `# 📅 ${year} 월간 목표\n\n`;

// 1월부터 12월까지 자동 반복 생성
for (let m = 1; m <= 12; m++) {
    tR += `## ${m}월\n\n`;
    tR += `> **💡 이달의 핵심 키워드:** \n\n`;
    tR += `**🎯 월간 목표 (Milestones)**\n`;
    tR += `- [ ] \n`;
    tR += `- [ ] \n\n`;
    tR += `**📝 월말 회고 / 메모**\n`;
    tR += `- \n\n`;
    tR += `---\n\n`;
}
_%>