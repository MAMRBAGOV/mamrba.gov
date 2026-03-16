---
layout: default
title: Page Title
---
# Merrimack River Beach Alliance (MRBA)

Welcome to the Merrimack River Beach Alliance — a regional partnership of Salisbury, Newbury, and Newburyport working together with state and federal agencies to protect, improve, and enhance the beaches and shoreline along the Merrimack River and surrounding coast.

Our beaches are a shared resource. They support local communities, tourism, wildlife habitat, and coastal resilience. By working together across town boundaries, we can make smarter investments, plan for the future, and create a safer, more accessible shoreline for everyone.
<style>
:root{
  --ocean-dark:#0b3d91;
  --ocean:#1565c0;
  --ocean-light:#e3f2fd;
  --white:#ffffff;
  --gray:#e0e0e0;
}

body{
  font-family: Arial, sans-serif;
}

.calendar{
  max-width: 720px;
  margin: 24px auto;
  border: 1px solid var(--gray);
  border-radius: 10px;
  overflow: hidden;
  background: var(--white);
}

.cal-header{
  background: linear-gradient(135deg,var(--ocean-dark),var(--ocean));
  color: var(--white);
  padding: 14px;
  display:flex;
  justify-content:space-between;
  align-items:center;
}

.cal-header button{
  background: var(--white);
  color: var(--ocean-dark);
  border:none;
  padding:6px 10px;
  border-radius:4px;
  cursor:pointer;
  font-weight:bold;
}

.month-year{
  font-size:18px;
  font-weight:bold;
}

.days, .dates{
  display:grid;
  grid-template-columns: repeat(7,1fr);
  text-align:center;
}

.days{
  background: var(--ocean-light);
  font-weight:bold;
  padding:8px 0;
}

.dates div{
  padding:14px 6px;
  border:1px solid #f5f5f5;
  min-height:60px;
  position:relative;
}

.today{
  background: var(--ocean-light);
  border:2px solid var(--ocean);
}

.meeting-day{
  background:#e8f5e9;
  cursor:pointer;
}

.meeting-dot{
  width:3px;
  height:3px;
  background:var(--ocean);
  border-radius:50%;
  margin:4px auto 0;
}

.event-panel{
  border-top:1px solid var(--gray);
  padding:16px;
  background:#fafafa;
}

.event-title{
  font-weight:bold;
  color:var(--ocean-dark);
  margin-bottom:6px;
}
</style>

<div class="calendar">
  <div class="cal-header">
    <button onclick="changeMonth(-1)">◀</button>
    <div class="month-year" id="monthYear"></div>
    <button onclick="changeMonth(1)">▶</button>
  </div>

  <div class="days">
    <div>Sun</div><div>Mon</div><div>Tue</div><div>Wed</div>
    <div>Thu</div><div>Fri</div><div>Sat</div>
  </div>

  <div class="dates" id="dates"></div>

  <div class="event-panel" id="eventPanel">
    <div class="event-title">Public Meetings</div>
    <div>Select a highlighted date to view meetings.</div>
  </div>
</div>

<script>
// ====== ADD MEETINGS HERE ======
const meetings = {
   "2026-03-13": [
    { title:"MRBA Meeting", time:"10:00 AM", location:"PITA Hall" }
  ],
};
// ===============================

const monthYear = document.getElementById("monthYear");
const datesContainer = document.getElementById("dates");
const eventPanel = document.getElementById("eventPanel");

let currentDate = new Date();

function formatDateKey(year, month, day){
  const m = String(month+1).padStart(2,'0');
  const d = String(day).padStart(2,'0');
  return `${year}-${m}-${d}`;
}

