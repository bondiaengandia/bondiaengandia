---
layout: default
title: Dostępność
icon:	fas fa-calendar
---

<link href="https://cdn.jsdelivr.net/npm/fullcalendar@6.1.11/index.global.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/fullcalendar@6.1.11/index.global.min.js"></script>

<h2>Dostępność</h2>
<div id="calendar"></div>

<script>
document.addEventListener('DOMContentLoaded', async function() {
  const el = document.getElementById('calendar');
  const cal = new FullCalendar.Calendar(el, {
    initialView: 'dayGridMonth',
    height: 'auto',
    events: async function(fetchInfo, successCallback, failureCallback) {
      try {
        const res = await fetch('/data/booking-events.json', { cache: 'no-store' });
        const events = await res.json();
        successCallback(events);
      } catch (e) { failureCallback(e); }
    }
  });
  cal.render();
});
</script>