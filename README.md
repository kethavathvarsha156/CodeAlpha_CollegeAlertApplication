# CodeAlpha_CollegeAlertApplication

<h2 class="sr-only">College Alert Application — interactive prototype showing dashboard, events, and notifications</h2>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--font-sans)}
.app{display:flex;gap:0;border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);overflow:hidden;min-height:580px;background:var(--color-background-primary)}
.sidebar{width:200px;flex-shrink:0;background:var(--color-background-secondary);border-right:0.5px solid var(--color-border-tertiary);display:flex;flex-direction:column;padding:16px 0}
.sidebar-logo{padding:0 16px 20px;display:flex;align-items:center;gap:8px;border-bottom:0.5px solid var(--color-border-tertiary)}
.logo-icon{width:32px;height:32px;background:#185FA5;border-radius:8px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:16px}
.logo-text{font-size:14px;font-weight:500;color:var(--color-text-primary);line-height:1.2}
.logo-sub{font-size:11px;color:var(--color-text-secondary)}
.nav{padding:16px 0;flex:1}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 16px;cursor:pointer;font-size:13px;color:var(--color-text-secondary);border-left:2px solid transparent;transition:all .15s}
.nav-item:hover{background:var(--color-background-primary);color:var(--color-text-primary)}
.nav-item.active{color:#185FA5;background:var(--color-background-primary);border-left-color:#185FA5;font-weight:500}
.nav-item i{font-size:16px;width:18px;text-align:center}
.nav-badge{margin-left:auto;background:#E24B4A;color:#fff;font-size:10px;padding:2px 6px;border-radius:10px;font-weight:500}
.sidebar-footer{padding:12px 16px;border-top:0.5px solid var(--color-border-tertiary)}
.avatar{display:flex;align-items:center;gap:8px}
.avatar-circle{width:30px;height:30px;border-radius:50%;background:#B5D4F4;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:500;color:#0C447C}
.avatar-info p{font-size:12px;color:var(--color-text-primary);font-weight:500}
.avatar-info span{font-size:10px;color:var(--color-text-secondary)}
.main{flex:1;display:flex;flex-direction:column;min-width:0}
.topbar{padding:14px 20px;border-bottom:0.5px solid var(--color-border-tertiary);display:flex;align-items:center;justify-content:space-between}
.topbar-title{font-size:16px;font-weight:500;color:var(--color-text-primary)}
.topbar-sub{font-size:12px;color:var(--color-text-secondary);margin-top:1px}
.topbar-actions{display:flex;align-items:center;gap:8px}
.icon-btn{width:32px;height:32px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;cursor:pointer;display:flex;align-items:center;justify-content:center;color:var(--color-text-secondary);position:relative}
.icon-btn:hover{background:var(--color-background-secondary)}
.notif-dot{position:absolute;top:5px;right:5px;width:7px;height:7px;background:#E24B4A;border-radius:50%}
.content{flex:1;overflow-y:auto;padding:20px}
.page{display:none}
.page.active{display:block}
.stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:20px}
.stat-card{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:12px;text-align:center}
.stat-num{font-size:22px;font-weight:500;color:var(--color-text-primary)}
.stat-label{font-size:11px;color:var(--color-text-secondary);margin-top:2px}
.stat-card.blue .stat-num{color:#185FA5}
.stat-card.red .stat-num{color:#A32D2D}
.stat-card.green .stat-num{color:#3B6D11}
.stat-card.amber .stat-num{color:#854F0B}
.section-title{font-size:14px;font-weight:500;color:var(--color-text-primary);margin-bottom:12px;display:flex;align-items:center;justify-content:space-between}
.section-title a{font-size:12px;font-weight:400;color:#185FA5;cursor:pointer;text-decoration:none}
.events-list{display:flex;flex-direction:column;gap:8px}
.event-card{border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);padding:12px 14px;display:flex;align-items:flex-start;gap:12px;background:var(--color-background-primary)}
.event-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:5px}
.event-dot.exam{background:#E24B4A}
.event-dot.seminar{background:#185FA5}
.event-dot.fest{background:#3B6D11}
.event-dot.notice{background:#BA7517}
.event-info{flex:1;min-width:0}
.event-title{font-size:13px;font-weight:500;color:var(--color-text-primary)}
.event-meta{font-size:11px;color:var(--color-text-secondary);margin-top:3px;display:flex;align-items:center;gap:10px}
.event-meta i{font-size:12px;vertical-align:-1px}
.event-badge{font-size:10px;padding:2px 8px;border-radius:10px;font-weight:500;flex-shrink:0;margin-top:2px}
.badge-exam{background:#FCEBEB;color:#A32D2D}
.badge-seminar{background:#E6F1FB;color:#185FA5}
.badge-fest{background:#EAF3DE;color:#3B6D11}
.badge-notice{background:#FAEEDA;color:#854F0B}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:20px}
.notif-item{padding:10px 0;border-bottom:0.5px solid var(--color-border-tertiary);display:flex;gap:10px;align-items:flex-start}
.notif-item:last-child{border-bottom:none}
.notif-icon{width:32px;height:32px;border-radius:var(--border-radius-md);display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0}
.ni-exam{background:#FCEBEB;color:#A32D2D}
.ni-seminar{background:#E6F1FB;color:#185FA5}
.ni-fest{background:#EAF3DE;color:#3B6D11}
.ni-notice{background:#FAEEDA;color:#854F0B}
.notif-text p{font-size:12px;color:var(--color-text-primary);font-weight:500;line-height:1.4}
.notif-text span{font-size:11px;color:var(--color-text-secondary)}
.unread-dot{width:6px;height:6px;background:#185FA5;border-radius:50%;margin-top:6px;flex-shrink:0}
.add-btn{display:inline-flex;align-items:center;gap:6px;padding:7px 14px;background:#185FA5;color:#fff;border:none;border-radius:var(--border-radius-md);font-size:13px;cursor:pointer;font-weight:500}
.add-btn:hover{background:#0C447C}
.filter-row{display:flex;gap:6px;margin-bottom:14px;flex-wrap:wrap}
.filter-btn{padding:5px 12px;border:0.5px solid var(--color-border-secondary);border-radius:20px;font-size:12px;cursor:pointer;background:transparent;color:var(--color-text-secondary)}
.filter-btn.active{background:#185FA5;color:#fff;border-color:#185FA5}
.cat-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}
.cat-card{border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);padding:14px;cursor:pointer}
.cat-card:hover{border-color:var(--color-border-secondary)}
.cat-icon{width:36px;height:36px;border-radius:var(--border-radius-md);display:flex;align-items:center;justify-content:center;font-size:18px;margin-bottom:8px}
.cat-name{font-size:13px;font-weight:500;color:var(--color-text-primary)}
.cat-count{font-size:11px;color:var(--color-text-secondary);margin-top:2px}
.form-group{margin-bottom:14px}
.form-label{font-size:12px;color:var(--color-text-secondary);margin-bottom:5px;display:block}
.form-input{width:100%;padding:8px 10px;border:0.5px solid var(--color-border-secondary);border-radius:var(--border-radius-md);font-size:13px;background:var(--color-background-primary);color:var(--color-text-primary);outline:none}
.form-input:focus{border-color:#185FA5}
select.form-input option{background:var(--color-background-primary)}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.submit-btn{width:100%;padding:9px;background:#185FA5;color:#fff;border:none;border-radius:var(--border-radius-md);font-size:13px;font-weight:500;cursor:pointer;margin-top:4px}
.submit-btn:hover{background:#0C447C}
.success-toast{position:fixed;bottom:20px;right:20px;background:#185FA5;color:#fff;padding:10px 16px;border-radius:var(--border-radius-md);font-size:13px;display:none;z-index:99;align-items:center;gap:8px}
.upcoming-section h4{font-size:12px;font-weight:500;color:var(--color-text-secondary);text-transform:uppercase;letter-spacing:.05em;margin-bottom:8px}
.timeline-item{display:flex;gap:12px;padding:8px 0;border-bottom:0.5px solid var(--color-border-tertiary)}
.timeline-item:last-child{border-bottom:none}
.tl-date{width:38px;flex-shrink:0;text-align:center}
.tl-day{font-size:18px;font-weight:500;color:var(--color-text-primary);line-height:1}
.tl-mon{font-size:10px;color:var(--color-text-secondary)}
.tl-bar{width:3px;background:var(--color-border-tertiary);border-radius:2px;flex-shrink:0}
.tl-content p{font-size:13px;font-weight:500;color:var(--color-text-primary)}
.tl-content span{font-size:11px;color:var(--color-text-secondary)}
</style>

<div class="app">
  <div class="sidebar">
    <div class="sidebar-logo">
      <div class="logo-icon"><i class="ti ti-bell" aria-hidden="true"></i></div>
      <div>
        <div class="logo-text">CampusAlert</div>
        <div class="logo-sub">JNTU Hyderabad</div>
      </div>
    </div>
    <nav class="nav">
      <div class="nav-item active" onclick="showPage('dashboard',this)"><i class="ti ti-layout-dashboard" aria-hidden="true"></i> Dashboard</div>
      <div class="nav-item" onclick="showPage('events',this)"><i class="ti ti-calendar-event" aria-hidden="true"></i> Events <span class="nav-badge" id="evbadge">8</span></div>
      <div class="nav-item" onclick="showPage('notifications',this)"><i class="ti ti-bell" aria-hidden="true"></i> Notifications <span class="nav-badge" id="nbadge">3</span></div>
      <div class="nav-item" onclick="showPage('add',this)"><i class="ti ti-circle-plus" aria-hidden="true"></i> Add Event</div>
      <div class="nav-item" onclick="showPage('settings',this)"><i class="ti ti-settings" aria-hidden="true"></i> Settings</div>
    </nav>
    <div class="sidebar-footer">
      <div class="avatar">
        <div class="avatar-circle">RS</div>
        <div class="avatar-info"><p>Rahul S.</p><span>CSE — Sem 5</span></div>
      </div>
    </div>
  </div>

  <div class="main">
    <div class="topbar">
      <div>
        <div class="topbar-title" id="page-title">Dashboard</div>
        <div class="topbar-sub" id="page-sub">Wednesday, 20 May 2026</div>
      </div>
      <div class="topbar-actions">
        <button class="icon-btn" aria-label="Search"><i class="ti ti-search" aria-hidden="true"></i></button>
        <button class="icon-btn" aria-label="Notifications" onclick="showPage('notifications',null)">
          <i class="ti ti-bell" aria-hidden="true"></i>
          <span class="notif-dot" id="notif-dot"></span>
        </button>
      </div>
    </div>

    <div class="content">

      <div class="page active" id="page-dashboard">
        <div class="stats-grid">
          <div class="stat-card blue"><div class="stat-num">12</div><div class="stat-label">Upcoming events</div></div>
          <div class="stat-card red"><div class="stat-num">3</div><div class="stat-label">Exams this week</div></div>
          <div class="stat-card green"><div class="stat-num">2</div><div class="stat-label">Fests this month</div></div>
          <div class="stat-card amber"><div class="stat-num">5</div><div class="stat-label">Notices unread</div></div>
        </div>

        <div class="section-title">Today's alerts <a onclick="showPage('events',null)">View all →</a></div>
        <div class="events-list">
          <div class="event-card">
            <span class="event-dot exam"></span>
            <div class="event-info">
              <div class="event-title">Data Structures Mid-Semester Exam</div>
              <div class="event-meta"><i class="ti ti-clock" aria-hidden="true"></i> 9:00 AM &nbsp;·&nbsp; <i class="ti ti-map-pin" aria-hidden="true"></i> Block A, Hall 204</div>
            </div>
            <span class="event-badge badge-exam">Exam</span>
          </div>
          <div class="event-card">
            <span class="event-dot seminar"></span>
            <div class="event-info">
              <div class="event-title">IEEE Guest Lecture: AI in Healthcare</div>
              <div class="event-meta"><i class="ti ti-clock" aria-hidden="true"></i> 2:30 PM &nbsp;·&nbsp; <i class="ti ti-map-pin" aria-hidden="true"></i> Seminar Hall 1</div>
            </div>
            <span class="event-badge badge-seminar">Seminar</span>
          </div>
          <div class="event-card">
            <span class="event-dot notice"></span>
            <div class="event-info">
              <div class="event-title">Fee payment deadline extended to May 25</div>
              <div class="event-meta"><i class="ti ti-clock" aria-hidden="true"></i> All day &nbsp;·&nbsp; <i class="ti ti-user" aria-hidden="true"></i> Accounts Dept.</div>
            </div>
            <span class="event-badge badge-notice">Notice</span>
          </div>
        </div>

        <div class="two-col">
          <div>
            <div class="section-title">Categories</div>
            <div class="cat-grid">
              <div class="cat-card" onclick="filterAndShow('Exam')">
                <div class="cat-icon" style="background:#FCEBEB;color:#A32D2D"><i class="ti ti-writing" aria-hidden="true"></i></div>
                <div class="cat-name">Exams</div>
                <div class="cat-count">3 upcoming</div>
              </div>
              <div class="cat-card" onclick="filterAndShow('Seminar')">
                <div class="cat-icon" style="background:#E6F1FB;color:#185FA5"><i class="ti ti-presentation" aria-hidden="true"></i></div>
                <div class="cat-name">Seminars</div>
                <div class="cat-count">4 upcoming</div>
              </div>
              <div class="cat-card" onclick="filterAndShow('Fest')">
                <div class="cat-icon" style="background:#EAF3DE;color:#3B6D11"><i class="ti ti-confetti" aria-hidden="true"></i></div>
                <div class="cat-name">Fests</div>
                <div class="cat-count">2 upcoming</div>
              </div>
              <div class="cat-card" onclick="filterAndShow('Notice')">
                <div class="cat-icon" style="background:#FAEEDA;color:#854F0B"><i class="ti ti-info-circle" aria-hidden="true"></i></div>
                <div class="cat-name">Notices</div>
                <div class="cat-count">5 unread</div>
              </div>
            </div>
          </div>
          <div class="upcoming-section">
            <h4>Upcoming timeline</h4>
            <div class="timeline-item">
              <div class="tl-date"><div class="tl-day">21</div><div class="tl-mon">MAY</div></div>
              <div class="tl-bar" style="background:#E24B4A"></div>
              <div class="tl-content"><p>DBMS Lab Exam</p><span>10:00 AM · Lab 3</span></div>
            </div>
            <div class="timeline-item">
              <div class="tl-date"><div class="tl-day">23</div><div class="tl-mon">MAY</div></div>
              <div class="tl-bar" style="background:#3B6D11"></div>
              <div class="tl-content"><p>Techfest 2026 begins</p><span>All day · Main Ground</span></div>
            </div>
            <div class="timeline-item">
              <div class="tl-date"><div class="tl-day">25</div><div class="tl-mon">MAY</div></div>
              <div class="tl-bar" style="background:#185FA5"></div>
              <div class="tl-content"><p>Robotics Workshop</p><span>3:00 PM · Workshop Hall</span></div>
            </div>
            <div class="timeline-item">
              <div class="tl-date"><div class="tl-day">28</div><div class="tl-mon">MAY</div></div>
              <div class="tl-bar" style="background:#BA7517"></div>
              <div class="tl-content"><p>Sports Day Registration</p><span>Deadline · Online form</span></div>
            </div>
          </div>
        </div>
      </div>

      <div class="page" id="page-events">
        <div class="filter-row">
          <button class="filter-btn active" id="fAll" onclick="setFilter('All')">All</button>
          <button class="filter-btn" id="fExam" onclick="setFilter('Exam')">Exams</button>
          <button class="filter-btn" id="fSeminar" onclick="setFilter('Seminar')">Seminars</button>
          <button class="filter-btn" id="fFest" onclick="setFilter('Fest')">Fests</button>
          <button class="filter-btn" id="fNotice" onclick="setFilter('Notice')">Notices</button>
        </div>
        <div class="events-list" id="events-list"></div>
      </div>

      <div class="page" id="page-notifications">
        <div class="section-title">Recent notifications
          <a onclick="clearNotifs()">Mark all read</a>
        </div>
        <div id="notif-list">
          <div class="notif-item">
            <div class="notif-icon ni-exam"><i class="ti ti-writing" aria-hidden="true"></i></div>
            <div class="notif-text" style="flex:1"><p>Reminder: Data Structures exam in 1 hour</p><span>Today, 8:00 AM</span></div>
            <div class="unread-dot"></div>
          </div>
          <div class="notif-item">
            <div class="notif-icon ni-notice"><i class="ti ti-info-circle" aria-hidden="true"></i></div>
            <div class="notif-text" style="flex:1"><p>Fee payment deadline extended to May 25</p><span>Today, 7:30 AM</span></div>
            <div class="unread-dot"></div>
          </div>
          <div class="notif-item">
            <div class="notif-icon ni-seminar"><i class="ti ti-presentation" aria-hidden="true"></i></div>
            <div class="notif-text" style="flex:1"><p>IEEE Lecture: AI in Healthcare — seats limited</p><span>Yesterday, 6:00 PM</span></div>
            <div class="unread-dot"></div>
          </div>
          <div class="notif-item">
            <div class="notif-icon ni-fest"><i class="ti ti-confetti" aria-hidden="true"></i></div>
            <div class="notif-text" style="flex:1"><p>Techfest 2026 registrations now open!</p><span>19 May, 10:00 AM</span></div>
          </div>
          <div class="notif-item">
            <div class="notif-icon ni-exam"><i class="ti ti-writing" aria-hidden="true"></i></div>
            <div class="notif-text" style="flex:1"><p>DBMS Lab Exam scheduled for May 21</p><span>18 May, 3:00 PM</span></div>
          </div>
          <div class="notif-item">
            <div class="notif-icon ni-notice"><i class="ti ti-info-circle" aria-hidden="true"></i></div>
            <div class="notif-text" style="flex:1"><p>Library hours updated for exam season</p><span>17 May, 9:00 AM</span></div>
          </div>
        </div>
      </div>

      <div class="page" id="page-add">
        <div class="section-title">Add new event</div>
        <div style="border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:18px;background:var(--color-background-primary)">
          <div class="form-group">
            <label class="form-label">Event title</label>
            <input type="text" class="form-input" id="ev-title" placeholder="e.g. Operating Systems End-Sem Exam">
          </div>
          <div class="form-row">
            <div class="form-group">
              <label class="form-label">Category</label>
              <select class="form-input" id="ev-cat">
                <option value="Exam">Exam</option>
                <option value="Seminar">Seminar</option>
                <option value="Fest">Fest</option>
                <option value="Notice">Notice</option>
              </select>
            </div>
            <div class="form-group">
              <label class="form-label">Date</label>
              <input type="date" class="form-input" id="ev-date">
            </div>
          </div>
          <div class="form-row">
            <div class="form-group">
              <label class="form-label">Time</label>
              <input type="time" class="form-input" id="ev-time">
            </div>
            <div class="form-group">
              <label class="form-label">Location</label>
              <input type="text" class="form-input" id="ev-loc" placeholder="e.g. Block A, Hall 204">
            </div>
          </div>
          <div class="form-group">
            <label class="form-label">Description (optional)</label>
            <textarea class="form-input" id="ev-desc" rows="2" placeholder="Add more details about this event..."></textarea>
          </div>
          <div class="form-row">
            <div class="form-group">
              <label class="form-label">Notify</label>
              <select class="form-input" id="ev-notify">
                <option>1 hour before</option>
                <option>3 hours before</option>
                <option>1 day before</option>
                <option>At event time</option>
              </select>
            </div>
            <div class="form-group">
              <label class="form-label">Department</label>
              <select class="form-input" id="ev-dept">
                <option>All departments</option>
                <option>CSE</option>
                <option>ECE</option>
                <option>Mechanical</option>
                <option>Civil</option>
              </select>
            </div>
          </div>
          <button class="submit-btn" onclick="addEvent()">
            <i class="ti ti-circle-plus" aria-hidden="true"></i> Add event & send notification
          </button>
        </div>
      </div>

      <div class="page" id="page-settings">
        <div class="section-title">Notification preferences</div>
        <div style="border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:18px;background:var(--color-background-primary);margin-bottom:14px">
          <div style="display:flex;flex-direction:column;gap:14px" id="pref-list">
          </div>
        </div>
        <div class="section-title">Account</div>
        <div style="border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:18px;background:var(--color-background-primary)">
          <div class="form-group"><label class="form-label">Full name</label><input type="text" class="form-input" value="Rahul Sharma"></div>
          <div class="form-row">
            <div class="form-group"><label class="form-label">Roll number</label><input type="text" class="form-input" value="21B81A0511"></div>
            <div class="form-group"><label class="form-label">Branch</label><select class="form-input"><option>CSE</option><option>ECE</option><option>Mechanical</option></select></div>
          </div>
          <button class="submit-btn" style="background:var(--color-background-secondary);color:var(--color-text-primary);border:0.5px solid var(--color-border-secondary)">Save changes</button>
        </div>
      </div>

    </div>
  </div>
</div>

<div class="success-toast" id="toast"><i class="ti ti-check" aria-hidden="true"></i> <span id="toast-msg">Event added!</span></div>

<script>
const titles={dashboard:'Dashboard',events:'All Events',notifications:'Notifications',add:'Add Event',settings:'Settings'};
const subs={dashboard:'Wednesday, 20 May 2026',events:'Browse and filter campus events',notifications:'Stay up to date',add:'Create a new alert',settings:'Manage your preferences'};

let events=[
  {title:'Data Structures Mid-Sem Exam',cat:'Exam',date:'2026-05-20',time:'09:00',loc:'Block A, Hall 204'},
  {title:'IEEE Guest Lecture: AI in Healthcare',cat:'Seminar',date:'2026-05-20',time:'14:30',loc:'Seminar Hall 1'},
  {title:'Fee Payment Deadline Extended',cat:'Notice',date:'2026-05-20',time:'',loc:'Accounts Dept.'},
  {title:'DBMS Lab Exam',cat:'Exam',date:'2026-05-21',time:'10:00',loc:'Lab 3'},
  {title:'Techfest 2026 Opening Ceremony',cat:'Fest',date:'2026-05-23',time:'09:00',loc:'Main Ground'},
  {title:'Robotics Workshop by IEEE',cat:'Seminar',date:'2026-05-25',time:'15:00',loc:'Workshop Hall'},
  {title:'Sports Day Registration Deadline',cat:'Notice',date:'2026-05-28',time:'',loc:'Online'},
  {title:'Cultural Night — Techfest',cat:'Fest',date:'2026-05-24',time:'18:00',loc:'Open Air Theatre'},
];

let activeFilter='All';

function catDot(c){return c==='Exam'?'exam':c==='Seminar'?'seminar':c==='Fest'?'fest':'notice';}
function catBadge(c){return c==='Exam'?'badge-exam':c==='Seminar'?'badge-seminar':c==='Fest'?'badge-fest':'badge-notice';}

function renderEvents(){
  const list=document.getElementById('events-list');
  const filtered=activeFilter==='All'?events:events.filter(e=>e.cat===activeFilter);
  list.innerHTML=filtered.map(e=>`
    <div class="event-card">
      <span class="event-dot ${catDot(e.cat)}"></span>
      <div class="event-info">
        <div class="event-title">${e.title}</div>
        <div class="event-meta"><i class="ti ti-calendar-event" aria-hidden="true"></i> ${e.date}${e.time?' &nbsp;·&nbsp; <i class="ti ti-clock" aria-hidden="true"></i> '+e.time:''}&nbsp;·&nbsp;<i class="ti ti-map-pin" aria-hidden="true"></i> ${e.loc||'TBA'}</div>
      </div>
      <span class="event-badge ${catBadge(e.cat)}">${e.cat}</span>
    </div>`).join('');
  document.getElementById('evbadge').textContent=events.length;
}

function setFilter(f){
  activeFilter=f;
  ['All','Exam','Seminar','Fest','Notice'].forEach(x=>{
    document.getElementById('f'+x).classList.toggle('active',x===f);
  });
  renderEvents();
}

function filterAndShow(cat){
  showPage('events',null);
  document.querySelectorAll('.nav-item').forEach((el,i)=>{if(i===1)el.classList.add('active');else el.classList.remove('active');});
  setFilter(cat);
}

function showPage(id,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  document.getElementById('page-title').textContent=titles[id]||id;
  document.getElementById('page-sub').textContent=subs[id]||'';
  if(el){document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));el.classList.add('active');}
  if(id==='events')renderEvents();
  if(id==='notifications'){document.getElementById('nbadge').textContent='0';document.getElementById('notif-dot').style.display='none';}
}

function clearNotifs(){
  document.querySelectorAll('.unread-dot').forEach(d=>d.remove());
}

function addEvent(){
  const t=document.getElementById('ev-title').value.trim();
  if(!t){alert('Please enter an event title');return;}
  const cat=document.getElementById('ev-cat').value;
  const date=document.getElementById('ev-date').value||'2026-05-30';
  const time=document.getElementById('ev-time').value;
  const loc=document.getElementById('ev-loc').value||'TBA';
  events.unshift({title:t,cat,date,time,loc});
  document.getElementById('ev-title').value='';
  document.getElementById('ev-loc').value='';
  document.getElementById('ev-desc').value='';
  const toast=document.getElementById('toast');
  document.getElementById('toast-msg').textContent='Event added & notification scheduled!';
  toast.style.display='flex';
  setTimeout(()=>{toast.style.display='none';},2500);
  const nb=parseInt(document.getElementById('nbadge').textContent||0)+1;
  document.getElementById('nbadge').textContent=nb;
  document.getElementById('notif-dot').style.display='block';
}

const prefs=[
  {label:'Exam alerts',icon:'ti-writing',on:true,color:'#A32D2D',bg:'#FCEBEB'},
  {label:'Seminar alerts',icon:'ti-presentation',on:true,color:'#185FA5',bg:'#E6F1FB'},
  {label:'Fest alerts',icon:'ti-confetti',on:true,color:'#3B6D11',bg:'#EAF3DE'},
  {label:'Notice alerts',icon:'ti-info-circle',on:true,color:'#854F0B',bg:'#FAEEDA'},
  {label:'Push notifications',icon:'ti-bell',on:true,color:'#533AB7',bg:'#EEEDFE'},
];
function renderPrefs(){
  document.getElementById('pref-list').innerHTML=prefs.map((p,i)=>`
    <div style="display:flex;align-items:center;gap:12px">
      <div style="width:32px;height:32px;border-radius:var(--border-radius-md);background:${p.bg};color:${p.color};display:flex;align-items:center;justify-content:center;font-size:15px"><i class="ti ${p.icon}" aria-hidden="true"></i></div>
      <span style="flex:1;font-size:13px;color:var(--color-text-primary)">${p.label}</span>
      <div onclick="togglePref(${i})" style="width:38px;height:22px;border-radius:11px;background:${p.on?'#185FA5':'var(--color-border-secondary)'};cursor:pointer;position:relative;transition:background .2s">
        <div style="width:16px;height:16px;border-radius:50%;background:#fff;position:absolute;top:3px;left:${p.on?'19px':'3px'};transition:left .2s"></div>
      </div>
    </div>`).join('');
}
function togglePref(i){prefs[i].on=!prefs[i].on;renderPrefs();}
renderPrefs();

document.getElementById('ev-date').valueAsDate=new Date(Date.now()+3*86400000);
renderEvents();
</script>
