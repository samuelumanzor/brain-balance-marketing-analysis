[brain_balance_dashboard.html](https://github.com/user-attachments/files/28123775/brain_balance_dashboard.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Brain Balance — Marketing Analytics Dashboard</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Bricolage+Grotesque:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0c0f0a;
  --surface: #141810;
  --surface2: #1c2118;
  --border: #2a3325;
  --accent: #a8e063;
  --accent2: #f4a261;
  --accent3: #52b5f5;
  --accent4: #e76f51;
  --text: #e8f0e0;
  --muted: #6b7c5e;
  --mono: 'Space Mono', monospace;
  --sans: 'Bricolage Grotesque', sans-serif;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--sans);
  font-size: 14px;
  line-height: 1.6;
  min-height: 100vh;
}
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background:
    radial-gradient(ellipse 60% 40% at 20% 10%, rgba(168,224,99,0.06) 0%, transparent 60%),
    radial-gradient(ellipse 40% 50% at 80% 80%, rgba(82,181,245,0.04) 0%, transparent 60%);
  pointer-events: none;
  z-index: 0;
}

.wrap { position: relative; z-index: 1; max-width: 1120px; margin: 0 auto; padding: 40px 24px 80px; }

/* HEADER */
header { margin-bottom: 40px; display: flex; align-items: flex-start; justify-content: space-between; flex-wrap: wrap; gap: 20px; }
.header-left {}
.eyebrow { font-family: var(--mono); font-size: 10px; letter-spacing: 0.18em; text-transform: uppercase; color: var(--accent); margin-bottom: 12px; display: flex; align-items: center; gap: 8px; }
.eyebrow::before { content: ''; display: block; width: 24px; height: 1px; background: var(--accent); }
h1 { font-size: clamp(26px, 4vw, 42px); font-weight: 800; letter-spacing: -0.03em; line-height: 1.05; }
h1 em { color: var(--accent); font-style: normal; }
.header-meta { display: flex; gap: 20px; flex-wrap: wrap; margin-top: 16px; }
.meta-pill { font-family: var(--mono); font-size: 10px; color: var(--muted); border: 1px solid var(--border); border-radius: 20px; padding: 4px 12px; }
.meta-pill strong { color: var(--accent); }

/* TABS */
.tabs { display: flex; gap: 4px; margin-bottom: 32px; border-bottom: 1px solid var(--border); padding-bottom: 0; }
.tab {
  font-family: var(--mono); font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase;
  color: var(--muted); padding: 10px 20px; cursor: pointer; border-radius: 6px 6px 0 0;
  border: 1px solid transparent; border-bottom: none; transition: all 0.2s; position: relative; bottom: -1px;
  background: none;
}
.tab:hover { color: var(--text); }
.tab.active { color: var(--accent); border-color: var(--border); border-bottom-color: var(--bg); background: var(--bg); }

/* PANELS */
.panel { display: none; }
.panel.active { display: block; animation: fadeIn 0.3s ease; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: none; } }

