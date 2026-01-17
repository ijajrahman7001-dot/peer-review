<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Radiology Templates System</title>
	
	<!-- PWA Manifest -->
<link rel="manifest" href="./manifest.json">

<!-- Theme Color -->
<meta name="theme-color" content="#3498db">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="RadTemplates">

<!-- PWA Icons -->
<link rel="apple-touch-icon" href="./icons/icon-192.png">
<link rel="icon" type="image/png" sizes="192x192" href="./icons/icon-192.png">
<link rel="icon" type="image/png" sizes="512x512" href="./icons/icon-512.png">

<!-- ✅ Intro.js CSS and JS -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/intro.js/7.2.0/introjs.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/intro.js/7.2.0/intro.min.js"></script>

    <style>
	/* Meeting Badge Animations */
@keyframes meetingPulse {
    0%, 100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(231, 76, 60, 0.7); }
    50% { transform: scale(1.1); box-shadow: 0 0 0 10px rgba(231, 76, 60, 0); }
}

@keyframes slideDown {
    from { transform: translateY(-100%); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
}

/* Meeting Alert Banner */
.meeting-alert-banner {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    background: linear-gradient(135deg, #ff6b6b, #ee5a6f);
    color: white;
    padding: 15px 20px;
    z-index: 9998;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    animation: slideDown 0.5s ease;
}

.meeting-alert-banner strong {
    font-size: 16px;
}

.meeting-alert-actions {
    display: flex;
    gap: 10px;
}

.meeting-alert-actions button {
    background: white;
    color: #e74c3c;
    border: none;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
    transition: all 0.3s;
}

.meeting-alert-actions button:hover {
    background: #f8f9fa;
    transform: scale(1.05);
}

/* Meeting Cards */
.meeting-card {
    background: white;
    border: 2px solid #e3f2fd;
    border-left: 5px solid #3498db;
    border-radius: 10px;
    padding: 20px;
    margin: 15px 0;
    box-shadow: 0 3px 10px rgba(0,0,0,0.1);
    transition: all 0.3s;
}

.meeting-card:hover {
    box-shadow: 0 5px 20px rgba(0,0,0,0.2);
    transform: translateY(-2px);
}

.meeting-card.urgent {
    border-left-color: #e74c3c;
    background: #fff5f5;
}

.meeting-card-header {
    display: flex;
    justify-content: space-between;
    align-items: start;
    margin-bottom: 15px;
}

.meeting-title {
    font-size: 18px;
    font-weight: bold;
    color: #2c3e50;
    margin-bottom: 5px;
}

.meeting-type-badge {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 11px;
    font-weight: bold;
    text-transform: uppercase;
}

.meeting-type-badge.qa-review { background: #e74c3c; color: white; }
.meeting-type-badge.training { background: #3498db; color: white; }
.meeting-type-badge.department { background: #9b59b6; color: white; }
.meeting-type-badge.emergency { background: #e67e22; color: white; }
.meeting-type-badge.other { background: #95a5a6; color: white; }

.meeting-details {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    margin: 15px 0;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
}

.meeting-detail-item {
    display: flex;
    align-items: center;
    font-size: 13px;
    color: #555;
}

.meeting-detail-item strong {
    margin-right: 8px;
    color: #2c3e50;
}

.meeting-agenda {
    background: #e8f5e9;
    padding: 15px;
    border-radius: 8px;
    margin: 15px 0;
    border-left: 4px solid #27ae60;
}

.meeting-agenda h4 {
    margin: 0 0 10px 0;
    color: #27ae60;
    font-size: 14px;
}

.meeting-attachments {
    margin: 15px 0;
}

.attachment-item {
    display: inline-flex;
    align-items: center;
    background: #fff;
    border: 1px solid #dee2e6;
    padding: 8px 12px;
    border-radius: 5px;
    margin: 5px 5px 5px 0;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.2s;
}

.attachment-item:hover {
    background: #e3f2fd;
    border-color: #3498db;
}

.meeting-rsvp-buttons {
    display: flex;
    gap: 10px;
    margin-top: 20px;
}

.rsvp-btn {
    flex: 1;
    padding: 12px;
    border: none;
    border-radius: 8px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s;
}

.rsvp-btn.accept {
    background: #27ae60;
    color: white;
}

.rsvp-btn.accept:hover {
    background: #229954;
    transform: scale(1.05);
}

.rsvp-btn.decline {
    background: #e74c3c;
    color: white;
}

.rsvp-btn.decline:hover {
    background: #c0392b;
    transform: scale(1.05);
}

.rsvp-btn.tentative {
    background: #f39c12;
    color: white;
}

.rsvp-btn.tentative:hover {
    background: #e67e22;
    transform: scale(1.05);
}

/* HR Meeting Management */
.hr-meeting-dashboard {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 15px;
    margin-bottom: 20px;
}

.hr-meeting-stat-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
}

.hr-meeting-stat-card.pending {
    background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
}

.hr-meeting-stat-card.upcoming {
    background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
}

.hr-meeting-stat-card.completed {
    background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
}

.meeting-stat-value {
    font-size: 36px;
    font-weight: bold;
    margin: 10px 0;
}

.meeting-stat-label {
    font-size: 14px;
    opacity: 0.9;
}

.participant-selector {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    max-height: 300px;
    overflow-y: auto;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    margin: 15px 0;
}

.participant-checkbox {
    display: flex;
    align-items: center;
    padding: 8px;
    background: white;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.2s;
}

.participant-checkbox:hover {
    background: #e3f2fd;
}

.participant-checkbox input[type="checkbox"] {
    margin-right: 10px;
    transform: scale(1.3);
    cursor: pointer;
}

.response-summary {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    margin: 15px 0;
}

.response-stat {
    text-align: center;
    padding: 15px;
    border-radius: 8px;
    background: #f8f9fa;
}

.response-stat.accepted { background: #d4edda; color: #155724; }
.response-stat.declined { background: #f8d7da; color: #721c24; }
.response-stat.tentative { background: #fff3cd; color: #856404; }
.response-stat.pending { background: #d1ecf1; color: #0c5460; }

.response-stat-value {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 5px;
}

.response-stat-label {
    font-size: 12px;
}
		@keyframes blinkBadge {
			0%, 100% { background: #e74c3c; transform: scale(1); }
			50% { background: #c0392b; transform: scale(1.2); }
		}

		.tab-counter.new-assignment {
			animation: blinkBadge 1s ease-in-out 5;
		}
		
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f5f6fa;
            color: #333;
        }
		
		/* ============================================== */
/* SCHEDULING SYSTEM STYLES */
/* ============================================== */

.schedule-panel {
    background: white;
    padding: 15px 20px 20px 20px;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    margin-bottom: 20px;
}

.schedule-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 2px solid #3498db;
}

.schedule-tabs {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.schedule-tab {
    padding: 10px 20px;
    background: #ecf0f1;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.3s;
}

.schedule-tab.active {
    background: #3498db;
    color: white;
}

.schedule-controls {
    display: flex;
    gap: 10px;
    align-items: center;
    margin-bottom: 20px;
}

.month-nav {
    display: flex;
    align-items: center;
    gap: 15px;
}

.month-nav button {
    background: #3498db;
    color: white;
    border: none;
    padding: 8px 15px;
    border-radius: 5px;
    cursor: pointer;
    font-size: 14px;
}

.month-nav button:hover {
    background: #2980b9;
}

.current-month {
    font-size: 18px;
    font-weight: bold;
    color: #2c3e50;
    min-width: 200px;
    text-align: center;
}

.schedule-table-container {
    overflow-x: auto;
    max-height: 600px;
    overflow-y: auto;
    border: 2px solid #ecf0f1;
    border-radius: 8px;
}

.schedule-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 14px;
    min-width: auto;
}

.schedule-table thead {
    position: sticky;
    top: 0;
    z-index: 10;
    background: #34495e;
    color: white;
}

.schedule-table th {
    padding: 12px 8px;
    text-align: center;
    border: 1px solid #2c3e50;
    font-weight: 600;
	position: relative; 
	min-width: 120px;
}

.col-resizer {
    position: absolute;
    right: 0;
    top: 0;
    width: 5px;
    height: 100%;
    cursor: col-resize;
    user-select: none;
    background: transparent; /* invisible */
}
.schedule-table th:hover .col-resizer {
    background: #ccc; /* visible only on hover */
}

.schedule-table th.date-column {
    text-align: left;
    position: sticky;
    left: 0;
    background: #34495e;
    z-index: 11;
    min-width: 100px;
}

.schedule-table td {
    padding: 12px;
    border: 1px solid #ecf0f1;
    text-align: center;
    vertical-align: middle;
    min-height: 100px;
	min-width: 120px;

}

.schedule-table th.employee-header {
    text-align: center;
    min-width: 150px;
    background: #34495e;
}

.schedule-table td.date-column {
    position: sticky;
    left: 0;
    background: #f8f9fa;
    font-weight: 600;
    z-index: 5;
    border-right: 2px solid #dee2e6;
    text-align: center;
    font-size: 13px;
}

.schedule-table tr:nth-child(even) td.employee-name {
    background: #f8f9fa;
}

.shift-cell {
    min-height: 50px;
    position: relative;
    cursor: pointer;
    transition: all 0.2s;
}

.shift-cell:hover {
    background: #f0f8ff;
}

.shift-cell.has-shift {
    background: #d4edda;
    cursor: grab;
}

.shift-cell.has-shift:active {
    cursor: grabbing;
}

.shift-cell.overtime {
    background: #fff3cd;
    border: 2px solid #ffc107;
}

.shift-cell.leave-approved {
    background: #cfe2ff;
    border: 2px solid #0d6efd;
}

.shift-cell.leave-pending {
    background: #ffe5b4;
    border: 2px solid #ff8c00;
}
.shift-cell.selected {
    background: #2196f3  !important;
	color: white;
    border: 2px solid #2196f3 !important;
    box-shadow: 0 0 5px rgba(33, 150, 243, 0.5) !important;
}
.shift-time {
    font-weight: 600;
    color: #2c3e50;
    display: block;
}

.shift-duration {
    font-size: 12px;
    color: #7f8c8d;
    display: block;
}
.shift-note {
    font-size: 10px;
    color: #e67e22;
    margin-top: 3px;
    display: block;
    word-wrap: break-word;
    max-width: 100%;
    font-weight: 500;
}

.note-input {
    width: 100%;
    border: 1px solid #3498db;
    border-radius: 3px;
    padding: 6px;
    font-size: 12px;
    font-family: inherit;
    margin-top: 3px;
    background: #fff;
    color: #e67e22;
}

.note-input:focus {
    outline: none;
    border-color: #2980b9;
    box-shadow: 0 0 5px rgba(52, 152, 219, 0.3);
}

.note-only-cell {
    background: #fff8e1 !important;
    font-size: 11px;
    color: #e67e22;
    font-weight: 500;
    padding: 8px !important;
}
.weekend-column {
    background: #f9e79f  !important;
	color: #333 !important; 
}

.leave-badge {
    display: inline-block;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 10px;
    font-weight: bold;
    margin-top: 2px;
}

.leave-badge.approved {
    background: #0d6efd;
    color: white;
}

.leave-badge.pending {
    background: #ff8c00;
    color: white;
}

.overtime-indicator {
    position: absolute;
    top: 2px;
    right: 2px;
    background: #ffc107;
    color: #000;
    padding: 2px 5px;
    border-radius: 3px;
    font-size: 9px;
    font-weight: bold;
}

.notification-badge {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px 40px;
    border-radius: 15px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.3);
    z-index: 10002;
    text-align: center;
    min-width: 400px;
    animation: slideIn 0.3s ease;
}

@keyframes slideIn {
    from { transform: translate(-50%, -60%); opacity: 0; }
    to { transform: translate(-50%, -50%); opacity: 1; }
}

.notification-badge h3 {
    margin: 0 0 15px 0;
    font-size: 22px;
}

.notification-badge p {
    margin: 10px 0;
    line-height: 1.6;
}

.accept-btn {
    background: #27ae60;
    color: white;
    border: none;
    padding: 12px 30px;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    font-weight: bold;
    margin-top: 15px;
}

.accept-btn:hover {
    background: #229954;
}

.leave-summary {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 15px;
    margin-bottom: 20px;
}

.leave-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
}

.leave-card.used {
    background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
}

.leave-card.pending {
    background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
}

.leave-card.available {
    background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
}

.leave-value {
    font-size: 32px;
    font-weight: bold;
    margin: 10px 0;
}

.leave-label {
    font-size: 14px;
    opacity: 0.9;
}

.drag-over {
    background: #90caf9 !important;
    border: 2px dashed #2196f3 !important;
}

.copy-schedule-controls {
    display: flex;
    gap: 10px;
    margin-bottom: 15px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
}

.login-page {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
    position: fixed; /* CHANGED FROM RELATIVE */
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 9999; /* ENSURE LOGIN IS ABOVE EVERYTHING */
    overflow: hidden;
}

/* Animated background medical pattern */
.login-page::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background-image: 
        radial-gradient(circle, rgba(52, 152, 219, 0.1) 1px, transparent 1px),
        radial-gradient(circle, rgba(52, 152, 219, 0.1) 1px, transparent 1px);
    background-size: 50px 50px;
    background-position: 0 0, 25px 25px;
    animation: backgroundMove 20s linear infinite;
    z-index: 1;
}

@keyframes backgroundMove {
    0% { transform: translate(0, 0); }
    100% { transform: translate(50px, 50px); }
}

/* Floating medical icons */
.login-page::after {
    content: '🏥 ⚕️ 🩺 💊 🔬';
    position: absolute;
    font-size: 60px;
    opacity: 0.05;
    animation: floatIcons 30s linear infinite;
    z-index: 1;
    white-space: nowrap;
    letter-spacing: 100px;
}

@keyframes floatIcons {
    0% { transform: translateY(100vh) rotate(0deg); }
    100% { transform: translateY(-100vh) rotate(360deg); }
}

.login-container {
    background: rgba(255, 255, 255, 0.15);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    padding: 50px 45px;
    border-radius: 20px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
    width: 100%;
    max-width: 420px;
    position: relative;
    z-index: 10000; /* INCREASED FROM 10 */
    animation: cardSlideIn 0.6s ease-out;
}

.login-container a {
    position: relative;
    z-index: 10001; /* ENSURE LINKS ARE ABOVE EVERYTHING */
    cursor: pointer;
}

@keyframes cardSlideIn {
    0% {
        opacity: 0;
        transform: translateY(30px) scale(0.95);
    }
    100% {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
}

/* Glowing border effect */
.login-container::before {
    content: '';
    position: absolute;
    inset: -2px;
    border-radius: 20px;
    padding: 2px;
    background: linear-gradient(45deg, #3498db, #2ecc71, #3498db);
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    -webkit-mask-composite: xor;
    mask-composite: exclude;
    opacity: 0.6;
    animation: borderGlow 3s ease-in-out infinite;
}

@keyframes borderGlow {
    0%, 100% { opacity: 0.4; }
    50% { opacity: 0.8; }
}

        .login-container h1 {
    text-align: center;
    color: #ffffff;
    margin-bottom: 40px;
    font-size: 32px;
    font-weight: 700;
    text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    letter-spacing: 1px;
	pointer-events: none;        /* ADD THIS */
    user-select: none;           /* ADD THIS */
    cursor: default;  
}
.login-container input,
.login-container button,
.login-container a {
    pointer-events: auto;
}

.login-container h1::before {
    content: '🏥 ';
    font-size: 40px;
    display: block;
    margin-bottom: 10px;
    animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
}

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #ffffff;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.form-group input {
    width: 100%;
    padding: 14px 18px;
    border: 2px solid rgba(255, 255, 255, 0.3);
    border-radius: 12px;
    font-size: 16px;
    background: rgba(255, 255, 255, 0.9);
    color: #2c3e50;
    transition: all 0.3s ease;
    font-weight: 500;
}

.form-group input:focus {
    outline: none;
    border-color: #3498db;
    background: rgba(255, 255, 255, 1);
    box-shadow: 0 0 20px rgba(52, 152, 219, 0.4);
    transform: translateY(-2px);
}

.form-group input::placeholder {
    color: #95a5a6;
    font-weight: 400;
}

        .login-btn {
    width: 100%;
    padding: 16px;
    background: linear-gradient(135deg, #3498db 0%, #2ecc71 100%);
    color: white;
    border: none;
    border-radius: 12px;
    font-size: 18px;
    font-weight: 700;
    cursor: pointer;
    text-transform: uppercase;
    letter-spacing: 1px;
    transition: all 0.3s ease;
    box-shadow: 0 8px 20px rgba(52, 152, 219, 0.4);
    position: relative;
    overflow: hidden;
}

.login-btn::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
    transition: left 0.5s ease;
}

.login-btn:hover::before {
    left: 100%;
}

.login-btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 30px rgba(52, 152, 219, 0.6);
}

.login-btn:active {
    transform: translateY(-1px);
}

       .error {
    color: #ffffff;
    margin-top: 15px;
    text-align: center;
    padding: 14px;
    background: rgba(231, 76, 60, 0.85);
    backdrop-filter: blur(10px);
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.3);
    font-weight: 600;
    animation: shake 0.5s ease;
    box-shadow: 0 4px 15px rgba(231, 76, 60, 0.4);
}

@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-10px); }
    75% { transform: translateX(10px); }
}

.login-container small a {
    color: rgba(255, 255, 255, 0.8);
    text-decoration: none;
    font-weight: 500;
    transition: all 0.3s ease;
    border-bottom: 1px solid transparent;
}

.login-container small a:hover {
    color: #3498db;
    border-bottom: 1px solid #3498db;
}

        /* Dashboard */
        .dashboard {
            display: none;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
		
/* Force hide dashboard and all child elements when on login page */
		body:has(#loginPage[style*="display: flex"]) #dashboard,
		body:has(#loginPage[style*="display: flex"]) #dashboard * {
			display: none !important;
			pointer-events: none !important;
			visibility: hidden !important;
		}

        .header {
            background: #2c3e50;
            color: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .sync-status {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 8px 12px;
            border-radius: 20px;
            font-size: 12px;
            z-index: 1000;
            background: #27ae60;
            color: white;
        }

        /* Employee Boards */
        .employee-boards {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        .board {
            background: white;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .board-header {
            padding: 15px 20px;
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: 500;
        }

        .qa-board .board-header {
            background: #e74c3c;
        }

        .peer-board .board-header {
            background: #9b59b6;
        }

        .board-counter {
            background: rgba(255,255,255,0.2);
            padding: 4px 10px;
            border-radius: 15px;
            font-size: 12px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
		@keyframes spin {
			0% { transform: rotate(0deg); }
			100% { transform: rotate(360deg); }
		}
        .board-content {
            padding: 20px;
            max-height: 400px;
            overflow-y: auto;
        }

        .task-item {
            background: #f8f9fa;
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            border-left: 4px solid #007bff;
        }

        .task-item.urgent {
            border-left-color: #dc3545;
            background: #fff5f5;
        }

        .task-item.overdue {
            border-left-color: #ffc107;
            background: #fff8e1;
        }

        /* Toolbar */
        .toolbar {
            background: #34495e;
            color: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            display: flex;
            gap: 15px;
            align-items: center;
            flex-wrap: wrap;
        }

        .mic-btn {
            background: #e74c3c;
            color: white;
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            cursor: pointer;
            font-size: 20px;
        }

        .mic-btn.active {
            background: #27ae60;
            animation: pulse 1s infinite;
        }

        .tab {
            padding: 10px 20px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-right: 5px;
        }

        .tab.active {
            background: #27ae60;
        }

        .gender-btn {
            padding: 8px 15px;
            background: #95a5a6;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-left: 5px;
        }

        .gender-btn.active {
            background: #27ae60;
        }

        /* Main Container */
        .main-container {
            display: grid;
            grid-template-columns: 280px 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        .sidebar {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            height: fit-content;
        }

        .sidebar h3 {
            margin-bottom: 15px;
            color: #2c3e50;
            border-bottom: 2px solid #3498db;
            padding-bottom: 5px;
        }

        .template-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .template-item {
            padding: 10px;
            margin: 5px 0;
            background: #ecf0f1;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .template-item:hover {
            background: #3498db;
            color: white;
            transform: translateX(3px);
        }

        /* Category Styles */
        .category-header {
            background: #3498db;
            color: white;
            padding: 12px 15px;
            margin: 8px 0;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 14px;
            font-weight: 500;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .category-header:hover {
            background: #2980b9;
            transform: translateY(-1px);
        }

        .category-header.active {
            background: #27ae60;
        }

        .category-icon {
            font-size: 12px;
            transition: transform 0.3s ease;
            font-weight: bold;
        }

        .category-header.active .category-icon {
            transform: rotate(90deg);
        }

        .subcategory-list {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.4s ease-out, padding 0.3s ease;
            background: #f8f9fa;
            border-radius: 0 0 8px 8px;
            margin-bottom: 5px;
            border-left: 3px solid #3498db;
            margin-left: 8px;
        }

        .subcategory-list.expanded {
            max-height: 600px;
            padding: 12px 0;
        }

        .subcategory-item {
            padding: 10px 20px;
            margin: 3px 10px;
            background: white;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 13px;
            border-left: 3px solid transparent;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        .subcategory-item:hover {
            background: #3498db;
            color: white;
            transform: translateX(8px);
        }

        /* Editor */
        .editor-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .editor-toolbar {
            margin-bottom: 15px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 10px 15px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
        }

        .btn:hover {
            background: #2980b9;
        }

        .btn.format { background: #27ae60; }
        .btn.copy { background: #f39c12; }
        .btn.clear { background: #e74c3c; }

		.text-editor {
					width: 100%;
					height: 500px;
					padding: 20px;
					border: 2px solid #bdc3c7;
					border-radius: 8px;
					font-family: 'Courier New', monospace;
					font-size: 14px;
					line-height: 1.6;
					resize: vertical;
					overflow-wrap: break-word;
					word-wrap: break-word;
					white-space: pre-wrap;
					overflow-x: auto;
					text-align: left;
					direction: ltr;
					overflow-y: auto;
					pointer-events: none; /* DISABLE INTERACTION WHEN NOT LOGGED IN */
					user-select: none; /* PREVENT TEXT SELECTION */
				}

			.text-editor[contenteditable="true"] {
						pointer-events: auto; /* RE-ENABLE WHEN EDITABLE */
						user-select: text;
					}
					.text-editor:empty:before {
						content: attr(placeholder);
						color: #999;
						pointer-events: none;
					}
					
					.text-editor:focus {
						outline: none;
						border-color: #3498db;
					}

}

        /* HR Panels */
        .hr-panel {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        .hr-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .hr-tab {
            padding: 10px 20px;
            background: #95a5a6;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            position: relative;
        }

        .hr-tab.active {
            background: #3498db;
        }

        .hr-tab-counter {
            position: absolute;
            top: -8px;
            right: -8px;
            background: #e74c3c;
            color: white;
            border-radius: 10px;
            padding: 2px 6px;
            font-size: 10px;
            min-width: 16px;
            text-align: center;
        }
		
			.tab-counter {
				position: absolute;
				top: -8px;
				right: -8px;
				background: #e74c3c;
				color: white;
				border-radius: 10px;
				padding: 2px 6px;
				font-size: 10px;
				min-width: 16px;
				text-align: center;
			}

        /* Admin Panel */
        .admin-panel {
            display: none;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-top: 20px;
        }

        .admin-panel h2 {
            color: #e74c3c;
            margin-bottom: 20px;
            text-align: center;
        }

        .admin-sections {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
        }

        .admin-section {
            border: 2px solid #ecf0f1;
            border-radius: 8px;
            padding: 20px;
        }

        .admin-section h3 {
            color: #2c3e50;
            margin-bottom: 15px;
        }

        .admin-textarea {
            width: 100%;
            height: 300px;
            padding: 15px;
            border: 1px solid #bdc3c7;
            border-radius: 5px;
            font-family: 'Courier New', monospace;
            font-size: 12px;
            line-height: 1.4;
        }

        .save-btn {
            background: #27ae60;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
        }

        .save-btn:hover {
            background: #229954;
        }

        .logout-btn {
            background: #e74c3c;
            color: white;
            padding: 8px 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
		/* Critical Findings Alert */
		.critical-alert {
			position: fixed;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			background: linear-gradient(135deg, #e74c3c, #c0392b);
			color: white;
			padding: 25px 35px;
			border-radius: 12px;
			z-index: 10001;
			box-shadow: 0 10px 40px rgba(231, 76, 60, 0.5);
			font-size: 18px;
			font-weight: bold;
			text-align: center;
			border: 3px solid white;
			animation: criticalPulse 0.5s ease-in-out;
		}

		@keyframes criticalPulse {
			0%, 100% { transform: translate(-50%, -50%) scale(1); }
			50% { transform: translate(-50%, -50%) scale(1.05); }
		}

		.critical-alert-icon {
			font-size: 40px;
			margin-bottom: 10px;
		}
        /* Modals */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 10000;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 800px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        /* Notifications */
        .notification {
            position: fixed;
            top: 70px;
            right: 20px;
            background: #27ae60;
            color: white;
            padding: 15px 20px;
            border-radius: 5px;
            z-index: 9999;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            transform: translateX(400px);
            transition: transform 0.3s ease;
        }

        .notification.show {
            transform: translateX(0);
        }

        .status-bar {
            background: #2c3e50;
            color: white;
            padding: 10px 20px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* Statistics Cards */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-value {
            font-size: 32px;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 14px;
            opacity: 0.9;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .main-container {
                grid-template-columns: 1fr;
            }
            
            .employee-boards {
                grid-template-columns: 1fr;
            }
            
            .admin-sections {
                grid-template-columns: 1fr;
            }
        }
		/* Notes Board Styles */
.note-item {
    background: white;
    border: 1px solid #dee2e6;
    border-left: 4px solid #3498db;
    border-radius: 5px;
    padding: 12px;
    margin-bottom: 10px;
    font-size: 12px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.note-item.review {
    border-left-color: #e74c3c;
}

.note-item.other {
    border-left-color: #9b59b6;
}

.note-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
    padding-bottom: 8px;
    border-bottom: 1px solid #ecf0f1;
}

.note-category {
    display: inline-block;
    padding: 2px 8px;
    border-radius: 3px;
    font-size: 10px;
    font-weight: bold;
    color: white;
}

.note-category.review {
    background: #e74c3c;
}

.note-category.other {
    background: #9b59b6;
}

.note-timestamp {
    font-size: 10px;
    color: #6c757d;
}

.note-content {
    color: #212529;
    line-height: 1.4;
    white-space: pre-wrap;
    word-wrap: break-word;
}

.note-author {
    font-size: 10px;
    color: #6c757d;
    margin-top: 8px;
    padding-top: 8px;
    border-top: 1px solid #ecf0f1;
}

.note-actions {
    display: flex;
    gap: 5px;
    margin-top: 8px;
}

.note-actions button {
    padding: 4px 8px;
    font-size: 10px;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    color: white;
}

.note-edit-btn {
    background: #3498db;
}

.note-delete-btn {
    background: #e74c3c;
}
/* Completely disable text selection and interaction on login page */
.login-page * {
    pointer-events: none;
    user-select: none;
    cursor: default;
    -webkit-user-select: none;
    -moz-user-select: none;
}

/* Re-enable ONLY for interactive elements */
.login-page input,
.login-page button,
.login-page a {
    pointer-events: auto;
    user-select: auto;
    cursor: auto;
}

.login-page input {
    cursor: text;
}

.login-page button {
    cursor: pointer;
}
/* What's New Bell Notification */
.whats-new-bell {
    position: absolute;
    top: -8px;
    right: -8px;
    background: #e74c3c;
    color: white;
    border-radius: 50%;
    width: 24px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    animation: bellRing 1s ease-in-out infinite;
    box-shadow: 0 2px 8px rgba(231, 76, 60, 0.4);
    z-index: 10;
}

@keyframes bellRing {
    0%, 100% { transform: rotate(0deg); }
    10%, 30%, 50%, 70%, 90% { transform: rotate(-15deg); }
    20%, 40%, 60%, 80% { transform: rotate(15deg); }
}

.whats-new-bell.hidden {
    display: none;
}
.format-btn {
    padding: 6px 10px;
    border: 1px solid #ced4da;
    border-radius: 4px;
    background: white;
    cursor: pointer;
    font-size: 12px;
    transition: all 0.2s;
}

.format-btn:hover {
    background: #e9ecef;
    border-color: #3498db;
}

.format-btn:active {
    background: #dee2e6;
}

/* Fix for lists in contenteditable */
#textEditor ul, #textEditor ol {
    margin-left: 20px;
    padding-left: 20px;
}

#textEditor li {
    margin-left: 0;
    padding-left: 5px;
}
.shift-cell { overflow: visible; }
.shift-note-container { position: relative; display: flex; align-items: center; justify-content: space-between; gap: 4px; margin-top: 3px; padding: 3px 6px; background: rgba(155, 89, 182, 0.1); border-radius: 4px; font-size: 10px; }
.shift-note { flex: 1; color: #8e44ad; font-weight: 500; white-space: normal; word-wrap: break-word; max-width: 100px; }
.delete-note-btn { background: #e74c3c; color: white; border: none; border-radius: 3px; width: 16px; height: 16px; font-size: 14px; cursor: pointer; padding: 0; opacity: 0.7;  pointer-events: auto; z-index: 1000; }
.delete-note-btn:hover { opacity: 1; background: #c0392b; }
.shift-note-container[title]:hover::after { content: attr(title); position: absolute; bottom: 100%; left: 0; background: #2c3e50; color: white; padding: 6px 10px; border-radius: 5px; white-space: nowrap; font-size: 11px; z-index: 10001; margin-bottom: 5px; box-shadow: 0 2px 8px rgba(0,0,0,0.3); }

.reorder-employee-item {
    background: #f8f9fa;
    padding: 12px 15px;
    margin: 8px 0;
    border-radius: 6px;
    border: 2px solid #dee2e6;
    cursor: move;
    display: flex;
    align-items: center;
    gap: 10px;
    transition: all 0.2s;
}

.reorder-employee-item:hover {
    background: #e9ecef;
    border-color: #3498db;
}

.reorder-employee-item.dragging {
    opacity: 0.5;
    background: #3498db;
    color: white;
}

.reorder-drag-handle {
    font-size: 20px;
    color: #95a5a6;
}

.reorder-employee-name {
    flex: 1;
    font-weight: 600;
}

.reorder-employee-code {
    font-size: 12px;
    color: #7f8c8d;
    background: #e9ecef;
    padding: 3px 8px;
    border-radius: 4px;
}
    </style>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <!-- Sync Status Indicator -->
    <div class="sync-status" id="syncStatus">🟢 Online</div>

    <!-- Login Page -->
    <div id="loginPage" class="login-page">
        <div class="login-container">
            <h1>🏥 Radiology Templates</h1>
            
            <div id="empLogin">
				<form onsubmit="return handleEmpLogin(event)">
					<div class="form-group">
						<label for="empCode">Employee Code:</label>
						<input type="text" id="empCode" required placeholder="Enter your employee code" 
						autofocus
							   style="text-align: center; font-size: 18px; font-weight: bold;" maxlength="10">
					</div>
					<button type="submit" class="login-btn">Access System</button>
				</form>
				<div style="text-align: center; margin-top: 20px;">
					<small><a href="#" onclick="showAdminLogin()" style="color: #7f8c8d; text-decoration: none;">Admin Access</a></small>
				</div>
			</div>
            
            <div id="adminLogin" style="display: none;">
                <form onsubmit="return handleAdminLogin(event)">
                    <div class="form-group">
                        <label for="username">Admin Username:</label>
                        <input type="text" id="username" required>
                    </div>
                    <div class="form-group">
                        <label for="password">Admin Password:</label>
                        <input type="password" id="password" required>
                    </div>
                    <button type="submit" class="login-btn">Admin Login</button>
                </form>
                <div style="text-align: center; margin-top: 15px;">
                    <small><a href="#" onclick="showEmpLogin()" style="color: #7f8c8d; text-decoration: none;">← Back to Employee Access</a></small>
                </div>
            </div>
            
            <div id="errorMessage" class="error" style="display: none;"></div>
        </div>
    </div>

    <!-- Dashboard -->
    <div id="dashboard" class="dashboard">
        <!-- Header -->
        <div class="header">
    <div>
        <h1 id="welcomeText">Welcome, User</h1>
	<div style="font-size: 11px; color: rgba(255,255,255,0.6); margin-top: 5px; display: flex; align-items: center; gap: 10px;">
            <span>v<strong id="appVersion">...</strong></span>
            <button id="updateAvailableBtn" onclick="userChooseUpdate()" style="display: none; background: #27ae60; color: white; border: none; padding: 4px 12px; border-radius: 12px; font-size: 11px; cursor: pointer; animation: pulse 2s infinite;">
                ✨ Update Available
            </button>
			</div>
        </div>
		<div style="display: flex; gap: 10px; align-items: center;">		
			<div style="position: relative;">
				<button id="toolsBtn" class="btn" onclick="toggleToolsDropdown()" style="background: #9b59b6; display: none;">
					🔧 Tools ▼
				</button>
				<!-- What's New Button -->
<div style="position: relative; display: inline-block;">
    <button id="whatsNewBtn" class="btn" onclick="toggleWhatsNewDropdown()" style="background: #00a86b; display: inline-block; position: relative;">
    ✨ What's New
    <span id="whatsNewBell" class="whats-new-bell hidden">🔔</span>
	</button>
    <div id="whatsNewDropdown" style="display: none; position: absolute; top: 45px; right: 0; background: white; border: 2px solid #00a86b; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); z-index: 1000; min-width: 350px; max-width: 450px; max-height: 500px; overflow-y: auto;">
        <!-- Header -->
        <div style="background: linear-gradient(135deg, #00a86b 0%, #008f5a 100%); color: white; padding: 15px 20px; border-radius: 10px 10px 0 0; display: flex; justify-content: space-between; align-items: center;">
            <div style="font-weight: bold; font-size: 16px;">✨ What's New</div>
            <button onclick="toggleWhatsNewDropdown()" style="background: none; border: none; color: white; font-size: 20px; cursor: pointer; padding: 0; width: 24px; height: 24px;">×</button>
        </div>
        
        <!-- Content Area -->
        <div id="whatsNewContent" style="padding: 20px; min-height: 150px; color: #2c3e50; line-height: 1.6;">
            <div style="text-align: center; color: #999; padding: 40px 20px;">
                <div style="font-size: 32px; margin-bottom: 10px;">📢</div>
                <div style="font-size: 14px;">No announcements yet</div>
            </div>
        </div>
        
        <!-- Admin Edit Section (Hidden by default) -->
        <div id="whatsNewEditSection" style="display: none; border-top: 2px solid #e0e0e0; padding: 15px 20px; background: #f8f9fa;">
            <textarea id="whatsNewEditor" style="width: 100%; height: 200px; padding: 12px; border: 2px solid #e0e0e0; border-radius: 8px; font-size: 13px; font-family: inherit; resize: vertical;" placeholder="Enter announcement here...&#10;&#10;Supports:&#10;• Bullet points&#10;• Line breaks&#10;• Simple text formatting"></textarea>
            <div style="display: flex; gap: 10px; margin-top: 10px;">
                <button onclick="saveWhatsNew()" style="flex: 1; background: #00a86b; color: white; border: none; padding: 10px; border-radius: 8px; cursor: pointer; font-weight: 600;">💾 Save</button>
                <button onclick="cancelWhatsNewEdit()" style="flex: 1; background: #6c757d; color: white; border: none; padding: 10px; border-radius: 8px; cursor: pointer; font-weight: 600;">Cancel</button>
            </div>
        </div>
        
        <!-- Admin Edit Button (Visible only to admins) -->
        <div id="whatsNewAdminControls" style="display: none; border-top: 2px solid #e0e0e0; padding: 12px 20px; background: #fff;">
            <button onclick="startEditWhatsNew()" style="width: 100%; background: #0066cc; color: white; border: none; padding: 10px; border-radius: 8px; cursor: pointer; font-weight: 600;">✏️ Edit Announcement</button>
        </div>
        
        <!-- Footer -->
        <div style="background: #f8f9fa; padding: 10px 20px; border-top: 1px solid #e0e0e0; border-radius: 0 0 10px 10px; text-align: center; font-size: 11px; color: #666;">
            Last updated: <span id="whatsNewLastUpdated">Never</span>
        </div>
    </div>
</div>
				<div id="toolsDropdown" style="display: none; position: absolute; top: 45px; right: 0; background: white; border: 2px solid #9b59b6; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); z-index: 1000; min-width: 200px;">
					<div onclick="openAdvancedSearch(); closeToolsDropdown();" style="padding: 12px 20px; cursor: pointer; border-bottom: 1px solid #ecf0f1; transition: background 0.2s; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#f8f9fa'" onmouseout="this.style.background='white'">
						🔍 Advanced Search
					</div>
					<div onclick="openTicketModal(); closeToolsDropdown();" style="padding: 12px 20px; cursor: pointer; border-bottom: 1px solid #ecf0f1; transition: background 0.2s; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#f8f9fa'" onmouseout="this.style.background='white'">
						🎫 Report Issue
					</div>
					<div onclick="openMyFiles(); closeToolsDropdown();" style="padding: 12px 20px; cursor: pointer; transition: background 0.2s; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#f8f9fa'" onmouseout="this.style.background='white'">
						📁 My Files
					</div>
				</div>
			</div>
			<button class="logout-btn" onclick="logout()">Logout</button>
			<button id="adminBtn" class="btn" onclick="showAdminPanel()" style="display: none;">Admin Panel</button>
		</div>
	</div>

<!-- Employee Boards (Full Width) -->
			<div id="qaBoard" class="hr-panel" style="display: none;">
				<h3>QA Board</h3>
				<div id="qaContent">
					<div style="text-align: center; color: #666; padding: 20px;">No QA assignments</div>
				</div>
			</div>

			<div id="peerBoard" class="hr-panel" style="display: none;">
				<h3>Peer Review Board</h3>
				<div id="peerContent">
					<div style="text-align: center; color: #666; padding: 20px;">No peer reviews</div>
				</div>
			</div>

		<!-- Employee Toolbar -->
		<div class="toolbar" id="empToolbar" style="display: none;">
		<button class="mic-btn" id="micBtn" onclick="toggleMic()" title="Voice Input">🎤</button>
		<span id="micStatus">Voice Ready</span>
		
		<button class="btn" onclick="startTutorial()" title="Help & Tutorial" 
				style="background: #9b59b6; border-radius: 50%; width: 40px; height: 40px;">?</button>
    
			<div>
			<button class="tab" data-tab="QABoard" onclick="selectTab('QABoard')">
				QA Board <span id="empQACounter" style="display: none;"></span>
			</button>
			<button class="tab" data-tab="PeerBoard" onclick="selectTab('PeerBoard')">
				Peer Review Board <span id="empPeerCounter" style="display: none;"></span>
			</button>
			
			<select id="modalityDropdown" onchange="selectModalityFromDropdown(this.value)" 
					style="padding: 10px 20px; background: #3498db; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 14px; font-weight: 500; margin-right: 5px;">
				<option value="">Templates</option>
				<option value="US">US</option>
				<option value="CT">CT</option>
				<option value="MRI">MRI</option>
				<option value="XR">X-Ray</option>
				<option value="Biotronics">Biotronics</option>
			</select>
			
			<!-- NEW EVENTS DROPDOWN FOR EMPLOYEES -->
			<div style="display: inline-block; position: relative;">
				<button class="btn" onclick="toggleEmpEventsDropdown()" id="empEventsBtn" style="background: #27ae60; position: relative;">
					📅 Events
					<span id="empEventsNotification" style="display: none; position: absolute; top: -8px; right: -8px; background: #e74c3c; color: white; border-radius: 50%; width: 20px; height: 20px; font-size: 10px; font-weight: bold; align-items: center; justify-content: center;">0</span>
				</button>
				<div id="empEventsDropdown" style="display: none; position: absolute; top: 45px; left: 0; background: white; border: 2px solid #27ae60; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); z-index: 1000; min-width: 200px;">
					<div onclick="selectTab('Schedule')" style="padding: 12px 20px; cursor: pointer; border-bottom: 1px solid #ecf0f1; transition: all 0.2s; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#3498db'; this.style.color='white';" onmouseout="this.style.background='white'; this.style.color='#2c3e50';">
						📅 My Schedule
					</div>
					<div onclick="selectTab('Meetings')" style="padding: 12px 20px; cursor: pointer; transition: all 0.2s; position: relative; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#3498db'; this.style.color='white';" onmouseout="this.style.background='white'; this.style.color='#2c3e50';">
						🔔 Meetings
						<span id="empMeetingDropdownBadge" style="display: none; position: absolute; right: 10px; top: 50%; transform: translateY(-50%); background: #e74c3c; color: white; padding: 2px 8px; border-radius: 10px; font-size: 10px; font-weight: bold;">0</span>
					</div>
				</div>
			</div>
		</div>
				
    <div>
        Gender:
        <button class="gender-btn active" id="maleBtn" onclick="selectGender('male')">♂ Male</button>
        <button class="gender-btn" id="femaleBtn" onclick="selectGender('female')">♀ Female</button>
    </div>
</div>

        <!-- HR Toolbar -->
        <div class="toolbar" id="hrToolbar" style="display: none;">
            <div class="hr-tabs">
                <button class="hr-tab active" onclick="selectHRTab('QA')">
                    QA Management
                    <span class="hr-tab-counter" id="hrQACounter" style="display: none;">0</span>
                </button>
                <button class="hr-tab" onclick="selectHRTab('PeerReview')">
                    Peer Review
                    <span class="hr-tab-counter" id="hrPeerCounter" style="display: none;">0</span>
                </button>
				<button class="hr-tab" onclick="selectHRTab('Reports')">📊 Reports Dashboard</button>
				<button class="hr-tab" onclick="selectHRTab('TimeLogs')">⏱️ Time Logs</button>
				<button class="hr-tab" onclick="selectHRTab('BodyPartRules')" id="bodyPartRulesTab" style="background: #9b59b6;">⚙️ Body Part Rules</button>
				<!-- NEW EVENTS DROPDOWN FOR HR -->
				<div style="display: inline-block; position: relative; margin-left: 10px;">
					<button class="hr-tab" onclick="toggleHREventsDropdown()" id="hrEventsBtn" style="background: #27ae60; position: relative;">
						📅 Events
						<span id="hrEventsNotification" style="display: none; position: absolute; top: -8px; right: -8px; background: #e74c3c; color: white; border-radius: 50%; width: 20px; height: 20px; font-size: 10px; font-weight: bold; display: flex; align-items: center; justify-content: center;">0</span>
					</button>
					<div id="hrEventsDropdown" style="display: none; position: absolute; top: 45px; left: 0; background: white; border: 2px solid #27ae60; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); z-index: 1000; min-width: 220px;">
						<div onclick="selectHRTab('Schedule')" style="padding: 12px 20px; cursor: pointer; border-bottom: 1px solid #ecf0f1; transition: all 0.2s; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#3498db'; this.style.color='white';" onmouseout="this.style.background='white'; this.style.color='#2c3e50';">
							📅 Schedule Management
						</div>
						<div onclick="selectHRTab('Meetings')" style="padding: 12px 20px; cursor: pointer; transition: all 0.2s; color: #2c3e50; font-weight: 500;" onmouseover="this.style.background='#3498db'; this.style.color='white';" onmouseout="this.style.background='white'; this.style.color='#2c3e50';">
							🔔 Meeting Management
						</div>
					</div>
				</div>
            </div>
        </div>

<div class="main-container" id="mainContainer" style="display: none;">
<!-- Sidebar -->
    <div class="sidebar" id="templateSidebar">
<!-- NOTES BOARD SECTION -->
        <div style="background: #fff3cd; border: 2px solid #f39c12; border-radius: 8px; padding: 12px; margin-bottom: 20px; cursor: pointer; transition: all 0.3s;" 
             onclick="openNotesBoard()" 
             onmouseover="this.style.background='#ffe5a0'" 
             onmouseout="this.style.background='#fff3cd'"
             id="notesBoardButton"
             style="display: none;">
            <div style="display: flex; justify-content: space-between; align-items: center;">
                <h3 style="margin: 0; color: #856404; font-size: 14px;">📝 Notes Board</h3>
                <span id="notesCounter" style="background: #f39c12; color: white; padding: 4px 8px; border-radius: 10px; font-size: 11px; font-weight: bold; display: none;">0</span>
            </div>
            <div style="font-size: 11px; color: #856404; margin-top: 5px;">Click to view notes</div>
        </div>
        
<!-- Template Search Bar -->
        <div style="background: #e3f2fd; padding: 12px; margin-bottom: 15px; border: 2px solid #3498db; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
            <input type="text" id="templateSearch" placeholder="Search templates... (Ctrl+K)" 
                   style="width: 100%; padding: 10px 12px; border: 1px solid #90caf9; border-radius: 5px; font-size: 14px; outline: none;"
                   onkeyup="searchTemplates(event)">
            <div id="searchResults" style="display: none; max-height: 320px; overflow-y: auto; margin-top: 8px; border: 1px solid #90caf9; border-radius: 5px; background: white; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"></div>
        </div>
        
        <h3>Recent Templates</h3>
        <ul id="recentList" class="template-list">
            <li class="template-item" onclick="loadTemplate('us_abdomen')">US Abdomen</li>
            <li class="template-item" onclick="loadTemplate('us_pelvis')">US Pelvis</li>
        </ul>

        <h3 id="categoryTitle">US Templates</h3>
        <ul id="templateList" class="template-list">
            <!-- Templates will be loaded dynamically -->
        </ul>
    </div>

 <div class="editor-container" id="editorContainer">
 
     <!-- Main Toolbar Row 1: Primary Actions -->
	 
<div style="display: flex; gap: 10px; margin-bottom: 10px; flex-wrap: wrap; align-items: center;">
    <button class="btn format" onclick="formatReport()" style="flex: 0 0 auto;">📝 Format</button>
    <button class="btn" onclick="generateAIRecommendations()" style="background: #9b59b6; flex: 0 0 auto;">🤖 AI</button>
    <button class="btn copy" onclick="copyToClipboard()" style="flex: 0 0 auto;">📋 Copy</button>
    
    <select id="reportCountSelector" style="padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-size: 14px; width: 60px; font-weight: bold; flex: 0 0 auto;">
        <!-- Populated by JS -->
    </select>
    
    <button id="copyAndCountBtn" class="btn" onclick="copyAndCount()" 
            style="background: #27ae60; padding: 10px 15px; font-size: 14px; font-weight: bold; flex: 0 0 auto;">
        📊 Copy & Count (<span id="reportCounter">0</span>)
    </button>
    
    <select id="institutionDropdown" style="padding: 10px 15px; border: 2px solid #3498db; border-radius: 5px; cursor: pointer; font-size: 14px; background: white; flex: 1 1 200px; min-width: 150px;">
        <option value="">Select Institution</option>
    </select>
	<input type="text" id="accessionNumber" placeholder="Accession No. (required)" 
       style="padding: 10px 15px; border: 2px solid #3498db; border-radius: 5px; font-size: 14px; margin-right: 5px; width: 200px;">
    
    <button class="btn clear" onclick="clearEditor()" style="flex: 0 0 auto;">🗑️ Clear</button>
</div>

<!-- Submission Row -->
<div style="background: #f8f9fa; padding: 12px; margin-bottom: 10px; border-radius: 8px; border: 2px solid #e9ecef; display: flex; gap: 15px; align-items: center; flex-wrap: wrap;">
    <div style="flex: 1 1 250px;">
        <label style="font-weight: 500; color: #495057; display: flex; align-items: center;">
            <input type="checkbox" id="peerReviewCheck" style="margin-right: 8px; transform: scale(1.3); cursor: pointer;">
            Submit for Peer Review
        </label>
        <input type="text" id="peerReviewAccession" placeholder="Enter accession number"
               style="width: 100%; margin-top: 5px; padding: 8px; border: 1px solid #ced4da; border-radius: 4px; font-size: 13px;" disabled>
    </div>
    
    <button class="btn" onclick="submitForReview()" 
            style="background: #28a745; padding: 10px 20px; font-size: 14px; font-weight: bold; flex: 0 0 auto;">
        📤 Submit
    </button>
</div>

<!-- Formatting Toolbar -->
<div style="background: #f8f9fa; padding: 10px; margin-bottom: 10px; border-radius: 8px; border: 1px solid #dee2e6;">
    <div style="display: flex; gap: 8px; flex-wrap: wrap; align-items: center; justify-content: space-between;">
        
        <!-- Formatting Controls -->
        <div style="display: flex; gap: 6px; align-items: center;">
            <select id="fontSize" onchange="changeFontSize()" title="Font Size" 
                    style="padding: 6px; border: 1px solid #ced4da; border-radius: 4px; font-size: 12px; cursor: pointer; width: 60px;">
                <option value="12">12px</option>
                <option value="14" selected>14px</option>
                <option value="16">16px</option>
                <option value="18">18px</option>
            </select>
            
            <button onclick="formatText('bold')" title="Bold" class="format-btn"><strong>B</strong></button>
            <button onclick="formatText('italic')" title="Italic" class="format-btn"><em>I</em></button>
            <button onclick="formatText('underline')" title="Underline" class="format-btn" style="text-decoration: underline;">U</button>
            
            <div style="width: 1px; height: 20px; background: #ced4da; margin: 0 4px;"></div>
            
            <button onclick="formatText('justifyLeft')" title="Left" class="format-btn">⬅️</button>
            <button onclick="formatText('justifyCenter')" title="Center" class="format-btn">↔️</button>
            <button onclick="formatText('justifyRight')" title="Right" class="format-btn">➡️</button>
            
            <div style="width: 1px; height: 20px; background: #ced4da; margin: 0 4px;"></div>
            
            <button onclick="insertBulletList()" title="Bullets" class="format-btn">• List</button>
            <button onclick="insertNumberList()" title="Numbers" class="format-btn">1. List</button>
            
            <div style="width: 1px; height: 20px; background: #ced4da; margin: 0 4px;"></div>
            
            <button onclick="textToUpperCase()" title="UPPERCASE" class="format-btn" style="font-size: 10px;">AB</button>
            <button onclick="textToLowerCase()" title="lowercase" class="format-btn" style="font-size: 10px;">ab</button>
        </div>
        
        <!-- Draft Controls -->
        <div style="display: flex; gap: 6px; align-items: center;">
            <select id="autoSaveInterval" onchange="updateAutoSavePreference()" 
                    style="padding: 5px 8px; border: 1px solid #ced4da; border-radius: 4px; font-size: 11px; cursor: pointer;">
                <option value="0">No Auto-save</option>
                <option value="15">15s</option>
                <option value="30" selected>30s</option>
                <option value="60">60s</option>
                <option value="120">2min</option>
            </select>
            
            <button onclick="saveDraft(false)" title="Save Draft" 
                    style="background: #17a2b8; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer; font-size: 11px; font-weight: bold;">
                💾 Save
            </button>
            
            <div style="position: relative; display: inline-block;">
    <button id="loadDraftBtn" title="Load Saved Draft" 
            onmouseenter="showDraftMenu()" 
            style="background: #6c757d; color: white; border: none; padding: 6px 10px; border-radius: 5px; cursor: pointer; font-size: 11px; font-weight: bold;">
        📂 Load ▼
    </button>
    
    <div id="draftMenu" 
         onmouseleave="this.style.display='none'"
         style="display:none; position:absolute; top:100%; right:0; margin-top:2px; background:white; 
                border:1px solid #ccc; border-radius:5px; box-shadow:0 2px 8px rgba(0,0,0,0.15); 
                min-width:300px; max-width:400px; z-index:1000;">
    </div>
</div>
            
            <span id="autoSaveIndicator" style="font-size: 11px; color: #28a745; opacity: 0; transition: opacity 0.3s; font-weight: bold;">✓</span>
            <span id="lastSavedTime" style="font-size: 10px; color: #6c757d; display: none;"></span>
        </div>
    </div>
</div>


  <!-- Text Editor -->
  <div class="text-editor" id="textEditor" contenteditable="false"
		style="font-family: 'Courier New', monospace; font-size: 14px; line-height: 1.6; padding: 20px; padding-left: 40px;">            <br>
        </div>
    </div>
</div>
<!-- Employee Meetings Panel -->
<div id="empMeetingsPanel" class="hr-panel" style="display: none;">
    <div class="schedule-header">
        <h2>📅 My Meetings</h2>
    </div>
    
    <div id="empUpcomingMeetingsList">
        <div style="padding: 40px; text-align: center; color: #666;">No upcoming meetings scheduled</div>
    </div>
</div>

<!-- HR Time Logs Panel -->
<div id="hrTimeLogsPanel" style="display: none; padding: 20px;">
    <div style="background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">
        <h2>⏱️ Employee Time Logs & Work Sessions</h2>
        
        <!-- Filters -->
        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin: 20px 0; padding: 15px; background: #f8f9fa; border-radius: 8px;">
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Employee:</label>
                <select id="timeLogEmpFilter" onchange="filterTimeLogs()" style="width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ddd;">
                    <option value="">All Employees</option>
                </select>
            </div>
			<!--
			<div>
				<label style="font-size: 12px; margin-bottom: 5px; display: block;">Institution:</label>
				<select id="timeLogsFilterInstitution" onchange="filterTimeLogs()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
					<option value="">All Institutions</option>
				</select>
			</div>
			-->
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">From Date:</label>
                <input type="date" id="timeLogFromDate" onchange="filterTimeLogs()" style="width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ddd;">
            </div>
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">To Date:</label>
                <input type="date" id="timeLogToDate" onchange="filterTimeLogs()" style="width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ddd;">
            </div>
            <div style="display: flex; align-items: flex-end;">
                <button onclick="exportTimeLogs()" class="btn" style="background: #27ae60; width: 100%;">📊 Export CSV</button>
            </div>
        </div>
        
        <!-- Summary Cards -->
        <div id="timeLogSummary" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
            <!-- Summary cards will be populated here -->
        </div>
        
        <!-- Time Logs Table -->
        <div style="overflow-x: auto;">
            <table style="width: 100%; border-collapse: collapse; font-size: 13px;">
                <thead style="background: #34495e; color: white; position: sticky; top: 0;">
                    <tr>
						<th style="padding: 12px; text-align: center; width: 40px;"></th>
						<th style="padding: 12px; text-align: left;">Employee</th>
						<th style="padding: 12px; text-align: center;">First Login</th>
						<th style="padding: 12px; text-align: center;">Last Logout</th>
						<th style="padding: 12px; text-align: center;">Total Time</th>
						<th style="padding: 12px; text-align: center;">Idle Time</th>
						<th style="padding: 12px; text-align: center;">Active Work</th>
						<th style="padding: 12px; text-align: center;">Scheduled Regular</th>
						<th style="padding: 12px; text-align: center;">Scheduled Extra</th>
						<th style="padding: 12px; text-align: center;">Cases (Regular)</th>
						<th style="padding: 12px; text-align: center;">Cases (Extra)</th>
						<th style="padding: 12px; text-align: center;">Actions</th>
                    </tr>
                </thead>
                <tbody id="timeLogsTableBody">
                    <tr><td colspan="9" style="text-align: center; padding: 20px; color: #7f8c8d;">Loading time logs...</td></tr>
                </tbody>
            </table>
            <div id="paginationInfo" style="display: none; padding: 10px; text-align: center; color: #7f8c8d; font-size: 13px; background: #f8f9fa; border-top: 1px solid #ddd;">
                Showing 1-15 of 47 results
            </div>
            
            <!-- Pagination Controls -->
            <div id="paginationControls" style="display: none; padding: 15px; background: #f8f9fa; border-top: 1px solid #ddd; justify-content: center; align-items: center;">
                <!-- Controls will be populated by JavaScript -->
            </div>
        </div>
    </div>
</div>
<!-- HR Password Management Panel -->
<div id="passwordManagementPanel" class="hr-panel" style="display: none;">
    <h3>🔐 Password Management</h3>
    <div id="passwordManagementContent">
        <!-- Content loads here -->
    </div>
</div>
<!-- Body Part Rules Panel -->
<div id="bodyPartRulesPanel" style="display: none; padding: 20px;">
    <div style="background: white; padding: 25px; border-radius: 10px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
            <h3 style="margin: 0; color: #2c3e50;">⚙️ Body Part Counting Rules</h3>
            <button onclick="showAddRuleModal()" class="btn" style="background: #27ae60;">
                ➕ Add New Rule
            </button>
        </div>
        
        <div id="rulesListContainer">
            <!-- Rules will be loaded here -->
        </div>
    </div>
    
    <!-- Unmatched Reports Queue -->
    <div style="background: white; padding: 25px; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <h3 style="margin: 0 0 20px 0; color: #2c3e50;">🚩 Unmatched Reports Queue</h3>
        <div id="unmatchedReportsContainer">
            <!-- Unmatched reports will be loaded here -->
        </div>
    </div>
</div>
<!-- HR Reports Dashboard Panel -->
<div id="hrReportsPanel" style="display: none;">
    <!-- Statistics Cards -->
    <div style="background: white; padding: 20px; border-radius: 10px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <h3 style="margin: 0 0 20px 0; color: #2c3e50;">📊 Today's Report Statistics</h3>
        <div style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 20px;">
            <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 10px; color: white;">
                <div style="font-size: 36px; font-weight: bold;" id="totalReportsCount">0</div>
                <div style="font-size: 14px; opacity: 0.9;">Total Reports</div>
            </div>
            <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); border-radius: 10px; color: white;">
                <div style="font-size: 36px; font-weight: bold;" id="usReportsCount">0</div>
                <div style="font-size: 14px; opacity: 0.9;">US Reports</div>
            </div>
            <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); border-radius: 10px; color: white;">
                <div style="font-size: 36px; font-weight: bold;" id="ctReportsCount">0</div>
                <div style="font-size: 14px; opacity: 0.9;">CT Reports</div>
            </div>
				<div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); border-radius: 10px; color: white;">
				<div style="font-size: 36px; font-weight: bold;" id="xrReportsCount">0</div>
				<div style="font-size: 14px; opacity: 0.9;">X-Ray Reports</div>
			</div>
            <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); border-radius: 10px; color: white;">
                <div style="font-size: 36px; font-weight: bold;" id="mriReportsCount">0</div>
                <div style="font-size: 14px; opacity: 0.9;">MRI Reports</div>
            </div>
        </div>
    </div>
    
    <!-- Filter Bar -->
    <div style="background: white; padding: 20px; border-radius: 10px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <div style="display: grid; grid-template-columns: repeat(7, 1fr); gap: 15px; margin-bottom: 15px;">
			<div>
				<label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">From Date:</label>
				<input type="date" id="reportsFilterFrom" onchange="applyReportsFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
			</div>
			<div>
				<label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">From Time:</label>
				<input type="time" id="reportsFilterFromTime" onchange="applyReportsFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
			</div>
			<div>
				<label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">To Date:</label>
				<input type="date" id="reportsFilterTo" onchange="applyReportsFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
			</div>
			<div>
				<label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">To Time:</label>
				<input type="time" id="reportsFilterToTime" onchange="applyReportsFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
			</div>
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">Radiologist:</label>
                <select id="reportsFilterRad" onchange="applyReportsFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
                    <option value="">All Radiologists</option>
                </select>
            </div>
			<div>
				<label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">
					Institution:
				</label>
				<select id="filterInstitution" onchange="applyReportsFilters()"
						style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
					<option value="">All Institutions</option>
				</select>
			</div>
			<div>
				<label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">
					Accession No:
				</label>
				<input type="text" id="filterAccession" onchange="applyReportsFilters()" placeholder="Search accession..."
					   style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
			</div>

            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500; font-size: 13px;">Modality:</label>
                <select id="reportsFilterModality" onchange="applyReportsFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
                    <option value="">All Modalities</option>
                    <option value="US">Ultrasound</option>
                    <option value="CT">CT Scan</option>
                    <option value="MRI">MRI</option>
                    <option value="XR">X-Ray</option>
                    <option value="Biotronics">Biotronics</option>
                </select>
            </div>
        </div>
        <div style="display: flex; gap: 10px;">
            <input type="text" id="reportsSearchText" placeholder="🔍 Search within reports..." onkeyup="applyReportsFilters()" style="flex: 1; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
            <button onclick="applyReportsFilters()" class="btn" style="background: #3498db;">🔄 Refresh</button>
            <button onclick="clearReportsFilters()" class="btn" style="background: #95a5a6;">❌ Clear</button>
        </div>
    </div>
    
    <!-- Bulk Action Bar (appears when items selected) -->
    <div id="bulkActionBar" style="display: none; background: #f39c12; color: white; padding: 15px 20px; border-radius: 10px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <div style="display: flex; justify-content: space-between; align-items: center;">
            <div style="font-weight: bold; font-size: 16px;">
                ☑ <span id="selectedReportsCount">0</span> Selected
            </div>
            <div style="display: flex; gap: 10px;">
                <button onclick="exportSelectedReports()" class="btn" style="background: #27ae60;">📥 Export Selected</button>
                <button onclick="deleteSelectedReports()" class="btn" style="background: #e74c3c;">🗑️ Delete Selected</button>
                <button onclick="deselectAllReports()" class="btn" style="background: #95a5a6;">❌ Deselect All</button>
            </div>
        </div>
    </div>
    
    <!-- Reports Table -->
    <div style="background: white; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); overflow: hidden;">
        <div style="background: #2c3e50; color: white; padding: 15px 20px; display: flex; justify-content: space-between; align-items: center;">
            <h4 style="margin: 0;">Report List (<span id="reportsShowingCount">0</span> of <span id="reportsTotalCount">0</span>)</h4>
            <button onclick="exportAllReports()" class="btn" style="background: #27ae60; padding: 8px 15px; font-size: 13px;">📥 Export All</button>
        </div>
        <div style="overflow-x: auto; max-height: 600px; overflow-y: auto;">
            <table style="width: 100%; border-collapse: collapse; font-size: 13px; min-width: 1200px;">
                <thead style="position: sticky; top: 0; background: #34495e; color: white; z-index: 10;">
                    <tr>
                        <th style="padding: 12px; text-align: center; width: 50px;">
                            <input type="checkbox" id="selectAllReportsCheckbox" onchange="toggleSelectAllReports()" style="transform: scale(1.3);">
                        </th>
                        <th style="padding: 12px; text-align: left;">Time</th>
                        <th style="padding: 12px; text-align: left;">Radiologist</th>
						<th style="padding: 12px; text-align: center;">Institution</th>
						<th style="padding: 12px; text-align: center;">Accession</th>
                        <th style="padding: 12px; text-align: center;">Modality</th>
                        <th style="padding: 12px; text-align: center;">Words</th>
                        <th style="padding: 12px; text-align: center;">Type</th>
                        <th style="padding: 12px; text-align: center;">Actions</th>
                    </tr>
                </thead>
                <tbody id="reportsTableBody">
                    <tr>
                        <td colspan="8" style="padding: 60px; text-align: center; color: #666;">
                            Loading reports...
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<!-- HR Meetings Panel -->
<div id="hrMeetingsPanel" class="hr-panel" style="display: none;">
    <div class="schedule-header">
        <h2>🔔 Meeting Management</h2>
        <button class="btn" onclick="openCreateMeetingModal()" style="background: #27ae60; padding: 12px 24px; font-weight: bold;">
            ➕ Create New Meeting
        </button>
    </div>
    
    <!-- Meeting Statistics Dashboard -->
    <div class="hr-meeting-dashboard">
        <div class="hr-meeting-stat-card">
            <div class="meeting-stat-label">Total Meetings</div>
            <div class="meeting-stat-value" id="hrTotalMeetings">0</div>
        </div>
        <div class="hr-meeting-stat-card pending">
            <div class="meeting-stat-label">Pending Responses</div>
            <div class="meeting-stat-value" id="hrPendingResponses">0</div>
        </div>
        <div class="hr-meeting-stat-card upcoming">
            <div class="meeting-stat-label">Upcoming</div>
            <div class="meeting-stat-value" id="hrUpcomingMeetings">0</div>
        </div>
        <div class="hr-meeting-stat-card completed">
            <div class="meeting-stat-label">Completed</div>
            <div class="meeting-stat-value" id="hrCompletedMeetings">0</div>
        </div>
    </div>
	
    <!-- Advanced Filters -->
	<div style="background: #f8f9fa; padding: 20px; border-radius: 10px; margin: 20px 0;">
    <h4 style="margin: 0 0 15px 0; color: #2c3e50;">🔍 Search & Filter Meetings</h4>
    
    <div style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 15px; margin-bottom: 15px;">
        <div>
            <label style="font-size: 12px; margin-bottom: 5px; display: block;">From Date:</label>
            <input type="date" id="meetingFilterFrom" onchange="applyMeetingFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
        </div>
        <div>
            <label style="font-size: 12px; margin-bottom: 5px; display: block;">To Date:</label>
            <input type="date" id="meetingFilterTo" onchange="applyMeetingFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
        </div>
        <div>
            <label style="font-size: 12px; margin-bottom: 5px; display: block;">Organizer:</label>
            <select id="meetingFilterOrganizer" onchange="applyMeetingFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                <option value="">All Organizers</option>
                ${Object.entries(authorizedEmployees)
                    .filter(([code, emp]) => emp.role === 'hr' || emp.role === 'admin')
                    .map(([code, emp]) => `<option value="${code}">${emp.name}</option>`)
                    .join('')}
            </select>
        </div>
        <div>
            <label style="font-size: 12px; margin-bottom: 5px; display: block;">Type:</label>
            <select id="meetingFilterType" onchange="applyMeetingFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                <option value="">All Types</option>
                <option value="QA Review">QA Review</option>
                <option value="Training">Training</option>
                <option value="Department Meeting">Department Meeting</option>
                <option value="Emergency">Emergency</option>
                <option value="Other">Other</option>
            </select>
        </div>
        <div>
            <label style="font-size: 12px; margin-bottom: 5px; display: block;">Search Title:</label>
            <input type="text" id="meetingFilterSearch" placeholder="Search..." onkeyup="applyMeetingFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
        </div>
    </div>
    
    <div style="display: flex; gap: 10px;">
        <button onclick="clearMeetingFilters()" style="background: #95a5a6; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">Clear Filters</button>
        <button onclick="exportAllMeetingsToExcel()" style="background: #27ae60; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">📥 Export to Excel</button>
    </div>
</div>
    <!-- Meeting Tabs -->
    <div style="display: flex; gap: 10px; margin: 20px 0; border-bottom: 2px solid #ecf0f1;">
        <button class="btn active" id="hrMeetingTabUpcoming" onclick="switchHRMeetingTab('upcoming')" style="background: #3498db; border-radius: 8px 8px 0 0;">
            Upcoming
        </button>
        <button class="btn" id="hrMeetingTabPending" onclick="switchHRMeetingTab('pending')" style="background: #95a5a6; border-radius: 8px 8px 0 0;">
            Pending Responses
        </button>
        <button class="btn" id="hrMeetingTabCompleted" onclick="switchHRMeetingTab('completed')" style="background: #95a5a6; border-radius: 8px 8px 0 0;">
            Completed
        </button>
    </div>
    
    <!-- Meeting List Container -->
    <div id="hrMeetingListContainer" style="min-height: 300px;">
        <!-- Meeting list will load here -->
    </div>
</div>

<!-- Employee Schedule View -->
<div id="empSchedulePanel" class="schedule-panel" style="display: none;">
    <div class="schedule-header">
        <h2>📅 My Schedule</h2>
        <button class="btn" onclick="requestLeave()" style="background: #9b59b6;">
            ✈️ Request Leave
        </button>
    </div>
    
<!-- Leave Summary -->
    <div class="leave-summary">
        <div class="leave-card">
            <div class="leave-label">Total Annual Leave</div>
            <div class="leave-value" id="empTotalLeave">30</div>
            <div class="leave-label">days/year</div>
        </div>
        <div class="leave-card used">
            <div class="leave-label">Used Leave</div>
            <div class="leave-value" id="empUsedLeave">0</div>
            <div class="leave-label">days</div>
        </div>
        <div class="leave-card pending">
            <div class="leave-label">Pending Approval</div>
            <div class="leave-value" id="empPendingLeave">0</div>
            <div class="leave-label">days</div>
        </div>
        <div class="leave-card available">
            <div class="leave-label">Available Leave</div>
            <div class="leave-value" id="empAvailableLeave">30</div>
            <div class="leave-label">days</div>
        </div>
    </div>
    
<!-- Month Navigation -->
    <div class="schedule-controls">
        <div class="month-nav">
            <button onclick="navigateMonth(-1, 'emp')">◀ Previous</button>
            <span class="current-month" id="empCurrentMonth"></span>
            <button onclick="navigateMonth(1, 'emp')">Next ▶</button>
        </div>
    </div>
    
<!-- Schedule Table -->
    <div class="schedule-table-container">
        <table class="schedule-table" id="empScheduleTable">
            <thead>
                <tr>
                    <th class="employee-name">Date</th>
                    <th>Shift Time</th>
                    <th>Duration</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody id="empScheduleBody">
                <!-- Schedule rows will be loaded here -->
            </tbody>
        </table>
    </div>
</div>

<!-- HR Panels -->
<div id="hrQAPanel" class="hr-panel" style="display: none;">
    <h3>QA Management</h3>
    
    <!-- Monthly QA Bar Chart -->
    <div style="background: white; padding: 20px; border-radius: 10px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <h4 style="margin: 0 0 15px 0; color: #2c3e50;">Monthly QA Statistics</h4>
        <div style="height:300px; position:relative;">
            <canvas id="monthlyQAChart"></canvas>
        </div>
    </div>
    
<!-- QA Statistics Cards -->
    <div style="display: grid; grid-template-columns: repeat(6, 1fr); gap: 15px; margin-bottom: 20px;">
        <div style="background: linear-gradient(135deg, #3498db, #2980b9); color: white; padding: 15px; border-radius: 8px; text-align: center;">
            <div style="font-size: 24px; font-weight: bold;" id="totalQAReceived">0</div>
            <div style="font-size: 12px;">Total QA</div>
        </div>
        <div style="background: linear-gradient(135deg, #27ae60, #229954); color: white; padding: 15px; border-radius: 8px; text-align: center;">
            <div style="font-size: 20px; font-weight: bold;" id="grade1Total">0</div>
            <div style="font-size: 11px;">Grade 1</div>
        </div>
        <div style="background: linear-gradient(135deg, #f39c12, #e67e22); color: white; padding: 15px; border-radius: 8px; text-align: center;">
            <div style="font-size: 20px; font-weight: bold;" id="grade2Total">0</div>
            <div style="font-size: 11px;">Grade 2</div>
        </div>
        <div style="background: linear-gradient(135deg, #9b59b6, #8e44ad); color: white; padding: 15px; border-radius: 8px; text-align: center;">
            <div style="font-size: 20px; font-weight: bold;" id="grade3Total">0</div>
            <div style="font-size: 11px;">Grade 3</div>
        </div>
        <div style="background: linear-gradient(135deg, #e67e22, #d35400); color: white; padding: 15px; border-radius: 8px; text-align: center;">
            <div style="font-size: 20px; font-weight: bold;" id="grade4Total">0</div>
            <div style="font-size: 11px;">Grade 4</div>
        </div>
        <div style="background: linear-gradient(135deg, #e74c3c, #c0392b); color: white; padding: 15px; border-radius: 8px; text-align: center;">
            <div style="font-size: 20px; font-weight: bold;" id="grade5Total">0</div>
            <div style="font-size: 11px;">Grade 5</div>
        </div>
    </div>
    
<!-- QA Filters -->
    <div style="background: #f8f9fa; padding: 20px; border-radius: 10px; margin-bottom: 20px;">
        <h5 style="margin: 0 0 15px 0;">QA Filters</h5>
        <div style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 10px; margin-bottom: 15px;">
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">From Date:</label>
                <input type="date" id="qaFilterFrom" onchange="applyQAFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">To Date:</label>
                <input type="date" id="qaFilterTo" onchange="applyQAFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">Radiologist:</label>
                <select id="qaFilterRad" onchange="applyQAFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                    <option value="">All Radiologists</option>
                </select>
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">Hospital:</label>
                <select id="qaFilterHospital" onchange="applyQAFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                    <option value="">All Hospitals</option>
                    <option value="MPHS">MPHS</option>
                    <option value="Menonita">Menonita</option>
                    <option value="NOVARAD">NOVARAD</option>
                    <option value="eRAD">eRAD</option>
                    <option value="Corozal">Corozal</option>
                </select>
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">QA Grade:</label>
                <select id="qaFilterGrade" onchange="applyQAFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                    <option value="">All Grades</option>
                    <option value="1">Grade 1</option>
                    <option value="2">Grade 2</option>
                    <option value="3">Grade 3</option>
                    <option value="4">Grade 4</option>
                    <option value="5">Grade 5</option>
                </select>
            </div>
        </div>
        <div style="display: flex; gap: 10px;">
            <button onclick="clearQAFilters()" style="background: #95a5a6; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">Clear Filters</button>
            <button onclick="exportQAData()" style="background: #27ae60; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">Export Data</button>
            <button onclick="createNewQA()" style="background: #8e44ad; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">Create New QA</button>
        </div>
    </div>
<!-- QA Details Table -->
    <div style="background: #2c3e50; color: white; padding: 15px; border-radius: 10px 10px 0 0; display: flex; justify-content: space-between; align-items: center;">
        <h4 style="margin: 0;">QA Details</h4>
        <div id="qaTableInfo" style="font-size: 12px;">Showing <span id="qaShowingCount">0</span> of <span id="qaTotalCount">0</span></div>
    </div>
    
    <div style="overflow-x: auto; background: white; border-radius: 0 0 10px 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <table style="width: 100%; border-collapse: collapse; font-size: 13px;">
            <thead>
                <tr style="background: #34495e; color: white;">
                    <th style="padding: 12px; text-align: left; border-bottom: 2px solid #2c3e50;">
                        Rad Name
                        <input type="text" id="filterRadName" placeholder="Search..." onkeyup="filterQATable()" 
                               style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 80px;">
                        QA Grade
                        <select id="filterQAGrade" onchange="filterQATable()" style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                            <option value="">All</option>
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                            <option value="4">4</option>
                            <option value="5">5</option>
                            <option value="-">-</option>
                        </select>
                    </th>
                    <th style="padding: 12px; text-align: left; border-bottom: 2px solid #2c3e50;">
                        QA Details
                        <input type="text" id="filterQADetails" placeholder="Search..." onkeyup="filterQATable()" 
                               style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 100px;">
                        QA Received
                        <input type="date" id="filterQAReceived" onchange="filterQATable()" 
                               style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 100px;">
                        QA Responded
                        <input type="date" id="filterQAResponded" onchange="filterQATable()" 
                               style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 100px;">
                        Hospital
                        <select id="filterHospital" onchange="filterQATable()" style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                            <option value="">All</option>
                            <option value="abc2">abc2</option>
                            <option value="rahman">rahman</option>
                            <option value="susoni">susoni</option>
                            <option value="abc">abc</option>
                        </select>
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 80px;">
                        Modality
                        <select id="filterModality" onchange="filterQATable()" style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                            <option value="">All</option>
                            <option value="US">US</option>
                            <option value="CT">CT</option>
                            <option value="MRI">MRI</option>
                            <option value="XR">XR</option>
                        </select>
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 100px;">
                        Accession
                        <input type="text" id="filterAccession" placeholder="Search..." onkeyup="filterQATable()" 
                               style="width: 100%; margin-top: 5px; padding: 4px; font-size: 11px; border: 1px solid #ddd; border-radius: 3px;">
                    </th>
                    <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; width: 120px;">Actions</th>
                </tr>
            </thead>
            <tbody id="qaTableBody">
                <tr>
                    <td colspan="9" style="padding: 20px; text-align: center; color: #666;">Loading QA data...</td>
                </tr>
            </tbody>
        </table>
    </div>
<!-- View More Button -->
    <div style="text-align: center; margin-top: 15px;">
        <button id="qaViewMoreBtn" onclick="loadMoreQA()" style="background: #3498db; color: white; border: none; padding: 10px 30px; border-radius: 5px; cursor: pointer; display: none;">
            View More
        </button>
    </div>
</div>
<div id="hrPeerPanel" class="hr-panel" style="display: none;">
    <h3>Peer Review Management</h3>
    
    <!-- Monthly Peer Review Bar Chart -->
    <div style="background: white; padding: 20px; border-radius: 10px; margin-bottom: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <h4 style="margin: 0 0 15px 0; color: #2c3e50;">Monthly Peer Reviews Completed</h4>
        <div style="height:300px; position:relative;">
            <canvas id="monthlyPeerChart"></canvas>
        </div>
    </div>
    
    <!-- Peer Review Filters -->
    <div style="background: #f8f9fa; padding: 20px; border-radius: 10px; margin-bottom: 20px;">
        <h5 style="margin: 0 0 15px 0;">Peer Review Filters</h5>
        <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-bottom: 15px;">
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">From Date:</label>
                <input type="date" id="peerFilterFrom" onchange="applyPeerFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">To Date:</label>
                <input type="date" id="peerFilterTo" onchange="applyPeerFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">Peer Reviewer:</label>
                <select id="peerFilterRad" onchange="applyPeerFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                    <option value="">All Reviewers</option>
                </select>
            </div>
            <div>
                <label style="font-size: 12px; margin-bottom: 5px; display: block;">Status:</label>
                <select id="peerFilterStatus" onchange="applyPeerFilters()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; font-size: 12px;">
                    <option value="">All Status</option>
                    <option value="Pending">Pending</option>
                    <option value="Completed">Completed</option>
                </select>
            </div>
        </div>
        <div style="display: flex; gap: 10px;">
            <button onclick="clearPeerFilters()" style="background: #95a5a6; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">Clear Filters</button>
            <button onclick="exportPeerData()" style="background: #27ae60; color: white; border: none; padding: 8px 15px; border-radius: 4px; cursor: pointer; font-size: 12px;">Export Data</button>
        </div>
    </div>
    
    <!-- Pending Submissions -->
    <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
        <h4 style="color: #856404;">Pending Peer Review Submissions</h4>
        <div id="pendingSubmissions">Loading...</div>
    </div>

    <!-- Completed Reviews -->
    <div>
        <h4>Completed Peer Reviews</h4>
        <div id="completedReviews">Loading...</div>
    </div>
</div>
		<!-- HR Schedule Management Panel -->
<div id="hrSchedulePanel" class="schedule-panel" style="display: none;">
    <div class="schedule-header">
    <h2>📅 Schedule Management</h2>
    <div style="display: flex; gap: 10px;" id="scheduleHeaderButtons">
        <button class="btn" onclick="exportScheduleData()" style="background: #27ae60;">
            📥 Export Schedule
        </button>
        <button class="btn" onclick="showLeaveRequests()" style="background: #9b59b6;">
            ✈️ Leave Requests <span id="leaveRequestCount" style="background: #e74c3c; padding: 2px 6px; border-radius: 10px; margin-left: 5px;">0</span>
        </button>
		<button class="btn" onclick="showReorderEmployees()" style="background: #3498db;">
			🔄 Reorder Employees
		</button>
    </div>
</div>
    <!-- Keyboard Shortcuts Info -->
    <div style="background: #e3f2fd; padding: 10px 15px; border-radius: 8px; margin-bottom: 15px; border-left: 4px solid #3498db;">
    <strong>⌨️ Quick Actions:</strong> 
    <kbd style="background: #fff; padding: 2px 6px; border: 1px solid #ccc; border-radius: 3px;">Click</kbd> select → 
    <kbd style="background: #fff; padding: 2px 6px; border: 1px solid #ccc; border-radius: 3px;">Ctrl+C</kbd> copy → 
    <kbd style="background: #fff; padding: 2px 6px; border: 1px solid #ccc; border-radius: 3px;">Ctrl+V</kbd> paste | 
    <kbd style="background: #fff; padding: 2px 6px; border: 1px solid #ccc; border-radius: 3px;">Double-click</kbd> quick note | 
    <kbd style="background: #fff; padding: 2px 6px; border: 1px solid #ccc; border-radius: 3px;">Right-click</kbd> full menu
</div>
    <!-- Category Tabs -->
    <div class="schedule-tabs">
        <button class="schedule-tab active" onclick="selectScheduleCategory('RAD')">
            Radiologists (RAD)
        </button>
        <button class="schedule-tab" onclick="selectScheduleCategory('TECH')">
            Technicians (TECH)
        </button>
        <button class="schedule-tab" onclick="selectScheduleCategory('RA')">
            Radiologist Assistants (RA)
        </button>
		<button class="schedule-tab" onclick="selectScheduleCategory('COORD')">
			Coordinators (COORD)
		</button>
    </div>
    
    <!-- Schedule Controls -->
    <div class="schedule-controls">
        <div class="month-nav">
            <button onclick="navigateMonth(-1, 'hr')">◀ Previous</button>
            <span class="current-month" id="hrCurrentMonth"></span>
            <button onclick="navigateMonth(1, 'hr')">Next ▶</button>
        </div>
        
        <div class="copy-schedule-controls">
            <button class="btn" onclick="clearMonthSchedule()" style="background: #e74c3c;">
                🗑️ Clear This Month
            </button>
			<button class="btn" onclick="publishScheduleUpdates()" style="background: #27ae60; font-weight: bold; border: 2px solid #1e8449;">
            📢 Publish Schedule Updates
        </button>
        </div>
    </div>
	    
<!-- Overtime Summary (HR Only) -->
    <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin-bottom: 20px; border-left: 4px solid #ffc107;">
        <strong>⚠️ Overtime Alert:</strong> Employees exceeding 48 hours/week are highlighted in yellow with orange border.
    </div>
    
    <!-- Schedule Table -->
    <div class="schedule-table-container">
        <table class="schedule-table" id="hrScheduleTable">
            <thead id="hrScheduleHeader">
                <!-- Dynamic header will be loaded here -->
            </thead>
            <tbody id="hrScheduleBody">
                <!-- Schedule rows will be loaded here -->
            </tbody>
        </table>
    </div>
</div>
        <!-- Admin Panel -->
        <div id="adminPanel" class="admin-panel">
            <h2>🔧 Admin Control Panel</h2>
             <!-- Proxy Settings -->
            <div class="admin-sections">
                <!-- Employee Management -->
                <div class="admin-section">
    <h3>👥 Employee Management</h3>
    <p>Format: CODE = Name | Specialty | Department | Category | Email | ProxyEnabled</p>
    <p style="font-size: 12px; color: #666;">Categories: RAD (Radiologists), TECH (Technicians), RA (Radiologist Assistants), COORD (Coordinators)</p>
    <textarea id="employeeData" class="admin-textarea" 
              placeholder="RAD001 = Dr.Anderson | General Radiology | Radiology | RAD | anderson@hospital.com | FALSE
TECH001 = John Smith | CT Tech | Radiology | TECH | jsmith@hospital.com | false
RA001 = Mary Johnson | Assistant | Radiology | RA | mjohnson@hospital.com | false

Add all your authorized employees here..."></textarea>
    <button class="save-btn" onclick="saveEmployees()">💾 Save Employee List</button>
	<!-- Proxy Settings Management -->
<div style="margin-top: 20px; padding: 15px; background: #f8f9fa; border-radius: 8px; border: 2px solid #3498db;">
    <h4 style="color: #3498db;">🔄 Proxy QA Entry Settings</h4>
    <p style="font-size: 12px; margin-bottom: 15px;">Enable/disable proxy mode for employees who cannot log in to submit QA responses.</p>
    <div id="proxyToggleList" style="max-height: 300px; overflow-y: auto;">
        <!-- Will be populated by JavaScript -->
    </div>
    <button onclick="refreshProxyToggles()" class="btn" style="background: #3498db; margin-top: 10px;">
        🔄 Refresh Proxy Settings
    </button>
</div>
    <div style="margin-top: 10px;">
        <small>Current authorized employees: <span id="empCount">0</span></small>
    </div>
</div>

                <!-- Shortcuts Management -->
                <div class="admin-section">
                    <h3>📝 AutoHotkey Shortcuts</h3>
                    <p>Add your shortcuts in format: shortcut = expansion text</p>
                    <textarea id="shortcutsData" class="admin-textarea" 
                              placeholder="aav = an anatomic variant
aaw = anterior abdominal wall
kd = Both kidneys are normal in size and echogenicity
liv = The liver demonstrates normal size and echogenicity

Add all your shortcuts here..."></textarea>
                    <button class="save-btn" onclick="saveShortcuts()">💾 Save Shortcuts</button>
                </div>
            </div>

            <div class="admin-sections">
                <!-- Templates Management -->
                <div class="admin-section">
                    <h3>📋 Report Templates</h3>
                    <p>Add your templates in format: template_name = template content</p>
                    <textarea id="templatesData" class="admin-textarea" 
                              placeholder="us_abdomen_male = **Abdominal Ultrasound**

ULTRASOUND OF THE ABDOMEN
TECHNIQUE: Real-time ultrasound...

---

us_pelvis_female = **Pelvic Ultrasound**

ULTRASOUND OF THE PELVIS
TECHNIQUE: Transabdominal and transvaginal...

Add all your templates here..."></textarea>
                    <button class="save-btn" onclick="saveTemplates()">💾 Save Templates</button>
                </div>
<!-- Institution Management -->
<div class="admin-section">
    <h3>🏥 Institution Management</h3>
    <p>Add institution names (one per line). These will appear in dropdown for report submission.</p>
    <textarea id="institutionsData" class="admin-textarea" 
              placeholder="Apollo Hospital
DMC Medical Center
City General Hospital
Memorial Clinic

Add all institutions here..."></textarea>
    <button class="save-btn" onclick="saveInstitutions()">💾 Save Institutions</button>
    <div style="margin-top: 10px;">
        <small>Current institutions: <span id="institutionCount">0</span></small>
    </div>
</div>
			<!-- Critical Findings Management -->
<div class="admin-section">
    <h3>⚠️ Critical Findings Alert System</h3>
    <p>Add critical phrases (one per line). Alert pops up when found in FINDINGS section of report.</p>
    <textarea id="criticalFindingsData" class="admin-textarea" 
              placeholder="acute stroke
aortic dissection
free air
pneumothorax
massive pe
ruptured aneurysm
acute bleed
subdural hematoma

Add all critical phrases here (case-insensitive)..."></textarea>
    <button class="save-btn" onclick="saveCriticalFindings()">💾 Save Critical Findings</button>
    <div style="margin-top: 10px;">
        <small>Current critical phrases: <span id="criticalCount">0</span></small>
    </div>
</div>

<!-- Modality Keywords Management -->
<div class="admin-section">
    <h3>🏥 Modality Keywords Management</h3>
    <p>Configure modality-specific keywords for reports.</p>
    <button onclick="showModalityKeywordsManager()" class="save-btn">
        💾 Manage Modality Keywords
    </button>
</div>

	<!-- AI Configuration -->
<div class="admin-section">
    <h3>🤖 AI Configuration</h3>
    <p>Configure Google Gemini API for AI-powered recommendations</p>
    
    <div style="margin-bottom: 15px;">
        <label style="display: block; margin-bottom: 5px; font-weight: 500;">API Key:</label>
        <input type="password" id="geminiApiKey" placeholder="AIza..." 
               style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: monospace; font-size: 12px;">
        <small style="font-size: 11px; color: #666;">Get free key from: <a href="https://aistudio.google.com/app/apikey" target="_blank">Google AI Studio</a></small>
    </div>
    
    <div style="margin-bottom: 15px;">
        <label style="display: flex; align-items: center;">
            <input type="checkbox" id="aiEnabled" style="margin-right: 8px; transform: scale(1.2);">
            <span style="font-weight: 500;">Enable AI Recommendations</span>
        </label>
        <small style="font-size: 11px; color: #666; margin-left: 28px;">Free tier: 1,500 requests/day, 15/minute</small>
    </div>
    
    <button class="save-btn" onclick="saveAIConfig()">💾 Save AI Configuration</button>
</div>
            <!-- Employee Permissions -->
            <div class="admin-section">
                    <h3>🔐 Employee Permissions</h3>
                    <div id="permissionsList">
                        <!-- Dynamic permissions list -->
                    </div>
                    <button class="btn" onclick="refreshPermissions()">🔄 Refresh Permissions</button>
                </div>
            </div>

            <!-- Access Log -->
            <div class="admin-section" style="grid-column: span 2;">
                <h3>📊 System Access Log</h3>
                <div style="max-height: 240px; overflow-y: auto; background: #f8f9fa; padding: 10px; border-radius: 5px; font-family: monospace; font-size: 11px;">
                    <div id="accessLog">Loading access log...</div>
                </div>
                <div style="margin-top: 10px;">
                    <button class="btn" onclick="refreshAccessLog()">🔄 Refresh Log</button>
                    <button class="btn clear" onclick="clearAccessLog()" style="background: #e74c3c;">🗑️ Clear Log</button>
            </div>
        </div>
		<!-- Password Management Section -->
<div class="admin-section" style="grid-column: span 2; border: 2px solid #e67e22;">
    <h3 style="color: #e67e22;">🔒 Password Management</h3>
    <div style="margin: 30px 0; padding: 20px; background: #f8f9fa; border-radius: 8px;">
    <h3 style="margin: 0 0 15px 0;">🔒 Credential Backups</h3>
    <p style="color: #666; font-size: 13px; margin-bottom: 15px;">
        View and restore employee credentials from automatic backups
    </p>
    <button onclick="viewCredentialBackups()" class="btn" style="background: #9b59b6;">
        📋 View All Backups
    </button>
</div>
    <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
        <strong>📊 Migration Status:</strong>
        <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; margin-top: 10px;">
            <div style="background: white; padding: 15px; border-radius: 8px; text-align: center;">
                <div style="font-size: 28px; font-weight: bold; color: #27ae60;" id="passwordsSetCount">0</div>
                <div style="font-size: 12px; color: #666;">Passwords Set</div>
            </div>
            <div style="background: white; padding: 15px; border-radius: 8px; text-align: center;">
                <div style="font-size: 28px; font-weight: bold; color: #e74c3c;" id="passwordsPendingCount">0</div>
                <div style="font-size: 12px; color: #666;">Pending Setup</div>
            </div>
            <div style="background: white; padding: 15px; border-radius: 8px; text-align: center;">
                <div style="font-size: 28px; font-weight: bold; color: #95a5a6;" id="accountsLockedCount">0</div>
                <div style="font-size: 12px; color: #666;">Locked Accounts</div>
            </div>
        </div>
    </div>
    
    <div style="margin-bottom: 15px;">
        <input type="text" id="passwordSearchInput" placeholder="🔍 Search employee..." 
               onkeyup="filterPasswordList()" 
               style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
    </div>
    
    <div id="passwordManagementList" style="max-height: 400px; overflow-y: auto; border: 1px solid #ddd; border-radius: 8px; background: #f8f9fa; padding: 10px;">
        <!-- Employee password status list will load here -->
    </div>
    
    <div style="margin-top: 15px;">
        <button onclick="loadPasswordManagement()" class="btn" style="background: #3498db;">
            🔄 Refresh Status
        </button>
    </div>
</div>

<!-- Notes Board Log -->
<div class="admin-section" style="grid-column: span 2; border: 2px solid #f39c12;">
    <h3 style="color: #f39c12;">📝 Notes Board Log</h3>
    
    <div style="margin-bottom: 15px;">
        <button onclick="viewAllNotes()" class="btn" style="background: #3498db; font-size: 12px;">View All Notes</button>
        <button onclick="deleteOldNotes()" class="btn" style="background: #e74c3c; font-size: 12px; margin-left: 10px;">Delete Notes Older Than 6 Months</button>
    </div>
    
    <div style="background: #fff3cd; padding: 10px; border-radius: 5px; font-size: 12px;">
        <strong>Total Notes:</strong> <span id="totalNotesCount">0</span>
    </div>
</div>

<div class="admin-section" style="grid-column: span 2;">
    <h3>📊 Data Management</h3>
    
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
        <div style="border: 1px solid #e74c3c; padding: 15px; border-radius: 8px;">
            <h4 style="color: #e74c3c;">QA Reports Management</h4>
            <p style="font-size: 12px; margin-bottom: 15px;">Total QA Reports: <span id="totalQAReports">0</span></p>
            
            <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                <button onclick="viewAllQAReports()" class="btn" style="background: #3498db; font-size: 12px;">View All</button>
                <button onclick="deleteCompletedQA()" class="btn" style="background: #e67e22; font-size: 12px;">Delete Completed</button>
                <button onclick="deleteOldQA()" class="btn" style="background: #e74c3c; font-size: 12px;">Delete Older Than 6 Months</button>
                <button onclick="deleteAllQA()" class="btn" style="background: #c0392b; font-size: 12px;">⚠️ Delete ALL</button>
            </div>
        </div>
        
        <div style="border: 1px solid #9b59b6; padding: 15px; border-radius: 8px;">
            <h4 style="color: #9b59b6;">Peer Review Management</h4>
            <p style="font-size: 12px; margin-bottom: 15px;">Total Peer Reviews: <span id="totalPeerReviews">0</span></p>
            
            <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                <button onclick="viewAllPeerReviews()" class="btn" style="background: #3498db; font-size: 12px;">View All</button>
                <button onclick="deleteCompletedPeer()" class="btn" style="background: #e67e22; font-size: 12px;">Delete Completed</button>
                <button onclick="deleteOldPeer()" class="btn" style="background: #e74c3c; font-size: 12px;">Delete Older Than 6 Months</button>
                <button onclick="deleteAllPeer()" class="btn" style="background: #c0392b; font-size: 12px;">⚠️ Delete ALL</button>
            </div>
        </div>
    </div>
    
    <div style="margin-top: 20px; padding: 15px; background: #fff3cd; border-radius: 5px;">
        <strong>⚠️ Warning:</strong> Deletion is permanent and cannot be undone. Always export data before bulk deletion.
    </div>
</div>

<!-- Ticket System -->
<div class="admin-section" style="grid-column: span 2; border: 2px solid #f39c12;">
    <h3 style="color: #f39c12;">🎫 Support Tickets</h3>
    
    <div style="display: flex; gap: 10px; margin-bottom: 20px;">
        <button onclick="filterTickets('open')" class="btn" style="background: #e74c3c;">
            Open Tickets <span id="openTicketsCount">0</span>
        </button>
        <button onclick="filterTickets('in-progress')" class="btn" style="background: #f39c12;">
            In Progress <span id="progressTicketsCount">0</span>
        </button>
        <button onclick="filterTickets('closed')" class="btn" style="background: #27ae60;">
            Closed <span id="closedTicketsCount">0</span>
        </button>
        <button onclick="filterTickets('all')" class="btn" style="background: #3498db;">
            View All
        </button>
    </div>
    
    <div id="ticketsContainer" style="max-height: 500px; overflow-y: auto;">
        <!-- Tickets will load here -->
    </div>
</div>

<!-- Admin Schedule Management -->
<div class="admin-section" style="grid-column: span 2; border: 2px solid #3498db;">
    <h3 style="color: #3498db;">📅 Schedule Management (Admin)</h3>
    <p>View and manage all employee schedules across all categories.</p>
    
    <div style="margin: 20px 0;">
        <button onclick="openAdminScheduleManager()" class="btn" style="background: #3498db; font-size: 14px; padding: 12px 24px;">
            📅 Open Schedule Manager
        </button>
    </div>
    
    <div style="background: #e3f2fd; padding: 15px; border-radius: 5px; font-size: 13px;">
        <strong>Admin Privileges:</strong>
        <ul style="margin: 10px 0 0 20px; line-height: 1.8;">
            <li>View all categories (RAD, TECH, RA, COORD)</li>
            <li>Create and edit shifts for all employees</li>
            <li>Delete individual shifts</li>
            <li>Clear entire month schedules</li>
            <li>Approve/reject leave requests</li>
        </ul>
    </div>
</div>

<!-- Template Categories Management -->
<div class="admin-section">
    <h3>📂 Template Categories Management</h3>
    <p>Manage template categories without redeploying. Format: JSON structure</p>
    <textarea id="categoriesData" class="admin-textarea" 
              placeholder='Example format:
{
  "CT": {
    "Abdomen": ["Normal abdomen", "Trauma Abdomen", "Pancreas"],
    "Chest": ["Normal Chest", "Chest PE"]
  },
  "US": {
    "Small Parts": ["Breast", "Thyroid", "Neck"]
  }
}'></textarea>
    <button class="save-btn" onclick="saveCategories()">💾 Save Categories</button>
    <div style="margin-top: 10px;">
        <small>Current categories loaded: <span id="categoriesCount">0</span></small>
    </div>
</div>
            <div style="text-align: center; margin-top: 20px;">
                <button class="btn" onclick="hideAdminPanel()" style="background: #95a5a6;">Close Admin Panel</button>
            </div>
        <!-- Status Bar -->
        <div class="status-bar">
            <span id="statusText">Ready</span>
            <span id="wordCount">Words: 0 | Characters: 0</span>
        </div>
    </div>

   <!-- Firebase CDN Scripts -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
	<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-storage-compat.js"></script>
    
    <script>
        // Firebase Configuration
        const firebaseConfig = {
            apiKey: "AIzaSyD1jMv2cPO5v2E-r1TWLzOZen0yZOpEJuU",
            authDomain: "template-dashboard-18c19.firebaseapp.com",
            projectId: "template-dashboard-18c19",
            storageBucket: "template-dashboard-18c19.firebasestorage.app",
            messagingSenderId: "267870042057",
            appId: "1:267870042057:web:c78278c84a641493141a18"
        };
		const GEMINI_CONFIG = {
    apiKey: '', // Paste your key directly here for now
    enabled: false
};

        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();
		const storage = firebase.storage();

        // Global Variables
        let currentUser = null;
        let currentGender = 'male';
        let currentTab = 'US';
		let lastSelectedModality = null;
        let isListening = false;
        let unsubscribeListeners = [];
        let qaAssignments = [];
        let peerAssignments = [];
        let pendingSubmissions = [];
		let monthlyQAChart = null;
		let monthlyPeerChart = null;
		let currentLoadedTemplate = null;
		let todayReportHashes = new Set();
		let isPasswordInitRunning = false;
		let currentPage = 1;
		let rowsPerPage = 15;
		let proxyQAData = {};
		let allFilteredSummaries = [];
		let autoSaveInterval = null;
		let lastSavedContent = '';
		let lastSavedReportHeading = '';
		let lastSavedTimestamp = null;
		let userAutoSavePreference = 30;
		let isUserActive = true;
		let inactivityTimer = null;
		let draftList = []; // Store last 2 drafts
		let currentCaseHash = null;  // Tracks hash of current working case
		let lastNormalizedText = '';  // Store normalized text for comparison
		// Near top of script with other global variables
//const TODAY = new Date().toISOString().split('T')[0];
		
		// Critical findings phrases
let criticalFindings = [
    'acute stroke',
    'aortic dissection',
    'free air',
    'pneumothorax',
    'massive pe',
    'pulmonary embolism',
    'ruptured aneurysm',
    'acute bleed',
    'subdural hematoma',
    'tension pneumothorax',
    'cardiac tamponade',
    'bowel perforation'
];
// Session Timeout Variables
let sessionTimeout = null;
let sessionWarningTimeout = null;
let lastActivity = Date.now();
const TIMEOUT_DURATION = 25 * 60 * 1000; // 15 minutes
const WARNING_TIME = 60 * 1000; // Warn 1 minute before
const INACTIVITY_DETECTION = 15 * 60 * 1000;

// Scheduling System Variables
		let currentScheduleMonth = new Date();
		let currentScheduleCategory = 'RAD';
		let scheduleData = {}; // { empCode: { 'YYYY-MM-DD': { start: 'HH:MM', end: 'HH:MM', duration: hours } } }
		let leaveData = {}; // { empCode: { total: 30, used: 0, pending: 0, requests: [] } }
		let pendingScheduleNotifications = new Set(); // Track unacknowledged schedule changes
		let leaveCancellationRequests = [];
		let allReportsData = [];
		let filteredReportsData = [];
		let selectedReportIds = new Set();

// Track which critical findings have been alerted in current report
let alertedFindingsInCurrentReport = new Set();
let institutions = [
    'Apollo Hospital',
    'DMC Medical Center',
    'City General Hospital',
    'Memorial Clinic'
];
function getUserLocalDate() {
    const now = new Date();
    const year = now.getFullYear();
    const month = String(now.getMonth() + 1).padStart(2, '0');
    const day = String(now.getDate()).padStart(2, '0');
    return `${year}-${month}-${day}`;
}

// Helper function to get user's local time in 12-hour format
function getUserLocalTime12Hour() {
    const now = new Date();
    let hours = now.getHours();
    const minutes = String(now.getMinutes()).padStart(2, '0');
    const seconds = String(now.getSeconds()).padStart(2, '0');
    const ampm = hours >= 12 ? 'PM' : 'AM';
    hours = hours % 12 || 12;
    return `${hours}:${minutes}:${seconds} ${ampm}`;
}

        // Master employee list (will be loaded from Firebase)
        let authorizedEmployees = {};

        // Admin users
        const adminUsers = {
            'admin': { password: 'ij12345', name: 'System Administrator', role: 'admin' }
        };

        // Data storage
        let shortcuts = {
            'aav': 'an anatomic variant',
            'aaw': 'anterior abdominal wall',
            'kd': 'Both kidneys are normal in size and echogenicity',
            'liv': 'The liver demonstrates normal size and echogenicity'
        };

        let templates = {
            'us_abdomen_male': `**Abdominal Ultrasound**

ULTRASOUND OF THE ABDOMEN

TECHNIQUE: Real-time ultrasound examination of the abdomen was performed using a curvilinear transducer.

CLINICAL HISTORY: _____
COMPARISON: _____

FINDINGS:

LIVER:
The liver demonstrates normal size, echogenicity, and contour. No focal lesions identified.

GALLBLADDER:
The gallbladder is normally distended without wall thickening. No cholelithiasis or sludge identified.

KIDNEYS:
Both kidneys are normal in size and echogenicity. No hydronephrosis, stones, or masses identified.

PANCREAS:
The visualized portions of the pancreas appear unremarkable.

IMPRESSION:
Normal abdominal ultrasound.`,

            'us_pelvis_female': `**Pelvic Ultrasound**

ULTRASOUND OF THE PELVIS

TECHNIQUE: Transabdominal and transvaginal ultrasound examination was performed.

CLINICAL HISTORY: _____
COMPARISON: _____

FINDINGS:

UTERUS:
The uterus is normal in size and echogenicity. The endometrial stripe measures _____ mm.

OVARIES:
Both ovaries are visualized and appear normal in size and echogenicity.

IMPRESSION:
Normal pelvic ultrasound.`
        };

        const templateCategories = {
            'US':{
                'Small Parts':['Axilla', 'Canal', 'Breast', 'Buttock', 'Chest', 'Elastography', 'Groin', 'Hernia', 'Jugular Subclavian', 'Maxillofacial', 'Tissue Mass', 'Neck', 'Penis', 'Thyroid'],
                'Abdomen':['Complete', 'Appendix', 'Aorta', 'Ascites', 'Limited', 'Intussusception', 'Pylorus', 'RUQ', 'Abdomen Doppler', 'Gallbladder', 'Hepatobiliary', 'Renal', 'Renal Doppler', 'Pancreas', 'Liver', 'Spleen'],
                'Pelvis':['Endovaginal', 'Abortion', 'TA and TV', 'Kidney Transplant', 'Transabdominal', 'Transvaginal', 'Pelvis', 'Male pelvis', 'Scrotum doppler'],
				'Pediatric':['Brain', 'Pediatric hips', 'Pediatric spine'],
				'Mapping':['Normal', 'Liver Doppler', 'Thyroid Nodule', 'Lymph node', 'Abnormal Vein', 'Abnormal Thyroid', 'Abnormal Lymph'],
                'OB GYN':['Follicular', 'Fetal Umbilical', 'OB', 'Pelvic Doppler', 'OB 14 weeks', 'BPP', 'Ultrasound Twin', 'No Fetal Pole', 'Early Pregnancy', 'Fetal Demise'],
				'Extremity': ['Ankle', 'Hand', 'Shoulder', 'Knee', 'Hip', 'Thigh', 'Wrist', 'Elbow'],
                'Vascular':['Carotid Doppler Normal', 'Bil LE venous', 'Bil UE venous', 'Bil LE Arterial', 'Bil UE Arterial', 'Bil LE Art and ven', 'Brachial Indices']
            },
           'CT': {
                'Head': ['Trauma', 'WMD', 'Stroke Normal', 'Stroke Atrophy', 'Brain IAC', 'Pituitary', 'Neck soft tissue'],
				'Face': ['Orbits', 'Temporal Bone', 'Sinus', 'Maxillofacial', 'Mandible', 'Mastoid'],
				'Spine': ['Cervical', 'Trauma Cervical', 'Thoracic', 'Lumbar', 'Sacrum'],
                'Chest': ['Trauma', 'CAP Trauma', 'HRCT', 'CAP Normal', 'Normal', 'Sternum', 'Low Dose', 'Chest PE'],
                'Abdomen': ['Normal', 'Trauma', 'Pancreas'],
				'Pelvis': ['Normal'],
				'MSK Extremity': ['Ankle', 'Scanogram', 'Elbow', 'Hip', 'Knee', 'Shoulder', 'Wrist', 'Forearm', 'Tibia Fibula', 'Hand', 'Foot'],
				'Angio': ['CTA Head', 'Bilateral LE', 'CTA Neck', 'Chest and Abdomen', 'CAP Runoff', 'CTA Chest', 'Chest Runoff', 'Abdomen Runoff']
            },
            'MRI': {
                'Brain': ['Normal', 'HNG', 'HNC', 'Atrophy', 'IAC', 'WMD', 'Venogram', 'Pituitary'],
				'Face': ['Maxillofacial', 'Orbit', 'Sinuses', 'Temporomandibular Joint'],
				'Abdomen': ['Normal', 'Chest', 'MRCP', 'Pelvis', 'Groin', 'Scrotum', 'Sacroiliac joint', 'CAP'],
				'Angio': ['Abdomen','Pelvis', 'Neck', 'Head', 'Chest', 'Abdomen Runoff'],
                'UpperExt': ['Hand', 'Shoulder', 'Humerus', 'Elbow', 'Finger', 'Forearm', 'Clavicle', 'Wrist'],
				'LowerExt': ['Ankle', 'Hip', 'Knee', 'Tibia Fibula', 'Femur', 'Toe', 'Sacroiliac joint', 'Foot'],
				'Spine': ['Coccyx', 'Cervical', 'Thoracic', 'Lumbar', 'Neck', 'Brachial Plexuses', 'Whole Spine']
            },
            'XR': {
                'Chest': ['Bronchitis', 'Bronchiolitis', 'Normal', 'COPD', 'CHF', 'Ribs'],
				'Spine': ['Cervical', 'Coccyx', 'Thoracic', 'Lumbar', 'Shunt Series', 'Thoracolumbar', 'Scoliosis Series'],
				'UpperExt': ['Clavicle', 'Elbow', 'Finger', 'Forearm', 'Forearm Wrist', 'Bonesurvey Hand', 'Hand', 'Hand Wrist', 'Humerus', 'Left UE', 'Right UE', 'Scapula', 'Shoulder', 'Wrist'],
				'LowerExt': ['Ankle', 'Calcaneus', 'Femur', 'Foot', 'Left LE', 'Knee', 'Right LE','Tibia Fibula', 'Toe'],
				'FaceNeck': ['Facial Bones', 'Adenoids', 'Neck', 'Neck FB', 'Orbits', 'Mandible', 'Maxilla', 'Mastoids', 'TMJ', 'PNS', 'Skull', 'Nasal Bones'],
				'Pelvis': ['Trauma', 'Hip Joint', 'Hip Osteoarthritis', 'Hip Replacement', 'Humerus', 'Sacroiliac Joint'],
				'Others': ['Format 1', 'Format 2', 'Format 3', 'Format 4', 'Format 5', 'For`mat 6', 'Format 7', 'Format 8', 'Format 9', 'Format 10'],
				'Abdomen': ['KUB', 'Acute Abdomen', 'Bone Survey', 'Bowel Series', 'Barium Swallow', 'Barium Enema', 'NG tube', 'PEG Tube', 'Obstruction Series']
            },
            'Biotronics': {
                'Apollo Head': ['Normal', 'CT Head', 'HNG', 'HNC', 'Atrophy', 'IAC', 'WMD', 'Pituitary', 'MRA Head'],
                'Apollo Face': ['Maxillofacial', 'Orbit', 'Temporomandibular'],
                'Apollo Spine': ['Neck', 'Cervical', 'Thoracic', 'Lumbar', 'MRA Neck', 'Whole Spine', 'Coccyx'],
                'Apollo Extremity': ['Knee', 'Hip'],
                'DMC Head': ['Normal', 'CT Head', 'HNG', 'HNC', 'Atrophy', 'IAC', 'WMD', 'Pituitary', 'MRA Head'],
                'DMC Face': ['Maxillofacial', 'Orbit', 'Temporomandibular'],
                'DMC Spine': ['Neck', 'Cervical', 'Thoracic', 'Lumbar', 'MRA Neck', 'Whole Spine', 'Coccyx']
            }
        };

// ==============================================
// HELPER FUNCTIONS
// ==============================================

function isElementVisible(element) {
    if (!element) return false;
    
    // Check if element exists in DOM
    if (!document.body.contains(element)) return false;
    
    // Check computed style (accounts for CSS, inline styles, everything)
    const style = window.getComputedStyle(element);
    
    // Check display
    if (style.display === 'none') return false;
    
    // Check visibility
    if (style.visibility === 'hidden') return false;
    
    // Check opacity
    if (style.opacity === '0') return false;
    
    // Check if element has dimensions (not collapsed)
    const rect = element.getBoundingClientRect();
    if (rect.width === 0 && rect.height === 0) return false;
    
    // Check parent visibility recursively
    let parent = element.parentElement;
    while (parent && parent !== document.body) {
        const parentStyle = window.getComputedStyle(parent);
        if (parentStyle.display === 'none' || parentStyle.visibility === 'hidden') {
            return false;
        }
        parent = parent.parentElement;
    }
    
    return true;
}

        // ==============================================
        // AUTHENTICATION SYSTEM
        // ==============================================
        
function showAdminLogin() {
			document.getElementById('empLogin').style.display = 'none';
			document.getElementById('adminLogin').style.display = 'block';
			document.getElementById('username').focus();
		}

		function showEmpLogin() {
			document.getElementById('empLogin').style.display = 'block';
			document.getElementById('adminLogin').style.display = 'none';
			document.getElementById('empCode').focus();
		}

// ✅ FIXED VERSION - Updates Firestore directly for login-related changes

async function handleEmpLogin(event) {
    if (event) event.preventDefault();
    
    const empCode = document.getElementById('empCode').value.trim().toUpperCase();
    const password = document.getElementById('empPassword') ? document.getElementById('empPassword').value : null;
    const errorDiv = document.getElementById('errorMessage');
    
    if (!empCode) {
        errorDiv.textContent = 'Please enter your employee code.';
        errorDiv.style.display = 'block';
        return false;
    }
    
    // Load latest employee data from Firebase
    await loadSystemData();
    
    // Check if employee exists
    if (!authorizedEmployees[empCode]) {
        errorDiv.textContent = 'Access Denied: Invalid or unauthorized employee code.';
        errorDiv.style.display = 'block';
        await logFailedAccess(empCode);
        document.getElementById('empCode').value = '';
        return false;
    }
    
    const employee = authorizedEmployees[empCode];
    if (!employee.passwordSet && employee.passwordReminderCount >= 10) {
    errorDiv.textContent = '⛔ Account suspended: Password setup required.\n\nYou ignored 10 reminders. Contact HR to unlock your account.';
    errorDiv.style.display = 'block';
    
    // Lock the account
    if (!employee.accountLocked) {
        await updateEmployeeFieldDirectly(empCode, { 
            accountLocked: true,
            lockedReason: 'Exceeded password setup reminders'
        });
    }
    
    return false;
}
    // Check if employee has set up password
    if (employee.passwordSet) {
        if (!document.getElementById('empPassword')) {
            showPasswordInputField();
            return false;
        }
        
        if (!password) {
            errorDiv.textContent = 'Please enter your password.';
            errorDiv.style.display = 'block';
            return false;
        }
        
         // ✅ CASE-INSENSITIVE PASSWORD COMPARISON (converted to lowercase)
        if (!employee.password || employee.password.toLowerCase() !== password.toLowerCase()) {
            errorDiv.textContent = 'Incorrect password.';
            errorDiv.style.display = 'block';
            
            // Track failed attempts with transaction lock
            const failedAttempts = (employee.failedLoginAttempts || 0) + 1;

try {
    // Use Firestore transaction to prevent race conditions
    await db.runTransaction(async (transaction) => {
        const employeesRef = db.collection('system_data').doc('employees');
        const employeesDoc = await transaction.get(employeesRef);
        
        if (!employeesDoc.exists) {
            throw new Error('Employees document not found');
        }
        
        const allEmployees = employeesDoc.data().data;
        
        allEmployees[empCode].failedLoginAttempts = failedAttempts;
        
        if (failedAttempts >= 3) {
            allEmployees[empCode].accountLocked = true;
            errorDiv.textContent = 'Account locked after 3 failed attempts. Contact HR to reset your password.';
        }
        
        transaction.update(employeesRef, {
            data: allEmployees,
            lastUpdated: new Date().toISOString(),
            updatedBy: 'SYSTEM_LOGIN'
        });
    });
     authorizedEmployees[empCode].failedLoginAttempts = failedAttempts;
    if (failedAttempts >= 3) authorizedEmployees[empCode].accountLocked = true;
    // Reload from Firestore after transaction
    await loadSystemData();
    
} catch (error) {
    console.error('Error updating failed login attempts:', error);
}
            
            await logFailedAccess(empCode);
            return false;
        }
        
        // Reset failed attempts on successful login
        if (employee.failedLoginAttempts > 0) {
            try {
                await db.runTransaction(async (transaction) => {
                    const employeesRef = db.collection('system_data').doc('employees');
                    const employeesDoc = await transaction.get(employeesRef);
                    
                    if (!employeesDoc.exists) {
                        throw new Error('Employees document not found');
                    }
                    
                    const allEmployees = employeesDoc.data().data;
                    allEmployees[empCode].failedLoginAttempts = 0;
                    
                    transaction.update(employeesRef, {
                        data: allEmployees,
                        lastUpdated: new Date().toISOString(),
                        updatedBy: 'SYSTEM_LOGIN'
                    });
                });
                authorizedEmployees[empCode].failedLoginAttempts = 0;
                await loadSystemData();
            } catch (error) {
                console.error('Error resetting failed attempts:', error);
            }
        }
    }
    
    // Check if account is locked
    if (employee.accountLocked) {
        errorDiv.textContent = 'Your account is locked. Contact HR to unlock it.';
        errorDiv.style.display = 'block';
        return false;
    }
    
// Login successful
currentUser = { 
    ...employee, 
    code: empCode, 
    loginTime: new Date().toISOString()
};
// 🆕 Sync role for What's New feature
currentUserRole = currentUser.role;

await loadAutoSavePreference();
await logEmployeeAccess(empCode, employee.name);

// 🆕 CHECK IF HR RESET PASSWORD - FORCE CHANGE
if (employee.mustChangePassword) {
    errorDiv.style.display = 'none';
    showForcePasswordChangeModal(empCode);
    return false; // Don't show dashboard yet
}

await showDashboard();
errorDiv.style.display = 'none';
// Show password setup reminder if not set
if (!employee.passwordSet) {
    setTimeout(() => {
        showPasswordSetupReminder(empCode);
    }, 2000);
}
    
    return false;
}

function showPasswordInputField() {
    // EXPLANATION: This function dynamically adds a password field to the login form
    // It's called when a user who has already set a password tries to login
    
    const empLogin = document.getElementById('empLogin');
    const errorDiv = document.getElementById('errorMessage');
    
    // Check if password field already exists
    if (document.getElementById('empPassword')) {
        return;
    }
    
    // EXPLANATION: Create password field HTML
    const passwordHTML = `
        <div class="form-group" id="passwordFieldGroup" style="margin-top: 15px;">
            <label for="empPassword">Password:</label>
            <input type="password" id="empPassword" required placeholder="Enter your password" 
                   style="text-align: left; font-size: 16px;">
        </div>
    `;
    
    // EXPLANATION: Insert password field after employee code field
    const empCodeGroup = empLogin.querySelector('.form-group');
    empCodeGroup.insertAdjacentHTML('afterend', passwordHTML);
    
    // EXPLANATION: Update error message
    errorDiv.textContent = 'Password required for this account.';
    errorDiv.style.display = 'block';
    errorDiv.style.background = 'rgba(52, 152, 219, 0.85)'; // Blue instead of red
    
    // EXPLANATION: Focus on password field
    setTimeout(() => {
        document.getElementById('empPassword').focus();
    }, 100);
}

async function showPasswordSetupReminder(empCode) {
    // EXPLANATION: Shows a dismissible banner reminding users to set up password
    // Can be closed - non-intrusive approach for gradual migration
    
    const employee = authorizedEmployees[empCode];
    
    // EXPLANATION: Track how many times we've shown this reminder
    if (!employee.passwordReminderCount) {
        employee.passwordReminderCount = 0;
    }
    
    employee.passwordReminderCount++;
    
    // EXPLANATION: Calculate deadline (30 days from first reminder)
    if (!employee.passwordSetupDeadline) {
        const deadline = new Date();
        deadline.setDate(deadline.getDate() + 30);
        employee.passwordSetupDeadline = deadline.toISOString();
    }
    
    const deadline = new Date(employee.passwordSetupDeadline);
    const daysLeft = Math.ceil((deadline - new Date()) / (1000 * 60 * 60 * 24));
    
    // ✅ CHECK 1: Block if 10 reminders reached
    if (employee.passwordReminderCount >= 10) {
        await updateEmployeeFieldDirectly(empCode, { 
            accountLocked: true,
            lockedReason: 'Exceeded 10 password setup reminders',
            passwordReminderCount: employee.passwordReminderCount
        });
        
        alert('⛔ Account locked: You ignored 10 password setup reminders. Contact HR to unlock your account.');
        logout();
        return;
    }
    
    // ✅ CHECK 2: Block if 30-day deadline passed
    if (daysLeft <= 0) {
        await updateEmployeeFieldDirectly(empCode, { 
            accountLocked: true,
            lockedReason: 'Password setup deadline expired (30 days)',
            passwordReminderCount: employee.passwordReminderCount
        });
        
        alert('⛔ Account locked: You exceeded the 30-day password setup deadline. Contact HR to unlock your account.');
        logout();
        return;
    }
    
    // EXPLANATION: Save updated reminder count to Firestore
    await updateEmployeeFieldDirectly(empCode, { 
        passwordReminderCount: employee.passwordReminderCount,
        passwordSetupDeadline: employee.passwordSetupDeadline
    });
    
    // EXPLANATION: Create reminder banner
    const banner = document.createElement('div');
    banner.id = 'passwordReminderBanner';
    banner.style.cssText = `
        position: fixed;
        top: 70px;
        left: 50%;
        transform: translateX(-50%);
        background: linear-gradient(135deg, #f39c12, #e67e22);
        color: white;
        padding: 20px 30px;
        border-radius: 12px;
        box-shadow: 0 10px 40px rgba(0,0,0,0.3);
        z-index: 10001;
        max-width: 600px;
        animation: slideDown 0.5s ease;
    `;
    
    banner.innerHTML = `
        <div style="display: flex; justify-content: space-between; align-items: center; gap: 20px;">
            <div style="flex: 1;">
                <div style="font-size: 18px; font-weight: bold; margin-bottom: 8px;">
                    🔒 Security Enhancement Required
                </div>
                <div style="font-size: 14px; opacity: 0.95; line-height: 1.5;">
                    Please set up your password to secure your account.<br>
                    <strong>${daysLeft} days remaining</strong> (Reminder ${employee.passwordReminderCount} of 10)
                </div>
            </div>
            <div style="display: flex; gap: 10px;">
                <button onclick="openPasswordSetupModal('${empCode}')" 
                        style="background: #27ae60; color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 14px;">
                    Set Up Now
                </button>
                <button onclick="dismissPasswordReminder()" 
                        style="background: rgba(255,255,255,0.2); color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-size: 14px;">
                    Later
                </button>
            </div>
        </div>
    `;
    
    // EXPLANATION: Show banner only if not already shown
    const existing = document.getElementById('passwordReminderBanner');
    if (existing) existing.remove();
    
    document.body.appendChild(banner);
    
    // EXPLANATION: Auto-dismiss after 10 seconds if user doesn't interact
    setTimeout(() => {
        if (document.getElementById('passwordReminderBanner')) {
            dismissPasswordReminder();
        }
    }, 10000);
}

function showForcePasswordChangeModal(empCode) {
    const modal = createModal(`
        <h2 style="color: #e74c3c; margin-bottom: 20px;">🔒 Password Change Required</h2>
        
        <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin-bottom: 20px; border-left: 4px solid #f39c12;">
            <strong>⚠️ Your password was reset by HR.</strong><br>
            You MUST set a new password before continuing.
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 8px; font-weight: 500;">New Password:</label>
            <input type="password" id="forceNewPassword" placeholder="Enter new password (min 6 characters)" 
                   style="width: 100%; padding: 12px; border: 2px solid #ddd; border-radius: 8px; font-size: 16px;">
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 8px; font-weight: 500;">Confirm Password:</label>
            <input type="password" id="forceConfirmPassword" placeholder="Re-enter new password" 
                   style="width: 100%; padding: 12px; border: 2px solid #ddd; border-radius: 8px; font-size: 16px;">
        </div>
        
        <div id="forcePasswordError" style="display: none; background: #f8d7da; color: #721c24; padding: 12px; border-radius: 8px; margin-bottom: 20px; font-size: 14px;"></div>
        
        <div style="text-align: right;">
            <button onclick="saveForcedPasswordChange('${empCode}')" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                💾 Set New Password
            </button>
        </div>
        
        <div style="background: #f8d7da; padding: 10px; border-radius: 5px; margin-top: 20px; font-size: 12px; color: #721c24;">
            ⚠️ You cannot access the system until you change your password.
        </div>
    `);
    
    // Prevent closing modal
    const modalEl = document.querySelector('.modal');
    if (modalEl) {
        modalEl.onclick = null; // Disable click-outside-to-close
    }
}

async function saveForcedPasswordChange(empCode) {
    const newPassword = document.getElementById('forceNewPassword').value;
    const confirmPassword = document.getElementById('forceConfirmPassword').value;
    const errorDiv = document.getElementById('forcePasswordError');
    
    if (!newPassword || !confirmPassword) {
        errorDiv.textContent = 'Please fill in both password fields.';
        errorDiv.style.display = 'block';
        return;
    }
    
    if (newPassword.length < 6) {
        errorDiv.textContent = 'Password must be at least 6 characters.';
        errorDiv.style.display = 'block';
        return;
    }
    
    if (newPassword !== confirmPassword) {
        errorDiv.textContent = 'Passwords do not match.';
        errorDiv.style.display = 'block';
        return;
    }
    
    try {
        // ✅ BACKUP BEFORE FORCED CHANGE
        await backupEmployeeCredentials(empCode, 'forced_change', authorizedEmployees[empCode]);
        
        // ✅ USE TRANSACTION PATTERN A
        await db.runTransaction(async (transaction) => {
            const employeesRef = db.collection('system_data').doc('employees');
            const employeesDoc = await transaction.get(employeesRef);
            
            if (!employeesDoc.exists) {
                throw new Error('Employees document not found');
            }
            
            const allEmployees = employeesDoc.data().data;
            
            if (!allEmployees[empCode]) {
                throw new Error('Employee not found');
            }
            
            allEmployees[empCode].password = newPassword;
            allEmployees[empCode].passwordSet = true;
            allEmployees[empCode].passwordSetDate = new Date().toISOString();
            allEmployees[empCode].mustChangePassword = false;
            allEmployees[empCode].failedLoginAttempts = 0;
            allEmployees[empCode].accountLocked = false;
            
            transaction.update(employeesRef, {
                data: allEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: empCode
            });
        });
        
        // ✅ RELOAD FROM FIRESTORE
        await loadSystemData();
        
        currentUser = {
    ...authorizedEmployees[empCode],
    code: empCode,
    loginTime: currentUser.loginTime
};
        
        showNotification('✅ Password changed successfully!');
        closeModal();
        await showDashboard();
        
    } catch (error) {
        console.error('Error changing password:', error);
        errorDiv.textContent = 'Error changing password. Please try again.';
        errorDiv.style.display = 'block';
    }
}

function dismissPasswordReminder() {
    // EXPLANATION: Remove the reminder banner
    const banner = document.getElementById('passwordReminderBanner');
    if (banner) {
        banner.style.animation = 'slideUp 0.3s ease';
        setTimeout(() => banner.remove(), 300);
    }
}

function openPasswordSetupModal(empCode) {
    // EXPLANATION: Opens modal for user to create their password
    // Simple form - just password + confirmation
    
    dismissPasswordReminder(); // Close reminder banner
    
    const modal = createModal(`
        <h2 style="color: #27ae60; margin-bottom: 20px;">🔒 Set Up Your Password</h2>
        
        <div style="background: #e3f2fd; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <strong>Employee:</strong> ${authorizedEmployees[empCode].name} (${empCode})
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 8px; font-weight: 500;">New Password:</label>
            <input type="password" id="newPassword" placeholder="Enter your password" 
                   style="width: 100%; padding: 12px; border: 2px solid #ddd; border-radius: 8px; font-size: 16px;">
            <div style="font-size: 12px; color: #666; margin-top: 5px;">
                Minimum 6 characters (no special requirements)
            </div>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 8px; font-weight: 500;">Confirm Password:</label>
            <input type="password" id="confirmPassword" placeholder="Re-enter your password" 
                   style="width: 100%; padding: 12px; border: 2px solid #ddd; border-radius: 8px; font-size: 16px;">
        </div>
        
        <div id="passwordSetupError" style="display: none; background: #f8d7da; color: #721c24; padding: 12px; border-radius: 8px; margin-bottom: 20px; font-size: 14px;"></div>
        
        <div style="display: flex; gap: 10px; justify-content: flex-end;">
            <button onclick="saveNewPassword('${empCode}')" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                💾 Save Password
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">
                Cancel
            </button>
        </div>
        
        <div style="background: #fff3cd; padding: 12px; border-radius: 8px; margin-top: 20px; font-size: 12px; color: #856404;">
            <strong>Note:</strong> Once set, you'll need both your employee code and password to login.
        </div>
    `);
    
    // EXPLANATION: Focus on password field
    setTimeout(() => {
        document.getElementById('newPassword').focus();
    }, 100);
}

async function saveNewPassword(empCode) {
    const newPassword = document.getElementById('newPassword').value;
    const confirmPassword = document.getElementById('confirmPassword').value;
    const errorDiv = document.getElementById('passwordSetupError');
    
    // Validation
    if (!newPassword || !confirmPassword) {
        errorDiv.textContent = 'Please fill in both password fields.';
        errorDiv.style.display = 'block';
        return;
    }
    
    if (newPassword.length < 6) {
        errorDiv.textContent = 'Password must be at least 6 characters long.';
        errorDiv.style.display = 'block';
        return;
    }
    
    if (newPassword !== confirmPassword) {
        errorDiv.textContent = 'Passwords do not match. Please try again.';
        errorDiv.style.display = 'block';
        return;
    }
    
    try {
        await backupEmployeeCredentials(empCode, 'initial_setup', authorizedEmployees[empCode]);
        
        // ✅ USE TRANSACTION PATTERN A
        await db.runTransaction(async (transaction) => {
            const employeesRef = db.collection('system_data').doc('employees');
            const employeesDoc = await transaction.get(employeesRef);
            
            if (!employeesDoc.exists) {
                throw new Error('Employees document not found');
            }
            
            const allEmployees = employeesDoc.data().data;
            
            if (!allEmployees[empCode]) {
                throw new Error('Employee not found');
            }
            
            // Update employee record
            allEmployees[empCode].password = newPassword;
            allEmployees[empCode].passwordSet = true;
            allEmployees[empCode].passwordSetDate = new Date().toISOString();
            allEmployees[empCode].failedLoginAttempts = 0;
            allEmployees[empCode].accountLocked = false;
            
            transaction.update(employeesRef, {
                data: allEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: empCode
            });
        });
        
        // Reload from Firestore after transaction
        await loadSystemData();
        
        showNotification('✅ Password set successfully! Please use it for your next login.');
        closeModal();
        dismissPasswordReminder();
        
    } catch (error) {
        console.error('Error saving password:', error);
        errorDiv.textContent = 'Error saving password. Please try again.';
        errorDiv.style.display = 'block';
    }
}

        async function handleAdminLogin(event) {
    if (event) event.preventDefault();
    
    // ✅ CASE-INSENSITIVE: Convert both to lowercase for comparison
    const username = document.getElementById('username').value.trim().toLowerCase();
    const password = document.getElementById('password').value;
    const errorDiv = document.getElementById('errorMessage');
    
    if (!username || !password) {
        errorDiv.textContent = 'Please enter both username and password.';
        errorDiv.style.display = 'block';
        return false;
    }
    
    // ✅ CASE-INSENSITIVE: Check if admin exists (lowercase comparison)
    if (adminUsers[username] && adminUsers[username].password.toLowerCase() === password.toLowerCase()) {
        currentUser = { 
            ...adminUsers[username], 
            username: username,
            loginTime: new Date().toISOString()
        };
		// ✅ Sync role for What's New feature
        currentUserRole = currentUser.role;

        await showDashboard();
        errorDiv.style.display = 'none';
    } else {
        errorDiv.textContent = 'Invalid admin credentials';
        errorDiv.style.display = 'block';
    }
    
    return false;
}

async function showDashboard() {
    document.getElementById('loginPage').style.display = 'none';
    document.getElementById('dashboard').style.display = 'block';
    
    const welcomeText = currentUser.code 
        ? `Welcome, ${currentUser.name} (${currentUser.code})`
        : `Welcome, ${currentUser.name}`;
    document.getElementById('welcomeText').textContent = welcomeText;
	await loadBodyPartRules();
	
	// Show PWA install button if prompt is available
    if (deferredPrompt) {
        showInstallButton();
    }
    
    // Setup interface based on role
    if (currentUser.role === 'admin') {
        document.getElementById('adminBtn').style.display = 'inline-block';
        setupEmployeeInterface();
    } else if (currentUser.role === 'hr') {
        setupHRInterface();
    } else if (currentUser.role === 'employee') {
        setupEmployeeInterface();
    }
	
	// ENABLE TEXT EDITOR AFTER LOGIN
    const textEditor = document.getElementById('textEditor');
    if (textEditor && (currentUser.role === 'employee' || currentUser.role === 'admin')) {
        textEditor.style.display = 'block';
        textEditor.style.visibility = 'visible';    // ADDED: Make visible
        textEditor.style.position = 'static';       // ADDED: Return to normal flow
        textEditor.style.top = 'auto';              // ADDED: Reset position
        textEditor.style.pointerEvents = 'auto';    // ADDED: Enable mouse events
        textEditor.contentEditable = 'true';
    }
    
    await loadSystemData(); 
if (currentUser.role === 'admin') {
    await checkPasswordSystemInitialization();
	}
// Load today's report counter
    if (currentUser.role === 'employee' || currentUser.role === 'admin') {
        await updateReportCounter();
		initializeReportCountSelector();
		populateInstitutionDropdown();
        
        const textEditor = document.getElementById('textEditor');
        if (textEditor) {
           textEditor.addEventListener('input', debounce(autoSuggestReportCount, 800));
        }
    
    }
	setupRealtimeListeners();
	updateStatus('Dashboard loaded');
    initSessionTimeout();
	await startSessionTracking();
	const whatsNewBtn = document.getElementById('whatsNewBtn');
		if (whatsNewBtn) {
			whatsNewBtn.style.display = 'inline-block';  // Show for ALL roles
		}

		// Show admin-only edit controls
		if (currentUser.role === 'admin') {
			const adminControls = document.getElementById('whatsNewAdminControls');
			if (adminControls) {
				adminControls.style.display = 'block';

        }
    }
	checkWhatsNewUnread();
}

function setupEmployeeInterface() {
			document.getElementById('empToolbar').style.display = 'flex';
			if ('Notification' in window && Notification.permission === 'default') {
				Notification.requestPermission();
			}
			
			// Show Tools button
			document.getElementById('toolsBtn').style.display = 'inline-block';
			
			// Hide HR elements
			document.getElementById('hrToolbar').style.display = 'none';
			document.getElementById('hrQAPanel').style.display = 'none';
			document.getElementById('hrPeerPanel').style.display = 'none';

			document.getElementById('qaBoard').style.display = 'none';
			document.getElementById('peerBoard').style.display = 'none';
			
			// Show main container by default
			document.getElementById('mainContainer').style.display = 'grid';
			
			// Show advanced search button if user has permission
			if (currentUser.permissions && currentUser.permissions.includes('adv_search')) {
				// Advanced search is now in Tools dropdown - no separate button needed
			}

			loadEmployeeBoards();
			loadTemplateCategories('US');
			initializeCheckboxListeners();
			initializeNotesBoard();
			loadUserTicketNotifications();
			initializeMeetingSystem();
			populateInstitutionDropdown();
		}

 function setupHRInterface() {
    const hrToolbar = document.getElementById('hrToolbar');
    if (hrToolbar) hrToolbar.style.display = 'flex';

    const toolsBtn = document.getElementById('toolsBtn');
    if (toolsBtn) toolsBtn.style.display = 'inline-block';

    const employeeBoards = document.getElementById('employeeBoards');
    if (employeeBoards) employeeBoards.style.display = 'none';

    const empToolbar = document.getElementById('empToolbar');
    if (empToolbar) empToolbar.style.display = 'none';

    const mainContainer = document.getElementById('mainContainer');
    if (mainContainer) mainContainer.style.display = 'none';

    const bodyPartRulesTab = document.getElementById('bodyPartRulesTab');
    if (bodyPartRulesTab) {
        const hasAccess = currentUser.role === 'hr' ||
                          currentUser.role === 'admin' ||
                          (currentUser.permissions && currentUser.permissions.includes('body_part_rules_manager'));
        bodyPartRulesTab.style.display = hasAccess ? 'inline-block' : 'none';
    }
	// Show password management tab if HR has permission
	if (hasPermission('password_manager')) {
    const hrToolbar = document.querySelector('.hr-tabs');
    if (hrToolbar && !document.getElementById('passwordManagementTab')) {
        const passwordTab = document.createElement('button');
        passwordTab.id = 'passwordManagementTab';
        passwordTab.className = 'hr-tab';
        passwordTab.style.background = '#e67e22';
        passwordTab.textContent = '🔐 Password Management';
        passwordTab.onclick = () => selectHRTab('PasswordManagement');
        hrToolbar.appendChild(passwordTab);
    }
}
    selectHRTab('QA');
    loadHRNotifications();
}

async function logout() {
    await endSessionTracking('manual'); // NEW LINE
    
    cleanupListeners();
    currentUser = null;
    stopSessionTimeout();
    
    // Reset UI
    document.getElementById('loginPage').style.display = 'flex';
    document.getElementById('dashboard').style.display = 'none';
    document.getElementById('adminPanel').style.display = 'none';
    
    // DISABLE TEXT EDITOR ON LOGOUT
    const textEditor = document.getElementById('textEditor');
    if (textEditor) {
        textEditor.contentEditable = 'false';
        textEditor.style.display = 'none';
		textEditor.style.visibility = 'hidden';     // ADDED: Make invisible
        textEditor.style.position = 'absolute';     // ADDED: Remove from flow
        textEditor.style.top = '-9999px';           // ADDED: Move offscreen
        textEditor.style.pointerEvents = 'none'; 
        textEditor.innerHTML = '<br>'; // Clear content
        textEditor.blur();
    }
    
    // Clear form inputs
    document.getElementById('empCode').value = '';
    document.getElementById('username').value = '';
    document.getElementById('password').value = '';
    document.getElementById('errorMessage').style.display = 'none';
    
    showEmpLogin();
    
    // Refocus on employee code input
    setTimeout(() => {
        const empCodeInput = document.getElementById('empCode');
        if (empCodeInput) {
            empCodeInput.focus();
        }
    }, 100);
}

		function toggleToolsDropdown() {
    const dropdown = document.getElementById('toolsDropdown');
    if (dropdown.style.display === 'none') {
        dropdown.style.display = 'block';
    } else {
        dropdown.style.display = 'none';
    }
}

function closeToolsDropdown() {
    document.getElementById('toolsDropdown').style.display = 'none';
}

// Close dropdown when clicking outside
document.addEventListener('click', function(e) {
    const toolsBtn = document.getElementById('toolsBtn');
    const toolsDropdown = document.getElementById('toolsDropdown');
    
    if (toolsBtn && toolsDropdown && 
        !toolsBtn.contains(e.target) && 
        !toolsDropdown.contains(e.target)) {
        closeToolsDropdown();
    }
});

        // ==============================================
        // EMPLOYEE BOARDS SYSTEM
        // ==============================================

		async function loadEmployeeBoards() {
			if (currentUser.role !== 'employee' && currentUser.role !== 'admin') return;
			
			await Promise.all([
				loadQABoard(),
				loadPeerBoard()
			]);
		}

async function loadQABoard() {
    try {
        const qaData = await getFromFirestore('qa_assignments');
        const userQAs = qaData.filter(qa => 
            qa.assignedTo === currentUser.code && 
            (qa.status === 'Pending' || qa.status === 'In Progress' || qa.status === 'Reverted')
        );
        
        // Update counter in toolbar with null check
		const empQACounter = document.getElementById('empQACounter');
		if (empQACounter) {
			const previousCount = parseInt(empQACounter.getAttribute('data-count')) || 0;
			
			if (userQAs.length > 0) {
				empQACounter.textContent = ' (' + userQAs.length + ')';
				empQACounter.style.display = 'inline';
				empQACounter.setAttribute('data-count', userQAs.length);
				
				// Add blink animation if count increased
				if (userQAs.length > previousCount && previousCount > 0) {
					empQACounter.classList.add('new-assignment');
					setTimeout(() => empQACounter.classList.remove('new-assignment'), 5000);
				}
           } else {
                empQACounter.textContent = '';
                empQACounter.style.display = 'none';
                empQACounter.setAttribute('data-count', 0);
            }
        }
        
        // Load content
        const qaContent = document.getElementById('qaContent');
        if (!qaContent) return;
        
        if (userQAs.length === 0) {
            qaContent.innerHTML = '<div style="text-align: center; color: #666; padding: 20px;">No QA assignments</div>';
            return;
        }
        
			const html = userQAs.map(qa => {
			const isOverdue = new Date(qa.dueDate) < new Date() && qa.status !== 'Completed';
			const isReverted = qa.status === 'Reverted';
			const urgencyClass = isOverdue ? 'urgent' : '';
			
			return `
				<div class="task-item ${urgencyClass}" style="${isReverted ? 'border-left: 4px solid #f39c12; background: #fff3cd;' : ''}">
					<div style="font-weight: bold; margin-bottom: 8px;">
						${isReverted ? '↩️ REVERTED BY HR - ' : ''}${qa.caseDetails}
						${isOverdue ? ' <span style="color: #dc3545;">(OVERDUE)</span>' : ''}
					</div>
					${isReverted ? `
						<div style="background: #f39c12; color: white; padding: 8px; border-radius: 4px; margin-bottom: 10px; font-size: 12px;">
							<strong>HR Feedback:</strong> ${qa.hrFeedback || 'Please review and resubmit'}
						</div>
					` : ''}
                    <div style="font-size: 12px; color: #666; margin-bottom: 10px;">
                        <strong>Due:</strong> ${qa.dueDate}<br>
                        <strong>Hospital:</strong> ${qa.hospitalName || 'N/A'}<br>
                        <strong>Accession:</strong> ${qa.accessionNo || 'N/A'}
                    </div>
                    <button onclick="openQAModal('${qa.id}')" class="btn" style="background: #e74c3c; font-size: 12px;">
                        Respond to QA
                    </button>
                </div>
            `;
        }).join('');
        
        qaContent.innerHTML = html;
        
    } catch (error) {
        console.error('Error loading QA board:', error);
    }
}

async function loadPeerBoard() {
    try {
        const peerData = await getFromFirestore('peer_review_assignments');
        const userPeers = peerData.filter(peer => 
            peer.assignedTo === currentUser.code && 
            (peer.status === 'Pending' || peer.status === 'In Progress')
        );
        
        // Update counter in toolbar
        const empPeerCounter = document.getElementById('empPeerCounter');
        if (empPeerCounter) {
            const previousCount = parseInt(empPeerCounter.getAttribute('data-count')) || 0;
            
            if (userPeers.length > 0) {
                empPeerCounter.textContent = ' (' + userPeers.length + ')';
                empPeerCounter.style.display = 'inline';
                empPeerCounter.setAttribute('data-count', userPeers.length);
                
                // Add blink animation if count increased
                if (userPeers.length > previousCount && previousCount > 0) {
                    empPeerCounter.classList.add('new-assignment');
                    setTimeout(() => empPeerCounter.classList.remove('new-assignment'), 5000);
                }
            } else {
                empPeerCounter.textContent = '';
                empPeerCounter.style.display = 'none';
                empPeerCounter.setAttribute('data-count', 0);
            }
        }
        
        // Load content
        const peerContent = document.getElementById('peerContent');
        if (!peerContent) return;
        
        if (userPeers.length === 0) {
            peerContent.innerHTML = '<div style="text-align: center; color: #666; padding: 20px;">No peer reviews</div>';
            return;
        }
        
        const html = userPeers.map(peer => {
            const isOverdue = new Date(peer.dueDate) < new Date();
            const urgencyClass = isOverdue ? 'urgent' : '';
            
            return `
                <div class="task-item ${urgencyClass}">
                    <div style="font-weight: bold; margin-bottom: 8px;">
                        Peer Review: ${peer.accession}
                        ${isOverdue ? ' <span style="color: #dc3545;">(OVERDUE)</span>' : ''}
                    </div>
                    <div style="font-size: 12px; color: #666; margin-bottom: 10px;">
                        <strong>Due:</strong> ${peer.dueDate}<br>
                        <strong>Original by:</strong> ${peer.originalSubmitter}<br>
                        <strong>Status:</strong> ${peer.status}
                    </div>
                    <button onclick="openPeerModal('${peer.id}')" class="btn" style="background: #9b59b6; font-size: 12px;">
                        ${peer.status === 'Completed' ? 'View Review' : 'Start Review'}
                    </button>
                </div>
            `;
        }).join('');
        
        peerContent.innerHTML = html;
        
    } catch (error) {
        console.error('Error loading peer board:', error);
    }
}

async function applyPeerFilters() {
    const fromDate = document.getElementById('peerFilterFromDate').value;
    const toDate = document.getElementById('peerFilterToDate').value;
    
    // Filter and reload peer data based on dates
    await loadHRPeerData(fromDate, toDate);
}

async function exportPeerData() {
    try {
        const peerData = await getFromFirestore('peer_review_assignments');
        const csvContent = convertPeerToCSV(peerData);
        downloadCSV(csvContent, `peer_reviews_${new Date().toISOString().split('T')[0]}.csv`);
        showNotification('Peer review data exported successfully!');
    } catch (error) {
        console.error('Error exporting peer data:', error);
        showNotification('Error exporting data.');
    }
}

function convertPeerToCSV(peerData) {
    if (peerData.length === 0) return '';
    
    const headers = ['Date', 'Original Reader', 'Peer Reviewer', 'Accession', 'Due Date', 'Completed Date', 'Status'];
    const rows = peerData.map(peer => [
        new Date(peer.assignedDate).toLocaleDateString(),
        peer.originalSubmitter,
        authorizedEmployees[peer.assignedTo]?.name || peer.assignedTo,
        peer.accession,
        peer.dueDate,
        peer.completedDate ? new Date(peer.completedDate).toLocaleDateString() : '',
        peer.status
    ]);
    
    return [headers.join(','), ...rows.map(row => row.join(','))].join('\n');
}

        // ==============================================
        // QA SYSTEM
        // ==============================================

async function openQAModal(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) return;
    
    const isReverted = qa.status === 'Reverted';
    
    const modal = createModal(`
        <h3>${isReverted ? '↩️ QA Assignment - REVERTED BY HR' : 'QA Assignment'}</h3>
        
        ${isReverted ? `
            <div style="background: #fff3cd; padding: 15px; border-left: 4px solid #f39c12; margin-bottom: 20px; border-radius: 4px;">
                <strong style="color: #856404;">⚠️ HR has reverted this QA back to you</strong>
                <div style="margin-top: 10px; color: #856404;">
                    <strong>Feedback:</strong> ${qa.hrFeedback || 'Please review and resubmit'}
                </div>
                <div style="font-size: 11px; margin-top: 5px; color: #856404;">
                    Reverted by: ${qa.revertedBy} on ${new Date(qa.revertedDate).toLocaleString()}
                </div>
            </div>
        ` : ''}
                
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
                    <p><strong>Case:</strong> ${qa.caseDetails}</p>
                    <p><strong>Due Date:</strong> ${qa.dueDate}</p>
                    <p><strong>Hospital:</strong> ${qa.hospitalName || 'N/A'}</p>
                    <p><strong>Accession:</strong> ${qa.accessionNo || 'N/A'}</p>
                    ${qa.instructions ? `<p><strong>Instructions:</strong> ${qa.instructions}</p>` : ''}
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label><strong>Your QA Response:</strong></label>
                    <textarea id="qaResponse" rows="8" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: monospace;"
                              placeholder="Enter your detailed QA response here...">${qa.report || ''}</textarea>
                </div>
                
                <div style="text-align: right;">
                    <button onclick="submitQAResponse('${qa.id}')" class="btn" style="background: #28a745; margin-right: 10px;">
                        Submit QA Response
                    </button>
                    <button onclick="closeModal()" class="btn" style="background: #6c757d;">Cancel</button>
                </div>
            `);
            
            // Mark as In Progress
            if (qa.status === 'Pending') {
                await updateFirestoreDoc('qa_assignments', qa.id, { status: 'In Progress' });
            }
        }

async function submitQAResponse(qaId) {
    const response = document.getElementById('qaResponse').value.trim();
    
    if (!response) {
        alert('Please enter your QA response before submitting.');
        return;
    }
    
    try {
        const allQAs = await getFromFirestore('qa_assignments');
        const qaData = allQAs.find(qa => qa.id === qaId);
        
        const isProxyEntry = qaData && qaData.isProxy && currentUser.role !== 'employee';
        
        let entryType = 'SELF';
        if (qaData && qaData.isProxy && currentUser.role !== 'employee') {
            entryType = 'PROXY';
        }
        
        const now = new Date();
        
        // Format user's LOCAL date as YYYY-MM-DD
        const localDate = now.getFullYear() + '-' + 
                         String(now.getMonth() + 1).padStart(2, '0') + '-' + 
                         String(now.getDate()).padStart(2, '0');
        
        const updateData = {
            report: response,
            status: 'Completed',
            submittedDate: now.toISOString(), // ✅ UTC for audit
            qaRespondedDate: localDate, // ✅ User's local date
            respondedBy: currentUser.code,
            actualEntryType: entryType
        };
        
        // Clear revert data on resubmission
        if (qaData.status === 'Reverted') {
            updateData.revertedBy = '';
            updateData.revertedDate = '';
            updateData.hrFeedback = '';
        }
        
        await updateFirestoreDoc('qa_assignments', qaId, updateData);
        
        showNotification('QA response submitted successfully!');
        closeModal();
        
        if (currentUser.role === 'employee') {
            loadEmployeeBoards();
        } else {
            loadHRQAData();
        }
        
    } catch (error) {
        console.error('Error submitting QA response:', error);
        alert('Error submitting response. Please try again.');
    }
}
async function openProxyQAModal(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) return;
    
    const employee = authorizedEmployees[qa.assignedTo];
    const employeeName = employee ? employee.name : qa.assignedTo;
    
    const modal = createModal(`
        <h3>🔄 Proxy QA Entry</h3>
        
        <div style="background: #fff3cd; padding: 12px; border-radius: 8px; margin-bottom: 15px; border-left: 4px solid #ffc107;">
            <strong style="color: #856404;">⚠️ You are entering response on behalf of:</strong>
            <div style="font-size: 16px; margin-top: 5px; color: #856404; font-weight: 600;">${employeeName} (${qa.assignedTo})</div>
        </div>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <p><strong>Case:</strong> ${qa.caseDetails}</p>
            <p><strong>Due Date:</strong> ${qa.dueDate}</p>
            <p><strong>Hospital:</strong> ${qa.hospitalName || 'N/A'}</p>
            <p><strong>Accession:</strong> ${qa.accessionNo || 'N/A'}</p>
            ${qa.instructions ? `<p><strong>Instructions:</strong> ${qa.instructions}</p>` : ''}
        </div>
        
        <div style="margin-bottom: 15px;">
            <label><strong>Response received via:</strong></label>
            <select id="proxyResponseSource" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; margin-top: 5px;">
                <option value="Email">Email</option>
                <option value="WhatsApp">WhatsApp</option>
                <option value="Phone">Phone Call</option>
                <option value="In-Person">In-Person</option>
            </select>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label><strong>QA Response:</strong></label>
            <textarea id="proxyQAResponse" rows="8" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: monospace; margin-top: 5px;"
                      placeholder="Enter the employee's QA response here..."></textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="submitProxyQAResponse('${qa.id}')" class="btn" style="background: #28a745; margin-right: 10px;">
                Submit Proxy Response
            </button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Cancel</button>
        </div>
    `);
}

async function submitProxyQAResponse(qaId) {
    const response = document.getElementById('proxyQAResponse').value.trim();
    const responseSource = document.getElementById('proxyResponseSource').value;
    
    if (!response) {
        alert('Please enter the QA response before submitting.');
        return;
    }
    
    try {
        const qaData = await getFromFirestore('qa_assignments');
        const qa = qaData.find(q => q.id === qaId);
        
        if (!qa) {
            alert('QA assignment not found. Please refresh and try again.');
            return;
        }
        
        const now = new Date();
        
        // Format local date as YYYY-MM-DD
        const localDate = now.getFullYear() + '-' + 
                         String(now.getMonth() + 1).padStart(2, '0') + '-' + 
                         String(now.getDate()).padStart(2, '0');
        
        await updateFirestoreDoc('qa_assignments', qaId, {
            report: response,
            status: 'Completed',
            submittedDate: now.toISOString(), // Keep UTC for exact timestamp
            qaRespondedDate: localDate, // Use local date for user-facing date
            
            enteredBy: currentUser.code || currentUser.username,
            actualRespondent: qa.assignedTo,
            entryType: 'PROXY',
            responseSource: responseSource,
            proxyEntryDate: now.toISOString() // Keep UTC for exact timestamp
        });
        
        showNotification('✅ Proxy QA response submitted successfully!');
        closeModal();
        loadHRQAData();
        
    } catch (error) {
        console.error('Error submitting proxy QA response:', error);
        alert('Error submitting response. Please try again.');
    }
}

// Helper function
async function getFirestoreDocId(collection, customId) {
    const snapshot = await db.collection(collection).get();
    let docId = null;
    snapshot.forEach(doc => {
        if (doc.data().id === customId) {
            docId = doc.id;
        }
    });
    return docId;
}

function displayProxyToggles() {
    const container = document.getElementById('proxyToggleList');
    if (!container) return;
    
    const employees = Object.entries(authorizedEmployees)
        .filter(([code, emp]) => emp.role === 'employee');
    
    if (employees.length === 0) {
        container.innerHTML = '<p style="color: #666; text-align: center;">No employees found. Add employees first.</p>';
        return;
    }
    
    container.innerHTML = employees.map(([code, emp]) => `
        <div style="display: flex; justify-content: space-between; align-items: center; padding: 10px; border-bottom: 1px solid #dee2e6; background: ${emp.proxyEnabled ? '#e8f5e9' : 'white'};">
            <div>
                <strong>${code}</strong> - ${emp.name}
                <span style="font-size: 11px; color: #666;">(${emp.category})</span>
            </div>
            <label style="cursor: pointer; display: flex; align-items: center; gap: 8px; pointer-events: auto;">
                <input type="checkbox" 
                       id="proxy_${code}" 
                       ${emp.proxyEnabled ? 'checked' : ''} 
                       onchange="toggleProxyForEmployee('${code}', this.checked)"
                       style="transform: scale(1.3); pointer-events: auto; cursor: pointer;">
                <span style="font-weight: 500; color: ${emp.proxyEnabled ? '#27ae60' : '#95a5a6'}; pointer-events: none;">
                    ${emp.proxyEnabled ? '✓ Proxy ON' : 'Proxy OFF'}
                </span>
            </label>
        </div>
    `).join('');
}

// Toggle proxy for specific employee
async function toggleProxyForEmployee(empCode, isEnabled) {
    try {
        // Update in memory
        authorizedEmployees[empCode].proxyEnabled = isEnabled;
        
        // Save to correct Firestore location
        await db.collection('system_data').doc('employees').set({
            data: authorizedEmployees,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        showNotification(`✅ Proxy ${isEnabled ? 'enabled' : 'disabled'} for ${empCode}`);
        console.log(`[PROXY] ${empCode} proxy set to ${isEnabled}`);
        
    } catch (error) {
        console.error('Error toggling proxy:', error);
        alert('❌ Failed to update proxy setting');
    }
}

// Refresh proxy toggles display
function refreshProxyToggles() {
    displayProxyToggles();
    showNotification('Proxy settings refreshed');
}

// Load Monthly Peer Chart
async function loadMonthlyPeerChart(peerData) {
    const ctx = document.getElementById('monthlyPeerChart');
    if (!ctx) return;
    
    if (monthlyPeerChart) {
        monthlyPeerChart.destroy();
    }
    
    const monthlyData = {};
    peerData.forEach(peer => {
        if (peer.completedDate) {
            const month = new Date(peer.completedDate).toLocaleDateString('en-US', { year: 'numeric', month: 'short' });
            monthlyData[month] = (monthlyData[month] || 0) + 1;
        }
    });
    
    const months = [];
    const counts = [];
    const now = new Date();
    
    for (let i = 11; i >= 0; i--) {
        const date = new Date(now.getFullYear(), now.getMonth() - i, 1);
        const monthKey = date.toLocaleDateString('en-US', { year: 'numeric', month: 'short' });
        months.push(monthKey);
        counts.push(monthlyData[monthKey] || 0);
    }
    
    monthlyPeerChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: months,
            datasets: [{
                label: 'Peer Reviews Completed',
                data: counts,
                backgroundColor: '#9b59b6',
                borderColor: '#8e44ad',
                borderWidth: 1
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
                y: {
                    beginAtZero: true,
                    ticks: { stepSize: 1 }
                }
            },
            plugins: { legend: { display: false } }
        }
    });
}

async function applyPeerFilters() {
    // Implementation for peer filtering
    await loadHRPeerData();
}

function clearPeerFilters() {
    document.getElementById('peerFilterFrom').value = '';
    document.getElementById('peerFilterTo').value = '';
    document.getElementById('peerFilterRad').value = '';
    document.getElementById('peerFilterStatus').value = '';
    loadHRPeerData();
}
        // ==============================================
        // PEER REVIEW SYSTEM
        // ==============================================

        async function openPeerModal(peerId) {
            const peerData = await getFromFirestore('peer_review_assignments');
            const peer = peerData.find(p => p.id === peerId);
            
            if (!peer) return;
            
            const modal = createModal(`
                <h3>Peer Review Assignment</h3>
                
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                        <div>
                            <strong>Accession:</strong> ${peer.accession}<br>
                            <strong>Original Reader:</strong> ${peer.originalSubmitter}<br>
                            <strong>Due Date:</strong> ${peer.dueDate}
                        </div>
                        <div>
                            <strong>Assigned:</strong> ${new Date(peer.assignedDate).toLocaleDateString()}<br>
                            <strong>Status:</strong> ${peer.status}<br>
                            ${peer.instructions ? `<strong>Instructions:</strong> ${peer.instructions}` : ''}
                        </div>
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                    <div>
                        <h4 style="color: #3498db;">Original Report</h4>
                        <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; height: 300px; overflow-y: auto; 
                            font-family: monospace; font-size: 12px; white-space: pre-wrap; border: 2px solid #3498db;">
${peer.originalReport}</div>
                    </div>
                    <div>
                        <h4 style="color: #e74c3c;">Your Peer Review</h4>
                        <textarea id="peerResponse" style="width: 100%; height: 300px; padding: 15px; border: 2px solid #e74c3c; 
                            border-radius: 5px; font-family: monospace; font-size: 12px;" 
                            placeholder="Enter your peer review here...">${peer.peerReport || ''}</textarea>
                    </div>
                </div>
                
                <div style="text-align: right;">
                    <button onclick="submitPeerResponse('${peer.id}')" class="btn" style="background: #9b59b6; margin-right: 10px;">
                        ${peer.status === 'Completed' ? 'Update Review' : 'Submit Review'}
                    </button>
                    <button onclick="closeModal()" class="btn" style="background: #6c757d;">Close</button>
                </div>
            `);
            
            // Mark as In Progress
            if (peer.status === 'Pending') {
                await updateFirestoreDoc('peer_review_assignments', peer.id, { status: 'In Progress' });
            }
        }
async function submitPeerResponse(peerId) {
            const response = document.getElementById('peerResponse').value.trim();
            
            if (!response) {
                alert('Please enter your peer review before submitting.');
                return;
            }
            
            try {
                await updateFirestoreDoc('peer_review_assignments', peerId, {
                    peerReport: response,
                    status: 'Completed',
                    completedDate: new Date().toISOString()
                });
                
                showNotification('Peer review submitted successfully!');
                closeModal();
                loadEmployeeBoards();
                
            } catch (error) {
                console.error('Error submitting peer review:', error);
                alert('Error submitting review. Please try again.');
            }
        }

        // ==============================================
        // HR SYSTEM
        // ==============================================
function selectHRTab(tab) {
    // Close dropdown
    closeHREventsDropdown();
    
    document.querySelectorAll('.hr-tab').forEach(t => t.classList.remove('active'));
    document.querySelector(`[onclick*="selectHRTab('${tab}')"]`)?.classList.add('active');
    
    document.getElementById('hrQAPanel').style.display = 'none';
    document.getElementById('hrPeerPanel').style.display = 'none';
    document.getElementById('hrSchedulePanel').style.display = 'none';
    document.getElementById('hrMeetingsPanel').style.display = 'none';
	document.getElementById('hrReportsPanel').style.display = 'none';
	document.getElementById('hrTimeLogsPanel').style.display = 'none';
	document.getElementById('bodyPartRulesPanel').style.display = 'none';
	document.getElementById('passwordManagementPanel').style.display = 'none';

    
    switch(tab) {
        case 'QA':
            document.getElementById('hrQAPanel').style.display = 'block';
            loadHRQAData();
            break;
        case 'PeerReview':
            document.getElementById('hrPeerPanel').style.display = 'block';
            loadHRPeerData();
            break;
        case 'Schedule':
            document.getElementById('hrSchedulePanel').style.display = 'block';
            currentScheduleMonth = new Date();
            loadHRSchedule();
            updateLeaveRequestCounter();
            break;
        case 'Meetings':
            document.getElementById('hrMeetingsPanel').style.display = 'block';
            loadHRMeetingsPanel();
            break;
		case 'Reports':
            document.getElementById('hrReportsPanel').style.display = 'block';
            loadHRReportsPanel();
            break;
		case 'TimeLogs':
			document.getElementById('hrTimeLogsPanel').style.display = 'block';
			loadHRTimeLogs();
			break;
		case 'BodyPartRules': 
            document.getElementById('bodyPartRulesPanel').style.display = 'block';
            initializeBodyPartRulesSystem();
            break;
		case 'PasswordManagement':
			document.getElementById('passwordManagementPanel').style.display = 'block';
			loadHRPasswordManagement();
			break;
    }
}
async function loadHRQAData() {
    try {
        const qaData = await getFromFirestore('qa_assignments');
        allQAData = qaData.sort((a, b) => new Date(b.createdDate) - new Date(a.createdDate));
        
        updateQAStatistics(allQAData);
        loadMonthlyQAChart(allQAData);
        populateRadiologistFilter();
        
        applyQAFilters();
        
    } catch (error) {
        console.error('Error loading HR QA data:', error);
        document.getElementById('qaTableBody').innerHTML = '<tr><td colspan="9" style="padding: 20px; text-align: center; color: #e74c3c;">Error loading QA data</td></tr>';
    }
}
async function loadHRPeerData() {
    try {
        // Load pending submissions (waiting for assignment)
        const submissions = await getFromFirestore('peer_review_submissions');
        const pendingSubmissions = submissions.filter(sub => 
            !sub.assignmentStatus || sub.assignmentStatus === 'unassigned'
        );
        
        // Update HR notification counter
        const hrPeerCounter = document.getElementById('hrPeerCounter');
        if (pendingSubmissions.length > 0) {
            hrPeerCounter.textContent = pendingSubmissions.length;
            hrPeerCounter.style.display = 'block';
        } else {
            hrPeerCounter.style.display = 'none';
        }
        
        // Load pending submissions list
        const pendingDiv = document.getElementById('pendingSubmissions');
        if (pendingSubmissions.length === 0) {
            pendingDiv.innerHTML = '<div style="text-align: center; color: #666; padding: 20px;">No pending submissions</div>';
        } else {
            const pendingHtml = pendingSubmissions.map(sub => `
                <div style="background: white; padding: 15px; margin: 10px 0; border-radius: 8px; border-left: 4px solid #ffc107; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
                    <div style="display: flex; justify-content: space-between; align-items: start;">
                        <div style="flex: 1;">
                            <div style="font-weight: bold; margin-bottom: 5px;">
                                Accession: ${sub.accession}
                            </div>
                            <div style="font-size: 12px; color: #666; margin-bottom: 8px;">
                                <strong>Submitted by:</strong> ${sub.submitter} (${sub.submitterCode}) on ${new Date(sub.timestamp).toLocaleDateString()}
                            </div>
                            <div style="background: #f8f9fa; padding: 8px; border-radius: 4px; font-size: 11px; font-family: monospace;">
                                <strong>Report Preview:</strong><br>
                                ${sub.report ? sub.report.substring(0, 150) + '...' : 'No report'}
                            </div>
                        </div>
                        <button onclick="assignPeerReview('${sub.id}')" class="btn" style="background: #9b59b6; margin-left: 15px;">
                            Assign for Review
                        </button>
                    </div>
                </div>
            `).join('');
            
            pendingDiv.innerHTML = pendingHtml;
        }
        
        // Load completed reviews
        const assignments = await getFromFirestore('peer_review_assignments');
		loadMonthlyPeerChart(assignments);
        const completedReviews = assignments.filter(a => a.status === 'Completed');
        
        const completedDiv = document.getElementById('completedReviews');
        if (completedReviews.length === 0) {
            completedDiv.innerHTML = '<div style="text-align: center; color: #666; padding: 20px;">No completed reviews</div>';
        } else {
            const completedHtml = completedReviews.map(review => `
                <div style="background: white; padding: 15px; margin: 10px 0; border-radius: 8px; border-left: 4px solid #28a745; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
                    <div style="display: flex; justify-content: space-between; align-items: start;">
                        <div style="flex: 1;">
                            <div style="font-weight: bold; margin-bottom: 5px;">
                                ${review.accession} - Peer Review Completed
                            </div>
                            <div style="font-size: 12px; color: #666; margin-bottom: 8px;">
                                <strong>Original:</strong> ${review.originalSubmitter} | 
                                <strong>Reviewer:</strong> ${authorizedEmployees[review.assignedTo]?.name || review.assignedTo} |
                                <strong>Completed:</strong> ${new Date(review.completedDate).toLocaleDateString()}
                            </div>
                        </div>
                        <button onclick="viewPeerComparison('${review.id}')" class="btn" style="background: #28a745;">
                            View Comparison
                        </button>
                    </div>
                </div>
            `).join('');
            
            completedDiv.innerHTML = completedHtml;
        }
        
    } catch (error) {
        console.error('Error loading HR peer data:', error);
    }
}

async function assignPeerReview(submissionId) {
    const submissions = await getFromFirestore('peer_review_submissions');
    const submission = submissions.find(s => s.id === submissionId);
    
    if (!submission) return;
    
    const modal = createModal(`
        <h3>Assign Peer Review</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <p><strong>Original Report by:</strong> ${submission.submitter} (${submission.submitterCode})</p>
            <p><strong>Accession:</strong> ${submission.accession}</p>
            <p><strong>Submitted:</strong> ${new Date(submission.timestamp).toLocaleString()}</p>
        </div>
        
        <div style="margin-bottom: 20px;">
            <h4>Original Report:</h4>
            <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; max-height: 200px; overflow-y: auto; 
                font-family: monospace; font-size: 12px; white-space: pre-wrap;">
${submission.report}</div>
        </div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin: 20px 0;">
            <div>
                <label><strong>Assign to Radiologist:</strong></label>
                <select id="assignToEmployee" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; margin-top: 5px;">
                    <option value="">Select Employee...</option>
                    ${Object.entries(authorizedEmployees)
                        .filter(([code, emp]) => emp.role === 'employee')
                        .map(([code, emp]) => `<option value="${code}">${emp.name} (${code})</option>`)
                        .join('')}
                </select>
            </div>
            <div>
                <label><strong>Due Date:</strong></label>
                <input type="date" id="assignDueDate" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; margin-top: 5px;" 
                       value="${new Date(Date.now() + 7 * 24 * 60 * 60 * 1000).toISOString().split('T')[0]}">
            </div>
        </div>
        
        <div style="margin: 15px 0;">
            <label><strong>Instructions for Reviewer:</strong></label>
            <textarea id="assignInstructions" rows="3" placeholder="Special instructions..." 
                style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; margin-top: 5px;"></textarea>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="savePeerAssignment('${submissionId}')" class="btn" style="background: #9b59b6; margin-right: 10px;">
                Assign Peer Review
            </button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Cancel</button>
        </div>
    `);
}

async function savePeerAssignment(submissionId) {
    const assignedTo = document.getElementById('assignToEmployee').value;
    const dueDate = document.getElementById('assignDueDate').value;
    const instructions = document.getElementById('assignInstructions').value.trim();
    
    if (!assignedTo || !dueDate) {
        alert('Please select a radiologist and due date.');
        return;
    }
    
    try {
        const submissions = await getFromFirestore('peer_review_submissions');
        const submission = submissions.find(s => s.id === submissionId);
        
        // Create peer review assignment
        const assignmentId = 'PEER_' + Date.now();
        const peerAssignment = {
            id: assignmentId,
            originalSubmissionId: submissionId,
            originalSubmitter: submission.submitter,
            originalSubmitterCode: submission.submitterCode,
            accession: submission.accession,
            originalReport: submission.report,
            assignedTo: assignedTo,
            instructions: instructions,
            dueDate: dueDate,
            status: 'Pending',
            assignedBy: currentUser.code || currentUser.username,
            assignedDate: new Date().toISOString(),
            peerReport: '',
            completedDate: ''
        };
        
        await saveToFirestore('peer_review_assignments', peerAssignment);
        
        // Update submission status
        await updateFirestoreDoc('peer_review_submissions', submissionId, {
            assignmentStatus: 'assigned',
            assignedDate: new Date().toISOString()
        });
        
        showNotification('Peer review assigned successfully!');
        closeModal();
        loadHRPeerData();
        
    } catch (error) {
        console.error('Error assigning peer review:', error);
        alert('Error assigning peer review. Please try again.');
    }
}

async function viewPeerComparison(assignmentId) {
    const assignments = await getFromFirestore('peer_review_assignments');
    const assignment = assignments.find(a => a.id === assignmentId);
    
    if (!assignment) return;
    
    const employee = authorizedEmployees[assignment.assignedTo];
    const reviewerName = employee ? employee.name : assignment.assignedTo;
    
    const modal = createModal(`
        <h3>Peer Review Comparison</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                <div>
                    <strong>Original Reader:</strong> ${assignment.originalSubmitter}<br>
                    <strong>Accession:</strong> ${assignment.accession}<br>
                    <strong>Assigned Date:</strong> ${new Date(assignment.assignedDate).toLocaleDateString()}
                </div>
                <div>
                    <strong>Peer Reviewer:</strong> ${reviewerName}<br>
                    <strong>Due Date:</strong> ${assignment.dueDate}<br>
                    <strong>Completed:</strong> ${new Date(assignment.completedDate).toLocaleDateString()}
                </div>
            </div>
        </div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
            <div>
                <h4 style="color: #3498db; margin-bottom: 10px;">Original Report</h4>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; height: 300px; overflow-y: auto; 
                    font-family: monospace; font-size: 12px; white-space: pre-wrap; border: 2px solid #3498db;">
${assignment.originalReport}</div>
            </div>
            <div>
                <h4 style="color: #e74c3c; margin-bottom: 10px;">Peer Review Report</h4>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; height: 300px; overflow-y: auto; 
                    font-family: monospace; font-size: 12px; white-space: pre-wrap; border: 2px solid #e74c3c;">
${assignment.peerReport}</div>
            </div>
        </div>
        
        <div style="text-align: right;">
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Close</button>
        </div>
    `);
}

async function loadHRPasswordManagement() {
    console.log('[HR Password Mgmt] Loading...');
    
    await loadSystemData();
    
    const container = document.getElementById('passwordManagementContent');
    if (!container) {
        console.error('[HR Password Mgmt] Container not found');
        return;
    }
    
    const employees = Object.entries(authorizedEmployees)
        .filter(([code, emp]) => emp.role === 'employee')
        .sort((a, b) => a[1].name.localeCompare(b[1].name));
    
    if (employees.length === 0) {
        container.innerHTML = '<p style="color: #666; padding: 20px;">No employees found in system.</p>';
        return;
    }
    
    const html = `
<div style="
    background: #ffffff;
    padding: 24px;
    border-radius: 14px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.08);
">
    <div style="display: flex; justify-content: space-between; align-items: center;">
        <div>
            <h3 style="margin: 0; color: #2c3e50;">🔐 Employee Password Management</h3>
            <p style="margin: 6px 0 0; color: #7f8c8d; font-size: 13px;">
                Securely manage employee login credentials and account status
            </p>
        </div>
    </div>

    <div style="
        max-height: 600px;
        overflow-y: auto;
        margin-top: 20px;
        border-radius: 10px;
        border: 1px solid #ecf0f1;
    ">
        <table style="
            width: 100%;
            border-collapse: collapse;
            font-size: 13px;
            background: #fff;
        ">
            <thead style="
                position: sticky;
                top: 0;
                background: linear-gradient(90deg, #34495e, #2c3e50);
                color: white;
                z-index: 5;
            ">
                <tr>
                    <th style="padding: 14px; text-align: left;">Employee</th>
                    <th style="padding: 14px; text-align: center;">Code</th>
                    <th style="padding: 14px; text-align: center;">Password</th>
                    <th style="padding: 14px; text-align: center;">Reminders</th>
                    <th style="padding: 14px; text-align: center;">Status</th>
                    <th style="padding: 14px; text-align: center;">Actions</th>
                </tr>
            </thead>
            <tbody>
                ${employees.map(([empCode, emp]) => {
                    const hasPassword = emp.passwordSet || false;
                    const reminderCount = emp.passwordReminderCount || 0;
                    const isLocked = emp.accountLocked || false;
                    const mustChange = emp.mustChangePassword || false;
                    const failedAttempts = emp.failedLoginAttempts || 0;

                    let statusBadge = '';
                    if (isLocked) {
                        statusBadge = '<span style="background:#e74c3c;color:#fff;padding:5px 12px;border-radius:20px;font-weight:600;">🔒 LOCKED</span>';
                    } else if (mustChange) {
                        statusBadge = '<span style="background:#f39c12;color:#fff;padding:5px 12px;border-radius:20px;font-weight:600;">⚠️ MUST CHANGE</span>';
                    } else if (!hasPassword && reminderCount >= 10) {
                        statusBadge = '<span style="background:#c0392b;color:#fff;padding:5px 12px;border-radius:20px;font-weight:600;">⛔ SUSPENDED</span>';
                    } else if (!hasPassword) {
                        statusBadge = '<span style="background:#95a5a6;color:#fff;padding:5px 12px;border-radius:20px;font-weight:600;">❌ NO PASSWORD</span>';
                    } else {
                        statusBadge = '<span style="background:#27ae60;color:#fff;padding:5px 12px;border-radius:20px;font-weight:600;">✅ ACTIVE</span>';
                    }

                    return `
                    <tr style="border-bottom: 1px solid #ecf0f1;">
                        <td style="padding: 14px; font-weight: 600; color: #2c3e50;">
                            ${emp.name}
                        </td>
                        <td style="padding: 14px; text-align: center; font-weight: 600;">
                            ${empCode}
                        </td>
                        <td style="padding: 14px; text-align: center;">
                            ${hasPassword ? '✅ Yes' : '❌ No'}
                        </td>
                        <td style="padding: 14px; text-align: center;">
                            ${reminderCount}
                            ${reminderCount >= 8 ? '<span style="color:#e74c3c;font-weight:700;"> ⚠</span>' : ''}
                        </td>
                        <td style="padding: 14px; text-align: center;">
                            ${statusBadge}
                        </td>
                        <td style="padding: 14px; text-align: center;">
                            ${isLocked ? `
                                <button onclick="hrUnlockEmployee('${empCode}')" 
                                    style="background:#27ae60;color:#fff;border:none;padding:7px 14px;border-radius:6px;font-size:12px;cursor:pointer;margin:2px;">
                                    🔓 Unlock
                                </button>` : ''}
                            <button onclick="hrResetPassword('${empCode}')"
                                style="background:#e67e22;color:#fff;border:none;padding:7px 14px;border-radius:6px;font-size:12px;cursor:pointer;margin:2px;">
                                🔑 Reset
                            </button>
                            ${failedAttempts > 0 ? `
                                <div style="font-size:11px;color:#e74c3c;margin-top:6px;">
                                    Failed attempts: ${failedAttempts}
                                </div>` : ''}
                        </td>
                    </tr>
                    `;
                }).join('')}
            </tbody>
        </table>
    </div>
</div>
`;

    
    container.innerHTML = html;
    console.log('[HR Password Mgmt] Loaded successfully');
}

async function hrResetPassword(empCode) {
    const emp = authorizedEmployees[empCode];
    if (!emp) {
        alert('Employee not found.');
        return;
    }
    
    const newPassword = prompt(`Reset password for ${emp.name} (${empCode})\n\nEnter new temporary password (min 4 characters):`);
    
    if (!newPassword || newPassword.trim().length < 4) {
        alert('Password must be at least 4 characters.');
        return;
    }
    
    if (!confirm(`Confirm password reset for ${emp.name}?\n\nEmployee will be required to change this password on next login.`)) {
        return;
    }
    
    try {
        await updateEmployeeFieldDirectly(empCode, {
            password: newPassword.trim().toLowerCase(),
            passwordSet: true,
            mustChangePassword: true,
            passwordResetBy: currentUser.code,
            passwordResetDate: new Date().toISOString(),
            accountLocked: false,
            failedLoginAttempts: 0
        });
        
        showNotification(`✅ Password reset for ${emp.name}. Employee must change on next login.`);
        loadHRPasswordManagement(); // Reload table
        
    } catch (error) {
        console.error('[HR] Error resetting password:', error);
        alert('Failed to reset password. Please try again.');
    }
}

async function hrUnlockEmployee(empCode) {
    const emp = authorizedEmployees[empCode];
    if (!emp) {
        alert('Employee not found.');
        return;
    }
    
    if (!confirm(`Unlock account for ${emp.name} (${empCode})?`)) {
        return;
    }
    
    try {
        await updateEmployeeFieldDirectly(empCode, {
            accountLocked: false,
            failedLoginAttempts: 0,
            unlockedBy: currentUser.code,
            unlockedDate: new Date().toISOString()
        });
        
        showNotification(`✅ Account unlocked for ${emp.name}`);
        loadHRPasswordManagement(); // Reload table
        
    } catch (error) {
        console.error('[HR] Error unlocking account:', error);
        alert('Failed to unlock account. Please try again.');
    }
}


// ===== WHAT'S NEW FEATURE =====
async function toggleWhatsNewDropdown() {
    const dropdown = document.getElementById('whatsNewDropdown');
    const toolsDropdown = document.getElementById('toolsDropdown');
    
    // Close tools dropdown if open
    if (toolsDropdown && toolsDropdown.style.display === 'block') {
        toolsDropdown.style.display = 'none';
    }
    
    if (dropdown.style.display === 'none' || dropdown.style.display === '') {
        dropdown.style.display = 'block';
        await loadWhatsNewContent();
        
        // Mark as read for this user
        await markWhatsNewAsRead();
        hideWhatsNewBell();
    } else {
        dropdown.style.display = 'none';
    }
}
async function loadWhatsNewContent() {
    const contentDiv = document.getElementById('whatsNewContent');
    const lastUpdatedSpan = document.getElementById('whatsNewLastUpdated');
    const adminControls = document.getElementById('whatsNewAdminControls');
    
    // Show admin controls ONLY if user is admin
    if (currentUserRole === 'admin') {
        adminControls.style.display = 'block';
    } else {
        adminControls.style.display = 'none';
    }
    
    try {
        const whatsNewRef = db.collection('whatsNew').doc('announcement');
        const doc = await whatsNewRef.get();
        
        if (doc.exists) {
            const data = doc.data();
            const content = data.content || '';
            const timestamp = data.timestamp;
            
            if (content.trim() !== '') {
                const formattedContent = formatWhatsNewContent(content);
                contentDiv.innerHTML = formattedContent;
                
                if (timestamp) {
                    const date = new Date(timestamp);
                    lastUpdatedSpan.textContent = date.toLocaleDateString() + ' ' + date.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                }
            } else {
                contentDiv.innerHTML = `
                    <div style="text-align: center; color: #999; padding: 40px 20px;">
                        <div style="font-size: 32px; margin-bottom: 10px;">📢</div>
                        <div style="font-size: 14px;">No announcements yet</div>
                    </div>
                `;
                lastUpdatedSpan.textContent = 'Never';
            }
        } else {
            contentDiv.innerHTML = `
                <div style="text-align: center; color: #999; padding: 40px 20px;">
                    <div style="font-size: 32px; margin-bottom: 10px;">📢</div>
                    <div style="font-size: 14px;">No announcements yet</div>
                </div>
            `;
            lastUpdatedSpan.textContent = 'Never';
        }
    } catch (error) {
        console.error('Error loading What\'s New:', error);
        contentDiv.innerHTML = '<div style="color: #e74c3c; padding: 20px;">Error loading announcements</div>';
    }
}

function formatWhatsNewContent(content) {
    // Convert plain text to formatted HTML
    let formatted = content
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/\n\n/g, '<br><br>') // Double line breaks
        .replace(/\n/g, '<br>') // Single line breaks
        .replace(/^• (.+)$/gm, '<div style="margin-left: 20px; margin-bottom: 5px;">• $1</div>') // Bullets
        .replace(/^\* (.+)$/gm, '<div style="margin-left: 20px; margin-bottom: 5px;">• $1</div>') // Asterisk bullets
        .replace(/^- (.+)$/gm, '<div style="margin-left: 20px; margin-bottom: 5px;">• $1</div>'); // Dash bullets
    
    return formatted;
}

async function startEditWhatsNew() {
    const contentDiv = document.getElementById('whatsNewContent');
    const editSection = document.getElementById('whatsNewEditSection');
    const adminControls = document.getElementById('whatsNewAdminControls');
    const editor = document.getElementById('whatsNewEditor');
    
    try {
        const whatsNewRef = db.collection('whatsNew').doc('announcement');
        const doc = await whatsNewRef.get();
        
        if (doc.exists) {
            editor.value = doc.data().content || '';
        } else {
            editor.value = '';
        }
        
        contentDiv.style.display = 'none';
        adminControls.style.display = 'none';
        editSection.style.display = 'block';
        
    } catch (error) {
        console.error('Error loading content for edit:', error);
        editor.value = '';
        editSection.style.display = 'block';
    }
}

async function saveWhatsNew() {
    // Only admin can save
    if (currentUserRole !== 'admin') {
        alert('❌ Only administrators can edit announcements');
        return;
    }
    
    const editor = document.getElementById('whatsNewEditor');
    const content = editor.value.trim();
    
    try {
        // Save to Firebase
        const whatsNewRef = db.collection('whatsNew').doc('announcement');
        await whatsNewRef.set({
            content: content,
            timestamp: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username,
            readBy: {} // Reset read status when new content is posted
        });
        
        showNotification('✅ What\'s New updated successfully!', 'success');
        
        // Close editor and reload content
        cancelWhatsNewEdit();
        loadWhatsNewContent();
        
        // Show bell for current admin too
        showWhatsNewBell();
        
    } catch (error) {
        console.error('Error saving What\'s New:', error);
        alert('❌ Error saving announcement');
    }
}

function cancelWhatsNewEdit() {
    const contentDiv = document.getElementById('whatsNewContent');
    const editSection = document.getElementById('whatsNewEditSection');
    const adminControls = document.getElementById('whatsNewAdminControls');
    
    contentDiv.style.display = 'block';
    editSection.style.display = 'none';
    
    // Only show admin controls if user is admin
    if (currentUserRole === 'admin') {
        adminControls.style.display = 'block';
    } else {
        adminControls.style.display = 'none';
    }
}
// 🔔 Mark What's New as read for current user
async function markWhatsNewAsRead() {
    if (!currentUser || !currentUser.code) return;
    
    try {
        const whatsNewRef = db.collection('whatsNew').doc('announcement');
        const userCode = currentUser.code;
        
        await whatsNewRef.update({
            [`readBy.${userCode}`]: new Date().toISOString()
        });
    } catch (error) {
        console.error('Error marking as read:', error);
    }
}

// 🔔 Check if current user has unread What's New
async function checkWhatsNewUnread() {
    if (!currentUser || !currentUser.code) return;
    
    try {
        const whatsNewRef = db.collection('whatsNew').doc('announcement');
        const doc = await whatsNewRef.get();
        
        if (doc.exists) {
            const data = doc.data();
            const userCode = currentUser.code;
            const readBy = data.readBy || {};
            
            // If user hasn't read it, show bell
            if (!readBy[userCode]) {
                showWhatsNewBell();
            } else {
                hideWhatsNewBell();
            }
        }
    } catch (error) {
        console.error('Error checking unread status:', error);
    }
}

// 🔔 Show bell notification
function showWhatsNewBell() {
    const bell = document.getElementById('whatsNewBell');
    if (bell) {
        bell.classList.remove('hidden');
    }
}

// 🔔 Hide bell notification
function hideWhatsNewBell() {
    const bell = document.getElementById('whatsNewBell');
    if (bell) {
        bell.classList.add('hidden');
    }
}

// Close What's New dropdown when clicking outside
document.addEventListener('click', function(e) {
    const dropdown = document.getElementById('whatsNewDropdown');
    const btn = document.getElementById('whatsNewBtn');
    
    if (dropdown && btn && 
        !dropdown.contains(e.target) && 
        !btn.contains(e.target)) {
        dropdown.style.display = 'none';
    }
});

// ==============================================
// QA MANAGEMENT FUNCTIONS
// ==============================================

	async function createNewQA() {
    const modal = createModal(`
        <h3>Create New QA Assignment</h3>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin: 20px 0;">
			<div>
				<label>Assign to Employee:</label>
				<select id="qaAssignEmployee" onchange="checkQAProxyStatus()" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
					<option value="">Select Employee...</option>
					${Object.entries(authorizedEmployees)
						.filter(([code, emp]) => emp.role === 'employee')
						.map(([code, emp]) => {
							const proxyLabel = emp.proxyEnabled ? ' [PROXY]' : '';
							return `<option value="${code}" data-proxy="${emp.proxyEnabled || false}">${emp.name} (${code})${proxyLabel}</option>`;
						})
						.join('')}
				</select>
			</div>
            <div>
                <label>Due Date:</label>
                <input type="date" id="qaDueDate" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;"
                       value="${new Date(Date.now() + 7 * 24 * 60 * 60 * 1000).toISOString().split('T')[0]}">
            </div>
        </div>
        
        <!-- PROXY MODE INDICATOR -->
			<div id="qaProxyIndicator" style="display: none; margin: 15px 0; padding: 12px; background: #fff3cd; border-left: 4px solid #ffc107; border-radius: 4px;">
				<div style="color: #856404; font-weight: 600; margin-bottom: 8px;">
					⚠️ Proxy Mode Enabled - You can enter response on behalf of this employee
				</div>
				<div style="font-size: 12px; color: #856404;">
					Employee cannot log in. You will enter their response after receiving it externally.
				</div>
			</div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; margin: 15px 0;">
            <div>
                <label>Hospital Name:</label>
                <input type="text" id="qaHospitalName" placeholder="Hospital name" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
            <div>
                <label>Accession No:</label>
                <input type="text" id="qaAccessionNo" placeholder="Accession number" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
            <div>
                <label>Modality:</label>
                <select id="qaModality" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
                    <option value="">Select Modality...</option>
                    <option value="US">Ultrasound</option>
                    <option value="CT">CT Scan</option>
                    <option value="MRI">MRI</option>
                    <option value="XR">X-Ray</option>
                    <option value="Biotronics">Biotronics</option>
                </select>
            </div>
        </div>
        
        <div style="margin: 15px 0;">
            <label>Case Details:</label>
            <input type="text" id="qaCaseDetails" placeholder="e.g., CT Chest - Patient complaint" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
        </div>
        
        <div style="margin: 15px 0;">
            <label>Instructions:</label>
            <textarea id="qaInstructions" rows="3" placeholder="QA review instructions..." style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;"></textarea>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="saveNewQA()" class="btn" style="background: #28a745; margin-right: 10px;">Save QA Assignment</button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Cancel</button>
        </div>
    `);
}

function checkQAProxyStatus() {
    const empSelect = document.getElementById('qaAssignEmployee');
    const selectedOption = empSelect.options[empSelect.selectedIndex];
    const isProxy = selectedOption.getAttribute('data-proxy') === 'true';
    
    const proxyIndicator = document.getElementById('qaProxyIndicator');
    if (proxyIndicator) {
        proxyIndicator.style.display = isProxy ? 'block' : 'none';
    }
}

async function saveNewQA() {
    const assignedTo = document.getElementById('qaAssignEmployee').value;
    const dueDate = document.getElementById('qaDueDate').value;
    const caseDetails = document.getElementById('qaCaseDetails').value.trim();
    const instructions = document.getElementById('qaInstructions').value.trim();
    const hospitalName = document.getElementById('qaHospitalName').value.trim();
    const accessionNo = document.getElementById('qaAccessionNo').value.trim();
    const modality = document.getElementById('qaModality').value;
    
    if (!assignedTo || !dueDate || !caseDetails) {
        alert('Please fill in all required fields (Employee, Due Date, Case Details).');
        return;
    }
    
    try {
        const isProxyEmployee = authorizedEmployees[assignedTo]?.proxyEnabled || false;

		const responseSourceEl = document.getElementById('qaResponseSource');
        const responseSource = isProxyEmployee && responseSourceEl ? responseSourceEl.value : null;
		
		const newQA = {
			id: 'QA_' + Date.now(),
			assignedTo: assignedTo,
			caseDetails: caseDetails,
			instructions: instructions,
			hospitalName: hospitalName,
			accessionNo: accessionNo,
			modality: modality,
			dueDate: dueDate,
			status: 'Pending',
			createdBy: currentUser.code || currentUser.username,
			createdDate: new Date().toISOString(),
			qaReceivedDate: new Date().toISOString().split('T')[0],
			report: '',
			qaGrade: '',
			qaRespondedDate: '',
			isProxy: isProxyEmployee,
			entryType: isProxyEmployee ? 'PROXY_PENDING' : 'SELF'
		};
        
        await saveToFirestore('qa_assignments', newQA);
        
        showNotification('QA Assignment created successfully!');
        closeModal();
        loadHRQAData();
        
    } catch (error) {
        console.error('Error creating QA assignment:', error);
        alert('Error creating QA assignment. Please try again.');
    }
}

async function editQAAssignment(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) {
        alert('QA assignment not found.');
        return;
    }
    
    if (qa.status !== 'Pending' && qa.status !== 'In Progress') {
    alert('Can only edit pending or in-progress QA assignments.');
    return;
}
    
    const modal = createModal(`
        <h3>✏️ Edit QA Assignment</h3>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin: 20px 0;">
            <div>
                <label>Assign to Employee:</label>
                <select id="editQAAssignEmployee" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
                    ${Object.entries(authorizedEmployees)
                        .filter(([code, emp]) => emp.role === 'employee')
                        .map(([code, emp]) => {
                            const selected = code === qa.assignedTo ? 'selected' : '';
                            const proxyLabel = emp.proxyEnabled ? ' [PROXY]' : '';
                            return `<option value="${code}" ${selected}>${emp.name} (${code})${proxyLabel}</option>`;
                        })
                        .join('')}
                </select>
            </div>
            <div>
                <label>Due Date:</label>
                <input type="date" id="editQADueDate" value="${qa.dueDate}" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
        </div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; margin: 15px 0;">
            <div>
                <label>Hospital Name:</label>
                <input type="text" id="editQAHospitalName" value="${qa.hospitalName || ''}" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
            <div>
                <label>Accession No:</label>
                <input type="text" id="editQAAccessionNo" value="${qa.accessionNo || ''}" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
            <div>
                <label>Modality:</label>
                <select id="editQAModality" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
                    <option value="">Select Modality...</option>
                    <option value="US" ${qa.modality === 'US' ? 'selected' : ''}>Ultrasound</option>
                    <option value="CT" ${qa.modality === 'CT' ? 'selected' : ''}>CT Scan</option>
                    <option value="MRI" ${qa.modality === 'MRI' ? 'selected' : ''}>MRI</option>
                    <option value="XR" ${qa.modality === 'XR' ? 'selected' : ''}>X-Ray</option>
                    <option value="Biotronics" ${qa.modality === 'Biotronics' ? 'selected' : ''}>Biotronics</option>
                </select>
            </div>
        </div>
        
        <div style="margin: 15px 0;">
            <label>Case Details:</label>
            <input type="text" id="editQACaseDetails" value="${qa.caseDetails}" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
        </div>
        
        <div style="margin: 15px 0;">
            <label>Instructions:</label>
            <textarea id="editQAInstructions" rows="3" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">${qa.instructions || ''}</textarea>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="saveEditedQA('${qa.id}')" class="btn" style="background: #28a745; margin-right: 10px;">💾 Save Changes</button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Cancel</button>
        </div>
    `);
}

async function saveEditedQA(qaId) {
    const assignedTo = document.getElementById('editQAAssignEmployee').value;
    const dueDate = document.getElementById('editQADueDate').value;
    const caseDetails = document.getElementById('editQACaseDetails').value.trim();
    const instructions = document.getElementById('editQAInstructions').value.trim();
    const hospitalName = document.getElementById('editQAHospitalName').value.trim();
    const accessionNo = document.getElementById('editQAAccessionNo').value.trim();
    const modality = document.getElementById('editQAModality').value;
    
    if (!assignedTo || !dueDate || !caseDetails) {
        alert('Please fill in all required fields (Employee, Due Date, Case Details).');
        return;
    }
    
    try {
        await updateFirestoreDoc('qa_assignments', qaId, {
            assignedTo: assignedTo,
            caseDetails: caseDetails,
            instructions: instructions,
            hospitalName: hospitalName,
            accessionNo: accessionNo,
            modality: modality,
            dueDate: dueDate,
            lastEditedBy: currentUser.code || currentUser.username,
            lastEditedDate: new Date().toISOString()
        });
        
        showNotification('✅ QA assignment updated successfully!');
        closeModal();
        loadHRQAData();
        
    } catch (error) {
        console.error('Error updating QA assignment:', error);
        alert('Error updating QA assignment. Please try again.');
    }
}

async function deleteQAAssignment(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) {
        alert('QA assignment not found.');
        return;
    }
    
    if (qa.status !== 'Pending') {
        alert('Can only delete pending QA assignments.');
        return;
    }
    
    const employee = authorizedEmployees[qa.assignedTo];
    const employeeName = employee ? employee.name : qa.assignedTo;
    
    if (!confirm(`Delete this QA assignment?\n\nEmployee: ${employeeName}\nCase: ${qa.caseDetails}\n\nThis cannot be undone.`)) {
        return;
    }
    
    try {
        const snapshot = await db.collection('qa_assignments').get();
        snapshot.forEach(async (doc) => {
            if (doc.data().id === qaId) {
                await doc.ref.delete();
            }
        });
        
        showNotification('✅ QA assignment deleted successfully!');
        loadHRQAData();
        
    } catch (error) {
        console.error('Error deleting QA assignment:', error);
        alert('Error deleting QA assignment. Please try again.');
    }
}

async function revertQAToEmployee(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) {
        alert('QA assignment not found.');
        return;
    }
    
    if (qa.status !== 'Completed') {
        alert('Can only revert completed QA submissions.');
        return;
    }
    
    const employee = authorizedEmployees[qa.assignedTo];
    const employeeName = employee ? employee.name : qa.assignedTo;
    
    const feedback = prompt(`Revert QA back to ${employeeName}\n\nEnter feedback for the employee (why you're reverting):`);
    
    if (!feedback || feedback.trim().length < 10) {
        alert('Please provide detailed feedback (minimum 10 characters).');
        return;
    }
    
    try {
        const revertCount = (qa.revertCount || 0) + 1;
        
        await updateFirestoreDoc('qa_assignments', qaId, {
            status: 'Reverted',
            revertedBy: currentUser.code || currentUser.username,
            revertedDate: new Date().toISOString(),
            hrFeedback: feedback.trim(),
            revertCount: revertCount,
            qaGrade: '',
            submittedDate: ''
        });
        
        showNotification(`✅ QA reverted back to ${employeeName}`);
        loadHRQAData();
        
    } catch (error) {
        console.error('Error reverting QA:', error);
        alert('Error reverting QA. Please try again.');
    }
}

async function gradeQA(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) return;
    
    const employee = authorizedEmployees[qa.assignedTo];
    const employeeName = employee ? employee.name : qa.assignedTo;
    
    const modal = createModal(`
        <h3>Grade QA Report</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <p><strong>Employee:</strong> ${employeeName} (${qa.assignedTo})</p>
            <p><strong>Case:</strong> ${qa.caseDetails}</p>
            <p><strong>Hospital:</strong> ${qa.hospitalName || 'N/A'}</p>
            <p><strong>Accession:</strong> ${qa.accessionNo || 'N/A'}</p>
        </div>
        
        <div style="margin-bottom: 20px;">
            <h4>QA Report:</h4>
            <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; max-height: 200px; overflow-y: auto; 
                font-family: monospace; font-size: 12px; white-space: pre-wrap;">
${qa.report}</div>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label><strong>QA Grade:</strong></label>
            <select id="qaGradeSelect" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; margin-top: 5px;">
                <option value="">Select Grade</option>
                <option value="1" ${qa.qaGrade === '1' ? 'selected' : ''}>1 - Moderate Clinical Miss</option>
                <option value="2" ${qa.qaGrade === '2' ? 'selected' : ''}>2 - Clinically Significant Omission</option>
                <option value="3" ${qa.qaGrade === '3' ? 'selected' : ''}>3 - Major Diagnostic Gap</option>
                <option value="4" ${qa.qaGrade === '4' ? 'selected' : ''}>4 - Severe Clinical discrepancy</option>
                <option value="5" ${qa.qaGrade === '5' ? 'selected' : ''}>5 - Catastrophic Clinical Event</option>
            </select>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label><strong>HR Feedback:</strong></label>
            <textarea id="hrFeedbackText" rows="4" placeholder="Optional feedback for the employee..." 
                style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; margin-top: 5px;">${qa.hrFeedback || ''}</textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="saveQAGrade('${qaId}')" class="btn" style="background: #28a745; margin-right: 10px;">
                Save Grade
            </button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Cancel</button>
        </div>
    `);
}

async function viewQADetails(qaId) {
    const qaData = await getFromFirestore('qa_assignments');
    const qa = qaData.find(q => q.id === qaId);
    
    if (!qa) return;
    
    const employee = authorizedEmployees[qa.assignedTo];
    const employeeName = employee ? employee.name : qa.assignedTo;
    
    const modal = createModal(`
        <h3>QA Details</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                <div>
                    <strong>Employee:</strong> ${employeeName} (${qa.assignedTo})<br>
                    <strong>Case:</strong> ${qa.caseDetails}<br>
                    <strong>Status:</strong> ${qa.status}<br>
                    <strong>Due Date:</strong> ${qa.dueDate}
                </div>
                <div>
                    <strong>Hospital:</strong> ${qa.hospitalName || 'N/A'}<br>
                    <strong>Accession:</strong> ${qa.accessionNo || 'N/A'}<br>
                    <strong>Modality:</strong> ${qa.modality || 'N/A'}<br>
                    ${qa.qaGrade ? `<strong>Grade:</strong> ${qa.qaGrade}` : ''}
                </div>
            </div>
        </div>
        
        ${qa.instructions ? `
        <div style="margin-bottom: 20px;">
            <h4>Instructions:</h4>
            <div style="background: #fff3cd; padding: 10px; border-radius: 5px;">
                ${qa.instructions}
            </div>
        </div>` : ''}
        
        <div style="margin-bottom: 20px;">
            <h4>QA Report:</h4>
            <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; max-height: 300px; overflow-y: auto; 
                font-family: monospace; font-size: 12px; white-space: pre-wrap;">
${qa.report || 'No report submitted yet.'}</div>
        </div>
        
        ${qa.hrFeedback ? `
        <div style="margin-bottom: 20px;">
            <h4>HR Feedback:</h4>
            <div style="background: #e3f2fd; padding: 10px; border-radius: 5px;">
                ${qa.hrFeedback}
            </div>
        </div>` : ''}
        
        <div style="text-align: right;">
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">Close</button>
        </div>
    `);
}

// ==============================================
// SUBMISSION SYSTEM FOR EMPLOYEES
// ==============================================

function initializeCheckboxListeners() {
    setTimeout(() => {
        const peerCheckbox = document.getElementById('peerReviewCheck');
        
        if (peerCheckbox) {
            peerCheckbox.addEventListener('change', function() {
                const input = document.getElementById('peerReviewAccession');
                if (input) {
                    input.disabled = !this.checked;
                    if (this.checked) input.focus();
                    else input.value = '';
                }
            });
        }
    }, 100);
}

async function submitForReview() {
    const peerReviewChecked = document.getElementById('peerReviewCheck').checked;
    const peerAccession = document.getElementById('peerReviewAccession').value.trim();
    
    if (!peerReviewChecked) {
        alert('Please check the peer review checkbox.');
        return;
    }
    
    if (!peerAccession) {
        alert('Please enter an accession number.');
        return;
    }
    
    const editor = document.getElementById('textEditor');
		const reportText = (editor.innerText || editor.textContent || '').trim();

		if (!reportText || reportText.length < 10) {
			alert('Please enter a report before submitting (minimum 10 characters).');
			return;
		}
    
    try {
        const peerReviewData = {
            id: 'PEER_SUB_' + Date.now(),
            type: 'Peer Review',
            accession: peerAccession,
            report: reportText,
            submitter: currentUser.name,
            submitterCode: currentUser.code,
            timestamp: new Date().toISOString(),
            assignmentStatus: 'unassigned'
        };
        
        await saveToFirestore('peer_review_submissions', peerReviewData);
        showNotification('Peer review submitted! HR will assign it for review.');
        
        // Reset form
        document.getElementById('peerReviewCheck').checked = false;
        document.getElementById('peerReviewAccession').value = '';
        document.getElementById('peerReviewAccession').disabled = true;
        
    } catch (error) {
        console.error('Error submitting review:', error);
        alert('Error submitting review. Please try again.');
    }
}

// ==============================================
// TEMPLATE SEARCH SYSTEM
// ==============================================
const textEditor = document.getElementById('textEditor');

// ===== SMART TEMPLATE SEARCH WITH // TRIGGER IN EDITOR =====
let templateDropdown = null;
let dropdownTimeout = null;

// Event listener for text editor input with // trigger
textEditor.addEventListener('input', function(e) {
    if (dropdownTimeout) {
        clearTimeout(dropdownTimeout);
    }
    
    dropdownTimeout = setTimeout(() => {
        const text = this.innerText || this.textContent || '';
        
        if (!text) {
            hideTemplateDropdown();
            return;
        }
        
        const selection = window.getSelection();
        if (!selection || !selection.focusNode) {
            hideTemplateDropdown();
            return;
        }
        
        const cursorPosition = selection.focusOffset;
        const currentNode = selection.focusNode;
        const textBeforeCursor = currentNode.textContent?.substring(0, cursorPosition) || '';
        
        // Check for // trigger
        const lastChars = textBeforeCursor.slice(-30);
        const triggerMatch = lastChars.match(/\/\/([a-zA-Z\s]+)$/);
        
        if (triggerMatch) {
            const query = triggerMatch[1].trim().toLowerCase();
            console.log('Template search triggered with query:', query);
            
            if (query.length >= 2) {
                const matches = findMatchingTemplatesSmart(query);
                console.log('Found matches:', matches.length);
                
                if (matches.length > 0) {
                    showTemplateDropdownInEditor(matches);
                } else {
                    showNoTemplatesMessage();
                }
            } else {
                hideTemplateDropdown();
            }
        } else {
            hideTemplateDropdown();
        }
    }, 200);
});

// ===== SMART SEARCH FUNCTION (WORKS FOR BOTH EDITOR AND SIDEBAR) =====
function findMatchingTemplatesSmart(query) {
    if (!query || query.length < 2) return [];
    
    const matches = [];
    const searchQuery = query.toLowerCase().trim();
    const words = searchQuery.split(/\s+/);
    
    // Detect if first word is a modality
    const modalities = ['us', 'ct', 'mri', 'xr', 'biotronics'];
    let modalityFilter = null;
    let bodyPartQuery = searchQuery;
    
    if (words.length > 0 && modalities.includes(words[0])) {
        modalityFilter = words[0];
        bodyPartQuery = words.slice(1).join(' ');
        console.log('Modality detected:', modalityFilter, '| Body part:', bodyPartQuery);
    }
    
    // Search through templates
    if (typeof templates !== 'undefined' && templates) {
        try {
            Object.keys(templates).forEach(templateKey => {
                const templateLower = templateKey.toLowerCase();
                const parts = templateKey.split('_');
                const templateModality = parts[0].toLowerCase();
                
                // If modality filter exists, only search that modality
                if (modalityFilter && templateModality !== modalityFilter) {
                    return; // Skip this template
                }
                
                // Search logic
                let isMatch = false;
                
                if (bodyPartQuery.length === 0 && modalityFilter) {
                    // User typed only modality (e.g., "//CT")
                    isMatch = true;
                } else if (bodyPartQuery.length > 0) {
                    // Search in template name (after modality)
                    const templateBodyPart = parts.slice(1).join('_').toLowerCase();
                    const displayName = templateKey.replace(/_/g, ' ').toLowerCase();
                    
                    // Match if body part query is found anywhere in template
                    if (templateBodyPart.includes(bodyPartQuery) || 
                        displayName.includes(bodyPartQuery) ||
                        templateLower.includes(bodyPartQuery)) {
                        isMatch = true;
                    }
                    
                    // Fuzzy match: if individual words match
                    const bodyPartWords = bodyPartQuery.split(/\s+/);
                    const allWordsMatch = bodyPartWords.every(word => 
                        templateLower.includes(word)
                    );
                    if (allWordsMatch) {
                        isMatch = true;
                    }
                }
                
                if (isMatch) {
                    const displayName = templateKey.replace(/_/g, ' ');
                    const category = parts.slice(1, -1).join(' ') || parts.slice(1).join(' ');
                    
                    matches.push({
                        key: templateKey,
                        name: displayName.toUpperCase(),
                        modality: templateModality.toUpperCase(),
                        category: category
                    });
                }
            });
        } catch (error) {
            console.error('Error searching templates:', error);
        }
    } else {
        console.error('templates object is undefined');
    }
    
    // Remove duplicates and limit to top 8
    const uniqueMatches = matches.filter((match, index, self) =>
        index === self.findIndex((m) => m.key === match.key)
    );
    
    return uniqueMatches.slice(0, 8);
}

// Show dropdown in editor
function showTemplateDropdownInEditor(matches) {
    hideTemplateDropdown();
    
    templateDropdown = document.createElement('div');
    templateDropdown.id = 'editorTemplateDropdown';
    templateDropdown.style.cssText = `
        position: fixed;
        background: white;
        border: 3px solid #0066cc;
        border-radius: 12px;
        box-shadow: 0 8px 24px rgba(0,0,0,0.3);
        z-index: 99999;
        max-height: 400px;
        overflow-y: auto;
        min-width: 320px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    `;
    
    const editorRect = textEditor.getBoundingClientRect();
    templateDropdown.style.left = (editorRect.left + 50) + 'px';
    templateDropdown.style.top = (editorRect.top + 100) + 'px';
    
    // Header
    const header = document.createElement('div');
    header.style.cssText = `
        background: linear-gradient(135deg, #0066cc, #004d99);
        color: white;
        padding: 12px 15px;
        font-weight: bold;
        font-size: 13px;
        border-radius: 9px 9px 0 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
    `;
    header.innerHTML = `
        <span>💡 Suggested Templates</span>
        <span style="font-size: 11px; opacity: 0.8;">${matches.length} found</span>
    `;
    templateDropdown.appendChild(header);
    
    // Template items
    matches.forEach((match, index) => {
        const item = document.createElement('div');
        item.style.cssText = `
            padding: 12px 15px;
            cursor: pointer;
            border-bottom: 1px solid #f0f0f0;
            transition: all 0.2s;
            font-size: 13px;
        `;
        
        if (index === matches.length - 1) {
            item.style.borderBottom = 'none';
        }
        
        item.innerHTML = `
            <div style="font-weight: bold; color: #1a1a1a; margin-bottom: 3px;">${match.name}</div>
            <div style="font-size: 11px; color: #666;">${match.modality} › ${match.category}</div>
        `;
        
        item.addEventListener('mouseenter', function() {
            this.style.background = '#0066cc';
            const titleDiv = this.querySelector('div:first-child');
            const subtitleDiv = this.querySelector('div:last-child');
            if (titleDiv) titleDiv.style.color = 'white';
            if (subtitleDiv) subtitleDiv.style.color = 'rgba(255,255,255,0.8)';
        });
        
        item.addEventListener('mouseleave', function() {
            this.style.background = 'white';
            const titleDiv = this.querySelector('div:first-child');
            const subtitleDiv = this.querySelector('div:last-child');
            if (titleDiv) titleDiv.style.color = '#1a1a1a';
            if (subtitleDiv) subtitleDiv.style.color = '#666';
        });
        
        item.addEventListener('click', function(e) {
            e.stopPropagation();
            console.log('Loading template:', match.key);
            
            removeDoubleslashFromEditor();
            
            if (typeof loadTemplate === 'function') {
                loadTemplate(match.key);
            } else {
                console.error('loadTemplate function not found');
            }
            
            hideTemplateDropdown();
        });
        
        templateDropdown.appendChild(item);
    });
    
    // Footer
    const footer = document.createElement('div');
    footer.style.cssText = `
        background: #f5f5f5;
        padding: 8px 15px;
        font-size: 11px;
        color: #666;
        text-align: center;
        border-radius: 0 0 9px 9px;
        border-top: 1px solid #e0e0e0;
    `;
    footer.textContent = 'Click to insert template • ESC to close';
    templateDropdown.appendChild(footer);
    
    document.body.appendChild(templateDropdown);
}

// Show "no templates found" message
function showNoTemplatesMessage() {
    hideTemplateDropdown();
    
    templateDropdown = document.createElement('div');
    templateDropdown.id = 'editorTemplateDropdown';
    templateDropdown.style.cssText = `
        position: fixed;
        background: white;
        border: 3px solid #e74c3c;
        border-radius: 12px;
        box-shadow: 0 8px 24px rgba(0,0,0,0.3);
        z-index: 99999;
        min-width: 280px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    `;
    
    const editorRect = textEditor.getBoundingClientRect();
    templateDropdown.style.left = (editorRect.left + 50) + 'px';
    templateDropdown.style.top = (editorRect.top + 100) + 'px';
    
    templateDropdown.innerHTML = `
        <div style="padding: 20px; text-align: center;">
            <div style="font-size: 32px; margin-bottom: 10px;">🔍</div>
            <div style="color: #e74c3c; font-weight: bold; margin-bottom: 5px;">No Templates Found</div>
            <div style="color: #666; font-size: 12px;">Try different keywords</div>
        </div>
    `;
    
    document.body.appendChild(templateDropdown);
    
    setTimeout(() => {
        hideTemplateDropdown();
    }, 2000);
}

// Remove // from editor
function removeDoubleslashFromEditor() {
    try {
        const selection = window.getSelection();
        if (!selection || !selection.focusNode) return;
        
        const currentNode = selection.focusNode;
        const cursorPosition = selection.focusOffset;
        const textBeforeCursor = currentNode.textContent?.substring(0, cursorPosition) || '';
        
        const doubleslashIndex = textBeforeCursor.lastIndexOf('//');
        
        if (doubleslashIndex !== -1 && currentNode.nodeType === Node.TEXT_NODE) {
            const textAfterCursor = currentNode.textContent.substring(cursorPosition);
            const newText = currentNode.textContent.substring(0, doubleslashIndex) + textAfterCursor;
            currentNode.textContent = newText;
            
            const range = document.createRange();
            range.setStart(currentNode, doubleslashIndex);
            range.collapse(true);
            selection.removeAllRanges();
            selection.addRange(range);
        }
    } catch (error) {
        console.error('Error removing // from editor:', error);
    }
}

// Hide dropdown
function hideTemplateDropdown() {
    if (templateDropdown) {
        try {
            if (templateDropdown.parentNode) {
                templateDropdown.parentNode.removeChild(templateDropdown);
            }
        } catch (error) {
            console.error('Error hiding dropdown:', error);
        }
        templateDropdown = null;
    }
}

// Close dropdown when clicking outside
document.addEventListener('click', function(e) {
    if (templateDropdown && 
        !templateDropdown.contains(e.target) && 
        e.target.id !== 'textEditor' &&
        !textEditor.contains(e.target)) {
        hideTemplateDropdown();
    }
});

// Close dropdown on Escape key
document.addEventListener('keydown', function(e) {
    if (e.key === 'Escape' && templateDropdown) {
        hideTemplateDropdown();
    }
});

// Close dropdown when editor loses focus
textEditor.addEventListener('blur', function() {
    setTimeout(() => {
        if (templateDropdown && !templateDropdown.matches(':hover')) {
            hideTemplateDropdown();
        }
    }, 150);
});

// Add Ctrl+K keyboard shortcut
document.addEventListener('keydown', function(e) {
    if (e.ctrlKey && e.key === 'k') {
        e.preventDefault();
        const searchBox = document.getElementById('templateSearch');
        if (searchBox) {
            searchBox.focus();
            searchBox.select();
        }
    }
});

console.log('✅ Smart template search initialized for both editor and sidebar');

function searchTemplates(event) {
    const searchInput = document.getElementById('templateSearch');
    const searchResults = document.getElementById('searchResults');
    const query = searchInput.value.toLowerCase().trim();
    
    // Handle Ctrl+K shortcut
    if (event && event.ctrlKey && event.key === 'k') {
        event.preventDefault();
        searchInput.focus();
        return;
    }
    
    // Clear results if query is empty
    if (query.length === 0) {
        searchResults.style.display = 'none';
        searchResults.innerHTML = '';
        return;
    }
    
    // Use the existing pagination function with smart search
    searchTemplatesWithPagination(query, 1);
    
    // Handle Enter key to load first result
    if (event && event.key === 'Enter') {
        const matches = findMatchingTemplatesSmart(query);
        if (matches.length > 0 && templates.hasOwnProperty(matches[0].key)) {
            loadTemplateFromSearch(matches[0].key, matches[0].modality);
        }
    }
}

function loadSearchPage(pageNum, query) {
    const searchInput = document.getElementById('templateSearch');
    if (searchInput) {
        searchInput.value = query;
        searchInput.setAttribute('data-page', pageNum);
    }
    
    // Re-trigger search with page number
    searchTemplatesWithPagination(query, pageNum);
}

function searchTemplatesWithPagination(query, pageNum = 1) {
    const searchResults = document.getElementById('searchResults');
    
    // Use smart search function instead of old search
    const matches = findMatchingTemplatesSmart(query);
    
    if (matches.length === 0) {
        searchResults.innerHTML = '<div style="padding: 20px; text-align: center; color: #666;"><div style="font-size: 24px; margin-bottom: 8px;">🔍</div><div style="font-size: 13px;">No templates found</div></div>';
        searchResults.style.display = 'block';
        return;
    }
    
    // Calculate pagination
    const itemsPerPage = 6;
    const startIndex = (pageNum - 1) * itemsPerPage;
    const endIndex = startIndex + itemsPerPage;
    const pageMatches = matches.slice(startIndex, endIndex);
    const totalPages = Math.ceil(matches.length / itemsPerPage);
    
    const html = pageMatches.map((match) => {
        const templateExists = templates.hasOwnProperty(match.key);
        const statusIcon = templateExists ? '📋' : '⚠️';
        const statusColor = templateExists ? '#1a1a1a' : '#999';
        
        return `
            <div style="padding: 12px 15px; cursor: pointer; border-bottom: 1px solid #f0f0f0; transition: all 0.2s; color: ${statusColor};"
                 onmouseover="this.style.background='#0066cc'; this.querySelector('.template-title').style.color='white'; this.querySelector('.template-subtitle').style.color='rgba(255,255,255,0.8)';" 
                 onmouseout="this.style.background='white'; this.querySelector('.template-title').style.color='${statusColor}'; this.querySelector('.template-subtitle').style.color='#666';"
                 onclick="loadTemplateFromSearch('${match.key}', '${match.modality}')">
                <div class="template-title" style="font-size: 13px; font-weight: 600; margin-bottom: 3px;">
                    ${statusIcon} ${match.name}
                </div>
                <div class="template-subtitle" style="font-size: 11px; color: #666;">
                    ${match.modality} › ${match.category}
                </div>
                ${!templateExists ? '<div style="font-size: 11px; color: #e74c3c; margin-top: 3px;">⚠️ Template not configured yet</div>' : ''}
            </div>
        `;
    }).join('');
    
    // Pagination footer
    let paginationHtml = '';
    if (matches.length > 6) {
        paginationHtml = `
            <div style="padding: 10px; text-align: center; background: #f5f5f5; border-top: 1px solid #e0e0e0;">
                <div style="font-size: 11px; color: #666; margin-bottom: 8px;">
                    Showing ${startIndex + 1}-${Math.min(endIndex, matches.length)} of ${matches.length} results
                </div>
                <div style="display: flex; justify-content: center; gap: 5px; flex-wrap: wrap;">
                    ${Array.from({length: Math.min(totalPages, 10)}, (_, i) => {
                        const displayPageNum = i + 1;
                        const isActive = displayPageNum === pageNum;
                        return `<button onclick="searchTemplatesWithPagination('${query.replace(/'/g, "\\'")}', ${displayPageNum})" 
                                style="padding: 5px 10px; background: ${isActive ? '#0066cc' : 'white'}; 
                                color: ${isActive ? 'white' : '#333'}; border: 1px solid #e0e0e0; 
                                border-radius: 6px; cursor: pointer; font-size: 11px; font-weight: 600; transition: all 0.2s;"
                                onmouseover="if(!${isActive}) { this.style.background='#e3f2fd'; this.style.borderColor='#0066cc'; }"
                                onmouseout="if(!${isActive}) { this.style.background='white'; this.style.borderColor='#e0e0e0'; }">${displayPageNum}</button>`;
                    }).join('')}
                    ${totalPages > 6 ? '<span style="padding: 5px; color: #666;">...</span>' : ''}
                </div>
            </div>
        `;
    }
    
    searchResults.innerHTML = html + paginationHtml;
    searchResults.style.display = 'block';
}

function loadTemplateFromSearch(templateKey, modality) {
    // Check if template exists
    if (!templates[templateKey]) {
        showNotification(`Template "${templateKey}" not found. Please configure it in Admin Panel.`);
        return;
    }
    
    // Switch to the correct modality tab
    selectTab(modality);
    
    // Load the template
    loadTemplate(templateKey);
    
    // Clear search
    document.getElementById('templateSearch').value = '';
    document.getElementById('searchResults').style.display = 'none';
    
    // Focus on editor
    document.getElementById('textEditor').focus();
    
    updateStatus(`Loaded: ${templateKey}`);
}

// Close search results when clicking outside
document.addEventListener('click', function(event) {
    const searchInput = document.getElementById('templateSearch');
    const searchResults = document.getElementById('searchResults');
    
    // Don't close if clicking on pagination buttons or search results
    if (searchInput && searchResults && 
        !searchInput.contains(event.target) && 
        !searchResults.contains(event.target) &&
        event.target.tagName !== 'BUTTON') {
        searchResults.style.display = 'none';
    }
});

// Keyboard shortcut: Ctrl+K to focus search
document.addEventListener('keydown', function(event) {
    if ((event.ctrlKey || event.metaKey) && event.key === 'k') {
        event.preventDefault();
        const searchInput = document.getElementById('templateSearch');
        if (searchInput) {
            searchInput.focus();
            searchInput.select();
        }
    }
});
function selectTab(tab) {
    currentTab = tab;
    if (['US', 'CT', 'MRI', 'XR', 'Biotronics'].includes(tab)) {
    lastSelectedModality = tab;
}

    // Close dropdowns
    closeEmpEventsDropdown();
    closeHREventsDropdown();
    
    // Clear all active tabs
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    
    // Set active tab
    document.querySelectorAll('.tab').forEach(t => {
        if (t.getAttribute('data-tab') === tab) {
            t.classList.add('active');
        }
    });
    
    // Hide all panels first
    document.getElementById('mainContainer').style.display = 'none';
    document.getElementById('qaBoard').style.display = 'none';
    document.getElementById('peerBoard').style.display = 'none';
    document.getElementById('empSchedulePanel').style.display = 'none';
    document.getElementById('hrSchedulePanel').style.display = 'none';
    document.getElementById('empMeetingsPanel').style.display = 'none';
    document.getElementById('hrMeetingsPanel').style.display = 'none';
    
    // Handle special tabs
    if (tab === 'QABoard') {
        document.getElementById('qaBoard').style.display = 'block';
        loadQABoard();
        updateStatus('QA Board loaded');
        
        const dropdown = document.getElementById('modalityDropdown');
        if (dropdown) dropdown.value = '';
        return;
    } else if (tab === 'PeerBoard') {
        document.getElementById('peerBoard').style.display = 'block';
        loadPeerBoard();
        updateStatus('Peer Review Board loaded');
        
        const dropdown = document.getElementById('modalityDropdown');
        if (dropdown) dropdown.value = '';
        return;
    } else if (tab === 'Schedule') {
        // Check if user has master schedule view permission
        const hasMasterView = currentUser.permissions && currentUser.permissions.includes('master_schedule_view');
        
        if (hasMasterView) {
            // Show master schedule (all categories) - READ ONLY
            document.getElementById('hrSchedulePanel').style.display = 'block';
            currentScheduleMonth = new Date();
            currentScheduleCategory = 'RAD';
            loadMasterScheduleReadOnly();
            updateStatus('Master Schedule loaded (View Only)');
        } else {
            // Show personal schedule only
            document.getElementById('empSchedulePanel').style.display = 'block';
            currentScheduleMonth = new Date();
            loadEmployeeSchedule();
            updateStatus('My Schedule loaded');
        }
        
        const dropdown = document.getElementById('modalityDropdown');
        if (dropdown) dropdown.value = '';
        return;
    } else if (tab === 'Meetings') {
        // Employee or HR meetings view
        if (currentUser.role === 'employee' || currentUser.role === 'admin') {
            document.getElementById('empMeetingsPanel').style.display = 'block';
            loadEmployeeMeetingsPanel();
            updateStatus('My Meetings loaded');
        } else if (currentUser.role === 'hr') {
            document.getElementById('hrMeetingsPanel').style.display = 'block';
            loadHRMeetingsPanel();
            updateStatus('Meeting Management loaded');
        }
        
        const dropdown = document.getElementById('modalityDropdown');
        if (dropdown) dropdown.value = '';
        return;
    } else {
        document.getElementById('mainContainer').style.display = 'grid';
    }
    
    // Update template list for modality tabs
    document.getElementById('categoryTitle').textContent = `${tab} Templates`;
    loadTemplateCategories(tab);
    updateStatus(`Selected ${tab} templates`);
    
    // Sync dropdown with selected modality
    // Sync dropdowns with selected modality
const modalityDropdown = document.getElementById('modalityDropdown');
const modalitySelect = document.getElementById('modalitySelect');

if (['US', 'CT', 'MRI', 'XR', 'Biotronics'].includes(tab)) {
    if (modalityDropdown) modalityDropdown.value = tab;
    if (modalitySelect) modalitySelect.value = tab;
} else {
    if (modalityDropdown) modalityDropdown.value = '';
    if (modalitySelect) modalitySelect.value = '';
}

}

async function loadEmployeeMeetingsPanel() {
    try {
        const allMeetings = await getFromFirestore('meetings');
        
        const now = new Date();
        now.setHours(0, 0, 0, 0);
        
        // Calculate 30 days from now
        const thirtyDaysFromNow = new Date(now);
        thirtyDaysFromNow.setDate(thirtyDaysFromNow.getDate() + 30);
        
        // Filter meetings: next 30 days, not cancelled
        const myMeetings = allMeetings.filter(m => {
            if (!m.participants || !m.participants.includes(currentUser.code)) return false;
                  
            const meetingStart = new Date(m.date + 'T' + m.startTime);
            
            // Check if meeting is cancelled
            if (m.status === 'cancelled') {
                if (!m.cancelledDate) return false; // No cancellation date, hide it
                const cancelledTime = new Date(m.cancelledDate);
                const hoursSinceCancellation = (now - cancelledTime) / (1000 * 60 * 60);
                if (hoursSinceCancellation > 1) return false;
            }
             const cutoff = new Date(meetingStart.getTime() + (30 * 60 * 1000));
    if (cutoff < new Date()) return false;

            return meetingStart >= now && meetingStart <= thirtyDaysFromNow;
        }).sort((a, b) => new Date(a.date + 'T' + a.startTime) - new Date(b.date + 'T' + b.startTime));
        
        // Load upcoming meetings list
        const upcomingList = document.getElementById('empUpcomingMeetingsList');
        if (upcomingList) {
            if (myMeetings.length > 0) {
                const upcomingHtml = myMeetings.map(meeting => {
                    if (meeting.status === 'cancelled') {
                        // Render cancelled meeting card
                        return renderCancelledMeetingCard(meeting);
                    } else {
                        return renderMeetingCard(meeting, false);
                    }
                }).join('');
                
                upcomingList.innerHTML = upcomingHtml;
            } else {
                upcomingList.innerHTML = '<div style="padding: 40px; text-align: center; color: #666;">No upcoming meetings in the next 30 days</div>';
            }
        }
        
    } catch (error) {
        console.error('Error loading employee meetings:', error);
        alert('Error loading meetings: ' + error.message);
    }
}

function selectModalityFromDropdown(modality) {
    if (!modality) return;
    selectTab(modality);
    document.getElementById('modalityDropdown').value = modality;
}

function selectGender(gender) {
    currentGender = gender;
    
    document.querySelectorAll('.gender-btn').forEach(btn => btn.classList.remove('active'));
    document.getElementById(gender === 'male' ? 'maleBtn' : 'femaleBtn').classList.add('active');
    
    updateStatus(`Gender set to ${gender}`);
}

function loadTemplate(templateKey) {
    resetCriticalFindingsTracker();
	currentCaseHash = null;
    lastNormalizedText = '';
    console.log('Template loaded - case tracking reset');
	currentLoadedTemplate = templateKey;
    
    // Try loading gender-specific template first
    let genderTemplateKey = `${templateKey}_${currentGender}`;
    let template = templates[genderTemplateKey];
    
    // If gender-specific doesn't exist, try base template
    if (!template) {
        template = templates[templateKey];
    }
    
    if (!template) {
        updateStatus(`Template '${templateKey}' not found`);
        return;
    }
    
    const editor = document.getElementById('textEditor');
    
    // Apply gender-specific pronoun modifications (for templates without male/female versions)
    let processedTemplate = template;
    if (currentGender === 'female' && !templates[genderTemplateKey]) {
        processedTemplate = processedTemplate.replace(/\bhe\b/g, 'she');
        processedTemplate = processedTemplate.replace(/\bhis\b/g, 'her');
        processedTemplate = processedTemplate.replace(/\bhim\b/g, 'her');
    }
    
    editor.innerHTML = processedTemplate.replace(/\n/g, '<br>');
    
	if (userAutoSavePreference > 0) {
        setTimeout(() => saveDraft(true), 1000);
    }
	
    addToRecentTemplates(templateKey);
    updateWordCount();
    updateStatus(`Loaded template: ${genderTemplateKey || templateKey}`);
}

function loadTemplateCategories(tab) {
    const templateList = document.getElementById('templateList');
    const categories = templateCategories[tab];
    
    if (!categories) {
        templateList.innerHTML = '<li>No templates available</li>';
        return;
    }
    
    let html = '';
    
    Object.entries(categories).forEach(([categoryName, items]) => {
        const categoryId = categoryName.replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
        
        html += `
            <div class="category-header" onclick="toggleCategory('${categoryId}')">
                <span>${categoryName}</span>
                <span class="category-icon">▶</span>
            </div>
            <div class="subcategory-list" id="${categoryId}-list">
                ${items.map(item => {
                    // FIXED: Now includes parent category in the template key
                    const parentCategory = categoryName.toLowerCase().replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
                    const itemName = item.toLowerCase().replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
                    const templateKey = `${tab.toLowerCase()}_${parentCategory}_${itemName}`;
                    
                    return `<div class="subcategory-item" onclick="loadTemplate('${templateKey}')">${item}</div>`;
                }).join('')}
            </div>
        `;
    });
    
    templateList.innerHTML = html;
}

function toggleCategory(categoryId) {
    const categoryList = document.getElementById(`${categoryId}-list`);
    const categoryHeader = event.target.closest('.category-header');
    const icon = categoryHeader.querySelector('.category-icon');
    
    if (!categoryList || !categoryHeader || !icon) return;
    
    if (categoryList.classList.contains('expanded')) {
        categoryList.classList.remove('expanded');
        icon.textContent = '▶';
        categoryHeader.classList.remove('active');
    } else {
        // Close other open categories first
        document.querySelectorAll('.subcategory-list.expanded').forEach(list => {
            list.classList.remove('expanded');
        });
        document.querySelectorAll('.category-header.active').forEach(header => {
            header.classList.remove('active');
            const headerIcon = header.querySelector('.category-icon');
            if (headerIcon) headerIcon.textContent = '▶';
        });
        
        // Open selected category
        categoryList.classList.add('expanded');
        icon.textContent = '▼';
        categoryHeader.classList.add('active');
    }
}

function addToRecentTemplates(templateKey) {
    const recentList = document.getElementById('recentList');
    const templateName = templateKey.replace(/_/g, ' ').replace(/\b\w/g, l => l.toUpperCase());
    
    const existing = recentList.querySelector(`[onclick*="${templateKey}"]`);
    if (existing) existing.remove();
    
    const recentItem = document.createElement('li');
    recentItem.className = 'template-item';
    recentItem.onclick = () => loadTemplate(templateKey);
    recentItem.textContent = templateName;
    
    recentList.insertBefore(recentItem, recentList.firstChild);
    
    while (recentList.children.length > 3) {
        recentList.removeChild(recentList.lastChild);
    }
}

// ==============================================
// CRITICAL FINDINGS DETECTION
// ==============================================
let lastCheckedFindingsText = '';

function detectCriticalFindings() {
    const editor = document.getElementById('textEditor');
    const fullText = editor.textContent || editor.innerText || '';
    
    // Extract only FINDINGS section
    const findingsRegex = /FINDINGS:(.*?)(?=IMPRESSION:|$)/is;
    const match = fullText.match(findingsRegex);
    
    if (!match) return;
    
    const findingsText = match[1].trim();
    
    // Only check if findings text actually changed
    if (findingsText === lastCheckedFindingsText) return;
    
    // Find what was ADDED (new text only)
    const newContent = findingsText.replace(lastCheckedFindingsText, '').trim();
    
    // Update last checked text
    lastCheckedFindingsText = findingsText;
    
    // If nothing new added, skip
    if (!newContent || newContent.length < 3) return;
    
    // Check critical findings ONLY in new content
    criticalFindings.forEach(phrase => {
        const phraseLower = phrase.toLowerCase();
        
        // Skip if already alerted
        if (alertedFindingsInCurrentReport.has(phraseLower)) return;
        
        // Check if phrase exists in NEW content only
        if (!newContent.toLowerCase().includes(phraseLower)) return;
        
        // Context-aware detection: check for negation in the new content
        if (isNegatedFinding(newContent, phrase)) {
            return; // Don't alert on negated findings
        }
        
        // Only alert on positive findings
        showCriticalAlert(phrase);
        alertedFindingsInCurrentReport.add(phraseLower);
    });
}



function isNegatedFinding(text, criticalPhrase) {
    const phraseLower = criticalPhrase.toLowerCase();
    const textLower = text.toLowerCase();
    
    // Find ALL occurrences of the critical phrase
    let index = textLower.indexOf(phraseLower);
    
    while (index !== -1) {
        // Extract sentence containing this occurrence
        // Look backwards for sentence start
        let sentenceStart = 0;
        for (let i = index - 1; i >= 0; i--) {
            if (textLower[i] === '.' || textLower[i] === '!' || textLower[i] === '?') {
                sentenceStart = i + 1;
                break;
            }
        }
        
        // Look forwards for sentence end
        let sentenceEnd = textLower.length;
        for (let i = index; i < textLower.length; i++) {
            if (textLower[i] === '.' || textLower[i] === '!' || textLower[i] === '?') {
                sentenceEnd = i;
                break;
            }
        }
        
        // Extract the full sentence
        const sentence = textLower.substring(sentenceStart, sentenceEnd).trim();
        
        // Negation patterns - check if they appear BEFORE the critical phrase in this sentence
        const negationPatterns = [
            /\b(no|without|absence of|ruled out|negative for|excluding)\b/i,
            /\b(not seen|not identified|not evident|not present|not demonstrated)\b/i,
            /\b(free of|clear of|unremarkable for)\b/i
        ];
        
        // Get the part of sentence BEFORE the critical phrase
        const phrasePositionInSentence = sentence.indexOf(phraseLower);
        const textBeforePhrase = sentence.substring(0, phrasePositionInSentence);
        
        // Check if negation exists before the phrase
        const hasNegation = negationPatterns.some(pattern => pattern.test(textBeforePhrase));
        
        if (!hasNegation) {
            // Found at least one occurrence that is NOT negated
            return false;
        }
        
        // Check for next occurrence
        index = textLower.indexOf(phraseLower, index + 1);
    }
    
    // All occurrences were negated
    return true;
}

function showCriticalAlert(finding) {
    // Create alert element
    const alert = document.createElement('div');
    alert.className = 'critical-alert';
    alert.innerHTML = `
        <div class="critical-alert-icon">⚠️</div>
        <div>CRITICAL FINDING DETECTED</div>
        <div style="font-size: 16px; margin-top: 10px; font-weight: normal;">${finding.toUpperCase()}</div>
    `;
    
    document.body.appendChild(alert);
    
    // Play alert sound (optional - browser beep)
    try {
        const audio = new Audio('data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAoUXrTp6qFTE');
        audio.play().catch(() => {}); // Ignore if audio fails
    } catch (e) {}
    
    // Auto-dismiss after 3 seconds
    setTimeout(() => {
        alert.style.opacity = '0';
        alert.style.transition = 'opacity 0.3s ease';
        setTimeout(() => {
            if (alert.parentNode) {
                document.body.removeChild(alert);
            }
        }, 300);
    }, 3000);
}

// Reset alerts when editor is cleared or new report starts
function resetCriticalFindingsTracker() {
    alertedFindingsInCurrentReport.clear();
	lastCheckedFindingsText = ''; 
	
}

// ==============================================
// EDITOR FUNCTIONS
// ==============================================

function formatReport() {
    const editor = document.getElementById('textEditor');
    let text = editor.textContent || editor.innerText || '';
    
    // Step 1: Normalize line breaks (keep single and double line breaks)
    text = text.replace(/\r\n/g, '\n'); // Windows line breaks
    text = text.replace(/\r/g, '\n');   // Old Mac line breaks
    
    // Step 2: Remove excessive blank lines (3+ → 2 max)
    text = text.replace(/\n{3,}/g, '\n\n');
    
    // Step 3: Remove trailing/leading spaces from each line
    const lines = text.split('\n');
    const cleanedLines = lines.map(line => line.trim());
    text = cleanedLines.join('\n');
    
    // Step 4: Capitalize section headers (ONLY if they start the line)
    text = text.replace(/^(technique|clinical history|comparison|findings|impression|recommendation):/gmi, 
                       match => match.toUpperCase());
    
    // Step 5: Ensure section headers have proper spacing
    text = text.replace(/(TECHNIQUE:|CLINICAL HISTORY:|COMPARISON:|FINDINGS:|IMPRESSION:|RECOMMENDATION:)/g, 
                       '\n\n$1\n');
    
    // Step 6: Clean up multiple line breaks again (after adding section spacing)
    text = text.replace(/\n{3,}/g, '\n\n');
    
    // Step 7: Remove blank line at start
    text = text.replace(/^\n+/, '');
    
    // Step 8: Ensure no trailing blank lines
    text = text.replace(/\n+$/, '');
    
    // Update editor with formatted text
    editor.innerHTML = text.replace(/\n/g, '<br>');
    
    updateStatus('Report formatted (spacing cleaned)');
    updateWordCount();
    
    // Show brief feedback
    showNotification('✓ Report formatted: excess spaces removed, structure preserved');
}

function copyToClipboard() {
    const editor = document.getElementById('textEditor');
    
    // Get the exact HTML content as displayed
    const htmlContent = editor.innerHTML;
    
    // Convert HTML to plain text preserving ALL line breaks and spacing
    const plainText = convertHtmlToPlainText(htmlContent);
    
    try {
        // Modern clipboard API - copy both HTML and plain text
        const clipboardItem = new ClipboardItem({
            'text/html': new Blob([htmlContent], { type: 'text/html' }),
            'text/plain': new Blob([plainText], { type: 'text/plain' })
        });
        
        navigator.clipboard.write([clipboardItem]).then(() => {
            updateStatus('Report copied (formatting preserved)');
            showNotification('✓ Report copied with exact formatting');
        }).catch(() => {
            // Fallback: copy as plain text with preserved formatting
            fallbackCopyPreserveFormat();
        });
    } catch (err) {
        // Browser doesn't support ClipboardItem
        fallbackCopyPreserveFormat();
    }
    
function fallbackCopyPreserveFormat(text) {
        const tempTextarea = document.createElement('textarea');
        tempTextarea.value = text;
        tempTextarea.style.position = 'fixed';
        tempTextarea.style.left = '-9999px';
        document.body.appendChild(tempTextarea);
        
        tempTextarea.select();
        document.execCommand('copy');
        document.body.removeChild(tempTextarea);
        
        updateStatus('Report copied to clipboard');
    }
}

function convertHtmlToPlainText(html) {
    // Create temporary div to parse HTML
    const temp = document.createElement('div');
    temp.innerHTML = html;
    
    // Process each node to preserve formatting
    let text = '';
    
    function processNode(node) {
        if (node.nodeType === Node.TEXT_NODE) {
            text += node.textContent;
        } else if (node.nodeType === Node.ELEMENT_NODE) {
            const tagName = node.tagName.toLowerCase();
            
            // Handle line breaks
            if (tagName === 'br') {
                text += '\n';
            } else if (tagName === 'div' || tagName === 'p') {
                // Add line break before block elements (except first)
                if (text.length > 0 && !text.endsWith('\n')) {
                    text += '\n';
                }
                
                // Process children
                for (let child of node.childNodes) {
                    processNode(child);
                }
                
                // Add line break after block elements
                if (!text.endsWith('\n')) {
                    text += '\n';
                }
            } else {
                // Process inline elements
                for (let child of node.childNodes) {
                    processNode(child);
                }
            }
        }
    }
    
    processNode(temp);
    
    return text;
}

function clearEditor() {
    if (confirm('Clear the editor?')) {
        const editor = document.getElementById('textEditor');
        editor.innerHTML = '';
        resetCriticalFindingsTracker();
		lastSavedContent = '';
		currentCaseHash = null;
        lastNormalizedText = '';
        console.log('Editor cleared - case tracking reset');
        updateWordCount();
        updateStatus('Editor cleared');
		editor.focus();
        const range = document.createRange();
        const sel = window.getSelection();
        range.setStart(editor, 0);
        range.collapse(true);
        sel.removeAllRanges();
        sel.addRange(range);
    }
}

function updateWordCount() {
    const editor = document.getElementById('textEditor');
    const text = editor.textContent || '';
    const words = text.trim() ? text.trim().split(/\s+/).length : 0;
    const chars = text.length;
    const wordCountEl = document.getElementById('wordCount');
    if (wordCountEl) {
        wordCountEl.textContent = `Words: ${words} | Characters: ${chars}`;
    }
}

// Helper to re-enable the copy button immediately
function enableCopyButton() {
    const btn = document.getElementById('copyAndCountBtn');
    if (btn) {
        btn.disabled = false;
        btn.style.opacity = '1';
        btn.style.cursor = 'pointer';
    }
}

async function copyAndCount() {
    const btn = document.getElementById('copyAndCountBtn');
    if (btn) {
        btn.disabled = true;
        btn.style.opacity = '0.5';
        btn.style.cursor = 'not-allowed';
    }

    try {
        console.log('=== copyAndCount START ===');
        
        const editor = document.getElementById('textEditor');
        const htmlContent = editor.innerHTML;
        const reportText = convertHtmlToPlainText(htmlContent);
        
        console.log('1. Report text length:', reportText.length);
        
        if (!reportText || reportText.trim().length < 50) {
            alert('Report is too short. Please write at least 50 characters.');
			enableCopyButton();
            return;
        }
        
        const countSelector = document.getElementById('reportCountSelector');
        console.log('2. Count selector found:', !!countSelector);
        
        if (!countSelector) {
            alert('Error: Count selector not found. Please refresh the page.');
			enableCopyButton();
            return;
        }
        
        const userSelectedCount = parseInt(countSelector.value);
        countSelector.value = '1'; // Reset to default
        console.log('3. Selected count:', userSelectedCount);
        
        // ✅ DETECT MODALITY from multiple sources
        let detectedModality = null;
        
        // Priority 1: modalitySelect dropdown
        const modalitySelect = document.getElementById('modalitySelect');
        const modalityDropdown = document.getElementById('modalityDropdown');

        // Use modalityDropdown (visible one at top) first
        if (modalityDropdown && modalityDropdown.value) {
            detectedModality = modalityDropdown.value;
            console.log('[Modality] From visible dropdown:', detectedModality);
        } else if (modalitySelect && modalitySelect.value) {
            detectedModality = modalitySelect.value;
            console.log('[Modality] From hidden dropdown:', detectedModality);
        }
        
        // Priority 2: lastSelectedModality variable
        if (!detectedModality && lastSelectedModality) {
            detectedModality = lastSelectedModality;
            console.log('[Modality] From lastSelected:', detectedModality);
        }
        
        // Priority 3: Detect from template name
        if (!detectedModality && currentLoadedTemplate) {
            const templateName = currentLoadedTemplate.toLowerCase();
            if (templateName.startsWith('us_')) detectedModality = 'US';
            else if (templateName.startsWith('ct_')) detectedModality = 'CT';
            else if (templateName.startsWith('mri_')) detectedModality = 'MRI';
            else if (templateName.startsWith('xr_')) detectedModality = 'XR';
            else if (templateName.startsWith('biotronics_')) detectedModality = 'Biotronics';
            console.log('[Modality] From template name:', detectedModality);
        }
        
        // Priority 4: currentTab
        if (!detectedModality) {
            detectedModality = currentTab;
            console.log('[Modality] From currentTab:', detectedModality);
        }
        
        console.log('✅ INITIAL MODALITY:', detectedModality);

        // ============================================
        // MODALITY DETECTION & WARNING - ALWAYS RUN
        // ============================================
        try {
            const detectedInfo = await detectModalityFromReport(reportText);
            
            // If we detected a modality with high confidence or ambiguous
            if (detectedInfo.confidence === 'high' || detectedInfo.confidence === 'ambiguous') {
                
                // Case 1: No modality selected OR not a valid modality tab
                if (!detectedModality || !['US', 'CT', 'MRI', 'XR', 'Biotronics'].includes(detectedModality)) {
                    console.log('[Modality Warning] No valid modality selected');
                    
                    if (detectedInfo.confidence === 'ambiguous') {
                        // Multiple modalities detected - show warning to choose
                        const userChoice = await showModalityWarning('Templates', detectedInfo);
                        
                        if (userChoice.startsWith('correct_')) {
                            const correctedModality = userChoice.replace('correct_', '');
                            detectedModality = correctedModality;
                            currentTab = correctedModality;
                            
                            if (modalityDropdown) modalityDropdown.value = correctedModality;
                            if (modalitySelect) modalitySelect.value = correctedModality;
                            
                            const correctedName = detectedInfo.allMatches.find(m => m.id === correctedModality)?.name || correctedModality;
                            showNotification(`✅ Modality set to ${correctedName}`);
                        } else if (userChoice === 'cancel') {
                            console.log('[Modality] User cancelled submission');
                            updateStatus('Report submission cancelled');
							enableCopyButton();
                            return;
                        } else if (userChoice === 'keep') {
                            // User chose to keep "Templates" - not allowed
                            alert('⚠️ You must select a specific modality to submit report.');
                            return;
                        }
                    } else {
                        // Single modality detected - show warning to confirm
                        const userChoice = await showModalityWarning('Templates', detectedInfo);
                        
                        if (userChoice === 'correct') {
                            detectedModality = detectedInfo.detected;
                            currentTab = detectedInfo.detected;
                            
                            if (modalityDropdown) modalityDropdown.value = detectedInfo.detected;
                            if (modalitySelect) modalitySelect.value = detectedInfo.detected;
                            
                            showNotification(`✅ Modality set to ${detectedInfo.name}`);
                        } else if (userChoice === 'cancel') {
                            console.log('[Modality] User cancelled submission');
                            updateStatus('Report submission cancelled');
							enableCopyButton();
                            return;
                        } else if (userChoice === 'keep') {
                            alert('⚠️ You must select a specific modality to submit report.');
                            return;
                        }
                    }
                }
                // Case 2: Modality IS selected but doesn't match detected
                else if (detectedInfo.detected && detectedInfo.detected !== detectedModality) {
                    
                    if (detectedInfo.confidence === 'high') {
                        // Single mismatch detected
                        console.log('[Modality Warning] Mismatch:', detectedModality, 'vs', detectedInfo.detected);
                        
                        const userChoice = await showModalityWarning(detectedModality, detectedInfo);
                        
                        if (userChoice === 'correct') {
                            // User wants to correct - update detectedModality AND sync dropdowns
                            detectedModality = detectedInfo.detected;
                            currentTab = detectedInfo.detected;
                            
                            if (modalityDropdown) modalityDropdown.value = detectedInfo.detected;
                            if (modalitySelect) modalitySelect.value = detectedInfo.detected;
                            
                            console.log('[Modality] Corrected to:', detectedModality);
                            showNotification(`✅ Modality corrected to ${detectedInfo.name}`);
                        } else if (userChoice === 'cancel') {
                            console.log('[Modality] User cancelled submission');
                            updateStatus('Report submission cancelled');
                            return;
                        }
                        // If 'keep', continue with current detectedModality
                        
                    } else if (detectedInfo.confidence === 'ambiguous') {
                        // Multiple modalities detected
                        console.log('[Modality Warning] Ambiguous detection:', detectedInfo.allMatches);
                        
                        const userChoice = await showModalityWarning(detectedModality, detectedInfo);
                        
                        if (userChoice.startsWith('correct_')) {
                            // Extract modality ID from choice
                            const correctedModality = userChoice.replace('correct_', '');
                            detectedModality = correctedModality;
                            currentTab = correctedModality;
                            
                            if (modalityDropdown) modalityDropdown.value = correctedModality;
                            if (modalitySelect) modalitySelect.value = correctedModality;
                            
                            const correctedName = detectedInfo.allMatches.find(m => m.id === correctedModality)?.name || correctedModality;
                            console.log('[Modality] User selected:', correctedModality);
                            showNotification(`✅ Modality set to ${correctedName}`);
                        } else if (userChoice === 'cancel') {
                            console.log('[Modality] User cancelled submission');
                            updateStatus('Report submission cancelled');
                            return;
                        }
                        // If 'keep', continue with current detectedModality
                    }
                }
                
            }
        } catch (error) {
            console.error('[Modality Detection] Error:', error);
            // Continue with submission even if detection fails
        }
        // ============================================
        // END MODALITY DETECTION
        // ============================================
		if (!detectedModality || !['US', 'CT', 'MRI', 'XR', 'Biotronics'].includes(detectedModality)) {
			alert('⚠️ Please select a modality (US/CT/MRI/X-Ray/Biotronics) before submitting.');
			return;
		}

		console.log('✅ FINAL MODALITY TO SAVE:', detectedModality);

        console.log('✅ FINAL MODALITY TO SAVE:', detectedModality);

        // Institution validation - MANDATORY
        const institutionDropdown = document.getElementById('institutionDropdown');
        const selectedInstitution = institutionDropdown ? institutionDropdown.value : '';
        const accessionNumber = document.getElementById('accessionNumber')?.value.trim() || '';
        
        if (!selectedInstitution) {
            alert('Please select an institution before submitting.');
			enableCopyButton();
            return;
        }
        if (!accessionNumber) {
            alert('Please enter an accession number before submitting.');
			enableCopyButton();
            return;
        }

        // Check if this is edit of current case or new case
        let reportHash;
        let saveType = 'new';
        
        if (currentCaseHash && lastNormalizedText) {
            const wordDiff = countWordDifference(lastNormalizedText, reportText);
            console.log('4. Word difference from current case:', wordDiff);
            
            if (wordDiff < 5) {
                reportHash = currentCaseHash;
                saveType = 'update';
                console.log('5. Minor edit - will UPDATE');
            } else {
                reportHash = generateReportHash(reportText);
                saveType = 'new';
                console.log('5. Major changes - will save as NEW');
            }
        } else {
            reportHash = generateReportHash(reportText);
            console.log('4. New case - hash:', reportHash);
        }
        
        // Update tracking
        currentCaseHash = reportHash;
        lastNormalizedText = reportText;

        console.log('6. Calling saveReportAndCount with modality:', detectedModality);
        
        // Pass all parameters
        await saveReportAndCount(reportHash, reportText, saveType, userSelectedCount, htmlContent, selectedInstitution, detectedModality, accessionNumber);
 
        // Clear institution after save
        if (institutionDropdown) {
            institutionDropdown.value = '';
        }
        
        const accessionInput = document.getElementById('accessionNumber');
        if (accessionInput) {
            accessionInput.value = '';
        }
        
        console.log('7. saveReportAndCount completed');
        console.log('=== copyAndCount END ===');
        
    } finally {
        if (btn) {
            setTimeout(() => {
                btn.disabled = false;
                btn.style.opacity = '1';
                btn.style.cursor = 'pointer';
            }, 5000);
        }
    }
}

// Check if report already exists today
async function checkDuplicateReport(hash, reportText) {
    try {
        const allReports = await getFromFirestore('daily_reports');

        // Get today's date in USER'S LOCAL timezone (YYYY-MM-DD)
        const today = new Date().toLocaleDateString('en-CA');

        console.log('CHECK - Today (User Local):', today);
        console.log('CHECK - Looking for hash:', hash);
        console.log('CHECK - User:', currentUser.code);

        const duplicate = allReports.find(report =>
            report.empCode === currentUser.code &&
            report.submittedDate === today &&
            report.contentHash === hash
        );

        console.log('CHECK - Found duplicate?', !!duplicate);

        return !!duplicate;

    } catch (error) {
        console.error('Error checking duplicate:', error);
        return false;
    }
}

// Show popup when duplicate detected
function showDuplicateOptionsModal(hash, reportText, userSelectedCount, htmlContent) { 
    // Escape backticks and dollar signs so they don’t break template literals
    const escapedReportText = reportText.replace(/`/g, '\\`').replace(/\$/g, '\\$');
    const escapedHtml = htmlContent.replace(/`/g, '\\`').replace(/\$/g, '\\$');

    const modal = createModal(`
        <h2 style="color: #e67e22;">⚠️ Duplicate Report Detected</h2>
        
        <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin: 20px 0; border-left: 4px solid #f39c12;">
            <strong>This report matches an existing submission from today.</strong>
        </div>
        
        <div style="display: flex; flex-direction: column; gap: 10px; margin: 20px 0;">
            <button onclick="handleDuplicateAction('copy_only', '${hash}', \`${escapedReportText}\`, ${userSelectedCount}, \`${escapedHtml}\`)" 
                    class="btn" style="background: #3498db; padding: 15px; text-align: left;">
                <div style="font-weight: bold;">📋 Copy Only</div>
            </button>
            
            <button onclick="handleDuplicateAction('update', '${hash}', \`${escapedReportText}\`, ${userSelectedCount}, \`${escapedHtml}\`)" 
                    class="btn" style="background: #f39c12; padding: 15px; text-align: left;">
                <div style="font-weight: bold;">🔄 Update Previous</div>
            </button>
            
            <button onclick="handleDuplicateAction('addendum', '${hash}', \`${escapedReportText}\`, ${userSelectedCount}, \`${escapedHtml}\`)" 
                    class="btn" style="background: #27ae60; padding: 15px; text-align: left;">
                <div style="font-weight: bold;">➕ Save as Addendum</div>
            </button>
            
            <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 15px;">
                ❌ Cancel
            </button>
        </div>
    `);
}
async function handleDuplicateAction(action, hash, reportText, userSelectedCount, htmlContent) {
    closeModal();
    
    switch(action) {
        case 'copy_only':
            await copyWithFormatting(htmlContent);
            showNotification('📋 Report copied');
            break;
            
        case 'update':
            await saveReportAndCount(hash, reportText, 'update', userSelectedCount, htmlContent);
            showNotification('🔄 Report updated');
            break;
            
        case 'addendum':
            const newHash = hash + '_ADD_' + Date.now();
           await saveReportAndCount(newHash, reportText, 'addendum', userSelectedCount, htmlContent);
            showNotification('✅ Saved as addendum');
            break;
    }
}

// Helper function to copy text to clipboard
function copyTextToClipboard(text) {
    const tempTextarea = document.createElement('textarea');
    tempTextarea.value = text;
    tempTextarea.style.position = 'fixed';
    tempTextarea.style.left = '-9999px';
    document.body.appendChild(tempTextarea);
    tempTextarea.select();
    document.execCommand('copy');
    document.body.removeChild(tempTextarea);
}

async function saveReportAndCount(hash, reportText, saveType, userSelectedCount, htmlContent, selectedInstitution, modalityToSave, accessionNumber) {
    try {
        const now = new Date();

		// ✅ FIXED: Use helper functions for user's local timezone
		const today = getUserLocalDate();
		const submittedTime = getUserLocalTime12Hour();
		const currentTime = now.toISOString();
        

        console.log('[Save Report] Saving with modality:', modalityToSave);
        console.log('[Save Report] Institution:', selectedInstitution);

        if (saveType === 'update') {
            console.log('[Update Mode] Looking for existing report with hash:', hash);
            
            const allReports = await getFromFirestore('daily_reports');
            const existingReport = allReports.find(report => 
                report.empCode === currentUser.code &&
                report.submittedDate === today &&
                report.contentHash === hash
            );
            
            if (existingReport) {
                console.log('[Update Mode] Found existing report, updating:', existingReport.id);
                
                await updateFirestoreDoc('daily_reports', existingReport.id, {
                    reportText: reportText,
                    reportCount: userSelectedCount,
                    lastModified: currentTime,
                    wordCount: reportText.trim().split(/\s+/).length,
                    modality: modalityToSave,
                    institution: selectedInstitution || '',
					 accessionNumber: accessionNumber || ''

                });
                
                await copyWithFormatting(htmlContent);
                await updateReportCounter();
                showNotification('✓ Report updated');
                
            } else {
                console.log('[Update Mode] No existing report found, saving as new');
                
                const reportData = {
                    id: `REPORT_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`,
                    empCode: currentUser.code,
                    empName: currentUser.name,
                    reportText: reportText,
                    contentHash: hash,
                    modality: modalityToSave,
                    submittedDate: today,
                    submittedTime: submittedTime,
                    timestamp: currentTime,
                    wordCount: reportText.trim().split(/\s+/).length,
                    reportType: 'new',
                    status: 'submitted',
                    reportCount: userSelectedCount,
                    institution: selectedInstitution || '',
					accessionNumber: accessionNumber || '' 
                };
                
                await saveToFirestore('daily_reports', reportData);
                await copyWithFormatting(htmlContent);
                await updateReportCounter();
                showNotification('✓ Report saved');
            }
            
        } else {
            console.log('[New Report Mode] Saving with hash:', hash);
            
            const reportData = {
                id: `REPORT_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`,
                empCode: currentUser.code,
                empName: currentUser.name,
                reportText: reportText,
                contentHash: hash,
                modality: modalityToSave,
                submittedDate: today,
                submittedTime: submittedTime,
                timestamp: currentTime,
                wordCount: reportText.trim().split(/\s+/).length,
                reportType: saveType,
                status: 'submitted',
                institution: selectedInstitution || '',
				accessionNumber: accessionNumber || '' ,
                reportCount: userSelectedCount
            };
            
            await saveToFirestore('daily_reports', reportData);
            await copyWithFormatting(htmlContent);
            await updateReportCounter();
            
            if (saveType === 'addendum') {
                showNotification('✓ Saved as addendum');
            } else {
                showNotification('✓ Report saved and counted');
            }
        }
        
    } catch (error) {
        console.error('[Save Report] Error:', error);
        alert('Error saving report. Please try again.');
    }
}

// Update the counter badge on button
async function updateReportCounter() {
    if (!currentUser || !currentUser.code) {
        console.error('[Report Counter] No current user');
        return;
    }
    
    try {
        const allReports = await getFromFirestore('daily_reports');
        const today = getUserLocalDate();
        
        console.log('[Report Counter] Checking reports for:', currentUser.code, 'on', today);
        
        // Sum reportCount (body part counts), not document counts
        const todayCount = allReports
            .filter(report => 
                report.empCode === currentUser.code &&
                report.submittedDate === today
            )
            .reduce((total, report) => total + (report.reportCount || 1), 0);
        
        console.log('[Report Counter] Total count:', todayCount);
        
        // Update button badge (NOT the dropdown!)
        const counterSpan = document.getElementById('reportCounter');
        if (counterSpan) {
            counterSpan.textContent = todayCount;
            console.log('[Report Counter] ✅ Display updated to:', todayCount);
        } else {
            console.error('[Report Counter] ❌ Counter span not found');
        }
        
        // Update button color based on count
        const button = document.getElementById('copyCountBtn');
        if (button) {
            if (todayCount === 0) {
                button.style.background = '#95a5a6'; // Grey
            } else if (todayCount <= 10) {
                button.style.background = '#3498db'; // Blue
            } else if (todayCount <= 20) {
                button.style.background = '#27ae60'; // Green
            } else {
                button.style.background = '#f39c12'; // Gold
            }
        }
        
    } catch (error) {
        console.error('[Report Counter] ❌ Error updating:', error);
    }
}
function populateInstitutionDropdown() {
    const dropdown = document.getElementById('institutionDropdown');
    if (!dropdown) return;
    
    // Keep first option "Select Institution"
    dropdown.innerHTML = '<option value="">Select Institution (required)</option>';
    
    // Add all institutions
    institutions.forEach(inst => {
        const option = document.createElement('option');
        option.value = inst;
        option.textContent = inst;
        dropdown.appendChild(option);
    });
}

async function copyWithFormatting(htmlContent) {
    const plainText = convertHtmlToPlainText(htmlContent);
    
    try {
        const clipboardItem = new ClipboardItem({
            'text/html': new Blob([htmlContent], { type: 'text/html' }),
            'text/plain': new Blob([plainText], { type: 'text/plain' })
        });
        
        await navigator.clipboard.write([clipboardItem]);
        updateStatus('Report copied (formatting preserved)');
    } catch (err) {
        // Fallback
		
        const tempTextarea = document.createElement('textarea');
        tempTextarea.value = plainText;
        tempTextarea.style.position = 'fixed';
        tempTextarea.style.left = '-9999px';
        document.body.appendChild(tempTextarea);
        tempTextarea.select();
        document.execCommand('copy');
        document.body.removeChild(tempTextarea);
        updateStatus('Report copied to clipboard');
    }
	//fallbackCopyPreserveFormat(plainText);
}
async function loadInstitutionsForEmployee() {
    try {
        const doc = await db
            .collection('system_data')
            .doc('institutions')
            .get();

        if (!doc.exists) return;

        const institutions = doc.data().data || [];
        const dropdown = document.getElementById('institutionDropdown');

        if (!dropdown) return;

        dropdown.innerHTML = '<option value="">Select Institution</option>';

        institutions.forEach(inst => {
            const opt = document.createElement('option');
            opt.value = inst;
            opt.textContent = inst;
            dropdown.appendChild(opt);
        });

    } catch (err) {
        console.error('Failed to load institutions:', err);
    }
}

// ==============================================
// ADMIN PANEL FUNCTIONS
// ==============================================

function showAdminPanel() {
	document.getElementById('empToolbar').style.display = 'none';
    document.getElementById('hrToolbar').style.display = 'none';
    document.getElementById('mainContainer').style.display = 'none';
    document.getElementById('hrQAPanel').style.display = 'none';
    document.getElementById('hrPeerPanel').style.display = 'none';
    document.getElementById('qaBoard').style.display = 'none';
    document.getElementById('peerBoard').style.display = 'none';
    
    // Show admin panel
    document.getElementById('adminPanel').style.display = 'block';
    loadAdminData();
	
	    console.log('Admin panel should now be visible');
}

function hideAdminPanel() {
    document.getElementById('adminPanel').style.display = 'none';
    
if (currentUser.role === 'admin' || currentUser.role === 'employee') {
        setupEmployeeInterface();
    } else if (currentUser.role === 'hr') {
        setupHRInterface();
    }
    
    console.log('Admin panel hidden, restored interface');
}
function openAdminScheduleManager() {
    // Hide admin panel
    document.getElementById('adminPanel').style.display = 'none';
    
    // Show HR schedule panel
    document.getElementById('hrSchedulePanel').style.display = 'block';
    
    // Add back button for admin ONLY
    const headerButtons = document.getElementById('scheduleHeaderButtons');
    if (headerButtons && !document.getElementById('adminBackBtn')) {
        const backBtn = document.createElement('button');
        backBtn.id = 'adminBackBtn';
        backBtn.className = 'btn';
        backBtn.style.background = '#95a5a6';
        backBtn.style.marginRight = 'auto';
        backBtn.textContent = '← Back to Admin Panel';
        backBtn.onclick = backToAdminPanel;
        headerButtons.insertBefore(backBtn, headerButtons.firstChild);
    }
    
    // Hide other panels
    document.getElementById('empToolbar').style.display = 'none';
    document.getElementById('mainContainer').style.display = 'none';
    document.getElementById('hrQAPanel').style.display = 'none';
    document.getElementById('hrPeerPanel').style.display = 'none';
    document.getElementById('qaBoard').style.display = 'none';
    document.getElementById('peerBoard').style.display = 'none';
    
    // Load schedule
    currentScheduleMonth = new Date();
    currentScheduleCategory = 'RAD';
    loadHRSchedule();
    updateLeaveRequestCounter();
    
    updateStatus('Schedule Manager opened');
}
function backToAdminPanel() {
    document.getElementById('hrSchedulePanel').style.display = 'none';
    showAdminPanel();
}

async function loadAdminData() {
    try {
        await loadSystemData();
       
        // ✅ CONSISTENT: Use empCode everywhere
        const employeeText = Object.entries(authorizedEmployees)
		.map(([empCode, emp]) => `${empCode} = ${emp.name} | ${emp.specialty} | ${emp.department} | ${emp.category || 'RAD'} | ${emp.email || ''} | ${emp.proxyEnabled || false}`)
		.join('\n');
        document.getElementById('employeeData').value = employeeText;
        updateEmployeeCount();
        
        // ... rest of function
        const shortcutsText = Object.entries(shortcuts)
            .map(([key, value]) => `${key} = ${value}`)
            .join('\n');
        document.getElementById('shortcutsData').value = shortcutsText;
        
        const templatesText = Object.entries(templates)
            .map(([key, value]) => `${key} = ${value}\n\n---\n`)
            .join('\n');
        document.getElementById('templatesData').value = templatesText;
        
        const criticalText = criticalFindings.join('\n');
        document.getElementById('criticalFindingsData').value = criticalText;
        updateCriticalFindingsCount();
		
		const institutionsText = institutions.join('\n');
		document.getElementById('institutionsData').value = institutionsText;
		updateInstitutionCount();
        
        // Load AI configuration
        const aiConfigDoc = await db.collection('system_data').doc('ai_config').get();
        if (aiConfigDoc.exists) {
            const aiConfig = aiConfigDoc.data();
            document.getElementById('geminiApiKey').value = aiConfig.apiKey || '';
            document.getElementById('aiEnabled').checked = aiConfig.enabled || false;
        }
        
        // Load template categories
        const categoriesDoc = await db.collection('system_data').doc('template_categories').get();
        if (categoriesDoc.exists) {
            const categoriesData = categoriesDoc.data().data;
            document.getElementById('categoriesData').value = JSON.stringify(categoriesData, null, 2);
        } else {
            document.getElementById('categoriesData').value = JSON.stringify(templateCategories, null, 2);
        }
        updateCategoriesCount();
        
        loadPermissionsList();
		refreshAccessLog();
		updateDataCounts();
		loadTickets('open');

		// Load notes count
		const allNotes = await getFromFirestore('notes_board');
		document.getElementById('totalNotesCount').textContent = allNotes.length;

		loadPasswordManagement();
        
    } catch (error) {
        console.error('Error loading admin data:', error);
    }
}

function loadPermissionsList() {
    const permissionsList = document.getElementById('permissionsList');
    
    const html = Object.entries(authorizedEmployees).map(([empCode, emp]) => {
        const permissions = emp.permissions || [];
        const allPermissions = [
            'templates', 'voice', 'qa_response', 'peer_response', 
            'qa_assign', 'peer_assign', 'qa_grade', 'view_logs', 
            'export_data', 'adv_search', 'peer_review', 
            'master_schedule_view', 'note_creator', 'note_manager', 
            'file_upload', 'file_delete', 'report_viewer', 'report_manager', 
            'emp_session', 'body_part_rules_manager', 'password_manager', 'qa_edit', 'qa_delete', 'qa_revert'
        ];
        
        return `
            <div style="border: 1px solid #ddd; padding: 15px; margin: 10px 0; border-radius: 5px;">
                <h4>${emp.name} (${empCode}) - ${emp.role}</h4>
                <div style="margin-top: 10px;">
					${allPermissions.map(perm => {
						const isHighPrivilege = ['password_manager', 'body_part_rules_manager', 'report_manager'].includes(perm);
						const labelStyle = isHighPrivilege ? 'background: #fff3cd; padding: 5px 8px; border-radius: 3px; border: 1px solid #ffc107;' : '';
						
						return `
						<label style="display: inline-block; margin: 5px 10px 5px 0; ${labelStyle}">
							<input type="checkbox" ${permissions.includes(perm) ? 'checked' : ''} 
								   onchange="updatePermission('${empCode}', '${perm}', this.checked)">
							${perm.replace(/_/g, ' ').replace(/\b\w/g, l => l.toUpperCase())}
							${isHighPrivilege ? ' 🔒' : ''}
						</label>
						`;
					}).join('')}
				</div>
                <div style="margin-top: 10px;">
                    <label style="display: inline-block; margin: 5px 10px 5px 0;">
						<input type="checkbox" ${emp.proxyEnabled ? 'checked' : ''} 
							   onchange="toggleProxyForEmployee('${empCode}', this.checked)">
						Proxy Enabled
					</label>
                </div>
            </div>
        `;
    }).join('');
    
    permissionsList.innerHTML = html;
}

async function updatePermission(empCode, permission, isGranted) {
    // ✅ CONSISTENT: Use empCode parameter name
    try {
        // ✅ Validate empCode exists
        if (!authorizedEmployees[empCode]) {
            console.error(`Employee ${empCode} not found`);
            showNotification('❌ Employee not found');
            return;
        }
        
        if (!authorizedEmployees[empCode].permissions) {
            authorizedEmployees[empCode].permissions = [];
        }
        
        if (isGranted) {
            if (!authorizedEmployees[empCode].permissions.includes(permission)) {
                authorizedEmployees[empCode].permissions.push(permission);
            }
        } else {
            authorizedEmployees[empCode].permissions = 
                authorizedEmployees[empCode].permissions.filter(p => p !== permission);
        }
        
        // ✅ Save to Firestore
        await saveEmployees();
        showNotification(`✅ Permission updated for ${authorizedEmployees[empCode].name}`);
        
    } catch (error) {
        console.error('Error updating permission:', error);
        showNotification('❌ Error updating permission');
    }
}

function refreshPermissions() {
    loadAdminData();
    showNotification('Permissions refreshed');
}

async function saveEmployees() {
    try {
	 if (document.getElementById('adminPanel').style.display !== 'block') {
            console.log('[SAVE] Skipped - not in admin panel');
            return;
        }
        const data = document.getElementById('employeeData').value;
        const newEmployees = {};
        
        // ✅ BACKUP ALL CURRENT CREDENTIALS BEFORE EDITING
        console.log('[SAVE] Creating backup before employee list edit...');
        for (const [empCode, emp] of Object.entries(authorizedEmployees)) {
            if (emp.role === 'employee') {
                await backupEmployeeCredentials(empCode, 'admin_edit', emp);
            }
        }
        
        data.split('\n').forEach(line => {
            const trimmedLine = line.trim();
            // ✅ FIX: More flexible parsing - handles =, = , or spaces around =
            if (trimmedLine && trimmedLine.includes('=')) {
                // Split on first = only, handling any spacing
                const equalIndex = trimmedLine.indexOf('=');
                if (equalIndex === -1) return;
                
                const rawCode = trimmedLine.substring(0, equalIndex).trim();
                const info = trimmedLine.substring(equalIndex + 1).trim();
                
                // Skip if no code or no info
                if (!rawCode || !info) return;
                
                // ✅ STANDARDIZE IMMEDIATELY
                const empCode = rawCode.toUpperCase();
                
                const parts = info.split('|').map(s => s.trim());
                
                const name = parts[0] || 'Unknown';
                const specialty = parts[1] || 'General';
                const department = parts[2] || 'Radiology';
                const category = parts[3] || 'RAD';
                const email = parts[4] || '';
				const proxyEnabled = (parts[5] || '').toLowerCase() === 'true';

                
                // ✅ CONSISTENT: Always use empCode
                const existingEmployee = authorizedEmployees[empCode] || {};
                
                let role = 'employee';
                if (department.toLowerCase().includes('hr') || empCode.startsWith('HR')) {
                    role = 'hr';
                }
                
                const validCategories = ['RAD', 'TECH', 'RA', 'COORD'];
                const empCategory = validCategories.includes(category.toUpperCase()) 
                    ? category.toUpperCase() 
                    : 'RAD';
                
                // ✅ CONSISTENT: Always use empCode as key
                newEmployees[empCode] = {
                    name: name,
                    specialty: specialty,
                    department: department,
                    category: empCategory,
                    email: email,
                    role: role,
					                    
                    // ✅ Preserve existing data
					proxyEnabled: proxyEnabled,
                    permissions: existingEmployee.permissions || [],
                    passwordSet: existingEmployee.passwordSet || false,
                    password: existingEmployee.password || null,
                    passwordSetDate: existingEmployee.passwordSetDate || null,
                    passwordReminderCount: existingEmployee.passwordReminderCount || 0,
                    passwordSetupDeadline: existingEmployee.passwordSetupDeadline || null,
                    failedLoginAttempts: existingEmployee.failedLoginAttempts || 0,
                    accountLocked: existingEmployee.accountLocked || false,
                    mustChangePassword: existingEmployee.mustChangePassword || false,
                    passwordResetBy: existingEmployee.passwordResetBy || null,
                    passwordResetDate: existingEmployee.passwordResetDate || null,
                    unlockedBy: existingEmployee.unlockedBy || null,
                    unlockedDate: existingEmployee.unlockedDate || null
                };
                
                // Initialize leave balance for NEW employees only
                if (!existingEmployee.name) {
                    initializeLeaveBalance(empCode);
                }
            }
        });
        
        // ✅ Debug logging
        console.log(`[PARSE RESULT] Parsed ${Object.keys(newEmployees).length} employees`);
        console.log('[SAMPLE]', Object.keys(newEmployees).slice(0, 3));
        
        // ✅ Safety checks
        const currentCount = Object.keys(authorizedEmployees).length;
        const newCount = Object.keys(newEmployees).length;
        
        console.log(`[Save Check] Current: ${currentCount} employees, New: ${newCount} employees`);
        
        if (newCount === 0) {
            alert('⛔ BLOCKED: Cannot save ZERO employees!\n\nThis would delete all employee data.\n\nCheck your data format. Each line should be:\nCODE=Name|Specialty|Department|Category|Email');
            console.error('[BLOCKED] Attempted to save 0 employees');
            console.error('[DATA]', data.substring(0, 200)); // Log first 200 chars
            return;
        }
        
        if (newCount < 5) {
            alert(`⛔ BLOCKED: Only ${newCount} employees detected!\n\nYou have ${currentCount} employees in the system.\n\nThis looks like an error. Save blocked for safety.`);
            console.error(`[BLOCKED] Too few employees (${newCount}), expected around ${currentCount}`);
            return;
        }
        
        if (newCount < currentCount * 0.7) {
            const proceed = confirm(
                `⚠️ CRITICAL WARNING!\n\n` +
                `Current employees: ${currentCount}\n` +
                `New employee count: ${newCount}\n\n` +
                `You are about to LOSE ${currentCount - newCount} employees!\n\n` +
                `Are you ABSOLUTELY SURE this is correct?`
            );
            if (!proceed) {
                showNotification('❌ Save cancelled - employee count dropped too much');
                console.log('[CANCELLED] User cancelled save due to employee count drop');
                return;
            }
        }
        
        console.log(`[SAVE] ✅ Proceeding to save ${newCount} employees (passwords preserved)`);
        
        await db.runTransaction(async (transaction) => {
            const employeesRef = db.collection('system_data').doc('employees');
            const employeesDoc = await transaction.get(employeesRef);
            
            if (!employeesDoc.exists) {
                throw new Error('Employees document not found');
            }
            
            transaction.update(employeesRef, {
                data: newEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: currentUser.code || currentUser.username
            });
        });
        
        authorizedEmployees = newEmployees;
        await loadSystemData();
        updateEmployeeCount();
        loadPermissionsList();
        showNotification('✅ Employees saved successfully!');
        
    } catch (error) {
        console.error('Error saving employees:', error);
        showNotification('❌ Error saving employees: ' + error.message);
    }
}

async function saveShortcuts() {
    try {
        const data = document.getElementById('shortcutsData').value;
        const newShortcuts = {};
        
        data.split('\n').forEach(line => {
            const [key, ...valueParts] = line.split(' = ');
            if (key && valueParts.length > 0) {
                newShortcuts[key.trim()] = valueParts.join(' = ').trim();
            }
        });
        
        await db.collection('system_data').doc('shortcuts').set({
            data: newShortcuts,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        shortcuts = newShortcuts;
        showNotification('Shortcuts saved and updated for all users!');
        
    } catch (error) {
        console.error('Error saving shortcuts:', error);
        showNotification('Error saving shortcuts.');
    }
}

async function saveTemplates() {
    try {
        const data = document.getElementById('templatesData').value;
        const newTemplates = {};
        
        const templateBlocks = data.split('---');
        templateBlocks.forEach(block => {
            const lines = block.trim().split('\n');
            if (lines.length > 0) {
                const firstLine = lines[0];
                const [key, ...valueParts] = firstLine.split(' = ');
                if (key && valueParts.length > 0) {
                    const templateContent = [valueParts.join(' = '), ...lines.slice(1)].join('\n').trim();
                    newTemplates[key.trim()] = templateContent;
                }
            }
        });
        
        await db.collection('system_data').doc('templates').set({
            data: newTemplates,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        templates = newTemplates;
        showNotification('Templates saved and updated for all users!');
        
    } catch (error) {
        console.error('Error saving templates:', error);
        showNotification('Error saving templates.');
    }
}

function updateEmployeeCount() {
    const empCountEl = document.getElementById('empCount');
    if (empCountEl) {
        empCountEl.textContent = Object.keys(authorizedEmployees).length;
    }
}

async function refreshAccessLog() {
    try {
        const accessLogs = await getFromFirestore('access_logs');
        const logDiv = document.getElementById('accessLog');
        
        if (accessLogs.length === 0) {
            logDiv.innerHTML = '<em>No access attempts logged yet.</em>';
            return;
        }
        
        const sortedLogs = accessLogs
            .sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp))
            .slice(0, 50);
        
        const logHtml = sortedLogs.map(log => {
            const date = new Date(log.timestamp).toLocaleString();
            const statusIcon = log.action === 'login_success' ? '✅' : '❌';
            const statusColor = log.action === 'login_success' ? '#27ae60' : '#e74c3c';
            
            return `<div style="margin: 3px 0; color: ${statusColor};">
                ${statusIcon} ${date} | ${log.code} | ${log.name} | ${log.action.toUpperCase()}
            </div>`;
        }).join('');
        
        logDiv.innerHTML = logHtml;
        
    } catch (error) {
        console.error('Error loading access log:', error);
        document.getElementById('accessLog').innerHTML = '<em>Error loading access log.</em>';
    }
}

async function clearAccessLog() {
    if (!confirm('Clear all access logs? This cannot be undone.')) return;
    
    try {
        const accessLogs = await getFromFirestore('access_logs');
        const batch = db.batch();
        
        const snapshot = await db.collection('access_logs').get();
        snapshot.forEach(doc => {
            batch.delete(doc.ref);
        });
        
        await batch.commit();
        refreshAccessLog();
        showNotification('Access logs cleared successfully!');
        
    } catch (error) {
        console.error('Error clearing access log:', error);
        showNotification('Error clearing access logs.');
    }
}

async function saveCriticalFindings() {
    try {
        const data = document.getElementById('criticalFindingsData').value;
        const newCriticalFindings = [];
        
        data.split('\n').forEach(line => {
            const phrase = line.trim();
            if (phrase) {
                newCriticalFindings.push(phrase.toLowerCase());
            }
        });
        
        await db.collection('system_data').doc('critical_findings').set({
            data: newCriticalFindings,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        criticalFindings = newCriticalFindings;
        updateCriticalFindingsCount();
        showNotification('Critical findings saved and updated!');
        
    } catch (error) {
        console.error('Error saving critical findings:', error);
        showNotification('Error saving critical findings.');
    }
}

function updateCriticalFindingsCount() {
    const countEl = document.getElementById('criticalCount');
    if (countEl) {
        countEl.textContent = criticalFindings.length;
    }
}
async function saveAIConfig() {
    const apiKey = document.getElementById('geminiApiKey').value.trim();
    const enabled = document.getElementById('aiEnabled').checked;
    
    if (enabled && !apiKey) {
        alert('Please enter an API key to enable AI recommendations');
        return;
    }
    
    try {
        await db.collection('system_data').doc('ai_config').set({
            apiKey: apiKey,
            enabled: enabled,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        GEMINI_CONFIG.apiKey = apiKey;
        GEMINI_CONFIG.enabled = enabled;
        
        showNotification('AI configuration saved successfully!');
        
    } catch (error) {
        console.error('Error saving AI config:', error);
        showNotification('Error saving AI configuration');
    }
}
async function saveCategories() {
    try {
        const data = document.getElementById('categoriesData').value;
        
        // Validate JSON format
        let newCategories;
        try {
            newCategories = JSON.parse(data);
        } catch (e) {
            alert('Invalid JSON format. Please check your syntax.');
            return;
        }
        
        await db.collection('system_data').doc('template_categories').set({
            data: newCategories,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        // Update global variable
        Object.assign(templateCategories, newCategories);
        
        updateCategoriesCount();
        showNotification('Categories saved successfully!');
        
    } catch (error) {
        console.error('Error saving categories:', error);
        showNotification('Error saving categories');
    }
}

function updateCategoriesCount() {
    const countEl = document.getElementById('categoriesCount');
    if (countEl) {
        const totalCategories = Object.values(templateCategories).reduce((sum, modality) => 
            sum + Object.keys(modality).length, 0
        );
        countEl.textContent = totalCategories;
    }
}

async function saveInstitutions() {
    try {
        const data = document.getElementById('institutionsData').value;
        const newInstitutions = [];
        
        data.split('\n').forEach(line => {
            const inst = line.trim();
            if (inst) {
                newInstitutions.push(inst);
            }
        });
        
        await db.collection('system_data').doc('institutions').set({
            data: newInstitutions,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        });
        
        institutions = newInstitutions;
        updateInstitutionCount();
        populateInstitutionDropdown();
        showNotification('✅ Institutions saved and updated!');
        
    } catch (error) {
        console.error('Error saving institutions:', error);
        showNotification('❌ Error saving institutions.');
    }
}

function updateInstitutionCount() {
    const countEl = document.getElementById('institutionCount');
    if (countEl) {
        countEl.textContent = institutions.length;
    }
}

// ==============================================
// NOTES BOARD SYSTEM
// ==============================================

async function initializeNotesBoard() {
    if (!currentUser || currentUser.role !== 'employee') return;
    
    const isCreator = currentUser.permissions && currentUser.permissions.includes('note_creator');
    const isManager = currentUser.permissions && currentUser.permissions.includes('note_manager');
    
    if (!isCreator && !isManager) {
        // Hide notes board if no permission
        document.querySelector('.sidebar > div:first-child').style.display = 'none';
        return;
    }
    
    // Show create button for creators
    if (isCreator) {
        document.getElementById('createNoteBtn').style.display = 'block';
    }
    
    // Load notes
    await loadNotesBoard();
    
    // Setup real-time listener
    setupNotesListener();
}

async function loadNotesBoard() {
    const allNotes = await getFromFirestore('notes_board');
    const isCreator = currentUser.permissions && currentUser.permissions.includes('note_creator');
    const isManager = currentUser.permissions && currentUser.permissions.includes('note_manager');
    
    let notesToShow = [];
    
    if (isManager) {
        // Managers see ALL notes
        notesToShow = allNotes.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
    } else if (isCreator) {
        // Creators see only their own
        notesToShow = allNotes.filter(n => n.createdBy === currentUser.code)
            .sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
    }
    
    // Update counter for managers
    if (isManager) {
        const counter = document.getElementById('notesCounter');
        if (notesToShow.length > 0) {
            counter.textContent = notesToShow.length;
            counter.style.display = 'inline-block';
        } else {
            counter.style.display = 'none';
        }
    }
    
    // Render notes
    const notesList = document.getElementById('notesList');
    
    if (notesToShow.length === 0) {
        notesList.innerHTML = '<div style="text-align: center; color: #666; padding: 20px; font-size: 12px;">No notes</div>';
        return;
    }
    
    const html = notesToShow.map(note => {
        const date = new Date(note.timestamp);
        const dateStr = date.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
        const timeStr = date.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' });
        
        const authorName = authorizedEmployees[note.createdBy]?.name || note.createdBy;
        
        return `
            <div class="note-item ${note.category}">
                <div class="note-header">
                    <span class="note-category ${note.category}">${note.category === 'review' ? 'REVIEW' : 'OTHER'}</span>
                    <span class="note-timestamp">${dateStr} ${timeStr}</span>
                </div>
                <div class="note-content">${escapeHtml(note.content)}</div>
                <div class="note-author">By: ${authorName}</div>
                ${renderNoteActions(note, isManager, isCreator)}
            </div>
        `;
    }).join('');
    
    notesList.innerHTML = html;
}

function renderNoteActions(note, isManager, isCreator) {
    const isOwnNote = note.createdBy === currentUser.code;
    
    let actions = '<div class="note-actions">';
    
    // Creators can edit their own notes
    if (isCreator && isOwnNote) {
        actions += `<button class="note-edit-btn" onclick="editNote('${note.id}')">✏️ Edit</button>`;
    }
    
    // Managers can edit/delete any note
    if (isManager) {
        actions += `<button class="note-edit-btn" onclick="editNote('${note.id}')">✏️ Edit</button>`;
        actions += `<button class="note-delete-btn" onclick="deleteNote('${note.id}')">🗑️ Delete</button>`;
    }
    
    // Creators can delete only their own
    if (isCreator && isOwnNote && !isManager) {
        actions += `<button class="note-delete-btn" onclick="deleteNote('${note.id}')">🗑️ Delete</button>`;
    }
    
    actions += '</div>';
    
    return actions;
}

function setupNotesListener() {
    const notesListener = db.collection('notes_board').onSnapshot((snapshot) => {
        loadNotesBoard();
    });
    
    unsubscribeListeners.push(notesListener);
}

// ==============================================
// NOTES BOARD SYSTEM
// ==============================================

async function initializeNotesBoard() {
    if (!currentUser || currentUser.role !== 'employee') return;
    
    const isCreator = currentUser.permissions && currentUser.permissions.includes('note_creator');
    const isManager = currentUser.permissions && currentUser.permissions.includes('note_manager');
    
    if (!isCreator && !isManager) {
        // Hide notes board button if no permission
        const notesBtn = document.getElementById('notesBoardButton');
        if (notesBtn) notesBtn.style.display = 'none';
        return;
    }
    
    // Show notes board button
    const notesBtn = document.getElementById('notesBoardButton');
    if (notesBtn) notesBtn.style.display = 'block';
    
    // Setup real-time listener for counter
    setupNotesListener();
}

async function updateNotesCounter() {
    const isManager = currentUser.permissions && currentUser.permissions.includes('note_manager');
    
    if (isManager) {
        const allNotes = await getFromFirestore('notes_board');
        const counter = document.getElementById('notesCounter');
        
        if (allNotes.length > 0) {
            counter.textContent = allNotes.length;
            counter.style.display = 'inline-block';
        } else {
            counter.style.display = 'none';
        }
    }
}

async function openNotesBoard() {
    const allNotes = await getFromFirestore('notes_board');
    const isCreator = currentUser.permissions && currentUser.permissions.includes('note_creator');
    const isManager = currentUser.permissions && currentUser.permissions.includes('note_manager');
    
    let notesToShow = [];
    
    if (isManager) {
        // Managers see ALL notes
        notesToShow = allNotes.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
    } else if (isCreator) {
        // Creators see only their own
        notesToShow = allNotes.filter(n => n.createdBy === currentUser.code)
            .sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
    }
    
    const createButton = isCreator ? `
        <button onclick="openCreateNoteModal()" class="btn" style="background: #27ae60; margin-right: 10px;">
            ➕ Create New Note
        </button>
    ` : '';
    
    const notesHtml = notesToShow.length === 0 
        ? '<div style="text-align: center; color: #666; padding: 40px;">No notes available</div>'
        : notesToShow.map(note => renderNoteCard(note, isManager, isCreator)).join('');
    
    const modal = createModal(`
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
            <h2 style="margin: 0;">📝 Notes Board</h2>
            <div>
                ${createButton}
                <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
            </div>
        </div>
        
        <div style="max-height: 600px; overflow-y: auto; padding: 10px;">
            ${notesHtml}
        </div>
    `);
}

function renderNoteCard(note, isManager, isCreator) {
    const date = new Date(note.timestamp);
    const dateStr = date.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
    const timeStr = date.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' });
    
    const authorName = authorizedEmployees[note.createdBy]?.name || note.createdBy;
    const isOwnNote = note.createdBy === currentUser.code;
    
    const categoryColor = note.category === 'review' ? '#e74c3c' : '#9b59b6';
    const categoryText = note.category === 'review' ? 'REVIEW' : 'OTHER NOTE';
    
    let actionButtons = '';
    
    if (isManager) {
        actionButtons = `
            <button onclick="editNoteInline('${note.id}')" style="background: #3498db; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer; font-size: 12px; margin-right: 5px;">✏️ Edit</button>
            <button onclick="deleteNote('${note.id}')" style="background: #e74c3c; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer; font-size: 12px;">🗑️ Delete</button>
        `;
    } else if (isCreator && isOwnNote) {
        actionButtons = `
            <button onclick="editNoteInline('${note.id}')" style="background: #3498db; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer; font-size: 12px; margin-right: 5px;">✏️ Edit</button>
            <button onclick="deleteNote('${note.id}')" style="background: #e74c3c; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer; font-size: 12px;">🗑️ Delete</button>
        `;
    }
    
    return `
        <div style="background: white; border: 1px solid #dee2e6; border-left: 4px solid ${categoryColor}; border-radius: 8px; padding: 20px; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
            <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 15px; padding-bottom: 10px; border-bottom: 2px solid #ecf0f1;">
                <div>
                    <span style="background: ${categoryColor}; color: white; padding: 4px 10px; border-radius: 4px; font-size: 11px; font-weight: bold;">${categoryText}</span>
                    <div style="font-size: 11px; color: #6c757d; margin-top: 5px;">${dateStr} at ${timeStr}</div>
                </div>
                <div style="font-size: 12px; color: #495057; font-weight: 500;">By: ${authorName}</div>
            </div>
            
            <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; font-family: 'Courier New', monospace; font-size: 13px; line-height: 1.6; white-space: pre-wrap; word-wrap: break-word; margin-bottom: 15px; max-height: 300px; overflow-y: auto;">
${escapeHtml(note.content)}</div>
            
            <div style="text-align: right;">
                ${actionButtons}
            </div>
        </div>
    `;
}

function openCreateNoteModal() {
    closeModal(); // Close notes board
    
    const modal = createModal(`
        <h3>📝 Create New Note</h3>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Category:</label>
            <select id="noteCategory" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-size: 14px;">
                <option value="review">Review</option>
                <option value="other">Other Note</option>
            </select>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Note Content:</label>
            <textarea id="noteContent" rows="15" placeholder="Type your note here..." 
                style="width: 100%; padding: 15px; border: 2px solid #ddd; border-radius: 5px; font-family: 'Courier New', monospace; font-size: 14px; line-height: 1.6; resize: vertical;"></textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="saveNote()" class="btn" style="background: #27ae60; margin-right: 10px;">
                💾 Save Note
            </button>
            <button onclick="openNotesBoard()" class="btn" style="background: #95a5a6;">Back to Notes</button>
        </div>
    `);
}

async function saveNote(noteId = null) {
    const category = document.getElementById('noteCategory').value;
    const content = document.getElementById('noteContent').value.trim();
    
    if (!content) {
        alert('Please enter note content');
        return;
    }
    
    try {
        if (noteId) {
            // Update existing note
            await updateFirestoreDoc('notes_board', noteId, {
                category: category,
                content: content,
                lastModified: new Date().toISOString(),
                lastModifiedBy: currentUser.code
            });
            
            showNotification('Note updated successfully!');
        } else {
            // Create new note
            const newNote = {
                id: `NOTE_${Date.now()}`,
                category: category,
                content: content,
                createdBy: currentUser.code,
                createdByName: currentUser.name,
                timestamp: new Date().toISOString(),
                lastModified: new Date().toISOString(),
                lastModifiedBy: currentUser.code
            };
            
            await saveToFirestore('notes_board', newNote);
            showNotification('Note created successfully!');
        }
        
        closeModal();
        openNotesBoard();
        
    } catch (error) {
        console.error('Error saving note:', error);
        alert('Error saving note. Please try again.');
    }
}

async function editNoteInline(noteId) {
    const allNotes = await getFromFirestore('notes_board');
    const note = allNotes.find(n => n.id === noteId);
    
    if (!note) return;
    
    closeModal(); // Close notes board
    
    const modal = createModal(`
        <h3>✏️ Edit Note</h3>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Category:</label>
            <select id="noteCategory" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-size: 14px;">
                <option value="review" ${note.category === 'review' ? 'selected' : ''}>Review</option>
                <option value="other" ${note.category === 'other' ? 'selected' : ''}>Other Note</option>
            </select>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Note Content:</label>
            <textarea id="noteContent" rows="15" 
                style="width: 100%; padding: 15px; border: 2px solid #ddd; border-radius: 5px; font-family: 'Courier New', monospace; font-size: 14px; line-height: 1.6; resize: vertical;">${note.content}</textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="saveNote('${noteId}')" class="btn" style="background: #27ae60; margin-right: 10px;">
                💾 Update Note
            </button>
            <button onclick="openNotesBoard()" class="btn" style="background: #95a5a6;">Back to Notes</button>
        </div>
    `);
}

async function deleteNote(noteId) {
    if (!confirm('Delete this note permanently? This will remove it for all users.')) return;
    
    try {
        const snapshot = await db.collection('notes_board').get();
        snapshot.forEach(async (doc) => {
            if (doc.data().id === noteId) {
                await doc.ref.delete();
            }
        });
        
        showNotification('Note deleted successfully!');
        closeModal();
        openNotesBoard();
        
    } catch (error) {
        console.error('Error deleting note:', error);
        alert('Error deleting note. Please try again.');
    }
}
// ==============================================
// FILE UPLOAD SYSTEM
// ==============================================

async function openMyFiles() {
    try {
        const isHR = currentUser.role === 'hr' || currentUser.role === 'admin';
        const canUpload = isHR && currentUser.permissions && currentUser.permissions.includes('file_upload');
        const canDelete = currentUser.permissions && currentUser.permissions.includes('file_delete');
        
// Fetch files from Firestore
        const allFiles = await getFromFirestore('employee_files');
        
// Filter files based on role
			let userFiles = [];
			if (isHR || currentUser.role === 'admin') {
				userFiles = allFiles; // HR/Admin see all files
			} else {
				// Employee sees files shared with them OR shared with ALL
				userFiles = allFiles.filter(f => 
					f.sharedWith && (
						f.sharedWith.includes(currentUser.code) || 
						f.sharedWith.includes('ALL')
					)
				);
			}
        
        // Sort by upload date (newest first)
        userFiles.sort((a, b) => new Date(b.uploadedDate) - new Date(a.uploadedDate));
        
        const modal = createModal(`
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; padding-bottom: 15px; border-bottom: 2px solid #9b59b6;">
                <h2 style="margin: 0; color: #2c3e50;">📁 My Files</h2>
                <div>
                    ${canUpload ? '<button onclick="openUploadFileModal()" class="btn" style="background: #27ae60; margin-right: 10px;">➕ Upload File</button>' : ''}
                    <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
                </div>
            </div>
            
            <div style="display: flex; gap: 10px; margin-bottom: 20px;">
                <input type="text" id="fileSearchInput" placeholder="🔍 Search files..." 
                       onkeyup="filterMyFiles()" 
                       style="flex: 1; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <select id="fileCategoryFilter" onchange="filterMyFiles()" 
                        style="padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    <option value="">All Categories</option>
                    <option value="personal">Personal</option>
                    <option value="work">Work</option>
                </select>
                ${isHR ? `
                <select id="fileEmployeeFilter" onchange="filterMyFiles()" 
                        style="padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    <option value="">All Employees</option>
                    <option value="ALL">Generic (All Employees)</option>
                    ${Object.entries(authorizedEmployees)
                        .filter(([code, emp]) => emp.role === 'employee')
                        .map(([code, emp]) => `<option value="${code}">${emp.name} (${code})</option>`)
                        .join('')}
                </select>
                ` : ''}
            </div>
            
            <div id="myFilesContainer" style="max-height: 500px; overflow-y: auto;">
                ${renderFilesTable(userFiles, canDelete, isHR)}
            </div>
        `);
        
        // Store files globally for filtering
        window.currentFilesData = userFiles;
        window.canDeleteFiles = canDelete;
        window.isHRView = isHR;
        
    } catch (error) {
        console.error('Error loading files:', error);
        alert('Error loading files. Please try again.');
    }
}

async function openUploadFileModal() {
    closeModal(); // Close My Files modal
    
    const modal = createModal(`
        <h3>➕ Upload File</h3>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Category:</label>
            <select id="uploadFileCategory" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="personal">Personal</option>
                <option value="work">Work</option>
            </select>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Select File (PDF, Word, Excel - Max 10MB):</label>
            <input type="file" id="uploadFileInput" accept=".pdf,.doc,.docx,.xls,.xlsx" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
            <div id="uploadFilePreview" style="margin-top: 10px; font-size: 12px; color: #666;"></div>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 10px; font-weight: 500;">Share with Employees:</label>
            
            <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; border: 1px solid #ddd;">
                <!-- All Employees checkbox -->
                <label style="display: flex; align-items: center; padding: 8px; background: #fff3cd; border-radius: 5px; margin-bottom: 10px; cursor: pointer;">
                    <input type="checkbox" id="shareWithAll" onchange="toggleAllEmployeesShare()" style="margin-right: 10px; transform: scale(1.3);">
                    <span style="font-weight: bold; color: #856404;">📢 All Employees (Generic File)</span>
                </label>
                
                <!-- Select All / Deselect All -->
                <div style="display: flex; gap: 10px; margin-bottom: 10px; padding: 8px; background: white; border-radius: 5px;">
                    <button onclick="selectAllEmployees()" class="btn" style="flex: 1; background: #3498db; padding: 6px 10px; font-size: 12px;">
                        ✓ Select All
                    </button>
                    <button onclick="deselectAllEmployees()" class="btn" style="flex: 1; background: #95a5a6; padding: 6px 10px; font-size: 12px;">
                        ✗ Deselect All
                    </button>
                </div>
                
                <!-- Role-based bulk selection -->
                <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin-bottom: 10px;">
                    <button onclick="selectByRole('RAD')" class="btn" style="background: #e74c3c; padding: 6px 8px; font-size: 11px;">
                        All RAD
                    </button>
                    <button onclick="selectByRole('TECH')" class="btn" style="background: #f39c12; padding: 6px 8px; font-size: 11px;">
                        All TECH
                    </button>
                    <button onclick="selectByRole('RA')" class="btn" style="background: #9b59b6; padding: 6px 8px; font-size: 11px;">
                        All RA
                    </button>
                    <button onclick="selectByRole('COORD')" class="btn" style="background: #27ae60; padding: 6px 8px; font-size: 11px;">
                        All COORD
                    </button>
                </div>
                
                <!-- Employee list with checkboxes -->
                <div id="employeeCheckboxList" style="max-height: 300px; overflow-y: auto; background: white; padding: 10px; border-radius: 5px; border: 1px solid #ddd;">
                    ${generateEmployeeCheckboxes()}
                </div>
                
                <div style="margin-top: 10px; font-size: 12px; color: #666; text-align: center;">
                    <span id="selectedEmployeeCount">0 employees selected</span>
                </div>
            </div>
        </div>
        
        <div style="background: #e3f2fd; padding: 10px; border-radius: 5px; margin-bottom: 20px; font-size: 12px;">
            💡 <strong>Tip:</strong> Select specific employees to share the file with. You can change sharing later.
        </div>
        
        <div style="text-align: right;">
            <button onclick="uploadFileToStorage()" class="btn" style="background: #27ae60; margin-right: 10px;">
                ☁️ Upload File
            </button>
            <button onclick="closeModal(); openMyFiles();" class="btn" style="background: #95a5a6;">
                Cancel
            </button>
        </div>
    `);
    
    // Add file input listener for preview
    setTimeout(() => {
        const fileInput = document.getElementById('uploadFileInput');
        if (fileInput) {
            fileInput.addEventListener('change', function(e) {
                const file = e.target.files[0];
                const preview = document.getElementById('uploadFilePreview');
                
                if (file) {
                    const fileSize = formatFileSize(file.size);
                    const fileType = file.name.split('.').pop().toLowerCase();
                    const icon = getFileTypeIcon(fileType);
                    
                    if (file.size > 10 * 1024 * 1024) {
                        preview.innerHTML = '<span style="color: #e74c3c;">❌ File too large! Maximum 10MB allowed.</span>';
                        fileInput.value = '';
                    } else {
                        preview.innerHTML = `${icon} <strong>${file.name}</strong> (${fileSize})`;
                    }
                }
            });
        }
    }, 100);
}

function generateEmployeeCheckboxes() {
    const employees = Object.entries(authorizedEmployees)
        .filter(([code, emp]) => emp.role === 'employee')
        .sort((a, b) => a[1].name.localeCompare(b[1].name));
    
    return employees.map(([code, emp]) => {
        const categoryBadge = emp.category ? 
            `<span style="background: #ecf0f1; padding: 2px 6px; border-radius: 3px; font-size: 10px; margin-left: 5px;">${emp.category}</span>` : '';
        
        return `
            <label style="display: flex; align-items: center; padding: 8px; margin: 4px 0; cursor: pointer; border-radius: 4px; transition: background 0.2s;"
                   onmouseover="this.style.background='#f8f9fa'"
                   onmouseout="this.style.background='white'">
                <input type="checkbox" class="employee-checkbox" data-empcode="${code}" data-category="${emp.category || 'RAD'}" 
                       onchange="updateSelectedCount()" style="margin-right: 10px; transform: scale(1.2);">
                <span style="flex: 1;">${emp.name} (${code})</span>
                ${categoryBadge}
            </label>
        `;
    }).join('');
}

function toggleAllEmployeesShare() {
    const allCheckbox = document.getElementById('shareWithAll');
    const employeeCheckboxes = document.querySelectorAll('.employee-checkbox');
    
    if (allCheckbox.checked) {
        // Disable individual checkboxes when "All Employees" is checked
        employeeCheckboxes.forEach(cb => {
            cb.checked = false;
            cb.disabled = true;
            cb.parentElement.style.opacity = '0.5';
        });
        document.getElementById('selectedEmployeeCount').textContent = 'All employees will have access';
    } else {
        // Enable individual checkboxes
        employeeCheckboxes.forEach(cb => {
            cb.disabled = false;
            cb.parentElement.style.opacity = '1';
        });
        updateSelectedCount();
    }
}

function selectAllEmployees() {
    const allCheckbox = document.getElementById('shareWithAll');
    if (allCheckbox.checked) return; // Don't select if "All Employees" is checked
    
    document.querySelectorAll('.employee-checkbox').forEach(cb => {
        cb.checked = true;
    });
    updateSelectedCount();
}

function deselectAllEmployees() {
    document.getElementById('shareWithAll').checked = false;
    document.querySelectorAll('.employee-checkbox').forEach(cb => {
        cb.checked = false;
        cb.disabled = false;
        cb.parentElement.style.opacity = '1';
    });
    updateSelectedCount();
}

function selectByRole(category) {
    const allCheckbox = document.getElementById('shareWithAll');
    if (allCheckbox.checked) return; // Don't select if "All Employees" is checked
    
    document.querySelectorAll('.employee-checkbox').forEach(cb => {
        if (cb.dataset.category === category) {
            cb.checked = true;
        }
    });
    updateSelectedCount();
}

function updateSelectedCount() {
    const checked = document.querySelectorAll('.employee-checkbox:checked').length;
    document.getElementById('selectedEmployeeCount').textContent = `${checked} employee${checked !== 1 ? 's' : ''} selected`;
}

async function showSharingDetails(fileId) {
    const allFiles = await getFromFirestore('employee_files');
    const file = allFiles.find(f => f.id === fileId);
    
    if (!file || !file.sharedWith) return;
    
    const sharedEmployees = file.sharedWith
        .filter(code => code !== 'ALL')
        .map(code => {
            const emp = authorizedEmployees[code];
            return emp ? `${emp.name} (${code})` : code;
        })
        .sort()
        .join('<br>');
    
    const modal = createModal(`
        <h3>👥 Shared With</h3>
        <div style="margin: 20px 0;">
            <strong>File:</strong> ${file.originalFileName || file.fileName}
        </div>
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; max-height: 400px; overflow-y: auto;">
            ${sharedEmployees || 'No employees'}
        </div>
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}

async function editFileSharing(fileId) {
    const allFiles = await getFromFirestore('employee_files');
    const file = allFiles.find(f => f.id === fileId);
    
    if (!file) {
        alert('File not found');
        return;
    }
    
    closeModal(); // Close My Files modal
    
    const modal = createModal(`
        <h3>👥 Edit File Sharing</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <strong>File:</strong> ${file.originalFileName || file.fileName}<br>
            <strong>Category:</strong> ${file.category}<br>
            <strong>Uploaded:</strong> ${new Date(file.uploadedDate).toLocaleDateString()}
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 10px; font-weight: 500;">Update Sharing:</label>
            
            <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; border: 1px solid #ddd;">
                <!-- All Employees checkbox -->
                <label style="display: flex; align-items: center; padding: 8px; background: #fff3cd; border-radius: 5px; margin-bottom: 10px; cursor: pointer;">
                    <input type="checkbox" id="shareWithAll" onchange="toggleAllEmployeesShare()" 
                           ${file.sharedWith && file.sharedWith.includes('ALL') ? 'checked' : ''}
                           style="margin-right: 10px; transform: scale(1.3);">
                    <span style="font-weight: bold; color: #856404;">📢 All Employees (Generic File)</span>
                </label>
                
                <!-- Select All / Deselect All -->
                <div style="display: flex; gap: 10px; margin-bottom: 10px; padding: 8px; background: white; border-radius: 5px;">
                    <button onclick="selectAllEmployees()" class="btn" style="flex: 1; background: #3498db; padding: 6px 10px; font-size: 12px;">
                        ✓ Select All
                    </button>
                    <button onclick="deselectAllEmployees()" class="btn" style="flex: 1; background: #95a5a6; padding: 6px 10px; font-size: 12px;">
                        ✗ Deselect All
                    </button>
                </div>
                
                <!-- Role-based bulk selection -->
                <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin-bottom: 10px;">
                    <button onclick="selectByRole('RAD')" class="btn" style="background: #e74c3c; padding: 6px 8px; font-size: 11px;">
                        All RAD
                    </button>
                    <button onclick="selectByRole('TECH')" class="btn" style="background: #f39c12; padding: 6px 8px; font-size: 11px;">
                        All TECH
                    </button>
                    <button onclick="selectByRole('RA')" class="btn" style="background: #9b59b6; padding: 6px 8px; font-size: 11px;">
                        All RA
                    </button>
                    <button onclick="selectByRole('COORD')" class="btn" style="background: #27ae60; padding: 6px 8px; font-size: 11px;">
                        All COORD
                    </button>
                </div>
                
                <!-- Employee list with checkboxes -->
                <div id="employeeCheckboxList" style="max-height: 300px; overflow-y: auto; background: white; padding: 10px; border-radius: 5px; border: 1px solid #ddd;">
                    ${generateEmployeeCheckboxes()}
                </div>
                
                <div style="margin-top: 10px; font-size: 12px; color: #666; text-align: center;">
                    <span id="selectedEmployeeCount">0 employees selected</span>
                </div>
            </div>
        </div>
        
        <div style="text-align: right;">
            <button onclick="saveFileSharing('${fileId}')" class="btn" style="background: #27ae60; margin-right: 10px;">
                💾 Save Changes
            </button>
            <button onclick="closeModal(); openMyFiles();" class="btn" style="background: #95a5a6;">
                Cancel
            </button>
        </div>
    `);
    
    // Pre-select employees after modal loads
    setTimeout(() => {
        if (file.sharedWith && !file.sharedWith.includes('ALL')) {
            file.sharedWith.forEach(empCode => {
                const checkbox = document.querySelector(`.employee-checkbox[data-empcode="${empCode}"]`);
                if (checkbox) checkbox.checked = true;
            });
        }
        
        // If "ALL" is checked, trigger the toggle function
        if (file.sharedWith && file.sharedWith.includes('ALL')) {
            toggleAllEmployeesShare();
        } else {
            updateSelectedCount();
        }
    }, 100);
}

async function saveFileSharing(fileId) {
    const shareWithAll = document.getElementById('shareWithAll').checked;
    
    let sharedWith = [];
    
    if (shareWithAll) {
        sharedWith = ['ALL'];
    } else {
        const checkedBoxes = document.querySelectorAll('.employee-checkbox:checked');
        if (checkedBoxes.length === 0) {
            alert('Please select at least one employee or check "All Employees"');
            return;
        }
        sharedWith = Array.from(checkedBoxes).map(cb => cb.dataset.empcode);
    }
    
    try {
        // Update file sharing in Firestore
        const snapshot = await db.collection('employee_files')
            .where('id', '==', fileId)
            .get();
        
        if (snapshot.empty) {
            alert('File not found');
            return;
        }
        
        await snapshot.docs[0].ref.update({
            sharedWith: sharedWith,
            lastModified: new Date().toISOString()
        });
        
        showNotification('✅ Sharing updated successfully!');
        closeModal();
        openMyFiles();
        
    } catch (error) {
        console.error('Error updating sharing:', error);
        alert('Error updating sharing. Please try again.');
    }
}

async function uploadFileToStorage() {
    const category = document.getElementById('uploadFileCategory').value;
    const fileInput = document.getElementById('uploadFileInput');
    const shareWithAll = document.getElementById('shareWithAll').checked;
    
    if (!fileInput.files[0]) {
        alert('Please select a file to upload');
        return;
    }
    
    // Get selected employees
    let sharedWith = [];
    
    if (shareWithAll) {
        sharedWith = ['ALL'];
    } else {
        const checkedBoxes = document.querySelectorAll('.employee-checkbox:checked');
        if (checkedBoxes.length === 0) {
            alert('Please select at least one employee or check "All Employees"');
            return;
        }
        sharedWith = Array.from(checkedBoxes).map(cb => cb.dataset.empcode);
    }
    
    const file = fileInput.files[0];
    
    // Validate file size
    if (file.size > 10 * 1024 * 1024) {
        alert('File size exceeds 10MB limit');
        return;
    }
    
    // Validate file type
    const allowedTypes = ['pdf', 'doc', 'docx', 'xls', 'xlsx'];
    const fileType = file.name.split('.').pop().toLowerCase();
    
    if (!allowedTypes.includes(fileType)) {
        alert('Invalid file type. Only PDF, Word, and Excel files allowed.');
        return;
    }
    
    try {
        showNotification('⏳ Uploading file...');
        
        // Create storage path (NEW STRUCTURE)
        const timestamp = Date.now();
        const sanitizedFileName = file.name.replace(/[^a-zA-Z0-9._-]/g, '_');
        const storagePath = `shared_files/${category}/${timestamp}_${sanitizedFileName}`;
        
        // Upload to Firebase Storage
        const storageRef = firebase.storage().ref(storagePath);
        const uploadTask = await storageRef.put(file);
        
        // Get download URL
        const downloadURL = await uploadTask.ref.getDownloadURL();
        
        // Save metadata to Firestore
        const fileMetadata = {
            id: `FILE_${timestamp}`,
            fileName: sanitizedFileName,
            originalFileName: file.name, // User-friendly name
            fileType: fileType,
            fileSize: file.size,
            category: category,
            sharedWith: sharedWith, // ARRAY of employee codes or ["ALL"]
            storagePath: storagePath,
            downloadURL: downloadURL,
            uploadedBy: currentUser.code || currentUser.username,
            uploadedByName: currentUser.name,
            uploadedDate: new Date().toISOString(),
            lastModified: new Date().toISOString()
        };
        
        await saveToFirestore('employee_files', fileMetadata);
        
        showNotification('✅ File uploaded successfully!');
        closeModal();
        openMyFiles();
        
    } catch (error) {
        console.error('Error uploading file:', error);
        alert('Error uploading file: ' + error.message);
    }
}

async function viewFile(fileId) {
    try {
        const allFiles = await getFromFirestore('employee_files');
        const file = allFiles.find(f => f.id === fileId);
        
        if (!file) {
            alert('File not found');
            return;
        }
        
        // For PDF, show in modal with embed
        if (file.fileType.toLowerCase() === 'pdf') {
            const modal = createModal(`
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
                    <h3 style="margin: 0;">📄 ${file.fileName}</h3>
                    <button onclick="closeModal(); openMyFiles();" class="btn" style="background: #95a5a6;">Close</button>
                </div>
                <embed src="${file.downloadURL}" type="application/pdf" width="100%" height="600px" style="border-radius: 8px;">
            `);
        } else {
            // For Word/Excel, open in new tab
            window.open(file.downloadURL, '_blank');
        }
        
    } catch (error) {
        console.error('Error viewing file:', error);
        alert('Error viewing file. Please try downloading instead.');
    }
}

async function downloadFile(fileId) {
    try {
        const allFiles = await getFromFirestore('employee_files');
        const file = allFiles.find(f => f.id === fileId);
        
        if (!file) {
            alert('File not found');
            return;
        }
        
        // Create download link
        const link = document.createElement('a');
        link.href = file.downloadURL;
        link.download = file.fileName;
        link.target = '_blank';
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        
        showNotification('⬇️ Downloading ' + file.fileName);
        
    } catch (error) {
        console.error('Error downloading file:', error);
        alert('Error downloading file. Please try again.');
    }
}

async function deleteFile(fileId) {
    if (!confirm('⚠️ Delete this file permanently? This will remove it for all users who have access to it.')) {
        return;
    }
    
    try {
        const allFiles = await getFromFirestore('employee_files');
        const file = allFiles.find(f => f.id === fileId);
        
        if (!file) {
            alert('File not found');
            return;
        }
        
        // Delete from Firebase Storage
        const storageRef = firebase.storage().ref(file.storagePath);
        await storageRef.delete();
        
        // Delete from Firestore
        const snapshot = await db.collection('employee_files').get();
        for (const doc of snapshot.docs) {
            if (doc.data().id === fileId) {
                await doc.ref.delete();
                break;
            }
        }
        
        showNotification('✅ File deleted successfully');
        openMyFiles(); // Refresh the list
        
    } catch (error) {
        console.error('Error deleting file:', error);
        alert('Error deleting file: ' + error.message);
    }
}

function renderFilesTable(files, canDelete, isHR) {
    if (files.length === 0) {
        return '<div style="text-align: center; padding: 60px; color: #666;">📭 No files found</div>';
    }
    
    return `
        <table style="width: 100%; border-collapse: collapse; font-size: 13px; background: white;">
            <thead style="background: #9b59b6; color: white; position: sticky; top: 0;">
                <tr>
                    <th style="padding: 12px; text-align: left;">File Name</th>
                    <th style="padding: 12px; text-align: center;">Type</th>
                    <th style="padding: 12px; text-align: center;">Size</th>
                    <th style="padding: 12px; text-align: center;">Category</th>
                    ${isHR ? '<th style="padding: 12px; text-align: center;">Shared With</th>' : ''}
                    <th style="padding: 12px; text-align: center;">Uploaded By</th>
                    <th style="padding: 12px; text-align: center;">Uploaded On</th>
                    <th style="padding: 12px; text-align: center;">Actions</th>
                </tr>
            </thead>
            <tbody>
                ${files.map(file => {
                    const fileTypeIcon = getFileTypeIcon(file.fileType);
                    const fileSize = formatFileSize(file.fileSize);
                    // Calculate sharing info
						let sharingInfo = '';
						if (file.sharedWith) {
							if (file.sharedWith.includes('ALL')) {
								sharingInfo = '<span style="background: #fff3cd; color: #856404; padding: 4px 10px; border-radius: 4px; font-size: 11px; font-weight: bold;">📢 All Employees</span>';
							} else {
								const count = file.sharedWith.length;
								sharingInfo = `
									<span style="background: #e3f2fd; color: #1976d2; padding: 4px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; cursor: pointer;"
										  onclick="showSharingDetails('${file.id}')">
										👥 ${count} employee${count !== 1 ? 's' : ''}
									</span>
								`;
							}
						}
                    
                    return `
                        <tr style="border-bottom: 1px solid #ecf0f1;">
                            <td style="padding: 12px;">
                                ${fileTypeIcon} ${file.fileName}
                            </td>
                            <td style="padding: 12px; text-align: center;">
                                <span style="background: #ecf0f1; padding: 3px 8px; border-radius: 3px; font-size: 11px; font-weight: bold;">
                                    ${file.fileType.toUpperCase()}
                                </span>
                            </td>
                            <td style="padding: 12px; text-align: center;">${fileSize}</td>
                            <td style="padding: 12px; text-align: center;">
                                <span style="background: ${file.category === 'personal' ? '#e3f2fd' : '#fff3cd'}; 
                                             color: ${file.category === 'personal' ? '#1976d2' : '#f57c00'}; 
                                             padding: 4px 10px; border-radius: 4px; font-size: 11px; font-weight: bold;">
                                    ${file.category.toUpperCase()}
                                </span>
                            </td>
                            ${isHR ? `<td style="padding: 12px; text-align: center;">${sharingInfo}</td>` : ''}
                            <td style="padding: 12px; text-align: center;">${file.uploadedByName}</td>
                            <td style="padding: 12px; text-align: center;">
                                ${new Date(file.uploadedDate).toLocaleDateString('en-US', { year: 'numeric', month: 'short', day: 'numeric' })}
                            </td>
                            <td style="padding: 12px; text-align: center;">
								${canDelete ? `
								<button onclick="editFileSharing('${file.id}')" class="btn" style="background: #9b59b6; padding: 6px 12px; font-size: 11px; margin: 2px;">
									👥 Edit Sharing
								</button>
								` : ''}
								<button onclick="viewFile('${file.id}')" class="btn" style="background: #3498db; padding: 6px 12px; font-size: 11px; margin: 2px;">
									👁️ View
								</button>
                                <button onclick="downloadFile('${file.id}')" class="btn" style="background: #27ae60; padding: 6px 12px; font-size: 11px; margin: 2px;">
                                    ⬇️ Download
                                </button>
                                ${canDelete ? `
                                <button onclick="deleteFile('${file.id}')" class="btn" style="background: #e74c3c; padding: 6px 12px; font-size: 11px; margin: 2px;">
                                    🗑️ Delete
                                </button>
                                ` : ''}
                            </td>
                        </tr>
                    `;
                }).join('')}
            </tbody>
        </table>
    `;
}

function getFileTypeIcon(fileType) {
    const icons = {
        'pdf': '📄',
        'docx': '📝',
        'doc': '📝',
        'xlsx': '📊',
        'xls': '📊'
    };
    return icons[fileType.toLowerCase()] || '📎';
}

function formatFileSize(bytes) {
    if (bytes === 0) return '0 Bytes';
    const k = 1024;
    const sizes = ['Bytes', 'KB', 'MB', 'GB'];
    const i = Math.floor(Math.log(bytes) / Math.log(k));
    return Math.round(bytes / Math.pow(k, i) * 100) / 100 + ' ' + sizes[i];
}

function filterMyFiles() {
    const searchTerm = document.getElementById('fileSearchInput').value.toLowerCase();
    const categoryFilter = document.getElementById('fileCategoryFilter').value;
    const employeeFilter = document.getElementById('fileEmployeeFilter') ? 
                          document.getElementById('fileEmployeeFilter').value : '';
    
    let filtered = window.currentFilesData.filter(file => {
        const matchesSearch = file.fileName.toLowerCase().includes(searchTerm);
        const matchesCategory = !categoryFilter || file.category === categoryFilter;
        const matchesEmployee = !employeeFilter || file.empCode === employeeFilter;
        
        return matchesSearch && matchesCategory && matchesEmployee;
    });
    
    document.getElementById('myFilesContainer').innerHTML = 
        renderFilesTable(filtered, window.canDeleteFiles, window.isHRView);
}

//==============================
//TICKET SYSTEM
//==================================

async function openTicketModal() {
    const modal = createModal(`
        <h3>Report an Issue</h3>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Issue Type:</label>
            <select id="ticketType" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="bug">Bug/Error</option>
                <option value="template">Template Issue</option>
                <option value="access">Access Problem</option>
                <option value="feature">Feature Request</option>
                <option value="other">Other</option>
            </select>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Priority:</label>
            <select id="ticketPriority" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="low">Low - Can wait</option>
                <option value="medium">Medium - Soon as possible</option>
                <option value="high">High - Blocking my work</option>
            </select>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Description:</label>
            <textarea id="ticketDescription" rows="6" placeholder="Please describe the issue in detail..."
                style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: inherit;"></textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="submitTicket()" class="btn" style="background: #27ae60; margin-right: 10px;">Submit Ticket</button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Cancel</button>
        </div>
    `);
}

async function submitTicket() {
    const type = document.getElementById('ticketType').value;
    const priority = document.getElementById('ticketPriority').value;
    const description = document.getElementById('ticketDescription').value.trim();
    
    if (!description) {
        alert('Please describe the issue');
        return;
    }
    
    try {
        const ticket = {
            id: 'TICKET_' + Date.now(),
            type: type,
            priority: priority,
            description: description,
            submittedBy: currentUser.name,
            submitterCode: currentUser.code,
            submittedDate: new Date().toISOString(),
            status: 'open',
            adminResponse: '',
            closedDate: ''
        };
        
        await saveToFirestore('support_tickets', ticket);
        
        showNotification('Ticket submitted successfully!');
        closeModal();
        
    } catch (error) {
        console.error('Error submitting ticket:', error);
        alert('Error submitting ticket. Please try again.');
    }
}

async function loadTickets(filter = 'open') {
    const tickets = await getFromFirestore('support_tickets');
    
    let filteredTickets = tickets;
    if (filter !== 'all') {
        filteredTickets = tickets.filter(t => t.status === filter);
    }
    
    filteredTickets.sort((a, b) => new Date(b.submittedDate) - new Date(a.submittedDate));
    
    const container = document.getElementById('ticketsContainer');
    
    if (filteredTickets.length === 0) {
        container.innerHTML = '<div style="text-align: center; padding: 40px; color: #666;">No tickets found</div>';
        return;
    }
    
    const priorityColors = {
        low: '#3498db',
        medium: '#f39c12',
        high: '#e74c3c'
    };
    
    const statusColors = {
        open: '#e74c3c',
        'in-progress': '#f39c12',
        closed: '#27ae60'
    };
    
    const html = filteredTickets.map(ticket => `
        <div style="background: white; border: 2px solid ${statusColors[ticket.status]}; border-radius: 8px; padding: 15px; margin-bottom: 15px;">
            <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                <div>
                    <span style="background: ${priorityColors[ticket.priority]}; color: white; padding: 4px 8px; border-radius: 4px; font-size: 11px; font-weight: bold;">
                        ${ticket.priority.toUpperCase()}
                    </span>
                    <span style="background: #ecf0f1; padding: 4px 8px; border-radius: 4px; font-size: 11px; margin-left: 5px;">
                        ${ticket.type}
                    </span>
                </div>
                <div style="font-size: 12px; color: #666;">
                    ${new Date(ticket.submittedDate).toLocaleString()}
                </div>
            </div>
            
            <div style="font-weight: bold; margin-bottom: 5px;">
                ${ticket.submittedBy} (${ticket.submitterCode})
            </div>
            
            <div style="background: #f8f9fa; padding: 10px; border-radius: 5px; margin-bottom: 10px; white-space: pre-wrap;">
                ${ticket.description}
            </div>
            
            ${ticket.adminResponse ? `
                <div style="background: #e8f5e9; padding: 10px; border-radius: 5px; margin-bottom: 10px; border-left: 3px solid #27ae60;">
                    <strong>Admin Response:</strong><br>
                    ${ticket.adminResponse}
                </div>
            ` : ''}
            
            <div style="display: flex; gap: 10px;">
                ${ticket.status !== 'closed' ? `
                    <button onclick="respondToTicket('${ticket.id}')" class="btn" style="background: #3498db; font-size: 12px;">Respond</button>
                    ${ticket.status === 'open' ? `
                        <button onclick="updateTicketStatus('${ticket.id}', 'in-progress')" class="btn" style="background: #f39c12; font-size: 12px;">Mark In Progress</button>
                    ` : ''}
                    <button onclick="closeTicket('${ticket.id}')" class="btn" style="background: #27ae60; font-size: 12px;">Close Ticket</button>
                ` : `
                    <span style="color: #27ae60; font-weight: bold;">✓ Closed on ${new Date(ticket.closedDate).toLocaleDateString()}</span>
                `}
                <button onclick="deleteTicket('${ticket.id}')" class="btn" style="background: #e74c3c; font-size: 12px;">Delete</button>
            </div>
        </div>
    `).join('');
    
    container.innerHTML = html;
    updateTicketCounts(tickets);
}

async function respondToTicket(ticketId) {
    const tickets = await getFromFirestore('support_tickets');
    const ticket = tickets.find(t => t.id === ticketId);
    
    const modal = createModal(`
        <h3>Respond to Ticket</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 5px; margin-bottom: 20px;">
            <strong>Issue:</strong> ${ticket.description}
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Your Response:</label>
            <textarea id="adminResponse" rows="6" placeholder="Explain what you did to fix the issue..."
                style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">${ticket.adminResponse || ''}</textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="saveTicketResponse('${ticketId}')" class="btn" style="background: #27ae60; margin-right: 10px;">Save Response</button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Cancel</button>
        </div>
    `);
}

async function saveTicketResponse(ticketId) {
    const response = document.getElementById('adminResponse').value.trim();
    
    if (!response) {
        alert('Please enter a response');
        return;
    }
    
    try {
        await updateFirestoreDoc('support_tickets', ticketId, {
            adminResponse: response,
            status: 'in-progress'
        });
        
        showNotification('Response saved!');
        closeModal();
        loadTickets();
        
    } catch (error) {
        console.error('Error saving response:', error);
    }
}

async function updateTicketStatus(ticketId, status) {
    try {
        await updateFirestoreDoc('support_tickets', ticketId, { status: status });
        showNotification('Status updated');
        loadTickets();
    } catch (error) {
        console.error('Error updating status:', error);
    }
}

async function closeTicket(ticketId) {
    if (!confirm('Close this ticket?')) return;
    
    try {
        await updateFirestoreDoc('support_tickets', ticketId, {
            status: 'closed',
            closedDate: new Date().toISOString()
        });
        
        showNotification('Ticket closed');
        loadTickets();
        
    } catch (error) {
        console.error('Error closing ticket:', error);
    }
}

async function deleteTicket(ticketId) {
    if (!confirm('Delete this ticket permanently?')) return;
    
    try {
        const snapshot = await db.collection('support_tickets').get();
        snapshot.forEach(async (doc) => {
            if (doc.data().id === ticketId) {
                await doc.ref.delete();
            }
        });
        
        showNotification('Ticket deleted');
        loadTickets();
        
    } catch (error) {
        console.error('Error deleting ticket:', error);
    }
}

function filterTickets(status) {
    loadTickets(status);
}

function updateTicketCounts(tickets) {
    const open = tickets.filter(t => t.status === 'open').length;
    const inProgress = tickets.filter(t => t.status === 'in-progress').length;
    const closed = tickets.filter(t => t.status === 'closed').length;
    
    document.getElementById('openTicketsCount').textContent = open;
    document.getElementById('progressTicketsCount').textContent = inProgress;
    document.getElementById('closedTicketsCount').textContent = closed;
}

async function loadUserTicketNotifications() {
    if (currentUser.role !== 'employee') return;
    
    const tickets = await getFromFirestore('support_tickets');
    const userTickets = tickets.filter(t => 
        t.submitterCode === currentUser.code && 
        (t.status === 'closed' || t.adminResponse)
    );
    
    const toolsTicketBadge = document.getElementById('toolsTicketBadge');
    if (toolsTicketBadge && userTickets.length > 0) {
        toolsTicketBadge.textContent = userTickets.length;
        toolsTicketBadge.style.display = 'inline';
    }
}

// ==============================================
// DATA MANAGEMENT FUNCTIONS
// ==============================================

async function viewAllQAReports() {
    const qaData = await getFromFirestore('qa_assignments');
    
    const modal = createModal(`
        <h3>All QA Reports (${qaData.length} total)</h3>
        <div style="max-height: 500px; overflow-y: auto;">
            <table style="width: 100%; border-collapse: collapse; font-size: 12px;">
                <thead style="position: sticky; top: 0; background: #34495e; color: white;">
                    <tr>
                        <th style="padding: 8px; text-align: left;">Date</th>
                        <th style="padding: 8px; text-align: left;">Employee</th>
                        <th style="padding: 8px; text-align: left;">Case</th>
                        <th style="padding: 8px; text-align: center;">Status</th>
                        <th style="padding: 8px; text-align: center;">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    ${qaData.map(qa => `
                        <tr style="border-bottom: 1px solid #ddd;">
                            <td style="padding: 8px;">${new Date(qa.createdDate).toLocaleDateString()}</td>
                            <td style="padding: 8px;">${authorizedEmployees[qa.assignedTo]?.name || qa.assignedTo}</td>
                            <td style="padding: 8px;">${qa.caseDetails}</td>
                            <td style="padding: 8px; text-align: center;">${qa.status}</td>
                            <td style="padding: 8px; text-align: center;">
                                <button onclick="deleteSingleQA('${qa.id}')" style="background: #e74c3c; color: white; border: none; padding: 4px 8px; border-radius: 3px; cursor: pointer; font-size: 11px;">Delete</button>
                            </td>
                        </tr>
                    `).join('')}
                </tbody>
            </table>
        </div>
        <div style="text-align: right; margin-top: 15px;">
            <button onclick="closeModal()" class="btn">Close</button>
        </div>
    `);
    
    updateDataCounts();
}

async function viewAllPeerReviews() {
    const peerData = await getFromFirestore('peer_review_assignments');
    
    const modal = createModal(`
        <h3>All Peer Reviews (${peerData.length} total)</h3>
        <div style="max-height: 500px; overflow-y: auto;">
            <table style="width: 100%; border-collapse: collapse; font-size: 12px;">
                <thead style="position: sticky; top: 0; background: #34495e; color: white;">
                    <tr>
                        <th style="padding: 8px; text-align: left;">Date</th>
                        <th style="padding: 8px; text-align: left;">Reviewer</th>
                        <th style="padding: 8px; text-align: left;">Accession</th>
                        <th style="padding: 8px; text-align: center;">Status</th>
                        <th style="padding: 8px; text-align: center;">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    ${peerData.map(peer => `
                        <tr style="border-bottom: 1px solid #ddd;">
                            <td style="padding: 8px;">${new Date(peer.assignedDate).toLocaleDateString()}</td>
                            <td style="padding: 8px;">${authorizedEmployees[peer.assignedTo]?.name || peer.assignedTo}</td>
                            <td style="padding: 8px;">${peer.accession}</td>
                            <td style="padding: 8px; text-align: center;">${peer.status}</td>
                            <td style="padding: 8px; text-align: center;">
                                <button onclick="deleteSinglePeer('${peer.id}')" style="background: #e74c3c; color: white; border: none; padding: 4px 8px; border-radius: 3px; cursor: pointer; font-size: 11px;">Delete</button>
                            </td>
                        </tr>
                    `).join('')}
                </tbody>
            </table>
        </div>
        <div style="text-align: right; margin-top: 15px;">
            <button onclick="closeModal()" class="btn">Close</button>
        </div>
    `);
    
    updateDataCounts();
}

async function deleteSingleQA(qaId) {
    if (!confirm('Delete this QA report permanently?')) return;
    
    try {
        const snapshot = await db.collection('qa_assignments').get();
        snapshot.forEach(async (doc) => {
            if (doc.data().id === qaId) {
                await doc.ref.delete();
            }
        });
        
        showNotification('QA report deleted');
        viewAllQAReports();
        
    } catch (error) {
        console.error('Error deleting QA:', error);
        showNotification('Error deleting QA report');
    }
}

async function deleteSinglePeer(peerId) {
    if (!confirm('Delete this peer review permanently?')) return;
    
    try {
        const snapshot = await db.collection('peer_review_assignments').get();
        snapshot.forEach(async (doc) => {
            if (doc.data().id === peerId) {
                await doc.ref.delete();
            }
        });
        
        showNotification('Peer review deleted');
        viewAllPeerReviews();
        
    } catch (error) {
        console.error('Error deleting peer review:', error);
        showNotification('Error deleting peer review');
    }
}

async function deleteCompletedQA() {
    if (!confirm('Delete ALL completed QA reports? This cannot be undone!')) return;
    
    try {
        const qaData = await getFromFirestore('qa_assignments');
        const completedQAs = qaData.filter(qa => qa.status === 'Completed');
        
        const batch = db.batch();
        const snapshot = await db.collection('qa_assignments').get();
        
        snapshot.forEach((doc) => {
            if (doc.data().status === 'Completed') {
                batch.delete(doc.ref);
            }
        });
        
        await batch.commit();
        showNotification(`Deleted ${completedQAs.length} completed QA reports`);
        updateDataCounts();
        
    } catch (error) {
        console.error('Error deleting completed QAs:', error);
        showNotification('Error deleting QA reports');
    }
}

async function deleteCompletedPeer() {
    if (!confirm('Delete ALL completed peer reviews? This cannot be undone!')) return;
    
    try {
        const peerData = await getFromFirestore('peer_review_assignments');
        const completedPeers = peerData.filter(p => p.status === 'Completed');
        
        const batch = db.batch();
        const snapshot = await db.collection('peer_review_assignments').get();
        
        snapshot.forEach((doc) => {
            if (doc.data().status === 'Completed') {
                batch.delete(doc.ref);
            }
        });
        
        await batch.commit();
        showNotification(`Deleted ${completedPeers.length} completed peer reviews`);
        updateDataCounts();
        
    } catch (error) {
        console.error('Error deleting completed peer reviews:', error);
        showNotification('Error deleting peer reviews');
    }
}

async function deleteOldQA() {
    if (!confirm('Delete QA reports older than 6 months? This cannot be undone!')) return;
    
    try {
        const sixMonthsAgo = new Date();
        sixMonthsAgo.setMonth(sixMonthsAgo.getMonth() - 6);
        
        const qaData = await getFromFirestore('qa_assignments');
        const oldQAs = qaData.filter(qa => new Date(qa.createdDate) < sixMonthsAgo);
        
        const batch = db.batch();
        const snapshot = await db.collection('qa_assignments').get();
        
        snapshot.forEach((doc) => {
            if (new Date(doc.data().createdDate) < sixMonthsAgo) {
                batch.delete(doc.ref);
            }
        });
        
        await batch.commit();
        showNotification(`Deleted ${oldQAs.length} old QA reports`);
        updateDataCounts();
        
    } catch (error) {
        console.error('Error deleting old QAs:', error);
        showNotification('Error deleting QA reports');
    }
}

async function deleteOldPeer() {
    if (!confirm('Delete peer reviews older than 6 months? This cannot be undone!')) return;
    
    try {
        const sixMonthsAgo = new Date();
        sixMonthsAgo.setMonth(sixMonthsAgo.getMonth() - 6);
        
        const peerData = await getFromFirestore('peer_review_assignments');
        const oldPeers = peerData.filter(p => new Date(p.assignedDate) < sixMonthsAgo);
        
        const batch = db.batch();
        const snapshot = await db.collection('peer_review_assignments').get();
        
        snapshot.forEach((doc) => {
            if (new Date(doc.data().assignedDate) < sixMonthsAgo) {
                batch.delete(doc.ref);
            }
        });
        
        await batch.commit();
        showNotification(`Deleted ${oldPeers.length} old peer reviews`);
        updateDataCounts();
        
    } catch (error) {
        console.error('Error deleting old peer reviews:', error);
        showNotification('Error deleting peer reviews');
    }
}

async function deleteAllQA() {
    const confirmation = prompt('Type "DELETE ALL QA" to confirm permanent deletion of ALL QA reports:');
    if (confirmation !== 'DELETE ALL QA') {
        showNotification('Deletion cancelled');
        return;
    }
    
    try {
        const batch = db.batch();
        const snapshot = await db.collection('qa_assignments').get();
        
        snapshot.forEach((doc) => {
            batch.delete(doc.ref);
        });
        
        await batch.commit();
        showNotification(`Deleted ${snapshot.size} QA reports`);
        updateDataCounts();
        
    } catch (error) {
        console.error('Error deleting all QAs:', error);
        showNotification('Error deleting QA reports');
    }
}

async function deleteAllPeer() {
    const confirmation = prompt('Type "DELETE ALL PEER" to confirm permanent deletion of ALL peer reviews:');
    if (confirmation !== 'DELETE ALL PEER') {
        showNotification('Deletion cancelled');
        return;
    }
    
    try {
        const batch = db.batch();
        const snapshot = await db.collection('peer_review_assignments').get();
        
        snapshot.forEach((doc) => {
            batch.delete(doc.ref);
        });
        
        await batch.commit();
        showNotification(`Deleted ${snapshot.size} peer reviews`);
        updateDataCounts();
        
    } catch (error) {
        console.error('Error deleting all peer reviews:', error);
        showNotification('Error deleting peer reviews');
    }
}

async function viewAllNotes() {
    const allNotes = await getFromFirestore('notes_board');
    
    document.getElementById('totalNotesCount').textContent = allNotes.length;
    
    const modal = createModal(`
        <h3>All Notes (${allNotes.length} total)</h3>
        <div style="max-height: 500px; overflow-y: auto;">
            <table style="width: 100%; border-collapse: collapse; font-size: 12px;">
                <thead style="position: sticky; top: 0; background: #34495e; color: white;">
                    <tr>
                        <th style="padding: 8px; text-align: left;">Date</th>
                        <th style="padding: 8px; text-align: left;">Author</th>
                        <th style="padding: 8px; text-align: center;">Category</th>
                        <th style="padding: 8px; text-align: left;">Content</th>
                        <th style="padding: 8px; text-align: center;">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    ${allNotes.map(note => `
                        <tr style="border-bottom: 1px solid #ddd;">
                            <td style="padding: 8px;">${new Date(note.timestamp).toLocaleDateString()}</td>
                            <td style="padding: 8px;">${note.createdByName}</td>
                            <td style="padding: 8px; text-align: center;">
                                <span class="note-category ${note.category}">${note.category === 'review' ? 'REVIEW' : 'OTHER'}</span>
                            </td>
                            <td style="padding: 8px; max-width: 300px; white-space: pre-wrap;">${escapeHtml(note.content.substring(0, 100))}${note.content.length > 100 ? '...' : ''}</td>
                            <td style="padding: 8px; text-align: center;">
                                <button onclick="deleteSingleNote('${note.id}')" style="background: #e74c3c; color: white; border: none; padding: 4px 8px; border-radius: 3px; cursor: pointer; font-size: 11px;">Delete</button>
                            </td>
                        </tr>
                    `).join('')}
                </tbody>
            </table>
        </div>
        <div style="text-align: right; margin-top: 15px;">
            <button onclick="closeModal()" class="btn">Close</button>
        </div>
    `);
}

async function deleteSingleNote(noteId) {
    if (!confirm('Delete this note permanently?')) return;
    
    try {
        const snapshot = await db.collection('notes_board').get();
        snapshot.forEach(async (doc) => {
            if (doc.data().id === noteId) {
                await doc.ref.delete();
            }
        });
        
        showNotification('Note deleted');
        viewAllNotes();
        
    } catch (error) {
        console.error('Error deleting note:', error);
    }
}

async function deleteOldNotes() {
    if (!confirm('Delete notes older than 6 months? This cannot be undone!')) return;
    
    try {
        const sixMonthsAgo = new Date();
        sixMonthsAgo.setMonth(sixMonthsAgo.getMonth() - 6);
        
        const allNotes = await getFromFirestore('notes_board');
        const oldNotes = allNotes.filter(n => new Date(n.timestamp) < sixMonthsAgo);
        
        const snapshot = await db.collection('notes_board').get();
        const deletePromises = [];
        
        snapshot.forEach((doc) => {
            if (new Date(doc.data().timestamp) < sixMonthsAgo) {
                deletePromises.push(doc.ref.delete());
            }
        });
        
        await Promise.all(deletePromises);
        
        showNotification(`Deleted ${oldNotes.length} old notes`);
        viewAllNotes();
        
    } catch (error) {
        console.error('Error deleting old notes:', error);
    }
}

async function updateDataCounts() {
    const qaData = await getFromFirestore('qa_assignments');
    const peerData = await getFromFirestore('peer_review_assignments');
    
    const qaCountEl = document.getElementById('totalQAReports');
    const peerCountEl = document.getElementById('totalPeerReviews');
    
    if (qaCountEl) qaCountEl.textContent = qaData.length;
    if (peerCountEl) peerCountEl.textContent = peerData.length;
}

// ==============================================
// INTERESTING CASES
// ==============================================

async function exportQAData() {
    try {
        // ✅ FIX: Export filteredQAData instead of fetching all
        if (filteredQAData.length === 0) {
            alert('No QA data to export. Please adjust your filters.');
            return;
        }
        
        const csvContent = convertQAToCSV(filteredQAData); // ✅ Use filtered data
        downloadCSV(csvContent, `qa_data_${new Date().toISOString().split('T')[0]}.csv`);
        showNotification(`✓ Exported ${filteredQAData.length} QA records`);
    } catch (error) {
        console.error('Error exporting QA data:', error);
        showNotification('Error exporting data.');
    }
}

function convertQAToCSV(qaData) {
    if (qaData.length === 0) return '';
    
    const headers = ['QA ID', 'Radiologist', 'Case Details', 'Hospital', 'Accession', 'Modality', 'Due Date', 'Status', 'QA Grade', 'Received Date', 'Responded Date', 'Report', 'Entry Type', 'Response Source', 'Entered By'];
    
    const rows = qaData.map(qa => {
        const employee = authorizedEmployees[qa.assignedTo];
        const employeeName = employee ? employee.name : qa.assignedTo;
        
        // ✅ CLEAN all text fields properly
        const cleanText = (text) => {
            return (text || '')
                .replace(/"/g, '""')      // Escape quotes
                .replace(/\n/g, ' ')      // Remove line breaks
                .replace(/\r/g, ' ')      // Remove carriage returns
                .replace(/,/g, ';')       // Replace commas with semicolons
                .trim();
        };
        
        return [
            qa.id,
            `${employeeName} (${qa.assignedTo})`,
            `"${cleanText(qa.caseDetails)}"`,
            `"${cleanText(qa.hospitalName)}"`,
            qa.accessionNo || '',
            qa.modality || '',
            qa.dueDate,
            qa.status,
            qa.qaGrade || '',
            qa.qaReceivedDate || '',
            qa.qaRespondedDate || '',
            `"${cleanText(qa.report)}"`,
            qa.entryType || 'SELF',
            qa.responseSource || '-',
            qa.enteredBy || qa.assignedTo
        ];
    });
    
    return [headers.join(','), ...rows.map(row => row.join(','))].join('\n');
}

function downloadCSV(csvContent, filename) {
    // ✅ ADD BOM for proper UTF-8 support in Excel
    const BOM = '\uFEFF';
    const blob = new Blob([BOM + csvContent], { type: 'text/csv;charset=utf-8;' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    window.URL.revokeObjectURL(url);
}

// ==============================================
// VOICE INPUT SYSTEM
// ==============================================

function toggleMic() {
    const micBtn = document.getElementById('micBtn') || document.getElementById('hrMicBtn');
    const micStatus = document.getElementById('micStatus') || document.getElementById('hrMicStatus');
    
    if (!isListening) {
        if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            const recognition = new SpeechRecognition();
            
            recognition.continuous = true;
            recognition.interimResults = true;
            
            recognition.onresult = function(event) {
                const transcript = event.results[event.results.length - 1][0].transcript.toLowerCase().trim();
                
                if (event.results[event.results.length - 1].isFinal) {
                    processVoiceCommand(transcript);
                }
            };
            
            recognition.onerror = function() {
                isListening = false;
                if (micBtn) micBtn.classList.remove('active');
                if (micStatus) micStatus.textContent = 'Voice Error';
            };
            
            recognition.onend = function() {
                isListening = false;
                if (micBtn) micBtn.classList.remove('active');
                if (micStatus) micStatus.textContent = 'Voice Ready';
            };
            
            recognition.start();
            isListening = true;
            if (micBtn) micBtn.classList.add('active');
            if (micStatus) micStatus.textContent = 'Listening...';
            window.currentRecognition = recognition;
        } else {
            updateStatus('Voice recognition not supported');
        }
    } else {
        if (window.currentRecognition) {
            window.currentRecognition.stop();
        }
        isListening = false;
        if (micBtn) micBtn.classList.remove('active');
        if (micStatus) micStatus.textContent = 'Voice Ready';
    }
}

		function processVoiceCommand(transcript) {
    const command = transcript.toLowerCase().trim();
    
    // 1. TEMPLATE LOADING - CHECK FIRST
    if (command.startsWith('load ')) {
        const phrase = command.replace('load ', '').trim();
        voiceLoadTemplate(phrase);
        return;
    }
    
    // 2. REPORT NAVIGATION COMMANDS
    const editor = document.getElementById('textEditor');
    const editorText = editor.textContent || editor.innerText || '';
    
    // Go to specific sections
    if (command.includes('go to findings') || command.includes('goto findings')) {
        moveCursorToSection('FINDINGS:');
        showVoiceFeedback('Moving to FINDINGS');
        return;
    }
    
    if (command.includes('go to impression') || command.includes('goto impression')) {
        moveCursorToSection('IMPRESSION:');
        showVoiceFeedback('Moving to IMPRESSION');
        return;
    }
    
    if (command.includes('go to comparison') || command.includes('goto comparison')) {
        moveCursorToSection('COMPARISON:');
        showVoiceFeedback('Moving to COMPARISON');
        return;
    }
    
    if (command.includes('go to technique') || command.includes('goto technique')) {
        moveCursorToSection('TECHNIQUE:');
        showVoiceFeedback('Moving to TECHNIQUE');
        return;
    }
    
    if (command.includes('go to clinical history') || command.includes('goto clinical history') || command.includes('go to history')) {
        moveCursorToSection('CLINICAL HISTORY:');
        showVoiceFeedback('Moving to CLINICAL HISTORY');
        return;
    }
    
    if (command.includes('go to recommendation') || command.includes('goto recommendation')) {
        moveCursorToSection('RECOMMENDATION:');
        showVoiceFeedback('Moving to RECOMMENDATION');
        return;
    }
    
    // 3. FILL-IN-THE-BLANK COMMANDS
    if (command.includes('fill blank') || command.includes('fill in blank') || command.includes('next blank')) {
        findAndFillNextBlank();
        return;
    }
    
    // 4. PUNCTUATION & FORMATTING
    if (command === 'comma' || command === 'coma') {
        insertTextAtCursor(', ');
        return;
    }
    
    if (command === 'period' || command === 'full stop') {
        insertTextAtCursor('. ');
        return;
    }
    
    if (command === 'new line' || command === 'next line') {
        insertTextAtCursor('\n');
        return;
    }
    
    if (command === 'new paragraph' || command === 'next paragraph') {
        insertTextAtCursor('\n\n');
        return;
    }
    
    if (command === 'colon') {
        insertTextAtCursor(': ');
        return;
    }
    
    if (command === 'semicolon') {
        insertTextAtCursor('; ');
        return;
    }
    
    if (command === 'question mark') {
        insertTextAtCursor('? ');
        return;
    }
    
    if (command === 'exclamation mark' || command === 'exclamation point') {
        insertTextAtCursor('! ');
        return;
    }
    
    // 5. SPECIAL FORMATTING
    if (command === 'dash' || command === 'underscore blank') {
        insertTextAtCursor('____');
        return;
    }
    
    if (command === 'blank' || command === 'fill in') {
        insertTextAtCursor('____');
        return;
    }
    
    if (command === 'bullet point') {
        insertTextAtCursor('\n• ');
        return;
    }
    
    if (command === 'number' || command === 'numbered list') {
        insertTextAtCursor('\n1. ');
        return;
    }
    
    // 6. CONTRAST PHRASES (COMMON IN RADIOLOGY)
    if (command.includes('with contrast') || command.includes('with intravenous contrast')) {
        insertTextAtCursor('with intravenous contrast');
        return;
    }
    
    if (command.includes('without contrast') || command.includes('without intravenous contrast')) {
        insertTextAtCursor('without intravenous contrast');
        return;
    }
    
    if (command.includes('with and without contrast')) {
        insertTextAtCursor('with and without intravenous contrast');
        return;
    }
    
    // 7. COMMON RADIOLOGY PHRASES
    if (command.includes('no acute') || command.includes('no acute abnormality')) {
        insertTextAtCursor('No acute abnormality identified. ');
        return;
    }
    
    if (command.includes('within normal limits') || command.includes('normal limits')) {
        insertTextAtCursor('within normal limits');
        return;
    }
    
    if (command.includes('unremarkable')) {
        insertTextAtCursor('unremarkable');
        return;
    }
    
    // 8. EDITOR ACTIONS
    if (command.includes('format')) {
        formatReport();
        showVoiceFeedback('Report formatted');
        return;
    }
    
    if (command.includes('copy')) {
        copyToClipboard();
        showVoiceFeedback('Copied to clipboard');
        return;
    }
    
    if (command.includes('clear')) {
        if (confirm('Clear editor?')) {
            clearEditor();
            showVoiceFeedback('Editor cleared');
        }
        return;
    }
    
    // 9. GENDER COMMANDS
    if (command.includes('male patient')) {
        selectGender('male');
        showVoiceFeedback('Set to male patient');
        return;
    }
    
    if (command.includes('female patient')) {
        selectGender('female');
        showVoiceFeedback('Set to female patient');
        return;
    }
    
    // 10. UNDO LAST ENTRY
    if (command === 'undo' || command === 'delete that' || command === 'scratch that') {
        document.execCommand('undo');
        showVoiceFeedback('Undone');
        return;
    }
    
    // 11. DEFAULT: INSERT AS TEXT
    insertTextAtCursor(transcript + ' ');
    detectCriticalFindings();
}

		function moveCursorToSection(sectionName) {
    const editor = document.getElementById('textEditor');
    const text = editor.textContent || editor.innerText || '';
    
    // Find section position
    const sectionIndex = text.toUpperCase().indexOf(sectionName.toUpperCase());
    
    if (sectionIndex === -1) {
        showVoiceFeedback(`Section ${sectionName} not found`);
        return;
    }
    
    // Create range and selection
    const range = document.createRange();
    const selection = window.getSelection();
    
    // Find the text node containing the section
    let currentPos = 0;
    let targetNode = null;
    let targetOffset = 0;
    
    function findTextNode(node) {
        if (node.nodeType === Node.TEXT_NODE) {
            const nodeLength = node.textContent.length;
            if (currentPos + nodeLength >= sectionIndex + sectionName.length) {
                targetNode = node;
                targetOffset = sectionIndex + sectionName.length - currentPos;
                return true;
            }
            currentPos += nodeLength;
        } else {
            for (let child of node.childNodes) {
                if (findTextNode(child)) return true;
            }
        }
        return false;
    }
    
    findTextNode(editor);
    
    if (targetNode) {
        // Move cursor to end of section heading
        range.setStart(targetNode, Math.min(targetOffset, targetNode.textContent.length));
        range.collapse(true);
        selection.removeAllRanges();
        selection.addRange(range);
        
        // Add a space if needed
        if (targetNode.textContent[targetOffset] !== ' ' && targetNode.textContent[targetOffset] !== '\n') {
            insertTextAtCursor(' ');
        }
        
        editor.focus();
    }
}

		function findAndFillNextBlank() {
    const editor = document.getElementById('textEditor');
    const text = editor.textContent || editor.innerText || '';
    
    // Find next blank (____) after current cursor position
    const selection = window.getSelection();
    let currentPos = 0;
    
    if (selection.rangeCount > 0) {
        const range = selection.getRangeAt(0);
        currentPos = getCaretPosition(editor);
    }
    
    // Find next occurrence of ____
    const blankIndex = text.indexOf('____', currentPos);
    
    if (blankIndex === -1) {
        // No more blanks, search from beginning
        const firstBlank = text.indexOf('____');
        if (firstBlank === -1) {
            showVoiceFeedback('No blanks found in report');
            return;
        }
        moveToBlank(firstBlank);
    } else {
        moveToBlank(blankIndex);
    }
}

function moveToBlank(blankPosition) {
    const editor = document.getElementById('textEditor');
    const range = document.createRange();
    const selection = window.getSelection();
    
    let currentPos = 0;
    let targetNode = null;
    let startOffset = 0;
    let endOffset = 0;
    
    function findBlankNode(node) {
        if (node.nodeType === Node.TEXT_NODE) {
            const nodeLength = node.textContent.length;
            if (currentPos + nodeLength > blankPosition) {
                targetNode = node;
                startOffset = blankPosition - currentPos;
                endOffset = Math.min(startOffset + 4, nodeLength); // Select the ____
                return true;
            }
            currentPos += nodeLength;
        } else {
            for (let child of node.childNodes) {
                if (findBlankNode(child)) return true;
            }
        }
        return false;
    }
    
    findBlankNode(editor);
    
    if (targetNode) {
        // Select the blank
        range.setStart(targetNode, startOffset);
        range.setEnd(targetNode, endOffset);
        selection.removeAllRanges();
        selection.addRange(range);
        
        editor.focus();
        showVoiceFeedback('Blank selected - start dictating');
    }
}

function getCaretPosition(element) {
    let caretPos = 0;
    const selection = window.getSelection();
    
    if (selection.rangeCount > 0) {
        const range = selection.getRangeAt(0);
        const preCaretRange = range.cloneRange();
        preCaretRange.selectNodeContents(element);
        preCaretRange.setEnd(range.endContainer, range.endOffset);
        caretPos = preCaretRange.toString().length;
    }
    
    return caretPos;
}

function voiceLoadTemplate(phrase) {
    const words = phrase.split(' ');
    
    // Modality mapping (including common speech recognition errors)
    const modalityMap = {
        // Standard
        'ct': 'CT',
        'mri': 'MRI',
        'us': 'US',
        'xr': 'XR',
        'biotronics': 'Biotronics',
        
        // Variations
        'ultrasound': 'US',
        'xray': 'XR',
        'x-ray': 'XR',
        'mr': 'MRI',
        'mra': 'MRI',
        
        // Common speech errors
        'city': 'CT',
        'see tea': 'CT',
        'cat': 'CT',
        'cat scan': 'CT'
    };
    
    // Step 1: Find modality (check first 1-2 words)
    let modality = '';
    let procedureStartIndex = 1;
    
    // Check single word modality
    if (words.length > 0 && modalityMap[words[0]]) {
        modality = modalityMap[words[0]];
    }
    // Check two-word modality (e.g., "cat scan" or "see tea")
    else if (words.length > 1) {
        const twoWords = words[0] + ' ' + words[1];
        if (modalityMap[twoWords]) {
            modality = modalityMap[twoWords];
            procedureStartIndex = 2;
        }
    }
    
    if (!modality) {
        showVoiceFeedback('Could not detect modality. Say: LOAD [modality] [procedure]');
        return;
    }
    
    // Step 2: Get procedure (everything after modality)
    const procedure = words.slice(procedureStartIndex).join(' ');
    
    if (!procedure || procedure.length < 2) {
        showVoiceFeedback(`Say procedure name after ${modality}`);
        return;
    }
    
    // Step 3: Search for matches in this modality ONLY
    const categories = templateCategories[modality];
    
    if (!categories) {
        showVoiceFeedback(`No ${modality} templates available`);
        return;
    }
    
    const matches = [];
    const procedureLower = procedure.toLowerCase();
    const procedureWords = procedureLower.split(' ').filter(w => w.length > 1); // Ignore single letters
    
    Object.entries(categories).forEach(([categoryName, items]) => {
        items.forEach(item => {
            const itemLower = item.toLowerCase();
            
            // Match if ANY procedure word is found in template name
            const hasMatch = procedureWords.some(word => itemLower.includes(word));
            
            if (hasMatch) {
                const parentCategory = categoryName.toLowerCase().replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
                const itemName = item.toLowerCase().replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
                const templateKey = `${modality.toLowerCase()}_${parentCategory}_${itemName}`;
                
                // Calculate match score (how many words match)
                const matchScore = procedureWords.filter(word => itemLower.includes(word)).length;
                
                matches.push({
                    key: templateKey,
                    modality: modality,
                    categoryName: categoryName,
                    itemName: item,
                    displayName: item,
                    matchScore: matchScore
                });
            }
        });
    });
    
    if (matches.length === 0) {
        showVoiceFeedback(`No ${modality} templates found for "${procedure}"`);
        return;
    }
    
    // Sort by match score (best matches first)
    matches.sort((a, b) => b.matchScore - a.matchScore);
    
    // If only 1 match, load directly
    if (matches.length === 1) {
        if (templates[matches[0].key]) {
            selectTab(modality);
            loadTemplate(matches[0].key);
            showVoiceFeedback(`Loaded: ${matches[0].displayName}`);
        } else {
            showVoiceFeedback(`Template not configured: ${matches[0].displayName}`);
        }
        return;
    }
    
    // Multiple matches: show selection popup
    showVoiceTemplateSelection(matches, modality, procedure);
}

		function showVoiceTemplateSelection(matches, modality, procedure) {
    const matchesHtml = matches.map((match, index) => {
        const templateExists = templates.hasOwnProperty(match.key);
        const statusIcon = templateExists ? '✓' : '⚠️';
        const statusColor = templateExists ? '#27ae60' : '#e74c3c';
        const statusText = templateExists ? 'Available' : 'Not Configured';
        
        return `
            <div onclick="${templateExists ? `selectVoiceTemplate('${match.key}', '${modality}')` : ''}" 
                 style="padding: 15px; margin: 8px 0; background: white; border-left: 4px solid ${statusColor}; 
                        border-radius: 8px; cursor: ${templateExists ? 'pointer' : 'not-allowed'}; 
                        box-shadow: 0 2px 5px rgba(0,0,0,0.1); transition: all 0.2s; opacity: ${templateExists ? '1' : '0.6'};"
                 onmouseover="${templateExists ? `this.style.background='#e8f5e9'; this.style.transform='translateX(5px)';` : ''}" 
                 onmouseout="${templateExists ? `this.style.background='white'; this.style.transform='translateX(0)';` : ''}">
                <div style="display: flex; align-items: center; justify-content: space-between;">
                    <div style="flex: 1;">
                        <div style="font-weight: 600; color: #2c3e50; font-size: 15px; margin-bottom: 5px;">
                            ${match.displayName}
                        </div>
                        <div style="font-size: 12px; color: #7f8c8d;">
                            Category: ${match.categoryName}
                        </div>
                    </div>
                    <div style="text-align: right;">
                        <div style="color: ${statusColor}; font-size: 24px; margin-bottom: 3px;">${statusIcon}</div>
                        <div style="font-size: 10px; color: ${statusColor};">${statusText}</div>
                    </div>
                </div>
            </div>
        `;
    }).join('');
    
    const modal = createModal(`
        <div style="text-align: center; margin-bottom: 20px;">
            <h2 style="color: #2c3e50; margin: 0;">🎤 Voice Template Selection</h2>
            <p style="color: #7f8c8d; margin: 10px 0 0 0; font-size: 14px;">
                Found ${matches.length} ${modality} template(s) matching "<strong>${procedure}</strong>"
            </p>
        </div>
        
        <div style="max-height: 450px; overflow-y: auto; padding: 10px;">
            ${matchesHtml}
        </div>
        
        <div style="text-align: center; margin-top: 20px; padding-top: 15px; border-top: 1px solid #ecf0f1;">
            <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 10px 30px;">
                Cancel
            </button>
        </div>
    `);
}

function selectVoiceTemplate(templateKey, modality) {
    closeModal();
    
    if (!templates[templateKey]) {
        showNotification(`Template "${templateKey}" not configured in system`);
        return;
    }
    
    selectTab(modality);
    loadTemplate(templateKey);
}

function showVoiceFeedback(message) {
    const feedbackDiv = document.createElement('div');
    feedbackDiv.textContent = message;
    feedbackDiv.style.cssText = `
        position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
        background: rgba(39, 174, 96, 0.95); color: white; padding: 20px 30px;
        border-radius: 10px; z-index: 9999; font-size: 18px;
    `;
    document.body.appendChild(feedbackDiv);
    
    setTimeout(() => {
        if (feedbackDiv.parentNode) {
            feedbackDiv.parentNode.removeChild(feedbackDiv);
        }
    }, 2000);
}

function insertTextAtCursor(text) {
    const editor = document.getElementById('textEditor');
    
    if (editor.contentEditable === 'true') {
        const selection = window.getSelection();
        if (selection.rangeCount > 0) {
            document.execCommand('insertText', false, text);
        }
    }
    
    editor.focus();
    updateWordCount();
}

// ==============================================
// TUTORIAL SYSTEM
// ==============================================
// Tutorial Steps - Add more as you build features
const tutorialSteps = [
  {
    element: '#micBtn',
    intro: `
      <h3>🎤 Voice Input</h3>
      <p>Click this button to use voice dictation. Speak naturally and your words will appear in the editor.</p>
      <p><strong>Tip:</strong> Works best in quiet environment!</p>
    `,
    position: 'bottom'
  },
  {
    element: '#micStatus',
    intro: `
      <h3>🎙 Voice Status</h3>
      <p>This shows whether voice input is ready, listening, or processing your speech.</p>
    `,
    position: 'bottom'
  },
  {
    element: '[data-tab="QABoard"]',
    intro: `
      <h3>📋 QA Board</h3>
      <p>View quality assurance feedback on your reports. Check for any cases flagged by reviewers.</p>
    `,
    position: 'bottom'
  },
  {
    element: '[data-tab="PeerBoard"]',
    intro: `
      <h3>👥 Peer Review Board</h3>
      <p>Review cases submitted by your colleagues. Provide constructive feedback to improve quality.</p>
    `,
    position: 'bottom'
  },
  {
    element: '#modalityDropdown',
    intro: `
      <h3>🏥 Modality Selection</h3>
      <p>Choose the scan type: US (Ultrasound), CT, MRI, X-Ray. Make sure you are selecting the correct modality for the report</p>
      <p><strong>Note:</strong> The system will auto-detect modality from your report text!</p>
    `,
    position: 'bottom'
  },
  {
    element: '#empEventsBtn',
    intro: `
      <h3>🏥 Events</h3>
      <p>Find your schedule and Meeting management.</p>
      `,
    position: 'bottom'
  },
    {
    element: '.format',
    intro: `
      <h3>🏥 Format</h3>
      <p>Remove all spaces and paragraph from the report.</p>
      `,
    position: 'bottom'
  },
  {
    element: '.btn[onclick="generateAIRecommendations()"]',
    intro: `
      <h3>🏥 AI</h3>
      <p>Generate AI-powered recommendations for your report.</p>
      `,
    position: 'bottom'
  },
  {
    element: '.copy',
    intro: `
      <h3>🏥 Copy</h3>
      <p>Copy only the report text to your clipboard.</p>
      `,
    position: 'bottom'
  },
  {
    element: '.btn[onclick="copyAndCount()"]',
    intro: `
      <h3>🏥 Copy & Count</h3>
      <p>Copy the report to clipboard as well as submit your report. It also display the number of cases you reported.</p>
      `,
    position: 'bottom'
  },
  {
  element: '#institutionDropdown',
  intro: `
    <h3>🏥 Institution</h3>
    <p>Select the institution from the dropdown list before proceeding.</p>
  `,
  position: 'bottom'
},
{
  element: '#accessionNumber',
  intro: `
    <h3>🔢 Accession Number</h3>
    <p>Enter the accession number here. This field is required for submission.</p>
  `,
  position: 'bottom'
},
{
  element: '.clear',
  intro: `
    <h3>🗑️ Clear</h3>
    <p>Click this button to clear the editor content.</p>
  `,
  position: 'bottom'
},
{
  element: '.btn[onclick="submitForReview()"]',
  intro: `
    <h3>📤 Submit</h3>
    <p>Click here to submit your report for peer review. Peer review may take time, so please do not hold the report</p>
  `,
  position: 'bottom'
},
{
  element: '#textEditor',
  intro: `
    <h3>🖊️ Text Editor</h3>
    <p>This is where your report content will appear. Use shortcut "//" inside the editor followed by procedure name. Example: //ct stroke. You can edit, format, and review text here.</p>
    <p><strong>Note:</strong> Voice input and formatting actions will directly update this editor.</p>
  `,
  position: 'bottom'
},
{
  element: '#templateSearch',
  intro: `
    <h3>🔍 Template Search</h3>
    <p>Use this search bar to quickly find templates. Example- type CT stroke. Here you DO NOT need to enter "//". If there are multiple search result go to next page. You can also press <strong>Ctrl+K</strong> as a shortcut.</p>
  `,
  position: 'bottom'
},
{
  element: '#recentList',
  intro: `
    <h3>🕑 Recent Templates</h3>
    <p>Access your most recently used templates here for faster workflow.</p>
  `,
  position: 'bottom'
},
{
  element: '#categoryTitle',
  intro: `
    <h3>📂 Template Category</h3>
    <p>This section shows the current category of templates being displayed.</p>
  `,
  position: 'bottom'
},
{
  element: '#templateList',
  intro: `
    <h3>📑 Template List</h3>
    <p>Browse and select templates from this list. Templates will load dynamically based on category.</p>
  `,
  position: 'bottom'
},

];

function startTutorial() {
    // Initialize Intro.js with your steps
    introJs().setOptions({
        steps: tutorialSteps,
        showProgress: true,
        showBullets: false,
        exitOnOverlayClick: false,
        doneLabel: 'Got it!',
        nextLabel: 'Next →',
        prevLabel: '← Back',
        skipLabel: 'Exit'
    }).start();
}


// ==============================================
// ADVANCED SEARCH SYSTEM
// ==============================================

function openAdvancedSearch() {
    const modal = createModal(`
        <h2 style="color: #2c3e50; margin-bottom: 20px;">🔍 Advanced Search</h2>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 8px; font-weight: 500;">Search Type:</label>
            <select id="searchType" onchange="updateSearchFilters()" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-size: 14px;">
                <option value="">Select search type...</option>
                <option value="peer_review">Peer Review</option>
                <option value="qa" disabled style="color: #999;">QA (Coming Soon)</option>
                <option value="interesting_cases" disabled style="color: #999;">Interesting Cases (Coming Soon)</option>
            </select>
        </div>
        
        <div id="searchFiltersContainer" style="display: none; background: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
            <!-- Filters will be loaded here dynamically -->
        </div>
        
        <div id="searchResultsContainer" style="display: none;">
            <div style="background: #2c3e50; color: white; padding: 15px; border-radius: 8px 8px 0 0; margin-bottom: 0;">
                <h3 style="margin: 0;">Search Results (<span id="searchResultCount">0</span>)</h3>
            </div>
            <div id="searchResultsList" style="max-height: 400px; overflow-y: auto; background: white; border: 1px solid #ddd; border-top: none; border-radius: 0 0 8px 8px;">
                <!-- Results will appear here -->
            </div>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}

function updateSearchFilters() {
    const searchType = document.getElementById('searchType').value;
    const filtersContainer = document.getElementById('searchFiltersContainer');
    const resultsContainer = document.getElementById('searchResultsContainer');
    
    // Hide results when changing search type
    resultsContainer.style.display = 'none';
    
    if (!searchType) {
        filtersContainer.style.display = 'none';
        return;
    }
    
    if (searchType === 'peer_review') {
        loadPeerReviewFilters();
    } else if (searchType === 'qa') {
        loadQAFilters();
    }
    
    filtersContainer.style.display = 'block';
}

function loadPeerReviewFilters() {
    const filtersContainer = document.getElementById('searchFiltersContainer');
    
    // Check if user has permission to see reviewer names
    const canSeeReviewerNames = currentUser.permissions && currentUser.permissions.includes('peer_review');
    
    // Build radiologist dropdown options
    let radiologistOptions = '<option value="">All Reviewers</option>';
    if (canSeeReviewerNames) {
        Object.entries(authorizedEmployees).forEach(([code, emp]) => {
            if (emp.role === 'employee') {
                radiologistOptions += `<option value="${code}">${emp.name} (${code})</option>`;
            }
        });
    } else {
        radiologistOptions = '<option value="">All Reviewers (Permission Required)</option>';
    }
    
    filtersContainer.innerHTML = `
        <h4 style="margin: 0 0 15px 0; color: #2c3e50;">Peer Review Filters</h4>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 15px;">
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">Peer Reviewer:</label>
                <select id="searchPeerReviewer" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;" ${!canSeeReviewerNames ? 'disabled' : ''}>
                    ${radiologistOptions}
                </select>
            </div>
            
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">Hospital:</label>
                <select id="searchHospital" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
                    <option value="">All Hospitals</option>
                    <option value="MPHS">MPHS</option>
                    <option value="Menonita">Menonita</option>
                    <option value="NOVARAD">NOVARAD</option>
                    <option value="eRAD">eRAD</option>
                    <option value="Corozal">Corozal</option>
                </select>
            </div>
        </div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; margin-bottom: 15px;">
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">Modality:</label>
                <select id="searchModality" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
                    <option value="">All Modalities</option>
                    <option value="US">Ultrasound</option>
                    <option value="CT">CT Scan</option>
                    <option value="MRI">MRI</option>
                    <option value="XR">X-Ray</option>
                    <option value="Biotronics">Biotronics</option>
                </select>
            </div>
            
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">From Date:</label>
                <input type="date" id="searchFromDate" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
            
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">To Date:</label>
                <input type="date" id="searchToDate" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            </div>
        </div>
        
        <div style="margin-bottom: 15px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Accession Number:</label>
            <input type="text" id="searchAccession" placeholder="Search by accession number..." style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
        </div>
        
        <div style="display: flex; gap: 10px;">
            <button onclick="executeAdvancedSearch()" class="btn" style="background: #27ae60;">
                🔍 Search
            </button>
            <button onclick="clearAdvancedSearchFilters()" class="btn" style="background: #95a5a6;">
                Clear Filters
            </button>
        </div>
    `;
}

function loadQAFilters() {
    const filtersContainer = document.getElementById('searchFiltersContainer');
    
    // Check if user has permission to see QA details
    const canSeeQADetails = currentUser.permissions && currentUser.permissions.includes('qa_assign');
    
    // Build radiologist dropdown options
    let radiologistOptions = '<option value="">All Radiologists</option>';
    if (canSeeQADetails) {
        Object.entries(authorizedEmployees).forEach(([code, emp]) => {
            if (emp.role === 'employee') {
                radiologistOptions += `<option value="${code}">${emp.name} (${code})</option>`;
            }
        });
    } else {
        radiologistOptions = '<option value="">All Radiologists (Permission Required)</option>';
    }
    
    filtersContainer.innerHTML = `
        <h4 style="margin: 0 0 15px 0; color: #2c3e50;">QA Search Filters (Coming Soon)</h4>
        <p style="color: #666;">QA search functionality will be available in a future update.</p>
    `;
}

async function executeAdvancedSearch() {
    const searchType = document.getElementById('searchType').value;
    
    if (searchType === 'peer_review') {
        await searchPeerReviews();
    } else if (searchType === 'qa') {
        showNotification('QA search coming soon!');
    }
}

async function searchPeerReviews() {
    try {
        // Get filter values
        const reviewer = document.getElementById('searchPeerReviewer').value;
        const hospital = document.getElementById('searchHospital').value;
        const modality = document.getElementById('searchModality').value;
        const fromDate = document.getElementById('searchFromDate').value;
        const toDate = document.getElementById('searchToDate').value;
        const accession = document.getElementById('searchAccession').value.toLowerCase().trim();
        
        // Show loading
        const resultsContainer = document.getElementById('searchResultsContainer');
        const resultsList = document.getElementById('searchResultsList');
        resultsContainer.style.display = 'block';
        resultsList.innerHTML = '<div style="padding: 20px; text-align: center;">Searching...</div>';
        
        // Fetch all completed peer reviews
        const allPeerReviews = await getFromFirestore('peer_review_assignments');
        const completedReviews = allPeerReviews.filter(review => review.status === 'Completed');
        
        // Apply filters
        let filteredReviews = completedReviews.filter(review => {
            // Reviewer filter
            if (reviewer && review.assignedTo !== reviewer) return false;
            
            // Hospital filter (if hospitalName exists in review data)
            if (hospital && review.hospitalName && review.hospitalName !== hospital) return false;
            
            // Modality filter (if modality exists in review data)
            if (modality && review.modality && review.modality !== modality) return false;
            
            // Date range filter
            if (fromDate && review.completedDate) {
                const reviewDate = new Date(review.completedDate).toISOString().split('T')[0];
                if (reviewDate < fromDate) return false;
            }
            if (toDate && review.completedDate) {
                const reviewDate = new Date(review.completedDate).toISOString().split('T')[0];
                if (reviewDate > toDate) return false;
            }
            
            // Accession filter
            if (accession && review.accession && !review.accession.toLowerCase().includes(accession)) return false;
            
            return true;
        });
        
        // Sort by completion date (newest first)
        filteredReviews.sort((a, b) => new Date(b.completedDate) - new Date(a.completedDate));
        
        // Update count
        document.getElementById('searchResultCount').textContent = filteredReviews.length;
        
        // Display results
        if (filteredReviews.length === 0) {
            resultsList.innerHTML = '<div style="padding: 40px; text-align: center; color: #666;">No results found. Try adjusting your filters.</div>';
            return;
        }
        
        // Check permission to see reviewer names
        const canSeeReviewerNames = currentUser.permissions && currentUser.permissions.includes('peer_review');
        
        // Render results with pagination
        renderPeerReviewResults(filteredReviews, canSeeReviewerNames);
        
    } catch (error) {
        console.error('Error searching peer reviews:', error);
        showNotification('Error performing search');
    }
}

function renderPeerReviewResults(reviews, showReviewerNames, page = 1) {
    const itemsPerPage = 10;
    const startIndex = (page - 1) * itemsPerPage;
    const endIndex = startIndex + itemsPerPage;
    const pageReviews = reviews.slice(startIndex, endIndex);
    const totalPages = Math.ceil(reviews.length / itemsPerPage);
    
    const resultsList = document.getElementById('searchResultsList');
    
    let html = `
        <table style="width: 100%; border-collapse: collapse; font-size: 13px;">
            <thead style="background: #34495e; color: white; position: sticky; top: 0;">
                <tr>
                    <th style="padding: 10px; text-align: left;">Accession</th>
                    ${showReviewerNames ? '<th style="padding: 10px; text-align: left;">Peer Reviewer</th>' : ''}
                    <th style="padding: 10px; text-align: left;">Original Submitter</th>
                    <th style="padding: 10px; text-align: center;">Hospital</th>
                    <th style="padding: 10px; text-align: center;">Modality</th>
                    <th style="padding: 10px; text-align: center;">Completed Date</th>
                    <th style="padding: 10px; text-align: center;">Actions</th>
                </tr>
            </thead>
            <tbody>
    `;
    
    pageReviews.forEach(review => {
        const reviewerName = showReviewerNames 
            ? (authorizedEmployees[review.assignedTo]?.name || review.assignedTo)
            : 'Private';
        
        html += `
            <tr style="border-bottom: 1px solid #ecf0f1;">
                <td style="padding: 10px;">${review.accession || 'N/A'}</td>
                ${showReviewerNames ? `<td style="padding: 10px;">${reviewerName}</td>` : ''}
                <td style="padding: 10px;">${review.originalSubmitter || 'N/A'}</td>
                <td style="padding: 10px; text-align: center;">${review.hospitalName || 'N/A'}</td>
                <td style="padding: 10px; text-align: center;">${review.modality || 'N/A'}</td>
                <td style="padding: 10px; text-align: center;">${review.completedDate ? new Date(review.completedDate).toLocaleDateString() : 'N/A'}</td>
                <td style="padding: 10px; text-align: center;">
                    <button onclick="viewPeerComparisonFromSearch('${review.id}')" class="btn" style="background: #9b59b6; padding: 6px 12px; font-size: 11px;">
                        View Comparison
                    </button>
                </td>
            </tr>
        `;
    });
    
    html += `
            </tbody>
        </table>
    `;
    
    // Add pagination
    if (totalPages > 1) {
        html += `
            <div style="padding: 15px; text-align: center; background: #f5f5f5; border-top: 1px solid #ddd;">
                <div style="font-size: 12px; color: #666; margin-bottom: 10px;">
                    Showing ${startIndex + 1}-${Math.min(endIndex, reviews.length)} of ${reviews.length} results
                </div>
                <div style="display: flex; justify-content: center; gap: 5px; flex-wrap: wrap;">
                    ${Array.from({length: Math.min(totalPages, 10)}, (_, i) => {
                        const pageNum = i + 1;
                        return `<button onclick="renderPeerReviewResults(${JSON.stringify(reviews).replace(/"/g, '&quot;')}, ${showReviewerNames}, ${pageNum})" 
                                style="padding: 6px 12px; background: ${pageNum === page ? '#3498db' : 'white'}; 
                                color: ${pageNum === page ? 'white' : '#333'}; border: 1px solid #ddd; 
                                border-radius: 4px; cursor: pointer; font-size: 12px;">${pageNum}</button>`;
                    }).join('')}
                    ${totalPages > 10 ? '<span style="padding: 6px;">...</span>' : ''}
                </div>
            </div>
        `;
    }
    
    resultsList.innerHTML = html;
}

async function viewPeerComparisonFromSearch(reviewId) {
    // Reuse existing viewPeerComparison function
    await viewPeerComparison(reviewId);
}

function clearAdvancedSearchFilters() {
    document.getElementById('searchPeerReviewer').value = '';
    document.getElementById('searchHospital').value = '';
    document.getElementById('searchModality').value = '';
    document.getElementById('searchFromDate').value = '';
    document.getElementById('searchToDate').value = '';
    document.getElementById('searchAccession').value = '';
    
    // Hide results
    document.getElementById('searchResultsContainer').style.display = 'none';
}

// ==============================================
// PERMISSION HELPER FUNCTION
// ==============================================

function hasPermission(permission) {
    // No user logged in
    if (!currentUser) {
        return false;
    }
    if (currentUser.role === 'admin') {
        return true;
    }
    if (!currentUser.permissions || !Array.isArray(currentUser.permissions)) {
        return false;
    }
    return currentUser.permissions.includes(permission);
}

// Check if user has Body Part Rules access
function hasBodyPartRulesAccess() {
    return currentUser.role === 'hr' || 
           currentUser.role === 'admin' ||
           hasPermission('body_part_rules_manager');
}

// ==============================================
// REAL-TIME SYSTEM & NOTIFICATIONS
// ==============================================
let shortcutsInitialized = false;
let templatesInitialized = false; 

function setupRealtimeListeners() {
    // Real-time QA assignment notifications for employees
    if (currentUser.role === 'employee' || currentUser.role === 'admin') {
        const qaNotificationListener = db.collection('qa_assignments')
            .where('assignedTo', '==', currentUser.code)
            .where('status', 'in', ['Pending', 'In Progress'])
            .onSnapshot((snapshot) => {
                const newAssignments = snapshot.docs.filter(doc => {
                    const data = doc.data();
                    const assignedDate = new Date(data.createdDate);
                    const fiveMinutesAgo = new Date(Date.now() - 5 * 60 * 1000);
                    return assignedDate > fiveMinutesAgo && data.status === 'Pending';
                });
                
                if (newAssignments.length > 0) {
                    showNotification(`🔔 You have ${newAssignments.length} new QA assignment(s)!`);
                    playNotificationSound();
                    
                    // Desktop notification
                    if ('Notification' in window && Notification.permission === 'granted') {
                        new Notification('New QA Assignment', {
                            body: `You have ${newAssignments.length} new QA assignment(s)`,
                            icon: '🔔',
                            tag: 'qa-notification'
                        });
                    }
                }
                
                loadEmployeeBoards();
            });
			
        unsubscribeListeners.push(qaNotificationListener);
        
        // Real-time Peer Review notifications for employees
        const peerNotificationListener = db.collection('peer_review_assignments')
            .where('assignedTo', '==', currentUser.code)
            .where('status', 'in', ['Pending', 'In Progress'])
            .onSnapshot((snapshot) => {
                const newAssignments = snapshot.docs.filter(doc => {
                    const data = doc.data();
                    const assignedDate = new Date(data.assignedDate);
                    const fiveMinutesAgo = new Date(Date.now() - 5 * 60 * 1000);
                    return assignedDate > fiveMinutesAgo && data.status === 'Pending';
                });
                
                if (newAssignments.length > 0) {
                    showNotification(`🔔 You have ${newAssignments.length} new peer review assignment(s)!`);
                    playNotificationSound();
                    
                    // Desktop notification
                    if ('Notification' in window && Notification.permission === 'granted') {
                        new Notification('New Peer Review', {
                            body: `You have ${newAssignments.length} new peer review assignment(s)`,
                            icon: '🔔',
                            tag: 'peer-notification'
                        });
                    }
                }
                
                loadEmployeeBoards();
            });
        unsubscribeListeners.push(peerNotificationListener);
    }
    
    // QA Assignments Listener
    const qaListener = db.collection('qa_assignments').onSnapshot((snapshot) => {
    if (currentUser && currentUser.role === 'employee') {
        loadEmployeeBoards();
    }
    if (currentUser && (currentUser.role === 'hr' || currentUser.role === 'admin')) {
        if (document.getElementById('hrQAPanel').style.display === 'block') {
            loadHRQAData(); // This will update chart and table
        }
    }
});
unsubscribeListeners.push(qaListener)
const criticalListener = db.collection('system_data').doc('critical_findings').onSnapshot((doc) => {
    if (doc.exists) {
        const newCritical = doc.data().data || [];
        if (JSON.stringify(criticalFindings) !== JSON.stringify(newCritical)) {
            criticalFindings = newCritical;
            showNotification('Critical findings list updated by admin');
        }
    }
});
unsubscribeListeners.push(criticalListener);

    // Peer Review Submissions Listener (for HR)
    if (currentUser && (currentUser.role === 'hr' || currentUser.role === 'admin')) {
        const peerSubmissionsListener = db.collection('peer_review_submissions').onSnapshot((snapshot) => {
            const pendingSubmissions = snapshot.docs.filter(doc => {
                const data = doc.data();
                return !data.assignmentStatus || data.assignmentStatus === 'unassigned';
            });
            
            loadHRNotifications();
            
            if (document.getElementById('hrPeerPanel').style.display === 'block') {
                loadHRPeerData();
            }
        });
        unsubscribeListeners.push(peerSubmissionsListener);
    }

    // Peer Review Assignments Listener (for employees)
    if (currentUser.role === 'employee') {
        const peerAssignmentsListener = db.collection('peer_review_assignments').onSnapshot((snapshot) => {
            loadEmployeeBoards();
        });
        unsubscribeListeners.push(peerAssignmentsListener);
    }

    // Real-time template/shortcut updates
   const templatesListener = db.collection('system_data').doc('templates').onSnapshot((doc) => {
    if (doc.exists) {
        const newTemplates = doc.data().data || {};
        
        // Only show notification after initial load is complete
        if (templatesInitialized) {
            const hasChanged = JSON.stringify(templates) !== JSON.stringify(newTemplates);
            const updatedByOther = doc.data().updatedBy !== (currentUser.code || currentUser.username);
            
            if (hasChanged && updatedByOther) {
                showNotification('Templates updated by admin');
            }
        } else {
            // Mark as initialized after first load
            templatesInitialized = true;
        }
        
        templates = newTemplates;

    }
});
 unsubscribeListeners.push(templatesListener);

   const shortcutsListener = db.collection('system_data').doc('shortcuts').onSnapshot((doc) => {
        if (doc.exists) {
            const newShortcuts = doc.data().data || {};
            
            // Only show notification after initial load is complete
            if (shortcutsInitialized) {
                const hasChanged = JSON.stringify(shortcuts) !== JSON.stringify(newShortcuts);
                const updatedByOther = doc.data().updatedBy !== (currentUser.code || currentUser.username);
                
                if (hasChanged && updatedByOther) {
                    showNotification('Shortcuts updated by admin');
                }
            } else {
                // Mark as initialized after first load
                shortcutsInitialized = true;
            }
            
            shortcuts = newShortcuts;
        }
    });
    unsubscribeListeners.push(shortcutsListener);

const scheduleListener = db.collection('schedules').onSnapshot((snapshot) => {
        if (currentUser && currentUser.role === 'employee') {
            if (document.getElementById('empSchedulePanel').style.display === 'block') {
                loadEmployeeSchedule();
            }
        }
        if (currentUser && (currentUser.role === 'hr' || currentUser.role === 'admin')) {
            if (document.getElementById('hrSchedulePanel').style.display === 'block') {
                loadHRSchedule();
            }
        }
    });
    unsubscribeListeners.push(scheduleListener);
	
let isFirstBodyPartRulesLoad = true;

// Body Part Rules Listener - Auto-reload when HR updates rules	
const bodyPartRulesListener = db.collection('body_part_rules').onSnapshot(async (snapshot) => {
    if (isFirstBodyPartRulesLoad) {
        isFirstBodyPartRulesLoad = false;
        await loadBodyPartRules();
        return; // Skip notification on initial load
    }
    
    console.log('[Body Part Rules] Rules updated by HR - reloading...');
    await loadBodyPartRules();
    showNotification('📋 Body part rules updated');
});
unsubscribeListeners.push(bodyPartRulesListener);
    
    // Leave Requests Listener (for HR)
    if (currentUser && (currentUser.role === 'hr' || currentUser.role === 'admin')) {
        const leaveRequestsListener = db.collection('leave_requests').onSnapshot((snapshot) => {
            const pendingRequests = snapshot.docs.filter(doc => doc.data().status === 'pending');
            updateLeaveRequestCounter(pendingRequests.length);
        });
        unsubscribeListeners.push(leaveRequestsListener);
    }
    
// Real-time reports listener for HR/Admin dashboard
if (currentUser && (currentUser.role === 'hr' || currentUser.role === 'admin')) {
    console.log('[Reports Listener] Setting up real-time listener...');
    
    const reportsListener = db.collection('daily_reports')
        .onSnapshot((snapshot) => {
            console.log('[Reports Listener] ========== SNAPSHOT RECEIVED ==========');
            console.log('[Reports Listener] Timestamp:', new Date().toLocaleTimeString());
            console.log('[Reports Listener] Total documents:', snapshot.size);
            
            snapshot.docChanges().forEach((change) => {
                if (change.type === 'added') {
                    const data = change.doc.data();
                    console.log('[Reports Listener] NEW REPORT:', {
                        id: change.doc.id,
                        empCode: data.empCode,
                        time: data.submittedTime,
                        reportCount: data.reportCount
                    });
                }
            });
            
            // ✅ ALWAYS reload data from Firestore
            console.log('[Reports Listener] Reloading allReportsData...');
            
            getFromFirestore('daily_reports').then(reports => {
                allReportsData = reports;
                allReportsData.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
                console.log('[Reports Listener] ✅ Loaded', allReportsData.length, 'reports');
                
                // ✅ FIX: ALWAYS refresh UI if panel exists (even if not visible)
                const hrPanel = document.getElementById('hrReportsPanel');
                if (hrPanel) {
                    console.log('[Reports Listener] Refreshing UI...');
                    applyReportsFilters();
                    console.log('[Reports Listener] ✅ UI refreshed');
                }
            });
            
        }, (error) => {
            console.error('[Reports Listener] ❌ ERROR:', error);
        });
    
    unsubscribeListeners.push(reportsListener);
    console.log('[Reports Listener] ✅ Listener registered');
}
    // Schedule Notifications Listener (for employees)

	if (currentUser && currentUser.role === 'employee') {
    let notificationCheckTimeout = null;
    const notificationsListener = db.collection('schedule_notifications')
        .where('empCode', '==', currentUser.code)
        .where('acknowledged', '==', false)
        .onSnapshot((snapshot) => {
            // Debounce: only check once every 2 seconds
            clearTimeout(notificationCheckTimeout);
            notificationCheckTimeout = setTimeout(() => {
                if (snapshot.docs.length > 0 && !document.querySelector('.notification-badge')) {
                    checkPendingScheduleNotifications();
                }
            }, 2000);
        });
    unsubscribeListeners.push(notificationsListener);
}
}	
		function updateLeaveRequestCounter(count) {
    const counter = document.getElementById('leaveRequestCount');
    if (counter) {
        if (count === undefined) {
            // Load count from database
            getFromFirestore('leave_requests').then(requests => {
                const pending = requests.filter(r => r.status === 'pending').length;
                counter.textContent = pending;
            });
        } else {
            counter.textContent = count;
        }
    }
}

async function loadHRNotifications() {
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') return;
    
    try {
        // Load pending peer review submissions
        const submissions = await getFromFirestore('peer_review_submissions');
        const pendingSubmissions = submissions.filter(sub => 
            !sub.assignmentStatus || sub.assignmentStatus === 'unassigned'
        );
        
        const hrPeerCounter = document.getElementById('hrPeerCounter');
        if (pendingSubmissions.length > 0) {
            hrPeerCounter.textContent = pendingSubmissions.length;
            hrPeerCounter.style.display = 'block';
        } else {
            hrPeerCounter.style.display = 'none';
        }
        
        // Load QA data for HR QA counter
        const qaData = await getFromFirestore('qa_assignments');
        const completedQAs = qaData.filter(qa => qa.status === 'Completed' && !qa.qaGrade);
        
        const hrQACounter = document.getElementById('hrQACounter');
        if (completedQAs.length > 0) {
            hrQACounter.textContent = completedQAs.length;
            hrQACounter.style.display = 'block';
        } else {
            hrQACounter.style.display = 'none';
        }
        
    } catch (error) {
        console.error('Error loading HR notifications:', error);
    }
}

function cleanupListeners() {
    unsubscribeListeners.forEach(unsubscribe => unsubscribe());
    unsubscribeListeners = [];
}

// ==============================================
// FIREBASE HELPER FUNCTIONS
// ==============================================

async function saveToFirestore(collection, data) {
    try {
        const docRef = await db.collection(collection).add(data);
        return docRef.id;
    } catch (error) {
        console.error("Error adding document: ", error);
        throw error;
    }
}

async function getFromFirestore(collection) {
    try {
        const querySnapshot = await db.collection(collection).get();
        const data = [];
        querySnapshot.forEach((doc) => {
            data.push({ id: doc.id, ...doc.data() });
        });
        return data;
    } catch (error) {
        console.error("Error getting documents: ", error);
        return [];
    }
}

async function updateFirestoreDoc(collection, docId, data) {
    try {
        // Find document by custom ID field
        const querySnapshot = await db.collection(collection).get();
        let docRef = null;
        
        querySnapshot.forEach((doc) => {
            if (doc.data().id === docId) {
                docRef = doc.ref;
            }
        });
        
        if (docRef) {
            await docRef.update(data);
        } else {
            throw new Error('Document not found');
        }
        
    } catch (error) {
        console.error("Error updating document: ", error);
        throw error;
    }
}

async function loadSystemData() {
    try {
        const employeesDoc = await db.collection('system_data').doc('employees').get();
        if (employeesDoc.exists) {
            const firestoreData = employeesDoc.data().data;
            
            // ✅ SAFETY CHECK: Only load if Firestore has actual employee data
            if (firestoreData && Object.keys(firestoreData).length > 0) {
                authorizedEmployees = firestoreData;
                console.log(`[System] ✅ Loaded ${Object.keys(authorizedEmployees).length} employees from Firestore`);
                // ↑ FIXED: Changed console.log` to console.log(
            } else {
                console.error('[System] ⚠️ WARNING: Firestore employee data is empty!');
                // Keep existing authorizedEmployees (don't overwrite with empty)
            }
        } else {
            console.error('[System] ❌ ERROR: Employees document does not exist in Firestore!');
        }
        
        const shortcutsDoc = await db.collection('system_data').doc('shortcuts').get();
        if (shortcutsDoc.exists) {
            shortcuts = shortcutsDoc.data().data || shortcuts;
        }
        
        const templatesDoc = await db.collection('system_data').doc('templates').get();
        if (templatesDoc.exists) {
            templates = templatesDoc.data().data || templates;
        }
        
        const criticalDoc = await db.collection('system_data').doc('critical_findings').get();
        if (criticalDoc.exists) {
            criticalFindings = criticalDoc.data().data || criticalFindings;
        }
        
		const institutionsDoc = await db.collection('system_data').doc('institutions').get();
			if (institutionsDoc.exists) {
				institutions = institutionsDoc.data().data || institutions;
			}

        const aiConfigDoc = await db.collection('system_data').doc('ai_config').get();
        if (aiConfigDoc.exists) {
            const aiConfig = aiConfigDoc.data();
            GEMINI_CONFIG.apiKey = aiConfig.apiKey || '';
            GEMINI_CONFIG.enabled = aiConfig.enabled || false;
        }
        
        const categoriesDoc = await db.collection('system_data').doc('template_categories').get();
        if (categoriesDoc.exists) {
            const loadedCategories = categoriesDoc.data().data;
            // Use Object.assign to merge with existing templateCategories
            Object.keys(templateCategories).forEach(key => delete templateCategories[key]);
            Object.assign(templateCategories, loadedCategories);
        }
		
    } catch (error) {
        console.error('Error loading system data:', error);
    }
}

async function logEmployeeAccess(empCode, empName) {
    try {
        await saveToFirestore('access_logs', {
            code: empCode,
            name: empName,
            timestamp: new Date().toISOString(),
            action: 'login_success'
        });
    } catch (error) {
        console.error('Error logging access:', error);
    }
}

async function logFailedAccess(empCode) {
    try {
        await saveToFirestore('access_logs', {
            code: empCode,
            name: 'UNKNOWN',
            timestamp: new Date().toISOString(),
            action: 'login_failed'
        });
    } catch (error) {
        console.error('Error logging failed access:', error);
    }
}

// ==============================================
// DIRECT FIRESTORE EMPLOYEE UPDATE (SAFE)
// ==============================================

async function updateEmployeeFieldDirectly(empCode, updates) {
    try {
        console.log(`[Update] Updating employee ${empCode}:`, updates);
        
        const employeesDoc = await db.collection('system_data').doc('employees').get();
        
        if (!employeesDoc.exists) {
            throw new Error('Employees document not found in Firestore');
        }
        
        const allEmployees = employeesDoc.data().data;
        
        if (!allEmployees[empCode]) {
            throw new Error(`Employee ${empCode} not found`);
        }
        
        Object.keys(updates).forEach(key => {
            allEmployees[empCode][key] = updates[key];
        });
        
        await db.collection('system_data').doc('employees').update({
            data: allEmployees,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser ? (currentUser.code || currentUser.username) : 'SYSTEM'
        });
        
        Object.keys(updates).forEach(key => {
            authorizedEmployees[empCode][key] = updates[key];
        });
        
        console.log(`[Update] ✅ Successfully updated ${empCode}`);
        return true;
        
    } catch (error) {
        console.error(`[Update] ❌ Error updating ${empCode}:`, error);
        throw error;
    }
}

// ==============================================
// PASSWORD SYSTEM INITIALIZATION (ONE-TIME)
// ==============================================

async function initializePasswordSystemForExistingEmployees() {
    // EXPLANATION: This function runs ONCE to add password fields to existing employees
    // It does NOT change their login behavior - they can still login with just their code
    // It just prepares the data structure for the gradual migration
    
    try {
        console.log('[Password System] Checking if initialization needed...');
        
        // Load current employees from Firestore
        await loadSystemData();
        
        let updatedCount = 0;
        let alreadyInitialized = 0;
        
        // Check each employee
        for (const [empCode, employee] of Object.entries(authorizedEmployees)) {
            if (employee.role !== 'employee') continue; // Skip non-employees
            
            // Check if already initialized
            if (employee.hasOwnProperty('passwordSet')) {
                alreadyInitialized++;
                continue;
            }
            
            // EXPLANATION: Add password fields WITHOUT changing login behavior
            employee.passwordSet = false; // FALSE = can still login with just code
            employee.password = null; // No password yet
            employee.passwordSetDate = null;
            employee.passwordReminderCount = 0;
            employee.passwordSetupDeadline = null;
            employee.failedLoginAttempts = 0;
            employee.accountLocked = false;
            
            updatedCount++;
        }
        
        if (updatedCount > 0) {
            // Save updated employees to Firestore
            await db.collection('system_data').doc('employees').set({
                data: authorizedEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: 'SYSTEM_INIT',
                passwordSystemInitialized: true
            });
            
            console.log(`[Password System] ✅ Initialized ${updatedCount} employees for password migration`);
            console.log(`[Password System] ${alreadyInitialized} employees already had password fields`);
            
            return {
                success: true,
                initialized: updatedCount,
                alreadyInitialized: alreadyInitialized
            };
        } else {
            console.log(`[Password System] All ${alreadyInitialized} employees already initialized`);
            return {
                success: true,
                initialized: 0,
                alreadyInitialized: alreadyInitialized
            };
        }
        
    } catch (error) {
        console.error('[Password System] Initialization error:', error);
        return {
            success: false,
            error: error.message
        };
    }
}

// EXPLANATION: Auto-run initialization on admin login
// This ensures the system is set up before HR tries to use password management

async function checkPasswordSystemInitialization() {
    if (isPasswordInitRunning) {
        console.log('[Password System] Initialization already running, skipping...');
        return;
    }
    
    if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'hr')) {
        isPasswordInitRunning = true; // 🆕 SET FLAG
        
        try {
            const systemDoc = await db.collection('system_data').doc('employees').get();
            
            if (systemDoc.exists) {
                const data = systemDoc.data();
                
                if (!data.passwordSystemInitialized) {
                    console.log('[Password System] Running first-time initialization...');
                    const result = await initializePasswordSystemForExistingEmployees();
                    
                    if (result.success && result.initialized > 0) {
                        showNotification(`✅ Password system initialized for ${result.initialized} employees`);
                    }
                }
            }
        } finally {
            isPasswordInitRunning = false; // 🆕 CLEAR FLAG
        }
    }
}

// ==============================================
// UTILITY FUNCTIONS
// ==============================================

function createModal(content) {
    const modal = document.createElement('div');
    modal.className = 'modal';
    modal.innerHTML = `
        <div class="modal-content">
            ${content}
        </div>
    `;
    
    // Close modal when clicking outside
    modal.addEventListener('click', function(e) {
        if (e.target === modal) {
            closeModal();
        }
    });
    
    document.body.appendChild(modal);
    return modal;
}

function closeModal() {
    const modals = document.querySelectorAll('.modal');
    modals.forEach(modal => modal.remove());
}

function showNotification(message) {
    const notification = document.createElement('div');
    notification.className = 'notification';
    notification.textContent = message;
    
    document.body.appendChild(notification);
    
    setTimeout(() => {
        notification.classList.add('show');
    }, 100);
    
    setTimeout(() => {
        notification.classList.remove('show');
        setTimeout(() => {
            if (notification.parentNode) {
                document.body.removeChild(notification);
            }
        }, 300);
    }, 4000);
}
function playNotificationSound() {
    try {
        // Simple beep sound
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        oscillator.frequency.value = 800;
        oscillator.type = 'sine';
        
        gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
        
        oscillator.start(audioContext.currentTime);
        oscillator.stop(audioContext.currentTime + 0.5);
    } catch (e) {
        console.log('Audio not supported');
    }
}

function updateStatus(message) {
    const statusElement = document.getElementById('statusText');
    if (statusElement) {
        statusElement.textContent = message;
    }
}

function generateReportHash(text) {
    // Normalize text for smart duplicate detection
    let cleanText = text.toLowerCase().trim();
    
    // Remove punctuation
    cleanText = cleanText.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()'"?]/g, '');
    
    // Remove extra spaces (multiple spaces → single space)
    cleanText = cleanText.replace(/\s+/g, ' ');
    
    // Remove articles and common prepositions
    const stopWords = ['a', 'an', 'the', 'in', 'on', 'at', 'of', 'to', 'for', 'with', 'from', 'by', 'as', 'is', 'are', 'was', 'were'];
    const words = cleanText.split(' ');
    const filteredWords = words.filter(word => word.length > 0 && !stopWords.includes(word));
    cleanText = filteredWords.join(' ');
    
    // Generate hash from normalized text
    let hash = 0;
    for (let i = 0; i < cleanText.length; i++) {
        const char = cleanText.charCodeAt(i);
        hash = ((hash << 5) - hash) + char;
        hash = hash & hash;
    }
    
    return Math.abs(hash).toString(36);
}
function getNormalizedText(text) {
    // Same normalization as hash, but return the text for comparison
    let cleanText = text.toLowerCase().trim();
    cleanText = cleanText.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()'"?]/g, '');
    cleanText = cleanText.replace(/\s+/g, ' ');
    
    const stopWords = ['a', 'an', 'the', 'in', 'on', 'at', 'of', 'to', 'for', 'with', 'from', 'by', 'as', 'is', 'are', 'was', 'were'];
    const words = cleanText.split(' ');
    const filteredWords = words.filter(word => word.length > 0 && !stopWords.includes(word));
    
    return filteredWords;  // Return array of meaningful words
}
function countWordDifference(text1, text2) {
    const words1 = getNormalizedText(text1);
    const words2 = getNormalizedText(text2);
    
    // Count words that are in one but not the other
    const set1 = new Set(words1);
    const set2 = new Set(words2);
    
    let differences = 0;
    
    // Words in text1 but not in text2
    words1.forEach(word => {
        if (!set2.has(word)) differences++;
    });
    
    // Words in text2 but not in text1
    words2.forEach(word => {
        if (!set1.has(word)) differences++;
    });
    
    return differences;
}

// ==============================================
// EVENTS DROPDOWN MANAGEMENT
// ==============================================

function toggleEmpEventsDropdown() {
    const dropdown = document.getElementById('empEventsDropdown');
    const isVisible = dropdown.style.display === 'block';
    
    // Close any other dropdowns first
    closeHREventsDropdown();
    
    if (isVisible) {
        dropdown.style.display = 'none';
    } else {
        dropdown.style.display = 'block';
    }
}

function closeEmpEventsDropdown() {
    const dropdown = document.getElementById('empEventsDropdown');
    if (dropdown) {
        dropdown.style.display = 'none';
    }
}

function toggleHREventsDropdown() {
    const dropdown = document.getElementById('hrEventsDropdown');
    const isVisible = dropdown.style.display === 'block';
    
    // Close any other dropdowns first
    closeEmpEventsDropdown();
    
    if (isVisible) {
        dropdown.style.display = 'none';
    } else {
        dropdown.style.display = 'block';
    }
}

function closeHREventsDropdown() {
    const dropdown = document.getElementById('hrEventsDropdown');
    if (dropdown) {
        dropdown.style.display = 'none';
    }
}

// Close dropdowns when clicking outside
document.addEventListener('click', function(e) {
    const empBtn = document.getElementById('empEventsBtn');
    const empDropdown = document.getElementById('empEventsDropdown');
    const hrBtn = document.getElementById('hrEventsBtn');
    const hrDropdown = document.getElementById('hrEventsDropdown');
    
    // Close employee dropdown if clicking outside
    if (empBtn && empDropdown && !empBtn.contains(e.target) && !empDropdown.contains(e.target)) {
        closeEmpEventsDropdown();
    }
    
    // Close HR dropdown if clicking outside
    if (hrBtn && hrDropdown && !hrBtn.contains(e.target) && !hrDropdown.contains(e.target)) {
        closeHREventsDropdown();
    }
});

// ==============================================
// SESSION TIMEOUT MANAGEMENT
// ==============================================

function initSessionTimeout() {
    ['mousedown', 'keypress', 'scroll', 'touchstart', 'click'].forEach(event => {
        document.addEventListener(event, resetSessionTimer, true);
    });
    resetSessionTimer();
}

function resetSessionTimer() {
    lastActivity = Date.now();
    
    clearTimeout(sessionTimeout);
    clearTimeout(sessionWarningTimeout);
    
    // Show warning 1 minute before timeout
    sessionWarningTimeout = setTimeout(() => {
        showSessionWarning();
    }, TIMEOUT_DURATION - WARNING_TIME);
    
    // Force logout after full timeout
    sessionTimeout = setTimeout(() => {
        forceLogout();
    }, TIMEOUT_DURATION);
}

function showSessionWarning() {
    const modal = createModal(`
        <h3 style="color: #e67e22;">⏱️ Session Expiring Soon</h3>
        <p style="margin: 20px 0;">You will be automatically logged out in 60 seconds due to inactivity.</p>
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="extendSession()" class="btn" style="background: #27ae60; margin-right: 10px;">
                Stay Logged In
            </button>
            <button onclick="logout()" class="btn" style="background: #95a5a6;">
                Logout Now
            </button>
        </div>
    `);
    
    // Add backdrop click prevention for this modal
    const modalEl = document.querySelector('.modal');
    if (modalEl) {
        modalEl.style.pointerEvents = 'auto';
    }
}

function extendSession() {
    closeModal();
    resetSessionTimer();
    showNotification('Session extended');
}

async function forceLogout() {
    closeModal();
    await endSessionTracking('timeout'); // NEW LINE
    showNotification('Session expired due to inactivity');
    setTimeout(() => {
        logout();
    }, 1000);
}

function stopSessionTimeout() {
    clearTimeout(sessionTimeout);
    clearTimeout(sessionWarningTimeout);
}
	async function generateAIRecommendations() {
    const editor = document.getElementById('textEditor');
    const fullText = editor.textContent || editor.innerText || '';
    
    // Extract FINDINGS section
    const findingsMatch = fullText.match(/FINDINGS:(.*?)(?=IMPRESSION:|RECOMMENDATION:|$)/is);
    if (!findingsMatch) {
        showNotification('Please complete FINDINGS section first');
        return;
    }
    
    const findings = findingsMatch[1].trim();
    
    if (!GEMINI_CONFIG.enabled || !GEMINI_CONFIG.apiKey) {
        const modal = createModal(`
            <h3>AI Setup Required</h3>
            <p>Please ask your administrator to configure the AI system in Admin Panel.</p>
            <button onclick="closeModal()" class="btn">Close</button>
        `);
        return;
    }
    
    // DETECT MODALITY AND BODY PART FROM REPORT
    const modality = detectModality(fullText);
    const bodyPart = detectBodyPart(fullText);
    
    const loadingModal = createModal(`
        <h3>AI Analysis in Progress</h3>
        <div style="text-align: center; padding: 40px;">
            <div style="border: 4px solid #f3f3f3; border-top: 4px solid #9b59b6; border-radius: 50%; width: 60px; height: 60px; animation: spin 1s linear infinite; margin: 0 auto;"></div>
            <p style="margin-top: 20px;">Analyzing ${modality} ${bodyPart} findings...</p>
        </div>
    `);
    
    try {
        const apiUrl = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=' + GEMINI_CONFIG.apiKey;
        
        // BUILD CONTEXT-AWARE PROMPT
        const contextPrompt = `You are an expert radiologist. You are reviewing a ${modality} scan of the ${bodyPart}.

CRITICAL INSTRUCTIONS:
- This is a ${modality} exam (NOT MRI, NOT CT, NOT X-ray unless specified)
- The body part being examined is: ${bodyPart}
- Do NOT mention any other imaging modality
- Do NOT mention any other body part
- Base recommendations ONLY on the findings provided

Based on these ${modality} findings of the ${bodyPart}, provide 3-5 actionable clinical recommendations:

FINDINGS:
${findings}

Provide numbered RECOMMENDATIONS that are:
1. Specific follow-up imaging needed (modality, timeframe) - relevant to ${bodyPart}
2. Specialist consultation if required
3. Specific tests or workup to order
4. Management considerations

IMPORTANT: Only mention "${modality}" and "${bodyPart}" in your response. Do not reference other modalities or body parts.`;

        const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                contents: [{
                    parts: [{
                        text: contextPrompt
                    }]
                }],
                generationConfig: {
                    temperature: 0.6,
                    maxOutputTokens: 600,
                    topP: 0.8,
                    topK: 40
                }
            })
        });
        
        closeModal();
        
        if (!response.ok) {
            const errorData = await response.json().catch(() => ({}));
            const errorMsg = errorData.error?.message || 'Unknown error';
            
            if (errorMsg.includes('quota') || errorMsg.includes('Quota')) {
                throw new Error('Daily quota exceeded. Wait 24 hours or get new API key.');
            } else if (errorMsg.includes('API key')) {
                throw new Error('Invalid API key. Get new key from aistudio.google.com');
            } else {
                throw new Error('API Error: ' + errorMsg);
            }
        }
        
        const data = await response.json();
        
        if (!data.candidates || !data.candidates[0] || !data.candidates[0].content || !data.candidates[0].content.parts) {
            throw new Error('Invalid response from AI');
        }
        
        const recommendations = data.candidates[0].content.parts[0].text;
        showAIRecommendationsModal(recommendations, modality, bodyPart);
        
    } catch (error) {
        closeModal();
        console.error('Full error:', error);
        showNotification('AI Error: ' + error.message);
    }
}
		function detectModality(text) {
    if (!currentLoadedTemplate) {
        // Fallback to current tab if no template loaded
        const tabToModality = {
            'US': 'Ultrasound',
            'CT': 'CT',
            'MRI': 'MRI',
            'XR': 'X-Ray',
            'Biotronics': 'Biotronics'
        };
        return tabToModality[currentTab] || 'Imaging';
    }
    
    // Extract modality from template key (first part before underscore)
    const parts = currentLoadedTemplate.split('_');
    const modalityKey = parts[0].toUpperCase();
    
    const modalityMap = {
        'US': 'Ultrasound',
        'CT': 'CT',
        'MRI': 'MRI',
        'XR': 'X-Ray',
        'BIOTRONICS': 'Biotronics'
    };
    
    return modalityMap[modalityKey] || 'Imaging';
}

		function detectBodyPart(text) {
    if (!currentLoadedTemplate) {
        return 'the examined region';
    }
    
    // Parse template key: modality_category_procedure or modality_category_procedure_subprocedure
    const parts = currentLoadedTemplate.split('_');
    
    if (parts.length < 2) {
        return 'the examined region';
    }
    
    const modalityKey = parts[0].toUpperCase(); // e.g., 'CT'
    const categoryKey = parts[1]; // e.g., 'head'
    
    // Find the category in templateCategories
    const categories = templateCategories[modalityKey];
    if (!categories) {
        return 'the examined region';
    }
    
    // Find matching category name (case-insensitive)
    let matchedCategory = null;
    let matchedProcedure = null;
    
    for (const [categoryName, procedures] of Object.entries(categories)) {
        const categoryNormalized = categoryName.toLowerCase().replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
        
        if (categoryNormalized === categoryKey.toLowerCase()) {
            matchedCategory = categoryName;
            
            // Try to find the specific procedure
            if (parts.length > 2) {
                const procedureKey = parts.slice(2).join(' '); // Rejoin rest of parts
                
                for (const procedure of procedures) {
                    const procedureNormalized = procedure.toLowerCase().replace(/\s+/g, '_').replace(/[^a-zA-Z0-9_]/g, '');
                    const templateProcedureKey = parts.slice(2).join('_');
                    
                    if (procedureNormalized === templateProcedureKey.toLowerCase()) {
                        matchedProcedure = procedure;
                        break;
                    }
                }
            }
            break;
        }
    }
    
    // Build the body part description
    if (matchedProcedure) {
        return `${matchedCategory} - ${matchedProcedure}`;
    } else if (matchedCategory) {
        return matchedCategory;
    } else {
        return parts.slice(1).join(' ').replace(/_/g, ' ');
    }
}

	function showAIRecommendationsModal(recommendations, modality, bodyPart) {
    const modal = createModal(`
        <h3>AI-Generated Recommendations</h3>
        
        <div style="background: #e8f5e9; border-left: 4px solid #4caf50; padding: 15px; margin-bottom: 20px; border-radius: 5px;">
            <strong>✓ AI Analysis Complete</strong>
            <div style="margin-top: 8px; font-size: 13px;">
                <strong>Modality:</strong> ${modality} | <strong>Body Part:</strong> ${bodyPart}
            </div>
            <p style="margin: 5px 0 0 0; font-size: 13px;">Review and modify these recommendations based on complete clinical context.</p>
        </div>
        
        <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px; max-height: 400px; overflow-y: auto; border: 1px solid #dee2e6;">
            <pre style="white-space: pre-wrap; font-family: 'Segoe UI', Arial; line-height: 1.8; margin: 0; font-size: 14px;">${escapeHtml(recommendations)}</pre>
        </div>
        
        <div style="background: #fff3cd; padding: 10px; border-radius: 5px; margin-bottom: 20px; font-size: 12px;">
            ⚠️ <strong>Disclaimer:</strong> AI-generated content requires physician validation before clinical use.
        </div>
        
        <div style="display: flex; gap: 10px; justify-content: flex-end;">
            <button onclick="insertAIRecommendations(\`${recommendations.replace(/`/g, '\\`').replace(/\$/g, '\\$')}\`)" 
                    class="btn" style="background: #27ae60;">
                ✓ Insert into Report
            </button>
            <button onclick="copyAIRecommendations(\`${recommendations.replace(/`/g, '\\`').replace(/\$/g, '\\$')}\`)" 
                    class="btn" style="background: #3498db;">
                📋 Copy to Clipboard
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">
                Close
            </button>
        </div>
    `);
}
function insertAIRecommendations(recText) {
    const editor = document.getElementById('textEditor');
    let content = editor.textContent || editor.innerText || '';
    
    // Check if RECOMMENDATION section exists
    if (content.includes('RECOMMENDATION:')) {
        // Replace existing recommendations
        content = content.replace(/RECOMMENDATION:.*$/is, `RECOMMENDATION:\n${recText}`);
    } else {
        // Add new RECOMMENDATION section
        content += '\n\nRECOMMENDATION:\n' + recText;
    }
    
    editor.innerHTML = content.replace(/\n/g, '<br>');
    closeModal();
    showNotification('AI recommendations inserted into report');
    updateWordCount();
}

function copyAIRecommendations(text) {
    navigator.clipboard.writeText(text).then(() => {
        showNotification('Recommendations copied to clipboard');
    }).catch(err => {
        console.error('Copy failed:', err);
        showNotification('Copy failed. Please try again.');
    });
}

function escapeHtml(text) {
    const div = document.createElement('div');
    div.textContent = text;
    return div.innerHTML;
}

// ==============================================
// EMPLOYEE CREDENTIALS BACKUP SYSTEM
// ==============================================

async function backupEmployeeCredentials(empCode, reason, oldData = null) {
    // ✅ BACKUP EMPLOYEE DATA BEFORE ANY PASSWORD CHANGES
    try {
        const employee = oldData || authorizedEmployees[empCode];
        
        if (!employee) {
            console.error(`[BACKUP] Employee ${empCode} not found`);
            return;
        }
        
        const backup = {
            id: `BACKUP_${Date.now()}_${empCode}`,
            empCode: empCode,
            timestamp: new Date().toISOString(),
            reason: reason, // 'reset', 'unlock', 'initial_setup', 'admin_edit', 'forced_change'
            backupBy: currentUser ? (currentUser.code || currentUser.username) : 'SYSTEM',
            
            // ✅ CRITICAL FIELDS BACKUP
            employeeData: {
                name: employee.name,
                specialty: employee.specialty,
                department: employee.department,
                category: employee.category,
                email: employee.email,
                role: employee.role,
                
                // PASSWORD-RELATED FIELDS
                password: employee.password || null,
                passwordSet: employee.passwordSet || false,
                passwordSetDate: employee.passwordSetDate || null,
                failedLoginAttempts: employee.failedLoginAttempts || 0,
                accountLocked: employee.accountLocked || false,
                mustChangePassword: employee.mustChangePassword || false,
                passwordResetBy: employee.passwordResetBy || null,
                passwordResetDate: employee.passwordResetDate || null
            }
        };
        
        await saveToFirestore('employee_credentials_backup', backup);
        console.log(`[BACKUP] ✅ Credentials backed up for ${empCode} - Reason: ${reason}`);
        
        return true;
        
    } catch (error) {
        console.error('[BACKUP] ❌ Error backing up credentials:', error);
        return false;
    }
}

async function restoreEmployeeCredentials(backupId) {
    // ✅ RESTORE EMPLOYEE DATA FROM BACKUP
    try {
        const allBackups = await getFromFirestore('employee_credentials_backup');
        const backup = allBackups.find(b => b.id === backupId);
        
        if (!backup) {
            alert('Backup not found');
            return false;
        }
        
        if (!confirm(`Restore credentials for ${backup.empCode} from backup?\n\nBackup Date: ${new Date(backup.timestamp).toLocaleString()}\nReason: ${backup.reason}`)) {
            return false;
        }
        
        const empCode = backup.empCode;
        
        await db.runTransaction(async (transaction) => {
            const employeesRef = db.collection('system_data').doc('employees');
            const employeesDoc = await transaction.get(employeesRef);
            
            if (!employeesDoc.exists) {
                throw new Error('Employees document not found');
            }
            
            const allEmployees = employeesDoc.data().data;
            
            if (!allEmployees[empCode]) {
                throw new Error(`Employee ${empCode} not found in current database`);
            }
            
            // ✅ RESTORE PASSWORD-RELATED FIELDS ONLY (don't touch name, dept, etc.)
            allEmployees[empCode].password = backup.employeeData.password;
            allEmployees[empCode].passwordSet = backup.employeeData.passwordSet;
            allEmployees[empCode].passwordSetDate = backup.employeeData.passwordSetDate;
            allEmployees[empCode].failedLoginAttempts = backup.employeeData.failedLoginAttempts;
            allEmployees[empCode].accountLocked = backup.employeeData.accountLocked;
            allEmployees[empCode].mustChangePassword = false; // Allow login after restore
            
            transaction.update(employeesRef, {
                data: allEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: currentUser.code || currentUser.username
            });
        });
        
        await loadSystemData();
        
        showNotification(`✅ Credentials restored for ${backup.employeeData.name} (${empCode})`);
        console.log(`[BACKUP] ✅ Credentials restored from backup: ${backupId}`);
        
        return true;
        
    } catch (error) {
        console.error('[BACKUP] ❌ Error restoring credentials:', error);
        alert('Error restoring credentials: ' + error.message);
        return false;
    }
}

// ==============================================
// SCHEDULING SYSTEM
// ==============================================

function selectScheduleCategory(category) {
    currentScheduleCategory = category;
    
    document.querySelectorAll('.schedule-tab').forEach(tab => tab.classList.remove('active'));
    event.target.classList.add('active');
    
    // Check if coordinator viewing master schedule (read-only)
    const isCoordMasterView = currentUser.role === 'employee' && 
                              currentUser.permissions && 
                              currentUser.permissions.includes('master_schedule_view') &&
                              document.getElementById('hrSchedulePanel').style.display === 'block';
    
    if (isCoordMasterView) {
        loadMasterScheduleReadOnly();
    } else {
        loadHRSchedule();
    }
}

function navigateMonth(direction, viewType) {
    if (viewType === 'emp') {
        currentScheduleMonth.setMonth(currentScheduleMonth.getMonth() + direction);
        
        // Check if coordinator with master view permission
        const hasMasterView = currentUser.permissions && currentUser.permissions.includes('master_schedule_view');
        
        if (hasMasterView && document.getElementById('hrSchedulePanel').style.display === 'block') {
            loadMasterScheduleReadOnly();
        } else {
            loadEmployeeSchedule();
        }
    } else {
        currentScheduleMonth.setMonth(currentScheduleMonth.getMonth() + direction);
        loadHRSchedule();
    }
}

async function loadEmployeeSchedule() {
    if (!currentUser || currentUser.role !== 'employee') return;
    
    const monthName = currentScheduleMonth.toLocaleDateString('en-US', { month: 'long', year: 'numeric' });
    document.getElementById('empCurrentMonth').textContent = monthName;
    
    // Load employee's schedule data
    const allSchedules = await getFromFirestore('schedules');
    const empSchedule = allSchedules.filter(s => s.empCode === currentUser.code);
    
    // Load leave requests
    const allLeaveRequests = await getFromFirestore('leave_requests');
    const empLeaveRequests = allLeaveRequests.filter(r => r.empCode === currentUser.code);
    
    // Load leave data
    const allLeaves = await getFromFirestore('leave_balances');
    const empLeave = allLeaves.find(l => l.empCode === currentUser.code) || {
        total: 30,
        used: 0,
        pending: 0,
        available: 30
    };
    
    // Update leave summary
    document.getElementById('empTotalLeave').textContent = empLeave.total || 30;
    document.getElementById('empUsedLeave').textContent = empLeave.used || 0;
    document.getElementById('empPendingLeave').textContent = empLeave.pending || 0;
    document.getElementById('empAvailableLeave').textContent = empLeave.available || 30;
    
    // Generate calendar for current month
    const year = currentScheduleMonth.getFullYear();
    const month = currentScheduleMonth.getMonth();
    const daysInMonth = new Date(year, month + 1, 0).getDate();
    
    let html = '';
    
    for (let day = 1; day <= daysInMonth; day++) {
        const date = new Date(year, month, day);
        // FIX: Create date string directly without timezone conversion
        const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
        const dayName = date.toLocaleDateString('en-US', { weekday: 'short' });
        
        const shifts = empSchedule.filter(s => s.date === dateStr && !s.leaveType);
        const isWeekend = date.getDay() === 0 || date.getDay() === 6;
        
        // Find leave request for this date
        const leaveRequest = empLeaveRequests.find(req => 
            dateStr >= req.fromDate && dateStr <= req.toDate
        );
        
        let shiftTime = '-';
        let duration = '-';
        let status = 'Off';
        let statusColor = '#ecf0f1';
        let actionButton = '';
        
        // Show rejection reason if cancellation was rejected
        if (leaveRequest && leaveRequest.cancellationStatus === 'rejected' && dateStr === leaveRequest.fromDate) {
            actionButton = `<div style="color: #e74c3c; font-size: 10px; font-weight: bold; margin-top: 5px;">✗ Cancellation Rejected</div>
                            ${leaveRequest.cancellationRejectionReason ? 
                              `<div style="color: #666; font-size: 9px; margin-top: 3px;">${leaveRequest.cancellationRejectionReason}</div>` : ''}`;
        }

        // Handle leave requests (both pending and approved)
        if (leaveRequest) {
            // FIX: Parse dates properly to avoid timezone issues
            const today = new Date();
            today.setHours(0, 0, 0, 0);
            
            const [lYear, lMonth, lDay] = leaveRequest.fromDate.split('-').map(Number);
            const leaveStartDate = new Date(lYear, lMonth - 1, lDay);
            leaveStartDate.setHours(0, 0, 0, 0);
            
            const daysUntilLeave = Math.ceil((leaveStartDate - today) / (1000 * 60 * 60 * 24));
            
            // Determine leave status
            if (leaveRequest.status === 'pending') {
                status = 'Leave (Pending Approval)';
                statusColor = '#ffe5b4';
            } else if (leaveRequest.status === 'approved') {
                status = 'Leave (Approved)';
                statusColor = '#cfe2ff';
            }
            
            // Show cancel/request cancel button on first day of leave
            if (dateStr === leaveRequest.fromDate) {
                if (leaveRequest.cancellationStatus === 'requested') {
                    actionButton = '<span style="color: #f39c12; font-size: 11px; font-weight: bold;">⏳ Cancellation Pending</span>';
                } else if (leaveRequest.cancellationStatus === 'rejected') {
                    actionButton = `<span style="color: #e74c3c; font-size: 11px; font-weight: bold;">✗ Cancellation Rejected</span>
                                   ${leaveRequest.cancellationRejectionReason ? 
                                     `<div style="font-size: 9px; color: #666; margin-top: 3px;">${leaveRequest.cancellationRejectionReason}</div>` : ''}`;
                } else if (daysUntilLeave < 0) {
                    actionButton = '<span style="color: #95a5a6; font-size: 11px;">Leave started</span>';
                } else if (leaveRequest.status === 'pending') {
                    // Pending leaves can ALWAYS be cancelled (no 3-day rule)
                    actionButton = `<button onclick="cancelLeaveRequest('${leaveRequest.id}')" style="background: #e74c3c; color: white; border: none; padding: 4px 8px; border-radius: 4px; font-size: 11px; cursor: pointer; margin-top: 5px;">✗ Cancel Request</button>`;
                } else if (leaveRequest.status === 'approved') {
                    // Approved leaves require 3-day notice for cancellation request
                    if (daysUntilLeave < 3) {
                        actionButton = '<span style="color: #e74c3c; font-size: 11px;">Cannot cancel (< 3 days)</span>';
                    } else {
                        actionButton = `<button onclick="cancelLeaveRequest('${leaveRequest.id}')" style="background: #f39c12; color: white; border: none; padding: 4px 8px; border-radius: 4px; font-size: 11px; cursor: pointer; margin-top: 5px;">✗ Request Cancel</button>`;
                    }
                }
            }
        }

        // Override with shift data if present in schedule
				if (shifts.length > 0) {
			// Show all shifts for this day
			const shiftTimes = shifts.map(s => `${s.start}-${s.end}`).join(', ');
			const totalDuration = shifts.reduce((sum, s) => sum + parseFloat(s.duration || 0), 0).toFixed(1);
			
			// Check if any shift is marked as extra
			const hasExtra = shifts.some(s => s.shiftType === 'extra');
			
			shiftTime = shiftTimes;
			duration = `${totalDuration} hours`;
			status = shifts.length > 1 ? `${shifts.length} Shifts` : 'Scheduled';
			
			if (hasExtra) {
				status += ' ⚡';
			}
			
			statusColor = '#d4edda';
			
			// Show notes if any
			const notesText = shifts.filter(s => s.notes && !s.notes.includes('Overnight Part')).map(s => s.notes).join('; ');
			if (notesText) {
				status += ` - ${notesText}`;
			}
		}
        
        html += `
            <tr style="border-bottom: 1px solid #ecf0f1;">
                <td class="employee-name" style="${isWeekend ? 'background: #fff3cd;' : ''}">
                    ${dayName}, ${month + 1}/${day}/${year}
                </td>
                <td style="background: ${statusColor};">${shiftTime}</td>
                <td style="background: ${statusColor};">${duration}</td>
                <td style="background: ${statusColor}; font-weight: 600;">
                    ${status}
                    ${actionButton}
                </td>
            </tr>
        `;
    }
    
    document.getElementById('empScheduleBody').innerHTML = html;
}

async function cancelLeaveRequest(leaveId) {
    try {
        const allLeaveRequests = await getFromFirestore('leave_requests');
        const leaveRequest = allLeaveRequests.find(r => r.id === leaveId);
        
        if (!leaveRequest) {
            alert('Leave request not found');
            return;
        }
        
        // Get today's date at midnight in local timezone
        const today = new Date();
        today.setHours(0, 0, 0, 0);
        
        // Parse leave start date correctly (assuming YYYY-MM-DD format)
        const [year, month, day] = leaveRequest.fromDate.split('-').map(Number);
        const leaveStartDate = new Date(year, month - 1, day); // Local timezone
        leaveStartDate.setHours(0, 0, 0, 0);
        
        const daysUntilLeave = Math.ceil((leaveStartDate - today) / (1000 * 60 * 60 * 24));
        
        // Block if less than 3 days or already started
        if (daysUntilLeave < 3) {
            alert('Cannot cancel leave that starts in less than 3 days');
            return;
        }
        
        // Block if more than 30 days before
        if (daysUntilLeave > 30) {
            alert('Cannot cancel leave more than 30 days before start date');
            return;
        }
        
        if (leaveRequest.cancellationStatus === 'rejected') {
            alert('Your cancellation request was rejected by HR. You cannot request cancellation again for this leave.');
            return;
        }
        
        if (leaveRequest.status === 'pending') {
            // Direct cancellation for pending leave
            if (!confirm(`Cancel this pending leave request (${leaveRequest.fromDate} to ${leaveRequest.toDate})?`)) {
                return;
            }
            
            // Delete leave request
            const snapshot = await db.collection('leave_requests').get();
            for (const doc of snapshot.docs) {
                if (doc.data().id === leaveId) {
                    await doc.ref.delete();
                    break;
                }
            }
            
            // Restore leave balance
            await updateLeaveBalance(currentUser.code, 0, -leaveRequest.days, leaveRequest.days);
            
            // Save to history
            await saveToFirestore('leave_cancellation_history', {
                id: `CANCEL_${Date.now()}`,
                leaveRequestId: leaveId,
                empCode: currentUser.code,
                empName: currentUser.name,
                originalFromDate: leaveRequest.fromDate,
                originalToDate: leaveRequest.toDate,
                days: leaveRequest.days,
                leaveType: leaveRequest.leaveType,
                cancellationType: 'direct',
                requestedDate: new Date().toISOString(),
                approvedDate: new Date().toISOString(),
                approvedBy: 'SELF'
            });
            
            showNotification('Leave request cancelled successfully');
            loadEmployeeSchedule();
            
        } else if (leaveRequest.status === 'approved') {
            // Request cancellation for approved leave
            if (!confirm(`Request cancellation for approved leave (${leaveRequest.fromDate} to ${leaveRequest.toDate})?\n\nHR approval is required.`)) {
                return;
            }
            
            await updateFirestoreDoc('leave_requests', leaveId, {
                cancellationStatus: 'requested',
                cancellationRequestDate: new Date().toISOString(),
                cancellationRequestedBy: currentUser.code
            });
            
            showNotification('Cancellation request submitted. Awaiting HR approval.');
            loadEmployeeSchedule();
        }
        
    } catch (error) {
        console.error('Error cancelling leave:', error);
        alert('Error processing cancellation. Please try again.');
    }
}

async function loadMasterScheduleReadOnly() {
    const monthName = currentScheduleMonth.toLocaleDateString('en-US', { month: 'long', year: 'numeric' });
    document.getElementById('hrCurrentMonth').textContent = monthName;
    
    // Hide HR controls for coordinator view
    const scheduleControls = document.querySelector('.schedule-controls');
    if (scheduleControls) {
        scheduleControls.style.display = 'none';
    }
    
    const scheduleHeaderButtons = document.getElementById('scheduleHeaderButtons');
    if (scheduleHeaderButtons) {
        scheduleHeaderButtons.style.display = 'none';
    }
    
    // Get employees in selected category
    const categoryEmployees = Object.entries(authorizedEmployees)
        .filter(([code, emp]) => emp.category === currentScheduleCategory)
        .map(([code, emp]) => ({ code, name: emp.name, email: emp.email }));
    
    if (categoryEmployees.length === 0) {
        document.getElementById('hrScheduleBody').innerHTML = `
            <tr><td colspan="32" style="padding: 40px; text-align: center; color: #666;">
                No employees found in ${currentScheduleCategory} category.
            </td></tr>
        `;
        return;
    }
    
    // Load all schedules
    const allSchedules = await getFromFirestore('schedules');
    
    // Generate table header (dates)
    const year = currentScheduleMonth.getFullYear();
    const month = currentScheduleMonth.getMonth();
    const daysInMonth = new Date(year, month + 1, 0).getDate();
    
    let headerHtml = '<tr><th class="employee-name">Employee</th>';
    
    for (let day = 1; day <= daysInMonth; day++) {
        const date = new Date(year, month, day);
        const dayName = date.toLocaleDateString('en-US', { weekday: 'short' });
        const isWeekend = date.getDay() === 0 || date.getDay() === 6;
        
        headerHtml += `<th class="${isWeekend ? 'weekend-column' : ''}">${dayName}<br>${day}</th>`;
    }
    
    headerHtml += '</tr>';
    document.getElementById('hrScheduleHeader').innerHTML = headerHtml;
    
    // Generate table body (READ ONLY - NO INTERACTIONS)
    let bodyHtml = '';
    
    for (const emp of categoryEmployees) {
        bodyHtml += `<tr><td class="employee-name">${emp.name}</td>`;
        
        for (let day = 1; day <= daysInMonth; day++) {
            const date = new Date(year, month, day);
            const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;  // ✅ FIXED
            const isWeekend = date.getDay() === 0 || date.getDay() === 6;
            
            // Get ALL shifts for this employee on this date
            const shifts = allSchedules.filter(s => s.empCode === emp.code && s.date === dateStr);
            
            let cellClass = 'shift-cell';
            let cellContent = '';
            
            if (isWeekend) {
                cellClass += ' weekend-column';
            }
            
            // Check for leave
            const leaveShift = shifts.find(s => s.leaveType);
            
            if (leaveShift) {
                cellClass += leaveShift.leaveType === 'approved' ? ' leave-approved' : ' leave-pending';
                cellContent = `<div class="leave-badge ${leaveShift.leaveType}">${leaveShift.leaveType === 'approved' ? 'LEAVE' : 'PENDING'}</div>`;
            } else if (shifts.length > 0) {
                // Has shift timing(s)
                const workShifts = shifts.filter(s => s.start && s.end);
                
                if (workShifts.length > 0) {
                    cellClass += ' has-shift';
                    
                    // Show all shifts
                    workShifts.forEach((shift, idx) => {
                        const shiftTypeIcon = shift.shiftType === 'extra' ? '⚡' : '';
                        cellContent += `
                            <div style="margin-bottom: 2px;">
                                <span class="shift-time">${shift.start}-${shift.end}</span>
                                <span class="shift-duration">${shift.duration}h${shiftTypeIcon}</span>
                            </div>
                        `;
                    });
                    
                    // Show total if multiple shifts
                    if (workShifts.length > 1) {
                        const totalDayHours = workShifts.reduce((sum, s) => sum + (parseFloat(s.duration) || 0), 0);
                        cellContent += `<div style="font-size: 10px; color: #7f8c8d; font-weight: bold; margin-top: 2px;">Total: ${totalDayHours.toFixed(1)}h</div>`;
                    }
                    
                    // Add notes from shifts (exclude overnight auto-notes)
                    const allNotes = workShifts
                        .filter(s => s.notes && !s.notes.includes('Overnight Part'))
                        .map(s => s.notes)
                        .join('; ');
                    
                    if (allNotes) {
                        cellContent += `<span class="shift-note">${allNotes}</span>`;
                    }
                }
                
                // Note-only cells (no timing)
                const noteOnlyShifts = shifts.filter(s => !s.start && !s.end && s.notes);
                if (noteOnlyShifts.length > 0 && workShifts.length === 0) {
                    cellClass += ' note-only-cell';
                    const allNotes = noteOnlyShifts.map(s => s.notes).join('; ');
                    cellContent = `<span class="shift-note">${allNotes}</span>`;
                }
            }
            
            // READ ONLY - NO DRAG, NO CLICK, NO CONTEXT MENU
            bodyHtml += `<td class="${cellClass}">${cellContent}</td>`;
        }
        
        bodyHtml += '</tr>';
    }
    
    document.getElementById('hrScheduleBody').innerHTML = bodyHtml;
}

async function loadHRSchedule() {
    const monthName = currentScheduleMonth.toLocaleDateString('en-US', { month: 'long', year: 'numeric' });
    document.getElementById('hrCurrentMonth').textContent = monthName;
    
    // Get employees in selected category

		let categoryEmployees = Object.entries(authorizedEmployees)
			.filter(([code, emp]) => emp.category === currentScheduleCategory)
			.map(([code, emp]) => ({ code, name: emp.name, email: emp.email }));

		// Load saved custom order
		const savedOrder = await getEmployeeOrder(currentScheduleCategory);

		if (savedOrder && savedOrder.order) {
			const orderMap = {};
			savedOrder.order.forEach((code, index) => {
				orderMap[code] = index;
			});
			
			categoryEmployees.sort((a, b) => {
				const orderA = orderMap[a.code] !== undefined ? orderMap[a.code] : 999;
				const orderB = orderMap[b.code] !== undefined ? orderMap[b.code] : 999;
				return orderA - orderB;
			});
		}
    
    if (categoryEmployees.length === 0) {
        document.getElementById('hrScheduleBody').innerHTML = `
            <tr><td colspan="32" style="padding: 40px; text-align: center; color: #666;">
                No employees found in ${currentScheduleCategory} category. Please assign categories in Admin Panel.
            </td></tr>
        `;
        return;
    }
    
    // Load all schedules
    const allSchedules = await getFromFirestore('schedules');
	   
    // Generate table header and body
    const year = currentScheduleMonth.getFullYear();
    const month = currentScheduleMonth.getMonth();
    const daysInMonth = new Date(year, month + 1, 0).getDate();
    
    // NEW LAYOUT: Employees as columns, Dates as rows
    let headerHtml = '<tr><th class="date-column">Date</th>';
    
    // Employee names as column headers
    for (const emp of categoryEmployees) {
        headerHtml += `<th class="employee-header">${emp.name}</th>`;
    }
    
    headerHtml += '</tr>';
    document.getElementById('hrScheduleHeader').innerHTML = headerHtml;
    
    // Generate table body (date rows)
    let bodyHtml = '';
    
    for (let day = 1; day <= daysInMonth; day++) {
        const date = new Date(year, month, day);
        const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
        const dayName = date.toLocaleDateString('en-US', { weekday: 'short' });
        const isWeekend = date.getDay() === 0 || date.getDay() === 6;
        
        bodyHtml += `<tr>`;
        bodyHtml += `<td class="date-column ${isWeekend ? 'weekend-column' : ''}">${dayName}<br>${month + 1}/${day}</td>`;
        
        // Loop through employees for this date
        for (const emp of categoryEmployees) {
            // Get ALL shifts for this employee on this date
            const shifts = allSchedules.filter(s => s.empCode === emp.code && s.date === dateStr);
            
            let cellClass = 'shift-cell';
            let cellContent = '';
            
            if (isWeekend) {
                cellClass += ' weekend-column';
            }
            
            // Check for leave
            const leaveShift = shifts.find(s => s.leaveType);
            
            if (leaveShift) {
                cellClass += leaveShift.leaveType === 'approved' ? ' leave-approved' : ' leave-pending';
                cellContent = `<div class="leave-badge ${leaveShift.leaveType}">${leaveShift.leaveType === 'approved' ? 'LEAVE' : 'PENDING'}</div>`;
            } else if (shifts.length > 0) {
                // Has shift timing(s)
                const workShifts = shifts.filter(s => s.start && s.end);
                
                if (workShifts.length > 0) {
                    cellClass += ' has-shift';
                    
                    // Calculate total hours for the day
                    const totalDayHours = workShifts.reduce((sum, s) => sum + (parseFloat(s.duration) || 0), 0);
                    
                    // Calculate week hours (for overtime detection)
                    let weekHours = 0;
                    const weekStart = new Date(date);
                    weekStart.setDate(date.getDate() - date.getDay() + 1); // Get Monday
                    
                    for (let d = 0; d < date.getDay(); d++) {
                        const checkDate = new Date(weekStart);
                        checkDate.setDate(weekStart.getDate() + d);
                        const checkDateStr = `${checkDate.getFullYear()}-${String(checkDate.getMonth() + 1).padStart(2, '0')}-${String(checkDate.getDate()).padStart(2, '0')}`;
                        const dayShifts = allSchedules.filter(s => s.empCode === emp.code && s.date === checkDateStr && s.start && s.end);
                        weekHours += dayShifts.reduce((sum, s) => sum + (parseFloat(s.duration) || 0), 0);
                    }
                    weekHours += totalDayHours;
                    
                    // Check overtime (>48 hours/week)
                    if (weekHours > 48) {
                        cellClass += ' overtime';
                        cellContent = `<div class="overtime-indicator">OT</div>`;
                    }
                    
                    // Check if any shift is draft
                    if (workShifts.some(s => s.status === 'draft')) {
                        cellContent += `<div style="position: absolute; top: 2px; left: 2px; border: 1px solid #f39c12; color: #f39c12; padding: 2px 4px; border-radius: 3px; font-size: 8px; font-weight: bold; background: transparent;">DRAFT</div>`;
                    }
                    
                    // Show all shifts
                    workShifts.forEach((shift, idx) => {
                        const shiftTypeIcon = shift.shiftType === 'extra' ? '⚡' : '';
                        cellContent += `
                            <div style="margin-bottom: 2px;">
                                <span class="shift-time">${shift.start}-${shift.end}</span>
                                <span class="shift-duration">${shift.duration}h${shiftTypeIcon}</span>
                            </div>
                        `;
                    });
                    
                    // Show total if multiple shifts
                    if (workShifts.length > 1) {
                        cellContent += `<div style="font-size: 10px; color: #7f8c8d; font-weight: bold; margin-top: 2px;">Total: ${totalDayHours.toFixed(1)}h</div>`;
                    }
                    
                    // Add notes from shifts (exclude overnight auto-notes)
                    const allNotes = workShifts
                        .filter(s => s.notes && !s.notes.includes('Overnight Part'))
                        .map(s => s.notes)
                        .join('; ');
                    
                    if (allNotes) {
                        const noteText = allNotes.length > 30 ? allNotes.substring(0, 30) + '...' : allNotes;
                        cellContent += `
                            <div class="shift-note-container" title="${allNotes}" style="margin-top: 3px;">
                                <span class="shift-note">${noteText}</span>
                                <button class="delete-note-btn" onclick="deleteScheduleNote(event, '${emp.code}', '${dateStr}'); return false;" title="Delete note">×</button>
                            </div>
                        `;
                    }
                }
                
                // Note-only cells (no timing)
                const noteOnlyShifts = shifts.filter(s => !s.start && !s.end && s.notes);
                if (noteOnlyShifts.length > 0 && workShifts.length === 0) {
                    cellClass += ' note-only-cell';
                    const allNotes = noteOnlyShifts.map(s => s.notes).join('; ');
                    const noteText = allNotes.length > 30 ? allNotes.substring(0, 30) + '...' : allNotes;
                    cellContent = `
                        <div class="shift-note-container" title="${allNotes}">
                            <span class="shift-note">${noteText}</span>
                            <button class="delete-note-btn" onclick="deleteScheduleNote(event, '${emp.code}', '${dateStr}'); return false;" title="Delete note">×</button>
                        </div>
                    `;
                }
            }
            
            bodyHtml += `
                <td class="${cellClass}" 
                    data-emp="${emp.code}" 
                    data-date="${dateStr}">
                    ${cellContent}
                </td>
            `;
        }
        
        bodyHtml += '</tr>';
    }
    
    document.getElementById('hrScheduleBody').innerHTML = bodyHtml;
}

async function deleteScheduleNote(event, empCode, date) {
    // CRITICAL: Stop ALL event propagation
    event.stopPropagation();
    event.preventDefault();
    event.stopImmediatePropagation();
    
    if (!confirm('Delete this note?')) return;
    
    try {
        const allSchedules = await getFromFirestore('schedules');
        const shift = allSchedules.find(s => s.empCode === empCode && s.date === date);
        
        if (!shift) {
            showNotification('❌ Note not found');
            return;
        }
        
        if (shift.start && shift.end) {
            // Has shift timing - just remove note
            await updateFirestoreDoc('schedules', shift.id, {
                notes: ''
            });
        } else {
            // Note-only cell - delete entire entry
            const snapshot = await db.collection('schedules').get();
            for (const doc of snapshot.docs) {
                if (doc.data().id === shift.id) {
                    await doc.ref.delete();
                    break;
                }
            }
        }
        
        showNotification('✓ Note deleted');
        await loadHRSchedule();
        
    } catch (error) {
        console.error('Error deleting note:', error);
        showNotification('❌ Error deleting note');
    }
}

		// Drag and Drop Functions
function dragShift(event) {
    const empCode = event.target.dataset.emp;
    const date = event.target.dataset.date;
    
    event.dataTransfer.setData('empCode', empCode);
    event.dataTransfer.setData('date', date);
    event.target.style.opacity = '0.5';
}

function dragEnd(event) {
    event.target.style.opacity = '1';
}

function allowDrop(event) {
    event.preventDefault();
    event.target.classList.add('drag-over');
}
async function dropShift(event) {
    event.preventDefault();
    event.target.classList.remove('drag-over');
    
    const sourceEmpCode = event.dataTransfer.getData('empCode');
    const sourceDate = event.dataTransfer.getData('date');
    
    const targetEmpCode = event.target.dataset.emp;
    const targetDate = event.target.dataset.date;
    
    if (!targetEmpCode || !targetDate) return;
    
    if (event.target.classList.contains('leave-approved') || 
        event.target.classList.contains('leave-pending')) {
        showNotification('Cannot assign shift on leave day');
        return;
    }
    
    const sourceEmpName = authorizedEmployees[sourceEmpCode]?.name || sourceEmpCode;
    const targetEmpName = authorizedEmployees[targetEmpCode]?.name || targetEmpCode;
    
    const isSameEmployee = sourceEmpCode === targetEmpCode;
    const message = isSameEmployee 
        ? `Move ${sourceEmpName}'s shift from ${sourceDate} to ${targetDate}?`
        : `Copy ${sourceEmpName}'s shift from ${sourceDate} to ${targetEmpName} on ${targetDate}?`;
    
    if (!confirm(message)) return;
    
    try {
        const allSchedules = await getFromFirestore('schedules');
        const sourceShift = allSchedules.find(s => s.empCode === sourceEmpCode && s.date === sourceDate);
        
        if (!sourceShift) return;
        
        const newShift = {
            id: `SHIFT_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`,
            empCode: targetEmpCode,
            date: targetDate,
            start: sourceShift.start,
            end: sourceShift.end,
            duration: sourceShift.duration,
            notes: sourceShift.notes || '',
            createdBy: currentUser.code || currentUser.username,
            createdDate: new Date().toISOString(),
            category: currentScheduleCategory,
            status: 'draft'
        };
        
        await saveToFirestore('schedules', newShift);
        
        if (isSameEmployee) {
            const snapshot = await db.collection('schedules').get();
            snapshot.forEach(async (doc) => {
                if (doc.data().id === sourceShift.id) {
                    await doc.ref.delete();
                }
            });
        }
        
        showNotification('Shift moved as draft - Publish to notify employee');
        loadHRSchedule();
        
    } catch (error) {
        console.error('Error dropping shift:', error);
        showNotification('Error updating shift');
    }
}

// Multi-cell selection variables
let selectedCells = [];
let copiedShiftData = null;
let isMouseSelecting = false;
let startCell = null;

// Show reorder employees modal
async function showReorderEmployees() {
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') {
        alert('Only HR can reorder employees');
        return;
    }
    
    // Get employees in current category
    let categoryEmployees = Object.entries(authorizedEmployees)
        .filter(([code, emp]) => emp.category === currentScheduleCategory)
        .map(([code, emp]) => ({ code, name: emp.name }));
    
    if (categoryEmployees.length === 0) {
        alert('No employees in this category');
        return;
    }
    
    // Load saved order from Firestore
    const savedOrder = await getEmployeeOrder(currentScheduleCategory);
    
    // Sort employees by saved order
    if (savedOrder && savedOrder.order) {
        const orderMap = {};
        savedOrder.order.forEach((code, index) => {
            orderMap[code] = index;
        });
        
        categoryEmployees.sort((a, b) => {
            const orderA = orderMap[a.code] !== undefined ? orderMap[a.code] : 999;
            const orderB = orderMap[b.code] !== undefined ? orderMap[b.code] : 999;
            return orderA - orderB;
        });
    }
    
    // Generate employee list HTML
    const employeeListHtml = categoryEmployees.map(emp => `
        <div class="reorder-employee-item" draggable="true" data-code="${emp.code}">
            <span class="reorder-drag-handle">☰</span>
            <span class="reorder-employee-name">${emp.name}</span>
            <span class="reorder-employee-code">${emp.code}</span>
        </div>
    `).join('');
    
    const modal = createModal(`
        <h3>🔄 Reorder Employees - ${currentScheduleCategory}</h3>
        
        <div style="background: #e3f2fd; padding: 12px; border-radius: 6px; margin-bottom: 20px; font-size: 13px;">
            <strong>💡 How to reorder:</strong> Drag and drop employees to arrange them in your preferred order. This order will be saved and used in the schedule view.
        </div>
        
        <div id="reorderEmployeeList" style="max-height: 400px; overflow-y: auto;">
            ${employeeListHtml}
        </div>
        
        <div style="text-align: right; margin-top: 20px; display: flex; gap: 10px; justify-content: flex-end;">
            <button onclick="saveEmployeeOrder()" class="btn" style="background: #27ae60;">
                💾 Save Order
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">
                Cancel
            </button>
        </div>
    `);
    
    // Enable drag and drop
    enableEmployeeReordering();
}

// Enable drag and drop for employee reordering
function enableEmployeeReordering() {
    const container = document.getElementById('reorderEmployeeList');
    if (!container) return;
    
    let draggedElement = null;
    
    container.addEventListener('dragstart', (e) => {
        if (e.target.classList.contains('reorder-employee-item')) {
            draggedElement = e.target;
            e.target.classList.add('dragging');
        }
    });
    
    container.addEventListener('dragend', (e) => {
        if (e.target.classList.contains('reorder-employee-item')) {
            e.target.classList.remove('dragging');
        }
    });
    
    container.addEventListener('dragover', (e) => {
        e.preventDefault();
        const afterElement = getDragAfterElement(container, e.clientY);
        if (afterElement == null) {
            container.appendChild(draggedElement);
        } else {
            container.insertBefore(draggedElement, afterElement);
        }
    });
}

// Helper function to determine drop position
function getDragAfterElement(container, y) {
    const draggableElements = [...container.querySelectorAll('.reorder-employee-item:not(.dragging)')];
    
    return draggableElements.reduce((closest, child) => {
        const box = child.getBoundingClientRect();
        const offset = y - box.top - box.height / 2;
        
        if (offset < 0 && offset > closest.offset) {
            return { offset: offset, element: child };
        } else {
            return closest;
        }
    }, { offset: Number.NEGATIVE_INFINITY }).element;
}

// Save employee order to Firestore
async function saveEmployeeOrder() {
    const container = document.getElementById('reorderEmployeeList');
    if (!container) return;
    
    const items = container.querySelectorAll('.reorder-employee-item');
    const order = Array.from(items).map(item => item.dataset.code);
    
    try {
        const orderData = {
            id: `${currentScheduleCategory}_order`,
            category: currentScheduleCategory,
            order: order,
            lastUpdated: new Date().toISOString(),
            updatedBy: currentUser.code || currentUser.username
        };
        
        await saveToFirestore('employee_order', orderData);
        
        showNotification('✓ Employee order saved successfully');
        closeModal();
        
        // Reload schedule to show new order
        loadHRSchedule();
        
    } catch (error) {
        console.error('Error saving employee order:', error);
        showNotification('❌ Error saving order');
    }
}

// Get saved employee order from Firestore
async function getEmployeeOrder(category) {
    try {
        const allOrders = await getFromFirestore('employee_order');
        return allOrders.find(o => o.category === category);
    } catch (error) {
        console.error('Error loading employee order:', error);
        return null;
    }
}

// ============================================
// SIMPLE EXCEL-LIKE COPY/PASTE SYSTEM
// ============================================

// Keyboard shortcuts for schedule
document.addEventListener('keydown', function(e) {
    const panel = document.getElementById('hrSchedulePanel');
    if (!panel || panel.style.display !== 'block') return;
    if (!currentUser || (currentUser.role !== 'hr' && currentUser.role !== 'admin')) return;
    
    // Ctrl+C - Copy
    if ((e.ctrlKey || e.metaKey) && e.key.toLowerCase() === 'c') {
        e.preventDefault();
        excelCopy();
        return;
    }
    
    // Ctrl+V - Paste
    if ((e.ctrlKey || e.metaKey) && e.key.toLowerCase() === 'v') {
        e.preventDefault();
        excelPaste();
        return;
    }
    
    // Delete or Backspace - Clear cells
    if (e.key === 'Delete' || e.key === 'Backspace') {
        e.preventDefault();
        excelDelete();
        return;
    }
    
    // Escape - Clear selection
    if (e.key === 'Escape') {
        e.preventDefault();
        excelClearSelection();
        return;
    }
});

// Mouse selection for schedule cells
document.addEventListener('mousedown', function(e) {
    const panel = document.getElementById('hrSchedulePanel');
    if (!panel || panel.style.display !== 'block') return;
    if (!currentUser || (currentUser.role !== 'hr' && currentUser.role !== 'admin')) return;
    
    const cell = e.target.closest('.shift-cell');
    if (!cell || cell.classList.contains('employee-name')) return;
    
    e.preventDefault();
    isMouseSelecting = true;
    startCell = cell;
    
    // Clear previous selection
    excelClearSelection();
    
    // Select this cell
    cell.classList.add('selected');
    selectedCells = [cell];
});

document.addEventListener('mousemove', function(e) {
    if (!isMouseSelecting) return;
    
    const cell = e.target.closest('.shift-cell');
    if (!cell || cell.classList.contains('employee-name')) return;
    
    // Add to selection if not already
    if (!selectedCells.includes(cell)) {
        cell.classList.add('selected');
        selectedCells.push(cell);
    }
});

document.addEventListener('mouseup', function(e) {
    if (isMouseSelecting) {
        isMouseSelecting = false;
        startCell = null;
        
        if (selectedCells.length > 0) {
            console.log('Selected cells:', selectedCells.length);
        }
    }
});

// Double-click to edit note
document.addEventListener('dblclick', function(e) {
    const panel = document.getElementById('hrSchedulePanel');
    if (!panel || panel.style.display !== 'block') return;
    if (!currentUser || (currentUser.role !== 'hr' && currentUser.role !== 'admin')) return;
    
    const cell = e.target.closest('.shift-cell');
    if (!cell || cell.classList.contains('employee-name')) return;
    
    e.preventDefault();
    const empCode = cell.dataset.emp;
    const date = cell.dataset.date;
    if (empCode && date) {
        editCellNote(cell, empCode, date, e);
    }
});

// Right-click for menu
document.addEventListener('contextmenu', function(e) {
    const panel = document.getElementById('hrSchedulePanel');
    if (!panel || panel.style.display !== 'block') return;
    if (!currentUser || (currentUser.role !== 'hr' && currentUser.role !== 'admin')) return;
    
    const cell = e.target.closest('.shift-cell');
    if (!cell || cell.classList.contains('employee-name')) return;
    
    e.preventDefault();
    const empCode = cell.dataset.emp;
    const date = cell.dataset.date;
    if (empCode && date) {
        showScheduleCellMenu(e, empCode, date);
    }
});
//Drag logic schedule


// Excel-like Copy
async function excelCopy() {
    if (selectedCells.length === 0) {
        alert('No cells selected');
        return;
    }
    
    const schedules = await getFromFirestore('schedules');
    const cell = selectedCells[0];
    const empCode = cell.dataset.emp;
    const date = cell.dataset.date;
    const shift = schedules.find(s => s.empCode === empCode && s.date === date);
    
    if (shift && shift.start && shift.end && !shift.leaveType) {
        copiedShiftData = {
            start: shift.start,
            end: shift.end,
            duration: shift.duration,
            notes: shift.notes || ''
        };
        
        selectedCells.forEach(c => {
            c.style.outline = '2px dashed #27ae60';
            c.style.outlineOffset = '-2px';
        });
        
        showNotification(`✓ Copied shift: ${shift.start}-${shift.end}`);
    } else {
        showNotification('⚠️ No shift in selected cell');
    }
}

// Excel-like Paste
async function excelPaste() {
    if (!copiedShiftData) {
        alert('Nothing to paste. Copy a shift first (Ctrl+C)');
        return;
    }
    
    if (selectedCells.length === 0) {
        alert('Select cells to paste into');
        return;
    }
    
    const schedules = await getFromFirestore('schedules');
    let count = 0;
    const affectedEmployees = new Set(); // Track which employees were affected
    
    for (const cell of selectedCells) {
        if (cell.classList.contains('leave-approved') || cell.classList.contains('leave-pending')) {
            continue;
        }
        
        const empCode = cell.dataset.emp;
        const date = cell.dataset.date;
        const existing = schedules.find(s => s.empCode === empCode && s.date === date);
        
        // Check if data is actually changing
        const isChanging = !existing || 
                          existing.start !== copiedShiftData.start || 
                          existing.end !== copiedShiftData.end ||
                          existing.notes !== copiedShiftData.notes;
        
        if (!isChanging) {
            continue; // Skip if no change
        }
        
        const data = {
            empCode: empCode,
            date: date,
            start: copiedShiftData.start,
            end: copiedShiftData.end,
            duration: copiedShiftData.duration,
            notes: copiedShiftData.notes,
            createdBy: currentUser.code || currentUser.username,
            createdDate: new Date().toISOString(),
            category: currentScheduleCategory,
            status: 'draft'
        };
        
        if (existing) {
            await updateFirestoreDoc('schedules', existing.id, data);
        } else {
            data.id = `SHIFT_${Date.now()}_${count}_${Math.random().toString(36).substr(2, 9)}`;
            await saveToFirestore('schedules', data);
        }
        
        affectedEmployees.add(empCode);
        count++;
    }
    
    // Send ONE notification per affected employee (not per cell)
    // But DON'T send yet - only when published
    
    showNotification(`✓ Pasted to ${count} cells (${affectedEmployees.size} employees affected) - Will notify on publish`);
    setTimeout(() => loadHRSchedule(), 300);
}

// Excel-like Delete
async function excelDelete() {
    if (selectedCells.length === 0) {
        return;
    }
    
    if (!confirm(`Delete shifts from ${selectedCells.length} cells?`)) {
        return;
    }
    
    const schedules = await getFromFirestore('schedules');
    let count = 0;
    
    for (const cell of selectedCells) {
        const empCode = cell.dataset.emp;
        const date = cell.dataset.date;
        const shift = schedules.find(s => s.empCode === empCode && s.date === date);
        
        if (shift && !shift.leaveType) {
            const snapshot = await db.collection('schedules').get();
            for (const doc of snapshot.docs) {
                if (doc.data().id === shift.id) {
                    await doc.ref.delete();
                    count++;
                    break;
                }
            }
        }
    }
    
    showNotification(`✓ Deleted ${count} shifts`);
    setTimeout(() => loadHRSchedule(), 300);
}

// Excel-like Clear Selection
function excelClearSelection() {
    selectedCells.forEach(c => {
        c.classList.remove('selected');
        c.style.outline = '';
        c.style.outlineOffset = '';
    });
    selectedCells = [];
}

// Simple copy function
async function simpleCopy() {
    if (selectedCells.length === 0) {
        showNotification('No cells selected');
        return;
    }
    
    copiedData = [];
    const schedules = await getFromFirestore('schedules');
    
    for (const cell of selectedCells) {
        const empCode = cell.dataset.emp;
        const date = cell.dataset.date;
        const shift = schedules.find(s => s.empCode === empCode && s.date === date);
        
        if (shift && shift.start && shift.end && !shift.leaveType) {
            copiedData.push({
                start: shift.start,
                end: shift.end,
                duration: shift.duration,
                notes: shift.notes || ''
            });
        } else {
            copiedData.push(null);
        }
    }
    
    // Green flash
    selectedCells.forEach(c => {
        c.style.background = '#d4edda';
        setTimeout(() => c.style.background = '', 300);
    });
    
    const validCount = copiedData.filter(d => d !== null).length;
    showNotification(`Copied ${validCount} shifts. Ctrl+V to paste.`);
}

// Simple paste function
async function simplePaste() {
    if (copiedData.length === 0) {
        showNotification('Nothing to paste. Copy first.');
        return;
    }
    
    if (selectedCells.length === 0) {
        showNotification('Select cells to paste into');
        return;
    }
    
    const schedules = await getFromFirestore('schedules');
    const firstValidShift = copiedData.find(d => d !== null);
    
    if (!firstValidShift) {
        showNotification('No valid shift data copied');
        return;
    }
    
    let pastedCount = 0;
    
    for (const cell of selectedCells) {
        // Skip leave cells
        if (cell.classList.contains('leave-approved') || cell.classList.contains('leave-pending')) {
            continue;
        }
        
        const empCode = cell.dataset.emp;
        const date = cell.dataset.date;
        const existing = schedules.find(s => s.empCode === empCode && s.date === date);
        
        const shiftData = {
            empCode: empCode,
            date: date,
            start: firstValidShift.start,
            end: firstValidShift.end,
            duration: firstValidShift.duration,
            notes: firstValidShift.notes,
            createdBy: currentUser.code || currentUser.username,
            createdDate: new Date().toISOString(),
            category: currentScheduleCategory,
            status: 'draft'
        };
        
        if (existing) {
            await updateFirestoreDoc('schedules', existing.id, shiftData);
        } else {
            shiftData.id = `SHIFT_${Date.now()}_${Math.random()}`;
            await saveToFirestore('schedules', shiftData);
        }
        
        await sendScheduleNotification(empCode, date, firstValidShift.start, firstValidShift.end, 'updated');
        
        // Purple flash
        cell.style.background = '#e8daef';
        setTimeout(() => cell.style.background = '', 300);
        
        pastedCount++;
    }
    
    showNotification(`Pasted to ${pastedCount} cells`);
    
    setTimeout(() => {
        loadHRSchedule();
        simpleClear();
    }, 500);
}

// Simple clear function
function simpleClear() {
    document.querySelectorAll('.shift-cell.selected').forEach(c => {
        c.classList.remove('selected');
        c.style.background = '';
    });
    selectedCells = [];
    copiedData = [];
    showNotification('Selection cleared');
}


async function pasteToSingleCell(empCode, date) {
    if (!copiedShift || copiedShift.length === 0) {
        showNotification('⚠️ Nothing to paste. Copy a shift first.');
        return;
    }
    
    // Get first valid copied shift
    const firstValidShift = copiedShift.find(s => s !== null);
    
    if (!firstValidShift) {
        showNotification('⚠️ No valid shift data copied');
        return;
    }
    
    // Find the target cell
    const targetCell = document.querySelector(`[data-emp="${empCode}"][data-date="${date}"]`);
    
    if (!targetCell) {
        showNotification('⚠️ Target cell not found');
        return;
    }
    
    // Don't paste on leave cells
    if (targetCell.classList.contains('leave-approved') || targetCell.classList.contains('leave-pending')) {
        showNotification('⚠️ Cannot paste on leave day');
        return;
    }
    
    try {
        const allSchedules = await getFromFirestore('schedules');
        const existingShift = allSchedules.find(s => s.empCode === empCode && s.date === date);
        
        const newShiftData = {
            empCode: empCode,
            date: date,
            start: firstValidShift.start,
            end: firstValidShift.end,
            duration: firstValidShift.duration,
            notes: firstValidShift.notes || '',
            createdBy: currentUser.code || currentUser.username,
            createdDate: new Date().toISOString(),
            category: currentScheduleCategory
        };
        
        if (existingShift) {
            await updateFirestoreDoc('schedules', existingShift.id, newShiftData);
        } else {
            newShiftData.id = `SHIFT_${Date.now()}`;
            await saveToFirestore('schedules', newShiftData);
        }
        
        // Send notification
        await sendScheduleNotification(empCode, date, firstValidShift.start, firstValidShift.end, 'updated');
        
        // Visual feedback
        targetCell.style.outline = '3px solid #9b59b6';
        targetCell.style.outlineOffset = '-2px';
        setTimeout(() => {
            if (targetCell) {
                targetCell.style.outline = '';
                targetCell.style.outlineOffset = '';
            }
        }, 800);
        
        showNotification(`✓ Pasted shift to ${authorizedEmployees[empCode]?.name || empCode}`);
        loadHRSchedule();
        
    } catch (error) {
        console.error('Error pasting shift:', error);
        showNotification('❌ Error pasting shift');
    }
}

async function publishScheduleUpdates() {
    try {
        const allSchedules = await getFromFirestore('schedules');
        const draftSchedules = allSchedules.filter(s => 
            s.category === currentScheduleCategory && 
            s.status === 'draft'
        );
        
        if (draftSchedules.length === 0) {
            showNotification('No unpublished changes to publish');
            return;
        }
        
        const confirmed = confirm(`Publish ${draftSchedules.length} draft shifts for ${currentScheduleCategory}?\n\nThis will notify affected employees.`);
        if (!confirmed) return;
        
        showNotification('Publishing...');
        
        // Group drafts by employee
        const employeeChanges = new Map();
        
        for (const shift of draftSchedules) {
            if (!employeeChanges.has(shift.empCode)) {
                employeeChanges.set(shift.empCode, []);
            }
            employeeChanges.get(shift.empCode).push(shift);
        }
        
        // Update all drafts to published
        const updatePromises = [];
        
        for (const shift of draftSchedules) {
            updatePromises.push(
                updateFirestoreDoc('schedules', shift.id, {
                    status: 'published',
                    publishedDate: new Date().toISOString(),
                    publishedBy: currentUser.code || currentUser.username
                })
            );
        }
        
        await Promise.all(updatePromises);
        
       // Send ONE notification per employee
		const notificationPromises = [];

		for (const [empCode, shifts] of employeeChanges.entries()) {
			// Delete OLD unacknowledged notifications for this employee
			const existingNotifs = await getFromFirestore('schedule_notifications');
			const oldNotifs = existingNotifs.filter(n => 
				n.empCode === empCode && 
				!n.acknowledged
			);
			
			// Delete old notifications
			const snapshot = await db.collection('schedule_notifications').get();
			for (const doc of snapshot.docs) {
				const data = doc.data();
				if (oldNotifs.some(n => n.id === data.id)) {
					await doc.ref.delete();
				}
			}
			
			// Send ONE new notification
			notificationPromises.push(
				sendScheduleNotification(empCode, null, null, null, 'published')
			);
		}

		await Promise.all(notificationPromises);
        
        showNotification(`✓ Published ${draftSchedules.length} shifts to ${employeeChanges.size} employees`);
        loadHRSchedule();
        
    } catch (error) {
        console.error('Error publishing schedule:', error);
        showNotification('Error publishing schedule updates');
    }
}

function selectScheduleCell(cell, empCode, date) {
    // Don't interfere with new mouse selection system
    // But keep cell reference for context menu
    selectedCell = cell;
    lastSelectedCell = cell;
}

async function editShift(empCode, date) {
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') return;
    
    // Load existing shifts for this day
    const allSchedules = await getFromFirestore('schedules');
    const existingShifts = allSchedules.filter(s => 
        s.empCode === empCode && 
        s.date === date && 
        s.start && 
        s.end &&
        !s.leaveType
    );
    
    let shiftsHtml = '';
    if (existingShifts.length > 0) {
        shiftsHtml = `
            <div style="background: #e8f5e9; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
                <h4 style="margin-top: 0;">Existing Shifts (${existingShifts.length}):</h4>
                ${existingShifts.map((shift, idx) => `
                    <div style="display: flex; justify-content: space-between; align-items: center; padding: 8px; background: white; border-radius: 5px; margin-bottom: 8px;">
                        <span>
                            <strong>Shift ${idx + 1}:</strong> ${shift.start} - ${shift.end} 
                            (${shift.duration}h, ${shift.shiftType === 'extra' ? '⚡ Extra' : '📅 Regular'})
                            ${shift.isOvernightPart ? '<em style="color: #7f8c8d; font-size: 11px;"> - Overnight</em>' : ''}
                        </span>
                        <button onclick="deleteSpecificShift('${shift.id}', '${empCode}', '${date}')" class="btn" style="padding: 4px 8px; font-size: 11px; background: #e74c3c;">
                            🗑️
                        </button>
                    </div>
                `).join('')}
            </div>
        `;
    }
    
    const modal = createModal(`
        <h3>Manage Shifts</h3>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <p><strong>Employee:</strong> ${authorizedEmployees[empCode]?.name || empCode}</p>
            <p><strong>Date:</strong> ${formatDisplayDate(date)}</p>
        </div>
        
        ${shiftsHtml}
        
        <h4>Add New Shift:</h4>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin: 20px 0;">
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">Start Time (24h):</label>
                <input type="time" id="shiftStart" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
            </div>
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">End Time (24h):</label>
                <input type="time" id="shiftEnd" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
            </div>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Shift Type:</label>
            <select id="shiftType" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="regular">Regular Hours</option>
                <option value="extra">Extra Hours</option>
            </select>
            <small style="color: #7f8c8d; display: block; margin-top: 5px;">
                💡 Mark as "Extra" if this shift is overtime or additional hours
            </small>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Notes (optional):</label>
            <textarea id="shiftNotes" rows="3" placeholder="Optional notes..." 
                style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;"></textarea>
        </div>
        
        <div style="text-align: right; display: flex; gap: 10px; justify-content: flex-end;">
            <button onclick="saveNewShift('${empCode}', '${date}')" class="btn" style="background: #27ae60;">
                ➕ Add This Shift
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}


async function saveNewShift(empCode, date) {
    const start = document.getElementById('shiftStart').value;
    const end = document.getElementById('shiftEnd').value;
    const notes = document.getElementById('shiftNotes').value.trim();
    const shiftType = document.getElementById('shiftType').value;
    
    if (!start || !end) {
        alert('Please enter both start and end times');
        return;
    }
    
    // Calculate duration
    const [startH, startM] = start.split(':').map(Number);
    const [endH, endM] = end.split(':').map(Number);
    let duration = (endH * 60 + endM) - (startH * 60 + startM);
    
    const isOvernightShift = duration < 0;
    if (isOvernightShift) duration += 24 * 60;
    
    const durationHours = (duration / 60).toFixed(1);
    
    try {
        if (isOvernightShift) {
            // OVERNIGHT SHIFT: Split into 2 entries
            // Parse the date string manually to avoid timezone issues
const [year, month, day] = date.split('-').map(Number);
const nextDay = new Date(year, month - 1, day + 1);
const nextDayStr = `${nextDay.getFullYear()}-${String(nextDay.getMonth() + 1).padStart(2, '0')}-${String(nextDay.getDate()).padStart(2, '0')}`;
            
            const minutesUntilMidnight = (23 * 60 + 59) - (startH * 60 + startM) + 1;
            const minutesAfterMidnight = endH * 60 + endM;
            
            const day1Duration = (minutesUntilMidnight / 60).toFixed(1);
            const day2Duration = (minutesAfterMidnight / 60).toFixed(1);
            
            const shiftData1 = {
                empCode: empCode,
                date: date,
                start: start,
                end: '23:59',
                duration: day1Duration,
                shiftType: shiftType,
                notes: notes ? `${notes} (Part 1)` : '(Overnight Part 1)',
                createdBy: currentUser.code || currentUser.username,
                createdDate: new Date().toISOString(),
                category: currentScheduleCategory,
                status: 'draft',
                isOvernightPart: true,
                overnightGroup: `${empCode}_${date}_${start}_${end}`,
                id: `SHIFT_${Date.now()}_0_${Math.random().toString(36).substr(2, 9)}`
            };
            
            const shiftData2 = {
                empCode: empCode,
                date: nextDayStr,
                start: '00:00',
                end: end,
                duration: day2Duration,
                shiftType: shiftType,
                notes: notes ? `${notes} (Part 2)` : '(Overnight Part 2)',
                createdBy: currentUser.code || currentUser.username,
                createdDate: new Date().toISOString(),
                category: currentScheduleCategory,
                status: 'draft',
                isOvernightPart: true,
                overnightGroup: `${empCode}_${date}_${start}_${end}`,
                id: `SHIFT_${Date.now()}_1_${Math.random().toString(36).substr(2, 9)}`
            };
            
            await saveToFirestore('schedules', shiftData1);
            await saveToFirestore('schedules', shiftData2);
            
            showNotification(`✅ Overnight shift added: ${date} (${day1Duration}h) + ${nextDayStr} (${day2Duration}h)`);
            
        } else {
            // NORMAL SHIFT: Just add, don't delete anything
            const shiftData = {
                empCode: empCode,
                date: date,
                start: start,
                end: end,
                duration: durationHours,
                shiftType: shiftType,
                notes: notes,
                createdBy: currentUser.code || currentUser.username,
                createdDate: new Date().toISOString(),
                category: currentScheduleCategory,
                status: 'draft',
                id: `SHIFT_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`
            };
            
            await saveToFirestore('schedules', shiftData);
            showNotification('✅ Shift added successfully');
        }
        
        loadHRSchedule();
        
        // Reopen modal to show updated list
        setTimeout(() => editShift(empCode, date), 300);
        
    } catch (error) {
        console.error('Error saving shift:', error);
        alert('❌ Error saving shift. Please try again.');
    }
}

async function deleteShift(empCode, date) {
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') {
        alert('Access Denied: Only HR and administrators can delete schedules');
        return;
    }
    
    if (!confirm('Delete this shift? (Overnight shifts: both parts deleted)')) return;
    
    try {
        const snapshot = await db.collection('schedules')
            .where('empCode', '==', empCode)
            .where('date', '==', date)
            .get();
        
        if (!snapshot.empty) {
            const shiftData = snapshot.docs[0].data();
            
            // Check if part of overnight shift
            if (shiftData.isOvernightPart && shiftData.overnightGroup) {
                const allParts = await db.collection('schedules')
                    .where('overnightGroup', '==', shiftData.overnightGroup)
                    .get();
                
                for (const doc of allParts.docs) {
                    await doc.ref.delete();
                }
                
                showNotification('✅ Overnight shift (both parts) deleted');
            } else {
                await snapshot.docs[0].ref.delete();
                showNotification('✅ Shift deleted');
            }
            
            await sendScheduleNotification(empCode, date, null, null, 'deleted');
            
            closeModal();
            loadHRSchedule();
        }
        
    } catch (error) {
        console.error('Error deleting shift:', error);
        alert('❌ Error deleting shift');
    }
}

async function deleteSpecificShift(shiftId, empCode, date) {
    if (!confirm('Delete this shift?')) return;
    
    try {
        const snapshot = await db.collection('schedules').where('id', '==', shiftId).get();
        
        if (!snapshot.empty) {
            const shiftData = snapshot.docs[0].data();
            
            // Check if part of overnight shift
            if (shiftData.isOvernightPart && shiftData.overnightGroup) {
                const allParts = await db.collection('schedules')
                    .where('overnightGroup', '==', shiftData.overnightGroup)
                    .get();
                
                for (const doc of allParts.docs) {
                    await doc.ref.delete();
                }
                
                showNotification('✅ Overnight shift (both parts) deleted');
            } else {
                await snapshot.docs[0].ref.delete();
                showNotification('✅ Shift deleted');
            }
            
            loadHRSchedule();
            
            // Reopen modal to show updated list
            setTimeout(() => editShift(empCode, date), 300);
        }
        
    } catch (error) {
        console.error('Error deleting shift:', error);
        alert('❌ Error deleting shift');
    }
}

function showScheduleCellMenu(event, empCode, date) {
    event.preventDefault();
    
    // Remove existing menu
    const existingMenu = document.getElementById('scheduleCellMenu');
    if (existingMenu) existingMenu.remove();
    
    const menu = document.createElement('div');
    menu.id = 'scheduleCellMenu';
			menu.style.cssText = `
				position: fixed;
				background: white;
				border: 2px solid #3498db;
				border-radius: 8px;
				box-shadow: 0 4px 15px rgba(0,0,0,0.3);
				z-index: 10000;
				padding: 5px 0;
				min-width: 180px;
			`;
    
    const employeeName = authorizedEmployees[empCode]?.name || empCode;
    
    menu.innerHTML = `
        <div style="padding: 8px 15px; background: #f8f9fa; font-weight: bold; border-bottom: 1px solid #dee2e6;">
            ${employeeName}
        </div>
        <div onclick="editShift('${empCode}', '${date}'); closeScheduleMenu();" 
             style="padding: 10px 15px; cursor: pointer; transition: all 0.2s;"
             onmouseover="this.style.background='#3498db'; this.style.color='white';"
             onmouseout="this.style.background='white'; this.style.color='#333';">
            🕐 Edit Shift Time
        </div>
        <div onclick="editCellNote(event.target.closest('td') || document.querySelector('[data-emp=\\'${empCode}\\'][data-date=\\'${date}\\']'), '${empCode}', '${date}', event); closeScheduleMenu();" 
             style="padding: 10px 15px; cursor: pointer; transition: all 0.2s;"
             onmouseover="this.style.background='#9b59b6'; this.style.color='white';"
             onmouseout="this.style.background='white'; this.style.color='#333';">
            📝 Quick Note
        </div>
        <div onclick="excelCopy(); closeScheduleMenu();" 
             style="padding: 10px 15px; cursor: pointer; transition: all 0.2s;"
             onmouseover="this.style.background='#27ae60'; this.style.color='white';"
             onmouseout="this.style.background='white'; this.style.color='#333';">
            📋 Copy Shift
        </div>
		<div onclick="excelPaste(); closeScheduleMenu();"
             style="padding: 10px 15px; cursor: pointer; transition: all 0.2s;"
             onmouseover="this.style.background='#9b59b6'; this.style.color='white';"
             onmouseout="this.style.background='white'; this.style.color='#333';">
            📥 Paste Shift
        </div>
        <div onclick="event.stopPropagation(); deleteShift('${empCode}', '${date}'); closeScheduleMenu();"
             style="padding: 10px 15px; cursor: pointer; transition: all 0.2s; border-top: 1px solid #dee2e6;"
             onmouseover="this.style.background='#e74c3c'; this.style.color='white';"
             onmouseout="this.style.background='white'; this.style.color='#333';">
            🗑️ Delete Shift (HR/Admin)
        </div>
    `;
    
    document.body.appendChild(menu);
	
	 // Calculate safe position
    const menuHeight = menu.offsetHeight;
    const menuWidth = menu.offsetWidth;
    const viewportHeight = window.innerHeight;
    const viewportWidth = window.innerWidth;

    let top = event.clientY;
    let left = event.clientX;

    if (top + menuHeight > viewportHeight) {
        top = viewportHeight - menuHeight - 10;
    }
    if (left + menuWidth > viewportWidth) {
        left = viewportWidth - menuWidth - 10;
    }

    menu.style.top = `${top}px`;
    menu.style.left = `${left}px`;
    
    // Select the cell when right-clicked
    const cell = document.querySelector(`[data-emp="${empCode}"][data-date="${date}"]`);
    if (cell) {
        selectedCell = cell;
        selectScheduleCell(cell, empCode, date);
    }
    
    // Close menu when clicking elsewhere
    setTimeout(() => {
        document.addEventListener('click', closeScheduleMenu);
    }, 100);
}

function closeScheduleMenu() {
    const menu = document.getElementById('scheduleCellMenu');
    if (menu) menu.remove();
    document.removeEventListener('click', closeScheduleMenu);
	// ✅ Deselect previously selected cell
    if (selectedCell) {
        selectedCell.classList.remove('selected');
        selectedCell = null;
    }
}


async function editCellNote(cell, empCode, date, event) {
    event.stopPropagation();
    
    // Don't edit if already editing
    if (cell.querySelector('.note-input')) return;
    
    // Get existing shift data
    const allSchedules = await getFromFirestore('schedules');
    const shift = allSchedules.find(s => s.empCode === empCode && s.date === date);
    
    const currentNote = shift?.notes || '';
    
    // Create inline input
    const noteInput = document.createElement('input');
    noteInput.type = 'text';
    noteInput.className = 'note-input';
    noteInput.value = currentNote;
    noteInput.placeholder = 'Type note here...';
    noteInput.maxLength = 50;
    
    // Hide existing content temporarily
    const cellContent = Array.from(cell.children);
    cellContent.forEach(child => child.style.display = 'none');
    
    // Add input to cell
    cell.appendChild(noteInput);
    noteInput.focus();
    noteInput.select();
    
    // Save on Enter or blur
    const saveNote = async () => {
        const newNote = noteInput.value.trim();
        
        try {
            if (shift) {
                // Update existing shift/note
                await updateFirestoreDoc('schedules', shift.id, {
                    notes: newNote
                });
            } else if (newNote) {
                // Create new note-only entry
                const newShift = {
                    id: `SHIFT_${Date.now()}`,
                    empCode: empCode,
                    date: date,
                    notes: newNote,
                    createdBy: currentUser.code || currentUser.username,
                    createdDate: new Date().toISOString(),
                    category: currentScheduleCategory
                };
                await saveToFirestore('schedules', newShift);
            }
            
            // Reload schedule
            loadHRSchedule();
            
        } catch (error) {
            console.error('Error saving note:', error);
            showNotification('Error saving note');
            loadHRSchedule();
        }
    };
    
    // Save on Enter
    noteInput.addEventListener('keydown', (e) => {
        if (e.key === 'Enter') {
            e.preventDefault();
            saveNote();
        }
        if (e.key === 'Escape') {
            loadHRSchedule();
        }
    });
    
    // Save on blur
    noteInput.addEventListener('blur', () => {
        setTimeout(saveNote, 200);
    });
}

async function clearMonthSchedule() {
    const monthName = currentScheduleMonth.toLocaleDateString('en-US', { month: 'long', year: 'numeric' });
    
    if (!confirm(`Delete ALL ${currentScheduleCategory} schedules for ${monthName}? This cannot be undone!`)) return;
    
    // HR and Admin can clear monthly schedules
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') {
        alert('Only HR and admin can delete monthly schedules');
        return;
    }
    
    const verification = prompt(`Type "DELETE ${monthName}" to confirm:`);
    if (verification !== `DELETE ${monthName}`) {
        showNotification('Deletion cancelled');
        return;
    }
    
    try {
        const currentYear = currentScheduleMonth.getFullYear();
        const currentMonth = currentScheduleMonth.getMonth();
        
        const snapshot = await db.collection('schedules').get();
        const deletePromises = [];
        
        snapshot.forEach((doc) => {
            const data = doc.data();
            const shiftDate = new Date(data.date);
            if (data.category === currentScheduleCategory &&
                shiftDate.getFullYear() === currentYear &&
                shiftDate.getMonth() === currentMonth) {
                deletePromises.push(doc.ref.delete());
            }
        });
        
        await Promise.all(deletePromises);
        
        showNotification(`Deleted ${deletePromises.length} shifts from ${monthName}`);
        loadHRSchedule();
        
    } catch (error) {
        console.error('Error clearing month:', error);
        showNotification('Error clearing schedule');
    }
}
	
// Leave Request System
// Format date string for nice display (e.g., "Friday, December 27, 2025")
function formatDisplayDate(dateStr) {
    if (!dateStr) return '';
    
    // If it's ISO string with time, extract date only
    if (dateStr.includes('T')) {
        dateStr = dateStr.split('T')[0];
    }
    
    // Parse date string as local date (not UTC)
    const [year, month, day] = dateStr.split('-').map(Number);
    const date = new Date(year, month - 1, day);
    
    return date.toLocaleDateString('en-US', { 
        weekday: 'long', 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric' 
    });
}

// Format date+time string for display (e.g., "27/12/2025 14:30")
function formatDisplayDateTime(dateStr) {
    if (!dateStr) return '';
    
    // Create date in local timezone
    const date = new Date(dateStr);
    
    // Check if valid date
    if (isNaN(date.getTime())) return dateStr;
    
    // Get local components
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');
    
    return `${day}/${month}/${year} ${hours}:${minutes}`;
}

async function requestLeave() {
    const modal = createModal(`
        <h3>✈️ Request Leave</h3>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Leave Type:</label>
            <select id="leaveType" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="annual">Annual Leave</option>
                <option value="sick">Sick Leave</option>
                <option value="emergency">Emergency Leave</option>
                <option value="personal">Personal Leave</option>
            </select>
        </div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin: 20px 0;">
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">From Date:</label>
                <input type="date" id="leaveFromDate" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
            </div>
            <div>
                <label style="display: block; margin-bottom: 5px; font-weight: 500;">To Date:</label>
                <input type="date" id="leaveToDate" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
            </div>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Reason:</label>
            <textarea id="leaveReason" rows="4" placeholder="Please provide reason for leave..." 
                style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;"></textarea>
        </div>
        
        <div style="text-align: right;">
            <button onclick="submitLeaveRequest()" class="btn" style="background: #9b59b6; margin-right: 10px;">
                Submit Request
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Cancel</button>
        </div>
    `);
}
function datesOverlap(fromA, toA, fromB, toB) {
    const aStart = new Date(fromA);
    const aEnd   = new Date(toA);
    const bStart = new Date(fromB);
    const bEnd   = new Date(toB);
    return aStart <= bEnd && aEnd >= bStart;
}

async function submitLeaveRequest() {
    const leaveType = document.getElementById('leaveType').value;
    const fromDate = document.getElementById('leaveFromDate').value;
    const toDate = document.getElementById('leaveToDate').value;
    const reason = document.getElementById('leaveReason').value.trim();
    
    if (!fromDate || !toDate || !reason) {
        alert('Please fill in all fields');
        return;
    }
    
    const [fromY, fromM, fromD] = fromDate.split('-').map(Number);
	const [toY, toM, toD] = toDate.split('-').map(Number);
	if (new Date(fromY, fromM - 1, fromD) > new Date(toY, toM - 1, toD)) {
        alert('From date must be before To date');
        return;
    }
    
    // Check if dates were previously cancelled
    const wasCancelled = await checkCancelledLeaveDates(currentUser.code, fromDate, toDate);
    if (wasCancelled) {
        alert(`You previously cancelled leave for these dates (${fromDate} to ${toDate}). Please choose different dates.`);
        return;
    }
	
	// Check if there's already a pending/approved leave with rejected cancellation
		const existingLeaves = await getFromFirestore('leave_requests');
		const conflictingLeave = existingLeaves.find(req =>
			req.empCode === currentUser.code &&
			req.cancellationStatus === 'rejected' &&
			datesOverlap(req.fromDate, req.toDate, fromDate, toDate)
		);

		if (conflictingLeave) {
			alert(`You have an existing leave with rejected cancellation request overlapping these dates. Cannot create new leave.`);
			return;
		}
    
    // Calculate days
   
	const days = Math.ceil((new Date(toY, toM - 1, toD) - new Date(fromY, fromM - 1, fromD)) / (1000 * 60 * 60 * 24)) + 1;
    
    try {
        const leaveRequest = {
            id: `LEAVE_${Date.now()}`,
            empCode: currentUser.code,
            empName: currentUser.name,
            leaveType: leaveType,
            fromDate: fromDate,
            toDate: toDate,
            days: days,
            reason: reason,
            status: 'pending',
            requestDate: new Date().toISOString(),
            approvedBy: null,
            approvedDate: null,
            rejectionReason: null,
            cancellationStatus: 'none',
            wasCancelled: false
        };
        
        await saveToFirestore('leave_requests', leaveRequest);
        await updateLeaveBalance(currentUser.code, 0, days, -days);
        
        showNotification('Leave request submitted successfully!');
        closeModal();
        loadEmployeeSchedule();
        
    } catch (error) {
        console.error('Error submitting leave request:', error);
        alert('Error submitting leave request. Please try again.');
    }
}

async function showLeaveRequests() {
    const allRequests = await getFromFirestore('leave_requests');
    const pendingRequests = allRequests.filter(r => r.status === 'pending');
    const cancellationRequests = allRequests.filter(r => r.cancellationStatus === 'requested');
    
    // Update counter
    document.getElementById('leaveRequestCount').textContent = pendingRequests.length + cancellationRequests.length;
    
    const modal = createModal(`
        <h3>✈️ Leave Requests Management</h3>
        
        <div style="margin-bottom: 20px;">
            <button onclick="filterLeaveRequests('pending')" class="btn" style="background: #f39c12; margin-right: 10px;">
                Pending Requests (${pendingRequests.length})
            </button>
            <button onclick="filterLeaveRequests('cancellation')" class="btn" style="background: #e74c3c; margin-right: 10px;">
                Cancellation Requests (${cancellationRequests.length})
            </button>
            <button onclick="filterLeaveRequests('approved')" class="btn" style="background: #27ae60; margin-right: 10px;">
                Approved
            </button>
            <button onclick="filterLeaveRequests('rejected')" class="btn" style="background: #e74c3c;">
                Rejected
            </button>
        </div>
        
        <div id="leaveRequestsList" style="max-height: 500px; overflow-y: auto;">
            <!-- Leave requests will load here -->
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
    
    filterLeaveRequests('pending');
}

async function filterLeaveRequests(status) {
    const allRequests = await getFromFirestore('leave_requests');
    let filteredRequests = [];
    
    if (status === 'cancellation') {
        filteredRequests = allRequests.filter(r => r.cancellationStatus === 'requested');
    } else {
        filteredRequests = allRequests.filter(r => r.status === status);
    }
    
    const container = document.getElementById('leaveRequestsList');
    
    if (filteredRequests.length === 0) {
        container.innerHTML = '<div style="padding: 40px; text-align: center; color: #666;">No requests found</div>';
        return;
    }
    
    const statusColors = {
        pending: '#fff3cd',
        approved: '#d1ecf1',
        rejected: '#f8d7da',
        cancellation: '#ffe5b4'
    };
    
    if (status === 'cancellation') {
        // Cancellation requests view
        const html = filteredRequests.map(req => `
            <div style="background: ${statusColors.cancellation}; padding: 15px; margin: 10px 0; border-radius: 8px; border-left: 4px solid #f39c12;">
                <div style="display: flex; justify-content: space-between; align-items: start;">
                    <div style="flex: 1;">
                        <div style="font-weight: bold; margin-bottom: 5px; color: #e74c3c;">
                            🚨 CANCELLATION REQUEST
                        </div>
                        <div style="font-weight: bold; margin-bottom: 5px;">
                            ${req.empName} (${req.empCode})
                        </div>
                        <div style="font-size: 13px; color: #666; margin-bottom: 8px;">
                            <strong>Type:</strong> ${req.leaveType.toUpperCase()} | 
                            <strong>Duration:</strong> ${req.days} day(s)<br>
                            <strong>From:</strong> ${new Date(req.fromDate).toLocaleDateString()} | 
                            <strong>To:</strong> ${new Date(req.toDate).toLocaleDateString()}<br>
                            <strong>Originally Approved:</strong> ${new Date(req.approvedDate).toLocaleDateString()}<br>
                            <strong>Cancellation Requested:</strong> ${new Date(req.cancellationRequestDate).toLocaleDateString()}
                        </div>
                        <div style="background: white; padding: 10px; border-radius: 5px; font-size: 12px;">
                            <strong>Original Reason:</strong> ${req.reason}
                        </div>
                    </div>
                    <div style="display: flex; gap: 5px; margin-left: 15px; flex-direction: column;">
                        <button onclick="approveCancellation('${req.id}')" class="btn" style="background: #27ae60; padding: 8px 12px; font-size: 12px; white-space: nowrap;">
                            ✓ Approve Cancel
                        </button>
                        <button onclick="rejectCancellation('${req.id}')" class="btn" style="background: #e74c3c; padding: 8px 12px; font-size: 12px; white-space: nowrap;">
                            ✗ Reject Cancel
                        </button>
                    </div>
                </div>
            </div>
        `).join('');
        
        container.innerHTML = html;
        return;
    }
    
    // Regular leave requests view
   const html = filteredRequests.map(req => `
        <div style="background: ${statusColors[req.status]}; padding: 15px; margin: 10px 0; border-radius: 8px; border-left: 4px solid ${status === 'pending' ? '#ff8c00' : status === 'approved' ? '#0d6efd' : '#dc3545'};">
            <div style="display: flex; justify-content: space-between; align-items: start;">
                <div style="flex: 1;">
                    <div style="font-weight: bold; margin-bottom: 5px;">
                        ${req.empName} (${req.empCode})
                    </div>
                    <div style="font-size: 13px; color: #666; margin-bottom: 8px;">
                        <strong>Type:</strong> ${req.leaveType.toUpperCase()} | 
                        <strong>Duration:</strong> ${req.days} day(s)<br>
                        <strong>From:</strong> ${formatDisplayDate(req.fromDate)} | 
                        <strong>To:</strong> ${formatDisplayDate(req.toDate)}<br>
                        <strong>Requested:</strong> ${formatDisplayDateTime(req.requestDate)}
                    </div>
                    <div style="background: white; padding: 10px; border-radius: 5px; font-size: 12px;">
                        <strong>Reason:</strong> ${req.reason}
                    </div>
                    ${req.rejectionReason ? `
                        <div style="background: #f8d7da; padding: 10px; border-radius: 5px; font-size: 12px; margin-top: 8px;">
                            <strong>Rejection Reason:</strong> ${req.rejectionReason}
                        </div>
                    ` : ''}
                </div>
                ${req.status === 'pending' ? `
                    <div style="display: flex; gap: 5px; margin-left: 15px;">
                        <button onclick="approveLeave('${req.id}')" class="btn" style="background: #27ae60; padding: 8px 12px; font-size: 12px;">
                            ✓ Approve
                        </button>
                        <button onclick="rejectLeave('${req.id}')" class="btn" style="background: #e74c3c; padding: 8px 12px; font-size: 12px;">
                            ✗ Reject
                        </button>
                    </div>
                ` : ''}
            </div>
        </div>
    `).join('');
    
    container.innerHTML = html;
}

async function approveCancellation(requestId) {
    try {
        const snapshot = await db.collection('leave_requests')
            .where('id', '==', requestId)
            .get();
        
        if (snapshot.empty) {
            alert('Leave request not found');
            return;
        }
        
        const doc = snapshot.docs[0];
        const request = doc.data();
        
        if (!confirm(`Approve cancellation for ${request.empName}?\n\nLeave: ${formatDisplayDate(request.fromDate)} to ${formatDisplayDate(request.toDate)}`)) {
            return;
        }
        
        // Update request status
        await doc.ref.update({
            cancellationStatus: 'approved',
            cancellationApprovedDate: new Date().toISOString(),
            cancellationApprovedBy: currentUser.code || currentUser.username,
            status: 'cancelled'
        });
        
        // Remove from schedule
        const allSchedules = await getFromFirestore('schedules');
        const leaveSchedules = allSchedules.filter(s => 
            s.empCode === request.empCode &&
            s.date >= request.fromDate &&
            s.date <= request.toDate &&
            s.leaveType === 'approved'
        );
        
        const scheduleSnapshot = await db.collection('schedules').get();
        for (const scheduleDoc of scheduleSnapshot.docs) {
            const scheduleData = scheduleDoc.data();
            if (leaveSchedules.some(ls => ls.id === scheduleData.id)) {
                await scheduleDoc.ref.delete();
            }
        }
        
        // Restore leave balance
        await updateLeaveBalance(request.empCode, -request.days, 0, request.days);
        
        // Save to history
        await saveToFirestore('leave_cancellation_history', {
            id: `CANCEL_${Date.now()}`,
            leaveRequestId: requestId,
            empCode: request.empCode,
            empName: request.empName,
            originalFromDate: request.fromDate,
            originalToDate: request.toDate,
            days: request.days,
            leaveType: request.leaveType,
            cancellationType: 'hr_approved',
            requestedDate: request.cancellationRequestDate,
            approvedDate: new Date().toISOString(),
            approvedBy: currentUser.code || currentUser.username
        });
        
        // Notify employee
        await sendCancellationNotification(request.empCode, 'approved', request.fromDate, request.toDate, null);
        
        showNotification('Leave cancellation approved. Schedule restored.');
        filterLeaveRequests('cancellation');
        
    } catch (error) {
        console.error('Error approving cancellation:', error);
        alert('Error approving cancellation. Please try again.');
    }
}

async function rejectCancellation(requestId) {
    const reason = prompt('Enter rejection reason (optional):');
    
    try {
        const snapshot = await db.collection('leave_requests')
            .where('id', '==', requestId)
            .get();
        
        if (snapshot.empty) {
            alert('Leave request not found');
            return;
        }
        
        const doc = snapshot.docs[0];
        const request = doc.data();
        
        // Update request status
        await doc.ref.update({
            cancellationStatus: 'rejected',
            cancellationRejectedDate: new Date().toISOString(),
            cancellationRejectedBy: currentUser.code || currentUser.username,
            cancellationRejectionReason: reason || 'No reason provided'
        });
        
        // Notify employee
        await sendCancellationNotification(request.empCode, 'rejected', request.fromDate, request.toDate, reason);
        
        showNotification('Cancellation request rejected');
        filterLeaveRequests('cancellation');
        
    } catch (error) {
        console.error('Error rejecting cancellation:', error);
        alert('Error rejecting cancellation. Please try again.');
    }
}

async function sendCancellationNotification(empCode, status, fromDate, toDate, reason) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const from = formatDisplayDate(fromDate);
    const to = formatDisplayDate(toDate);
    
    let message = '';
    let summary = '';
    
    if (status === 'approved') {
        message = `Your leave cancellation request for ${from} to ${to} has been APPROVED. Your schedule has been restored.`;
        summary = `Leave cancelled: ${from} - ${to}`;
    } else {
        message = `Your leave cancellation request for ${from} to ${to} has been REJECTED. ${reason ? 'Reason: ' + reason : 'No reason provided'}`;
        summary = `Cancellation denied: ${from} - ${to}`;
    }
    
    const notification = {
        id: `NOTIF_CANCEL_${Date.now()}`,
        empCode: empCode,
        type: 'leave_cancellation',
        message: message,
        summary: summary,
        status: status,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    // Send email
    await sendEmailNotification(employee.email, 'Leave Cancellation Update', message, summary);
}

async function approveLeave(requestId) {
    try {
        const snapshot = await db.collection('leave_requests')
            .where('id', '==', requestId)
            .get();
        
        if (snapshot.empty) {
            alert('Leave request not found');
            return;
        }
        
        const doc = snapshot.docs[0];
        const request = doc.data();
        
        // Update request status
        await doc.ref.update({
            status: 'approved',
            approvedBy: currentUser.code || currentUser.username,
            approvedDate: new Date().toISOString()
        });
        
        // Update leave balance
        await updateLeaveBalance(request.empCode, request.days, -request.days, 0);
        
        // Create leave entries in schedule
		// Fix: Use date strings directly to avoid timezone conversion
		const fromDateStr = request.fromDate;
		const toDateStr = request.toDate;

		// Parse dates properly in local timezone
		const [fromYear, fromMonth, fromDay] = fromDateStr.split('-').map(Number);
		const [toYear, toMonth, toDay] = toDateStr.split('-').map(Number);

		const fromDate = new Date(fromYear, fromMonth - 1, fromDay);
		const toDate = new Date(toYear, toMonth - 1, toDay);

		for (let d = new Date(fromDate); d <= toDate; d.setDate(d.getDate() + 1)) {
			const year = d.getFullYear();
			const month = String(d.getMonth() + 1).padStart(2, '0');
			const day = String(d.getDate()).padStart(2, '0');
			const dateStr = `${year}-${month}-${day}`;
            
            const leaveEntry = {
                id: `LEAVE_${Date.now()}_${Math.random()}`,
                empCode: request.empCode,
                date: dateStr,
                leaveType: 'approved',
                leaveCategory: request.leaveType,
                approvedBy: currentUser.code || currentUser.username,
                category: authorizedEmployees[request.empCode]?.category || 'RAD'
            };
            
            await saveToFirestore('schedules', leaveEntry);
        }
        
        // Send notification to employee
        await sendLeaveNotification(request.empCode, 'approved', request.fromDate, request.toDate, null);
        
        showNotification('Leave approved successfully!');
        filterLeaveRequests('pending');
        
    } catch (error) {
        console.error('Error approving leave:', error);
        alert('Error approving leave. Please try again.');
    }
}

async function rejectLeave(requestId) {
    const reason = prompt('Enter rejection reason:');
    if (!reason) return;
    
    try {
        const snapshot = await db.collection('leave_requests')
            .where('id', '==', requestId)
            .get();
        
        if (snapshot.empty) {
            alert('Leave request not found');
            return;
        }
        
        const doc = snapshot.docs[0];
        const request = doc.data();
        
        // Update request status
        await doc.ref.update({
            status: 'rejected',
            rejectionReason: reason,
            rejectedBy: currentUser.code || currentUser.username,
            rejectedDate: new Date().toISOString()
        });
        
        // Update leave balance (remove from pending)
        await updateLeaveBalance(request.empCode, 0, -request.days, request.days);
        
        // Send notification to employee
        await sendLeaveNotification(request.empCode, 'rejected', request.fromDate, request.toDate, reason);
        
        showNotification('Leave rejected');
        filterLeaveRequests('pending');
        
    } catch (error) {
        console.error('Error rejecting leave:', error);
        alert('Error rejecting leave. Please try again.');
    }
}

async function updateLeaveBalance(empCode, usedDelta, pendingDelta, availableDelta) {
    try {
        const snapshot = await db.collection('leave_balances')
            .where('empCode', '==', empCode)
            .get();
        
        let balance;
        let docRef;
        
        if (snapshot.empty) {
            // Create new balance record
            balance = {
                id: `BALANCE_${empCode}`,
                empCode: empCode,
                total: 30,
                used: 0,
                pending: 0,
                available: 30,
                year: new Date().getFullYear()
            };
            await saveToFirestore('leave_balances', balance);
            
            // Get the newly created document
            const newSnapshot = await db.collection('leave_balances')
                .where('empCode', '==', empCode)
                .get();
            docRef = newSnapshot.docs[0].ref;
            balance = newSnapshot.docs[0].data();
        } else {
            docRef = snapshot.docs[0].ref;
            balance = snapshot.docs[0].data();
        }
        
        // Calculate new values
        const newUsed = Math.max(0, balance.used + usedDelta);
        const newPending = Math.max(0, balance.pending + pendingDelta);
        const newAvailable = balance.total - newUsed - newPending;
        
        await docRef.update({
            used: newUsed,
            pending: newPending,
            available: newAvailable
        });
        
    } catch (error) {
        console.error('Error updating leave balance:', error);
    }
}

// Check if employee previously cancelled leave for same dates
async function checkCancelledLeaveDates(empCode, fromDate, toDate) {
    try {
        const history = await getFromFirestore('leave_cancellation_history');
        
        const match = history.find(h => 
            h.empCode === empCode &&
            h.originalFromDate === fromDate &&
            h.originalToDate === toDate
        );
        
        return match ? true : false;
        
    } catch (error) {
        console.error('Error checking cancelled dates:', error);
        return false;
    }
}

// Notification System
// Notification System
async function sendScheduleNotification(empCode, date, start, end, action) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const dateStr = formatDisplayDate(date);
    
    let message = '';
    let summary = '';
    
    switch(action) {
        case 'updated':
        case 'assigned':
            message = `New shift assigned for ${dateStr}: ${start} - ${end}`;
            summary = `Shift: ${start}-${end} on ${dateStr}`;
            break;
        case 'moved':
            message = `Your shift has been moved to ${dateStr}: ${start} - ${end}`;
            summary = `Shift moved to ${dateStr}: ${start}-${end}`;
            break;
        case 'deleted':
            message = `Your shift on ${dateStr} has been cancelled`;
            summary = `Shift cancelled: ${dateStr}`;
            break;
        case 'published': 
            message = `Schedule updated!! Please check your schedule for the latest changes.`;
            summary = `Schedule updated - check your shifts`;
            break;
    }
    
    const existingNotifs = await getFromFirestore('schedule_notifications');
    const oldNotifs = existingNotifs.filter(n => 
        n.empCode === empCode && 
        !n.acknowledged &&
        n.type === 'schedule'
    );
    const snapshot = await db.collection('schedule_notifications').get();
    for (const doc of snapshot.docs) {
        const data = doc.data();
        if (oldNotifs.some(n => n.id === data.id)) {
            await doc.ref.delete();
        }
    }
        
    // Create notification record
    const notification = {
        id: `NOTIF_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`,
        empCode: empCode,
        type: 'schedule',
        message: message,
        summary: summary,
        date: date,
        start: start,
        end: end,
        action: action,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    // Send email if employee is offline
    await sendEmailNotification(employee.email, 'Schedule Update', message, summary);
}

async function sendLeaveNotification(empCode, status, fromDate, toDate, reason) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const from = formatDisplayDate(fromDate);
    const to = formatDisplayDate(toDate);
    
    let message = status === 'approved' 
        ? `Your leave request from ${from} to ${to} has been APPROVED`
        : `Your leave request from ${from} to ${to} has been REJECTED. Reason: ${reason}`;
    
    let summary = status === 'approved'
        ? `Leave approved: ${from} - ${to}`
        : `Leave rejected: ${from} - ${to}`;
    
    const notification = {
        id: `NOTIF_${Date.now()}`,
        empCode: empCode,
        type: 'leave',
        message: message,
        summary: summary,
        status: status,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    // Send email
    await sendEmailNotification(employee.email, 'Leave Request Update', message, summary);
}

async function sendEmailNotification(email, subject, message, summary) {
    // This would integrate with your email service
    // For now, we'll just log it
    console.log('Email Notification:', {
        to: email,
        subject: subject,
        message: message,
        summary: summary
    });
    
    // You would integrate with EmailJS, SendGrid, or your backend email service here
}

async function checkPendingScheduleNotifications() {
    if (!currentUser || currentUser.role !== 'employee') return;
    
    // CRITICAL: Don't show if badge already visible
    if (document.querySelector('.notification-badge')) {
        console.log('Notification badge already showing, skipping...');
        return;
    }
    
    const allNotifications = await getFromFirestore('schedule_notifications');
    const pendingNotifications = allNotifications.filter(n => 
        n.empCode === currentUser.code && 
        !n.acknowledged
    );
    
    if (pendingNotifications.length > 0) {
        console.log(`Showing ${pendingNotifications.length} pending notifications`);
        showScheduleNotificationBadge(pendingNotifications);
    }
}

function showScheduleNotificationBadge(notifications) {
    // CRITICAL: Double-check badge doesn't exist
    const existing = document.querySelector('.notification-badge');
    if (existing) {
        console.log('Badge already exists, not creating another');
        return;
    }
    
    const notif = notifications[0];
    
    const badge = document.createElement('div');
    badge.className = 'notification-badge';
    badge.innerHTML = `
        <h3>📅 Schedule Update</h3>
        <p>${notif.message}</p>
        <p style="font-size: 14px; margin-top: 10px;"><strong>Summary:</strong> ${notif.summary}</p>
        <p style="font-size: 12px; color: rgba(255,255,255,0.8); margin-top: 10px;">
            ${notifications.length > 1 ? `+${notifications.length - 1} more notification(s)` : ''}
        </p>
        <button class="accept-btn" onclick="acknowledgeAllNotifications()">
            ✓ Accept ${notifications.length > 1 ? 'All' : ''} & Acknowledge
        </button>
    `;
    
    document.body.appendChild(badge);
}

async function acknowledgeNotification(notifId) {
    try {
        const snapshot = await db.collection('schedule_notifications')
            .where('id', '==', notifId)
            .get();
        
        if (snapshot.empty) {
            console.error('Notification not found:', notifId);
            return;
        }
        
        await snapshot.docs[0].ref.update({
            acknowledged: true,
            acknowledgedDate: new Date().toISOString()
        });
        
        // Remove badge
        const badges = document.querySelectorAll('.notification-badge');
        badges.forEach(badge => badge.remove());
        
        // Check for more notifications
        setTimeout(() => {
            checkPendingScheduleNotifications();
        }, 500);
        
    } catch (error) {
        console.error('Error acknowledging notification:', error);
    }
}
async function acknowledgeAllNotifications() {
    try {
        const snapshot = await db.collection('schedule_notifications')
            .where('empCode', '==', currentUser.code)
            .where('acknowledged', '==', false)
            .get();
        
        console.log(`Found ${snapshot.size} unacknowledged notifications`);
        
        const updatePromises = [];
        snapshot.forEach((doc) => {
            console.log('Acknowledging notification:', doc.id);
            updatePromises.push(
                doc.ref.update({
                    acknowledged: true,
                    acknowledgedDate: new Date().toISOString()
                })
            );
        });
        
        await Promise.all(updatePromises);
        
        // Remove ALL badges
        document.querySelectorAll('.notification-badge').forEach(badge => badge.remove());
        
        showNotification(`✓ Acknowledged ${snapshot.size} notification(s)`);
        
    } catch (error) {
        console.error('Error acknowledging notifications:', error);
        alert('Error acknowledging notifications');
    }
}

async function exportScheduleData() {
    try {
        const allSchedules = await getFromFirestore('schedules');
        const categorySchedules = allSchedules.filter(s => s.category === currentScheduleCategory);
        
        const csv = convertScheduleToCSV(categorySchedules);
        downloadCSV(csv, `schedule_${currentScheduleCategory}_${currentScheduleMonth.toISOString().split('T')[0]}.csv`);
        
        showNotification('Schedule exported successfully!');
        
    } catch (error) {
        console.error('Error exporting schedule:', error);
        showNotification('Error exporting schedule');
    }
}

function convertScheduleToCSV(schedules) {
    const headers = ['Employee Code', 'Employee Name', 'Date', 'Day', 'Start Time', 'End Time', 'Duration (hours)', 'Notes', 'Type'];
    
    const rows = schedules.map(shift => {
        const employee = authorizedEmployees[shift.empCode];
        const empName = employee ? employee.name : shift.empCode;
        
        // Fix: Parse date properly to avoid timezone issues
        const [year, month, day] = shift.date.split('-').map(Number);
        const date = new Date(year, month - 1, day);
        const dayName = date.toLocaleDateString('en-US', { weekday: 'long' });
        
        const type = shift.leaveType ? (shift.leaveType === 'approved' ? 'Leave (Approved)' : 'Leave (Pending)') : 'Shift';
        
        return [
            shift.empCode,
            empName,
            shift.date,  // Keep as YYYY-MM-DD format for CSV
            dayName,
            shift.start || '-',
            shift.end || '-',
            shift.duration || '-',
            (shift.notes || '-').replace(/,/g, ';'),
            type
        ];
    });
    
    return [headers.join(','), ...rows.map(row => row.join(','))].join('\n');
}

// Reset leave balances on January 1st
async function checkAndResetLeaveBalances() {
    const today = new Date();
    const currentYear = today.getFullYear();
    
    // Only run on January 1st
    if (today.getMonth() !== 0 || today.getDate() !== 1) return;
    
    try {
        const allBalances = await getFromFirestore('leave_balances');
        
        for (const balance of allBalances) {
            if (balance.year < currentYear) {
                const carryOver = balance.available; // Carry over unused leave
                
                await updateFirestoreDoc('leave_balances', balance.id, {
                    year: currentYear,
                    total: 30 + carryOver,
                    used: 0,
                    pending: 0,
                    available: 30 + carryOver,
                    previousYearCarryOver: carryOver
                });
                
                console.log(`Reset leave for ${balance.empCode}: Carried over ${carryOver} days`);
            }
        }
        
    } catch (error) {
        console.error('Error resetting leave balances:', error);
    }
}

// Initialize leave balance for new employee
async function initializeLeaveBalance(empCode) {
    const currentYear = new Date().getFullYear();
    
    const balance = {
        id: `BALANCE_${empCode}`,
        empCode: empCode,
        total: 30,
        used: 0,
        pending: 0,
        available: 30,
        year: currentYear,
        previousYearCarryOver: 0
    };
    
    await saveToFirestore('leave_balances', balance);
}

// ==============================================
// MEETING MANAGEMENT SYSTEM
// ==============================================

let meetingAlertBannerVisible = false;
let autoPopupShown = false;
let lastNotifiedMeetingCount = 0;

// Initialize meeting system for employees
async function initializeMeetingSystem() {
    if (!currentUser || currentUser.role !== 'employee') return;
    
    await checkPendingMeetingInvitations();
    setupMeetingListeners();
}

// Setup real-time listeners for meetings
function setupMeetingListeners() {
    if (currentUser.role === 'employee' || currentUser.role === 'admin') {
        const meetingListener = db.collection('meetings')
            .where('participants', 'array-contains', currentUser.code)
            .onSnapshot((snapshot) => {
                // Update badge counter
                checkPendingMeetingInvitations();
                
                // If meetings panel is open, reload it
                const meetingsPanel = document.getElementById('empMeetingsPanel');
                if (meetingsPanel && meetingsPanel.style.display === 'block') {
                    loadEmployeeMeetingsPanel();
                }
            });
        unsubscribeListeners.push(meetingListener);
    }
}

async function checkPendingMeetingInvitations() {
    if (!currentUser || (currentUser.role !== 'employee' && currentUser.role !== 'admin')) return;
    
    const allMeetings = await getFromFirestore('meetings');
    const now = new Date();
    now.setHours(0, 0, 0, 0);
    
    // Calculate 30 days from now
    const thirtyDaysFromNow = new Date(now);
    thirtyDaysFromNow.setDate(thirtyDaysFromNow.getDate() + 30);
    
    const upcomingMeetings = allMeetings.filter(meeting => {
        if (!meeting.participants || !meeting.participants.includes(currentUser.code)) return false;
        
        const meetingDate = new Date(meeting.date);
        
        // Only show meetings: today to +30 days, not cancelled
        return meetingDate >= now && 
               meetingDate <= thirtyDaysFromNow && 
               meeting.status !== 'cancelled';
    });
    
    // Update badge count
    updateMeetingBadge(upcomingMeetings.length);
}

function updateMeetingBadge(count) {
    const dropdownBadge = document.getElementById('empMeetingDropdownBadge');
    const eventsNotification = document.getElementById('empEventsNotification');
    
    if (count > 0) {
        if (dropdownBadge) {
            dropdownBadge.textContent = count;
            dropdownBadge.style.display = 'inline-block';
        }
        if (eventsNotification) {
            eventsNotification.textContent = count;
            eventsNotification.style.display = 'flex';
        }
    } else {
        if (dropdownBadge) dropdownBadge.style.display = 'none';
        if (eventsNotification) eventsNotification.style.display = 'none';
    }
}

// Render meeting card
function renderMeetingCard(meeting, isUrgent) {
    const meetingTime = new Date(meeting.date + 'T' + meeting.startTime);
    const now = new Date();
    const minutesUntil = Math.round((meetingTime - now) / (1000 * 60));
    const isToday = new Date(meeting.date).toDateString() === new Date().toDateString();
    
    // JOIN button: 15 min before to 30 min after start
    const canJoin = minutesUntil <= 15 && minutesUntil >= -30;
    const meetingStatus = minutesUntil > 15 ? 'upcoming' : minutesUntil > 0 ? 'starting-soon' : minutesUntil >= -30 ? 'ongoing' : 'ended';
    
    // Badge color based on time
    let badgeColor = '#95a5a6'; // Default gray
    let badgeText = '';
    
    if (minutesUntil > 1440) { // > 1 day
        badgeColor = '#27ae60'; // Green
        const daysUntil = Math.floor(minutesUntil / 1440);
        badgeText = `Starts in ${daysUntil} day${daysUntil > 1 ? 's' : ''}`;
    } else if (minutesUntil > 60) { // > 1 hour, < 1 day
        badgeColor = '#f39c12'; // Yellow/Orange
        const hoursUntil = Math.floor(minutesUntil / 60);
        badgeText = `Starts in ${hoursUntil} hour${hoursUntil > 1 ? 's' : ''}`;
    } else if (minutesUntil > 0) { // < 1 hour
        badgeColor = '#e74c3c'; // Red
        badgeText = `Starts in ${minutesUntil} minute${minutesUntil > 1 ? 's' : ''}`;
    } else if (minutesUntil >= -30) { // Meeting ongoing (within 30 min window)
        badgeColor = '#27ae60'; // Green (ongoing)
        badgeText = 'MEETING IN PROGRESS';
    }
   
    const attachmentsHtml = meeting.attachments && meeting.attachments.length > 0
        ? `
        <div class="meeting-attachments">
            <h4 style="font-size: 13px; color: #555; margin-bottom: 8px;">📎 Attachments (${meeting.attachments.length}):</h4>
            ${meeting.attachments.map(att => `
                <div class="attachment-item" onclick="downloadAttachment('${att.name}', '${att.url}')">
                    📄 ${att.name}
                </div>
            `).join('')}
        </div>
        ` : '';
    
    const organizer = authorizedEmployees[meeting.organizer];
    const organizerName = organizer ? organizer.name : meeting.organizer;
    
    return `
        <div class="meeting-card" style="border-left: 4px solid ${badgeColor};">
            <div class="meeting-card-header">
                <div>
                    <div class="meeting-title">${meeting.title}</div>
                    <span class="meeting-type-badge ${meeting.type.replace(' ', '-').toLowerCase()}">${meeting.type}</span>
                </div>
                ${isToday ? '<div style="background: #e74c3c; color: white; padding: 8px 12px; border-radius: 20px; font-size: 12px; font-weight: bold;">TODAY</div>' : ''}
            </div>
            
            ${badgeText ? `
                <div style="background: ${badgeColor}; color: white; padding: 12px; border-radius: 8px; text-align: center; font-weight: bold; margin: 15px 0;">
                    ${meetingStatus === 'ongoing' ? '🔴 ' : '⏰ '}${badgeText}
                </div>
            ` : ''}
            
            <div class="meeting-details">
                <div class="meeting-detail-item">
                    <strong>📅 Date:</strong> ${new Date(meeting.date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
                </div>
                <div class="meeting-detail-item">
                    <strong>⏰ Time:</strong> ${meeting.startTime} - ${meeting.endTime}
                </div>
                <div class="meeting-detail-item">
                    <strong>📍 Location:</strong> ${meeting.location || 'Virtual Meeting'}
                </div>
                <div class="meeting-detail-item">
                    <strong>👤 Organizer:</strong> ${organizerName}
                </div>
            </div>
            
            ${meeting.agenda ? `
                <div class="meeting-agenda">
                    <h4>📋 Agenda:</h4>
                    <div style="white-space: pre-wrap; line-height: 1.6;">${meeting.agenda}</div>
                </div>
            ` : ''}
            
            ${meeting.notes ? `
                <div style="background: #e3f2fd; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #3498db;">
                    <h4 style="margin: 0 0 10px 0; color: #3498db; font-size: 14px;">📝 Additional Notes:</h4>
                    <div style="white-space: pre-wrap; line-height: 1.6;">${meeting.notes}</div>
                </div>
            ` : ''}
            
            ${meeting.joinLink && canJoin ? `
                <div style="margin: 15px 0;">
                    ${meetingStatus === 'ongoing' ? `
                        <div style="background: linear-gradient(135deg, #27ae60, #229954); color: white; padding: 15px; border-radius: 8px; text-align: center; font-weight: bold; margin-bottom: 15px; animation: pulse 2s infinite;">
                            🔴 MEETING IN PROGRESS - JOIN NOW
                        </div>
                    ` : meetingStatus === 'starting-soon' ? `
                        <div style="background: #fff3cd; padding: 12px; border-radius: 8px; text-align: center; font-weight: bold; color: #856404; margin-bottom: 15px;">
                            ⏰ Meeting starts in ${minutesUntil} minute(s)
                        </div>
                    ` : ''}
                    
                    <div style="background: #e3f2fd; padding: 15px; border-radius: 8px; border-left: 4px solid #3498db;">
                        <div style="font-weight: bold; color: #2c3e50; margin-bottom: 10px;">🔗 Meeting Link:</div>
                        <button onclick="joinMeeting('${meeting.id}', '${meeting.joinLink}')" 
                                style="width: 100%; padding: 15px; background: linear-gradient(135deg, #27ae60, #229954); color: white; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; border: 3px solid #1e8449;">
                            🎥 JOIN MEETING NOW
                        </button>
                    </div>
                </div>
            ` : !canJoin && meeting.joinLink ? `
                <div style="background: #f8f9fa; padding: 12px; border-radius: 5px; text-align: center; color: #666; margin: 15px 0;">
                    Join button will appear 15 minutes before the meeting
                </div>
            ` : ''}
        </div>
    `;
}

// Render cancelled meeting card for employees
function renderCancelledMeetingCard(meeting) {
    const organizer = authorizedEmployees[meeting.organizer];
    const organizerName = organizer ? organizer.name : meeting.organizer;
    
    return `
        <div class="meeting-card" style="background: #f8d7da; border-left: 4px solid #e74c3c; opacity: 0.9;">
            <div style="background: #e74c3c; color: white; padding: 10px; border-radius: 8px 8px 0 0; text-align: center; font-weight: bold; margin: -15px -15px 15px -15px;">
                ❌ MEETING CANCELLED
            </div>
            
            <div class="meeting-card-header">
                <div>
                    <div class="meeting-title" style="text-decoration: line-through;">${meeting.title}</div>
                    <span class="meeting-type-badge ${meeting.type.replace(' ', '-').toLowerCase()}" style="opacity: 0.6;">${meeting.type}</span>
                </div>
            </div>
            
            <div class="meeting-details">
                <div class="meeting-detail-item">
                    <strong>📅 Was scheduled for:</strong> ${new Date(meeting.date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
                </div>
                <div class="meeting-detail-item">
                    <strong>⏰ Time:</strong> ${meeting.startTime} - ${meeting.endTime}
                </div>
                <div class="meeting-detail-item">
                    <strong>📍 Location:</strong> ${meeting.location || 'Virtual Meeting'}
                </div>
                <div class="meeting-detail-item">
                    <strong>👤 Organizer:</strong> ${organizerName}
                </div>
            </div>
            
            ${meeting.cancellationReason ? `
                <div style="background: white; padding: 12px; border-radius: 5px; margin: 15px 0; border-left: 3px solid #e74c3c;">
                    <strong style="color: #e74c3c;">Cancellation Reason:</strong><br>
                    <span style="color: #666; font-size: 14px;">${meeting.cancellationReason}</span>
                </div>
            ` : ''}
            
            <div style="background: #fff3cd; padding: 10px; border-radius: 5px; text-align: center; font-size: 12px; color: #856404; margin-top: 15px;">
                This notification will be automatically removed shortly
            </div>
        </div>
    `;
}
				
function trackMeetingJoin(meetingId) {
    // This will track attendance even if user clicks the link directly
    joinMeeting(meetingId, null);
}


// Join meeting and track attendance
async function joinMeeting(meetingId, joinLink) {
    if (!joinLink) {
        alert('Meeting link not available. Please contact the organizer.');
        return;
    }
    
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        // Standard attendance tracking
        const attendance = meeting.attendance || {};
        const hasJoined = attendance[currentUser.code];
        
        if (!hasJoined) {
            const joinTime = new Date();
            const meetingStartTime = new Date(meeting.date + 'T' + meeting.startTime);
            const minutesLate = Math.round((joinTime - meetingStartTime) / (1000 * 60));
            
            // Calculate duration (meeting end - join time)
            const meetingEndTime = new Date(meeting.date + 'T' + meeting.endTime);
            const durationMinutes = Math.round((meetingEndTime - joinTime) / (1000 * 60));
            
            attendance[currentUser.code] = {
                empCode: currentUser.code,
                empName: currentUser.name,
                attendance: 'present',
                joinTime: joinTime.toISOString(),
                joinedLate: minutesLate > 0,
                minutesLate: minutesLate > 0 ? minutesLate : 0,
                duration: `${durationMinutes} minutes`
            };
            
            await updateFirestoreDoc('meetings', meetingId, { attendance: attendance });
            
            if (minutesLate > 15) {
                showNotification(`⚠️ You joined ${minutesLate} minutes late`);
            } else if (minutesLate > 0) {
                showNotification(`✓ Attendance recorded (${minutesLate} min late)`);
            } else {
                showNotification('✓ Attendance recorded - Joining meeting...');
            }
        } else {
            showNotification('Opening meeting...');
        }
        
        // Open meeting link
        window.open(joinLink, '_blank');
        
    } catch (error) {
        console.error('Error joining meeting:', error);
        window.open(joinLink, '_blank');
    }
}

// Auto-mark absent after 30 minutes
async function autoMarkAbsentParticipants() {
    try {
        const allMeetings = await getFromFirestore('meetings');
        const now = new Date();
        
        for (const meeting of allMeetings) {
            if (meeting.status === 'cancelled') continue;
            
            const meetingStartTime = new Date(meeting.date + 'T' + meeting.startTime);
            const minutesSinceStart = Math.round((now - meetingStartTime) / (1000 * 60));
            
            // Check if exactly 30 minutes passed (run once)
            if (minutesSinceStart === 30) {
                const attendance = meeting.attendance || {};
                let updated = false;
                
                // Mark all non-joined participants as absent
                for (const empCode of meeting.participants) {
                    if (!attendance[empCode]) {
                        const employee = authorizedEmployees[empCode];
                        attendance[empCode] = {
                            empCode: empCode,
                            empName: employee ? employee.name : empCode,
                            attendance: 'absent',
                            joinTime: null,
                            joinedLate: null,
                            minutesLate: null,
                            duration: null
                        };
                        updated = true;
                    }
                }
                
                if (updated) {
                    await updateFirestoreDoc('meetings', meeting.id, { attendance: attendance });
                    console.log(`Auto-marked absent for meeting: ${meeting.title}`);
                }
            }
        }
    } catch (error) {
        console.error('Error auto-marking absent:', error);
    }
}
setInterval(autoMarkAbsentParticipants, 60000);


// Download attachment
function downloadAttachment(fileName, url) {
    const link = document.createElement('a');
    link.href = url;
    link.download = fileName;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
}


async function loadHRMeetingsPanel() {
    const allMeetings = await getFromFirestore('meetings');
    
    const now = new Date();
    const pendingResponseMeetings = allMeetings.filter(m => {
        const totalParticipants = m.participants.length;
        const respondedCount = Object.keys(m.rsvp || {}).filter(k => m.rsvp[k].status !== 'pending').length;
        return respondedCount < totalParticipants && m.status !== 'cancelled' && new Date(m.date) >= now;
    });
    
    const upcomingMeetings = allMeetings.filter(m => 
        new Date(m.date) >= now && m.status !== 'cancelled'
    );
    
    const completedMeetings = allMeetings.filter(m => 
        new Date(m.date) < now || m.status === 'completed'
    );
    
    // Update statistics
    document.getElementById('hrTotalMeetings').textContent = allMeetings.length;
    document.getElementById('hrPendingResponses').textContent = pendingResponseMeetings.length;
    document.getElementById('hrUpcomingMeetings').textContent = upcomingMeetings.length;
    document.getElementById('hrCompletedMeetings').textContent = completedMeetings.length;
    
    // Load upcoming meetings by default
    switchHRMeetingTab('upcoming');
}

// View full meeting details
async function viewFullMeetingDetails(meetingId) {
    const allMeetings = await getFromFirestore('meetings');
    const meeting = allMeetings.find(m => m.id === meetingId);
    
    if (!meeting) {
        alert('Meeting not found');
        return;
    }
    
    const organizer = authorizedEmployees[meeting.organizer];
    const organizerName = organizer ? organizer.name : meeting.organizer;
    
    const participantsList = meeting.participants.map(pCode => {
        const emp = authorizedEmployees[pCode];
        const empName = emp ? emp.name : pCode;
        const rsvp = meeting.rsvp && meeting.rsvp[pCode] ? meeting.rsvp[pCode].status : 'pending';
        const rsvpColor = rsvp === 'accepted' ? '#27ae60' : rsvp === 'declined' ? '#e74c3c' : rsvp === 'tentative' ? '#f39c12' : '#95a5a6';
        
        return `
            <div style="display: flex; justify-content: space-between; padding: 8px; background: #f8f9fa; border-radius: 5px; margin: 5px 0;">
                <span>${empName}</span>
                <span style="background: ${rsvpColor}; color: white; padding: 4px 10px; border-radius: 15px; font-size: 11px; font-weight: bold;">
                    ${rsvp.toUpperCase()}
                </span>
            </div>
        `;
    }).join('');
    
    const attachmentsHtml = meeting.attachments && meeting.attachments.length > 0
        ? `
        <div class="meeting-attachments" style="margin: 20px 0;">
            <h4 style="font-size: 14px; color: #555; margin-bottom: 10px;">📎 Attachments:</h4>
            ${meeting.attachments.map(att => `
                <div class="attachment-item" onclick="downloadAttachment('${att.name}', '${att.url}')">
                    📄 ${att.name}
                </div>
            `).join('')}
        </div>
        ` : '';
    
    const modal = createModal(`
        <h2>${meeting.title}</h2>
        
        <div style="background: #e3f2fd; padding: 15px; border-radius: 8px; margin: 20px 0;">
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                <div>
                    <strong>📅 Date:</strong> ${new Date(meeting.date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
                </div>
                <div>
                    <strong>⏰ Time:</strong> ${meeting.startTime} - ${meeting.endTime}
                </div>
                <div>
                    <strong>📍 Location:</strong> ${meeting.location || 'Not specified'}
                </div>
                <div>
                    <strong>👤 Organizer:</strong> ${organizerName}
                </div>
                <div>
                    <strong>📋 Type:</strong> ${meeting.type}
                </div>
            </div>
        </div>
        
        ${meeting.agenda ? `
            <div class="meeting-agenda" style="margin: 20px 0;">
                <h4>📋 Agenda:</h4>
                <div style="white-space: pre-wrap; line-height: 1.6;">${meeting.agenda}</div>
            </div>
        ` : ''}
        
        ${meeting.notes ? `
            <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin: 20px 0; border-left: 4px solid #f39c12;">
                <h4 style="margin: 0 0 10px 0; color: #856404; font-size: 14px;">📝 Additional Notes:</h4>
                <div style="white-space: pre-wrap; line-height: 1.6;">${meeting.notes}</div>
            </div>
        ` : ''}
        
        ${attachmentsHtml}
        
        <div style="margin: 20px 0;">
            <h4 style="margin-bottom: 10px;">👥 Participants (${meeting.participants.length}):</h4>
            <div style="max-height: 200px; overflow-y: auto;">
                ${participantsList}
            </div>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}


// Switch HR meeting tabs
async function switchHRMeetingTab(tab) {
    document.querySelectorAll('[id^="hrMeetingTab"]').forEach(btn => {
        btn.classList.remove('active');
        btn.style.background = '#95a5a6';
    });
    
    document.getElementById(`hrMeetingTab${tab.charAt(0).toUpperCase() + tab.slice(1)}`).classList.add('active');
    document.getElementById(`hrMeetingTab${tab.charAt(0).toUpperCase() + tab.slice(1)}`).style.background = '#3498db';
    
    const allMeetings = await getFromFirestore('meetings');
    const now = new Date();
    let filteredMeetings = [];
    
    if (tab === 'upcoming') {
        filteredMeetings = allMeetings.filter(m => 
            new Date(m.date) >= now && m.status !== 'cancelled'
        );
    } else if (tab === 'pending') {
        filteredMeetings = allMeetings.filter(m => {
            const totalParticipants = m.participants.length;
            const respondedCount = Object.keys(m.rsvp || {}).filter(k => m.rsvp[k].status !== 'pending').length;
            return respondedCount < totalParticipants && m.status !== 'cancelled' && new Date(m.date) >= now;
        });
    } else if (tab === 'completed') {
        filteredMeetings = allMeetings.filter(m => 
            new Date(m.date) < now || m.status === 'completed'
        );
    }
    
    // Apply filters
    filteredMeetings = applyMeetingFiltersToData(filteredMeetings);
    
    filteredMeetings.sort((a, b) => new Date(b.date + 'T' + b.startTime) - new Date(a.date + 'T' + a.startTime));
    
    renderHRMeetingTable(filteredMeetings, tab);
}

// Render HR meeting table (Excel-style)
function renderHRMeetingTable(meetings, tab) {
    const container = document.getElementById('hrMeetingListContainer');
    
    if (meetings.length === 0) {
        container.innerHTML = '<div style="padding: 60px; text-align: center; color: #666; font-size: 16px;">No meetings found</div>';
        return;
    }
    
    const tableHtml = `
        <div style="background: #2c3e50; color: white; padding: 15px; border-radius: 10px 10px 0 0; display: flex; justify-content: space-between; align-items: center;">
            <h4 style="margin: 0;">Meeting List (${meetings.length} results)</h4>
        </div>
        
        <div style="overflow-x: auto; background: white; border-radius: 0 0 10px 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
            <table style="width: 100%; border-collapse: collapse; font-size: 13px; min-width: 1200px;">
                <thead>
                    <tr style="background: #34495e; color: white;">
                        <th style="padding: 12px; text-align: left; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Date</th>
                        <th style="padding: 12px; text-align: left; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Meeting Title</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Organizer</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Type</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Time</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Duration</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Invited</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Attendance</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10;">Status</th>
                        <th style="padding: 12px; text-align: center; border-bottom: 2px solid #2c3e50; position: sticky; top: 0; background: #34495e; z-index: 10; width: 180px;">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    ${meetings.map(meeting => {
                        const organizer = authorizedEmployees[meeting.organizer];
                        const organizerName = organizer ? organizer.name : meeting.organizer;
                        
                        const startTime = meeting.startTime || '00:00';
                        const endTime = meeting.endTime || '00:00';
                        const [startH, startM] = startTime.split(':').map(Number);
                        const [endH, endM] = endTime.split(':').map(Number);
                        const durationMins = (endH * 60 + endM) - (startH * 60 + startM);
                        const durationText = `${Math.floor(durationMins / 60)}h ${durationMins % 60}m`;
                        
                        const totalInvited = meeting.participants.length;
                        const attendance = meeting.attendance || {};
                        const attendedCount = Object.keys(attendance).length;
                        const attendancePercent = totalInvited > 0 ? Math.round((attendedCount / totalInvited) * 100) : 0;
                        
                        const rsvpData = meeting.rsvp || {};
                        const respondedCount = Object.keys(rsvpData).filter(k => rsvpData[k].status !== 'pending').length;
                        const responseRate = totalInvited > 0 ? Math.round((respondedCount / totalInvited) * 100) : 0;
                        
                        const meetingDateTime = new Date(meeting.date + 'T' + meeting.endTime);
						const isPast = meetingDateTime < new Date();
                        const statusBadge = meeting.status === 'cancelled' 
    ? '<span style="background: #e74c3c; color: white; padding: 4px 8px; border-radius: 12px; font-size: 11px; font-weight: bold;">CANCELLED</span>'
    : isPast
    ? '<span style="background: #95a5a6; color: white; padding: 4px 8px; border-radius: 12px; font-size: 11px; font-weight: bold;">PAST</span>'
    : '<span style="background: #3498db; color: white; padding: 4px 8px; border-radius: 12px; font-size: 11px; font-weight: bold;">UPCOMING</span>';
                        
                        return `
                            <tr style="border-bottom: 1px solid #ecf0f1; transition: background 0.2s;" onmouseover="this.style.background='#f8f9fa'" onmouseout="this.style.background='white'">
                                <td style="padding: 12px;">${new Date(meeting.date).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })}</td>
                                <td style="padding: 12px; font-weight: 500;">${meeting.title}</td>
                                <td style="padding: 12px; text-align: center;">
    ${organizerName}
    ${meeting.organizer === (currentUser.code || currentUser.username) ? '<br><span style="background: #f39c12; color: white; padding: 2px 6px; border-radius: 10px; font-size: 9px;">YOU</span>' : ''}
</td>
                                <td style="padding: 12px; text-align: center;"><span class="meeting-type-badge ${meeting.type.replace(' ', '-').toLowerCase()}">${meeting.type}</span></td>
                                <td style="padding: 12px; text-align: center;">${startTime}</td>
                                <td style="padding: 12px; text-align: center;">${durationText}</td>
                                <td style="padding: 12px; text-align: center; font-weight: bold;">${totalInvited}</td>
                                <td style="padding: 12px; text-align: center;">
                                    ${isPast 
                                        ? `<span style="background: ${attendancePercent >= 80 ? '#d4edda' : attendancePercent >= 50 ? '#fff3cd' : '#f8d7da'}; padding: 4px 8px; border-radius: 12px; font-weight: bold; color: #333;">${attendedCount}/${totalInvited} (${attendancePercent}%)</span>`
                                        : `<span style="background: #e3f2fd; padding: 4px 8px; border-radius: 12px; font-weight: bold; color: #333;">${respondedCount}/${totalInvited} (${responseRate}%)</span>`
                                    }
                                </td>
                                <td style="padding: 12px; text-align: center;">${statusBadge}</td>
                                <td style="padding: 12px; text-align: center;">
                                    <div style="display: flex; gap: 5px; justify-content: center;">
                                        <button onclick="viewMeetingDetailsHR('${meeting.id}')" class="btn" style="background: #3498db; padding: 6px 10px; font-size: 11px;">View</button>
                                        ${!isPast && meeting.status !== 'cancelled' ? `
    <button onclick="editMeeting('${meeting.id}')" class="btn" style="background: #f39c12; padding: 6px 10px; font-size: 11px;">Edit</button>
    <button onclick="cancelMeetingHR('${meeting.id}')" class="btn" style="background: #e74c3c; padding: 6px 10px; font-size: 11px;">Cancel</button>
` : ''}
<button onclick="deleteMeetingHR('${meeting.id}')" class="btn" style="background: #c0392b; padding: 6px 10px; font-size: 11px;">Delete</button>
${isPast ? `
    <button onclick="exportMeetingAttendance('${meeting.id}')" class="btn" style="background: #27ae60; padding: 6px 10px; font-size: 11px;">📥 Export</button>
` : ''}
                                    </div>
                                </td>
                            </tr>
                        `;
                    }).join('')}
                </tbody>
            </table>
        </div>
    `;
    
    container.innerHTML = tableHtml;
}

// Apply meeting filters
function applyMeetingFilters() {
    switchHRMeetingTab(getCurrentHRMeetingTab());
}

function getCurrentHRMeetingTab() {
    if (document.getElementById('hrMeetingTabUpcoming')?.classList.contains('active')) return 'upcoming';
    if (document.getElementById('hrMeetingTabPending')?.classList.contains('active')) return 'pending';
    if (document.getElementById('hrMeetingTabCompleted')?.classList.contains('active')) return 'completed';
    return 'upcoming';
}

function applyMeetingFiltersToData(meetings) {
    const fromDate = document.getElementById('meetingFilterFrom')?.value;
    const toDate = document.getElementById('meetingFilterTo')?.value;
    const organizer = document.getElementById('meetingFilterOrganizer')?.value;
    const type = document.getElementById('meetingFilterType')?.value;
    const search = document.getElementById('meetingFilterSearch')?.value.toLowerCase().trim();
    
    return meetings.filter(meeting => {
        if (fromDate && meeting.date < fromDate) return false;
        if (toDate && meeting.date > toDate) return false;
        if (organizer && meeting.organizer !== organizer) return false;
        if (type && meeting.type !== type) return false;
        if (search && !meeting.title.toLowerCase().includes(search)) return false;
        return true;
    });
}

function clearMeetingFilters() {
    if (document.getElementById('meetingFilterFrom')) document.getElementById('meetingFilterFrom').value = '';
    if (document.getElementById('meetingFilterTo')) document.getElementById('meetingFilterTo').value = '';
    if (document.getElementById('meetingFilterOrganizer')) document.getElementById('meetingFilterOrganizer').value = '';
    if (document.getElementById('meetingFilterType')) document.getElementById('meetingFilterType').value = '';
    if (document.getElementById('meetingFilterSearch')) document.getElementById('meetingFilterSearch').value = '';
    applyMeetingFilters();
}

// View meeting details with full attendance tracking
async function viewMeetingDetailsHR(meetingId) {
    const allMeetings = await getFromFirestore('meetings');
    const meeting = allMeetings.find(m => m.id === meetingId);
    
    if (!meeting) {
        alert('Meeting not found');
        return;
    }
    
    const organizer = authorizedEmployees[meeting.organizer];
    const organizerName = organizer ? organizer.name : meeting.organizer;
    
    const isPast = new Date(meeting.date) < new Date();
    const attendance = meeting.attendance || {};
    const rsvpData = meeting.rsvp || {};
    
// Build attendance table - SIMPLIFIED STANDARD VIEW
    const attendanceTableHtml = meeting.participants.map(pCode => {
        const emp = authorizedEmployees[pCode];
        const empName = emp ? emp.name : pCode;
        
        const attend = attendance[pCode];
        
        let attendanceStatus = '-';
        let statusColor = '#95a5a6';
        let joinTimeText = '-';
        let lateText = '-';
        let durationText = '-';
        
        if (attend) {
            if (attend.attendance === 'present') {
                joinTimeText = new Date(attend.joinTime).toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' });
                lateText = attend.joinedLate ? `Yes (${attend.minutesLate} min)` : 'No';
                durationText = attend.duration || '-';
                
                if (attend.joinedLate && attend.minutesLate > 15) {
                    attendanceStatus = '⚠ Present (Late)';
                    statusColor = '#f39c12';
                } else {
                    attendanceStatus = '✓ Present';
                    statusColor = '#27ae60';
                }
            } else if (attend.attendance === 'absent') {
                attendanceStatus = '✗ Absent';
                statusColor = '#e74c3c';
            }
        } else if (isPast) {
            // Meeting ended but no attendance record
            attendanceStatus = '✗ No Record';
            statusColor = '#95a5a6';
        }
        
        return `
            <tr style="border-bottom: 1px solid #ecf0f1;">
                <td style="padding: 10px; font-weight: 500;">${empName}</td>
                <td style="padding: 10px; text-align: center;">${pCode}</td>
                <td style="padding: 10px; text-align: center;">${joinTimeText}</td>
                <td style="padding: 10px; text-align: center;">
                    <span style="background: ${statusColor}; color: white; padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold;">${attendanceStatus}</span>
                </td>
                <td style="padding: 10px; text-align: center;">${lateText}</td>
                <td style="padding: 10px; text-align: center;">${durationText}</td>
            </tr>
        `;
    }).join('');
    
    // Calculate statistics
    const totalInvited = meeting.participants.length;
    const attendanceRecords = Object.values(attendance);
    const totalPresent = attendanceRecords.filter(a => a.attendance === 'present').length;
    const totalAbsent = attendanceRecords.filter(a => a.attendance === 'absent').length;
    const totalLate = attendanceRecords.filter(a => a.attendance === 'present' && a.joinedLate && a.minutesLate > 15).length;
    const attendanceRate = totalInvited > 0 ? Math.round((totalPresent / totalInvited) * 100) : 0;
    
    const modal = createModal(`
        <h2>📊 Meeting Details & Attendance</h2>
        
        <!-- Meeting Info -->
        <div style="background: #e3f2fd; padding: 20px; border-radius: 8px; margin: 20px 0;">
            <h3 style="margin: 0 0 15px 0; color: #2c3e50;">${meeting.title}</h3>
            <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px;">
                <div>
                    <strong>📅 Date:</strong> ${new Date(meeting.date).toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric', year: 'numeric' })}
                </div>
                <div>
                    <strong>⏰ Time:</strong> ${meeting.startTime} - ${meeting.endTime}
                </div>
                <div>
                    <strong>📍 Location:</strong> ${meeting.location || 'Virtual'}
                </div>
                <div>
                    <strong>👤 Organizer:</strong> ${organizerName}
                </div>
                <div>
                    <strong>📋 Type:</strong> ${meeting.type}
                </div>
                <div>
                    <strong>🔗 Join Link:</strong> ${meeting.joinLink ? '<a href="' + meeting.joinLink + '" target="_blank" style="color: #3498db;">Open Link</a>' : 'Not available'}
                </div>
            </div>
        </div>
        
        ${meeting.agenda ? `
            <div class="meeting-agenda" style="margin: 20px 0;">
                <h4>📋 Agenda:</h4>
                <div style="white-space: pre-wrap; line-height: 1.6;">${meeting.agenda}</div>
            </div>
        ` : ''}
        
        <!-- Attendance Statistics -->
        ${isPast ? `
            <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <h4 style="margin: 0 0 15px 0;">📊 Attendance Summary</h4>
                <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 15px;">
                    <div style="text-align: center; padding: 15px; background: #e3f2fd; border-radius: 8px;">
                        <div style="font-size: 24px; font-weight: bold; color: #2c3e50;">${totalInvited}</div>
                        <div style="font-size: 12px; color: #666;">Total Invited</div>
                    </div>
                    <div style="text-align: center; padding: 15px; background: #d4edda; border-radius: 8px;">
                        <div style="font-size: 24px; font-weight: bold; color: #27ae60;">${totalPresent}</div>
                        <div style="font-size: 12px; color: #666;">Present</div>
                    </div>
                    <div style="text-align: center; padding: 15px; background: #f8d7da; border-radius: 8px;">
                        <div style="font-size: 24px; font-weight: bold; color: #e74c3c;">${totalAbsent}</div>
                        <div style="font-size: 12px; color: #666;">Absent</div>
                    </div>
                    <div style="text-align: center; padding: 15px; background: ${attendanceRate >= 80 ? '#d4edda' : attendanceRate >= 50 ? '#fff3cd' : '#f8d7da'}; border-radius: 8px;">
                        <div style="font-size: 24px; font-weight: bold; color: #2c3e50;">${attendanceRate}%</div>
                        <div style="font-size: 12px; color: #666;">Attendance Rate</div>
                    </div>
                </div>
            </div>
        ` : ''}
        
        <!-- Attendance Table -->
        <div style="margin: 20px 0;">
            <div style="background: #2c3e50; color: white; padding: 15px; border-radius: 8px 8px 0 0; display: flex; justify-content: space-between; align-items: center;">
                <h4 style="margin: 0;">${isPast ? 'Attendance Report' : 'Participant List'} (${meeting.participants.length})</h4>
            </div>
            <div style="overflow-x: auto; max-height: 400px; overflow-y: auto; border: 1px solid #dee2e6; border-top: none;">
                <table style="width: 100%; border-collapse: collapse; font-size: 13px;">
                    <thead style="position: sticky; top: 0; background: #34495e; color: white; z-index: 5;">
                        <tr>
                            <th style="padding: 10px; text-align: left;">Employee Name</th>
                            <th style="padding: 10px; text-align: center;">Code</th>
                            <th style="padding: 10px; text-align: center;">Join Time</th>
                            <th style="padding: 10px; text-align: center;">Status</th>
                            <th style="padding: 10px; text-align: center;">Late?</th>
                            <th style="padding: 10px; text-align: center;">Duration</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${attendanceTableHtml}
                    </tbody>
                </table>
            </div>
        </div>
        
        <!-- Action Buttons -->
        <div style="text-align: right; margin-top: 20px; display: flex; gap: 10px; justify-content: flex-end;">
            ${isPast ? `
                <button onclick="exportMeetingAttendance('${meetingId}')" class="btn" style="background: #27ae60;">
                    📥 Export to Excel
                </button>
            ` : ''}
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}
    

// Edit attendance remarks
async function editAttendanceRemarks(meetingId, empCode) {
    const allMeetings = await getFromFirestore('meetings');
    const meeting = allMeetings.find(m => m.id === meetingId);
    
    if (!meeting) return;
    
    const employee = authorizedEmployees[empCode];
    const empName = employee ? employee.name : empCode;
    
    const attendance = meeting.attendance || {};
    const currentRemarks = attendance[empCode]?.remarks || '';
    
    const newRemarks = prompt(`Edit remarks for ${empName}:`, currentRemarks);
    
    if (newRemarks === null) return; // User cancelled
    
    try {
        if (!attendance[empCode]) {
            // Manually mark attendance
            attendance[empCode] = {
                joinTime: new Date().toISOString(),
                status: 'manual',
                remarks: newRemarks || 'Manually marked present'
            };
        } else {
            attendance[empCode].remarks = newRemarks;
        }
        
        await updateFirestoreDoc('meetings', meetingId, { attendance: attendance });
        
        showNotification('Attendance updated');
        viewMeetingDetailsHR(meetingId);
        
    } catch (error) {
        console.error('Error updating attendance:', error);
        alert('Error updating attendance');
    }
}

// Send alerts to no-show participants
async function sendNoShowAlerts(meetingId) {
    const allMeetings = await getFromFirestore('meetings');
    const meeting = allMeetings.find(m => m.id === meetingId);
    
    if (!meeting) return;
    
    const rsvpData = meeting.rsvp || {};
    const attendance = meeting.attendance || {};
    
    // Find accepted/tentative who didn't join
    const noShows = meeting.participants.filter(pCode => {
        const rsvp = rsvpData[pCode];
        const attended = attendance[pCode];
        return (rsvp?.status === 'accepted' || rsvp?.status === 'tentative') && !attended;
    });
    
    if (noShows.length === 0) {
        alert('No no-shows found. All participants who accepted have joined.');
        return;
    }
    
    if (!confirm(`Send alert to ${noShows.length} no-show participant(s)?`)) return;
    
    try {
        for (const pCode of noShows) {
            const employee = authorizedEmployees[pCode];
            if (!employee) continue;
            
            const message = `⚠️ NO-SHOW ALERT: You accepted the meeting "${meeting.title}" on ${new Date(meeting.date).toLocaleDateString()} but did not attend. Please contact HR.`;
            
            // Send notification
            const notification = {
                id: `NOTIF_NOSHOW_${Date.now()}_${pCode}`,
                empCode: pCode,
                type: 'meeting_noshow',
                meetingId: meeting.id,
                message: message,
                acknowledged: false,
                createdDate: new Date().toISOString()
            };
            
            await saveToFirestore('schedule_notifications', notification);
            
            // Send email
            await sendEmailNotification(
                employee.email,
                'Meeting No-Show Alert',
                message,
                `You missed: ${meeting.title}`
            );
        }
        
        showNotification(`Alerts sent to ${noShows.length} participant(s)`);
        
    } catch (error) {
        console.error('Error sending alerts:', error);
        alert('Error sending alerts');
    }
}

// Cancel meeting (HR)
async function cancelMeetingHR(meetingId) {
    if (!confirm('Cancel this meeting? Employees will see it for 1 hour before it disappears.')) return;
    
    const reason = prompt('Enter cancellation reason (optional):');
    
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        await updateFirestoreDoc('meetings', meetingId, {
            status: 'cancelled',
            cancellationReason: reason || 'No reason provided',
            cancelledBy: currentUser.code || currentUser.username,
            cancelledDate: new Date().toISOString()
        });
        
        showNotification('Meeting cancelled. Employees will see it for 1 hour before auto-removal.');
        
        // Reload table
        switchHRMeetingTab(getCurrentHRMeetingTab());
        
    } catch (error) {
        console.error('Error cancelling meeting:', error);
        alert('Error cancelling meeting');
    }
}

// Auto-hide cancelled meetings from employee view after 1 hour
async function autoHideCancelledMeetings() {
    try {
        const allMeetings = await getFromFirestore('meetings');
        const now = new Date();
        
        const recentlyCancelled = allMeetings.filter(meeting => {
            if (meeting.status !== 'cancelled' || !meeting.cancelledDate) return false;
            
            const cancelledTime = new Date(meeting.cancelledDate);
            const hoursSinceCancellation = (now - cancelledTime) / (1000 * 60 * 60);
            
            // Return true if cancelled more than 1 hour ago
            return hoursSinceCancellation > 1;
        });
        
        // These meetings are already marked as cancelled in DB
        // Employee view filter will exclude them automatically
        console.log(`${recentlyCancelled.length} cancelled meetings are now hidden from employees`);
        
    } catch (error) {
        console.error('Error checking cancelled meetings:', error);
    }
}

// Check every 10 minutes
setInterval(autoHideCancelledMeetings, 600000);

// Delete meeting (HR/Admin only)
async function deleteMeetingHR(meetingId) {
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') {
        alert('Access Denied: Only HR and administrators can delete meetings');
        return;
    }
    
    const confirmed = confirm('⚠️ DELETE this meeting permanently?\n\nThis action CANNOT be undone.\n\nType "DELETE" to confirm.');
    if (!confirmed) return;
    
    const verification = prompt('Type DELETE in CAPS to confirm permanent deletion:');
    if (verification !== 'DELETE') {
        showNotification('Deletion cancelled');
        return;
    }
    
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        // Delete from Firestore
        const snapshot = await db.collection('meetings').get();
        for (const doc of snapshot.docs) {
            if (doc.data().id === meetingId) {
                await doc.ref.delete();
                break;
            }
        }
        
        // Notify all participants
        for (const pCode of meeting.participants) {
            const message = `Meeting DELETED: ${meeting.title} on ${new Date(meeting.date).toLocaleDateString()} has been permanently removed.`;
            
            const notification = {
                id: `NOTIF_DELETE_${Date.now()}_${pCode}`,
                empCode: pCode,
                type: 'meeting_deleted',
                meetingId: meetingId,
                message: message,
                acknowledged: false,
                createdDate: new Date().toISOString()
            };
            
            await saveToFirestore('schedule_notifications', notification);
        }
        
        showNotification('Meeting deleted permanently. Participants have been notified.');
        
        // Reload table
        switchHRMeetingTab(getCurrentHRMeetingTab());
        
    } catch (error) {
        console.error('Error deleting meeting:', error);
        alert('Error deleting meeting: ' + error.message);
    }
}

// Export meeting attendance to Excel/CSV
async function exportMeetingAttendance(meetingId) {
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        const attendance = meeting.attendance || {};
        
        const csvRows = [
            ['MEETING ATTENDANCE REPORT'],
            [''],
            ['Meeting Title', meeting.title],
            ['Date', new Date(meeting.date).toLocaleDateString()],
            ['Time', `${meeting.startTime} - ${meeting.endTime}`],
            ['Organizer', authorizedEmployees[meeting.organizer]?.name || meeting.organizer],
            ['Location', meeting.location || 'Virtual'],
            ['Join Link', meeting.joinLink || 'N/A'],
            [''],
            ['SUMMARY'],
            ['Total Invited', meeting.participants.length],
            ['Present', Object.values(attendance).filter(a => a.attendance === 'present').length],
            ['Absent', Object.values(attendance).filter(a => a.attendance === 'absent').length],
            ['Attendance Rate', `${meeting.participants.length > 0 ? Math.round((Object.values(attendance).filter(a => a.attendance === 'present').length / meeting.participants.length) * 100) : 0}%`],
            [''],
            ['DETAILED ATTENDANCE'],
            ['Employee Name', 'Employee Code', 'Department', 'Attendance Status', 'Join Time', 'Late?', 'Minutes Late', 'Duration']
        ];
        
        meeting.participants.forEach(pCode => {
            const emp = authorizedEmployees[pCode];
            const empName = emp ? emp.name : pCode;
            const department = emp ? emp.department : 'Unknown';
            const attend = attendance[pCode];
            
            let status = 'No Record';
            let joinTime = '-';
            let late = '-';
            let minutesLate = 0;
            let duration = '-';
            
            if (attend) {
                status = attend.attendance === 'present' ? 'Present' : 'Absent';
                if (attend.attendance === 'present') {
                    joinTime = attend.joinTime ? new Date(attend.joinTime).toLocaleTimeString() : '-';
                    late = attend.joinedLate ? 'Yes' : 'No';
                    minutesLate = attend.minutesLate || 0;
                    duration = attend.duration || '-';
                }
            }
            
            csvRows.push([
                empName,
                pCode,
                department,
                status,
                joinTime,
                late,
                minutesLate,
                duration
            ]);
        });
        
        const csvContent = csvRows.map(row => row.map(cell => `"${cell}"`).join(',')).join('\n');
        downloadCSV(csvContent, `meeting_attendance_${meeting.id}_${new Date().toISOString().split('T')[0]}.csv`);
        
        showNotification('Attendance report exported successfully!');
        
    } catch (error) {
        console.error('Error exporting attendance:', error);
        alert('Error exporting attendance report');
    }
}
// Export all meetings to Excel
async function exportAllMeetingsToExcel() {
    try {
        const allMeetings = await getFromFirestore('meetings');
        const filteredMeetings = applyMeetingFiltersToData(allMeetings);
        
        if (filteredMeetings.length === 0) {
            alert('No meetings to export');
            return;
        }
        
        const csvRows = [
            ['MEETING EXPORT REPORT'],
            ['Export Date', new Date().toLocaleString()],
            ['Total Meetings', filteredMeetings.length],
            [''],
            ['Date', 'Meeting Title', 'Organizer', 'Type', 'Start Time', 'End Time', 'Duration', 'Location', 'Join Link', 'Total Invited', 'Present', 'Absent', 'Attendance %', 'Status']
        ];
        
        filteredMeetings.forEach(meeting => {
            const organizer = authorizedEmployees[meeting.organizer];
            const organizerName = organizer ? organizer.name : meeting.organizer;
            
            const startTime = meeting.startTime || '00:00';
            const endTime = meeting.endTime || '00:00';
            const [startH, startM] = startTime.split(':').map(Number);
            const [endH, endM] = endTime.split(':').map(Number);
            const durationMins = (endH * 60 + endM) - (startH * 60 + startM);
            const durationText = `${Math.floor(durationMins / 60)}h ${durationMins % 60}m`;
            
            const totalInvited = meeting.participants.length;
            const attendance = meeting.attendance || {};
            const presentCount = Object.values(attendance).filter(a => a.attendance === 'present').length;
            const absentCount = Object.values(attendance).filter(a => a.attendance === 'absent').length;
            const attendancePercent = totalInvited > 0 ? Math.round((presentCount / totalInvited) * 100) : 0;
            
            const isPast = new Date(meeting.date + 'T' + meeting.endTime) < new Date();
            const status = meeting.status === 'cancelled' ? 'CANCELLED' : isPast ? 'COMPLETED' : 'UPCOMING';
            
            csvRows.push([
                meeting.date,
                meeting.title,
                organizerName,
                meeting.type,
                startTime,
                endTime,
                durationText,
                meeting.location || 'Virtual',
                meeting.joinLink || 'N/A',
                totalInvited,
                presentCount,
                absentCount,
                `${attendancePercent}%`,
                status
            ]);
        });
        
        // Add attendance details section
        csvRows.push([]);
        csvRows.push(['DETAILED ATTENDANCE BY MEETING']);
        csvRows.push([]);
        
        filteredMeetings.forEach(meeting => {
            const isPast = new Date(meeting.date + 'T' + meeting.endTime) < new Date();
            if (!isPast || meeting.status === 'cancelled') return; // Only export attendance for completed meetings
            
            csvRows.push([`Meeting: ${meeting.title}`]);
            csvRows.push([`Date: ${meeting.date}`, `Time: ${meeting.startTime} - ${meeting.endTime}`]);
            csvRows.push(['Employee Name', 'Employee Code', 'Attendance', 'Join Time', 'Late?', 'Minutes Late', 'Duration']);
            
            const attendance = meeting.attendance || {};
            meeting.participants.forEach(empCode => {
                const emp = authorizedEmployees[empCode];
                const empName = emp ? emp.name : empCode;
                const attend = attendance[empCode];
                
                if (attend) {
                    csvRows.push([
                        empName,
                        empCode,
                        attend.attendance === 'present' ? 'Present' : 'Absent',
                        attend.joinTime ? new Date(attend.joinTime).toLocaleTimeString() : '-',
                        attend.joinedLate ? 'Yes' : 'No',
                        attend.minutesLate || 0,
                        attend.duration || '-'
                    ]);
                }
            });
            
            csvRows.push([]); // Empty row between meetings
        });
        
        const csvContent = csvRows.map(row => row.map(cell => `"${cell}"`).join(',')).join('\n');
        downloadCSV(csvContent, `meetings_bulk_export_${new Date().toISOString().split('T')[0]}.csv`);
        
        showNotification(`Exported ${filteredMeetings.length} meeting(s) with attendance details!`);
        
    } catch (error) {
        console.error('Error exporting meetings:', error);
        alert('Error exporting meetings');
    }
}

// Render HR meeting list
function renderHRMeetingList(meetings, tab) {
    const container = document.getElementById('hrMeetingListContainer');
    
    if (meetings.length === 0) {
        container.innerHTML = '<div style="padding: 60px; text-align: center; color: #666; font-size: 16px;">No meetings found</div>';
        return;
    }
    
    const html = meetings.map(meeting => {
        const totalParticipants = meeting.participants.length;
        const rsvpData = meeting.rsvp || {};
        const acceptedCount = Object.values(rsvpData).filter(r => r.status === 'accepted').length;
        const declinedCount = Object.values(rsvpData).filter(r => r.status === 'declined').length;
        const tentativeCount = Object.values(rsvpData).filter(r => r.status === 'tentative').length;
        const pendingCount = totalParticipants - acceptedCount - declinedCount - tentativeCount;
        
        const responseRate = totalParticipants > 0 
            ? Math.round(((acceptedCount + declinedCount + tentativeCount) / totalParticipants) * 100) 
            : 0;
        
        return `
            <div class="meeting-card">
                <div class="meeting-card-header">
                    <div>
                        <div class="meeting-title">${meeting.title}</div>
                        <span class="meeting-type-badge ${meeting.type.replace(' ', '-').toLowerCase()}">${meeting.type}</span>
                    </div>
                </div>
                
                <div class="meeting-details">
                    <div class="meeting-detail-item">
                        <strong>📅 Date:</strong> ${new Date(meeting.date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
                    </div>
                    <div class="meeting-detail-item">
                        <strong>⏰ Time:</strong> ${meeting.startTime} - ${meeting.endTime}
                    </div>
                    <div class="meeting-detail-item">
                        <strong>📍 Location:</strong> ${meeting.location || 'Not specified'}
                    </div>
                    <div class="meeting-detail-item">
                        <strong>👥 Participants:</strong> ${totalParticipants}
                    </div>
                </div>
                
                <!-- Response Summary -->
                <div class="response-summary">
                    <div class="response-stat accepted">
                        <div class="response-stat-value">${acceptedCount}</div>
                        <div class="response-stat-label">Accepted</div>
                    </div>
                    <div class="response-stat declined">
                        <div class="response-stat-value">${declinedCount}</div>
                        <div class="response-stat-label">Declined</div>
                    </div>
                    <div class="response-stat tentative">
                        <div class="response-stat-value">${tentativeCount}</div>
                        <div class="response-stat-label">Tentative</div>
                    </div>
                    <div class="response-stat pending">
                        <div class="response-stat-value">${pendingCount}</div>
                        <div class="response-stat-label">Pending</div>
                    </div>
                </div>
                
                <div style="background: ${responseRate >= 80 ? '#d4edda' : responseRate >= 50 ? '#fff3cd' : '#f8d7da'}; padding: 10px; border-radius: 5px; text-align: center; font-weight: bold; margin: 15px 0;">
                    Response Rate: ${responseRate}%
                </div>
                
                <div style="display: flex; gap: 10px; margin-top: 15px;">
                    <button onclick="viewMeetingResponses('${meeting.id}')" class="btn" style="background: #3498db; flex: 1;">
                        View Responses
                    </button>
                    ${tab === 'upcoming' ? `
                        <button onclick="editMeeting('${meeting.id}')" class="btn" style="background: #f39c12; flex: 1;">
                            Edit
                        </button>
                        <button onclick="cancelMeeting('${meeting.id}')" class="btn" style="background: #e74c3c; flex: 1;">
                            Cancel
                        </button>
                    ` : ''}
                    ${pendingCount > 0 && tab === 'pending' ? `
                        <button onclick="sendReminderToPending('${meeting.id}')" class="btn" style="background: #9b59b6; flex: 1;">
                            Send Reminder
                        </button>
                    ` : ''}
                </div>
            </div>
        `;
    }).join('');
    
    container.innerHTML = html;
}

// Open create meeting modal
function openCreateMeetingModal() {
    const tomorrow = new Date();
    tomorrow.setDate(tomorrow.getDate() + 1);
    const tomorrowStr = tomorrow.toISOString().split('T')[0];
    
    const modal = createModal(`
        <h2>➕ Create New Meeting</h2>
        
        <div style="max-height: 70vh; overflow-y: auto; padding-right: 10px;">
            <!-- Basic Information -->
            <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <h3 style="margin: 0 0 15px 0; color: #2c3e50;">Basic Information</h3>
                
                <div style="margin-bottom: 15px;">
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Meeting Title *</label>
                    <input type="text" id="meetingTitle" placeholder="e.g., Weekly QA Review Meeting" 
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                </div>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 15px;">
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Meeting Type *</label>
                        <select id="meetingType" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                            <option value="QA Review">QA Review</option>
                            <option value="Training">Training</option>
                            <option value="Department Meeting">Department Meeting</option>
                            <option value="Emergency">Emergency</option>
                            <option value="Other">Other</option>
                        </select>
                    </div>
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Location</label>
                        <input type="text" id="meetingLocation" placeholder="Conference Room A / Virtual" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
					<div style="grid-column: span 2; margin-top: 15px;">
							<label style="display: block; margin-bottom: 5px; font-weight: 500;">Meeting Join Link *</label>
							<input type="url" id="meetingJoinLink" placeholder="https://zoom.us/j/123456789 or https://teams.microsoft.com/..." 
								style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
							<div style="font-size: 11px; color: #666; margin-top: 5px;">
								📎 Paste Zoom, Teams, Google Meet, or any meeting link here
							</div>
					</div>
                </div>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px;">
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Date *</label>
                        <input type="date" id="meetingDate" value="${tomorrowStr}" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Start Time *</label>
                        <input type="time" id="meetingStartTime" value="09:00" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">End Time *</label>
                        <input type="time" id="meetingEndTime" value="10:00" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                </div>
            </div>
            
            <!-- Participants Selection -->
            <div style="background: #e3f2fd; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <h3 style="margin: 0 0 15px 0; color: #2c3e50;">Select Participants *</h3>
                
                <div style="margin-bottom: 15px;">
                    <label style="display: flex; align-items: center; font-weight: 500; cursor: pointer;">
                        <input type="checkbox" id="selectAllParticipants" onchange="toggleSelectAllParticipants()" 
                            style="margin-right: 10px; transform: scale(1.3);">
                        Select All Employees
                    </label>
                </div>
                
                <div class="participant-selector" id="participantSelector">
                    ${Object.entries(authorizedEmployees)
                        .filter(([code, emp]) => emp.role === 'employee')
                        .map(([code, emp]) => `
                            <label class="participant-checkbox">
                                <input type="checkbox" class="participant-check" value="${code}">
                                ${emp.name} (${code})
                            </label>
                        `).join('')}
                </div>
                
                <div style="margin-top: 10px; font-size: 12px; color: #555;">
                    <span id="selectedParticipantCount">0</span> participant(s) selected
                </div>
            </div>
            
            <!-- Meeting Details -->
            <div style="background: #fff3cd; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <h3 style="margin: 0 0 15px 0; color: #856404;">Meeting Details</h3>
                
                <div style="margin-bottom: 15px;">
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Agenda</label>
                    <textarea id="meetingAgenda" rows="4" placeholder="Enter meeting agenda here..." 
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: inherit;"></textarea>
                </div>
                
                <div style="margin-bottom: 15px;">
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Additional Notes</label>
                    <textarea id="meetingNotes" rows="3" placeholder="Any additional information..." 
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: inherit;"></textarea>
                </div>
                
                <div>
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Attach Documents (Optional)</label>
                    <input type="file" id="meetingAttachments" multiple 
                        accept=".pdf,.doc,.docx,.xlsx,.xls,.png,.jpg,.jpeg"
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    <div style="font-size: 11px; color: #666; margin-top: 5px;">
                        Supported: PDF, DOC, XLSX, Images | Max 10MB per file
                    </div>
                    <div id="attachmentPreview" style="margin-top: 10px;"></div>
                </div>
            </div>
        </div>
        
        <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px; padding-top: 20px; border-top: 2px solid #ecf0f1;">
            <button onclick="saveMeetingAsDraft()" class="btn" style="background: #95a5a6;">
                💾 Save as Draft
            </button>
            <button onclick="createAndSendMeeting()" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                📧 Create & Send Invitations
            </button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">
                Cancel
            </button>
        </div>
    `);
    
    // Update participant count on change
    document.querySelectorAll('.participant-check').forEach(checkbox => {
        checkbox.addEventListener('change', updateParticipantCount);
    });
    
    // File preview
    document.getElementById('meetingAttachments').addEventListener('change', previewAttachments);
}

// Toggle select all participants
function toggleSelectAllParticipants() {
    const isChecked = document.getElementById('selectAllParticipants').checked;
    document.querySelectorAll('.participant-check').forEach(checkbox => {
        checkbox.checked = isChecked;
    });
    updateParticipantCount();
}

// Update participant count
function updateParticipantCount() {
    const count = document.querySelectorAll('.participant-check:checked').length;
    document.getElementById('selectedParticipantCount').textContent = count;
}

// Preview attachments
function previewAttachments(event) {
    const files = event.target.files;
    const preview = document.getElementById('attachmentPreview');
    
    if (files.length === 0) {
        preview.innerHTML = '';
        return;
    }
    
    let html = '<div style="font-size: 12px; color: #555; margin-top: 10px;">Files to upload:</div>';
    
    for (let i = 0; i < files.length; i++) {
        const file = files[i];
        const sizeKB = (file.size / 1024).toFixed(2);
        html += `
            <div style="display: flex; align-items: center; justify-content: space-between; background: white; padding: 8px; border-radius: 5px; margin: 5px 0; border: 1px solid #ddd;">
                <span style="font-size: 12px;">📄 ${file.name} (${sizeKB} KB)</span>
            </div>
        `;
    }
    
    preview.innerHTML = html;
}

// Create and send meeting
async function createAndSendMeeting() {
    const title = document.getElementById('meetingTitle').value.trim();
    const type = document.getElementById('meetingType').value;
    const location = document.getElementById('meetingLocation').value.trim();
    const date = document.getElementById('meetingDate').value;
    const startTime = document.getElementById('meetingStartTime').value;
    const endTime = document.getElementById('meetingEndTime').value;
    const agenda = document.getElementById('meetingAgenda').value.trim();
	const notes = document.getElementById('meetingNotes').value.trim();
	const joinLink = document.getElementById('meetingJoinLink').value.trim();

	const selectedParticipants = Array.from(document.querySelectorAll('.participant-check:checked'))
    .map(checkbox => checkbox.value);

// Validation
if (!title) {
    alert('Please enter meeting title');
    return;
}

if (!date || !startTime || !endTime) {
    alert('Please enter date and time');
    return;
}

if (!joinLink) {
    alert('Please enter a meeting join link (Zoom, Teams, Google Meet, etc.)');
    return;
}

if (selectedParticipants.length === 0) {
    alert('Please select at least one participant');
    return;
}

if (startTime >= endTime) {
    alert('End time must be after start time');
    return;
}
    
    try {
        const meetingId = `MEETING_${Date.now()}`;
        
        // Handle file uploads (simplified - store as base64 for small files)
        const attachments = [];
        const fileInput = document.getElementById('meetingAttachments');
        
        if (fileInput.files.length > 0) {
            for (let i = 0; i < fileInput.files.length; i++) {
                const file = fileInput.files[i];
                
                if (file.size > 10 * 1024 * 1024) {
                    alert(`File "${file.name}" is too large. Max 10MB per file.`);
                    continue;
                }
                
                // Convert to base64 for storage (for demo purposes)
                const base64 = await fileToBase64(file);
                
                attachments.push({
                    name: file.name,
                    size: file.size,
                    type: file.type,
                    url: base64
                });
            }
        }
        
        // Initialize RSVP object with all participants as pending
        const rsvp = {};
        selectedParticipants.forEach(pCode => {
            rsvp[pCode] = {
                status: 'pending',
                respondedDate: null,
                comment: ''
            };
        });
        
        // Create meeting object
	const meeting = {
    id: meetingId,
    title: title,
    type: type,
    location: location || 'Virtual Meeting',
    joinLink: joinLink,
    date: date,
    startTime: startTime,
    endTime: endTime,
    agenda: agenda || '',
    notes: notes || '',
    participants: selectedParticipants,
    attachments: attachments,
    organizer: currentUser.code || currentUser.username,
    rsvp: rsvp,
    attendance: {},
    status: 'scheduled',
    createdDate: new Date().toISOString()
};

console.log('Creating meeting:', meeting); // Debug log

// Save to Firestore
try {
    await saveToFirestore('meetings', meeting);
    console.log('Meeting saved successfully');
} catch (saveError) {
    console.error('Firestore save error:', saveError);
    throw new Error('Failed to save meeting to database: ' + saveError.message);
}
        
        // Send notifications to all participants
        for (const pCode of selectedParticipants) {
            await sendMeetingInvitationNotification(pCode, meeting);
        }
        
        showNotification(`Meeting created! Invitations sent to ${selectedParticipants.length} participants.`);
        closeModal();
        loadHRMeetingsPanel();
        
    } catch (error) {
        console.error('Error creating meeting:', error);
        alert('Error creating meeting. Please try again.');
    }
}

// Convert file to base64
function fileToBase64(file) {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve(reader.result);
        reader.onerror = error => reject(error);
    });
}

// Save meeting as draft
async function saveMeetingAsDraft() {
    const title = document.getElementById('meetingTitle').value.trim();
    
    if (!title) {
        alert('Please enter at least a meeting title to save as draft');
        return;
    }
    
    try {
        const type = document.getElementById('meetingType').value;
        const location = document.getElementById('meetingLocation').value.trim();
        const date = document.getElementById('meetingDate').value;
        const startTime = document.getElementById('meetingStartTime').value;
        const endTime = document.getElementById('meetingEndTime').value;
        const agenda = document.getElementById('meetingAgenda').value.trim();
        const notes = document.getElementById('meetingNotes').value.trim();
        
        const selectedParticipants = Array.from(document.querySelectorAll('.participant-check:checked'))
            .map(checkbox => checkbox.value);
        
        const meetingId = `MEETING_DRAFT_${Date.now()}`;
        
        const draftMeeting = {
            id: meetingId,
            title: title,
            type: type,
            location: location,
            date: date,
            startTime: startTime,
            endTime: endTime,
            agenda: agenda,
            notes: notes,
            participants: selectedParticipants,
            organizer: currentUser.code || currentUser.username,
            status: 'draft',
            createdDate: new Date().toISOString()
        };
        
        await saveToFirestore('meetings', draftMeeting);
        
        showNotification('Meeting saved as draft!');
        closeModal();
        loadHRMeetingsPanel();
        
    } catch (error) {
        console.error('Error saving draft:', error);
        alert('Error saving draft. Please try again.');
    }
}

// Send meeting invitation notification
async function sendMeetingInvitationNotification(empCode, meeting) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const meetingDate = new Date(meeting.date).toLocaleDateString('en-US', { 
        weekday: 'long', 
        month: 'long', 
        day: 'numeric', 
        year: 'numeric' 
    });
    
    const message = `New meeting invitation: ${meeting.title} on ${meetingDate} at ${meeting.startTime}`;
    
    // Create notification record
    const notification = {
        id: `NOTIF_MEETING_${Date.now()}_${empCode}`,
        empCode: empCode,
        type: 'meeting',
        meetingId: meeting.id,
        message: message,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    // Send browser notification if permission granted
    if ('Notification' in window && Notification.permission === 'granted') {
        new Notification('Meeting Invitation', {
            body: message,
            icon: '📅',
            tag: `meeting-${meeting.id}`,
            requireInteraction: false
        });
    }
    
    // Send email notification (if email service configured)
    await sendEmailNotification(
        employee.email,
        'New Meeting Invitation',
        message,
        `You have been invited to: ${meeting.title}`
    );
}

// View meeting responses
async function viewMeetingResponses(meetingId) {
    const allMeetings = await getFromFirestore('meetings');
    const meeting = allMeetings.find(m => m.id === meetingId);
    
    if (!meeting) {
        alert('Meeting not found');
        return;
    }
    
    const rsvpData = meeting.rsvp || {};
    
    const participantsList = meeting.participants.map(pCode => {
        const emp = authorizedEmployees[pCode];
        const empName = emp ? emp.name : pCode;
        const rsvp = rsvpData[pCode] || { status: 'pending', comment: '', respondedDate: null };
        
        let statusBadge = '';
        if (rsvp.status === 'accepted') {
            statusBadge = '<span style="background: #27ae60; color: white; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: bold;">✓ ACCEPTED</span>';
        } else if (rsvp.status === 'declined') {
            statusBadge = '<span style="background: #e74c3c; color: white; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: bold;">✗ DECLINED</span>';
        } else if (rsvp.status === 'tentative') {
            statusBadge = '<span style="background: #f39c12; color: white; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: bold;">? TENTATIVE</span>';
        } else {
            statusBadge = '<span style="background: #95a5a6; color: white; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: bold;">⏳ PENDING</span>';
        }
        
        return `
            <div style="background: white; border: 1px solid #dee2e6; border-radius: 8px; padding: 15px; margin: 10px 0;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
                    <div>
                        <strong style="font-size: 15px;">${empName}</strong>
                        <div style="font-size: 12px; color: #666; margin-top: 3px;">${pCode}</div>
                    </div>
                    <div>
                        ${statusBadge}
                    </div>
                </div>
                
                ${rsvp.respondedDate ? `
                    <div style="font-size: 12px; color: #666; margin-top: 8px;">
                        Responded: ${new Date(rsvp.respondedDate).toLocaleString()}
                    </div>
                ` : ''}
                
                ${rsvp.comment ? `
                    <div style="background: #f8f9fa; padding: 10px; border-radius: 5px; margin-top: 10px; font-size: 13px; border-left: 3px solid ${
                        rsvp.status === 'declined' ? '#e74c3c' : '#3498db'
                    };">
                        <strong>Comment:</strong> ${rsvp.comment}
                    </div>
                ` : ''}
            </div>
        `;
    }).join('');
    
    const totalParticipants = meeting.participants.length;
    const acceptedCount = Object.values(rsvpData).filter(r => r.status === 'accepted').length;
    const declinedCount = Object.values(rsvpData).filter(r => r.status === 'declined').length;
    const tentativeCount = Object.values(rsvpData).filter(r => r.status === 'tentative').length;
    const pendingCount = totalParticipants - acceptedCount - declinedCount - tentativeCount;
    
    const modal = createModal(`
        <h2>📊 Meeting Responses: ${meeting.title}</h2>
        
        <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin: 20px 0;">
            <h4 style="margin: 0 0 15px 0;">Response Summary</h4>
            <div class="response-summary">
                <div class="response-stat accepted">
                    <div class="response-stat-value">${acceptedCount}</div>
                    <div class="response-stat-label">Accepted</div>
                </div>
                <div class="response-stat declined">
                    <div class="response-stat-value">${declinedCount}</div>
                    <div class="response-stat-label">Declined</div>
                </div>
                <div class="response-stat tentative">
                    <div class="response-stat-value">${tentativeCount}</div>
                    <div class="response-stat-label">Tentative</div>
                </div>
                <div class="response-stat pending">
                    <div class="response-stat-value">${pendingCount}</div>
                    <div class="response-stat-label">Pending</div>
                </div>
            </div>
        </div>
        
        <div style="margin: 20px 0;">
            <h4>Participant Details (${totalParticipants}):</h4>
            <div style="max-height: 500px; overflow-y: auto;">
                ${participantsList}
            </div>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            ${pendingCount > 0 ? `
                <button onclick="sendReminderToPending('${meetingId}')" class="btn" style="background: #9b59b6; margin-right: 10px;">
                    Send Reminder to Pending (${pendingCount})
                </button>
            ` : ''}
            <button onclick="exportMeetingResponses('${meetingId}')" class="btn" style="background: #27ae60; margin-right: 10px;">
                Export Responses
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}

// Send reminder to pending participants
async function sendReminderToPending(meetingId) {
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        const rsvpData = meeting.rsvp || {};
        const pendingParticipants = meeting.participants.filter(pCode => {
            const status = rsvpData[pCode] ? rsvpData[pCode].status : 'pending';
            return status === 'pending';
        });
        
        if (pendingParticipants.length === 0) {
            showNotification('No pending participants to remind');
            return;
        }
        
        if (!confirm(`Send reminder to ${pendingParticipants.length} pending participant(s)?`)) {
            return;
        }
        
        for (const pCode of pendingParticipants) {
            await sendMeetingReminderNotification(pCode, meeting);
        }
        
        showNotification(`Reminder sent to ${pendingParticipants.length} participant(s)!`);
        
    } catch (error) {
        console.error('Error sending reminders:', error);
        alert('Error sending reminders. Please try again.');
    }
}

// Send meeting reminder notification
async function sendMeetingReminderNotification(empCode, meeting) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const meetingDate = new Date(meeting.date).toLocaleDateString('en-US', { 
        weekday: 'long', 
        month: 'long', 
        day: 'numeric', 
        year: 'numeric' 
    });
    
    const message = `REMINDER: Please respond to meeting invitation - ${meeting.title} on ${meetingDate} at ${meeting.startTime}`;
    
    // Create notification record
    const notification = {
        id: `NOTIF_REMINDER_${Date.now()}_${empCode}`,
        empCode: empCode,
        type: 'meeting_reminder',
        meetingId: meeting.id,
        message: message,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    // Send browser notification
    if ('Notification' in window && Notification.permission === 'granted') {
        new Notification('Meeting Reminder', {
            body: message,
            icon: '⏰',
            tag: `meeting-reminder-${meeting.id}`,
            requireInteraction: true
        });
    }
    
    // Send email
    await sendEmailNotification(
        employee.email,
        'Meeting Invitation Reminder',
        message,
        `Please respond to: ${meeting.title}`
    );
}

// Export meeting responses
async function exportMeetingResponses(meetingId) {
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        const rsvpData = meeting.rsvp || {};
        
        const csvRows = [
            ['Meeting Title', meeting.title],
            ['Date', meeting.date],
            ['Time', `${meeting.startTime} - ${meeting.endTime}`],
            ['Location', meeting.location || 'Not specified'],
            ['Total Participants', meeting.participants.length],
            [],
            ['Participant Name', 'Employee Code', 'Response', 'Responded Date', 'Comment']
        ];
        
        meeting.participants.forEach(pCode => {
            const emp = authorizedEmployees[pCode];
            const empName = emp ? emp.name : pCode;
            const rsvp = rsvpData[pCode] || { status: 'pending', comment: '', respondedDate: null };
            
            csvRows.push([
                empName,
                pCode,
                rsvp.status.toUpperCase(),
                rsvp.respondedDate ? new Date(rsvp.respondedDate).toLocaleString() : 'Not responded',
                rsvp.comment || ''
            ]);
        });
        
        const csvContent = csvRows.map(row => row.map(cell => `"${cell}"`).join(',')).join('\n');
        downloadCSV(csvContent, `meeting_responses_${meeting.id}_${new Date().toISOString().split('T')[0]}.csv`);
        
        showNotification('Meeting responses exported successfully!');
        
    } catch (error) {
        console.error('Error exporting responses:', error);
        alert('Error exporting responses. Please try again.');
    }
}

// Edit meeting
async function editMeeting(meetingId) {
    const allMeetings = await getFromFirestore('meetings');
    const meeting = allMeetings.find(m => m.id === meetingId);
    
    if (!meeting) {
        alert('Meeting not found');
        return;
    }
    
    const modal = createModal(`
        <h2>✏️ Edit Meeting</h2>
        
        <div style="max-height: 70vh; overflow-y: auto; padding-right: 10px;">
            <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <h3 style="margin: 0 0 15px 0; color: #2c3e50;">Basic Information</h3>
                
                <div style="margin-bottom: 15px;">
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Meeting Title *</label>
                    <input type="text" id="editMeetingTitle" value="${meeting.title}" 
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                </div>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 15px;">
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Meeting Type *</label>
                        <select id="editMeetingType" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                            <option value="QA Review" ${meeting.type === 'QA Review' ? 'selected' : ''}>QA Review</option>
                            <option value="Training" ${meeting.type === 'Training' ? 'selected' : ''}>Training</option>
                            <option value="Department Meeting" ${meeting.type === 'Department Meeting' ? 'selected' : ''}>Department Meeting</option>
                            <option value="Emergency" ${meeting.type === 'Emergency' ? 'selected' : ''}>Emergency</option>
                            <option value="Other" ${meeting.type === 'Other' ? 'selected' : ''}>Other</option>
                        </select>
                    </div>
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Location</label>
                        <input type="text" id="editMeetingLocation" value="${meeting.location || ''}" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px;">
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Date *</label>
                        <input type="date" id="editMeetingDate" value="${meeting.date}" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">Start Time *</label>
                        <input type="time" id="editMeetingStartTime" value="${meeting.startTime}" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-weight: 500;">End Time *</label>
                        <input type="time" id="editMeetingEndTime" value="${meeting.endTime}" 
                            style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                    </div>
                </div>
            </div>
            
            <div style="background: #fff3cd; padding: 20px; border-radius: 8px; margin: 20px 0;">
                <h3 style="margin: 0 0 15px 0; color: #856404;">Meeting Details</h3>
                
                <div style="margin-bottom: 15px;">
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Agenda</label>
                    <textarea id="editMeetingAgenda" rows="4" 
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: inherit;">${meeting.agenda || ''}</textarea>
                </div>
                
                <div>
                    <label style="display: block; margin-bottom: 5px; font-weight: 500;">Additional Notes</label>
                    <textarea id="editMeetingNotes" rows="3" 
                        style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: inherit;">${meeting.notes || ''}</textarea>
                </div>
            </div>
        </div>
        
        <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px; padding-top: 20px; border-top: 2px solid #ecf0f1;">
            <button onclick="saveEditedMeeting('${meetingId}')" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                💾 Save Changes & Notify
            </button>
            <button onclick="closeModal()" class="btn" style="background: #6c757d;">
                Cancel
            </button>
        </div>
    `);
}

// Save edited meeting
async function saveEditedMeeting(meetingId) {
    const title = document.getElementById('editMeetingTitle').value.trim();
    const type = document.getElementById('editMeetingType').value;
    const location = document.getElementById('editMeetingLocation').value.trim();
    const date = document.getElementById('editMeetingDate').value;
    const startTime = document.getElementById('editMeetingStartTime').value;
    const endTime = document.getElementById('editMeetingEndTime').value;
    const agenda = document.getElementById('editMeetingAgenda').value.trim();
    const notes = document.getElementById('editMeetingNotes').value.trim();
    
    if (!title || !date || !startTime || !endTime) {
        alert('Please fill in all required fields');
        return;
    }
    
    if (startTime >= endTime) {
        alert('End time must be after start time');
        return;
    }
    
    try {
        await updateFirestoreDoc('meetings', meetingId, {
            title: title,
            type: type,
            location: location,
            date: date,
            startTime: startTime,
            endTime: endTime,
            agenda: agenda,
            notes: notes,
            lastModified: new Date().toISOString(),
            modifiedBy: currentUser.code || currentUser.username
        });
        
        // Notify all participants of the update
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (meeting) {
            for (const pCode of meeting.participants) {
                await sendMeetingUpdateNotification(pCode, meeting);
            }
        }
        
        showNotification('Meeting updated! Participants have been notified.');
        closeModal();
        loadHRMeetingsPanel();
        
    } catch (error) {
        console.error('Error updating meeting:', error);
        alert('Error updating meeting. Please try again.');
    }
}

// Send meeting update notification
async function sendMeetingUpdateNotification(empCode, meeting) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const message = `Meeting updated: ${meeting.title} - Please check new details`;
    
    const notification = {
        id: `NOTIF_UPDATE_${Date.now()}_${empCode}`,
        empCode: empCode,
        type: 'meeting_update',
        meetingId: meeting.id,
        message: message,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    if ('Notification' in window && Notification.permission === 'granted') {
        new Notification('Meeting Updated', {
            body: message,
            icon: '📅',
            tag: `meeting-update-${meeting.id}`
        });
    }
}

// Cancel meeting
async function cancelMeeting(meetingId) {
    if (!confirm('Cancel this meeting? All participants will be notified.')) {
        return;
    }
    
    const reason = prompt('Enter cancellation reason (optional):');
    
    try {
        const allMeetings = await getFromFirestore('meetings');
        const meeting = allMeetings.find(m => m.id === meetingId);
        
        if (!meeting) {
            alert('Meeting not found');
            return;
        }
        
        await updateFirestoreDoc('meetings', meetingId, {
            status: 'cancelled',
            cancellationReason: reason || 'No reason provided',
            cancelledBy: currentUser.code || currentUser.username,
            cancelledDate: new Date().toISOString()
        });
        
        // Notify all participants
        for (const pCode of meeting.participants) {
            await sendMeetingCancellationNotification(pCode, meeting, reason);
        }
        
        showNotification('Meeting cancelled. Participants have been notified.');
        loadHRMeetingsPanel();
        
    } catch (error) {
        console.error('Error cancelling meeting:', error);
        alert('Error cancelling meeting. Please try again.');
    }
}

// Send meeting cancellation notification
async function sendMeetingCancellationNotification(empCode, meeting, reason) {
    const employee = authorizedEmployees[empCode];
    if (!employee) return;
    
    const meetingDate = new Date(meeting.date).toLocaleDateString('en-US', { 
        weekday: 'long', 
        month: 'long', 
        day: 'numeric', 
        year: 'numeric' 
    });
    
    const message = `Meeting CANCELLED: ${meeting.title} on ${meetingDate}. Reason: ${reason || 'Not specified'}`;
    
    const notification = {
        id: `NOTIF_CANCEL_${Date.now()}_${empCode}`,
        empCode: empCode,
        type: 'meeting_cancelled',
        meetingId: meeting.id,
        message: message,
        acknowledged: false,
        createdDate: new Date().toISOString()
    };
    
    await saveToFirestore('schedule_notifications', notification);
    
    if ('Notification' in window && Notification.permission === 'granted') {
        new Notification('Meeting Cancelled', {
            body: message,
            icon: '❌',
            tag: `meeting-cancel-${meeting.id}`,
            requireInteraction: true
        });
    }
    
    await sendEmailNotification(
        employee.email,
        'Meeting Cancelled',
        message,
        `The meeting "${meeting.title}" has been cancelled`
    );
}
	
// ==============================================
// HR REPORTS DASHBOARD SYSTEM
// ==============================================
async function loadHRReportsPanel() {
    if (currentUser.role !== 'hr' && currentUser.role !== 'admin') {
        const hasPermission = currentUser.permissions && 
                             (currentUser.permissions.includes('report_viewer') || 
                              currentUser.permissions.includes('report_manager'));
        
        if (!hasPermission) return;
    }
    
    try {
        console.log('[HR Reports] Loading panel...');
        await loadBodyPartRules();
        
        // Load all reports from Firestore
        allReportsData = await getFromFirestore('daily_reports');
        console.log('[HR Reports] Loaded', allReportsData.length, 'reports from Firestore');
        
        // Sort by timestamp (newest first)
        allReportsData.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
        
        const filterFrom = document.getElementById('reportsFilterFrom');
        const filterTo = document.getElementById('reportsFilterTo');

        // Only set on very first load (when both are completely empty)
        if (!filterFrom.value && !filterTo.value) {
            const today = new Date().toISOString().split('T')[0];
            filterFrom.value = today;
            filterTo.value = today;
        }
                
        // Populate radiologist filter
        populateRadiologistFilterForReports();

        // ✅ FIX: Populate institution filter from admin-managed list
        const institutionFilter = document.getElementById('filterInstitution');
        if (institutionFilter) {
            institutionFilter.innerHTML = '<option value="">All Institutions</option>';
            
            // Use institutions array from admin settings
            institutions.forEach(inst => {
                const option = document.createElement('option');
                option.value = inst;
                option.textContent = inst;
                institutionFilter.appendChild(option);
            });
            
            console.log('[Institution Filter] ✅ Populated with', institutions.length, 'institutions');
        }

        // Apply filters and render
        applyReportsFilters();
        
        console.log('[HR Reports] ✅ Panel loaded successfully');
        
    } catch (error) {
        console.error('[HR Reports] ❌ Error loading panel:', error);
        document.getElementById('reportsTableBody').innerHTML = `
            <tr>
                <td colspan="8" style="padding: 40px; text-align: center; color: #e74c3c;">
                    Error loading reports. Please try again.
                </td>
            </tr>
        `;
    }
}

function populateRadiologistFilterForReports() {
    const radFilter = document.getElementById('reportsFilterRad');
    if (!radFilter) return;
    
    radFilter.innerHTML = '<option value="">All Radiologists</option>';
    
    Object.entries(authorizedEmployees)
        .filter(([code, emp]) => emp.role === 'employee')
        .sort((a, b) => a[1].name.localeCompare(b[1].name))
        .forEach(([code, emp]) => {
            radFilter.innerHTML += `<option value="${code}">${emp.name} (${code})</option>`;
        });
}


function clearReportsFilters() {
    const today = new Date().toISOString().split('T')[0];
    document.getElementById('reportsFilterFrom').value = today;
    document.getElementById('reportsFilterTo').value = today;
    document.getElementById('reportsFilterFromTime').value = '';
    document.getElementById('reportsFilterToTime').value = '';
    document.getElementById('reportsFilterRad').value = '';
    document.getElementById('reportsFilterModality').value = '';
    document.getElementById('reportsSearchText').value = '';
    document.getElementById('filterInstitution').value = '';
	const filterAccession = document.getElementById('filterAccession');
		if (filterAccession) filterAccession.value = '';

    
    applyReportsFilters();
}

function updateReportsStatistics(reports) {
    console.log('[Statistics] Updating with', reports.length, 'reports');
    
    // ✅ FIX: Sum reportCount for each report, not just count documents
    const totalCount = reports.reduce((sum, r) => {
        const count = r.reportCount || 1;
        console.log('[Statistics] Report:', r.empCode, 'Count:', count);
        return sum + count;
    }, 0);
    
    const usCount = reports
        .filter(r => r.modality === 'US')
        .reduce((sum, r) => sum + (r.reportCount || 1), 0);
    
    const ctCount = reports
        .filter(r => r.modality === 'CT')
        .reduce((sum, r) => sum + (r.reportCount || 1), 0);
    
    const mriCount = reports
        .filter(r => r.modality === 'MRI')
        .reduce((sum, r) => sum + (r.reportCount || 1), 0);
    
    const xrCount = reports
        .filter(r => r.modality === 'XR')
        .reduce((sum, r) => sum + (r.reportCount || 1), 0);
    
    console.log('[Statistics] Total:', totalCount, 'US:', usCount, 'CT:', ctCount, 'MRI:', mriCount, 'XR:', xrCount);
    
    document.getElementById('totalReportsCount').textContent = totalCount;
    document.getElementById('usReportsCount').textContent = usCount;
    document.getElementById('ctReportsCount').textContent = ctCount;
    document.getElementById('mriReportsCount').textContent = mriCount;
    
    const xrElement = document.getElementById('xrReportsCount');
    if (xrElement) {
        xrElement.textContent = xrCount;
    }
}

function renderReportsTable(reports) {
    const tbody = document.getElementById('reportsTableBody');
    
    // Update counts
    document.getElementById('reportsShowingCount').textContent = reports.length;
    document.getElementById('reportsTotalCount').textContent = allReportsData.length;
    
    if (reports.length === 0) {
        tbody.innerHTML = `
            <tr>
                <td colspan="9" style="padding: 60px; text-align: center; color: #666;">
                    No reports found matching your filters
                </td>
            </tr>
        `;
        return;
    }
    
    const html = reports.map(report => {
        const employee = authorizedEmployees[report.empCode];
        const empName = employee ? employee.name : report.empCode;
        
        const isSelected = selectedReportIds.has(report.id);
        
        // Modality color badges
        const modalityColors = {
            'US': 'background: #9b59b6; color: white;',
            'CT': 'background: #3498db; color: white;',
            'MRI': 'background: #e74c3c; color: white;',
            'XR': 'background: #f39c12; color: white;',
            'Biotronics': 'background: #27ae60; color: white;'
        };
        
        // Report type badges
        const typeColors = {
            'new': 'background: #27ae60; color: white;',
            'addendum': 'background: #f39c12; color: white;',
            'update': 'background: #3498db; color: white;'
        };
        
        return `
            <tr style="border-bottom: 1px solid #ecf0f1; background: ${isSelected ? '#e3f2fd' : 'white'};">
                <td style="padding: 12px; text-align: center;">
                    <input type="checkbox" class="report-checkbox" data-report-id="${report.id}" 
                           ${isSelected ? 'checked' : ''} onchange="toggleReportSelection('${report.id}')" 
                           style="transform: scale(1.3);">
                </td>
                <td style="padding: 12px;">${report.submittedTime || 'N/A'}</td>
                <td style="padding: 12px; font-weight: 500;">${empName}</td>
				<td style="padding: 12px; text-align: center;">
					<span style="background:#ecf0f1; padding:4px 8px; border-radius:8px; font-size:11px;">
						${report.institution || '—'}
					</span>
				</td>
								<td style="padding: 12px; text-align: center;">
					<span style="background:#e3f2fd; padding:4px 8px; border-radius:8px; font-size:11px;">
						${report.accessionNumber || '—'}
					</span>
				</td>

                <td style="padding: 12px; text-align: center;">
                    <span style="padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold; ${modalityColors[report.modality] || ''}">
                        ${report.modality || 'N/A'}
                    </span>
                </td>
                <td style="padding: 12px; text-align: center;">
					<div style="font-weight: bold; font-size: 14px;">${report.wordCount || 0}</div>
					<div style="font-size: 10px; color: #666; margin-top: 2px;">
						${report.reportCount > 1 ? `Counts as: ${report.reportCount} reports` : '1 report'}
					</div>
				</td>
                <td style="padding: 12px; text-align: center;">
                    <span style="padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold; ${typeColors[report.reportType] || ''}">
                        ${(report.reportType || 'new').toUpperCase()}
                    </span>
                </td>
                <td style="padding: 12px; text-align: center;">
                    <div style="display: flex; gap: 5px; justify-content: center;">
                        <button onclick="viewReportDetails('${report.id}')" class="btn" style="background: #3498db; padding: 6px 10px; font-size: 11px;" title="View Report">
                            👁️
                        </button>
                        <button onclick="downloadSingleReport('${report.id}')" class="btn" style="background: #27ae60; padding: 6px 10px; font-size: 11px;" title="Download">
                            📥
                        </button>
                        <button onclick="deleteSingleReport('${report.id}')" class="btn" style="background: #e74c3c; padding: 6px 10px; font-size: 11px;" title="Delete">
                            🗑️
                        </button>
                    </div>
                </td>
            </tr>
        `;
    }).join('');
    
    tbody.innerHTML = html;
}

// ==============================================
// BULK SELECTION SYSTEM
// ==============================================

function toggleSelectAllReports() {
    const checkbox = document.getElementById('selectAllReportsCheckbox');
    const isChecked = checkbox.checked;
    
    if (isChecked) {
        // Select all filtered reports
        filteredReportsData.forEach(report => {
            selectedReportIds.add(report.id);
        });
    } else {
        // Deselect all
        selectedReportIds.clear();
    }
    
    // Re-render table to show selection
    renderReportsTable(filteredReportsData);
    
    // Update bulk action bar
    updateBulkActionBar();
}

function toggleReportSelection(reportId) {
    if (selectedReportIds.has(reportId)) {
        selectedReportIds.delete(reportId);
    } else {
        selectedReportIds.add(reportId);
    }
    
    // Update "Select All" checkbox state
    const selectAllCheckbox = document.getElementById('selectAllReportsCheckbox');
    if (selectAllCheckbox) {
        selectAllCheckbox.checked = selectedReportIds.size === filteredReportsData.length && filteredReportsData.length > 0;
    }
    
    // Update bulk action bar
    updateBulkActionBar();
}

function updateBulkActionBar() {
    const bulkBar = document.getElementById('bulkActionBar');
    const countSpan = document.getElementById('selectedReportsCount');
    
    if (selectedReportIds.size > 0) {
        bulkBar.style.display = 'block';
        countSpan.textContent = selectedReportIds.size;
    } else {
        bulkBar.style.display = 'none';
    }
}

function deselectAllReports() {
    selectedReportIds.clear();
    
    // Uncheck "Select All"
    const selectAllCheckbox = document.getElementById('selectAllReportsCheckbox');
    if (selectAllCheckbox) {
        selectAllCheckbox.checked = false;
    }
    
    // Re-render table
    renderReportsTable(filteredReportsData);
    
    // Hide bulk action bar
    updateBulkActionBar();
}

// ==============================================
// VIEW REPORT DETAILS
// ==============================================

async function viewReportDetails(reportId) {
    const report = allReportsData.find(r => r.id === reportId);
    
    if (!report) {
        alert('Report not found');
        return;
    }
    
    const employee = authorizedEmployees[report.empCode];
    const empName = employee ? employee.name : report.empCode;
    
    // Modality colors
    const modalityColors = {
        'US': '#9b59b6',
        'CT': '#3498db',
        'MRI': '#e74c3c',
        'XR': '#f39c12',
        'Biotronics': '#27ae60'
    };
    
    const modalityColor = modalityColors[report.modality] || '#95a5a6';
    
    const modal = createModal(`
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; padding-bottom: 15px; border-bottom: 3px solid ${modalityColor};">
            <div>
                <h2 style="margin: 0; color: #2c3e50;">📄 Report Details</h2>
                <div style="font-size: 14px; color: #666; margin-top: 5px;">
                    ${empName} (${report.empCode}) | ${new Date(report.timestamp).toLocaleString()}
                </div>
            </div>
            <button onclick="closeModal()" style="background: #95a5a6; color: white; border: none; padding: 8px 15px; border-radius: 5px; cursor: pointer; font-size: 20px;">
                ✕
            </button>
        </div>
        
        <!-- Report Metadata -->
        <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
            <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px;">
                <div>
                    <div style="font-size: 11px; color: #666; text-transform: uppercase; margin-bottom: 5px;">Modality</div>
                    <div style="font-weight: bold; color: ${modalityColor}; font-size: 18px;">${report.modality || 'N/A'}</div>
                </div>
                <div>
                    <div style="font-size: 11px; color: #666; text-transform: uppercase; margin-bottom: 5px;">Word Count</div>
                    <div style="font-weight: bold; color: #2c3e50; font-size: 18px;">${report.wordCount || 0} words</div>
                </div>
                <div>
                    <div style="font-size: 11px; color: #666; text-transform: uppercase; margin-bottom: 5px;">Report Type</div>
                    <div style="font-weight: bold; color: #2c3e50; font-size: 18px;">${(report.reportType || 'new').toUpperCase()}</div>
                </div>
            </div>
        </div>
        
        <!-- Report Content -->
        <div style="margin-bottom: 20px;">
            <div style="background: #2c3e50; color: white; padding: 12px 15px; border-radius: 8px 8px 0 0; font-weight: bold;">
                📋 Report Content
            </div>
            <div style="background: white; border: 2px solid #ecf0f1; border-top: none; border-radius: 0 0 8px 8px; padding: 20px; max-height: 500px; overflow-y: auto; font-family: 'Courier New', monospace; font-size: 13px; line-height: 1.8; white-space: pre-wrap; word-wrap: break-word;">
${escapeHtml(report.reportText || 'No report content available')}</div>
        </div>
        
        <!-- Action Buttons -->
        <div style="display: flex; gap: 10px; justify-content: flex-end; padding-top: 15px; border-top: 2px solid #ecf0f1;">
            <button onclick="downloadSingleReport('${reportId}')" class="btn" style="background: #27ae60; padding: 10px 20px;">
                📥 Download Report
            </button>
            <button onclick="copyReportToClipboard('${reportId}')" class="btn" style="background: #3498db; padding: 10px 20px;">
                📋 Copy to Clipboard
            </button>
            <button onclick="deleteSingleReport('${reportId}')" class="btn" style="background: #e74c3c; padding: 10px 20px;">
                🗑️ Delete Report
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 10px 20px;">
                Close
            </button>
        </div>
    `);
}

function copyReportToClipboard(reportId) {
    const report = allReportsData.find(r => r.id === reportId);
    
    if (!report) {
        alert('Report not found');
        return;
    }
    
    navigator.clipboard.writeText(report.reportText).then(() => {
        showNotification('✓ Report copied to clipboard');
    }).catch(err => {
        console.error('Copy failed:', err);
        alert('Failed to copy report. Please try again.');
    });
}

// ==============================================
// EXPORT FUNCTIONS
// ==============================================

function downloadSingleReport(reportId) {
    const report = allReportsData.find(r => r.id === reportId);
    
    if (!report) {
        alert('Report not found');
        return;
    }
    
    const employee = authorizedEmployees[report.empCode];
    const empName = employee ? employee.name : report.empCode;
    
    // Create filename
    const date = report.submittedDate || new Date().toISOString().split('T')[0];
    const time = report.submittedTime ? report.submittedTime.replace(/:/g, '-') : 'unknown';
    const filename = `Report_${empName}_${report.modality}_${date}_${time}.txt`;
    
    // ✅ FIX: Added Institution field
    const content = `
RADIOLOGY REPORT
================

Radiologist: ${empName} (${report.empCode})
Date: ${date}
Time: ${report.submittedTime || 'N/A'}
Modality: ${report.modality || 'N/A'}
Institution: ${report.institution || 'Not specified'}
Accession No: ${report.accessionNumber || 'Not specified'}
Word Count: ${report.wordCount || 0}
Report Type: ${(report.reportType || 'new').toUpperCase()}

REPORT CONTENT:
${'-'.repeat(80)}

${report.reportText || 'No content'}

${'-'.repeat(80)}
Generated: ${new Date().toLocaleString()}
    `.trim();
    
    // Download file
    const blob = new Blob([content], { type: 'text/plain' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    window.URL.revokeObjectURL(url);
    
    showNotification('✓ Report downloaded');
}

async function exportSelectedReports() {
    if (selectedReportIds.size === 0) {
        alert('No reports selected. Please select reports first.');
        return;
    }
    
    // Get selected reports
    const selectedReports = allReportsData.filter(r => selectedReportIds.has(r.id));
    
    // Show export format modal
    showExportFormatModal(selectedReports);
}

function showExportFormatModal(reports) {

	window.currentExportReportIds = reports.map(r => r.id);
	
    const modal = createModal(`
        <h2 style="color: #2c3e50; margin-bottom: 20px;">📥 Export ${reports.length} Report(s)</h2>
        
        <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
            <h4 style="margin: 0 0 15px 0;">Choose Export Format:</h4>
            
            <label style="display: block; padding: 15px; margin: 10px 0; background: white; border: 2px solid #ddd; border-radius: 8px; cursor: pointer; transition: all 0.2s;" onmouseover="this.style.borderColor='#27ae60'; this.style.background='#e8f5e9';" onmouseout="this.style.borderColor='#ddd'; this.style.background='white';">
                <input type="radio" name="exportFormat" value="excel" checked style="margin-right: 10px; transform: scale(1.3);">
                <strong>📊 Excel Spreadsheet (.xlsx)</strong>
                <div style="font-size: 12px; color: #666; margin-left: 30px; margin-top: 5px;">Table format with metadata - Best for analysis</div>
            </label>
            
            <label style="display: block; padding: 15px; margin: 10px 0; background: white; border: 2px solid #ddd; border-radius: 8px; cursor: pointer; transition: all 0.2s;" onmouseover="this.style.borderColor='#3498db'; this.style.background='#e3f2fd';" onmouseout="this.style.borderColor='#ddd'; this.style.background='white';">
                <input type="radio" name="exportFormat" value="csv" style="margin-right: 10px; transform: scale(1.3);">
                <strong>📄 CSV File (.csv)</strong>
                <div style="font-size: 12px; color: #666; margin-left: 30px; margin-top: 5px;">Comma-separated values - Universal compatibility</div>
            </label>
            
            <label style="display: block; padding: 15px; margin: 10px 0; background: white; border: 2px solid #ddd; border-radius: 8px; cursor: pointer; transition: all 0.2s;" onmouseover="this.style.borderColor='#e74c3c'; this.style.background='#ffebee';" onmouseout="this.style.borderColor='#ddd'; this.style.background='white';">
                <input type="radio" name="exportFormat" value="txt" style="margin-right: 10px; transform: scale(1.3);">
                <strong>📝 Text Files (.zip)</strong>
                <div style="font-size: 12px; color: #666; margin-left: 30px; margin-top: 5px;">Individual TXT files in ZIP archive</div>
            </label>
            
            <label style="display: block; padding: 15px; margin: 10px 0; background: white; border: 2px solid #ddd; border-radius: 8px; cursor: pointer; transition: all 0.2s;" onmouseover="this.style.borderColor='#9b59b6'; this.style.background='#f3e5f5';" onmouseout="this.style.borderColor='#ddd'; this.style.background='white';">
                <input type="radio" name="exportFormat" value="pdf" style="margin-right: 10px; transform: scale(1.3);">
                <strong>📕 Combined PDF</strong>
                <div style="font-size: 12px; color: #666; margin-left: 30px; margin-top: 5px;">All reports in one PDF document</div>
            </label>
        </div>
        
        <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin-bottom: 20px; border-left: 4px solid #f39c12;">
            <strong>📋 Export will include:</strong>
            <ul style="margin: 10px 0 0 20px; font-size: 13px;">
                <li>Radiologist name and code</li>
                <li>Date and time of submission</li>
                <li>Modality and report type</li>
                <li>Full report content</li>
                <li>Word count</li>
            </ul>
        </div>
        
       <div style="display: flex; gap: 10px; justify-content: flex-end;">
            <button onclick="executeExport()" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                📥 Export Now
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 12px 30px;">
                Cancel
            </button>
        </div>
    `);
}

async function executeExport() {
    const selectedFormat = document.querySelector('input[name="exportFormat"]:checked')?.value;
    
    if (!selectedFormat) {
        alert('Please select an export format');
        return;
    }
    
    // Get report IDs from global variable
    const reportIds = window.currentExportReportIds;
    
    if (!reportIds || reportIds.length === 0) {
        alert('No reports to export');
        return;
    }
    
    const reports = allReportsData.filter(r => reportIds.includes(r.id));
    
    closeModal();
    showNotification('⏳ Preparing export...');
    
    try {
        switch(selectedFormat) {
            case 'excel':
                await exportToExcel(reports);
                break;
            case 'csv':
                exportToCSV(reports);
                break;
            case 'txt':
                exportToZip(reports);
                break;
            case 'pdf':
                exportToPDF(reports);
                break;
        }
        
        showNotification(`✓ Exported ${reports.length} report(s) successfully!`);
        
        // Clean up
        delete window.currentExportReportIds;
        
    } catch (error) {
        console.error('Export error:', error);
        alert('Export failed: ' + error.message);
    }
}

async function exportToExcel(reports) {
    const headers = ['Date', 'Time', 'Radiologist', 'Employee Code', 'Modality', 'Institution', 'Accession No', 'Word Count', 'Report Type', 'Report Content'];
    
    const rows = reports.map(report => {
        const employee = authorizedEmployees[report.empCode];
        const empName = employee ? employee.name : report.empCode;
        
        // ✅ CLEAN the report content properly
        const cleanReportText = (report.reportText || '')
            .replace(/"/g, '""')           // Escape double quotes
            .replace(/\n/g, ' ')           // Remove line breaks
            .replace(/\r/g, ' ')           // Remove carriage returns
            .replace(/,/g, ';')            // Replace commas with semicolons
            .trim();
        
        return [
            report.submittedDate || '',
            report.submittedTime || '',
            empName,
            report.empCode,
            report.modality || '',
            report.institution || 'Not specified',
            report.accessionNumber || '',
            report.wordCount || 0,
            (report.reportType || 'new').toUpperCase(),
            `"${cleanReportText}"`
        ];
    });
    
    const csvContent = [
        headers.join(','),
        ...rows.map(row => row.join(','))
    ].join('\n');
    
    const BOM = '\uFEFF';
    const blob = new Blob([BOM + csvContent], { type: 'text/csv;charset=utf-8;' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `Reports_Export_${new Date().toISOString().split('T')[0]}.csv`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    window.URL.revokeObjectURL(url);
}

function exportToCSV(reports) {
    exportToExcel(reports); // Same implementation
}

function exportToZip(reports) {
    alert('ZIP export feature coming soon. For now, please use Excel or CSV export.');
    // Note: Would need JSZip library for actual implementation
}

function exportToPDF(reports) {
    alert('PDF export feature coming soon. For now, please use Excel or CSV export.');
    // Note: Would need jsPDF library for actual implementation
}

async function exportAllReports() {
    if (filteredReportsData.length === 0) {
        alert('No reports to export');
        return;
    }
    
    showExportFormatModal(filteredReportsData);
}

// ==============================================
// DELETE FUNCTIONS
// ==============================================

async function deleteSingleReport(reportId) {
    const report = allReportsData.find(r => r.id === reportId);
    
    if (!report) {
        alert('Report not found');
        return;
    }
    
    const employee = authorizedEmployees[report.empCode];
    const empName = employee ? employee.name : report.empCode;
    
    if (!confirm(`Delete this report?\n\nRadiologist: ${empName}\nDate: ${report.submittedDate}\nModality: ${report.modality}\n\nThis action cannot be undone!`)) {
        return;
    }
    
    try {
        // Delete from Firestore
        const snapshot = await db.collection('daily_reports').get();
        for (const doc of snapshot.docs) {
            if (doc.data().id === reportId) {
                await doc.ref.delete();
                break;
            }
        }
        
        showNotification('✓ Report deleted successfully');
        
        // Close modal if open
        closeModal();
        
        // Reload reports panel
        await loadHRReportsPanel();
        
    } catch (error) {
        console.error('Error deleting report:', error);
        alert('Error deleting report. Please try again.');
    }
}

async function deleteSelectedReports() {
    if (selectedReportIds.size === 0) {
        alert('No reports selected');
        return;
    }
    
    const confirmed = confirm(`Delete ${selectedReportIds.size} selected report(s)?\n\nThis action cannot be undone!`);
    
    if (!confirmed) return;
    
    try {
        showNotification('⏳ Deleting reports...');
        
        const snapshot = await db.collection('daily_reports').get();
        const deletePromises = [];
        
        snapshot.forEach(doc => {
            if (selectedReportIds.has(doc.data().id)) {
                deletePromises.push(doc.ref.delete());
            }
        });
        
        await Promise.all(deletePromises);
        
        showNotification(`✓ Deleted ${selectedReportIds.size} report(s) successfully`);
        
        // Clear selection
        selectedReportIds.clear();
        
        // Reload panel
        await loadHRReportsPanel();
        
    } catch (error) {
        console.error('Error deleting reports:', error);
        alert('Error deleting reports. Please try again.');
    }
}

// ==============================================
// DRAFT AUTO-SAVE SYSTEM
// ==============================================

// Start auto-save with user's preferred interval
function startAutoSave() {
    // Clear any existing interval
    if (autoSaveInterval) {
        clearInterval(autoSaveInterval);
    }
    
    // Don't start if user disabled auto-save
    if (userAutoSavePreference === 0) {
        return;
    }
    
    // Auto-save based on user preference
    autoSaveInterval = setInterval(() => {
        // Only save if user was active in last 3 minutes
        if (isUserActive) {
            saveDraft(true); // true = auto-save (silent)
        }
    }, userAutoSavePreference * 1000);
}

// Stop auto-save
function stopAutoSave() {
    if (autoSaveInterval) {
        clearInterval(autoSaveInterval);
        autoSaveInterval = null;
    }
}

// Update auto-save preference
async function updateAutoSavePreference() {
    const select = document.getElementById('autoSaveInterval');
    userAutoSavePreference = parseInt(select.value);
    
    // Save preference to Firestore
    try {
        await db.collection('user_preferences').doc(currentUser.code || currentUser.username).set({
            autoSaveInterval: userAutoSavePreference,
            updatedAt: new Date().toISOString()
        }, { merge: true });
    } catch (error) {
        console.error('Error saving preference:', error);
    }
    
    // Restart auto-save with new interval
    stopAutoSave();
    if (userAutoSavePreference > 0) {
        startAutoSave();
        showNotification(`Auto-save updated: Every ${userAutoSavePreference}s`);
    } else {
        showNotification('Auto-save disabled');
    }
}

// Load user's auto-save preference
async function loadAutoSavePreference() {
    try {
        const prefDoc = await db.collection('user_preferences').doc(currentUser.code || currentUser.username).get();
        
        if (prefDoc.exists) {
            const pref = prefDoc.data();
            userAutoSavePreference = pref.autoSaveInterval || 30;
            
            // Update dropdown
            const select = document.getElementById('autoSaveInterval');
            if (select) {
                select.value = userAutoSavePreference;
            }
        }
    } catch (error) {
        console.error('Error loading preference:', error);
    }
}

// Save draft to Firestore
async function saveDraft(isAutoSave = false) {
    try {
        const editor = document.getElementById('textEditor');
        const content = editor.innerHTML;
        
        if (!content.trim()) {
            return;
        }
        
        // Extract first line as report identifier (minimum 10 characters to avoid partial typing)
        const textContent = editor.textContent.trim();
        const lines = textContent.split('\n').filter(line => line.trim().length > 0);
        
        // Get first meaningful line (at least 10 chars)
        let reportHeading = '';
        for (let line of lines) {
            if (line.trim().length >= 10) {
                reportHeading = line.trim().substring(0, 100);
                break;
            }
        }
        
        // If heading is too short, don't save yet (user still typing)
        if (reportHeading.length < 10) {
            return;
        }
        
        // Check if this is the same report or a new one
        const isSameReport = (reportHeading === lastSavedReportHeading);
        
        // Don't save if same report and content unchanged
        if (isSameReport && content === lastSavedContent) {
            return;
        }
        
        const firstLine = reportHeading.substring(0, 60);
        const draftData = {
            content: content,
            preview: firstLine,
            reportHeading: reportHeading,
            userCode: currentUser.code || currentUser.username,
            userName: currentUser.name || currentUser.username,
            timestamp: new Date().toISOString(),
            wordCount: textContent.split(/\s+/).filter(word => word.length > 0).length
        };
        
        // Get existing drafts
        const userDraftsRef = db.collection('drafts').doc(currentUser.code || currentUser.username);
        const draftsDoc = await userDraftsRef.get();
        
        let existingDrafts = [];
        if (draftsDoc.exists && draftsDoc.data().savedDrafts) {
            existingDrafts = draftsDoc.data().savedDrafts;
        }
        
        if (isSameReport && existingDrafts.length > 0) {
            // Update existing draft (same report, just modified)
            existingDrafts[0] = draftData;
        } else {
            // New report - add at beginning, push others down
            existingDrafts.unshift(draftData);
            if (existingDrafts.length > 2) {
                existingDrafts = existingDrafts.slice(0, 2);
            }
        }
        
        // Save to Firestore
        await userDraftsRef.set({ savedDrafts: existingDrafts }, { merge: true });
        
        lastSavedContent = content;
        lastSavedReportHeading = reportHeading;
        lastSavedTimestamp = new Date();
        draftList = existingDrafts;
        
        updateLastSavedTime();
        
        if (!isAutoSave) {
            showNotification('✅ Draft saved successfully!');
        } else {
            showAutoSaveIndicator();
        }
        
    } catch (error) {
        console.error('Error saving draft:', error);
        if (!isAutoSave) {
            alert('Error saving draft. Please try again.');
        }
    }
}


// Load saved draft
async function loadDraft(draftIndex = null) {
    try {
        // If specific index provided, load that draft
        if (draftIndex !== null) {
            await loadSpecificDraft(draftIndex);
            return;
        }
        
        // Otherwise show menu (this shouldn't be called directly now)
        showNotification('Please use the dropdown to select a draft.');
        
    } catch (error) {
        console.error('Error loading draft:', error);
        alert('Error loading draft. Please try again.');
    }
}
	async function showDraftMenu() {
    try {
        const menu = document.getElementById('draftMenu');
        
        const draftDoc = await db.collection('drafts').doc(currentUser.code || currentUser.username).get();
        
        if (!draftDoc.exists || !draftDoc.data().savedDrafts || draftDoc.data().savedDrafts.length === 0) {
            menu.innerHTML = '<div style="padding:10px; color:#666;">No saved drafts</div>';
            menu.style.display = 'block';
            return;
        }
        
        const drafts = draftDoc.data().savedDrafts;
        draftList = drafts;
        
        let menuHTML = '';
        drafts.forEach((draft, index) => {
            const date = new Date(draft.timestamp);
            const timeAgo = getTimeAgo(date);
            
            menuHTML += `
                <div onclick="loadSpecificDraft(${index})" style="padding:10px; border-bottom:1px solid #eee; cursor:pointer; hover:background:#f5f5f5;" 
                     onmouseover="this.style.background='#f5f5f5'" 
                     onmouseout="this.style.background='white'">
                    <div style="font-size:12px; color:#333; margin-bottom:3px;">
                        <strong>Draft ${index + 1}:</strong> ${draft.preview}...
                    </div>
                    <div style="font-size:10px; color:#666;">
                        ${draft.wordCount} words • ${timeAgo}
                    </div>
                </div>
            `;
        });
        
        menu.innerHTML = menuHTML;
        menu.style.display = 'block';
        
    } catch (error) {
        console.error('Error showing draft menu:', error);
    }
}

function getTimeAgo(date) {
    const now = new Date();
    const diff = Math.floor((now - date) / 1000);
    
    if (diff < 60) return 'Just now';
    if (diff < 3600) return `${Math.floor(diff / 60)}m ago`;
    if (diff < 86400) return `${Math.floor(diff / 3600)}h ago`;
    return `${Math.floor(diff / 86400)}d ago`;
}

async function loadSpecificDraft(index) {
    try {
        const draftDoc = await db.collection('drafts').doc(currentUser.code || currentUser.username).get();
        
        if (!draftDoc.exists || !draftDoc.data().savedDrafts) {
            showNotification('No saved drafts found.');
            return;
        }
        
        const drafts = draftDoc.data().savedDrafts;
        if (!drafts[index]) {
            showNotification('Draft not found.');
            return;
        }
        
        const draft = drafts[index];
        const editor = document.getElementById('textEditor');
        
        const currentContent = editor.innerHTML.trim();
        if (currentContent && currentContent !== draft.content) {
            const draftDate = new Date(draft.timestamp).toLocaleString();
            if (!confirm(`Load saved draft from ${draftDate}?\n\nThis will replace current content.`)) {
                return;
            }
        }
        
        editor.innerHTML = draft.content;
        lastSavedContent = draft.content;
        lastSavedTimestamp = new Date(draft.timestamp);
        updateWordCount();
        updateLastSavedTime();
        
        showNotification(`✅ Draft loaded (${draft.wordCount} words)`);
        
        // Hide the menu after loading
        document.getElementById('draftMenu').style.display = 'none';
        
    } catch (error) {
        console.error('Error loading draft:', error);
        alert('Error loading draft. Please try again.');
    }
}

// Delete draft
async function deleteDraft() {
    try {
        if (!confirm('Delete saved draft?')) {
            return;
        }
        
        await db.collection('drafts').doc(currentUser.code || currentUser.username).delete();
        lastSavedContent = '';
        lastSavedTimestamp = null;
        document.getElementById('lastSavedTime').style.display = 'none';
        showNotification('✅ Draft deleted.');
        
    } catch (error) {
        console.error('Error deleting draft:', error);
        alert('Error deleting draft.');
    }
}

// Show subtle auto-save indicator
function showAutoSaveIndicator() {
    const indicator = document.getElementById('autoSaveIndicator');
    if (indicator) {
        indicator.style.opacity = '1';
        setTimeout(() => {
            indicator.style.opacity = '0';
        }, 2000);
    }
}

// Update last saved time display
function updateLastSavedTime() {
    const timeDisplay = document.getElementById('lastSavedTime');
    if (!timeDisplay || !lastSavedTimestamp) return;
    
    const now = new Date();
    const diff = Math.floor((now - lastSavedTimestamp) / 1000); // seconds
    
    let timeText = '';
    if (diff < 60) {
        timeText = 'Just now';
    } else if (diff < 3600) {
        timeText = `${Math.floor(diff / 60)}m ago`;
    } else {
        timeText = `${Math.floor(diff / 3600)}h ago`;
    }
    
    timeDisplay.textContent = timeText;
    timeDisplay.style.display = 'inline';
}

// Track user activity
function resetInactivityTimer() {
    isUserActive = true;
    
    // Clear existing timer
    if (inactivityTimer) {
        clearTimeout(inactivityTimer);
    }
    
    // Set user as inactive after 3 minutes of no activity
    inactivityTimer = setTimeout(() => {
        isUserActive = false;
    }, 180000); // 3 minutes
}

// Update last saved time every minute
setInterval(() => {
    if (lastSavedTimestamp) {
        updateLastSavedTime();
    }
}, 60000); // Update every minute

//==============================
// RICH TEXT FORMATTING FUNCTION
//===============================

function formatText(command) {
    document.execCommand(command, false, null);
    document.getElementById('textEditor').focus();
}

function changeFontSize() {
    const size = document.getElementById('fontSize').value;
    document.execCommand('fontSize', false, '7');
    const fontElements = document.getElementById('textEditor').querySelectorAll('font[size="7"]');
    fontElements.forEach(el => {
        el.removeAttribute('size');
        el.style.fontSize = size + 'px';
    });
    document.getElementById('textEditor').focus();
}

function insertBulletList() {
    document.execCommand('insertUnorderedList', false, null);
    document.getElementById('textEditor').focus();
}

function insertNumberList() {
    document.execCommand('insertOrderedList', false, null);
    document.getElementById('textEditor').focus();
}

function textToUpperCase() {
    const selection = window.getSelection();
    if (selection.rangeCount > 0) {
        const range = selection.getRangeAt(0);
        const selectedText = range.toString();
        if (selectedText) {
            range.deleteContents();
            range.insertNode(document.createTextNode(selectedText.toUpperCase()));
        }
    }
    document.getElementById('textEditor').focus();
}

function textToLowerCase() {
    const selection = window.getSelection();
    if (selection.rangeCount > 0) {
        const range = selection.getRangeAt(0);
        const selectedText = range.toString();
        if (selectedText) {
            range.deleteContents();
            range.insertNode(document.createTextNode(selectedText.toLowerCase()));
        }
    }
    document.getElementById('textEditor').focus();
}

// ==============================================
// BODY PART COUNTING RULES SYSTEM
// ==============================================

let bodyPartRules = [];
let unmatchedReports = [];
async function loadBodyPartRules() {
    try {
        console.log('[Body Part Rules] Loading rules from Firestore...');
        bodyPartRules = await getFromFirestore('body_part_rules');
        
        if (!bodyPartRules || bodyPartRules.length === 0) {
            console.warn('[Body Part Rules] No rules found in Firestore');
            bodyPartRules = [];
        }
        
        bodyPartRules.sort((a, b) => (a.priority || 999) - (b.priority || 999));
        console.log(`[Body Part Rules] Loaded ${bodyPartRules.length} rules`);
        
        // Only render if we're on the admin panel
        if (document.getElementById('rulesListContainer')) {
            renderBodyPartRules();
        }
    } catch (error) {
        console.error('[Body Part Rules] Error loading rules:', error);
        bodyPartRules = [];
    }
}
async function initializeBodyPartRulesSystem() {
    console.log('[Body Part Rules] Initializing system...');
    await loadBodyPartRules();
    await loadUnmatchedReports();
    console.log('[Body Part Rules] System initialized successfully');
}
function renderBodyPartRules() {
    const container = document.getElementById('rulesListContainer');
    if (!container) {
        console.warn('[Body Part Rules] Container not found, skipping render');
        return;
    }
    
    if (bodyPartRules.length === 0) {
        container.innerHTML = `
            <div style="padding: 40px; text-align: center; color: #666; background: #f8f9fa; border-radius: 8px;">
                No rules defined yet. Click "Add New Rule" to create one.
            </div>
        `;
        return;
    }
    
    console.log(`[Body Part Rules] Rendering ${bodyPartRules.length} rules`);
    
    // Clear container
    container.innerHTML = '';
    
    // Render each rule
    bodyPartRules.forEach((rule, index) => {
        const ruleDiv = document.createElement('div');
        ruleDiv.style.cssText = `
            background: #f8f9fa; 
            padding: 20px; 
            border-radius: 8px; 
            margin-bottom: 15px; 
            border-left: 4px solid ${rule.isActive ? '#27ae60' : '#95a5a6'};
        `;
        
        // Header
        const headerDiv = document.createElement('div');
        headerDiv.style.cssText = 'display: flex; justify-content: space-between; align-items: start; margin-bottom: 15px;';
        
        // Info
        const infoDiv = document.createElement('div');
        infoDiv.innerHTML = `
            <div style="font-weight: bold; font-size: 16px; color: #2c3e50; margin-bottom: 5px;">
                Rule #${index + 1}: ${rule.phrase}
            </div>
            <div style="font-size: 12px; color: #666;">
                Priority: ${rule.priority || 999} | Mode: ${rule.matchingMode || 'standard'} | 
                Status: ${rule.isActive ? '✅ Active' : '⏸️ Inactive'}
            </div>
        `;
        
        // Buttons
        const buttonsDiv = document.createElement('div');
        buttonsDiv.style.cssText = 'display: flex; gap: 5px;';
        
        // Edit button
        const editBtn = document.createElement('button');
        editBtn.textContent = '✏️ Edit';
        editBtn.className = 'btn';
        editBtn.style.cssText = 'background: #3498db; padding: 6px 12px; font-size: 12px; cursor: pointer;';
        editBtn.onclick = () => editRule(rule.id);
        
        // Toggle button
        const toggleBtn = document.createElement('button');
        toggleBtn.textContent = rule.isActive ? '⏸️ Disable' : '▶️ Enable';
        toggleBtn.className = 'btn';
        toggleBtn.style.cssText = `background: ${rule.isActive ? '#f39c12' : '#27ae60'}; padding: 6px 12px; font-size: 12px; cursor: pointer;`;
        toggleBtn.onclick = () => toggleRuleStatus(rule.id);
        
        // Delete button
        const deleteBtn = document.createElement('button');
        deleteBtn.textContent = '🗑️';
        deleteBtn.className = 'btn';
        deleteBtn.style.cssText = 'background: #e74c3c; padding: 6px 12px; font-size: 12px; cursor: pointer;';
        deleteBtn.onclick = () => deleteRule(rule.id);
        
        buttonsDiv.appendChild(editBtn);
        buttonsDiv.appendChild(toggleBtn);
        buttonsDiv.appendChild(deleteBtn);
        
        headerDiv.appendChild(infoDiv);
        headerDiv.appendChild(buttonsDiv);
        
        // Details
        const detailsDiv = document.createElement('div');
        detailsDiv.style.cssText = 'background: white; padding: 15px; border-radius: 6px;';
        detailsDiv.innerHTML = `
            <div style="font-size: 13px; margin-bottom: 10px;">
                <strong>Count as:</strong> ${rule.reportCount} report(s)
            </div>
            <div style="font-size: 13px;">
                <strong>Split into:</strong> 
                ${rule.splitInto.map(part => 
                    `<span style="background: #e3f2fd; padding: 4px 8px; border-radius: 4px; margin-right: 5px; display: inline-block; margin-bottom: 5px;">
                        ${part.displayName || part.name}
                    </span>`
                ).join('')}
            </div>
        `;
        
        ruleDiv.appendChild(headerDiv);
        ruleDiv.appendChild(detailsDiv);
        container.appendChild(ruleDiv);
    });
    
    console.log('[Body Part Rules] Render complete');
}
async function toggleRuleStatus(ruleId) {
    console.log('[Body Part Rules] Toggling rule:', ruleId);
    
    const rule = bodyPartRules.find(r => r.id === ruleId);
    if (!rule) {
        console.error('[Body Part Rules] Rule not found:', ruleId);
        return;
    }
    
    rule.isActive = !rule.isActive;
    
    try {
        await updateFirestoreDoc('body_part_rules', rule.id, {
            isActive: rule.isActive,
            lastModified: new Date().toISOString()
        });
        
        showNotification(rule.isActive ? '✓ Rule enabled' : '⏸️ Rule disabled');
        await loadBodyPartRules();
    } catch (error) {
        console.error('[Body Part Rules] Error toggling rule:', error);
        alert('Error updating rule. Please try again.');
    }
}
async function deleteRule(ruleId) {
    console.log('[Body Part Rules] Deleting rule:', ruleId);
    
    if (!confirm('Delete this rule? This action cannot be undone.')) {
        return;
    }
    
    try {
        const snapshot = await db.collection('body_part_rules').get();
        for (const doc of snapshot.docs) {
            if (doc.data().id === ruleId) {
                await doc.ref.delete();
                break;
            }
        }
        showNotification('✓ Rule deleted');
        await loadBodyPartRules();
    } catch (error) {
        console.error('[Body Part Rules] Error deleting rule:', error);
        alert('Error deleting rule. Please try again.');
    }
}
async function editRule(ruleId) {
    console.log('[Body Part Rules] Editing rule:', ruleId);
    
    const rule = bodyPartRules.find(r => r.id === ruleId);
    
    if (!rule) {
        console.error('[Body Part Rules] Rule not found:', ruleId);
        alert('Rule not found');
        return;
    }
    
    // Show edit modal (your existing modal code)
    showEditRuleModal(rule);
}
function showEditRuleModal(rule) {
    const modal = createModal(`
        <h2 style="color: #2c3e50; margin-bottom: 20px;">✏️ Edit Body Part Rule</h2>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Body Part Phrase:</label>
            <input type="text" id="editRulePhrase" value="${rule.phrase}" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; text-transform: uppercase;">
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Matching Mode:</label>
            <select id="editRuleMatchingMode" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="standard" ${rule.matchingMode === 'standard' ? 'selected' : ''}>Standard Mode</option>
                <option value="advanced" ${rule.matchingMode === 'advanced' ? 'selected' : ''}>Advanced Mode</option>
            </select>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Priority:</label>
            <input type="number" id="editRulePriority" value="${rule.priority || 10}" min="1" max="999" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Count as how many reports?</label>
            <input type="number" id="editRuleCount" value="${rule.reportCount}" min="1" max="10" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 10px; font-weight: 500;">Split into parts:</label>
            <div id="editSplitPartsContainer">
                ${rule.splitInto.map(part => `
                    <div class="split-part-row" style="display: flex; gap: 10px; margin-bottom: 10px;">
                        <input type="text" class="split-part-input" value="${part.displayName || part.name}" 
                               style="flex: 1; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
                        <button onclick="this.parentElement.remove();" class="btn" 
                                style="background: #e74c3c; padding: 8px 15px;">❌</button>
                    </div>
                `).join('')}
            </div>
            <button onclick="addEditSplitPartRow()" class="btn" style="background: #3498db; width: 100%; margin-top: 10px;">
                ➕ Add Another Part
            </button>
        </div>
        
        <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 30px;">
            <button onclick="saveEditedRule('${rule.id}')" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                💾 Save Changes
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 12px 30px;">
                Cancel
            </button>
        </div>
    `);
}
function addEditSplitPartRow() {
    const container = document.getElementById('editSplitPartsContainer');
    const newRow = document.createElement('div');
    newRow.className = 'split-part-row';
    newRow.style.cssText = 'display: flex; gap: 10px; margin-bottom: 10px;';
    newRow.innerHTML = `
        <input type="text" class="split-part-input" placeholder="Part name" 
               style="flex: 1; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
        <button onclick="this.parentElement.remove();" class="btn" 
                style="background: #e74c3c; padding: 8px 15px;">❌</button>
    `;
    container.appendChild(newRow);
}
async function saveEditedRule(ruleId) {
    const phrase = document.getElementById('editRulePhrase').value.trim().toUpperCase();
    const matchingMode = document.getElementById('editRuleMatchingMode').value;
    const priority = parseInt(document.getElementById('editRulePriority').value);
    const reportCount = parseInt(document.getElementById('editRuleCount').value);
    
    const splitInputs = document.querySelectorAll('#editSplitPartsContainer .split-part-input');
    const splitInto = Array.from(splitInputs)
        .map(input => input.value.trim().toUpperCase())
        .filter(val => val.length > 0)
        .map(name => ({ name, displayName: name }));
    
    if (!phrase) {
        alert('Please enter a body part phrase');
        return;
    }
    
    if (splitInto.length === 0) {
        alert('Please add at least one part');
        return;
    }
    
    const updatedRule = {
        phrase,
        phraseNormalized: normalizePhrase(phrase),
        matchingMode,
        priority,
        reportCount,
        splitInto,
        lastModified: new Date().toISOString(),
        modifiedBy: currentUser?.code || 'Unknown'
    };
    
    try {
        await updateFirestoreDoc('body_part_rules', ruleId, updatedRule);
        showNotification('✓ Rule updated successfully');
        closeModal();
        await loadBodyPartRules();
    } catch (error) {
        console.error('[Body Part Rules] Error updating rule:', error);
        alert('Error updating rule. Please try again.');
    }
}
function showAddRuleModal() {
    const modal = createModal(`
        <h2 style="color: #2c3e50; margin-bottom: 20px;">➕ Create New Body Part Rule</h2>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Body Part Phrase:</label>
            <input type="text" id="newRulePhrase" placeholder="e.g., CHEST ABDOMEN PELVIS" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; text-transform: uppercase;">
            <div style="font-size: 12px; color: #666; margin-top: 5px;">
                This phrase will be detected in report headings (case-insensitive)
            </div>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Matching Mode:</label>
            <select id="newRuleMatchingMode" style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
                <option value="standard">Standard Mode (Ignores separator types)</option>
                <option value="advanced">Advanced Mode (Separator-specific)</option>
            </select>
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Priority (lower = checked first):</label>
            <input type="number" id="newRulePriority" value="10" min="1" max="999" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Count as how many reports?</label>
            <input type="number" id="newRuleCount" value="1" min="1" max="10" 
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
        </div>
        
        <div style="margin-bottom: 20px;">
            <label style="display: block; margin-bottom: 10px; font-weight: 500;">Split into parts:</label>
            <div id="splitPartsContainer">
                <div class="split-part-row" style="display: flex; gap: 10px; margin-bottom: 10px;">
                    <input type="text" class="split-part-input" placeholder="Part name (e.g., CHEST)" 
                           style="flex: 1; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
                    <button onclick="this.parentElement.remove(); updatePartCount();" class="btn" 
                            style="background: #e74c3c; padding: 8px 15px;">❌</button>
                </div>
            </div>
            <button onclick="addSplitPartRow()" class="btn" style="background: #3498db; width: 100%; margin-top: 10px;">
                ➕ Add Another Part
            </button>
        </div>
        
        <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 30px;">
            <button onclick="saveNewRule()" class="btn" style="background: #27ae60; padding: 12px 30px; font-weight: bold;">
                💾 Save Rule
            </button>
            <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 12px 30px;">
                Cancel
            </button>
        </div>
    `);
}
function addSplitPartRow() {
    const container = document.getElementById('splitPartsContainer');
    if (!container) return;
    
    const newRow = document.createElement('div');
    newRow.className = 'split-part-row';
    newRow.style.cssText = 'display: flex; gap: 10px; margin-bottom: 10px;';
    newRow.innerHTML = `
        <input type="text" class="split-part-input" placeholder="Part name" 
               style="flex: 1; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
        <button onclick="this.parentElement.remove(); updatePartCount();" class="btn" 
                style="background: #e74c3c; padding: 8px 15px;">❌</button>
    `;
    container.appendChild(newRow);
}
function updatePartCount() {
    const container = document.getElementById('splitPartsContainer');
    if (!container) return;
    
    const count = container.querySelectorAll('.split-part-input').length;
    const countInput = document.getElementById('newRuleCount');
    if (countInput) {
        countInput.value = count;
    }
}
function updateEditPartCount() {
    const container = document.getElementById('editSplitPartsContainer');
    if (!container) return;
    
    const count = container.querySelectorAll('.split-part-input').length;
    const countInput = document.getElementById('editRuleCount');
    if (countInput) {
        countInput.value = count;
    }
}
async function saveNewRule() {
    const phrase = document.getElementById('newRulePhrase')?.value.trim().toUpperCase();
    const matchingMode = document.getElementById('newRuleMatchingMode')?.value;
    const priority = parseInt(document.getElementById('newRulePriority')?.value || 10);
    const reportCount = parseInt(document.getElementById('newRuleCount')?.value || 1);
    
    if (!phrase) {
        alert('Please enter a body part phrase');
        return;
    }
    
    const splitInputs = document.querySelectorAll('#splitPartsContainer .split-part-input');
    const splitInto = Array.from(splitInputs)
        .map(input => input.value.trim().toUpperCase())
        .filter(val => val.length > 0)
        .map(name => ({ name, displayName: name }));
    
    if (splitInto.length === 0) {
        alert('Please add at least one part');
        return;
    }
    
    if (splitInto.length !== reportCount) {
        if (!confirm(`Report count (${reportCount}) doesn't match number of parts (${splitInto.length}). Continue anyway?`)) {
            return;
        }
    }
    
    const newRule = {
        id: `rule_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`,
        phrase,
        phraseNormalized: normalizePhrase(phrase),
        matchingMode,
        priority,
        reportCount,
        splitInto,
        isActive: true,
        createdBy: currentUser?.code || 'Unknown',
        createdAt: new Date().toISOString()
    };
    
    try {
        await saveToFirestore('body_part_rules', newRule);
        showNotification('✓ Rule created successfully');
        closeModal();
        await loadBodyPartRules();
    } catch (error) {
        console.error('[Body Part Rules] Error saving rule:', error);
        alert('Error saving rule. Please try again.');
    }
}

function normalizePhrase(phrase) {
    return phrase
        .toUpperCase()
        .replace(/&/g, ' ')           // Replace ampersand with space
        .replace(/\bAND\b/g, ' ')     // Remove the word AND
        .replace(/,/g, ' ')           // Remove commas
        .replace(/\s+/g, ' ')         // Collapse multiple spaces
        .trim();
}


// ==============================================
// APPLY RULES TO REPORTS
// ==============================================
function parseReportHeading(reportText) {
    if (!reportText) return null;
    
    const lines = reportText.split('\n');
    const firstLine = lines[0].trim().toUpperCase();
    
    // Extract body part phrase
    const patterns = [
        /(?:CT|MRI|US|ULTRASOUND|XR|X-RAY|XRAY)\s+(?:SCAN\s+)?OF\s+THE\s+(.+)/i,
        /(?:CT|MRI|US|ULTRASOUND|XR|X-RAY|XRAY)\s+(?:SCAN\s+)?OF\s+(.+)/i,
        /(?:CT|MRI|US|ULTRASOUND|XR|X-RAY|XRAY)\s+(.+)/i
    ];
    
    for (const pattern of patterns) {
        const match = firstLine.match(pattern);
        if (match) {
            let phrase = match[1].trim();
            
            // Remove trailing period if exists
            phrase = phrase.replace(/\.$/, '');
            
            // AUTO-DETECT BILATERAL
            const bilateralMatch = phrase.match(/BILATERAL\s+(.+)/i);
            if (bilateralMatch) {
                const bodyPart = bilateralMatch[1].trim();
                return {
                    original: phrase,
                    normalized: normalizePhrase(phrase),
                    isBilateral: true,
                    autoCount: 2,
                    autoParts: [`LEFT ${bodyPart}`, `RIGHT ${bodyPart}`]
                };
            }
            
            // AUTO-DETECT "LEFT AND RIGHT"
            const leftRightMatch = phrase.match(/LEFT\s+AND\s+RIGHT\s+(.+)/i);
            if (leftRightMatch) {
                const bodyPart = leftRightMatch[1].trim();
                return {
                    original: phrase,
                    normalized: normalizePhrase(phrase),
                    isLeftRight: true,
                    autoCount: 2,
                    autoParts: [`LEFT ${bodyPart}`, `RIGHT ${bodyPart}`]
                };
            }
            
            // ✅ FIXED: "X, Y AND Z" detection (comma-separated with AND)
            // Example: "CHEST, ABDOMEN AND PELVIS" → 3 parts
            if (phrase.includes(',') && phrase.includes(' AND ')) {
                // Split by comma first, then handle "AND" in last part
                const commaParts = phrase.split(',').map(p => p.trim());
                const lastPart = commaParts[commaParts.length - 1];
                
                if (lastPart.includes(' AND ')) {
                    // Split the last part by "AND"
                    const andParts = lastPart.split(' AND ').map(p => p.trim());
                    
                    // Combine: all comma parts except last + split last part
                    const allParts = [
                        ...commaParts.slice(0, -1),
                        ...andParts
                    ];
                    
                    return {
                        original: phrase,
                        normalized: normalizePhrase(phrase),
                        hasMultipleParts: true,
                        autoCount: allParts.length,
                        autoParts: allParts
                    };
                }
            }
            
            // AUTO-DETECT "X AND Y" (simple AND without comma)
            const simpleAndMatch = phrase.match(/^([A-Z\s]+)\s+AND\s+([A-Z\s]+)$/i);
            if (simpleAndMatch) {
                return {
                    original: phrase,
                    normalized: normalizePhrase(phrase),
                    hasMultipleParts: true,
                    autoCount: 2,
                    autoParts: [simpleAndMatch[1].trim(), simpleAndMatch[2].trim()]
                };
            }
            
            // Default: single body part
            return {
                original: phrase,
                normalized: normalizePhrase(phrase),
                autoCount: 1,
                autoParts: [phrase]
            };
        }
    }
    
    return null;
}

function findMatchingRule(bodyPartData) {
    if (!bodyPartData) return null;
    
    // PRIORITY 1: Admin-created rules (always override auto-detection)
    for (const rule of bodyPartRules) {
        if (!rule.isActive) continue;
        
        if (rule.matchingMode === 'standard') {
            // Standard mode: normalized matching
            if (rule.phraseNormalized === bodyPartData.normalized) {
                return rule;
            }
        } else {
            // Advanced mode: exact matching
            if (rule.phrase === bodyPartData.original) {
                return rule;
            }
        }
    }
    
    // PRIORITY 2: Auto-detected patterns (only if no admin rule)
    if (bodyPartData.autoCount > 1) {
        return {
            id: 'AUTO_DETECTED',
            phrase: bodyPartData.original,
            reportCount: bodyPartData.autoCount,
            splitInto: bodyPartData.autoParts.map(p => ({ name: p, displayName: p })),
            isAutoDetected: true,
            isActive: true
        };
    }
    
    // No rule found - will count as 1
    return null;
}
async function flagUnmatchedReport(report) {
    const unmatchedData = {
        id: `unmatched_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`,
        reportId: report.id,
        reportText: report.reportText,
        modality: report.modality,
        empCode: report.empCode,
        submittedDate: report.submittedDate,
        submittedTime: report.submittedTime,
        detectedPhrase: parseReportHeading(report.reportText),
        flaggedAt: new Date().toISOString(),
        status: 'pending'
    };
    
    try {
        await saveToFirestore('unmatched_reports', unmatchedData);
    } catch (error) {
        console.error('[Unmatched Reports] Error flagging:', error);
    }
}

// ==============================================
// TIME FILTER ENHANCEMENT
// ==============================================

function applyReportsFilters() {
    const fromDate = document.getElementById('reportsFilterFrom').value;
    const toDate = document.getElementById('reportsFilterTo').value;
    const fromTime = document.getElementById('reportsFilterFromTime')?.value || '00:00';
    const toTime = document.getElementById('reportsFilterToTime')?.value || '23:59';
    const radFilter = document.getElementById('reportsFilterRad').value;
    const modalityFilter = document.getElementById('reportsFilterModality').value;
    const searchText = document.getElementById('reportsSearchText').value.toLowerCase().trim();
    console.log('fromDate:', fromDate);
    console.log('toDate:', toDate);
    console.log('fromTime:', fromTime);
    console.log('toTime:', toTime);
    console.log('Sample report submittedDate:', allReportsData[0]?.submittedDate);
  filteredReportsData = allReportsData.filter(report => {
    // Date filter
    if (fromDate && report.submittedDate < fromDate) return false;
    if (toDate && report.submittedDate > toDate) return false;
    
    // Time filter - convert 12-hour format to 24-hour format
    if (fromDate && report.submittedDate === fromDate) {
        const reportTime24hr = convertTo24Hour(report.submittedTime || '12:00:00 AM');
        if (reportTime24hr < fromTime) return false;
    }
    
    if (toDate && report.submittedDate === toDate) {
        const reportTime24hr = convertTo24Hour(report.submittedTime || '11:59:59 PM');
        if (reportTime24hr > toTime) return false;
    }
    
    // Radiologist filter
    if (radFilter && report.empCode !== radFilter) return false;
    
   // Modality filter
	if (modalityFilter && report.modality !== modalityFilter) return false;

	// Institution filter
	const institutionFilter = document.getElementById('filterInstitution')?.value || '';
	const accession = document.getElementById('filterAccession')?.value.toLowerCase().trim() || '';

	if (institutionFilter && report.institution !== institutionFilter) return false;
	if (accession && (!report.accessionNumber || !report.accessionNumber.toLowerCase().includes(accession))) return false;
	

	// Search text filter
	if (searchText && !report.reportText.toLowerCase().includes(searchText)) return false;

	return true;
   }); 
    // Update statistics
    updateReportsStatistics(filteredReportsData);
    
    // Render table
    renderReportsTable(filteredReportsData);
}

function convertTo24Hour(time12hr) {
    const [time, period] = time12hr.split(' ');
    let [hours, minutes, seconds] = time.split(':');
    
    hours = parseInt(hours);
    
    if (period === 'PM' && hours !== 12) {
        hours += 12;
    } else if (period === 'AM' && hours === 12) {
        hours = 0;
    }
    
    return `${hours.toString().padStart(2, '0')}:${minutes}`;
}
// ==============================================
// UNMATCHED REPORTS QUEUE
// ==============================================

async function loadUnmatchedReports() {
    try {
        const allUnmatched = await getFromFirestore('unmatched_reports');
        unmatchedReports = allUnmatched.filter(r => r.status === 'pending');
        unmatchedReports.sort((a, b) => new Date(b.flaggedAt) - new Date(a.flaggedAt));
        
        // Only render if we're on the admin panel
        if (document.getElementById('unmatchedReportsContainer')) {
            renderUnmatchedReports();
        }
    } catch (error) {
        console.error('[Unmatched Reports] Error loading:', error);
    }
}
function renderUnmatchedReports() {
    const container = document.getElementById('unmatchedReportsContainer');
    if (!container) return;
    
    if (unmatchedReports.length === 0) {
        container.innerHTML = `
            <div style="padding: 40px; text-align: center; color: #666; background: #f8f9fa; border-radius: 8px;">
                ✅ No unmatched reports! All reports have matching rules.
            </div>
        `;
        return;
    }
    
    const html = unmatchedReports.slice(0, 10).map(report => {
        const employee = authorizedEmployees[report.empCode];
        const empName = employee ? employee.name : report.empCode;
        const detectedPhrase = report.detectedPhrase?.original || 'None';
        
        return `
            <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin-bottom: 10px; border-left: 4px solid #f39c12;">
                <div style="display: flex; justify-content: space-between; align-items: start;">
                    <div style="flex: 1;">
                        <div style="font-weight: bold; color: #2c3e50; margin-bottom: 5px;">
                            ${report.modality} - ${empName}
                        </div>
                        <div style="font-size: 12px; color: #666; margin-bottom: 8px;">
                            ${report.submittedDate} ${report.submittedTime || ''} | Detected: "${detectedPhrase}"
                        </div>
                        <div style="font-size: 12px; background: white; padding: 10px; border-radius: 4px; max-height: 60px; overflow: hidden;">
                            ${report.reportText ? report.reportText.substring(0, 200) : 'No content'}...
                        </div>
                    </div>
                    <div style="display: flex; flex-direction: column; gap: 5px; margin-left: 15px;">
                        <button onclick="createRuleFromUnmatched('${report.id}')" class="btn" 
                                style="background: #27ae60; padding: 6px 12px; font-size: 11px; white-space: nowrap;">
                            ➕ Create Rule
                        </button>
                        <button onclick="dismissUnmatched('${report.id}')" class="btn" 
                                style="background: #95a5a6; padding: 6px 12px; font-size: 11px;">
                            ✓ Dismiss
                        </button>
                    </div>
                </div>
            </div>
        `;
    }).join('');
    
    container.innerHTML = html + (unmatchedReports.length > 10 ? `
        <div style="text-align: center; padding: 15px; color: #666;">
            Showing 10 of ${unmatchedReports.length} unmatched reports
        </div>
    ` : '');
}
function createRuleFromUnmatched(unmatchedId) {
    const report = unmatchedReports.find(r => r.id === unmatchedId);
    if (!report) {
        alert('Report not found');
        return;
    }
    
    showAddRuleModal();
    
    // Pre-fill the form after modal renders
    setTimeout(() => {
        const phraseInput = document.getElementById('newRulePhrase');
        if (phraseInput && report.detectedPhrase) {
            phraseInput.value = report.detectedPhrase.original || report.detectedPhrase;
        }
    }, 100);
}
async function dismissUnmatched(unmatchedId) {
    if (!confirm('Mark this report as resolved?')) {
        return;
    }
    
    try {
        const snapshot = await db.collection('unmatched_reports').get();
        for (const doc of snapshot.docs) {
            if (doc.data().id === unmatchedId) {
                await doc.ref.update({ status: 'dismissed' });
                break;
            }
        }
        showNotification('✓ Report dismissed');
        await loadUnmatchedReports();
    } catch (error) {
        console.error('[Unmatched Reports] Error dismissing:', error);
        alert('Error dismissing report. Please try again.');
    }
}

// ==============================================
// PWA - SERVICE WORKER & UPDATE MANAGEMENT
// ==============================================

let deferredPrompt = null;
let updateAvailable = false;
let newServiceWorker = null;
let registration = null;

// Register Service Worker
if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
        registerServiceWorker();
        checkForUpdates();
    });
}

async function registerServiceWorker() {
    try {
        registration = await navigator.serviceWorker.register('./service-worker.js', {
            scope: './',
            updateViaCache: 'none'
        });
        
        console.log('[PWA] Service Worker registered successfully');
        
        // Listen for updates
        registration.addEventListener('updatefound', () => {
            newServiceWorker = registration.installing;
            console.log('[PWA] New service worker found, installing...');
            
            newServiceWorker.addEventListener('statechange', () => {
                console.log('[PWA] Service worker state:', newServiceWorker.state);
                if (newServiceWorker.state === 'installed' && navigator.serviceWorker.controller) {
                    updateAvailable = true;
                    console.log('[PWA] Update available!');
                    showUpdatePrompt();
                }
            });
        });
        
        // Check for updates every 60 seconds (more aggressive)
        setInterval(() => {
            console.log('[PWA] Checking for updates...');
            registration.update();
        }, 60 * 1000); // Changed from 5 minutes to 1 minute
        
        // CRITICAL: Also check when page becomes visible
        document.addEventListener('visibilitychange', () => {
            if (document.visibilityState === 'visible') {
                console.log('[PWA] Page visible, checking for updates...');
                registration.update();
            }
        });
        
    } catch (error) {
        console.error('[PWA] Service Worker registration failed:', error);
    }
}

async function checkForUpdates() {
    try {
        // Wait for registration to be ready
        const reg = await navigator.serviceWorker.ready;
        console.log('[PWA] Checking for updates...');
        await reg.update();
    } catch (error) {
        console.error('[PWA] Update check failed:', error);
    }
}

function showUpdatePrompt() {

	const existing = document.getElementById('pwaUpdateBanner');
    if (existing) existing.remove();
	
    const updateBanner = document.createElement('div');
    updateBanner.id = 'pwaUpdateBanner';
    updateBanner.style.cssText = `
        position: fixed;
        top: 20px;
        left: 50%;
        transform: translateX(-50%);
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
        padding: 20px 30px;
        border-radius: 12px;
        box-shadow: 0 10px 40px rgba(0,0,0,0.3);
        z-index: 10005;
        display: flex;
        align-items: center;
        gap: 20px;
        animation: slideDown 0.5s ease;
        max-width: 500px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    `;
    
    updateBanner.innerHTML = `
        <div style="flex: 1;">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 5px;">🎉 New Version Available!</div>
            <div style="font-size: 14px; opacity: 0.9;">Update now to get the latest features and improvements.</div>
        </div>
        <div style="display: flex; gap: 10px;">
            <button id="updateNowBtn" style="background: #27ae60; color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 14px;">
                Update Now
            </button>
            <button id="updateLaterBtn" style="background: rgba(255,255,255,0.2); color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-size: 14px;">
                Later
            </button>
        </div>
    `;
    
    document.body.appendChild(updateBanner);
    
    document.getElementById('updateNowBtn').addEventListener('click', () => {
		updateBanner.remove();
        applyUpdate();
    });
    
    document.getElementById('updateLaterBtn').addEventListener('click', () => {
        updateBanner.remove();
        setTimeout(() => {
            if (updateAvailable) {
               userChooseUpdate();
            }
        }, 60 * 60 * 1000);
    });
}

function applyUpdate() {
    if (newServiceWorker) {
        const loadingDiv = document.createElement('div');
        loadingDiv.style.cssText = `
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px 50px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.4);
            z-index: 10006;
            text-align: center;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        `;
        loadingDiv.innerHTML = `
            <div style="font-size: 20px; font-weight: bold; margin-bottom: 15px;">Updating...</div>
            <div style="font-size: 14px;">Please wait while we apply the update</div>
            <div style="margin-top: 20px;">
                <div style="border: 4px solid rgba(255,255,255,0.3); border-top: 4px solid white; border-radius: 50%; width: 40px; height: 40px; animation: spin 1s linear infinite; margin: 0 auto;"></div>
            </div>
        `;
        document.body.appendChild(loadingDiv);
        
        console.log('[PWA] Applying update...');
        
        // Standard approach: Post message then wait for controller change
        newServiceWorker.postMessage({ type: 'SKIP_WAITING' });
        
        // Set up controller change listener BEFORE posting message
        let controllerChanged = false;
        
        navigator.serviceWorker.addEventListener('controllerchange', () => {
            if (!controllerChanged) {
                controllerChanged = true;
                console.log('[PWA] Controller changed, reloading page');
                window.location.reload();
            }
        }, { once: true });
        
        // Safety timeout (international standard: 2 seconds)
        setTimeout(() => {
            if (!controllerChanged) {
                console.log('[PWA] Timeout reached, forcing reload');
                window.location.reload();
            }
        }, 2000);
    }
}

window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
    console.log('[PWA] Install prompt ready');
    
    showInstallButton(); // ← DELETE the if(currentUser) check
});

function showInstallButton() {
	const headerButtons = document.querySelector('.header > div:last-child');
    if (!headerButtons || document.getElementById('pwaInstallBtn')) return; 
    const installBtn = document.createElement('button');
    installBtn.id = 'pwaInstallBtn';
    installBtn.className = 'btn';
    installBtn.style.cssText = 'background: #9b59b6; margin-right: 10px; display: inline-block;';
    installBtn.textContent = '📱 Install App';
    installBtn.onclick = installPWA;
    
    headerButtons.insertBefore(installBtn, headerButtons.firstChild);
}

async function installPWA() {
    if (!deferredPrompt) {
        showNotification('App is already installed or installation not supported');
        return;
    }
    
    deferredPrompt.prompt();
    
    const { outcome } = await deferredPrompt.userChoice;
    
    if (outcome === 'accepted') {
        console.log('[PWA] User accepted installation');
        showNotification('✅ App installed successfully!');
        
        const installBtn = document.getElementById('pwaInstallBtn');
        if (installBtn) installBtn.remove();
    }
    
    deferredPrompt = null;
}

function isRunningAsPWA() {
    return window.matchMedia('(display-mode: standalone)').matches || 
           window.navigator.standalone === true;
}

if (isRunningAsPWA()) {
    window.addEventListener('load', () => {
        const statusBar = document.querySelector('.sync-status');
        if (statusBar) {
            statusBar.innerHTML = '📱 PWA | ' + statusBar.innerHTML;
        }
    });
}

function userChooseUpdate() {
    const modal = createModal(`
        <div style="text-align: center;">
            <h2 style="color: #27ae60; margin-bottom: 20px;">✨ Update Available</h2>
            <p style="font-size: 16px; margin-bottom: 30px;">A new version is ready.</p>
            <div style="display: flex; gap: 15px; justify-content: center;">
                <button onclick="applyUpdate()" class="btn" style="background: #27ae60; padding: 12px 30px;">
                    Update Now
                </button>
                <button onclick="closeModal()" class="btn" style="background: #95a5a6; padding: 12px 30px;">
                    Later
                </button>
            </div>
        </div>
    `);
}

window.addEventListener('online', () => {
    const syncStatus = document.getElementById('syncStatus');
    if (syncStatus) {
        syncStatus.style.background = '#27ae60';
        syncStatus.textContent = '🟢 Online';
    }
    showNotification('✅ Connection restored');
});

window.addEventListener('offline', () => {
    const syncStatus = document.getElementById('syncStatus');
    if (syncStatus) {
        syncStatus.style.background = '#e74c3c';
        syncStatus.textContent = '🔴 Offline';
    }
    showNotification('⚠️ Working offline - changes will sync when connection restored');
});

const pwaStyles = document.createElement('style');
pwaStyles.textContent = `
    @keyframes slideDown {
        from { transform: translate(-50%, -100%); opacity: 0; }
        to { transform: translate(-50%, 0); opacity: 1; }
    }
    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }
`;
document.head.appendChild(pwaStyles);

console.log('[PWA] Initialization complete');

// ==============================================
// TIME TRACKING & SESSION MANAGEMENT
// ==============================================

let currentSessionId = null;
let sessionStartTime = null;
let lastActivityTime = null;
let inactivityCheckInterval = null;
let isTrackingInactivity = false;
let inactivityLogId = null;

// Start tracking session on login
async function startSessionTracking() {
    if (!currentUser || !currentUser.code) {
        console.error('[Session] ❌ Cannot start tracking - no user');
        return;
    }
    
    currentSessionId = `SESSION_${Date.now()}_${currentUser.code}`;
    sessionStartTime = new Date().toISOString();
    lastActivityTime = Date.now();
    isTrackingInactivity = false;
    
    console.log('[Session] Starting tracking for:', currentUser.code);
    
    try {
        // Log login event
        const logId = await logTimeEvent('login', {
            sessionId: currentSessionId
        });
        
        console.log('[Session] ✅ Login logged successfully:', logId);
        
    } catch (error) {
        console.error('[Session] ❌ Failed to log login:', error);
    }
    
    // Start inactivity monitoring
    inactivityCheckInterval = setInterval(checkInactivityForLogging, 30000);
    
    console.log('[Session] Tracking started:', currentSessionId);
}
async function logTimeEvent(eventType, metadata = {}) {
    try {
        const eventData = {
            empCode: currentUser.code,
            empName: currentUser.name,
            eventType: eventType, // 'login', 'logout', 'inactivity_start', 'inactivity_end'
            timestamp: new Date().toISOString(),
            sessionId: currentSessionId,
            ...metadata
        };
        
        console.log('[Time Log] Logging event:', eventType, 'for', currentUser.code);
        
        const docId = await saveToFirestore('time_logs', eventData);
        
        console.log('[Time Log] ✅ Event logged successfully:', docId);
        
        return docId;
    } catch (error) {
        console.error('[Time Log] ❌ Error logging event:', error);
        throw error;
    }
}
// Check if user is inactive (for logging purposes only)
async function checkInactivityForLogging() {
    if (!currentUser || !sessionStartTime) return;
    
    const now = Date.now();
    const timeSinceActivity = now - lastActivity;
    
    // 10 minutes = start logging inactivity
    if (timeSinceActivity >= INACTIVITY_DETECTION && !isTrackingInactivity) {
        isTrackingInactivity = true;
        inactivityStartTime = now; // ✅ FIX: Use current time, not lastActivity
        
        // Log inactivity start
        inactivityLogId = await logTimeEvent('inactivity_start', {
            inactivityStartTime: new Date(inactivityStartTime).toISOString()
        });
        
        console.log('[Time Log] Inactivity detected after 10 minutes');
    }
    
    // If user becomes active again (activity within last 30 seconds)
    if (timeSinceActivity < 30000 && isTrackingInactivity) {
        // User is active again
        await logInactivityEnd();
    }
}

// Log inactivity end when user returns
async function logInactivityEnd() {
    if (inactivityStartTime && inactivityLogId && isTrackingInactivity) {
        const inactivityEndTime = Date.now();
        const durationSeconds = Math.floor((inactivityEndTime - inactivityStartTime) / 1000);
        
        await logTimeEvent('inactivity_end', {
            inactivityEndTime: new Date(inactivityEndTime).toISOString(),
            durationSeconds: durationSeconds,
            relatedStartLogId: inactivityLogId
        });
        
        console.log(`[Time Log] Inactivity ended. Duration: ${Math.floor(durationSeconds / 60)} minutes`);
        
        inactivityStartTime = null;
        inactivityLogId = null;
        isTrackingInactivity = false;
    }
}
// End session tracking on logout
async function endSessionTracking(logoutType = 'manual') {
    if (!currentSessionId) return;
    
    // If there's an ongoing inactivity period, close it
    if (isTrackingInactivity && inactivityStartTime) {
        await logInactivityEnd();
    }
    
    // Log logout event
    await logTimeEvent('logout', {
        sessionId: currentSessionId,
        logoutType: logoutType
    });
    
    // Stop inactivity monitoring
    if (inactivityCheckInterval) {
        clearInterval(inactivityCheckInterval);
        inactivityCheckInterval = null;
    }
    
    console.log('[Session] Ended:', currentSessionId);
    
    // Reset session variables
    currentSessionId = null;
    sessionStartTime = null;
    lastActivityTime = null;
    isTrackingInactivity = false;
    inactivityStartTime = null;
    inactivityLogId = null;
}
// Load HR Time Logs Panel
async function loadHRTimeLogs() {
    // Check permission FIRST
    if (!currentUser.permissions || !currentUser.permissions.includes('emp_session')) {
        const tbody = document.getElementById('timeLogsTableBody');
        if (tbody) {
            tbody.innerHTML = `
                <tr><td colspan="9" style="text-align: center; padding: 30px; color: #e74c3c;">
                    ⛔ Access Denied: You need "emp_session" permission to view time logs.
                </td></tr>
            `;
        }
        return;
    }
    
    // Populate employee filters
    const empFilter = document.getElementById('timeLogEmpFilter');
    if (!empFilter) return;
    
    const employeeOptions = '<option value="">All Employees</option>' + 
        Object.entries(authorizedEmployees)
            .sort((a, b) => a[1].name.localeCompare(b[1].name))
            .map(([code, emp]) => `<option value="${code}">${emp.name} (${code}) - ${emp.role}</option>`)
            .join('');
    
    empFilter.innerHTML = employeeOptions;
    
    // Set default date range (last 7 days)
    const today = new Date();
    const lastWeek = new Date(today);
    lastWeek.setDate(lastWeek.getDate() - 7);
    
    const toDateInput = document.getElementById('timeLogToDate');
    const fromDateInput = document.getElementById('timeLogFromDate');
    
    if (toDateInput) toDateInput.valueAsDate = today;
    if (fromDateInput) fromDateInput.valueAsDate = lastWeek;

    // Load data
    await filterTimeLogs();
}

// Filter and display time logs
async function filterTimeLogs() {
	
    const empCode = document.getElementById('timeLogEmpFilter')?.value || '';
    const fromDate = document.getElementById('timeLogFromDate')?.value || '';
    const toDate = document.getElementById('timeLogToDate')?.value || '';
    
    const tbody = document.getElementById('timeLogsTableBody');
    if (!tbody) {
        console.error('[Time Logs] Table body element not found');
        return;
    }
    
    if (!fromDate || !toDate) {
        showNotification('⚠️ Please select both From and To dates');
        return;
    }
    
    tbody.innerHTML = '<tr><td colspan="12" style="text-align: center; padding: 20px;">Loading...</td></tr>';
    
    try {
        // Fetch all time logs
        const allLogs = await getFromFirestore('time_logs');
       
        // Filter by date range and employee
				const filteredLogs = allLogs.filter(log => {
			if (!log.timestamp) return false;

			const logDate = new Date(log.timestamp).toISOString().split('T')[0];
			const matchesDate = logDate >= fromDate && logDate <= toDate;
			const matchesEmp = !empCode || log.empCode === empCode;
			const matchesInstitution = true;

			return matchesDate && matchesEmp;
		});

        
        // Calculate daily summaries
        const dailySummaries = await calculateDailySummaries(filteredLogs);
console.log('Daily Summaries:', dailySummaries, 'Is Array?', Array.isArray(dailySummaries));
// Safety check: ensure it's an array
if (!Array.isArray(dailySummaries)) {
    console.error('[Time Logs] calculateDailySummaries did not return an array:', dailySummaries);
    tbody.innerHTML = '<tr><td colspan="12" style="text-align: center; padding: 20px; color: #e74c3c;">Error: Invalid data format</td></tr>';
    return;
}
        
        // Store for pagination
        allFilteredSummaries = dailySummaries;
        currentPage = 1;
        
        // Display table
        displayTimeLogsTableExpandable(dailySummaries, filteredLogs);
        
    } catch (error) {
        console.error('[Time Logs] Error loading:', error);
        tbody.innerHTML = '<tr><td colspan="12" style="text-align: center; padding: 20px; color: #e74c3c;">Error loading time logs</td></tr>';
    }
}
    
async function calculateDailySummaries(logs) {
    const summaries = {};
    
    // Group logs by employee and date
    logs.forEach(log => {
        const date = new Date(log.timestamp).toISOString().split('T')[0];
if (log.empCode === 'RSSE1004') {
    console.log('[Time Logs] Original timestamp:', log.timestamp, '→ Extracted date:', date);
}
        const key = `${log.empCode}_${date}`;
        
        if (!summaries[key]) {
            summaries[key] = {
                empCode: log.empCode,
                empName: log.empName,
                date: date,
                logins: [],
                logouts: [],
                inactivityPeriods: [],
                inactivityStarts: {}
            };
        }
        
        const summary = summaries[key];
        
        if (log.eventType === 'login') {
            summary.logins.push(new Date(log.timestamp));
        } else if (log.eventType === 'logout') {
            summary.logouts.push({
                time: new Date(log.timestamp),
                type: log.logoutType || 'manual'
            });
        } else if (log.eventType === 'inactivity_start') {
            summary.inactivityStarts[log.id] = new Date(log.timestamp);
        } else if (log.eventType === 'inactivity_end') {
            const startTime = summary.inactivityStarts[log.relatedStartLogId];
            if (startTime) {
                summary.inactivityPeriods.push({
                    start: startTime,
                    end: new Date(log.timestamp),
                    duration: log.durationSeconds || 0
                });
            }
        }
    });
    
    // Fetch schedules and reports
    const allSchedules = await getFromFirestore('schedules');
    const allReports = await getFromFirestore('daily_reports');
    
    const results = [];
    
    for (const summary of Object.values(summaries)) {
        if (summary.logins.length === 0) continue;
        
        const firstLogin = new Date(Math.min(...summary.logins));
        const lastLogout = summary.logouts.length > 0 
            ? new Date(Math.max(...summary.logouts.map(l => l.time)))
            : null;
        
        // Calculate total logged time
        let totalLoggedSeconds = 0;
        if (lastLogout) {
            totalLoggedSeconds = Math.floor((lastLogout - firstLogin) / 1000);
        } else {
            totalLoggedSeconds = Math.floor((new Date() - firstLogin) / 1000);
        }
        
        // Calculate total inactivity
        const totalInactiveSeconds = summary.inactivityPeriods.reduce(
            (sum, period) => sum + period.duration, 0
        );
        
        // Calculate active work time
        const activeWorkSeconds = totalLoggedSeconds - totalInactiveSeconds;
        
        // Get employee schedules for this date
        const daySchedules = allSchedules.filter(s => 
    s.empCode === summary.empCode && 
    s.date === summary.date && 
    s.start && 
    s.end &&
    !s.leaveType
);

if (summary.empCode === 'RSSE1004' && summary.date === '2025-12-27') {
    console.log('[Time Logs] Looking for schedules:', {
        empCode: summary.empCode,
        date: summary.date,
        allSchedulesForEmp: allSchedules.filter(s => s.empCode === summary.empCode && (s.date === '2025-12-27' || s.date === '2025-12-26'))
    });
}
        if (daySchedules.length > 0) {
    console.log(`[Time Logs] ${summary.empCode} on ${summary.date}: Found ${daySchedules.length} shift(s)`, daySchedules);

}
        // Calculate scheduled hours by type
        let regularScheduledSeconds = 0;
        let extraScheduledSeconds = 0;
        
        daySchedules.forEach(shift => {
            const duration = parseFloat(shift.duration) || 0;
            const seconds = duration * 3600;
            
            if (shift.shiftType === 'extra') {
                extraScheduledSeconds += seconds;
            } else {
                regularScheduledSeconds += seconds;
            }
        });
        console.log(`[Time Logs] ${summary.empCode} on ${summary.date} - Scheduled Regular: ${regularScheduledSeconds}s (${(regularScheduledSeconds/3600).toFixed(1)}h), Extra: ${extraScheduledSeconds}s (${(extraScheduledSeconds/3600).toFixed(1)}h)`);

        // Count cases by shift type
        let casesInRegular = 0;
        let casesInExtra = 0;
		let modalityBreakdownRegular = {}; // { "CT": 5, "US": 3 }
		let modalityBreakdownExtra = {};
        
        const dayCases = allReports.filter(r => 
            r.empCode === summary.empCode && 
            r.submittedDate === summary.date &&
            r.submittedTime
        );
        
        dayCases.forEach(caseReport => {
            const time24h = convertTo24Hour(caseReport.submittedTime);
            if (!time24h) return;
            
            const [submittedHour, submittedMinute] = time24h.split(':').map(Number);
            const submittedTotalMinutes = submittedHour * 60 + submittedMinute;
            
            let matchedShiftType = null;
            
            // Check against all schedules for this day
            for (const shift of daySchedules) {
                const [startHour, startMin] = shift.start.split(':').map(Number);
                const [endHour, endMin] = shift.end.split(':').map(Number);
                
                let shiftStartMinutes = startHour * 60 + startMin;
                let shiftEndMinutes = endHour * 60 + endMin;
                
                // Check if submitted time falls in this shift
                if (submittedTotalMinutes >= shiftStartMinutes && submittedTotalMinutes < shiftEndMinutes) {
                    matchedShiftType = shift.shiftType || 'regular';
                    break;
                }
            }
            
            // Count case based on matched shift type
            // Count case based on matched shift type
				const modality = caseReport.modality || 'Unknown';

				if (matchedShiftType === 'extra') {
					casesInExtra++;
					modalityBreakdownExtra[modality] = (modalityBreakdownExtra[modality] || 0) + 1;
				} else {
					// If matched as regular OR no schedule found (fallback to regular)
					casesInRegular++;
					modalityBreakdownRegular[modality] = (modalityBreakdownRegular[modality] || 0) + 1;
				}
        });
        
        results.push({
            empCode: summary.empCode,
            empName: summary.empName,
            date: summary.date,
            firstLogin: firstLogin,
            lastLogout: lastLogout,
            totalLoggedSeconds: totalLoggedSeconds,
            totalInactiveSeconds: totalInactiveSeconds,
            activeWorkSeconds: activeWorkSeconds,
            regularScheduledSeconds: regularScheduledSeconds,
            extraScheduledSeconds: extraScheduledSeconds,
            casesInRegular: casesInRegular,
            casesInExtra: casesInExtra,
			modalityBreakdownRegular: modalityBreakdownRegular, 
			modalityBreakdownExtra: modalityBreakdownExtra, 
            logoutType: summary.logouts.length > 0 ? summary.logouts[summary.logouts.length - 1].type : null,


        });
    }
    
    return results.sort((a, b) => b.date.localeCompare(a.date));
}

// Display summary cards
function displayTimeLogSummary(summaries) {
    const summaryDiv = document.getElementById('timeLogSummary');
    
    if (summaries.length === 0) {
        summaryDiv.innerHTML = '';
        return;
    }
    
    const totalDays = summaries.length;
    const totalActiveWork = summaries.reduce((sum, s) => sum + s.activeWorkSeconds, 0);
    const totalExtra = summaries.reduce((sum, s) => sum + s.extraSeconds, 0);
    const totalInactive = summaries.reduce((sum, s) => sum + s.totalInactiveSeconds, 0);
    
    summaryDiv.innerHTML = `
        <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; border-radius: 8px; color: white;">
            <div style="font-size: 32px; font-weight: bold;">${totalDays}</div>
            <div style="opacity: 0.9;">Total Days</div>
        </div>
        <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); padding: 20px; border-radius: 8px; color: white;">
            <div style="font-size: 32px; font-weight: bold;">${formatHoursMinutes(totalActiveWork)}</div>
            <div style="opacity: 0.9;">Total Active Work</div>
        </div>
        <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 20px; border-radius: 8px; color: white;">
            <div style="font-size: 32px; font-weight: bold;">${formatHoursMinutes(totalExtra)}</div>
            <div style="opacity: 0.9;">Total Extra Hours</div>
        </div>
        <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 20px; border-radius: 8px; color: white;">
            <div style="font-size: 32px; font-weight: bold;">${formatHoursMinutes(totalInactive)}</div>
            <div style="opacity: 0.9;">Total Inactive Time</div>
        </div>
    `;
}

// Display time logs table
function displayTimeLogsTable(summaries) {
    const tbody = document.getElementById('timeLogsTableBody');
    
    if (summaries.length === 0) {
        tbody.innerHTML = '<tr><td colspan="11" style="text-align: center; padding: 20px; color: #7f8c8d;">No time logs found for selected filters</td></tr>';
        return;
    }
    
    // Group by date first, then by employee
    const groupedByDate = {};
    summaries.forEach(summary => {
        if (!groupedByDate[summary.date]) {
            groupedByDate[summary.date] = [];
        }
        groupedByDate[summary.date].push(summary);
    });
    
    let html = '';
    
    // Sort dates descending (newest first)
    Object.keys(groupedByDate).sort().reverse().forEach(date => {
        const dateData = groupedByDate[date];
        
        // Date header row
        html += `
            <tr style="background: #34495e; color: white;">
                <td colspan="9" style="padding: 12px; font-weight: 600; font-size: 14px;">
                    📅 ${new Date(date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
                    <span style="float: right; font-weight: normal; font-size: 12px;">
                        ${dateData.length} employee(s) worked
                    </span>
                </td>
            </tr>
        `;
        
        // Employee rows for this date
        dateData.forEach(summary => {
            const extraHoursColor = summary.extraSeconds > 0 ? '#e74c3c' : '#95a5a6';
            const logoutBadge = summary.lastLogout 
                ? (summary.logoutType === 'timeout' ? '⏱️ Timeout' : '✅ Manual')
                : '🟢 Still Active';
            
            const idleWarning = summary.totalInactiveSeconds > 3600 ? '⚠️ ' : ''; // Warn if >1h idle
            
            html += `
                <tr style="border-bottom: 1px solid #ecf0f1; background: white;">
                    <td style="padding: 12px;">
                        <strong>${summary.empName}</strong><br>
                        <small style="color: #7f8c8d;">${summary.empCode}</small>
                    </td>
                    <td style="padding: 12px; text-align: center;">
                        ${summary.firstLogin.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' })}
                    </td>
                    <td style="padding: 12px; text-align: center;">
                        ${summary.lastLogout 
                            ? summary.lastLogout.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }) 
                            : '<em style="color: #7f8c8d;">Active</em>'}
                        <br><small style="color: #7f8c8d; font-size: 10px;">${logoutBadge}</small>
                    </td>
                    <td style="padding: 12px; text-align: center; font-weight: 600;">
                        ${formatHoursMinutes(summary.totalLoggedSeconds)}
                    </td>
                    <td style="padding: 12px; text-align: center; color: #e67e22;">
                        ${idleWarning}${formatHoursMinutes(summary.totalInactiveSeconds)}
                    </td>
                    <td style="padding: 12px; text-align: center; font-weight: 600; color: #27ae60;">
                        ${formatHoursMinutes(summary.activeWorkSeconds)}
                    </td>
                    <td style="padding: 12px; text-align: center; font-weight: bold; font-size: 14px; color: ${extraHoursColor};">
                        ${summary.extraSeconds > 0 ? '+' : ''}${formatHoursMinutes(summary.extraSeconds)}
                    </td>
                    <td style="padding: 12px; text-align: center;">
                        <button onclick="viewDetailedSession('${summary.empCode}', '${summary.date}')" 
                                class="btn" style="padding: 6px 12px; font-size: 11px; background: #3498db;">
                            📋 Timeline
                        </button>
                    </td>
                </tr>
            `;
        });
    });
    
    tbody.innerHTML = html;
}
// Format seconds to "Xh Ym" format
function formatHoursMinutes(seconds) {
    if (!seconds || seconds === 0) return '0h 0m';
    
    const hours = Math.floor(seconds / 3600);
    const minutes = Math.floor((seconds % 3600) / 60);
    
    return `${hours}h ${minutes}m`;
}
// View detailed session timeline
async function viewDetailedSession(empCode, date) {
    try {
        // Fetch all logs for this employee and date
        const allLogs = await getFromFirestore('time_logs');
        const sessionLogs = allLogs.filter(log => {
            const logDate = new Date(log.timestamp).toISOString().split('T')[0];
            return log.empCode === empCode && logDate === date;
        }).sort((a, b) => new Date(a.timestamp) - new Date(b.timestamp));
        
        if (sessionLogs.length === 0) {
            showNotification('No logs found for this session');
            return;
        }
        
        const employee = authorizedEmployees[empCode];
        
        // Build timeline HTML
        let timelineHtml = `
            <div style="max-height: 500px; overflow-y: auto;">
                <h3>${employee.name} (${empCode})</h3>
                <h4>${new Date(date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</h4>
                <div style="margin-top: 20px; padding-left: 20px; border-left: 3px solid #3498db;">
        `;
        
        sessionLogs.forEach(log => {
            const time = new Date(log.timestamp).toLocaleTimeString();
            let icon = '';
            let color = '#34495e';
            let label = log.eventType;
            
            switch(log.eventType) {
                case 'login':
                    icon = '🟢';
                    color = '#27ae60';
                    label = 'Logged In';
                    break;
                case 'logout':
                    icon = '🔴';
                    color = '#e74c3c';
                    label = log.logoutType === 'timeout' ? 'Auto Logout (Timeout)' : 'Logged Out';
                    break;
                case 'inactivity_start':
                    icon = '😴';
                    color = '#f39c12';
                    label = 'Became Inactive';
                    break;
                case 'inactivity_end':
                    icon = '⚡';
                    color = '#16a085';
                    label = `Resumed Activity (${Math.floor(log.durationSeconds / 60)} min idle)`;
                    break;
            }
            
            timelineHtml += `
                <div style="margin-bottom: 15px; padding: 10px; background: ${color}10; border-radius: 5px;">
                    <div style="font-weight: 600; color: ${color};">${icon} ${label}</div>
                    <div style="font-size: 12px; color: #7f8c8d; margin-top: 5px;">${time}</div>
                </div>
            `;
        });
        
        timelineHtml += `
                </div>
            </div>
            <div style="text-align: right; margin-top: 20px;">
                <button onclick="closeModal()" class="btn">Close</button>
            </div>
        `;
        
        createModal(timelineHtml);
        
    } catch (error) {
        console.error('[Session Details] Error:', error);
        showNotification('Error loading session details');
    }
}

// Export time logs to CSV
async function exportTimeLogs() {
console.log("Export triggered");
    const empCode = document.getElementById('timeLogEmpFilter').value;
    const fromDate = document.getElementById('timeLogFromDate').value;
    const toDate = document.getElementById('timeLogToDate').value;
    
    if (!fromDate || !toDate) {
        showNotification('⚠️ Please select date range first');
        return;
    }
    
    try {
        // Get all logs and calculate summaries
        const allLogs = await getFromFirestore('time_logs');
        const filteredLogs = allLogs.filter(log => {
            const logDate = new Date(log.timestamp).toISOString().split('T')[0];
            const matchesDate = logDate >= fromDate && logDate <= toDate;
            const matchesEmp = !empCode || log.empCode === empCode;
            return matchesDate && matchesEmp;
        });
        
        const summaries = await calculateDailySummaries(filteredLogs);
        if (summaries.length === 0) {
            showNotification('⚠️ No data to export');
            return;
        }
        
        // Build CSV
		let csv = 'Date,Employee Code,Employee Name,First Login,Last Logout,Total Logged (hours),Inactive Time (hours),Active Work (hours),Scheduled Regular (hours),Scheduled Extra (hours),Cases (Regular),Modality Breakdown (Regular),Cases (Extra),Modality Breakdown (Extra),Logout Type\n';     
		if (!summaries || summaries.length === 0) {
			showNotification('⚠️ No data to export');
			return;
		}

		// Safety check
		if (!Array.isArray(summaries)) {
			console.error('[Export] summaries is not an array:', summaries);
			showNotification('❌ Error: Invalid data format');
			return;
		}

		summaries.forEach(summary => {
			// Format modality breakdowns for CSV
			const regularBreakdown = summary.modalityBreakdownRegular 
				? Object.entries(summary.modalityBreakdownRegular).map(([m, c]) => `${m}:${c}`).join('; ')
				: '';
			const extraBreakdown = summary.modalityBreakdownExtra
				? Object.entries(summary.modalityBreakdownExtra).map(([m, c]) => `${m}:${c}`).join('; ')
				: '';
			
			const row = [
				summary.date,
				summary.empCode,
				`"${summary.empName}"`,
				summary.firstLogin.toLocaleTimeString(),
				summary.lastLogout ? summary.lastLogout.toLocaleTimeString() : 'Still Active',
				(summary.totalLoggedSeconds / 3600).toFixed(2),
				(summary.totalInactiveSeconds / 3600).toFixed(2),
				(summary.activeWorkSeconds / 3600).toFixed(2),
				(summary.regularScheduledSeconds / 3600).toFixed(2),
				(summary.extraScheduledSeconds / 3600).toFixed(2),
				summary.casesInRegular || 0,
				`"${regularBreakdown}"`,  // ✅ ADD THIS
				summary.casesInExtra || 0,
				`"${extraBreakdown}"`,    // ✅ ADD THIS
				summary.logoutType || 'active'
			];
			csv += row.join(',') + '\n';
		});  
		
				// Download CSV
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `time_logs_${fromDate}_to_${toDate}.csv`;
        a.click();
        window.URL.revokeObjectURL(url);
        
        showNotification('✅ Time logs exported successfully');
        
    } catch (error) {
        console.error('[Export] Error:', error);
        showNotification('❌ Error exporting time logs');
    }
}

// Format modality breakdown for tooltip
function formatModalityBreakdown(breakdown) {
    if (!breakdown || Object.keys(breakdown).length === 0) {
        return 'No cases';
    }
    
    const lines = Object.entries(breakdown)
        .sort((a, b) => b[1] - a[1]) // Sort by count descending
        .map(([modality, count]) => `${modality}: ${count} case${count !== 1 ? 's' : ''}`)
        .join('\n');
    
    return lines;
}

function displayTimeLogsTableExpandable(summaries, rawLogs) {
    const tbody = document.getElementById('timeLogsTableBody');
    
    if (summaries.length === 0) {
        tbody.innerHTML = '<tr><td colspan="12" style="text-align: center; padding: 20px; color: #7f8c8d;">No time logs found for selected filters</td></tr>';
        document.getElementById('paginationInfo').style.display = 'none';
        document.getElementById('paginationControls').style.display = 'none';
        return;
    }
    
    // Store all summaries for pagination
    allFilteredSummaries = summaries;
    
    // Calculate pagination
    const totalResults = summaries.length;
    const totalPages = Math.ceil(totalResults / rowsPerPage);
    const startIndex = (currentPage - 1) * rowsPerPage;
    const endIndex = Math.min(startIndex + rowsPerPage, totalResults);
    const currentPageData = summaries.slice(startIndex, endIndex);
    
    // Update pagination info
    document.getElementById('paginationInfo').style.display = 'block';
    document.getElementById('paginationInfo').innerHTML = `
        Showing ${startIndex + 1}-${endIndex} of ${totalResults} results
    `;
    
    // Group by date
    const groupedByDate = {};
    currentPageData.forEach(summary => {
        if (!groupedByDate[summary.date]) {
            groupedByDate[summary.date] = [];
        }
        groupedByDate[summary.date].push(summary);
    });
    
    let html = '';
    
    // Sort dates descending
    Object.keys(groupedByDate).sort().reverse().forEach(date => {
        const dateData = groupedByDate[date];
        
        // Date header row
        html += `
            <tr style="background: #34495e; color: white;">
                <td colspan="12" style="padding: 12px; font-weight: 600; font-size: 14px;">
                    📅 ${new Date(date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
                    <span style="float: right; font-weight: normal; font-size: 12px;">
                        ${dateData.length} employee(s)
                    </span>
                </td>
            </tr>
        `;
        
        // Employee rows
        dateData.forEach(summary => {
            const extraHoursColor = summary.extraSeconds > 0 ? '#e74c3c' : '#95a5a6';
            const logoutBadge = summary.lastLogout 
                ? (summary.logoutType === 'timeout' ? '⏱️ Timeout' : '✅ Manual')
                : '🟢 Active';
            
            const idleWarning = summary.totalInactiveSeconds > 3600 ? '⚠️ ' : '';
            const rowId = `row_${summary.empCode}_${summary.date}`;
            const detailsId = `details_${summary.empCode}_${summary.date}`;
            
            // Main row
html += `
    <tr id="${rowId}" style="border-bottom: 1px solid #ecf0f1; background: white; cursor: pointer;" 
        onclick="toggleSessionDetails('${detailsId}', '${summary.empCode}', '${summary.date}')">
        <td style="padding: 12px; text-align: center;">
            <span id="icon_${detailsId}" style="font-size: 14px;">▶️</span>
        </td>
        <td style="padding: 12px;">
            <strong>${summary.empName}</strong><br>
            <small style="color: #7f8c8d;">${summary.empCode}</small>
        </td>
        <td style="padding: 12px; text-align: center;">
            ${summary.firstLogin.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' })}
        </td>
        <td style="padding: 12px; text-align: center;">
            ${summary.lastLogout 
                ? summary.lastLogout.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }) 
                : '<em style="color: #7f8c8d;">Active</em>'}
            <br><small style="color: #7f8c8d; font-size: 10px;">${logoutBadge}</small>
        </td>
        <td style="padding: 12px; text-align: center; font-weight: 600;">
            ${formatHoursMinutes(summary.totalLoggedSeconds)}
        </td>
        <td style="padding: 12px; text-align: center; color: #e67e22;">
            ${idleWarning}${formatHoursMinutes(summary.totalInactiveSeconds)}
        </td>
        <td style="padding: 12px; text-align: center; font-weight: 600; color: #27ae60;">
            ${formatHoursMinutes(summary.activeWorkSeconds)}
        </td>
        <td style="padding: 12px; text-align: center; font-weight: 600; color: #3498db;">
            ${formatHoursMinutes(summary.regularScheduledSeconds)}
        </td>
        <td style="padding: 12px; text-align: center; font-weight: 600; color: #9b59b6;">
            ${formatHoursMinutes(summary.extraScheduledSeconds)}
        </td>
        <td style="padding: 12px; text-align: center; font-weight: 600; color: #3498db; font-size: 16px; cursor: help;" 
			title="${formatModalityBreakdown(summary.modalityBreakdownRegular)}">
			${summary.casesInRegular || 0}
		</td>
		<td style="padding: 12px; text-align: center; font-weight: 600; color: #e74c3c; font-size: 16px; cursor: help;"
			title="${formatModalityBreakdown(summary.modalityBreakdownExtra)}">
			${summary.casesInExtra || 0}
		</td>
        <td style="padding: 12px; text-align: center;">
            <button onclick="event.stopPropagation(); viewDetailedSession('${summary.empCode}', '${summary.date}')" 
                    class="btn" style="padding: 6px 12px; font-size: 11px; background: #3498db;">
                📋 Timeline
            </button>
        </td>
    </tr>
`;
            
            // Expandable details row (hidden by default)
            html += `
                <tr id="${detailsId}" style="display: none; background: #f8f9fa;">
                    <td colspan="12" style="padding: 15px 20px;">
                        <div id="content_${detailsId}" style="padding: 10px;">
                            <em style="color: #7f8c8d;">Click to load session details...</em>
                        </div>
                    </td>
                </tr>
            `;
        });
    });
    
    tbody.innerHTML = html;
    
    // Update pagination controls
    updatePaginationControls(totalPages);
}

// Toggle session details in time logs
function toggleSessionDetails(detailsId, empCode, date) {
    const detailsRow = document.getElementById(detailsId);
    const icon = document.getElementById(`icon_${detailsId}`);
    
    if (!detailsRow || !icon) return;
    
    if (detailsRow.style.display === 'none' || !detailsRow.style.display) {
        detailsRow.style.display = 'table-row';
        icon.textContent = '🔽';
        
        // Load session details if not loaded yet
        const contentDiv = document.getElementById(`content_${detailsId}`);
        if (contentDiv && contentDiv.innerHTML.includes('Click to load')) {
            loadSessionDetailsInline(empCode, date, contentDiv);
        }
    } else {
        detailsRow.style.display = 'none';
        icon.textContent = '▶️';
    }
}

async function loadSessionDetailsInline(empCode, date, contentDiv) {
    contentDiv.innerHTML = '<em style="color: #7f8c8d;">Loading...</em>';
    
    try {
        const allLogs = await getFromFirestore('time_logs');
        const sessionLogs = allLogs.filter(log => {
            const logDate = new Date(log.timestamp).toISOString().split('T')[0];
            return log.empCode === empCode && logDate === date;
        }).sort((a, b) => new Date(a.timestamp) - new Date(b.timestamp));
        
        if (sessionLogs.length === 0) {
            contentDiv.innerHTML = '<em style="color: #7f8c8d;">No session logs found</em>';
            return;
        }
        
        let html = '<div style="padding-left: 20px; border-left: 3px solid #3498db;">';
        
        sessionLogs.forEach(log => {
            const time = new Date(log.timestamp).toLocaleTimeString();
            let icon = '';
            let color = '#34495e';
            let label = log.eventType;
            
            switch(log.eventType) {
                case 'login':
                    icon = '🟢';
                    color = '#27ae60';
                    label = 'Logged In';
                    break;
                case 'logout':
                    icon = '🔴';
                    color = '#e74c3c';
                    label = log.logoutType === 'timeout' ? 'Auto Logout (Timeout)' : 'Logged Out';
                    break;
                case 'inactivity_start':
                    icon = '😴';
                    color = '#f39c12';
                    label = 'Became Inactive';
                    break;
                case 'inactivity_end':
                    icon = '⚡';
                    color = '#16a085';
                    label = `Resumed Activity (${Math.floor(log.durationSeconds / 60)} min idle)`;
                    break;
            }
            
            html += `
                <div style="margin-bottom: 15px; padding: 10px; background: ${color}10; border-radius: 5px;">
                    <div style="font-weight: 600; color: ${color};">${icon} ${label}</div>
                    <div style="font-size: 12px; color: #7f8c8d; margin-top: 5px;">${time}</div>
                </div>
            `;
        });
        
        html += '</div>';
        contentDiv.innerHTML = html;
        
    } catch (error) {
        console.error('[Session Details] Error:', error);
        contentDiv.innerHTML = '<em style="color: #e74c3c;">Error loading session details</em>';
    }
}

// Update pagination controls
function updatePaginationControls(totalPages) {
    const controls = document.getElementById('paginationControls');
    controls.style.display = 'flex';
    
    const prevDisabled = currentPage === 1 ? 'disabled style="opacity: 0.5; cursor: not-allowed;"' : '';
    const nextDisabled = currentPage === totalPages ? 'disabled style="opacity: 0.5; cursor: not-allowed;"' : '';
    
    controls.innerHTML = `
        <button onclick="changePage(${currentPage - 1})" class="btn" ${prevDisabled} style="background: #95a5a6; margin-right: 10px;">
            ← Previous
        </button>
        <span style="margin: 0 15px; display: flex; align-items: center; font-weight: 600;">
            Page ${currentPage} of ${totalPages}
        </span>
        <button onclick="changePage(${currentPage + 1})" class="btn" ${nextDisabled} style="background: #95a5a6; margin-left: 10px;">
            Next →
        </button>
        <span style="margin-left: 30px; display: flex; align-items: center;">
            Show per page:
            <select onchange="changeRowsPerPage(this.value)" style="margin-left: 10px; padding: 5px; border-radius: 5px; border: 1px solid #ddd;">
                <option value="15" ${rowsPerPage === 15 ? 'selected' : ''}>15</option>
                <option value="25" ${rowsPerPage === 25 ? 'selected' : ''}>25</option>
                <option value="50" ${rowsPerPage === 50 ? 'selected' : ''}>50</option>
                <option value="100" ${rowsPerPage === 100 ? 'selected' : ''}>100</option>
            </select>
        </span>
    `;
}

// Change page
function changePage(newPage) {
    const totalPages = Math.ceil(allFilteredSummaries.length / rowsPerPage);
    
    if (newPage < 1 || newPage > totalPages) return;
    
    currentPage = newPage;
    
    // Re-fetch raw logs for current page data only
    const startIndex = (currentPage - 1) * rowsPerPage;
    const endIndex = Math.min(startIndex + rowsPerPage, allFilteredSummaries.length);
    const currentPageData = allFilteredSummaries.slice(startIndex, endIndex);
    
    // Get unique empCodes and dates for current page
    const empCodesAndDates = currentPageData.map(s => ({ empCode: s.empCode, date: s.date }));
    
    // Filter raw logs for only current page employees/dates
    const fromDate = document.getElementById('timeLogFromDate').value;
    const toDate = document.getElementById('timeLogToDate').value;
    
    getFromFirestore('time_logs').then(allLogs => {
        const filteredLogs = allLogs.filter(log => {
            if (!log.timestamp) return false;
            const logDate = new Date(log.timestamp).toISOString().split('T')[0];
            const matchesDate = logDate >= fromDate && logDate <= toDate;
            
            // Only include logs for employees on current page
            const isOnCurrentPage = empCodesAndDates.some(
                item => item.empCode === log.empCode && item.date === logDate
            );
            
            return matchesDate && isOnCurrentPage;
        });
        
        displayTimeLogsTableExpandable(allFilteredSummaries, filteredLogs);
    });
}

// Change rows per page
function changeRowsPerPage(newRowsPerPage) {
    rowsPerPage = parseInt(newRowsPerPage);
    currentPage = 1; // Reset to first page
    
    // Re-display with new page size
    changePage(1);
}

// ============================================
// MODALITY KEYWORDS MANAGER
// ============================================

async function showModalityKeywordsManager() {
    const modalityKeywords = await getFromFirestore('modality_keywords');
    
    let tableHtml = '';
    
    if (modalityKeywords.length === 0) {
        tableHtml = `
            <tr>
                <td colspan="5" style="text-align: center; padding: 40px; color: #7f8c8d;">
                    No modality keywords defined yet. Click "Add New Modality" to get started.
                </td>
            </tr>
        `;
    } else {
        modalityKeywords.sort((a, b) => (a.name || '').localeCompare(b.name || ''));
        
        modalityKeywords.forEach(modality => {
            const keywordCount = modality.keywords ? modality.keywords.length : 0;
            const keywordPreview = modality.keywords && modality.keywords.length > 0 
                ? modality.keywords.slice(0, 3).join(', ') + (keywordCount > 3 ? '...' : '')
                : 'No keywords';
            
            tableHtml += `
                <tr>
                    <td style="padding: 12px;">
                        <strong>${modality.name || modality.id}</strong>
                    </td>
                    <td style="padding: 12px;">
                        <span style="background: ${modality.color || '#95a5a6'}; color: white; padding: 4px 8px; border-radius: 4px; font-size: 11px;">
                            ${modality.id}
                        </span>
                    </td>
                    <td style="padding: 12px; font-size: 12px; color: #7f8c8d;">
                        ${keywordPreview}
                        <br><small>(${keywordCount} keyword${keywordCount !== 1 ? 's' : ''})</small>
                    </td>
                    <td style="padding: 12px; text-align: center;">
                        <span style="color: ${modality.enabled !== false ? '#27ae60' : '#e74c3c'};">
                            ${modality.enabled !== false ? '✅ Active' : '❌ Disabled'}
                        </span>
                    </td>
                    <td style="padding: 12px; text-align: center;">
                        <button onclick="editModalityKeywords('${modality.id}')" class="btn" style="padding: 6px 12px; font-size: 12px; background: #3498db; margin-right: 5px;">
                            ✏️ Edit
                        </button>
                        <button onclick="deleteModalityKeywords('${modality.id}')" class="btn" style="padding: 6px 12px; font-size: 12px; background: #e74c3c;">
                            🗑️ Delete
                        </button>
                    </td>
                </tr>
            `;
        });
    }
    
    const modal = createModal(`
        <h3>🏥 Modality Keywords Manager</h3>
        <p style="color: #7f8c8d; margin-bottom: 20px;">
            Define keywords to automatically detect modality from report text. 
            Keywords are checked against the <strong>first line</strong> of the report.
        </p>
        
        <div style="margin-bottom: 20px; text-align: right;">
            <button onclick="editModalityKeywords(null)" class="btn" style="background: #27ae60;">
                ➕ Add New Modality
            </button>
        </div>
        
        <div style="max-height: 500px; overflow-y: auto;">
            <table style="width: 100%; border-collapse: collapse; background: white;">
                <thead style="background: #34495e; color: white; position: sticky; top: 0;">
                    <tr>
                        <th style="padding: 12px; text-align: left;">Name</th>
                        <th style="padding: 12px; text-align: left;">ID</th>
                        <th style="padding: 12px; text-align: left;">Keywords</th>
                        <th style="padding: 12px; text-align: center;">Status</th>
                        <th style="padding: 12px; text-align: center;">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    ${tableHtml}
                </tbody>
            </table>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
        </div>
    `);
}

async function editModalityKeywords(modalityId) {
    let modalityData = {
        id: '',
        name: '',
        color: '#3498db',
        keywords: [],
        enabled: true
    };
    
    // Load existing data if editing
    if (modalityId) {
        const allModalities = await getFromFirestore('modality_keywords');
        const existing = allModalities.find(m => m.id === modalityId);
        if (existing) {
            modalityData = existing;
        }
    }
    
    const isNew = !modalityId;
    const keywordsText = modalityData.keywords ? modalityData.keywords.join('\n') : '';
    
    const modal = createModal(`
        <h3>${isNew ? '➕ Add New' : '✏️ Edit'} Modality</h3>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Modality ID (Short Code):</label>
            <input type="text" id="modalityId" value="${modalityData.id}" 
                   ${!isNew ? 'readonly' : ''} 
                   placeholder="e.g., CT, MRI, US, XR"
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; ${!isNew ? 'background: #ecf0f1;' : ''}">
            <small style="color: #7f8c8d;">Must be unique, uppercase (e.g., CT, MRI, US)</small>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Display Name:</label>
            <input type="text" id="modalityName" value="${modalityData.name}" 
                   placeholder="e.g., CT Scan, MRI, Ultrasound"
                   style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px;">
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Color:</label>
            <input type="color" id="modalityColor" value="${modalityData.color}" 
                   style="width: 100px; height: 40px; border: 1px solid #ddd; border-radius: 5px;">
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Keywords (one per line):</label>
            <textarea id="modalityKeywords" rows="10" 
                      placeholder="CT SCAN&#10;COMPUTED TOMOGRAPHY&#10;CECT&#10;NCCT&#10;CT BRAIN&#10;CT ABDOMEN"
                      style="width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; font-family: monospace;">${keywordsText}</textarea>
            <small style="color: #7f8c8d;">
                💡 Keywords will be checked in the <strong>first line</strong> of the report.<br>
                Plural forms are automatically matched (e.g., "RADIOGRAPH" matches "RADIOGRAPHS")
            </small>
        </div>
        
        <div style="margin: 20px 0;">
            <label style="display: flex; align-items: center; cursor: pointer;">
                <input type="checkbox" id="modalityEnabled" ${modalityData.enabled !== false ? 'checked' : ''}
                       style="margin-right: 10px; width: 20px; height: 20px;">
                <span style="font-weight: 500;">Enabled (active for detection)</span>
            </label>
        </div>
        
        <div style="text-align: right; margin-top: 20px;">
            <button onclick="saveModalityKeywords(${isNew})" class="btn" style="background: #27ae60;">
                💾 Save Modality
            </button>
            <button onclick="closeModal(); showModalityKeywordsManager();" class="btn" style="background: #95a5a6;">
                Cancel
            </button>
        </div>
    `);
}

async function saveModalityKeywords(isNew) {
    const id = document.getElementById('modalityId').value.trim().toUpperCase();
    const name = document.getElementById('modalityName').value.trim();
    const color = document.getElementById('modalityColor').value;
    const keywordsText = document.getElementById('modalityKeywords').value.trim();
    const enabled = document.getElementById('modalityEnabled').checked;
    
    // Validation
    if (!id) {
        alert('Please enter a Modality ID');
        return;
    }
    
    if (!name) {
        alert('Please enter a Display Name');
        return;
    }
    
    if (!keywordsText) {
        alert('Please enter at least one keyword');
        return;
    }
    
    // Check for duplicate ID if new
    if (isNew) {
        const allModalities = await getFromFirestore('modality_keywords');
        const exists = allModalities.find(m => m.id === id);
        if (exists) {
            alert(`Modality ID "${id}" already exists. Please use a different ID.`);
            return;
        }
    }
    
    // Parse keywords
    const keywords = keywordsText
        .split('\n')
        .map(k => k.trim().toUpperCase())
        .filter(k => k.length > 0);
    
    if (keywords.length === 0) {
        alert('Please enter at least one valid keyword');
        return;
    }
    
    const modalityData = {
        id: id,
        name: name,
        color: color,
        keywords: keywords,
        enabled: enabled,
        searchLocation: 'heading',  // Always search in heading (first line)
        updatedAt: new Date().toISOString()
    };
    
    try {
        if (isNew) {
            await saveToFirestore('modality_keywords', modalityData);
            showNotification('✅ Modality added successfully');
        } else {
            // Update existing
            const snapshot = await db.collection('modality_keywords')
                .where('id', '==', id)
                .get();
            
            if (!snapshot.empty) {
                await snapshot.docs[0].ref.update(modalityData);
                showNotification('✅ Modality updated successfully');
            }
        }
        
        closeModal();
        showModalityKeywordsManager();
        
    } catch (error) {
        console.error('Error saving modality:', error);
        alert('❌ Error saving modality. Please try again.');
    }
}

async function deleteModalityKeywords(modalityId) {
    if (!confirm(`Delete modality "${modalityId}"? This cannot be undone.`)) {
        return;
    }
    
    try {
        const snapshot = await db.collection('modality_keywords')
            .where('id', '==', modalityId)
            .get();
        
        if (!snapshot.empty) {
            await snapshot.docs[0].ref.delete();
            showNotification('✅ Modality deleted successfully');
            showModalityKeywordsManager();
        }
        
    } catch (error) {
        console.error('Error deleting modality:', error);
        alert('❌ Error deleting modality. Please try again.');
    }
}

// ============================================
// MODALITY DETECTION FROM REPORT TEXT
// ============================================

async function detectModalityFromReport(reportText) {
    if (!reportText || reportText.trim().length === 0) {
        return {
            detected: null,
            name: 'Unknown',
            confidence: 'none',
            matchedKeyword: null
        };
    }
    
    // Get all modality keywords from Firestore
    const modalityKeywords = await getFromFirestore('modality_keywords');
    
    // Filter only enabled modalities
    const enabledModalities = modalityKeywords.filter(m => m.enabled !== false);
    
    if (enabledModalities.length === 0) {
        return {
            detected: null,
            name: 'Unknown',
            confidence: 'none',
            matchedKeyword: null
        };
    }
    
    // Extract first line (heading) from report
    const lines = reportText.split('\n').map(l => l.trim()).filter(l => l.length > 0);
    if (lines.length === 0) {
        return {
            detected: null,
            name: 'Unknown',
            confidence: 'none',
            matchedKeyword: null
        };
    }
    
    const heading = lines[0].toUpperCase();
    console.log('[Modality Detection] First line:', heading);
    
    // Track all matches (for ambiguity detection)
    const allMatches = [];
    
    // Check each modality
    for (const modality of enabledModalities) {
        for (const keyword of modality.keywords || []) {
            const keywordUpper = keyword.toUpperCase().trim();
            
            // Create regex to match whole words (handles plurals)
            // "RADIOGRAPH" matches "RADIOGRAPH" and "RADIOGRAPHS"
            const regex = new RegExp(`\\b${keywordUpper}S?\\b`, 'i');
            
            if (regex.test(heading)) {
				allMatches.push({
					modality: modality,
					keyword: keyword,
					keywordLength: keyword.length  // ✅ Track length for priority
				});
				console.log('[Modality Detection] Matched:', modality.id, 'via keyword:', keyword);
			}
        }
    }
    
    // No matches found
			if (allMatches.length === 0) {
				return {
					detected: null,
					name: 'Unknown',
					confidence: 'none',
					matchedKeyword: null
				};
			}

			// Group matches by modality
		const matchesByModality = {};
		allMatches.forEach(match => {
			const modalityId = match.modality.id;
			if (!matchesByModality[modalityId]) {
				matchesByModality[modalityId] = [];
			}
			matchesByModality[modalityId].push(match);
		});

		const uniqueModalities = Object.keys(matchesByModality);

		// Single modality matched (possibly via multiple keywords) - high confidence
		if (uniqueModalities.length === 1) {
			// Pick the longest/most specific keyword from this modality
			const matches = matchesByModality[uniqueModalities[0]];
			const bestMatch = matches.reduce((best, current) => 
				current.keywordLength > best.keywordLength ? current : best
			);
			
			return {
				detected: bestMatch.modality.id,
				name: bestMatch.modality.name,
				confidence: 'high',
				matchedKeyword: bestMatch.keyword
			};
		}
    

		// For each modality, show only the longest matching keyword
		const ambiguousMatches = uniqueModalities.map(modalityId => {
			const matches = matchesByModality[modalityId];
			const bestMatch = matches.reduce((best, current) => 
				current.keywordLength > best.keywordLength ? current : best
			);
			return {
				id: bestMatch.modality.id,
				name: bestMatch.modality.name,
				keyword: bestMatch.keyword
			};
		});

		return {
			detected: null,
			name: 'Ambiguous',
			confidence: 'ambiguous',
			matchedKeyword: null,
			allMatches: ambiguousMatches
		};
}

// ============================================
// MODALITY MISMATCH WARNING MODAL
// ============================================

function showModalityWarning(selectedModality, detectedInfo) {
    return new Promise((resolve) => {
        let warningContent = '';
        
        if (detectedInfo.confidence === 'ambiguous') {
            // Multiple modalities detected - ask user to choose
            const modalitiesList = detectedInfo.allMatches
                .map(m => `<li><strong>${m.name}</strong> (found: "${m.keyword}")</li>`)
                .join('');
            
            warningContent = `
                <div style="background: #fff3cd; padding: 15px; border-radius: 8px; border-left: 4px solid #f39c12; margin: 20px 0;">
                    <p style="margin: 0 0 10px 0;"><strong>⚠️ Multiple Modalities Detected</strong></p>
                    <p style="margin: 0 0 10px 0;"><strong>Dropdown Selection:</strong> ${selectedModality}</p>
                    <p style="margin: 0 0 10px 0;"><strong>Report heading contains:</strong></p>
                    <ul style="margin: 10px 0; padding-left: 20px;">
                        ${modalitiesList}
                    </ul>
                    <p style="font-size: 12px; color: #7f8c8d; margin: 10px 0 0 0;">
                        The report heading matches multiple modalities. Please select the correct one.
                    </p>
                </div>
                
                <p style="font-weight: 500; margin-bottom: 15px;">What would you like to do?</p>
            `;
        } else {
            // Single mismatch
            warningContent = `
                <div style="background: #fff3cd; padding: 15px; border-radius: 8px; border-left: 4px solid #f39c12; margin: 20px 0;">
                    <p style="margin: 0 0 10px 0;"><strong>⚠️ Modality Mismatch Detected</strong></p>
                    <p style="margin: 0 0 5px 0;"><strong>Dropdown Selection:</strong> ${selectedModality}</p>
                    <p style="margin: 0 0 10px 0;"><strong>Report Text Suggests:</strong> ${detectedInfo.name}</p>
                    <p style="font-size: 12px; color: #7f8c8d; margin: 10px 0 0 0;">
                        Found keyword: "<strong>${detectedInfo.matchedKeyword}</strong>" in report heading
                    </p>
                </div>
                
                <p style="font-weight: 500; margin-bottom: 15px;">What would you like to do?</p>
            `;
        }
        
        const modal = createModal(`
            <h3>⚠️ Modality Verification Required</h3>
            
            ${warningContent}
       
	   
            <div style="display: flex; flex-direction: column; gap: 10px; margin-top: 20px;">
                ${detectedInfo.confidence === 'ambiguous' ? 
                    detectedInfo.allMatches.map(m => `
                        <button onclick="window.modalityWarningChoice='correct_${m.id}'; closeModal();" 
                                class="btn" style="background: #27ae60; width: 100%; padding: 12px;">
                            ✅ Correct to ${m.name}
                        </button>
                    `).join('') :
                    `<button onclick="window.modalityWarningChoice='correct'; closeModal();" 
                            class="btn" style="background: #27ae60; width: 100%; padding: 12px;">
                        ✅ Correct to ${detectedInfo.name}
                    </button>`
                }
                <button onclick="window.modalityWarningChoice='keep'; closeModal();" 
                        class="btn" style="background: #3498db; width: 100%; padding: 12px;">
                    📝 Keep ${selectedModality} & Submit Anyway
                </button>
                <button onclick="window.modalityWarningChoice='cancel'; closeModal();" 
                        class="btn" style="background: #95a5a6; width: 100%; padding: 12px;">
                    ❌ Cancel (Don't Submit)
                </button>
            </div>
        `);
        
        // Wait for user choice
        const checkChoice = setInterval(() => {
            if (window.modalityWarningChoice) {
                clearInterval(checkChoice);
                const choice = window.modalityWarningChoice;
                delete window.modalityWarningChoice;
                resolve(choice);
            }
        }, 100);
    });
}
	   
// ==============================================
// INITIALIZATION
// ==============================================

window.addEventListener('load', function() {
window.addEventListener('beforeunload', async () => {
        if (currentSessionId) {
            try {
                await endSessionTracking('window_close');
            } catch (error) {
                console.error('[Session] Cleanup error:', error);
            }
        }
    });
    const textEditor = document.getElementById('textEditor');

// Display app version (fetched from service worker)
fetchAndDisplayVersion();

async function fetchAndDisplayVersion() {
    const versionEl = document.getElementById('appVersion');
    if (!versionEl) return;
    
    // Show loading state
    versionEl.textContent = '...';
    
    // Wait for service worker to be ready
    if ('serviceWorker' in navigator) {
        try {
            // Wait for service worker registration
            const registration = await navigator.serviceWorker.ready;
            
            // Give it a moment to initialize
            await new Promise(resolve => setTimeout(resolve, 500));
            
            // Try to get version
            if (navigator.serviceWorker.controller) {
                const messageChannel = new MessageChannel();
                
                messageChannel.port1.onmessage = (event) => {
                    if (event.data && event.data.version) {
                        versionEl.textContent = event.data.version.replace('v', '');
                        console.log('[PWA] Version loaded:', event.data.version);
                    } else {
                        versionEl.textContent = '2.3.3'; // Fallback
                    }
                };
                
                navigator.serviceWorker.controller.postMessage(
                    { type: 'GET_VERSION' },
                    [messageChannel.port2]
                );
                
                // Timeout after 3 seconds
                setTimeout(() => {
                    if (versionEl.textContent === '...') {
                        versionEl.textContent = '2.3.3'; // Fallback
                        console.warn('[PWA] Version fetch timeout - using fallback');
                    }
                }, 3000);
                
            } else {
                versionEl.textContent = '2.3.3'; // Fallback
                console.warn('[PWA] No service worker controller');
            }
            
        } catch (error) {
            versionEl.textContent = '2.3.3'; // Fallback
            console.error('[PWA] Error fetching version:', error);
        }
    } else {
        versionEl.textContent = '2.3.3'; // Fallback
        console.warn('[PWA] Service workers not supported');
    }
}

	
    if (textEditor) {
        textEditor.contentEditable = 'false';
        textEditor.style.display = 'none';
		textEditor.style.pointerEvents = 'none'; // ADDED: Block all mouse events
        textEditor.style.visibility = 'hidden';
        textEditor.blur();
    }
    
    // Focus on employee code input
    const empCodeInput = document.getElementById('empCode');
    if (empCodeInput) {
        empCodeInput.focus();
    }
    
    checkAndResetLeaveBalances();
    
    // Show PWA install button if available
    if (deferredPrompt && currentUser) {
        showInstallButton();
    }
	 // 🔄 Midnight reset code
    let lastResetDate = null;
    setInterval(async () => {
        const now = new Date();
        if (now.getHours() === 0 && now.getMinutes() === 0) {
            const today = now.toDateString();
            if (lastResetDate !== today) {
                if (currentUser && (currentUser.role === 'employee' || currentUser.role === 'admin')) {
                    await updateReportCounter(currentUser.empCode);
                    showNotification(`📅 New day started - counter reset for ${currentUser.empCode}`);
                    lastResetDate = today;
                }
            }
        }
    }, 60000); // Check every minute

});

	document.addEventListener('DOMContentLoaded', function() {
    // Initialize form listeners
    setTimeout(() => {
        initializeCheckboxListeners();
    }, 100);
    
    // Initialize text editor
    const textEditor = document.getElementById('textEditor');
    if (textEditor) {
        // Disable on page load
        textEditor.contentEditable = 'false';
        textEditor.style.display = 'none';
        textEditor.style.pointerEvents = 'none';
        textEditor.style.visibility = 'hidden';
        textEditor.style.position = 'absolute';
        textEditor.style.top = '-9999px';  
        
        textEditor.addEventListener('input', function() {
			updateWordCount();
			detectCriticalFindings();
			resetInactivityTimer();
			
			// Don't auto-save on every keystroke - only start the timer
			if (!autoSaveInterval && userAutoSavePreference > 0) {
				startAutoSave();
			}
		});
        
        textEditor.addEventListener('paste', function() {
            setTimeout(() => {
                updateWordCount();
                detectCriticalFindings();
                resetInactivityTimer(); 
            }, 10);
        });
        
        // STRICT: Prevent ANY focus when not logged in
        textEditor.addEventListener('focus', function(e) {
            const dashboard = document.getElementById('dashboard');
            if (!dashboard || dashboard.style.display !== 'block') {
                e.preventDefault();
                e.stopPropagation();
                this.blur();
                
                // Refocus on login input
                const empCodeInput = document.getElementById('empCode');
                if (empCodeInput) {
                    empCodeInput.focus();
                }
            } else {
                resetInactivityTimer();
            }
        });
        
        // Prevent ALL mouse events when disabled
        textEditor.addEventListener('mousedown', function(e) {
            if (this.contentEditable === 'false') {
                e.preventDefault();
                e.stopPropagation();
                return false;
            }
        });
        
        textEditor.addEventListener('click', function(e) {
            if (this.contentEditable === 'false') {
                e.preventDefault();
                e.stopPropagation();
                return false;
            }
        });
        
        // Save when user clicks outside editor (blur event)
        textEditor.addEventListener('blur', function() {
			const dashboard = document.getElementById('dashboard');
			if (dashboard && dashboard.style.display === 'block') {
				// ALWAYS save when leaving editor, regardless of auto-save setting
				saveDraft(true);
			}
		});
		
    } // ← CLOSE the if (textEditor) block HERE
    
    // Ensure login input is focused on page load
    setTimeout(() => {
        const empCodeInput = document.getElementById('empCode');
        if (empCodeInput && document.getElementById('loginPage').style.display !== 'none') {
            empCodeInput.focus();
        }
    }, 200);
    
    // Save draft when user switches tab (this can be outside the textEditor check)
    document.addEventListener('visibilitychange', function() {
        if (document.hidden && userAutoSavePreference > 0) {
            const dashboard = document.getElementById('dashboard');
            if (dashboard && dashboard.style.display === 'block') {
                saveDraft(true);
            }
        }
    });
});

	let allQAData = [];
	let filteredQAData = [];
	let displayedQACount = 5;
	
async function loadMonthlyQAChart(qaData) {
    const ctx = document.getElementById('monthlyQAChart');
    if (!ctx) return;
    
    if (monthlyQAChart) {
        monthlyQAChart.destroy();
    }
    
    // Only count QAs that have been graded
    const gradedQAs = qaData.filter(qa => qa.qaGrade && qa.gradedDate);
    
    // Group by month when grading was done
    const monthlyData = {};
    gradedQAs.forEach(qa => {
        const month = new Date(qa.gradedDate).toLocaleDateString('en-US', { year: 'numeric', month: 'short' });
        monthlyData[month] = (monthlyData[month] || 0) + 1;
    });
    
    // Get last 12 months
    const months = [];
    const counts = [];
    const now = new Date();
    
    for (let i = 11; i >= 0; i--) {
        const date = new Date(now.getFullYear(), now.getMonth() - i, 1);
        const monthKey = date.toLocaleDateString('en-US', { year: 'numeric', month: 'short' });
        months.push(monthKey);
        counts.push(monthlyData[monthKey] || 0);
    }
    
    monthlyQAChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: months,
            datasets: [{
                label: 'QAs Received (Graded)',
                data: counts,
                backgroundColor: '#3498db',
                borderColor: '#2980b9',
                borderWidth: 1
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
                y: {
                    beginAtZero: true,
                    ticks: { stepSize: 1 }
                }
            },
            plugins: { 
                legend: { display: false }
            }
        }
    });
}

function updateQAStatistics(qaData) {
    const gradeCounts = { '1': 0, '2': 0, '3': 0, '4': 0, '5': 0 };
    
    // Only count graded QAs
    qaData.forEach(qa => {
        if (qa.qaGrade && gradeCounts.hasOwnProperty(qa.qaGrade)) {
            gradeCounts[qa.qaGrade]++;
        }
    });
    
    const totalGraded = Object.values(gradeCounts).reduce((a, b) => a + b, 0);
    
    document.getElementById('totalQAReceived').textContent = totalGraded;
    document.getElementById('grade1Total').textContent = gradeCounts['1'];
    document.getElementById('grade2Total').textContent = gradeCounts['2'];
    document.getElementById('grade3Total').textContent = gradeCounts['3'];
    document.getElementById('grade4Total').textContent = gradeCounts['4'];
    document.getElementById('grade5Total').textContent = gradeCounts['5'];
}
	function populateRadiologistFilter() {
    const radFilter = document.getElementById('qaFilterRad');
    if (!radFilter) return;
    
    radFilter.innerHTML = '<option value="">All Radiologists</option>';
    
    Object.entries(authorizedEmployees).forEach(([code, emp]) => {
        if (emp.role === 'employee') {
            radFilter.innerHTML += `<option value="${code}">${emp.name} (${code})</option>`;
        }
    });
}
function applyQAFilters() {
    const fromDate = document.getElementById('qaFilterFrom').value;
    const toDate = document.getElementById('qaFilterTo').value;
    const radFilter = document.getElementById('qaFilterRad').value;
    const hospitalFilter = document.getElementById('qaFilterHospital').value;
    const gradeFilter = document.getElementById('qaFilterGrade').value;
    
    filteredQAData = allQAData.filter(qa => {
        if (fromDate && qa.qaReceivedDate && qa.qaReceivedDate < fromDate) return false;
        if (toDate && qa.qaReceivedDate && qa.qaReceivedDate > toDate) return false;
        if (radFilter && qa.assignedTo !== radFilter) return false;
        if (hospitalFilter && qa.hospitalName !== hospitalFilter) return false;
        if (gradeFilter && qa.qaGrade !== gradeFilter) return false;
        
        return true;
    });
    
    displayedQACount = 5;
    renderQATable();
}

function clearQAFilters() {
    document.getElementById('qaFilterFrom').value = '';
    document.getElementById('qaFilterTo').value = '';
    document.getElementById('qaFilterRad').value = '';
    document.getElementById('qaFilterHospital').value = '';
    document.getElementById('qaFilterGrade').value = '';
    
    // Clear table filters
    document.getElementById('filterRadName').value = '';
    document.getElementById('filterQAGrade').value = '';
    document.getElementById('filterQADetails').value = '';
    document.getElementById('filterQAReceived').value = '';
    document.getElementById('filterQAResponded').value = '';
    document.getElementById('filterHospital').value = '';
    document.getElementById('filterModality').value = '';
    document.getElementById('filterAccession').value = '';
    
    applyQAFilters();
}

function filterQATable() {
    const radNameFilter = document.getElementById('filterRadName').value.toLowerCase();
    const gradeFilter = document.getElementById('filterQAGrade').value;
    const detailsFilter = document.getElementById('filterQADetails').value.toLowerCase();
    const receivedFilter = document.getElementById('filterQAReceived').value;
    const respondedFilter = document.getElementById('filterQAResponded').value;
    const hospitalFilter = document.getElementById('filterHospital').value.toLowerCase();
    const modalityFilter = document.getElementById('filterModality').value;
    const accessionFilter = document.getElementById('filterAccession').value.toLowerCase();
    
    filteredQAData = allQAData.filter(qa => {
        const employee = authorizedEmployees[qa.assignedTo];
        const employeeName = employee ? employee.name.toLowerCase() : qa.assignedTo.toLowerCase();
        
        if (radNameFilter && !employeeName.includes(radNameFilter)) return false;
        if (gradeFilter) {
            if (gradeFilter === '-' && qa.qaGrade) return false;
            if (gradeFilter !== '-' && qa.qaGrade !== gradeFilter) return false;
        }
        if (detailsFilter && !qa.caseDetails.toLowerCase().includes(detailsFilter)) return false;
        if (receivedFilter && qa.qaReceivedDate !== receivedFilter) return false;
        if (respondedFilter && qa.qaRespondedDate !== respondedFilter) return false;
        if (hospitalFilter && (!qa.hospitalName || !qa.hospitalName.toLowerCase().includes(hospitalFilter))) return false;
        if (modalityFilter && qa.modality !== modalityFilter) return false;
        if (accessionFilter && (!qa.accessionNo || !qa.accessionNo.toLowerCase().includes(accessionFilter))) return false;
        
        return true;
    });
    
    displayedQACount = 5;
    renderQATable();
}

function renderQATable() {
    const tbody = document.getElementById('qaTableBody');
    const displayData = filteredQAData.slice(0, displayedQACount);
    
    document.getElementById('qaShowingCount').textContent = displayData.length;
    document.getElementById('qaTotalCount').textContent = filteredQAData.length;
    
    if (displayData.length === 0) {
        tbody.innerHTML = '<tr><td colspan="9" style="padding: 20px; text-align: center; color: #666;">No QA records found</td></tr>';
        document.getElementById('qaViewMoreBtn').style.display = 'none';
        return;
    }
    
    const html = displayData.map(qa => {
        const employee = authorizedEmployees[qa.assignedTo];
        const employeeName = employee ? employee.name : qa.assignedTo;
        
        let gradeDisplay = '-';
        let gradeStyle = '';
        
        if (qa.qaGrade) {
            const gradeColors = {
                '1': 'background: #27ae60; color: white;',
                '2': 'background: #f39c12; color: white;',
                '3': 'background: #9b59b6; color: white;',
                '4': 'background: #e67e22; color: white;',
                '5': 'background: #e74c3c; color: white;'
            };
            gradeDisplay = qa.qaGrade;
            gradeStyle = gradeColors[qa.qaGrade] || '';
        }
        
        return `
            <tr style="border-bottom: 1px solid #ecf0f1;">
				<td style="padding: 12px;">
					${employeeName}
					${qa.isProxy ? '<span style="background: #9b59b6; color: white; padding: 2px 6px; border-radius: 3px; font-size: 10px; margin-left: 5px;">PROXY</span>' : ''}
				</td>
                <td style="padding: 12px; text-align: center;">
                    <span style="display: inline-block; padding: 4px 8px; border-radius: 4px; font-weight: bold; ${gradeStyle}">${gradeDisplay}</span>
                </td>
                <td style="padding: 12px;">${qa.caseDetails || '-'}</td>
                <td style="padding: 12px; text-align: center;">${qa.qaReceivedDate || '-'}</td>
                <td style="padding: 12px; text-align: center;">${qa.qaRespondedDate || '-'}</td>
                <td style="padding: 12px; text-align: center;">${qa.hospitalName || '-'}</td>
                <td style="padding: 12px; text-align: center;">${qa.modality || '-'}</td>
                <td style="padding: 12px; text-align: center;">${qa.accessionNo || '-'}</td>
                <td style="padding: 12px; text-align: center;">
					<button onclick="viewQADetails('${qa.id}')" class="btn" style="background: #3498db; padding: 6px 12px; font-size: 11px; margin: 2px;">View</button>
					
					${(qa.isProxy === true || qa.entryType === 'PROXY_PENDING') && (qa.status === 'Pending' || qa.status === 'In Progress') ? 
						`<button onclick="openProxyQAModal('${qa.id}')" class="btn" style="background: #9b59b6; padding: 6px 12px; font-size: 11px; margin: 2px;">🔄 Proxy Entry</button>` : ''}
					
					${hasPermission('qa_edit') && (qa.status === 'Pending' || qa.status === 'In Progress') ? 
						`<button onclick="editQAAssignment('${qa.id}')" class="btn" style="background: #3498db; padding: 6px 12px; font-size: 11px; margin: 2px;">✏️ Edit</button>` : ''}
					
					${hasPermission('qa_delete') && qa.status === 'Pending' ? 
						`<button onclick="deleteQAAssignment('${qa.id}')" class="btn" style="background: #e74c3c; padding: 6px 12px; font-size: 11px; margin: 2px;">🗑️ Delete</button>` : ''}
					
					${qa.status === 'Completed' && !qa.qaGrade && hasPermission('qa_revert') ? 
						`<button onclick="revertQAToEmployee('${qa.id}')" class="btn" style="background: #f39c12; padding: 6px 12px; font-size: 11px; margin: 2px;">↩️ Revert</button>` : ''}
					
					${qa.status === 'Completed' && !qa.qaGrade ? 
						`<button onclick="gradeQA('${qa.id}')" class="btn" style="background: #e67e22; padding: 6px 12px; font-size: 11px; margin: 2px;">Grade</button>` : ''}
				</td>
            </tr>
        `;
    }).join('');
    
    tbody.innerHTML = html;
    
    // Show/hide View More button
    if (filteredQAData.length > displayedQACount) {
        document.getElementById('qaViewMoreBtn').style.display = 'inline-block';
    } else {
        document.getElementById('qaViewMoreBtn').style.display = 'none';
    }
}
		function loadMoreQA() {
    displayedQACount += 5;
    renderQATable();
}
async function saveQAGrade(qaId) {
    const grade = document.getElementById('qaGradeSelect').value;
    const feedback = document.getElementById('hrFeedbackText').value.trim();
    
    if (!grade) {
        alert('Please select a QA grade.');
        return;
    }
    
    try {
        await updateFirestoreDoc('qa_assignments', qaId, {
            qaGrade: grade,
            hrFeedback: feedback,
            gradedBy: currentUser.code || currentUser.username,
            gradedDate: new Date().toISOString()
        });
        
        showNotification('QA grade saved successfully!');
        closeModal();
        
        // Reload QA data to update chart and statistics
        loadHRQAData();
        
    } catch (error) {
        console.error('Error saving QA grade:', error);
        alert('Error saving grade. Please try again.');
    }
}
// Prevent default drag behavior for schedule system
document.addEventListener('dragover', function(e) {
    if (e.target.classList.contains('shift-cell')) {
        e.preventDefault();
    }
}, false);

document.addEventListener('drop', function(e) {
    if (e.target.classList.contains('shift-cell')) {
        e.preventDefault();
    }
}, false);


// ==============================================
// PASSWORD MANAGEMENT FUNCTIONS
// ==============================================
async function loadPasswordManagement() {
    console.log('[Password Management] Loading...');
    
    await loadSystemData();
    
    let passwordsSet = 0;
    let passwordsPending = 0;
    let accountsLocked = 0;
    
    // ✅ FIXED: Show ALL employees, not just role='employee'
    const employees = Object.entries(authorizedEmployees)
        .sort((a, b) => {
            // Sort: Locked first, then by name
            if (a[1].accountLocked && !b[1].accountLocked) return -1;
            if (!a[1].accountLocked && b[1].accountLocked) return 1;
            return a[1].name.localeCompare(b[1].name);
        });
    
    console.log(`[Password Management] Processing ${employees.length} employees`);
    
    // Count statistics (only count employees, not HR/Admin)
    employees.forEach(([code, emp]) => {
        if (emp.role === 'employee') {
            if (emp.passwordSet) passwordsSet++;
            else passwordsPending++;
            if (emp.accountLocked) accountsLocked++;
        }
    });
    
    console.log(`[Password Management] Stats - Set: ${passwordsSet}, Pending: ${passwordsPending}, Locked: ${accountsLocked}`);
    
    // Update statistics
    document.getElementById('passwordsSetCount').textContent = passwordsSet;
    document.getElementById('passwordsPendingCount').textContent = passwordsPending;
    document.getElementById('accountsLockedCount').textContent = accountsLocked;
    
    // Build list for ALL employees
    const listHTML = employees.map(([code, emp]) => {
        // Skip admin role from password management
        if (emp.role === 'admin') return '';
        
        const statusBadge = emp.passwordSet 
            ? '<span style="background: #27ae60; color: white; padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold;">✓ Password Set</span>'
            : '<span style="background: #e74c3c; color: white; padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold;">⚠ Pending</span>';
        
        const lockBadge = emp.accountLocked 
            ? '<span style="background: #e74c3c; color: white; padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold; margin-left: 5px;">🔒 LOCKED</span>'
            : '';
        
        const roleBadge = emp.role === 'hr' 
            ? '<span style="background: #3498db; color: white; padding: 4px 10px; border-radius: 12px; font-size: 11px; font-weight: bold; margin-left: 5px;">HR</span>'
            : '';
        
        const reminderInfo = emp.passwordReminderCount 
            ? `<div style="font-size: 11px; color: #666; margin-top: 3px;">Reminded ${emp.passwordReminderCount} time(s)</div>`
            : '';
        
        const lastSetInfo = emp.passwordSetDate 
            ? `<div style="font-size: 11px; color: #666; margin-top: 3px;">Set on: ${new Date(emp.passwordSetDate).toLocaleDateString()}</div>`
            : '';
        
        const lockReasonInfo = emp.accountLocked && emp.lockedReason
            ? `<div style="font-size: 11px; color: #e74c3c; margin-top: 3px; font-weight: 500;">Reason: ${emp.lockedReason}</div>`
            : '';
        
        const borderColor = emp.accountLocked ? '#e74c3c' : (emp.passwordSet ? '#27ae60' : '#f39c12');
        
        return `
            <div style="background: white; padding: 15px; border-radius: 8px; margin-bottom: 10px; border-left: 4px solid ${borderColor};">
                <div style="display: flex; justify-content: space-between; align-items: start;">
                    <div style="flex: 1;">
                        <div style="font-weight: bold; font-size: 15px; margin-bottom: 5px;">
                            ${emp.name} (${code})
                        </div>
                        <div style="font-size: 12px; color: #666;">
                            ${emp.specialty} | ${emp.department}
                        </div>
                        ${reminderInfo}
                        ${lastSetInfo}
                        ${lockReasonInfo}
                    </div>
                    <div style="text-align: right;">
                        <div style="margin-bottom: 10px;">
                            ${statusBadge}
                            ${lockBadge}
                            ${roleBadge}
                        </div>
                        <div style="display: flex; gap: 5px; flex-wrap: wrap; justify-content: flex-end;">
                            ${emp.accountLocked ? `
                                <button onclick="unlockAccount('${code}')" class="btn" style="background: #27ae60; padding: 6px 12px; font-size: 11px;">
                                    🔓 Unlock
                                </button>
                            ` : ''}
                            <button onclick="resetPasswordToDefault('${code}')" class="btn" style="background: #e67e22; padding: 6px 12px; font-size: 11px;">
                                🔄 Reset
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        `;
    }).join('');
    
    const container = document.getElementById('passwordManagementList');
    if (container) {
        container.innerHTML = listHTML || '<div style="text-align: center; padding: 20px; color: #666;">No employees found</div>';
    }
    
    console.log('[Password Management] Complete');
}
async function viewCredentialBackups() {
    try {
        const allBackups = await getFromFirestore('employee_credentials_backup');
        
        if (allBackups.length === 0) {
            alert('No backups found');
            return;
        }
        
        // Sort by timestamp (newest first)
        allBackups.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
        
        // Group by employee
        const backupsByEmployee = {};
        allBackups.forEach(backup => {
            if (!backupsByEmployee[backup.empCode]) {
                backupsByEmployee[backup.empCode] = [];
            }
            backupsByEmployee[backup.empCode].push(backup);
        });
        
        const backupsHTML = Object.entries(backupsByEmployee).map(([empCode, backups]) => {
            const employee = authorizedEmployees[empCode];
            const empName = employee ? employee.name : empCode;
            
            const backupListHTML = backups.slice(0, 10).map(backup => {
                const reasonColors = {
                    'reset': '#e67e22',
                    'unlock': '#27ae60',
                    'initial_setup': '#3498db',
                    'admin_edit': '#9b59b6',
                    'forced_change': '#e74c3c'
                };
                
                const reasonColor = reasonColors[backup.reason] || '#95a5a6';
                
                return `
                    <div style="background: white; padding: 12px; margin: 8px 0; border-radius: 5px; border-left: 3px solid ${reasonColor};">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <div style="flex: 1;">
                                <div style="font-size: 12px; color: #666;">
                                    ${new Date(backup.timestamp).toLocaleString()}
                                </div>
                                <div style="font-size: 13px; font-weight: 500; margin-top: 3px;">
                                    Reason: <span style="color: ${reasonColor}; font-weight: bold;">${backup.reason.toUpperCase()}</span>
                                </div>
								<div style="font-size: 11px; color: #999; margin-top: 2px;">
                                    By: ${backup.backupBy}
                                </div>
                            </div>
                            <div>
                                <button onclick="restoreEmployeeCredentials('${backup.id}')" class="btn" style="background: #27ae60; padding: 6px 12px; font-size: 11px;">
                                    🔄 Restore
                                </button>
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
            
            return `
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-bottom: 15px;">
                    <h4 style="margin: 0 0 10px 0; color: #2c3e50;">
                        ${empName} (${empCode})
                        <span style="background: #3498db; color: white; padding: 4px 10px; border-radius: 12px; font-size: 11px; margin-left: 10px;">
                            ${backups.length} backup${backups.length > 1 ? 's' : ''}
                        </span>
                    </h4>
                    <div style="max-height: 300px; overflow-y: auto;">
                        ${backupListHTML}
                    </div>
                    ${backups.length > 10 ? `<div style="text-align: center; padding: 10px; color: #666; font-size: 12px;">Showing 10 of ${backups.length} backups</div>` : ''}
                </div>
            `;
        }).join('');
        
        const modal = createModal(`
            <h2>🔒 Credential Backups</h2>
            
            <div style="background: #e3f2fd; padding: 15px; border-radius: 8px; margin: 20px 0;">
                <div style="font-size: 13px; color: #1976d2;">
                    <strong>Total Backups:</strong> ${allBackups.length}<br>
                    <strong>Employees with Backups:</strong> ${Object.keys(backupsByEmployee).length}
                </div>
            </div>
            
            <div style="max-height: 500px; overflow-y: auto; padding-right: 10px;">
                ${backupsHTML}
            </div>
            
            <div style="text-align: right; margin-top: 20px; padding-top: 15px; border-top: 2px solid #ecf0f1;">
                <button onclick="closeModal()" class="btn" style="background: #95a5a6;">Close</button>
            </div>
        `);
        
    } catch (error) {
        console.error('Error loading backups:', error);
        alert('Error loading backups: ' + error.message);
    }
}

function filterPasswordList() {
    // EXPLANATION: Search/filter employees by name or code
    
    const searchTerm = document.getElementById('passwordSearchInput').value.toLowerCase();
    const listItems = document.getElementById('passwordManagementList').children;
    
    Array.from(listItems).forEach(item => {
        const text = item.textContent.toLowerCase();
        item.style.display = text.includes(searchTerm) ? 'block' : 'none';
    });
}

async function resetPasswordToDefault(empCode) {

	if (currentUser.role !== 'admin' && currentUser.role !== 'hr') {
        console.warn('[SECURITY] Unauthorized password reset attempt by:', currentUser.code || currentUser.username, '(Role:', currentUser.role + ')');
        alert('⛔ ACCESS DENIED: Only admin and HR can reset passwords.');
        return;
    }
    const employee = authorizedEmployees[empCode];
    
    if (!employee) {
        alert('Employee not found');
        return;
    }
    
    // ✅ BACKUP BEFORE RESET
    await backupEmployeeCredentials(empCode, 'reset', employee);
    
    const defaultPassword = empCode + '123';
    const confirmMsg = `Reset password for ${employee.name} (${empCode})?\n\nNew password will be: ${defaultPassword}\n\nEmployee MUST change password after first login.`;
    
    if (!confirm(confirmMsg)) {
        return;
    }
    
    try {
        // ✅ USE TRANSACTION PATTERN A
        await db.runTransaction(async (transaction) => {
            const employeesRef = db.collection('system_data').doc('employees');
            const employeesDoc = await transaction.get(employeesRef);
            
            if (!employeesDoc.exists) {
                throw new Error('Employees document not found');
            }
            
            const allEmployees = employeesDoc.data().data;
            
            if (!allEmployees[empCode]) {
                throw new Error('Employee not found in database');
            }
            
            // Update only password fields
            allEmployees[empCode].password = defaultPassword;
            allEmployees[empCode].passwordSet = true;
            allEmployees[empCode].passwordSetDate = new Date().toISOString();
            allEmployees[empCode].failedLoginAttempts = 0;
            allEmployees[empCode].accountLocked = false;
            allEmployees[empCode].passwordResetBy = currentUser.code || currentUser.username;
            allEmployees[empCode].passwordResetDate = new Date().toISOString();
            allEmployees[empCode].mustChangePassword = true;
            
            transaction.update(employeesRef, {
                data: allEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: currentUser.code || currentUser.username
            });
        });
        
        // ✅ RELOAD FROM FIRESTORE
        await loadSystemData();
        
        alert(`✅ Password reset!\n\nEmployee: ${employee.name}\nPassword: ${defaultPassword}\n\n⚠️ Tell employee to login and SET NEW PASSWORD immediately.`);
        
        showNotification(`Password reset for ${employee.name}`);
        loadPasswordManagement();
        
    } catch (error) {
        console.error('Error resetting password:', error);
        alert('Error resetting password. Please try again.');
    }
}

async function unlockAccount(empCode) {

if (currentUser.role !== 'admin' && currentUser.role !== 'hr') {
        console.warn('[SECURITY] Unauthorized unlock attempt by:', currentUser.code || currentUser.username, '(Role:', currentUser.role + ')');
        alert('⛔ ACCESS DENIED: Only admini and HR can unlock accounts.');
        return;
    }
    const employee = authorizedEmployees[empCode];
    
    if (!employee) {
        alert('Employee not found');
        return;
    }
    
    if (!confirm(`Unlock account for ${employee.name} (${empCode})?`)) {
        return;
    }
    
    try {
        // ✅ BACKUP BEFORE UNLOCK
        await backupEmployeeCredentials(empCode, 'unlock', employee);
        
        // ✅ USE TRANSACTION PATTERN A
        await db.runTransaction(async (transaction) => {
            const employeesRef = db.collection('system_data').doc('employees');
            const employeesDoc = await transaction.get(employeesRef);
            
            if (!employeesDoc.exists) {
                throw new Error('Employees document not found');
            }
            
            const allEmployees = employeesDoc.data().data;
            
            if (!allEmployees[empCode]) {
                throw new Error('Employee not found in database');
            }
            
            // Reset lock and failed attempts
            allEmployees[empCode].accountLocked = false;
            allEmployees[empCode].failedLoginAttempts = 0;
            allEmployees[empCode].unlockedBy = currentUser.code || currentUser.username;
            allEmployees[empCode].unlockedDate = new Date().toISOString();
            
            transaction.update(employeesRef, {
                data: allEmployees,
                lastUpdated: new Date().toISOString(),
                updatedBy: currentUser.code || currentUser.username
            });
        });
        
        // ✅ RELOAD FROM FIRESTORE
        await loadSystemData();
        
        showNotification(`✅ Account unlocked for ${employee.name}`);
        loadPasswordManagement();
        
    } catch (error) {
        console.error('Error unlocking account:', error);
        alert('Error unlocking account. Please try again.');
    }
}
// ==============================================
// REPORT COUNT SELECTOR FUNCTIONS
// ==============================================

function initializeReportCountSelector() {
    const selector = document.getElementById('reportCountSelector');
    if (!selector) {
        console.error('[Count Selector] Element not found');
        return;
    }
    
    let html = '';
    for (let i = 1; i <= 10; i++) {
        html += `<option value="${i}">${i}</option>`;
    }
    selector.innerHTML = html;
    selector.value = '1';
    
    console.log('[Count Selector] ✅ Initialized');
}

async function autoSuggestReportCount() {
    const editor = document.getElementById('textEditor');
    const text = editor.textContent || editor.innerText || '';
    
    if (text.length < 20) return;
    
    const countSelector = document.getElementById('reportCountSelector');
    if (!countSelector) return;
    
    // if (!bodyPartRules || bodyPartRules.length === 0) {
	//     countSelector.value = '1';
	//     countSelector.style.border = '1px solid #ddd';
	//     return;
	// }

	// const bodyPartPhrase = parseReportHeading(text);
	// const matchingRule = findMatchingRule(bodyPartPhrase);

	// if (matchingRule) {
	//     countSelector.value = matchingRule.reportCount.toString();
	//     countSelector.style.border = '2px solid #27ae60';
	// } else {
	//     countSelector.value = '1';
	//     countSelector.style.border = '1px solid #ddd';
	// }

}

function debounce(func, wait) {
    let timeout;
    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), wait);
    };
}

</script>
</body>
</html>
