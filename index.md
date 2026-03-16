---
layout: default
title: Page Title
---
# Merrimack River Beach Alliance (MRBA)

Welcome to the Merrimack River Beach Alliance — a regional partnership of Salisbury, Newbury, and Newburyport working together with state and federal agencies to protect, improve, and enhance the beaches and shoreline along the Merrimack River and surrounding coast.

Our beaches are a shared resource. They support local communities, tourism, wildlife habitat, and coastal resilience. By working together across town boundaries, we can make smarter investments, plan for the future, and create a safer, more accessible shoreline for everyone.

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

<div style="display:flex; gap:40px; align-items:flex-start; flex-wrap:wrap;">

  <!-- MAIN CONTENT (LEFT) -->
  <div style="flex:2; min-width:280px;">
    <p>
      Stay informed about upcoming MRBA public meetings.  
      Click highlighted dates to view details.
    </p>
  </div>

  <!-- CALENDAR (RIGHT SIDEBAR) -->
  <div style="flex:1; min-width:260px; max-width:320px;">

    <style>
    :root{
       --ocean-dark: #0b3c5d;
        --ocean: #1f6f8b;
        --ocean-light: #e6f3f7;
        --sand: #f7f9fb;
        --text: #1f2d3d;
    }
    .mini-cal{
      border:1px solid var(--gray);
      border-radius:10px;
      overflow:hidden;
      background:var(--white);
      font-family:Arial, sans-serif;
      font-size:14px;
    }
    .mini-cal-header{
      background:linear-gradient(135deg,var(--ocean-dark),var(--ocean));
      color:white;
      padding:10px;
      display:flex;
      justify-content:space-between;
      align-items:center;
    }
    .mini-cal-header button{
      background:white;
      color:var(--ocean-dark);
      border:none;
      padding:2px 6px;
      border-radius:4px;
      cursor:pointer;
      font-weight:bold;
    }
    .mini-month{ font-weight:bold; }
    .mini-days,.mini-dates{
      display:grid;
      grid-template-columns:repeat(7,1fr);
      text-align:center;
    }
    .mini-days{
      background:var(--ocean-light);
      font-weight:bold;
      padding:4px 0;
      font-size:12px;
    }
    .mini-dates div{
      padding:6px 0;
      border:1px solid #f5f5f5;
      min-height:28px;
    }
    .mini-today{
      background:var(--ocean-light);
      border:1px solid var(--ocean);
    }
    .mini-meeting{
      background:#e8f5e9;
      cursor:pointer;
    }
    .mini-dot{
      width:5px;height:5px;
      background:var(--ocean);
      border-radius:50%;
      margin:2px auto 0;
    }
    </style>

    <div class="mini-cal">
      <div class="mini-cal-header">
        <button onclick="miniChangeMonth(-1)">◀</button>
        <div class="mini-month" id="miniMonth"></div>
        <button onclick="miniChangeMonth(1)">▶</button>
      </div>

      <div class="mini-days">
        <div>S</div><div>M</div><div>T</div><div>W</div>
        <div>T</div><div>F</div><div>S</div>
      </div>

      <div class="mini-dates" id="miniDates"></div>
    </div>

  </div>
</div>

<script>
const miniMeetings = {
  "2026-03-18":[{title:"MRBA Board Meeting"}],
  "2026-04-02":[{title:"Coastal Planning Session"}]
};

const miniMonth = document.getElementById("miniMonth");
const miniDates = document.getElementById("miniDates");
let miniDate = new Date();

function miniKey(y,m,d){
  return `${y}-${String(m+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
}

function miniRender(date){
  const y=date.getFullYear();
  const m=date.getMonth();
  const first=new Date(y,m,1).getDay();
  const last=new Date(y,m+1,0).getDate();

  miniMonth.textContent=date.toLocaleString('default',{month:'short',year:'numeric'});
  miniDates.innerHTML="";

  for(let i=0;i<first;i++){ miniDates.innerHTML+="<div></div>"; }

  for(let d=1; d<=last; d++){
    const div=document.createElement("div");
    div.textContent=d;

    const today=new Date();
    if(d===today.getDate() && m===today.getMonth() && y===today.getFullYear()){
      div.classList.add("mini-today");
    }

    const key=miniKey(y,m,d);
    if(miniMeetings[key]){
      div.classList.add("mini-meeting");
      const dot=document.createElement("div");
      dot.className="mini-dot";
      div.appendChild(dot);
    }

    miniDates.appendChild(div);
  }
}

function miniChangeMonth(o){
  miniDate.setMonth(miniDate.getMonth()+o);
  miniRender(miniDate);
}

miniRender(miniDate);
</script>