function renderCalendar(date){
  const year = date.getFullYear();
  const month = date.getMonth();

  const firstDay = new Date(year, month, 1).getDay();
  const lastDate = new Date(year, month + 1, 0).getDate();

  monthYear.textContent = date.toLocaleString('default',{month:'long',year:'numeric'});
  datesContainer.innerHTML = "";

  for(let i=0;i<firstDay;i++){
    datesContainer.innerHTML += "<div></div>";
  }

  for(let day=1; day<=lastDate; day++){
    const div = document.createElement("div");
    div.textContent = day;

    const key = formatDateKey(year, month, day);

    const today = new Date();
    if(day===today.getDate() && month===today.getMonth() && year===today.getFullYear()){
      div.classList.add("today");
    }

    if(meetings[key]){
      div.classList.add("meeting-day");
      const dot = document.createElement("div");
      dot.className = "meeting-dot";
      div.appendChild(dot);
      div.onclick = ()=>showMeetings(key);
    }

    datesContainer.appendChild(div);
  }
}

function showMeetings(dateKey){
  const items = meetings[dateKey];
  let html = `<div class="event-title">Meetings on ${dateKey}</div>`;
  items.forEach(m=>{
    html += `<div><strong>${m.title}</strong><br>${m.time}<br>${m.location}</div><br>`;
  });
  eventPanel.innerHTML = html;
}

function changeMonth(offset){
  currentDate.setMonth(currentDate.getMonth()+offset);
  renderCalendar(currentDate);
}

renderCalendar(currentDate);
</script>
## What We Do
- Improve public access to beaches and waterfronts  
- Protect dunes, marshes, and natural coastal systems  
- Support coastal resilience and flood protection  
- Coordinate regional planning and grant funding  
- Keep the public informed and involved  

## Our Communities

<div style="display: flex; flex-wrap: wrap; gap: 20px; margin-top: 20px;">

  <!-- Salisbury Card -->
  <a href="/salisbury" style="flex: 1; min-width: 200px; max-width: 300px; text-decoration: none;">
    <div style="background: white; border-radius: 10px; overflow: hidden; box-shadow: 0 3px 8px rgba(0,0,0,.1);">
      <img src="/assets/images/towns/salisbury-beach-thumb.jpg" alt="Salisbury" style="width: 100%; display: block;">
      <div style="padding: 15px; color: var(--text); text-align: center;">
        <h3>Salisbury</h3>
        <p>Beach improvements, public access, and coastal protection initiatives.</p>
      </div>
    </div>
  </a>

  <!-- Newbury Card -->
  <a href="/newbury" style="flex: 1; min-width: 200px; max-width: 300px; text-decoration: none;">
    <div style="background: white; border-radius: 10px; overflow: hidden; box-shadow: 0 3px 8px rgba(0,0,0,.1);">
      <img src="/assets/images/towns/newbury-thumb.jpg" alt="Newbury" style="width: 100%; display: block;">
      <div style="padding: 15px; color: var(--text); text-align: center;">
        <h3>Newbury</h3>
        <p>Maintaining safe, accessible beaches and natural habitats.</p>
      </div>
    </div>
  </a>

  <!-- Newburyport Card -->
  <a href="/newburyport" style="flex: 1; min-width: 200px; max-width: 300px; text-decoration: none;">
    <div style="background: white; border-radius: 10px; overflow: hidden; box-shadow: 0 3px 8px rgba(0,0,0,.1);">
      <img src="/assets/images/towns/newburyport-thumb.jpg" alt="Newburyport" style="width: 100%; display: block;">
      <div style="padding: 15px; color: var(--text); text-align: center;">
        <h3>Newburyport</h3>
        <p>Shoreline resilience, public access, and regional coordination.</p>
      </div>
    </div>
  </a>

</div>

Past projects:

2024,2025 Salisbury Beach-DCR has received $1.75 million dollars to conduct a dune nourishment project from beach public access 5 to beach public access 11.  Permits filed through the Town of Salisbury.

2021 Newburyport Harbor dredging project to improve navigation. The project – was in the federal fiscal 2021 budget — moved sand from the Piscataqua River for placement near shore to protect the area from continuing erosion from major storms and waves.

2010 channel dredging

MRBA along with partner agencies working on coastal protection, environmental management, and public access.


## Get Involved
Residents, beach users, and community members are encouraged to follow our work, attend meetings, and share ideas. Visit our MRBA News page to sign up for updates.











