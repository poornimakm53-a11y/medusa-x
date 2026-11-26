<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MEDUSA-X | Agentic Clinical Intelligence</title>
<link rel="stylesheet" href="css/styles.css">
</head>
<body>

<!-- ══════════════════════════════════════════════════════════
     PAGE 1 — LOGIN
══════════════════════════════════════════════════════════ -->
<div id="loginPage" class="page active">
  <div class="login-box">
    <div class="login-brand">
      <div class="login-logo">✚</div>
      <h1>MEDUSA-X</h1>
      <p>AGENTIC CLINICAL INTELLIGENCE</p>
    </div>
    <div id="backendStatusBanner" class="backend-banner offline" style="display:none">
      Backend API is offline. Start it with <code>start_backend.bat</code> or <code>python backend/app.py</code>.
    </div>
    <div id="loginErr" class="login-err">Invalid username or password. Please try again.</div>
    <div class="login-form">
      <div class="login-field">
        <label for="loginUser">USERNAME</label>
        <input id="loginUser" type="text" placeholder="Enter your username" autocomplete="username">
      </div>
      <div class="login-field">
        <label for="loginPass">PASSWORD</label>
        <input id="loginPass" type="password" placeholder="Enter your password" autocomplete="current-password">
      </div>
      <button class="login-btn" type="button" onclick="doLogin()">Sign In to Clinical Workspace</button>
    </div>
    <div class="login-hint">
      <p>Demo credentials:<br><strong>Username: Electroforge &nbsp;|&nbsp; Password: @2016</strong></p>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════════
     PAGE 2 — APP SHELL