/* KPI GRID */
.kpi-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 12px; margin-bottom: 28px; }
.kpi {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 18px 20px;
  position: relative; overflow: hidden;
}
.kpi::after { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: var(--kpi-c, var(--accent)); }
.kpi-label { font-family: var(--mono); font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
.kpi-value { font-size: 28px; font-weight: 800; letter-spacing: -0.04em; color: var(--kpi-c, var(--accent)); line-height: 1; margin-bottom: 4px; }
.kpi-sub { font-size: 11px; color: var(--muted); }

/* CHART BOXES */
.chart-box { background: var(--surface); border: 1px solid var(--border); border-radius: 8px; padding: 22px; margin-bottom: 16px; }
.chart-title { font-weight: 700; font-size: 14px; margin-bottom: 2px; }
.chart-sub { font-size: 11px; color: var(--muted); margin-bottom: 20px; }
.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
@media(max-width:640px) { .grid-2 { grid-template-columns: 1fr; } }
.grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
@media(max-width:700px) { .grid-3 { grid-template-columns: 1fr; } }

/* FUNNEL */
.funnel { display: flex; flex-direction: column; gap: 8px; }
.funnel-row { display: flex; align-items: center; gap: 12px; }
.funnel-name { font-family: var(--mono); font-size: 10px; width: 110px; flex-shrink: 0; color: var(--muted); }
.funnel-track { flex: 1; height: 34px; background: var(--surface2); border-radius: 4px; overflow: hidden; }
.funnel-fill {
  height: 100%; border-radius: 4px;
  display: flex; align-items: center; padding-left: 10px;
  font-family: var(--mono); font-size: 11px; font-weight: 700; color: #0c0f0a;
  transition: width 1.2s cubic-bezier(0.4,0,0.2,1);
}
.funnel-right { font-family: var(--mono); font-size: 11px; width: 110px; flex-shrink: 0; text-align: right; display: flex; justify-content: flex-end; gap: 12px; }
.funnel-n { color: var(--text); }
.funnel-p { color: var(--muted); }

/* BAR CHART */
.bar-list { display: flex; flex-direction: column; gap: 10px; }
.bar-row { display: flex; align-items: center; gap: 10px; }
.bar-label { font-size: 12px; width: 110px; flex-shrink: 0; color: var(--text); }
.bar-track { flex: 1; height: 26px; background: var(--surface2); border-radius: 3px; overflow: hidden; position: relative; }
.bar-fill {
  height: 100%; border-radius: 3px;
  display: flex; align-items: center; padding-left: 8px;
  font-family: var(--mono); font-size: 10px; color: #0c0f0a; font-weight: 700;
  transition: width 1.2s cubic-bezier(0.4,0,0.2,1);
}
.bar-val { font-family: var(--mono); font-size: 11px; width: 54px; text-align: right; flex-shrink: 0; }

/* REVENUE CHART */
.rev-wrap { display: flex; align-items: flex-end; gap: 6px; height: 140px; }
.rev-col { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 4px; height: 100%; }
.rev-bar-area { flex: 1; width: 100%; display: flex; align-items: flex-end; }
.rev-bar { width: 100%; border-radius: 3px 3px 0 0; transition: height 1.2s cubic-bezier(0.4,0,0.2,1); min-height: 2px; }
.rev-val { font-family: var(--mono); font-size: 8px; color: var(--text); text-align: center; }
.rev-lbl { font-family: var(--mono); font-size: 8px; color: var(--muted); text-align: center; }

/* DONUT */
.donut-wrap { display: flex; align-items: center; gap: 24px; flex-wrap: wrap; }
.donut-legend { display: flex; flex-direction: column; gap: 10px; }
.legend-item { display: flex; align-items: center; gap: 8px; font-size: 12px; }
.legend-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.legend-val { font-family: var(--mono); font-size: 11px; color: var(--muted); }

/* TABLE */
table { width: 100%; border-collapse: collapse; }
th { font-family: var(--mono); font-size: 9px; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); text-align: left; padding: 8px 10px; border-bottom: 1px solid var(--border); }
td { padding: 10px 10px; font-size: 12px; border-bottom: 1px solid rgba(255,255,255,0.03); }
tr:last-child td { border-bottom: none; }
tr:hover td { background: var(--surface2); }
.num { font-family: var(--mono); }
.pill { display: inline-block; padding: 2px 8px; border-radius: 20px; font-family: var(--mono); font-size: 10px; font-weight: 700; }
.pill-g { background: rgba(168,224,99,0.15); color: var(--accent); }
.pill-b { background: rgba(82,181,245,0.15); color: var(--accent3); }
.pill-r { background: rgba(231,111,81,0.15); color: var(--accent4); }

/* INSIGHT CARDS */
.insight-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 14px; margin-top: 20px; }
.insight { background: var(--surface); border: 1px solid var(--border); border-radius: 8px; padding: 18px; border-left: 3px solid var(--ic, var(--accent)); }
.insight-icon { font-size: 18px; margin-bottom: 8px; }
.insight-title { font-weight: 700; font-size: 13px; margin-bottom: 6px; }
.insight-body { font-size: 12px; color: var(--muted); line-height: 1.7; }
.hl { color: var(--text); font-weight: 600; }

/* MOM CHART */
.mom-wrap { display: flex; align-items: center; gap: 6px; flex-wrap: wrap; margin-top: 8px; }
.mom-item { display: flex; flex-direction: column; align-items: center; gap: 3px; }
.mom-arrow { font-size: 14px; font-weight: 700; }
.mom-val { font-family: var(--mono); font-size: 9px; }
.mom-lbl { font-family: var(--mono); font-size: 8px; color: var(--muted); }

