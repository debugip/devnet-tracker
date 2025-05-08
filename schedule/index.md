---
layout: default
title: Study Schedule
---

# 📅 Study Schedule

<div id="calendar"></div>

<script>
  const topics = [
    "Software Dev",
    "APIs",
    "Cisco Platforms",
    "App Deployment",
    "Automation",
    "Networking"
  ];
  const today = new Date();
  const currentMonth = today.getMonth();
  const currentYear = today.getFullYear();

  const calendar = document.getElementById("calendar");
  const studyPlan = {}; // dateString => topic
  for (let i = 0; i < 30; i++) {
    const date = new Date(currentYear, currentMonth, today.getDate() + i);
    const key = date.toISOString().split("T")[0];
    const topic = topics[Math.floor(i / 5) % topics.length];
    studyPlan[key] = topic;
  }

  function generateCalendar(year, month) {
    const first = new Date(year, month, 1);
    const last = new Date(year, month + 1, 0);
    let html = "<table border='1' style='border-collapse:collapse;width:100%'><tr>";
    const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
    for (const d of days) html += "<th>" + d + "</th>";
    html += "</tr><tr>";

    for (let i = 0; i < first.getDay(); i++) html += "<td></td>";
    for (let d = 1; d <= last.getDate(); d++) {
      const day = new Date(year, month, d);
      const key = day.toISOString().split("T")[0];
      const plan = studyPlan[key] || "";
      html += `<td style='height:100px;vertical-align:top'><strong>${d}</strong><br/><small>${plan}</small></td>`;
      if (day.getDay() === 6) html += "</tr><tr>";
    }
    html += "</tr></table>";
    calendar.innerHTML = html;
  }

  generateCalendar(currentYear, currentMonth);
</script>
