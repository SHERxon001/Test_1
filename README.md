<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Platformasi - Ijtimoiy</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Header */
        .header-bar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 60px;
            background: white;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 20px;
            z-index: 1000;
        }

        .logo {
            font-size: 1.5em;
            font-weight: bold;
            color: #667eea;
        }

        .header-right {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-id-display {
            background: #f0f0f0;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.85em;
            color: #666;
            font-family: monospace;
        }

        .menu-btn {
            width: 35px;
            height: 35px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            gap: 5px;
            cursor: pointer;
            padding: 5px;
            border-radius: 5px;
            transition: background 0.3s;
        }

        .menu-btn:hover {
            background: #f0f0f0;
        }

        .menu-btn span {
            display: block;
            width: 100%;
            height: 3px;
            background: #333;
            border-radius: 2px;
            transition: all 0.3s;
        }

        /* Side Panel */
        .side-panel {
            position: fixed;
            top: 0;
            right: -400px;
            width: 400px;
            max-width: 90%;
            height: 100vh;
            background: white;
            box-shadow: -5px 0 20px rgba(0,0,0,0.2);
            z-index: 2000;
            transition: right 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .side-panel.open {
            right: 0;
        }

        .panel-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.5);
            z-index: 1999;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
        }

        .panel-overlay.open {
            opacity: 1;
            visibility: visible;
        }

        .panel-header {
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .panel-header h2 {
            margin-bottom: 5px;
        }

        .panel-header p {
            opacity: 0.9;
            font-size: 0.9em;
        }

        .panel-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: white;
            font-size: 1.5em;
            cursor: pointer;
        }

        .panel-tabs {
            display: flex;
            border-bottom: 2px solid #f0f0f0;
        }

        .panel-tab {
            flex: 1;
            padding: 15px;
            background: none;
            border: none;
            cursor: pointer;
            font-weight: 600;
            color: #666;
            transition: all 0.3s;
            position: relative;
        }

        .panel-tab.active {
            color: #667eea;
        }

        .panel-tab.active::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            right: 0;
            height: 2px;
            background: #667eea;
        }

        .panel-content {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Search Section */
        .search-box {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .search-box input {
            flex: 1;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
        }

        .user-card {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .user-info-small h4 {
            color: #333;
            margin-bottom: 3px;
        }

        .user-info-small p {
            color: #666;
            font-size: 0.85em;
            font-family: monospace;
        }

        /* Friends List */
        .friend-item {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .friend-status {
            display: inline-block;
            width: 8px;
            height: 8px;
            background: #4caf50;
            border-radius: 50%;
            margin-left: 5px;
        }

        .friend-status.offline {
            background: #999;
        }

        /* Groups Section */
        .group-card {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
        }

        .group-card:hover {
            border-color: #667eea;
            transform: translateX(5px);
        }

        .group-card h4 {
            color: #333;
            margin-bottom: 5px;
        }

        .group-card p {
            color: #666;
            font-size: 0.9em;
        }

        .group-card .member-count {
            display: inline-block;
            background: #667eea;
            color: white;
            padding: 2px 8px;
            border-radius: 10px;
            font-size: 0.8em;
            margin-top: 5px;
        }

        .create-group-btn {
            width: 100%;
            padding: 15px;
            background: #e3f2fd;
            border: 2px dashed #667eea;
            border-radius: 10px;
            color: #667eea;
            font-weight: 600;
            cursor: pointer;
            margin-bottom: 20px;
            transition: all 0.3s;
        }

        .create-group-btn:hover {
            background: #667eea;
            color: white;
        }

        /* Modal */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.5);
            z-index: 3000;
            display: none;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .modal.open {
            display: flex;
        }

        .modal-content {
            background: white;
            border-radius: 15px;
            padding: 30px;
            max-width: 500px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            animation: slideUp 0.3s ease;
        }

        @keyframes slideUp {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 1.5em;
            cursor: pointer;
            color: #666;
        }

        /* Main Container */
        .main-container {
            margin-top: 80px;
            padding: 20px;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }

        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            padding: 40px;
            position: relative;
        }

        /* Auth Screen */
        .auth-screen {
            text-align: center;
            max-width: 400px;
            margin: 0 auto;
        }

        .auth-screen h1 {
            color: #333;
            margin-bottom: 10px;
        }

        .auth-screen p {
            color: #666;
            margin-bottom: 30px;
        }

        .form-group {
            margin-bottom: 20px;
            text-align: left;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 10px;
            font-size: 1em;
            transition: all 0.3s;
        }

        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .btn {
            padding: 15px 40px;
            border: none;
            border-radius: 25px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #f0f0f0;
            color: #666;
        }

        .btn-success {
            background: #4caf50;
            color: white;
        }

        .btn-danger {
            background: #f44336;
            color: white;
        }

        .btn-small {
            padding: 8px 15px;
            font-size: 0.9em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        /* Group Room */
        .group-room {
            background: white;
            border-radius: 20px;
            padding: 30px;
            margin-top: 20px;
        }

        .group-members {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .member-badge {
            background: #e3f2fd;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9em;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .member-badge.ready {
            background: #e8f5e9;
            border: 2px solid #4caf50;
        }

        .member-score {
            background: #667eea;
            color: white;
            padding: 2px 8px;
            border-radius: 10px;
            font-size: 0.8em;
        }

        .live-scores {
            position: fixed;
            right: 20px;
            top: 80px;
            width: 250px;
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.2);
            z-index: 100;
        }

        .live-score-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #f0f0f0;
        }

        .live-score-item:last-child {
            border-bottom: none;
        }

        .score-bar {
            width: 100%;
            height: 6px;
            background: #f0f0f0;
            border-radius: 3px;
            margin-top: 5px;
            overflow: hidden;
        }

        .score-bar-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            border-radius: 3px;
            transition: width 0.5s ease;
        }

        /* Quiz Styles */
        .progress-container {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 10px;
            margin-bottom: 20px;
            overflow: hidden;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            border-radius: 10px;
            transition: width 0.5s ease;
        }

        .timer-display {
            text-align: center;
            margin-bottom: 25px;
        }

        .timer-circle {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: conic-gradient(#667eea var(--progress), #e0e0e0 var(--progress));
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto;
            position: relative;
        }

        .timer-circle::before {
            content: '';
            position: absolute;
            width: 80px;
            height: 80px;
            background: white;
            border-radius: 50%;
        }

        .timer-text {
            position: relative;
            z-index: 1;
            font-size: 1.5em;
            font-weight: bold;
            color: #333;
        }

        .question {
            font-size: 1.2em;
            color: #333;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .option {
            background: #f8f9fa;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            padding: 15px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .option:hover:not(.disabled) {
            border-color: #667eea;
            background: #e3f2fd;
        }

        .option.correct {
            background: #4caf50;
            color: white;
            border-color: #4caf50;
        }

        .option.wrong {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .option.disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }

        .hidden {
            display: none !important;
        }

        @media (max-width: 768px) {
            .live-scores {
                position: static;
                width: 100%;
                margin-bottom: 20px;
            }
            
            .side-panel {
                width: 100%;
                right: -100%;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <div class="header-bar" id="headerBar" style="display: none;">
        <div class="logo">🎯 Test Platform</div>
        <div class="header-right">
            <span class="user-id-display" id="userIdDisplay">ID: -------</span>
            <div class="menu-btn" onclick="toggleSidePanel()">
                <span></span>
                <span></span>
                <span></span>
            </div>
        </div>
    </div>

    <!-- Side Panel -->
    <div class="panel-overlay" id="panelOverlay" onclick="toggleSidePanel()"></div>
    <div class="side-panel" id="sidePanel">
        <div class="panel-header">
            <div>
                <h2 id="panelUserName">Foydalanuvchi</h2>
                <p id="panelUserId">ID: -------</p>
            </div>
            <button class="panel-close" onclick="toggleSidePanel()">×</button>
        </div>
        
        <div class="panel-tabs">
            <button class="panel-tab active" onclick="switchTab('friends')">👥 Do'stlar</button>
            <button class="panel-tab" onclick="switchTab('groups')">👥 Guruhlar</button>
            <button class="panel-tab" onclick="switchTab('search')">🔍 Qidirish</button>
        </div>
        
        <div class="panel-content">
            <!-- Friends Tab -->
            <div class="tab-content active" id="friendsTab">
                <h3 style="margin-bottom: 15px;">Mening do'stlarim</h3>
                <div id="friendsList">
                    <p style="color: #999; text-align: center; padding: 20px;">Hali do'stlar yo'q</p>
                </div>
            </div>
            
            <!-- Groups Tab -->
            <div class="tab-content" id="groupsTab">
                <button class="create-group-btn" onclick="openCreateGroupModal()">
                    + Yangi guruh yaratish
                </button>
                <h3 style="margin-bottom: 15px;">Mening guruhlarim</h3>
                <div id="groupsList">
                    <p style="color: #999; text-align: center; padding: 20px;">Hali guruh yo'q</p>
                </div>
            </div>
            
            <!-- Search Tab -->
            <div class="tab-content" id="searchTab">
                <div class="search-box">
                    <input type="text" id="searchInput" placeholder="ID raqamini kiriting...">
                    <button class="btn btn-primary" onclick="searchUser()" style="padding: 12px 20px;">Qidirish</button>
                </div>
                <div id="searchResults"></div>
            </div>
        </div>
    </div>

    <!-- Create Group Modal -->
    <div class="modal" id="createGroupModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Yangi guruh yaratish</h2>
                <button class="modal-close" onclick="closeModal('createGroupModal')">×</button>
            </div>
            <div class="form-group">
                <label>Guruh nomi:</label>
                <input type="text" id="groupName" placeholder="Guruh nomini kiriting...">
            </div>
            <div class="form-group">
                <label>Test tanlang:</label>
                <select id="groupTestSelect">
                    <option value="">Test tanlang...</option>
                </select>
            </div>
            <button class="btn btn-primary" onclick="createGroup()" style="width: 100%;">Guruh yaratish</button>
        </div>
    </div>

    <!-- Invite Friend Modal -->
    <div class="modal" id="inviteModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Do'stni taklif qilish</h2>
                <button class="modal-close" onclick="closeModal('inviteModal')">×</button>
            </div>
            <p style="margin-bottom: 15px;">Do'stingizga ushbu ID raqamini yuboring:</p>
            <div class="form-group">
                <input type="text" id="inviteCode" readonly style="text-align: center; font-size: 1.2em; font-family: monospace;">
            </div>
            <button class="btn btn-primary" onclick="copyInviteCode()" style="width: 100%;">Nusxa olish</button>
        </div>
    </div>

    <!-- Main Content -->
    <div class="main-container">
        <!-- Auth Screen -->
        <div class="container auth-screen" id="authScreen">
            <h1>🎯 Test Platformasi</h1>
            <p>Ijtimoiy test platformasiga xush kelibsiz!</p>
            
            <div class="form-group">
                <label>Ismingiz:</label>
                <input type="text" id="userName" placeholder="Ismingizni kiriting">
            </div>
            
            <div class="form-group">
                <label>Telefon raqamingiz:</label>
                <input type="tel" id="userPhone" placeholder="+998 90 123 45 67">
            </div>
            
            <button class="btn btn-primary" onclick="register()">Ro'yxatdan o'tish</button>
        </div>

        <!-- Home Screen -->
        <div class="container hidden" id="homeScreen">
            <div style="text-align: center; margin-bottom: 30px;">
                <h1>Asosiy Menyu</h1>
                <p style="color: #666;">Xush kelibsiz, <span id="welcomeName"></span>!</p>
            </div>

            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 30px;">
                <div style="background: #f8f9fa; padding: 30px; border-radius: 15px; text-align: center; cursor: pointer;" onclick="openCreator()">
                    <div style="font-size: 3em; margin-bottom: 10px;">✏️</div>
                    <h3>Test Yaratish</h3>
                </div>
                <div style="background: #f8f9fa; padding: 30px; border-radius: 15px; text-align: center; cursor: pointer;" onclick="openSavedTests()">
                    <div style="font-size: 3em; margin-bottom: 10px;">📚</div>
                    <h3>Saqlangan Testlar</h3>
                </div>
            </div>

            <button class="btn btn-secondary" onclick="openInviteModal()" style="width: 100%; margin-bottom: 10px;">
                👤 Do'stni taklif qilish
            </button>
            <button class="btn btn-primary" onclick="toggleSidePanel()" style="width: 100%;">
                👥 Guruhga qo'shilish
            </button>

            <div id="savedTestsSection" style="display: none; margin-top: 30px;">
                <h3 style="margin-bottom: 15px;">Saqlangan Testlar:</h3>
                <div id="savedTestsList"></div>
            </div>
        </div>

        <!-- Group Room -->
        <div class="group-room hidden" id="groupRoom">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                <div>
                    <h2 id="groupRoomName">Guruh nomi</h2>
                    <p style="color: #666;">Guruh ID: <span id="groupRoomId"></span></p>
                </div>
                <button class="btn btn-danger" onclick="leaveGroup()">Chiqish</button>
            </div>
            
            <div class="group-members" id="groupMembers"></div>
            
            <div style="text-align: center; margin: 30px 0;">
                <button class="btn btn-success" id="startGroupTestBtn" onclick="startGroupTest()" style="font-size: 1.2em; padding: 15px 40px;">
                    Testni boshlash
                </button>
                <p id="waitingText" style="color: #666; margin-top: 10px;">Boshqa a'zolar kutilmoqda...</p>
            </div>
        </div>

        <!-- Quiz Screen -->
        <div class="container hidden" id="quizScreen">
            <div class="live-scores hidden" id="liveScores">
                <h4 style="margin-bottom: 15px;">📊 Jonli natijalar</h4>
                <div id="liveScoresList"></div>
            </div>

            <div class="progress-container">
                <div class="progress-bar" id="progressBar"></div>
            </div>
            
            <div class="timer-display">
                <div class="timer-circle" id="timerCircle" style="--progress: 100%;">
                    <div class="timer-text" id="timerText">30</div>
                </div>
            </div>
            
            <div class="question">
                <span id="questionNumber">1.</span>
                <span id="questionText">Savol matni...</span>
            </div>
            
            <div class="options" id="optionsContainer"></div>
            <div id="feedbackContainer"></div>
            
            <div style="display: flex; justify-content: space-between; margin-top: 20px;">
                <button class="btn btn-secondary" id="prevBtn" onclick="previousQuestion()">Oldingi</button>
                <button class="btn btn-primary" id="nextBtn" onclick="nextQuestion()" disabled>Keyingi</button>
            </div>
        </div>

        <!-- Result Screen -->
        <div class="container hidden" id="resultScreen" style="text-align: center;">
            <div style="font-size: 4em; margin-bottom: 20px;">🏆</div>
            <h1>Test yakunlandi!</h1>
            <div style="font-size: 3em; font-weight: bold; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin: 20px 0;" id="scoreDisplay">0/0</div>
            
            <div id="groupResults" style="margin: 20px 0; display: none;">
                <h3>Guruh natijalari:</h3>
                <div id="groupResultsList"></div>
            </div>
            
            <button class="btn btn-primary" onclick="goHome()">Bosh menyu</button>
        </div>
    </div>

    <script>
        // Global Variables
        let currentUser = null;
        let currentUserId = null;
        let createdQuestions = [];
        let currentQuestions = [];
        let currentQuestion = 0;
        let userAnswers = [];
        let answerStatus = [];
        let timePerQuestion = 30;
        let currentTimer = null;
        let timeLeft = 0;
        let hasAnswered = false;
        let tempOptions = [];
        let tempCorrectAnswer = -1;
        let currentGroup = null;
        let isGroupMode = false;
        let groupScores = {};

        // Initialize
        window.onload = function() {
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                currentUserId = currentUser.id;
                showMainInterface();
            }
        };

        // Generate 7-digit ID
        function generateUserId() {
            return Math.floor(1000000 + Math.random() * 9000000).toString();
        }

        function register() {
            const name = document.getElementById('userName').value.trim();
            const phone = document.getElementById('userPhone').value.trim();
            
            if (!name || !phone) {
                alert('Barcha maydonlarni to\'ldiring!');
                return;
            }
            
            currentUserId = generateUserId();
            currentUser = {
                id: currentUserId,
                name: name,
                phone: phone,
                friends: [],
                groups: []
            };
            
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
            localStorage.setItem('user_' + currentUserId, JSON.stringify(currentUser));
            
            showMainInterface();
        }

        function showMainInterface() {
            document.getElementById('authScreen').classList.add('hidden');
            document.getElementById('headerBar').style.display = 'flex';
            document.getElementById('homeScreen').classList.remove('hidden');
            document.getElementById('userIdDisplay').textContent = 'ID: ' + currentUserId;
            document.getElementById('panelUserName').textContent = currentUser.name;
            document.getElementById('panelUserId').textContent = 'ID: ' + currentUserId;
            document.getElementById('welcomeName').textContent = currentUser.name;
            
            loadFriends();
            loadGroups();
            updateTestSelect();
        }

        // Side Panel Functions
        function toggleSidePanel() {
            document.getElementById('sidePanel').classList.toggle('open');
            document.getElementById('panelOverlay').classList.toggle('open');
        }

        function switchTab(tab) {
            document.querySelectorAll('.panel-tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(tab + 'Tab').classList.add('active');
        }

        // Friend Functions
        function searchUser() {
            const searchId = document.getElementById('searchInput').value.trim();
            if (!searchId || searchId.length !== 7) {
                alert('7 xonali ID kiriting!');
                return;
            }
            
            if (searchId === currentUserId) {
                alert('O\'zingizni qidiryapsiz!');
                return;
            }
            
            const userData = localStorage.getItem('user_' + searchId);
            if (!userData) {
                alert('Foydalanuvchi topilmadi!');
                return;
            }
            
            const user = JSON.parse(userData);
            const resultsDiv = document.getElementById('searchResults');
            
            const isFriend = currentUser.friends.includes(searchId);
            
            resultsDiv.innerHTML = `
                <div class="user-card">
                    <div class="user-info-small">
                        <h4>${user.name}</h4>
                        <p>ID: ${user.id}</p>
                    </div>
                    ${isFriend ? 
                        '<span style="color: #4caf50;">✓ Do\'st</span>' : 
                        `<button class="btn btn-success btn-small" onclick="addFriend('${user.id}')">Do'st qo'shish</button>`
                    }
                </div>
            `;
        }

        function addFriend(friendId) {
            if (!currentUser.friends.includes(friendId)) {
                currentUser.friends.push(friendId);
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                localStorage.setItem('user_' + currentUserId, JSON.stringify(currentUser));
                
                // Add to friend's list too
                const friendData = JSON.parse(localStorage.getItem('user_' + friendId));
                if (friendData && !friendData.friends.includes(currentUserId)) {
                    friendData.friends.push(currentUserId);
                    localStorage.setItem('user_' + friendId, JSON.stringify(friendData));
                }
                
                alert('Do\'st qo\'shildi!');
                searchUser();
                loadFriends();
            }
        }

        function loadFriends() {
            const list = document.getElementById('friendsList');
            if (!currentUser.friends || currentUser.friends.length === 0) {
                list.innerHTML = '<p style="color: #999; text-align: center;">Hali do\'stlarsiz</p>';
                return;
            }
            
            list.innerHTML = '';
            currentUser.friends.forEach(friendId => {
                const friendData = localStorage.getItem('user_' + friendId);
                if (friendData) {
                    const friend = JSON.parse(friendData);
                    list.innerHTML += `
                        <div class="friend-item">
                            <div>
                                <strong>${friend.name}</strong>
                                <span class="friend-status"></span>
                                <div style="font-size: 0.85em; color: #666;">ID: ${friend.id}</div>
                            </div>
                            <button class="btn btn-primary btn-small" onclick="inviteToGroup('${friend.id}')">Guruhga taklif</button>
                        </div>
                    `;
                }
            });
        }

        // Group Functions
        function openCreateGroupModal() {
            document.getElementById('createGroupModal').classList.add('open');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('open');
        }

        function updateTestSelect() {
            const select = document.getElementById('groupTestSelect');
            const tests = JSON.parse(localStorage.getItem('savedTests') || '[]');
            
            select.innerHTML = '<option value="">Test tanlang...</option>';
            tests.forEach(test => {
                select.innerHTML += `<option value="${test.id}">${test.name}</option>`;
            });
        }

        function createGroup() {
            const name = document.getElementById('groupName').value.trim();
            const testId = document.getElementById('groupTestSelect').value;
            
            if (!name || !testId) {
                alert('Barcha maydonlarni to\'ldiring!');
                return;
            }
            
            const groupId = Date.now().toString();
            const group = {
                id: groupId,
                name: name,
                testId: testId,
                creator: currentUserId,
                members: [currentUserId],
                status: 'waiting'
            };
            
            if (!currentUser.groups) currentUser.groups = [];
            currentUser.groups.push(groupId);
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
            localStorage.setItem('user_' + currentUserId, JSON.stringify(currentUser));
            localStorage.setItem('group_' + groupId, JSON.stringify(group));
            
            closeModal('createGroupModal');
            loadGroups();
            joinGroupRoom(groupId);
        }

        function loadGroups() {
            const list = document.getElementById('groupsList');
            if (!currentUser.groups || currentUser.groups.length === 0) {
                list.innerHTML = '<p style="color: #999; text-align: center;">Hali guruh yo\'q</p>';
                return;
            }
            
            list.innerHTML = '';
            currentUser.groups.forEach(groupId => {
                const groupData = localStorage.getItem('group_' + groupId);
                if (groupData) {
                    const group = JSON.parse(groupData);
                    list.innerHTML += `
                        <div class="group-card" onclick="joinGroupRoom('${group.id}')">
                            <h4>${group.name}</h4>
                            <p>Test ID: ${group.testId}</p>
                            <span class="member-count">${group.members.length} a'zo</span>
                        </div>
                    `;
                }
            });
        }

        function joinGroupRoom(groupId) {
            const groupData = localStorage.getItem('group_' + groupId);
            if (!groupData) return;
            
            currentGroup = JSON.parse(groupData);
            
            // Add member if not already
            if (!currentGroup.members.includes(currentUserId)) {
                currentGroup.members.push(currentUserId);
                localStorage.setItem('group_' + groupId, JSON.stringify(currentGroup));
            }
            
            document.getElementById('homeScreen').classList.add('hidden');
            document.getElementById('groupRoom').classList.remove('hidden');
            document.getElementById('groupRoomName').textContent = currentGroup.name;
            document.getElementById('groupRoomId').textContent = groupId;
            
            updateGroupMembers();
            
            // Check if creator
            if (currentGroup.creator === currentUserId) {
                document.getElementById('startGroupTestBtn').style.display = 'inline-block';
                document.getElementById('waitingText').style.display = 'none';
            } else {
                document.getElementById('startGroupTestBtn').style.display = 'none';
                document.getElementById('waitingText').textContent = 'Guruh rahbari testni boshlashini kutilmoqda...';
            }
            
            // Simulate real-time updates
            startGroupSync();
        }

        function updateGroupMembers() {
            const container = document.getElementById('groupMembers');
            container.innerHTML = '';
            
            currentGroup.members.forEach(memberId => {
                const memberData = localStorage.getItem('user_' + memberId);
                if (memberData) {
                    const member = JSON.parse(memberData);
                    const isReady = groupScores[memberId] !== undefined;
                    container.innerHTML += `
                        <div class="member-badge ${isReady ? 'ready' : ''}">
                            ${member.name} ${memberId === currentGroup.creator ? '👑' : ''}
                            ${isReady ? '<span class="member-score">' + groupScores[memberId] + '</span>' : ''}
                        </div>
                    `;
                }
            });
        }

        function startGroupSync() {
            // Simulate real-time sync
            setInterval(() => {
                if (currentGroup) {
                    const updated = localStorage.getItem('group_' + currentGroup.id);
                    if (updated) {
                        currentGroup = JSON.parse(updated);
                        updateGroupMembers();
                    }
                }
            }, 2000);
        }

        function startGroupTest() {
            const testData = localStorage.getItem('savedTests');
            if (!testData) return;
            
            const tests = JSON.parse(testData);
            const test = tests.find(t => t.id == currentGroup.testId);
            
            if (test) {
                isGroupMode = true;
                currentQuestions = test.questions;
                timePerQuestion = 30; // Default for groups
                
                document.getElementById('groupRoom').classList.add('hidden');
                document.getElementById('liveScores').classList.remove('hidden');
                startQuiz();
            }
        }

        function leaveGroup() {
            if (confirm('Guruhdan chiqishni xohlaysizmi?')) {
                currentGroup = null;
                document.getElementById('groupRoom').classList.add('hidden');
                document.getElementById('homeScreen').classList.remove('hidden');
            }
        }

        // Invite Functions
        function openInviteModal() {
            document.getElementById('inviteCode').value = currentUserId;
            document.getElementById('inviteModal').classList.add('open');
        }

        function copyInviteCode() {
            const code = document.getElementById('inviteCode');
            code.select();
            document.execCommand('copy');
            alert('ID nusxalandi: ' + code.value);
        }

        function inviteToGroup(friendId) {
            if (!currentGroup) {
                alert('Avval guruh yaratishingiz kerak!');
                return;
            }
            alert('Do\'stingizga guruh ID sini yuboring: ' + currentGroup.id);
        }

        // Test Creator Functions (simplified)
        function openCreator() {
            alert('Test yaratish funksiyasi (avvalgi versiyadan)');
        }

        function openSavedTests() {
            document.getElementById('savedTestsSection').style.display = 'block';
            const tests = JSON.parse(localStorage.getItem('savedTests') || '[]');
            const list = document.getElementById('savedTestsList');
            
            if (tests.length === 0) {
                list.innerHTML = '<p style="color: #999;">Test yo\'q</p>';
                return;
            }
            
            list.innerHTML = '';
            tests.forEach(test => {
                list.innerHTML += `
                    <div style="background: #f8f9fa; padding: 15px; border-radius: 10px; margin-bottom: 10px;">
                        <h4>${test.name}</h4>
                        <p>${test.questions.length} ta savol</p>
                    </div>
                `;
            });
        }

        // Quiz Functions
        function startQuiz() {
            currentQuestion = 0;
            userAnswers = new Array(currentQuestions.length).fill(null);
            answerStatus = new Array(currentQuestions.length).fill(null);
            
            document.getElementById('quizScreen').classList.remove('hidden');
            showQuestion();
        }

        function showQuestion() {
            hasAnswered = false;
            const q = currentQuestions[currentQuestion];
            
            document.getElementById('progressBar').style.width = ((currentQuestion + 1) / currentQuestions.length * 100) + '%';
            document.getElementById('questionNumber').textContent = (currentQuestion + 1) + '.';
            document.getElementById('questionText').textContent = q.question;
            document.getElementById('feedbackContainer').innerHTML = '';
            
            const container = document.getElementById('optionsContainer');
            container.innerHTML = '';
            
            const letters = 'ABCDEFGHIJ';
            q.options.forEach((opt, idx) => {
                const div = document.createElement('div');
                div.className = 'option';
                div.innerHTML = `<div class="option-letter">${letters[idx]}</div>${opt}<div class="option-icon"></div>`;
                div.onclick = () => selectOption(idx);
                container.appendChild(div);
            });
            
            document.getElementById('prevBtn').disabled = currentQuestion === 0;
            document.getElementById('nextBtn').disabled = true;
            
            startTimer(timePerQuestion);
            
            if (isGroupMode) {
                updateLiveScores();
            }
        }

        function startTimer(seconds) {
            timeLeft = seconds;
            updateTimerDisplay();
            
            if (currentTimer) clearInterval(currentTimer);
            currentTimer = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                if (timeLeft <= 0) {
                    clearInterval(currentTimer);
                    handleTimeUp();
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            document.getElementById('timerText').textContent = timeLeft;
            const pct = (timeLeft / timePerQuestion) * 100;
            document.getElementById('timerCircle').style.setProperty('--progress', pct + '%');
        }

        function handleTimeUp() {
            if (hasAnswered) return;
            hasAnswered = true;
            answerStatus[currentQuestion] = 'timeout';
            showCorrectAnswer();
        }

        function selectOption(idx) {
            if (hasAnswered) return;
            hasAnswered = true;
            clearInterval(currentTimer);
            
            const q = currentQuestions[currentQuestion];
            const isCorrect = idx === q.correct;
            answerStatus[currentQuestion] = isCorrect ? 'correct' : 'wrong';
            
            const options = document.querySelectorAll('.option');
            options.forEach((opt, i) => {
                opt.classList.add('disabled');
                opt.onclick = null;
                if (i === idx) {
                    opt.classList.add(isCorrect ? 'correct' : 'wrong');
                    opt.querySelector('.option-icon').textContent = isCorrect ? '✓' : '✗';
                } else if (i === q.correct && !isCorrect) {
                    opt.classList.add('correct');
                    opt.querySelector('.option-icon').textContent = '✓';
                }
            });
            
            const fb = document.createElement('div');
            fb.className = 'feedback-message ' + (isCorrect ? 'feedback-correct' : 'feedback-wrong');
            fb.textContent = isCorrect ? 'To\'g\'ri! 🎉' : 'Noto\'g\'ri!';
            document.getElementById('feedbackContainer').appendChild(fb);
            
            document.getElementById('nextBtn').disabled = false;
            
            if (isGroupMode) {
                updateLiveScores();
            }
        }

        function showCorrectAnswer() {
            const q = currentQuestions[currentQuestion];
            const options = document.querySelectorAll('.option');
            options.forEach((opt, i) => {
                opt.classList.add('disabled');
                if (i === q.correct) {
                    opt.classList.add('correct');
                    opt.querySelector('.option-icon').textContent = '✓';
                }
            });
            document.getElementById('nextBtn').disabled = false;
        }

        function nextQuestion() {
            if (currentTimer) clearInterval(currentTimer);
            if (currentQuestion < currentQuestions.length - 1) {
                currentQuestion++;
                showQuestion();
            } else {
                finishQuiz();
            }
        }

        function previousQuestion() {
            if (currentTimer) clearInterval(currentTimer);
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion();
            }
        }

        function updateLiveScores() {
            if (!isGroupMode) return;
            
            // Calculate current score
            let score = answerStatus.filter(s => s === 'correct').length;
            groupScores[currentUserId] = score;
            
            // Save to localStorage for others to see
            if (currentGroup) {
                const groupScoresKey = 'groupScores_' + currentGroup.id;
                const allScores = JSON.parse(localStorage.getItem(groupScoresKey) || '{}');
                allScores[currentUserId] = {
                    name: currentUser.name,
                    score: score,
                    total: currentQuestions.length,
                    answered: currentQuestion + 1
                };
                localStorage.setItem(groupScoresKey, JSON.stringify(allScores));
                
                // Display
                const list = document.getElementById('liveScoresList');
                list.innerHTML = '';
                
                // Get all members' scores
                currentGroup.members.forEach(memberId => {
                    const memberData = localStorage.getItem('user_' + memberId);
                    const memberScores = allScores[memberId];
                    
                    if (memberData) {
                        const member = JSON.parse(memberData);
                        const displayScore = memberScores ? memberScores.score : 0;
                        const percent = (displayScore / currentQuestions.length) * 100;
                        
                        list.innerHTML += `
                            <div class="live-score-item">
                                <div>
                                    <strong>${member.name} ${memberId === currentUserId ? '(Siz)' : ''}</strong>
                                    <div class="score-bar">
                                        <div class="score-bar-fill" style="width: ${percent}%"></div>
                                    </div>
                                </div>
                                <span>${displayScore}/${currentQuestions.length}</span>
                            </div>
                        `;
                    }
                });
            }
        }

        function finishQuiz() {
            if (currentTimer) clearInterval(currentTimer);
            
            let correct = answerStatus.filter(s => s === 'correct').length;
            
            document.getElementById('quizScreen').classList.add('hidden');
            document.getElementById('resultScreen').classList.remove('hidden');
            document.getElementById('scoreDisplay').textContent = correct + '/' + currentQuestions.length;
            
            if (isGroupMode && currentGroup) {
                document.getElementById('groupResults').style.display = 'block';
                showGroupResults();
            }
        }

        function showGroupResults() {
            const groupScoresKey = 'groupScores_' + currentGroup.id;
            const allScores = JSON.parse(localStorage.getItem(groupScoresKey) || '{}');
            
            // Sort by score
            const sorted = Object.entries(allScores).sort((a, b) => b[1].score - a[1].score);
            
            const list = document.getElementById('groupResultsList');
            list.innerHTML = '';
            
            sorted.forEach(([userId, data], index) => {
                const medal = index === 0 ? '🥇' : index === 1 ? '🥈' : index === 2 ? '🥉' : '•';
                list.innerHTML += `
                    <div style="background: #f8f9fa; padding: 15px; border-radius: 10px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center;">
                        <div>
                            <span style="font-size: 1.5em; margin-right: 10px;">${medal}</span>
                            <strong>${data.name}</strong>
                        </div>
                        <span style="font-size: 1.2em; font-weight: bold; color: #667eea;">${data.score}/${data.total}</span>
                    </div>
                `;
            });
        }

        function goHome() {
            if (currentTimer) clearInterval(currentTimer);
            isGroupMode = false;
            currentGroup = null;
            document.getElementById('resultScreen').classList.add('hidden');
            document.getElementById('quizScreen').classList.add('hidden');
            document.getElementById('groupRoom').classList.add('hidden');
            document.getElementById('homeScreen').classList.remove('hidden');
            document.getElementById('liveScores').classList.add('hidden');
        }
    </script>
</body>
</html>