══════════════════════════════════════════════════════════ -->
<div id="appShell" class="page">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="brand">
      <div class="logo">✚</div>
      <div><strong>MEDUSA-X</strong><br><small>CLINICAL INTELLIGENCE</small></div>
    </div>
    <div class="nav-label">WORKSPACE</div>
    <nav class="nav" id="sideNav">
      <a data-page="pgDashboard" class="active" onclick="showPage('pgDashboard',this)">▦ &nbsp; Dashboard</a>
      <a data-page="pgAgent"     onclick="showPage('pgAgent',this)">✦ &nbsp; Agentic Analysis</a>
      <a data-page="pgPatient"   onclick="showPage('pgPatient',this)">♙ &nbsp; Patient Overview</a>
      <a data-page="pgAdd"       onclick="showPage('pgAdd',this)">＋ &nbsp; Add Patient Data</a>
      <a data-page="pgRecords"   onclick="showPage('pgRecords',this)">▤ &nbsp; Medical Records</a>
      <a data-page="pgSafety"    onclick="showPage('pgSafety',this)">⚕ &nbsp; Safety Review</a>
    </nav>
    <div class="side-bottom">
      Agentic Clinical Intelligence<br>
      Backend API · Dataset storage<br>
      <div id="dbBadge" class="db-badge">0 records saved</div>
      <button class="logout-btn reset-btn" type="button" onclick="resetDemoDataset()">↻ &nbsp; Restore Demo Dataset</button>
      <button class="logout-btn" type="button" onclick="doLogout()">⬡ &nbsp; Sign Out</button>
      <button class="logout-btn clear-btn" type="button" onclick="clearAllData()">🗑 &nbsp; Clear All Data</button>
    </div>
  </aside>

  <!-- MAIN -->
  <main class="main">
    <header class="topbar">
      <div class="breadcrumb">Workspace / <b id="breadcrumbLabel">Clinical Dashboard</b></div>
      <div class="profile">
        <div class="avatar" id="userAvatar">EF</div>
        <div><b id="userDisplayName">Electroforge</b><br><span class="profile-sub">MEDUSA-X</span></div>
      </div>
    </header>

    <!-- ── DASHBOARD PAGE ─────────────────────────── -->
    <section id="pgDashboard" class="inner-page active">
      <div class="heading">
        <div>
          <div class="eyebrow">AGENTIC PATIENT ANALYTICS</div>
          <h1>Clinical Dashboard</h1>
          <div class="sub">Overview of fragmented clinical records, agentic reconciliation, and stop-gate escalations.</div>
        </div>
        <div class="sub" id="today"></div>
      </div>

      <div class="stats-grid">
        <div class="stat-card stat">
          <div class="stat-top">Total Records <div class="stat-icon">▤</div></div>
          <strong id="dTotalRecords">0</strong>
          <small>Scattered clinical documents</small>
        </div>
        <div class="stat-card stat">
          <div class="stat-top">Patients Analyzed <div class="stat-icon">♙</div></div>
          <strong id="dPatientCount">0</strong>
          <small>Unique reconstructed timelines</small>
        </div>
        <div class="stat-card stat">
          <div class="stat-top">Stop &amp; Escalate <div class="stat-icon icon-red">🛑</div></div>
          <strong id="dStopCount">0</strong>
          <small>Blocked by uncertainty gate</small>
        </div>
        <div class="stat-card stat">
          <div class="stat-top">Safe to Conclude <div class="stat-icon icon-green">✔</div></div>
          <strong id="dConcludeCount">0</strong>
          <small>Verified consistent records</small>
        </div>
      </div>

      <div class="section-label">QUICK ACTIONS</div>
      <div class="quick-actions">
        <button class="qa-btn" type="button" onclick="showPage('pgAgent',null)">
          <div class="qa-icon qa-purple">✦</div>
          <div><h4>Agentic Clinical Analysis</h4><p>Reconstruct timelines, reconcile conflicts &amp; check Stop-Gate</p></div>
        </button>
        <button class="qa-btn" type="button" onclick="showPage('pgPatient',null)">
          <div class="qa-icon qa-blue">♙</div>
          <div><h4>Patient Overview</h4><p>View detailed patient profile &amp; chronological timeline</p></div>
        </button>
        <button class="qa-btn" type="button" onclick="showPage('pgAdd',null)">
          <div class="qa-icon qa-green">＋</div>
          <div><h4>Add Patient Data</h4><p>Submit admission notes, labs, prescriptions or progress notes</p></div>
        </button>
        <button class="qa-btn" type="button" onclick="showPage('pgSafety',null)">
          <div class="qa-icon qa-red">⚕</div>
          <div><h4>Safety Review</h4><p>Documentation completeness &amp; cross-record flags</p></div>
        </button>
      </div>

      <div class="section-grid">
        <div class="card">
          <div class="panel-head"><h3>Agentic Stop-Gate Queue</h3><small>UNCERTAINTY &amp; ESCALATIONS</small></div>
          <div id="dGateQueue"></div>
        </div>
        <div class="card">
          <div class="panel-head"><h3>Recent Patient Records</h3><small>LATEST ENTRIES</small></div>
          <div id="dRecentList"></div>
        </div>
      </div>

      <div class="footer">MEDUSA-X Clinical Intelligence · Knows what it can conclude, what it cannot, and when it must stop</div>
    </section>

    <!-- ── AGENTIC CLINICAL ANALYSIS PAGE ─────────── -->
    <section id="pgAgent" class="inner-page">
      <div class="heading">
        <div>
          <div class="eyebrow">AUTONOMOUS RECONSTRUCTION &amp; VERIFICATION</div>
          <h1>Agentic Clinical Intelligence</h1>
          <div class="sub">Retrieves scattered records, reconstructs timelines, reconciles medications &amp; diagnoses, and halts when uncertainty is too high.</div>
        </div>
        <button class="btn primary" type="button" onclick="runAgenticAnalysis()">↻ Re-run Agentic Pipeline</button>
      </div>

      <div class="select-row">
        <label for="agentPatientSelector">SELECT PATIENT TO ANALYZE:</label>
        <select id="agentPatientSelector" onchange="runAgenticAnalysis()">
          <option value="">— Select a patient —</option>
        </select>
      </div>

      <div id="agentEmptyState" class="empty-state card">
        <div class="es-icon">✦</div>
        <h3>No patient selected</h3>
        <p>Select a patient above to run autonomous record retrieval, timeline reconstruction, medical reconciliation, and stop-gate verification.</p>
      </div>

      <div id="agentContent" style="display:none">
        <!-- Stop-Gate Decision Hero -->
        <div id="agentGateBanner" class="gate-banner gate-stop">
          <div class="gate-main">
            <div class="gate-pill" id="agentGatePill">STOP &amp; ESCALATE</div>
            <h2 id="agentGateLabel">—</h2>
            <p id="agentGateSub">—</p>
          </div>
          <div class="gate-metrics">
            <div class="gm-box">
              <span>CONFIDENCE</span>
              <strong id="agentConfidence">—</strong>
            </div>
            <div class="gm-box">
              <span>UNCERTAINTY</span>
              <strong id="agentUncertainty">—</strong>
            </div>
            <div class="gm-box">
              <span>COMPLETENESS</span>
              <strong id="agentCompleteness">—</strong>
            </div>
          </div>
        </div>

        <!-- 3-Column Epistemic Boundaries -->
        <div class="epistemic-grid">
          <div class="card ep-card ep-can">
            <div class="panel-head"><h3>✔ What System Can Conclude</h3><small>VERIFIED EVIDENCE</small></div>
            <div id="agentCanConclude"></div>
          </div>
          <div class="card ep-card ep-cannot">
            <div class="panel-head"><h3>❓ What It Cannot Conclude</h3><small>NEVER ASSUMED</small></div>
            <div id="agentCannotConclude"></div>
          </div>
          <div class="card ep-card ep-stop">
            <div class="panel-head"><h3>🛑 Escalated Issues</h3><small>STOP TRIGGERS</small></div>
            <div id="agentEscalations"></div>
          </div>
        </div>

        <!-- Structured Summary -->
        <div class="card" style="margin-bottom:18px">
          <div class="panel-head">
            <h3>Structured Clinical Summary</h3>
            <small id="agentSummaryStatus">—</small>
          </div>
          <div id="agentSummaryBody"></div>
        </div>

        <!-- Medication & Diagnosis Reconciliation -->
        <div class="section-grid">
          <div class="card">
            <div class="panel-head"><h3>Medication Reconciliation</h3><small>CROSS-RECORD TRACKING</small></div>
            <div id="agentMedRecon"></div>
          </div>
          <div class="card">
            <div class="panel-head"><h3>Diagnosis Reconciliation</h3><small>CONFLICT DETECTION</small></div>
            <div id="agentDiagRecon"></div>
          </div>
        </div>

        <!-- Reconstructed Timeline & Agent Reasoning Trace -->
        <div class="section-grid">
          <div class="card">
            <div class="panel-head"><h3>Reconstructed Patient Timeline</h3><small>SCATTERED SOURCES</small></div>
            <div id="agentTimeline"></div>
          </div>
          <div class="card">
            <div class="panel-head"><h3>Autonomous Agent Reasoning Trace</h3><small>ADAPTIVE PIPELINE</small></div>
            <div id="agentTrace"></div>
          </div>
        </div>
      </div>

      <div class="footer">MEDUSA-X Agentic Engine · Citations link every claim to source record [R# · Date · Document Type]</div>
    </section>

    <!-- ── PATIENT OVERVIEW PAGE ──────────────────── -->
    <section id="pgPatient" class="inner-page">
      <div class="heading">
        <div>
          <div class="eyebrow">CLINICAL PROFILE</div>
          <h1>Patient Overview</h1>
          <div class="sub">Select a patient to view their full clinical profile and record history.</div>
        </div>
      </div>

      <div class="select-row">
        <label for="patientSelector">SELECT PATIENT:</label>
        <select id="patientSelector" onchange="loadPatientProfile()">
          <option value="">— Select a patient —</option>
        </select>
      </div>

      <div id="patientBannerWrap">
        <div class="empty-state card" id="patientEmptyState">
          <div class="es-icon">♙</div>
          <h3>No patient selected</h3>
          <p>Select a patient from the dropdown above, or add a patient record first.</p>
        </div>
      </div>

      <div id="patientProfileContent" style="display:none">
        <div class="patient-banner">
          <div class="patient-left">
            <div class="patient-avatar">♙</div>
            <div>
              <h2 id="ovPatientName">—</h2>
              <p>Patient profile · ID <span id="ovPatientId">—</span></p>
            </div>
          </div>
          <div class="patient-meta">
            <div class="meta"><label>PATIENT ID</label><strong id="ovPatientIdMeta">—</strong></div>
            <div class="meta"><label>TOTAL RECORDS</label><strong id="ovTotalRec">0</strong></div>
            <div class="meta"><label>LATEST RECORD</label><strong id="ovLatestDate">—</strong></div>
            <button class="btn primary" type="button" onclick="openSelectedPatientInAgent()">✦ Run Agentic Analysis</button>
          </div>
        </div>

        <div class="section-grid">
          <div class="card">
            <div class="panel-head"><h3>Patient Information Summary</h3><small>LATEST RECORD</small></div>
            <div id="ovInfoRows"></div>
          </div>
          <div class="card">
            <div class="panel-head"><h3>Record Timeline</h3><small>CHRONOLOGICAL</small></div>
            <div id="ovTimeline"></div>
          </div>
        </div>
      </div>

      <div class="footer">MEDUSA-X · Backend dataset storage · Not a diagnostic system</div>
    </section>

    <!-- ── ADD PATIENT DATA PAGE ──────────────────── -->
    <section id="pgAdd" class="inner-page">
      <div class="heading">
        <div>
          <div class="eyebrow">DATA ENTRY</div>
          <h1>Add Patient Data</h1>
          <div class="sub">Submit a clinical document from any care source to test reconstruction and reconciliation.</div>
        </div>
      </div>

      <div id="addSuccessBanner" class="success-banner">
        <span>✔</span> Patient record saved to backend dataset. Inspect it in Agentic Analysis or Medical Records.
      </div>
      <div id="addErrorBanner" class="error-banner" style="display:none"></div>

      <div class="form-card">
        <div class="panel-head">
          <h3>＋ Patient Information Form</h3>
          <small>DATA ENTRY FORM</small>
        </div>
        <form id="patientForm">
          <div class="fields">
            <div class="field"><label for="pname">Patient Name *</label><input id="pname" required placeholder="Enter patient name"></div>
            <div class="field"><label for="pid">Patient ID *</label><input id="pid" required placeholder="e.g. P005"></div>
            <div class="field"><label for="pmobile">Mobile Number *</label><input id="pmobile" required type="tel" placeholder="e.g. 9876543210" pattern="[0-9+\-\s]{7,15}"></div>
            <div class="field"><label for="recDate">Record Date *</label><input id="recDate" type="date" required></div>
            <div class="field"><label for="doc">Document Type *</label>
              <select id="doc" required>
                <option value="">Select document type</option>
                <option>Admission Note</option>
                <option>Lab Report</option>
                <option>Prescription</option>
                <option>Progress Note</option>
                <option>Discharge Summary</option>
                <option>Follow-up Note</option>
                <option>Other</option>
              </select>
            </div>
            <div class="field full"><label for="title">Document Title *</label><input id="title" required placeholder="e.g. Cardiology Progress Note"></div>
            <div class="field full"><label for="symptoms">Symptoms / Patient-reported concerns</label><textarea id="symptoms" placeholder="Enter symptoms reported by the patient"></textarea></div>
            <div class="field full"><label for="diagnosis">Diagnosis / Clinical assessment</label><textarea id="diagnosis" placeholder="Enter documented diagnosis or assessment; do not infer"></textarea></div>
            <div class="field full"><label for="medications">Medications</label><textarea id="medications" placeholder="Enter documented medications separated by semicolons, e.g. Metformin 500 mg PO BD; Aspirin 75 mg OD"></textarea></div>
            <div class="field"><label for="allergies">Allergy information *</label>
              <select id="allergies" required>
                <option value="Not documented">Not documented / Unknown</option>
                <option value="No known allergies documented">No known allergies documented</option>
                <option value="Allergy reported">Allergy reported</option>
              </select>
            </div>
            <div class="field"><label for="allergyDetails">Allergy details</label><input id="allergyDetails" placeholder="Name of allergy, if reported (e.g. Penicillin)"></div>
            <div class="field full"><label for="notes">Clinical Notes / Lab Findings</label><textarea id="notes" placeholder="Additional clinical notes, lab values, or pending/delayed test notices"></textarea></div>
          </div>
          <div class="form-actions">
            <button class="btn primary" type="submit">Add Patient Record</button>
            <button class="btn secondary" type="reset" onclick="resetAddForm()">Clear Form</button>
          </div>
          <div class="notice">* Required fields. <strong style="color:#3978f6">✔ Data is persisted by the Python backend into <code>dataset/clinical_records.json</code> and <code>dataset/clinical_records.csv</code></strong>. Use verified clinical documentation; MEDUSA-X flags uncertainty rather than inventing missing details.</div>
        </form>
      </div>
      <div class="footer">MEDUSA-X · Enter only verified clinical information · Not a diagnostic system</div>
    </section>

    <!-- ── MEDICAL RECORDS PAGE ───────────────────── -->
    <section id="pgRecords" class="inner-page">
      <div class="heading">
        <div>
          <div class="eyebrow">RECORDS DATABASE</div>
          <h1>Medical Records</h1>
          <div class="sub">Browse, filter, search, and export all fragmented clinical records.</div>
        </div>
        <button class="btn secondary" type="button" onclick="exportDatasetCsv()">⬇ Export CSV</button>
      </div>

      <div class="filter-row">
        <span class="filter-label">FILTER:</span>
        <button class="filter-btn active" type="button" onclick="filterRecords('all',this)">All Records</button>
        <button class="filter-btn" type="button" onclick="filterRecords('Admission Note',this)">Admission Notes</button>
        <button class="filter-btn" type="button" onclick="filterRecords('Lab Report',this)">Lab Reports</button>
        <button class="filter-btn" type="button" onclick="filterRecords('Prescription',this)">Prescriptions</button>
        <button class="filter-btn" type="button" onclick="filterRecords('Progress Note',this)">Progress Notes</button>
        <button class="filter-btn" type="button" onclick="filterRecords('Discharge Summary',this)">Discharge</button>
      </div>

      <div class="table-wrap">
        <div class="table-tools">
          <input class="search-input" id="recSearch" type="search" placeholder="Search patient, ID, document or symptom…" oninput="renderRecordsTable()">
          <div class="rec-count" id="recCount">0 records</div>
        </div>
        <div class="table-scroll">
          <table>
            <thead>
              <tr>
                <th>DATE</th>
                <th>PATIENT</th>
                <th>DOCUMENT TYPE</th>
                <th>TITLE</th>
                <th>SYMPTOMS / NOTES</th>
                <th>STATUS</th>
                <th>ACTION</th>
              </tr>
            </thead>
            <tbody id="recTableBody">
              <tr><td colspan="7" class="empty-cell">No records yet. Add patient data to populate this table.</td></tr>
            </tbody>
          </table>
        </div>
      </div>
      <div class="footer">MEDUSA-X · Backed by dataset/clinical_records.json · Not a diagnostic system</div>
    </section>

    <!-- ── SAFETY REVIEW PAGE ─────────────────────── -->
    <section id="pgSafety" class="inner-page">
      <div class="heading">
        <div>
          <div class="eyebrow">CLINICAL SAFETY</div>
          <h1>Safety Review</h1>
          <div class="sub">Documentation completeness flags and clinical safety checks for all submitted records.</div>
        </div>
      </div>

      <div class="safety-score" id="safetyScoreBanner">
        <div class="score-ring mid" id="safetyScoreRing">—</div>
        <div>
          <h3 id="safetyScoreLabel">No Records Submitted</h3>
          <p id="safetyScoreSub">Add patient records to see safety analysis.</p>
        </div>
      </div>

      <div class="select-row">
        <label for="safetySelector">REVIEW RECORD:</label>
        <select id="safetySelector" onchange="renderSafetyFlags()">
          <option value="">— All records (latest) —</option>
        </select>
      </div>

      <div id="safetyFlagsArea"></div>

      <div class="card" style="margin-top:18px">
        <div class="panel-head"><h3>All Records Safety Summary</h3><small>FLAG TABLE</small></div>
        <div class="table-scroll">
          <table>
            <thead>
              <tr><th>PATIENT</th><th>ID</th><th>DATE</th><th>DOC TYPE</th><th>FLAGS</th><th>STATUS</th></tr>
            </thead>
            <tbody id="safetyTableBody">
              <tr><td colspan="6" class="empty-cell">No records submitted yet.</td></tr>
            </tbody>
          </table>
        </div>
      </div>

      <div class="footer">MEDUSA-X · Safety flags are documentation checks only · Not a clinical diagnosis</div>
    </section>

  </main>
</div>

<script src="js/api.js"></script>
<script src="js/app.js"></script>
</body>
</html>
