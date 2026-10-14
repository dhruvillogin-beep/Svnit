<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>SVNIT Smart Attendance</title>
  <style>
    :root {
      --navy: #002147;
      --navy-light: #003366;
      --saffron: #FF9933;
      --saffron-dark: #E67300;
      --green: #138808;
      --green-dark: #0F6B06;
      --bg: #F8FAFC;
      --card: #FFFFFF;
      --text: #0F172A;
      --muted: #64748B;
      --border: #E2E8F0;
      --danger: #DC2626;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
      line-height: 1.5;
      padding-bottom: 50px;
    }
    header {
      background: var(--navy);
      color: white;
      padding: 12px 16px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 2px 8px rgba(0,0,0,0.15);
    }
    .header-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 680px;
      margin: 0 auto;
    }
    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .crest {
      background: white;
      color: var(--navy);
      font-weight: 900;
      font-size: 13px;
      width: 34px;
      height: 34px;
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      border: 2px solid var(--saffron);
    }
    .title {
      font-size: 14px;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .dot-accent {
      width: 7px;
      height: 7px;
      background: var(--saffron);
      border-radius: 50%;
      display: inline-block;
    }
    .subtitle {
      font-size: 10px;
      color: #CBD5E1;
    }
    .role-bar {
      max-width: 680px;
      margin: 8px auto 0;
      padding-top: 8px;
      border-top: 1px solid rgba(255,255,255,0.15);
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
      flex-wrap: wrap;
      gap: 6px;
    }
    .btn-quick {
      background: rgba(255,255,255,0.15);
      color: white;
      border: 1px solid rgba(255,255,255,0.25);
      padding: 4px 10px;
      border-radius: 4px;
      font-size: 11px;
      font-weight: 600;
      cursor: pointer;
    }
    .btn-quick.active {
      background: var(--saffron);
      color: white;
      border-color: var(--saffron);
    }
    .container {
      max-width: 680px;
      margin: 16px auto;
      padding: 0 16px;
    }
    .card {
      background: var(--card);
      border-radius: 16px;
      border: 1px solid var(--border);
      padding: 16px;
      margin-bottom: 16px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.03);
    }
    .badge {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 9999px;
      font-size: 10px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    .badge-student { background: #DBEAFE; color: #1E40AF; }
    .badge-teacher { background: #FEF3C7; color: #92400E; }
    .badge-admin { background: #F3E8FF; color: #6B21A8; }
    .badge-pending { background: #FFF7ED; color: #C2410C; border: 1px solid #FDBA74; }
    .badge-approved { background: #ECFDF5; color: #047857; border: 1px solid #6EE7B7; }
    .badge-rejected { background: #FEF2F2; color: #B91C1C; border: 1px solid #FCA5A5; }

    .tabs {
      display: flex;
      background: #E2E8F0;
      padding: 4px;
      border-radius: 12px;
      margin-bottom: 16px;
      gap: 4px;
    }
    .tab-btn {
      flex: 1;
      padding: 8px 6px;
      text-align: center;
      font-size: 11px;
      font-weight: 700;
      border: none;
      border-radius: 8px;
      background: transparent;
      color: var(--muted);
      cursor: pointer;
      transition: background 0.15s;
    }
    .tab-btn.active {
      background: white;
      color: var(--navy);
      box-shadow: 0 1px 3px rgba(0,0,0,0.06);
    }
    .btn {
      width: 100%;
      padding: 10px 14px;
      border-radius: 10px;
      font-size: 12px;
      font-weight: 700;
      border: none;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: background 0.15s;
    }
    .btn-navy { background: var(--navy); color: white; }
    .btn-navy:hover { background: var(--navy-light); }
    .btn-saffron { background: var(--saffron); color: white; }
    .btn-saffron:hover { background: var(--saffron-dark); }
    .btn-green { background: var(--green); color: white; }
    .btn-green:hover { background: var(--green-dark); }
    .btn-secondary { background: #E2E8F0; color: #334155; }
    .btn-secondary:hover { background: #CBD5E1; }
    .btn-danger { background: var(--danger); color: white; }

    input, select {
      width: 100%;
      padding: 8px 12px;
      font-size: 12px;
      border: 1px solid var(--border);
      border-radius: 8px;
      outline: none;
      margin-top: 4px;
      background: white;
    }
    input:focus, select:focus {
      border-color: var(--navy);
    }
    label { font-size: 11px; font-weight: 600; color: #475569; }
    .video-preview {
      width: 100%;
      max-width: 280px;
      aspect-ratio: 4/3;
      object-fit: cover;
      border-radius: 12px;
      background: #000;
      margin: 10px auto;
      display: block;
      border: 2px solid var(--navy);
    }
    .selfie-thumb {
      width: 44px;
      height: 44px;
      border-radius: 8px;
      object-fit: cover;
      border: 1px solid var(--border);
      background: #E2E8F0;
    }
    .notice {
      padding: 10px 12px;
      border-radius: 10px;
      font-size: 11px;
      margin-bottom: 12px;
      line-height: 1.4;
    }
    .notice-warn { background: #FFFBEB; color: #B45309; border: 1px solid #FDE68A; }
    .notice-info { background: #EFF6FF; color: #1D4ED8; border: 1px solid #BFDBFE; }
    .notice-success { background: #F0FDF4; color: #15803D; border: 1px solid #BBF7D0; }
    .banner {
      background: #F1F5F9;
      border-bottom: 1px solid var(--border);
      padding: 6px 12px;
      text-align: center;
      font-size: 10px;
      color: #475569;
    }
    .qr-container {
      background: white;
      border: 2px solid var(--navy);
      padding: 12px;
      border-radius: 12px;
      display: inline-block;
      margin: 10px auto;
      box-shadow: 0 4px 12px rgba(0,0,0,0.06);
    }
    .qr-container svg {
      display: block;
      margin: 0 auto;
    }
  </style>
</head>
<body>

  <header>
    <div class="header-top">
      <div class="brand">
        <div class="crest">SV</div>
        <div>
          <div class="title">SVNIT Smart Attendance <span class="dot-accent"></span></div>
          <div class="subtitle">Sardar Vallabhbhai National Institute of Technology, Surat</div>
        </div>
      </div>
    </div>
    <div class="role-bar">
      <div>
        <span id="userName" style="font-weight:700;">Loading...</span>
        <span id="userRoleBadge"></span>
      </div>
      <div style="display:flex; gap:4px; align-items:center;">
        <span style="color:#CBD5E1; font-size:10px;">Switch:</span>
        <button class="btn-quick" id="btnStudent" onclick="window.switchRole('student')">Student</button>
        <button class="btn-quick" id="btnTeacher" onclick="window.switchRole('teacher')">Teacher</button>
        <button class="btn-quick" id="btnAdmin" onclick="window.switchRole('admin')">Admin</button>
      </div>
    </div>
  </header>

  <div class="banner">
    <strong style="color:var(--navy);">Role Simulation Engine:</strong> Tap buttons above to switch between <strong>Student</strong>, <strong>Teacher</strong>, and <strong>Admin</strong>.
  </div>

  <div class="container" id="appRoot"></div>

  <script>
    // --- Pure JS Reed-Solomon QR Vector Generator ---
    var GF_EXP = new Uint8Array(512), GF_LOG = new Uint8Array(256);
    (function() {
      var x = 1;
      for (var i = 0; i < 255; i++) {
        GF_EXP[i] = x; GF_LOG[x] = i; x <<= 1;
        if (x & 256) x ^= 0x11d;
      }
      for (var i = 255; i < 512; i++) GF_EXP[i] = GF_EXP[i - 255];
    })();
    function gfMul(x, y) { return (x === 0 || y === 0) ? 0 : GF_EXP[GF_LOG[x] + GF_LOG[y]]; }
    function rsGenPoly(d) {
      var p = new Uint8Array([1]);
      for (var i = 0; i < d; i++) {
        var n = new Uint8Array(p.length + 1);
        for (var j = 0; j < p.length; j++) { n[j] ^= gfMul(p[j], GF_EXP[i]); n[j + 1] ^= p[j]; }
        p = n;
      }
      return p;
    }
    function rsCalc(data, ecLen) {
      var gen = rsGenPoly(ecLen), msg = new Uint8Array(data.length + ecLen);
      msg.set(data);
      for (var i = 0; i < data.length; i++) {
        var c = msg[i];
        if (c !== 0) for (var j = 0; j < gen.length; j++) msg[i + j] ^= gfMul(gen[j], c);
      }
      return msg.slice(data.length);
    }
    function generateQRMatrix(text) {
      var version = 4, size = 17 + 4 * version, totalCodewords = 100, ecCodewords = 20, dataCodewords = 80;
      var utf8 = new TextEncoder().encode(text), buffer = [];
      function writeBits(val, len) { for (var i = len - 1; i >= 0; i--) buffer.push((val >> i) & 1); }
      writeBits(4, 4); writeBits(utf8.length, 8);
      for (var i = 0; i < utf8.length; i++) writeBits(utf8[i], 8);
      for (var i = 0; i < 4 && buffer.length < dataCodewords * 8; i++) buffer.push(0);
      while (buffer.length % 8 !== 0) buffer.push(0);
      var pads = [0xEC, 0x11], pIdx = 0;
      while (buffer.length < dataCodewords * 8) { writeBits(pads[pIdx % 2], 8); pIdx++; }
      var dataBytes = new Uint8Array(dataCodewords);
      for (var i = 0; i < dataCodewords; i++) {
        var bVal = 0;
        for (var b = 0; b < 8; b++) bVal = (bVal << 1) | buffer[i * 8 + b];
        dataBytes[i] = bVal;
      }
      var ecBytes = rsCalc(dataBytes, ecCodewords);
      var allCodewords = new Uint8Array(totalCodewords);
      allCodewords.set(dataBytes, 0); allCodewords.set(ecBytes, dataBytes.length);

      var grid = Array.from({ length: size }, function() { return Array(size).fill(null); });
      var isFunc = Array.from({ length: size }, function() { return Array(size).fill(false); });
      function setF(r, c, val) { grid[r][c] = val; isFunc[r][c] = true; }
      function drawFinder(row, col) {
        for (var r = -1; r <= 7; r++) {
          for (var c = -1; c <= 7; c++) {
            var nr = row + r, nc = col + c;
            if (nr >= 0 && nr < size && nc >= 0 && nc < size) {
              setF(nr, nc, (r >= 0 && r <= 6 && c >= 0 && c <= 6) ? (r === 0 || r === 6 || c === 0 || c === 6 || (r >= 2 && r <= 4 && c >= 2 && c <= 4)) : false);
            }
          }
        }
      }
      drawFinder(0, 0); drawFinder(0, size - 7); drawFinder(size - 7, 0);
      for (var i = 8; i < size - 8; i++) { setF(6, i, i % 2 === 0); setF(i, 6, i % 2 === 0); }
      var align = [6, 24];
      for (var ar = 0; ar < align.length; ar++) {
        for (var ac = 0; ac < align.length; ac++) {
          var rPos = align[ar], cPos = align[ac];
          if (grid[rPos][cPos] !== null) continue;
          for (var r = -2; r <= 2; r++) {
            for (var c = -2; c <= 2; c++) {
              setF(rPos + r, cPos + c, Math.abs(r) === 2 || Math.abs(c) === 2 || (r === 0 && c === 0));
            }
          }
        }
      }
      setF(4 * version + 9, 8, true);
      var formatBits = 0x77c4;
      for (var i = 0; i < 15; i++) {
        var bit = ((formatBits >> i) & 1) === 1;
        if (i < 6) setF(8, i, bit);
        else if (i === 6) setF(8, 7, bit);
        else if (i === 7) setF(8, 8, bit);
        else if (i === 8) setF(7, 8, bit);
        else setF(14 - i, 8, bit);
        if (i < 8) setF(8, size - 1 - i, bit);
        else setF(size - 15 + i, 8, bit);
      }
      var bitIdx = 0, totalBits = totalCodewords * 8;
      for (var right = size - 1; right > 0; right -= 2) {
        if (right === 6) right--;
        var upward = ((right + 1) / 2) % 2 === 1;
        for (var vert = 0; vert < size; vert++) {
          var row = upward ? size - 1 - vert : vert;
          for (var col = right; col >= right - 1; col--) {
            if (!isFunc[row][col]) {
              var bit = false;
              if (bitIdx < totalBits) {
                var byte = allCodewords[Math.floor(bitIdx / 8)];
                bit = ((byte >> (7 - (bitIdx % 8))) & 1) === 1;
                bitIdx++;
              }
              if ((row + col) % 2 === 0) bit = !bit;
              grid[row][col] = bit;
            }
          }
        }
      }
      return grid.map(function(r) { return r.map(function(c) { return !!c; }); });
    }

    function renderQRSVG(text, px) {
      px = px || 200;
      try {
        var matrix = generateQRMatrix(text), modCount = matrix.length, qz = 2, total = modCount + qz * 2, paths = '';
        for (var r = 0; r < modCount; r++) {
          for (var c = 0; c < modCount; c++) {
            if (matrix[r][c]) paths += 'M' + (c + qz) + ',' + (r + qz) + 'h1v1h-1z ';
          }
        }
        return '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 ' + total + ' ' + total + '" width="' + px + '" height="' + px + '" shape-rendering="crispEdges"><rect width="' + total + '" height="' + total + '" fill="#ffffff"/><path d="' + paths.trim() + '" fill="#002147"/></svg>';
      } catch (e) {
        return '<div style="font-size:11px; color:red;">QR Generation Error: ' + e.message + '</div>';
      }
    }

    var SAMPLE_SELFIE_SVG = 'data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 200 200"><rect width="200" height="200" fill="%23002147"/><circle cx="100" cy="80" r="40" fill="%23FF9933"/><path d="M40 180 C40 135 160 135 160 180 Z" fill="%23FFFFFF"/><text x="100" y="192" font-family="sans-serif" font-size="12" fill="%23002147" font-weight="bold" text-anchor="middle">SVNIT STUDENT</text></svg>';

    window.STATE = {
      currentUser: { uid: 'student-1', role: 'student', name: 'Aarav Mehta', rollNo: 'U21CS042', department: 'Computer Science', isApproved: true },
      users: [
        { uid: 'student-1', role: 'student', name: 'Aarav Mehta', rollNo: 'U21CS042', department: 'Computer Science', isApproved: true },
        { uid: 'student-2', role: 'student', name: 'Priya Sharma', rollNo: 'U21CS089', department: 'Computer Science', isApproved: false },
        { uid: 'teacher-1', role: 'teacher', name: 'Dr. Rajesh Patel', rollNo: 'EMP104', department: 'Computer Science', isApproved: true },
        { uid: 'admin-1', role: 'admin', name: 'Dr. S. K. Raman', rollNo: 'EMP001', department: 'Academic Section', isApproved: true }
      ],
      courses: [
        { id: 'cs-301', code: 'CS-301', name: 'Data Structures & Algorithms' },
        { id: 'cs-302', code: 'CS-302', name: 'Database Management Systems' }
      ],
      sessions: [
        { id: 'sess-init-1', courseId: 'cs-301', courseCode: 'CS-301', courseName: 'Data Structures & Algorithms', teacherId: 'teacher-1', teacherName: 'Dr. Rajesh Patel', token: 'svnit_active_token_99', status: 'active', expiresAt: Date.now() + 15 * 60 * 1000 }
      ],
      attendance: []
    };

    window.activeTab = 'main';
    window.mediaStream = null;
    window.capturedSelfie = null;
    window.selectedCourseId = 'cs-301';

    window.switchRole = function(role) {
      if (role === 'student') window.STATE.currentUser = window.STATE.users[0];
      if (role === 'teacher') window.STATE.currentUser = window.STATE.users[2];
      if (role === 'admin') window.STATE.currentUser = window.STATE.users[3];
      window.stopCamera();
      window.activeTab = 'main';
      window.render();
    };

    window.setTab = function(tab) { window.activeTab = tab; window.render(); };
    window.useSampleSelfie = function() { window.capturedSelfie = SAMPLE_SELFIE_SVG; window.stopCamera(); window.render(); };
    window.clearSelfie = function() { window.capturedSelfie = null; window.render(); };

    function renderRoleBar() {
      var u = window.STATE.currentUser;
      var nameEl = document.getElementById('userName'), badgeEl = document.getElementById('userRoleBadge');
      if (nameEl) nameEl.textContent = u.name;
      if (badgeEl) {
        badgeEl.innerHTML = '<span class="badge badge-' + u.role + '">' + u.role + '</span> <span class="badge ' + (u.isApproved ? 'badge-approved' : 'badge-pending') + '">' + (u.isApproved ? 'Approved' : 'Pending Approval') + '</span>';
      }
      var bStud = document.getElementById('btnStudent'), bTeach = document.getElementById('btnTeacher'), bAdm = document.getElementById('btnAdmin');
      if (bStud) bStud.className = 'btn-quick' + (u.role === 'student' ? ' active' : '');
      if (bTeach) bTeach.className = 'btn-quick' + (u.role === 'teacher' ? ' active' : '');
      if (bAdm) bAdm.className = 'btn-quick' + (u.role === 'admin' ? ' active' : '');
    }

    window.render = function() {
      renderRoleBar();
      var root = document.getElementById('appRoot');
      if (!root) return;
      var role = window.STATE.currentUser.role;
      if (role === 'student') renderStudent(root);
      else if (role === 'teacher') renderTeacher(root);
      else if (role === 'admin') renderAdmin(root);
    };

    function renderStudent(container) {
      var activeSession = window.STATE.sessions.find(function(s) { return s.status === 'active' && s.expiresAt > Date.now(); });
      var studentHistory = window.STATE.attendance.filter(function(a) { return a.studentId === window.STATE.currentUser.uid; });
      var isApproved = window.STATE.currentUser.isApproved;

      var html = '<div class="tabs"><button class="tab-btn ' + (window.activeTab === 'main' ? 'active' : '') + '" onclick="window.setTab(\'main\')">Mark Attendance</button><button class="tab-btn ' + (window.activeTab === 'history' ? 'active' : '') + '" onclick="window.setTab(\'history\')">My Records (' + studentHistory.length + ')</button></div>';

      if (!isApproved) {
        html += '<div class="notice notice-warn"><strong>Account Pending Admin Approval:</strong> Your student account is pending verification. Only approved students can record attendance. Switch to <strong>Admin</strong> to approve.</div>';
      }

      if (window.activeTab === 'main') {
        html += '<div class="card"><h3 style="font-size:14px; color:var(--navy); margin-bottom:8px;">Step 1: Active Classroom QR Session</h3>';
        if (activeSession) {
          html += '<div class="notice notice-info"><strong>Course:</strong> ' + activeSession.courseCode + ' — ' + activeSession.courseName + '<br><strong>Instructor:</strong> ' + activeSession.teacherName + '<br><strong>Time Remaining:</strong> <span id="studentTimer" style="font-weight:700;">' + getRemainingTimeStr(activeSession.expiresAt) + '</span><div style="margin-top:6px; font-family:monospace; font-size:10px; background:rgba(0,0,0,0.04); padding:4px 8px; border-radius:4px; word-break:break-all;">Payload Token: ' + activeSession.token + '</div></div>';
        } else {
          html += '<div class="notice notice-warn">No active class session right now. Switch to <strong>Teacher</strong> to start one!</div>';
        }

        html += '<h3 style="font-size:14px; color:var(--navy); margin-top:16px; margin-bottom:8px;">Step 2: Capture Verification Selfie</h3>';
        if (window.capturedSelfie) {
          html += '<div style="text-align:center;"><img src="' + window.capturedSelfie + '" style="width:130px; height:130px; border-radius:12px; object-fit:cover; border:2px solid var(--green); display:block; margin:0 auto;" /><div style="margin-top:8px;"><button class="btn btn-secondary" style="width:auto; display:inline-flex; padding:4px 12px; font-size:11px;" onclick="window.clearSelfie()">Retake Photo</button></div></div>';
        } else {
          html += '<video id# Svnit