/* SOURCE BUBBLE */
.bubble-chart { position: relative; height: 200px; background: var(--surface2); border-radius: 6px; overflow: hidden; }
.bubble {
  position: absolute;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  flex-direction: column;
  font-family: var(--mono);
  transition: all 0.3s;
  cursor: default;
}
.bubble:hover { filter: brightness(1.2); z-index: 10; }
.bubble-name { font-size: 9px; font-weight: 700; text-align: center; color: #0c0f0a; line-height: 1.2; }
.bubble-rate { font-size: 8px; color: rgba(0,0,0,0.6); }
</style>
</head>
<body>
<div class="wrap">

<header>
  <div class="header-left">
    <div class="eyebrow">Brain Balance · Marketing Ops</div>
    <h1>Lead Conversion<br><em>Analytics Dashboard</em></h1>
    <div class="header-meta">
      <span class="meta-pill">Inquiries: <strong>2,662</strong></span>
      <span class="meta-pill">Period: <strong>2024–2026</strong></span>
      <span class="meta-pill">Centers: <strong>SD · CV · EN</strong></span>
      <span class="meta-pill">Revenue: <strong>$491K</strong></span>
    </div>
  </div>
</header>

<div class="tabs">
  <button class="tab active" onclick="switchTab('overview')">Overview</button>
  <button class="tab" onclick="switchTab('sources')">Sources</button>
  <button class="tab" onclick="switchTab('revenue')">Revenue</button>
  <button class="tab" onclick="switchTab('centers')">Centers</button>
</div>

<!-- OVERVIEW -->
<div class="panel active" id="panel-overview">
  <div class="kpi-grid">
    <div class="kpi" style="--kpi-c:var(--accent)"><div class="kpi-label">Total Revenue</div><div class="kpi-value">$491K</div><div class="kpi-sub">Net payments collected</div></div>
    <div class="kpi" style="--kpi-c:var(--accent3)"><div class="kpi-label">Inquiry → Enroll</div><div class="kpi-value">~5%</div><div class="kpi-sub">Overall funnel rate</div></div>
    <div class="kpi" style="--kpi-c:#ffd166"><div class="kpi-label">Assess → Enroll</div><div class="kpi-value">30%</div><div class="kpi-sub">Once in, 1-in-3 enrolls</div></div>
    <div class="kpi" style="--kpi-c:var(--accent2)"><div class="kpi-label">Active Students</div><div class="kpi-value">46</div><div class="kpi-sub">SD:25 · CV:11 · EN:10</div></div>
    <div class="kpi" style="--kpi-c:var(--accent)"><div class="kpi-label">Cancel Rate</div><div class="kpi-value">1.1%</div><div class="kpi-sub">Retention is strong</div></div>
    <div class="kpi" style="--kpi-c:var(--accent4)"><div class="kpi-label">Avg Program</div><div class="kpi-value">62h</div><div class="kpi-sub">Range: 16–258h</div></div>
  </div>

  <div class="chart-box">
    <div class="chart-title">Sales Funnel — Where leads drop off</div>
    <div class="chart-sub">2,662 inquiries → 108 enrollments. Biggest drop: inquiry → booked assessment.</div>
    <div class="funnel" id="funnel"></div>
  </div>

  <div class="insight-grid">
    <div class="insight" style="--ic:var(--accent)">
      <div class="insight-icon">🎯</div>
      <div class="insight-title">Bottleneck is booking, not closing</div>
      <div class="insight-body">Once families come in for an assessment, <span class="hl">30% enroll</span>. The real problem is getting them through the door — inquiry → appointment conversion is only 13%.</div>
    </div>
    <div class="insight" style="--ic:var(--accent3)">
      <div class="insight-icon">📞</div>
      <div class="insight-title">Phone beats digital 2.5×</div>
      <div class="insight-body">Phone inquiries convert at <span class="hl">10.5%</span> vs digital at 4.2%. When someone calls, they're serious. Priority follow-up on phone leads pays off.</div>
    </div>
    <div class="insight" style="--ic:#ffd166">
      <div class="insight-icon">🤝</div>
      <div class="insight-title">Referrals are the #1 ROI channel</div>
      <div class="insight-body">Only 46 inquiries but <span class="hl">21.7% enroll</span> — 5× the average. A structured referral program would directly multiply the highest-converting lead type.</div>
    </div>
  </div>
</div>

<!-- SOURCES -->
<div class="panel" id="panel-sources">
  <div class="chart-box">
    <div class="chart-title">Enrollment rate by source</div>
    <div class="chart-sub">% of inquiries that become enrolled students — sorted by ROI</div>
    <div class="bar-list" id="enroll-bars"></div>
  </div>

  <div class="grid-2">
    <div class="chart-box">
      <div class="chart-title">Assessment rate by source</div>
      <div class="chart-sub">% of inquiries that book an assessment</div>
      <div class="bar-list" id="assess-bars"></div>
    </div>
    <div class="chart-box">
      <div class="chart-title">Volume vs. conversion efficiency</div>
      <div class="chart-sub">Bubble size = inquiry volume</div>
      <div class="bubble-chart" id="bubble-chart"></div>
    </div>
  </div>

  <div class="chart-box">
    <div class="chart-title">Full source breakdown</div>
    <div class="chart-sub">Sorted by enrollment rate — the metric that matters</div>
    <table>
      <thead><tr><th>Source</th><th>Inquiries</th><th>Assessments</th><th>Enrolled</th><th>Assess rate</th><th>Enroll rate</th><th>Signal</th></tr></thead>
      <tbody id="source-table"></tbody>
    </table>
  </div>
</div>

<!-- REVENUE -->
<div class="panel" id="panel-revenue">
  <div class="kpi-grid">
    <div class="kpi" style="--kpi-c:var(--accent)"><div class="kpi-label">Total Revenue</div><div class="kpi-value">$491K</div><div class="kpi-sub">Nov 2025 – May 2026</div></div>
    <div class="kpi" style="--kpi-c:#ffd166"><div class="kpi-label">Peak Month</div><div class="kpi-value">$107K</div><div class="kpi-sub">April 2026</div></div>
    <div class="kpi" style="--kpi-c:var(--accent3)"><div class="kpi-label">6-Month Growth</div><div class="kpi-value">+81%</div><div class="kpi-sub">Nov $59K → Apr $107K</div></div>
    <div class="kpi" style="--kpi-c:var(--accent2)"><div class="kpi-label">Avg Monthly</div><div class="kpi-value">$70K</div><div class="kpi-sub">Across active months</div></div>
  </div>

  <div class="chart-box">
    <div class="chart-title">Monthly net revenue</div>
    <div class="chart-sub">Paid collections only — April 2026 was the peak at $107K</div>
    <div class="rev-wrap" id="rev-chart"></div>
  </div>

  <div class="chart-box">
    <div class="chart-title">Month-over-month momentum</div>
    <div class="chart-sub">Revenue change between months</div>
    <div class="mom-wrap" id="mom-chart"></div>
  </div>

  <div class="insight-grid">
    <div class="insight" style="--ic:var(--accent)">
      <div class="insight-icon">📈</div>
      <div class="insight-title">Strong upward trajectory</div>
      <div class="insight-body">Revenue grew <span class="hl">+81% in 6 months</span> from $59K to $107K. The trend line is consistently positive with only one dip (Feb) that recovered strongly.</div>
    </div>
    <div class="insight" style="--ic:var(--accent2)">
      <div class="insight-icon">📉</div>
      <div class="insight-title">May is an outlier — not a drop</div>
      <div class="insight-body">May 2026 shows only $3.7K because the month was still in progress at time of analysis. <span class="hl">Not a revenue decline</span> — data is simply incomplete.</div>
    </div>
  </div>
</div>

<!-- CENTERS -->
<div class="panel" id="panel-centers">
  <div class="kpi-grid">
    <div class="kpi" style="--kpi-c:var(--accent3)"><div class="kpi-label">San Diego</div><div class="kpi-value">$261K</div><div class="kpi-sub">53% of total · 25 active</div></div>
    <div class="kpi" style="--kpi-c:var(--accent)"><div class="kpi-label">Chula Vista</div><div class="kpi-value">$121K</div><div class="kpi-sub">25% of total · 11 active</div></div>
    <div class="kpi" style="--kpi-c:var(--accent2)"><div class="kpi-label">Encinitas</div><div class="kpi-value">$109K</div><div class="kpi-sub">22% of total · 10 active</div></div>
  </div>

  <div class="grid-2">
    <div class="chart-box">
      <div class="chart-title">Revenue by center</div>
      <div class="chart-sub">Total net payments collected</div>
      <div class="bar-list" id="center-bars"></div>
    </div>
    <div class="chart-box">
      <div class="chart-title">Revenue share</div>
      <div class="chart-sub">San Diego drives the majority</div>
      <div class="donut-wrap" style="margin-top:12px">
        <canvas id="donut" width="140" height="140"></canvas>
        <div class="donut-legend">
          <div class="legend-item"><div class="legend-dot" style="background:var(--accent3)"></div><span>San Diego</span><span class="legend-val">53% · $261K</span></div>
          <div class="legend-item"><div class="legend-dot" style="background:var(--accent)"></div><span>Chula Vista</span><span class="legend-val">25% · $121K</span></div>
          <div class="legend-item"><div class="legend-dot" style="background:var(--accent2)"></div><span>Encinitas</span><span class="legend-val">22% · $109K</span></div>
        </div>
      </div>
    </div>
  </div>

  <div class="chart-box">
    <div class="chart-title">Staff performance comparison</div>
    <div class="chart-sub">Enroller effectiveness — completion rate is the key metric</div>
    <table>
      <thead><tr><th>Enroller</th><th>Enrollments</th><th>Avg Hours</th><th>Cancel Rate</th><th>Completion Rate</th><th>Assessment</th></tr></thead>
      <tbody>
        <tr><td><strong>JP</strong></td><td class="num">58</td><td class="num">61.7h</td><td><span class="pill pill-g">6.9%</span></td><td><span class="pill pill-g">84.5%</span></td><td style="color:var(--accent);font-size:11px">⭐ Best performer</td></tr>
        <tr><td><strong>LT</strong></td><td class="num">9</td><td class="num">66.7h</td><td><span class="pill pill-g">0.0%</span></td><td><span class="pill pill-b">77.8%</span></td><td style="color:var(--muted);font-size:11px">Small sample, strong</td></tr>
        <tr><td><strong>AL</strong></td><td class="num">104</td><td class="num">55.5h</td><td><span class="pill pill-r">9.6%</span></td><td><span class="pill pill-r">51.9%</span></td><td style="color:var(--muted);font-size:11px">High volume, lower completion</td></tr>
      </tbody>
    </table>
  </div>

  <div class="insight-grid">
    <div class="insight" style="--ic:var(--accent3)">
      <div class="insight-icon">🏆</div>
      <div class="insight-title">San Diego dominates revenue</div>
      <div class="insight-body">SD generates <span class="hl">$261K (53%)</span> of total revenue with 25 active students. Revenue per active student is higher than the other two centers.</div>
    </div>
    <div class="insight" style="--ic:var(--accent)">
      <div class="insight-icon">👤</div>
      <div class="insight-title">32-point completion gap worth closing</div>
      <div class="insight-body">JP completes <span class="hl">84.5%</span> of recommended hours vs AL at 51.9%. Documenting JP's enrollment conversation approach could lift program completion across all centers.</div>
    </div>
  </div>
</div>

</div><!-- end wrap -->

<script>
// DATA
const funnelData = [
  { label: 'Inquiries', n: 2662, pct: 100, color: '#52b5f5' },
  { label: 'Appt Set', n: 350, pct: 13.1, color: '#7ec8f7' },
  { label: 'Assessment', n: 381, pct: 14.3, color: '#a8e063' },
  { label: 'CNE Stage', n: 161, pct: 6.1, color: '#f4a261' },
  { label: 'Enrolled', n: 108, pct: 4.1, color: '#a8e063' },
];

const sourceData = [
  { src: 'Referrals', inq: 46, assess: 15, enroll: 10, assessRate: 32.6, enrollRate: 21.7 },
  { src: 'Phone In', inq: 133, assess: 52, enroll: 14, assessRate: 39.1, enrollRate: 10.5 },
  { src: 'Organic', inq: 136, assess: 29, enroll: 13, assessRate: 21.3, enrollRate: 9.6 },
  { src: 'Direct', inq: 161, assess: 32, enroll: 9, assessRate: 19.9, enrollRate: 5.6 },
  { src: 'Paid Search', inq: 339, assess: 54, enroll: 13, assessRate: 15.9, enrollRate: 3.8 },
  { src: 'Internet', inq: 1065, assess: 128, enroll: 41, assessRate: 12.0, enrollRate: 3.8 },
  { src: 'Paid Social', inq: 94, assess: 12, enroll: 3, assessRate: 12.8, enrollRate: 3.2 },
  { src: 'Events', inq: 517, assess: 19, enroll: 2, assessRate: 3.7, enrollRate: 0.4 },
];

const monthlyRev = [
  { m: 'Nov', v: 59274 },
  { m: 'Dec', v: 76147 },
  { m: 'Jan', v: 88752 },
  { m: 'Feb', v: 69920 },
  { m: 'Mar', v: 86521 },
  { m: 'Apr', v: 107213 },
  { m: 'May*', v: 3731 },
];

const centerData = [
  { name: 'San Diego', val: 261294, color: '#52b5f5' },
  { name: 'Chula Vista', val: 121033, color: '#a8e063' },
  { name: 'Encinitas', val: 109231, color: '#f4a261' },
];

// TAB SWITCHING
function switchTab(name) {
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('panel-' + name).classList.add('active');
  setTimeout(animateBars, 100);
}

// FUNNEL
function renderFunnel() {
  const el = document.getElementById('funnel');
  el.innerHTML = funnelData.map(d => `
    <div class="funnel-row">
      <div class="funnel-name">${d.label}</div>
      <div class="funnel-track">
        <div class="funnel-fill" style="width:0%;background:${d.color}" data-w="${d.pct}">
          ${d.n > 300 ? d.n.toLocaleString() : ''}
        </div>
      </div>
      <div class="funnel-right">
        <span class="funnel-n">${d.n.toLocaleString()}</span>
        <span class="funnel-p">${d.pct}%</span>
      </div>
    </div>
  `).join('');
}

// BAR LIST
function renderBarList(id, data, key, maxVal, color) {
  const el = document.getElementById(id);
  if (!el) return;
  el.innerHTML = data.map(d => {
    const pct = (d[key] / maxVal * 100).toFixed(1);
    const fmt = key.includes('Rate') ? d[key] + '%' : '$' + (d[key]/1000).toFixed(0) + 'K';
    return `
      <div class="bar-row">
        <div class="bar-label">${d.src || d.name}</div>
        <div class="bar-track">
          <div class="bar-fill" style="width:0%;background:${color}" data-w="${pct}">
            ${parseFloat(pct) > 20 ? fmt : ''}
          </div>
        </div>
        <div class="bar-val" style="color:${color}">${fmt}</div>
      </div>
    `;
  }).join('');
}

// CENTER BARS
function renderCenterBars() {
  const el = document.getElementById('center-bars');
  if (!el) return;
  const max = centerData[0].val;
  el.innerHTML = centerData.map(d => `
    <div class="bar-row">
      <div class="bar-label">${d.name}</div>
      <div class="bar-track">
        <div class="bar-fill" style="width:0%;background:${d.color}" data-w="${(d.val/max*100).toFixed(1)}"></div>
      </div>
      <div class="bar-val" style="color:${d.color}">$${(d.val/1000).toFixed(0)}K</div>
    </div>
  `).join('');
}

// REVENUE CHART
function renderRevChart() {
  const el = document.getElementById('rev-chart');
  if (!el) return;
  const active = monthlyRev.filter(m => m.v > 0);
  const max = Math.max(...active.map(m => m.v));
  el.innerHTML = monthlyRev.map(d => {
    const pct = d.v > 0 ? (d.v / max * 100) : 0;
    const isPeak = d.v === max;
    const color = isPeak ? '#a8e063' : d.v > 0 ? '#52b5f5' : '#1c2118';
    return `
      <div class="rev-col">
        <div class="rev-bar-area">
          <div class="rev-bar" style="height:0%;background:${color}" data-h="${pct.toFixed(1)}"></div>
        </div>
        ${d.v > 0 ? `<div class="rev-val">${isPeak ? '★' : ''}$${(d.v/1000).toFixed(0)}K</div>` : ''}
        <div class="rev-lbl">${d.m}</div>
      </div>
    `;
  }).join('');
}

// MOM CHART
function renderMom() {
  const el = document.getElementById('mom-chart');
  if (!el) return;
  const active = monthlyRev.filter(m => m.v > 1000);
  el.innerHTML = active.map((d, i) => {
    if (i === 0) return `<div class="mom-item"><div class="mom-arrow" style="color:var(--muted)">—</div><div class="mom-val" style="color:var(--muted)">base</div><div class="mom-lbl">${d.m}</div></div>`;
    const prev = active[i-1].v;
    const chg = ((d.v - prev) / prev * 100).toFixed(0);
    const up = d.v >= prev;
    return `
      <div class="mom-item">
        <div class="mom-arrow" style="color:${up ? 'var(--accent)' : 'var(--accent4)'}">${up ? '▲' : '▼'}</div>
        <div class="mom-val" style="color:${up ? 'var(--accent)' : 'var(--accent4)'}">${up ? '+' : ''}${chg}%</div>
        <div class="mom-lbl">${d.m}</div>
      </div>
    `;
  }).join('');
}

// SOURCE TABLE
function renderSourceTable() {
  const tbody = document.getElementById('source-table');
  if (!tbody) return;
  const sorted = [...sourceData].sort((a, b) => b.enrollRate - a.enrollRate);
  tbody.innerHTML = sorted.map(d => {
    const pill = d.enrollRate >= 10 ? 'pill-g' : d.enrollRate >= 4 ? 'pill-b' : 'pill-r';
    const sig = d.enrollRate >= 10 ? '🔥 High ROI' : d.enrollRate >= 4 ? '⚡ Moderate' : '⚠️ Low ROI';
    return `<tr>
      <td><strong>${d.src}</strong></td>
      <td class="num">${d.inq.toLocaleString()}</td>
      <td class="num">${d.assess}</td>
      <td class="num">${d.enroll}</td>
      <td class="num">${d.assessRate}%</td>
      <td><span class="pill ${pill}">${d.enrollRate}%</span></td>
      <td style="font-size:11px;color:var(--muted)">${sig}</td>
    </tr>`;
  }).join('');
}

// BUBBLE CHART
function renderBubble() {
  const el = document.getElementById('bubble-chart');
  if (!el) return;
  const maxInq = Math.max(...sourceData.map(d => d.inq));
  const colors = ['#a8e063','#52b5f5','#f4a261','#e76f51','#ffd166','#90e0ef','#b7e4c7','#ffb4a2'];
  const positions = [
    [15,20],[35,55],[55,20],[70,60],[20,70],[50,45],[75,25],[85,65]
  ];
  el.innerHTML = sourceData.map((d, i) => {
    const size = Math.max(30, Math.sqrt(d.inq / maxInq) * 90);
    const [lp, tp] = positions[i];
    return `
      <div class="bubble" style="
        width:${size}px;height:${size}px;
        left:${lp}%;top:${tp}%;
        transform:translate(-50%,-50%);
        background:${colors[i]};
        opacity:0.85;
      " title="${d.src}: ${d.inq} inquiries, ${d.enrollRate}% enroll">
        <span class="bubble-name">${d.src.split(' ')[0]}</span>
        <span class="bubble-rate">${d.enrollRate}%</span>
      </div>
    `;
  }).join('');
}

// DONUT CANVAS
function renderDonut() {
  const canvas = document.getElementById('donut');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  const data = [53, 25, 22];
  const colors = ['#52b5f5', '#a8e063', '#f4a261'];
  let start = -Math.PI / 2;
  const cx = 70, cy = 70, r = 55, inner = 32;
  ctx.clearRect(0, 0, 140, 140);
  data.forEach((val, i) => {
    const angle = (val / 100) * Math.PI * 2;
    ctx.beginPath();
    ctx.moveTo(cx, cy);
    ctx.arc(cx, cy, r, start, start + angle);
    ctx.closePath();
    ctx.fillStyle = colors[i];
    ctx.fill();
    start += angle;
  });
  ctx.beginPath();
  ctx.arc(cx, cy, inner, 0, Math.PI * 2);
  ctx.fillStyle = '#141810';
  ctx.fill();
  ctx.fillStyle = '#e8f0e0';
  ctx.font = 'bold 14px Bricolage Grotesque, sans-serif';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.fillText('$491K', cx, cy);
}

// ANIMATE BARS
function animateBars() {
  document.querySelectorAll('.bar-fill[data-w], .funnel-fill[data-w]').forEach(b => {
    b.style.width = b.dataset.w + '%';
  });
  document.querySelectorAll('.rev-bar[data-h]').forEach(b => {
    b.style.height = b.dataset.h + '%';
  });
}

// INIT
renderFunnel();
renderBarList('enroll-bars', sourceData, 'enrollRate', 21.7, '#a8e063');
renderBarList('assess-bars', sourceData, 'assessRate', 39.1, '#52b5f5');
renderBarList('center-bars', centerData, 'val', 261294, '#52b5f5');
renderCenterBars();
renderRevChart();
renderMom();
renderSourceTable();
renderBubble();
renderDonut();
setTimeout(animateBars, 300);
</script>
</body>
</html>
