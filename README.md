<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Points Table Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .hidden-section { display: none; }
    </style>
</head>
<body class="bg-slate-100 font-sans text-gray-800">

    <!-- Navbar -->
    <nav class="bg-emerald-700 text-white p-4 shadow-md flex justify-between items-center">
        <h1 class="text-xl font-bold">🏏 Cricket Portal</h1>
        <div id="nav-user-info" class="flex items-center gap-4 hidden-section">
            <span id="nav-phone" class="text-sm bg-emerald-800 px-3 py-1 rounded"></span>
            <span id="nav-wallet" class="text-sm bg-amber-500 text-slate-900 font-bold px-3 py-1 rounded"></span>
            <button onclick="logout()" class="bg-red-600 px-3 py-1 text-sm rounded hover:bg-red-700">Logout</button>
        </div>
    </nav>

    <div class="container mx-auto p-4 max-w-5xl">

        <!-- 1. LOGIN SECTION -->
        <div id="login-section" class="bg-white p-6 rounded-lg shadow-md max-w-md mx-auto mt-10">
            <h2 class="text-2xl font-bold text-center mb-4 text-emerald-700">Login / Register</h2>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Mobile Number:</label>
                <input type="text" id="login-phone" placeholder="Enter Mobile Number" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Unique User ID (Exactly 5 letters/chars):</label>
                <input type="text" id="login-userid" maxlength="5" placeholder="e.g. ab123" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <button onclick="handleLogin()" class="w-full bg-emerald-600 text-white py-2 rounded font-bold hover:bg-emerald-700">Login</button>
            <p class="text-xs text-gray-500 mt-3 text-center">Note: 50 Points free on new number. Special number `9569981484` gets 5000 points!</p>
        </div>

        <!-- 2. MAIN DASHBOARD -->
        <div id="dashboard-section" class="hidden-section">
            <!-- Tabs -->
            <div class="flex flex-wrap gap-2 mb-6 border-b pb-2">
                <button onclick="switchTab('matches')" class="px-4 py-2 bg-emerald-600 text-white rounded font-medium tab-btn" id="btn-matches">Match Schedule</button>
                <button onclick="switchTab('points')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-points">Points Table</button>
                <button onclick="switchTab('subscription')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-subscription">Subscriptions</button>
                <button onclick="switchTab('admin')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-admin">Admin Panel</button>
            </div>

            <!-- TAB 1: MATCH SCHEDULE -->
            <div id="tab-matches" class="space-y-4">
                <h3 id="schedule-series-title" class="text-xl font-bold text-emerald-800">Scheduled Matches</h3>
                <div id="matches-list" class="grid gap-4">
                    <!-- Dynamic Matches -->
                </div>
            </div>

            <!-- TAB 2: POINTS TABLE -->
            <div id="tab-points" class="hidden-section space-y-6">
                <h3 class="text-xl font-bold text-emerald-800">ICC Points Table</h3>
                <div id="points-tables-container" class="space-y-6">
                    <!-- Dynamic Groups Points Table -->
                </div>
            </div>

            <!-- TAB 3: SUBSCRIPTION -->
            <div id="tab-subscription" class="hidden-section bg-white p-6 rounded-lg shadow-md">
                <h3 class="text-xl font-bold mb-4 text-emerald-800">Active Admin Subscription</h3>
                <div id="subscription-status" class="mb-6 p-4 bg-amber-50 border border-amber-200 rounded">
                    <!-- Sub Status -->
                </div>
                <h4 class="text-lg font-semibold mb-3">Buy / Activate Subscription (Deduct Points)</h4>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">30 Minutes Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 149 Points</p>
                        <button onclick="buySubscription('30min', 149)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Half Monthly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 400 Points</p>
                        <button onclick="buySubscription('half_monthly', 400)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Monthly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 600 Points</p>
                        <button onclick="buySubscription('monthly', 600)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Half Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 6000 Points</p>
                        <button onclick="buySubscription('half_yearly', 6000)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm col-span-full">
                        <p class="font-bold">Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 8000 Points</p>
                        <button onclick="buySubscription('yearly', 8000)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                </div>

                <div class="bg-emerald-50 p-4 rounded border border-emerald-200">
                    <h4 class="font-bold text-emerald-900">Point Packages (Contact: 9569981484)</h4>
                    <p class="text-sm">₹80 = 1500 Points | ₹249 = 22000 Points</p>
                </div>
            </div>

            <!-- TAB 4: ADMIN PANEL -->
            <div id="tab-admin" class="hidden-section space-y-6">
                <div class="bg-white p-6 rounded-lg shadow-md border-t-4 border-emerald-600">
                    <h3 class="text-xl font-bold text-emerald-800 mb-4">👑 Admin Panel</h3>

                    <!-- Schedule Match Form -->
                    <div class="border-b pb-6 mb-6">
                        <h4 id="form-heading" class="font-semibold mb-3 text-lg">Schedule New Match</h4>
                        <input type="hidden" id="edit-match-index" value="-1">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm">Series Type:</label>
                                <select id="admin-series-type" class="w-full p-2 border rounded">
                                    <option value="existing">Usi Series ka Match (Same Series)</option>
                                    <option value="new">New Series ka Match (New Gap)</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Series Name:</label>
                                <input type="text" id="admin-series-name" placeholder="Series Name (e.g. West Indies tour of India 2026)" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Label (e.g. 1st T20, 2nd ODI):</label>
                                <input type="text" id="admin-match-label" placeholder="1st T20" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Group Name (e.g. Group A):</label>
                                <input type="text" id="admin-group-name" placeholder="Group Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Date & Time / Info:</label>
                                <input type="date" id="admin-date" class="w-full p-2 border rounded mb-2">
                                <input type="text" id="admin-time" placeholder="Time or Extra Tag (e.g. 3:30 | 1DAY GEP)" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 1 & Score / Status:</label>
                                <input type="text" id="admin-team1" placeholder="Team 1 Name (e.g. IND)" class="w-full p-2 border rounded mb-2">
                                <input type="text" id="admin-score1" placeholder="Score or Ticket Info" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 2 & Score / Status:</label>
                                <input type="text" id="admin-team2" placeholder="Team 2 Name (e.g. WI)" class="w-full p-2 border rounded mb-2">
                                <input type="text" id="admin-score2" placeholder="Score info" class="w-full p-2 border rounded">
                            </div>
                            <div class="col-span-full">
                                <label class="block text-sm">Venue:</label>
                                <input type="text" id="admin-venue" placeholder="Stadium / Venue" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <div class="flex gap-2 mt-4">
                            <button id="save-match-btn" onclick="scheduleMatch()" class="bg-emerald-600 text-white px-4 py-2 rounded font-bold hover:bg-emerald-700">Publish / Schedule Match</button>
                            <button id="cancel-edit-btn" onclick="resetMatchForm()" class="hidden bg-gray-500 text-white px-4 py-2 rounded font-bold hover:bg-gray-600">Cancel Edit</button>
                        </div>
                    </div>

                    <!-- Manage / Edit / Delete Existing Matches -->
                    <div class="border-b pb-6 mb-6">
                        <h4 class="font-semibold mb-3 text-lg">Manage Existing Matches (Edit / Delete)</h4>
                        <div id="admin-matches-manage-list" class="space-y-2 max-h-60 overflow-y-auto border p-2 rounded">
                            <!-- Populated dynamically -->
                        </div>
                    </div>

                    <!-- Points Table Updater -->
                    <div class="border-b pb-6 mb-6">
                        <h4 class="font-semibold mb-3 text-lg">Update Points Table</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                            <div>
                                <label class="block text-sm">Group Name:</label>
                                <input type="text" id="update-group-name" placeholder="Enter Group Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team Name:</label>
                                <input type="text" id="update-team-name" placeholder="Team Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Result:</label>
                                <select id="admin-match-result" class="w-full p-2 border rounded">
                                    <option value="won">Won (+2 Pts)</option>
                                    <option value="lost">Lost (0 Pts)</option>
                                    <option value="tied">Tied / NR (+1 Pt)</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Net Run Rate (NRR) change (+/-):</label>
                                <input type="number" step="0.01" id="admin-nrr-change" placeholder="e.g. +0.45" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="updatePointsTable()" class="bg-blue-600 text-white px-4 py-2 rounded font-bold hover:bg-blue-700">Update Points Table</button>
                    </div>

                    <!-- Admin Point Sender -->
                    <div>
                        <h4 class="font-semibold mb-3 text-lg">Send Points to User (Admin Only)</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm">Recipient User ID:</label>
                                <input type="text" id="admin-send-userid" placeholder="Enter User ID" oninput="checkRecipientUser()" class="w-full p-2 border rounded">
                                <span id="recipient-status" class="text-xs font-semibold mt-1 block"></span>
                            </div>
                            <div>
                                <label class="block text-sm">Points Amount:</label>
                                <input type="number" id="admin-send-points" placeholder="Points to send" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="adminSendPoints()" class="mt-4 bg-amber-600 text-white px-4 py-2 rounded font-bold hover:bg-amber-700">Send Points</button>
                    </div>

                </div>
            </div>

        </div>

    </div>

    <!-- JavaScript Logic -->
    <script>
        const DB_KEY = "cricket_portal_db_v4";
        let currentUser = localStorage.getItem("current_logged_user") || null;
        let currentDeviceId = localStorage.getItem("device_id");

        if (!currentDeviceId) {
            currentDeviceId = "dev_" + Math.random().toString(36).substring(2, 9);
            localStorage.setItem("device_id", currentDeviceId);
        }

        function getDB() {
            let data = localStorage.getItem(DB_KEY);
            if (!data) {
                let initial = {
                    users: {},
                    devices: {},
                    userIDs: [],
                    matches: [],
                    pointsTable: {}, 
                    subscription: { activeUntil: 0 }
                };
                localStorage.setItem(DB_KEY, JSON.stringify(initial));
                return initial;
            }
            return JSON.parse(data);
        }

        function saveDB(db) {
            localStorage.setItem(DB_KEY, JSON.stringify(db));
        }

        window.onload = function() {
            if (currentUser) {
                let db = getDB();
                if (db.users[currentUser]) {
                    initDashboard();
                } else {
                    currentUser = null;
                    localStorage.removeItem("current_logged_user");
                }
            }
        };

        function handleLogin() {
            let phone = document.getElementById("login-phone").value.trim();
            let userid = document.getElementById("login-userid").value.trim();

            if (!phone || !userid) {
                alert("Please enter both Mobile Number and User ID.");
                return;
            }

            if (userid.length !== 5) {
                alert("User ID must be exactly 5 letters/characters long.");
                return;
            }

            let db = getDB();

            if (db.userIDs.includes(userid) && (!db.users[phone] || db.users[phone].userid !== userid)) {
                alert("This User ID is already taken by another user. Please choose a unique User ID.");
                return;
            }

            if (!db.devices[currentDeviceId]) {
                db.devices[currentDeviceId] = [];
            }

            let devicePhones = db.devices[currentDeviceId];
            if (!devicePhones.includes(phone) && devicePhones.length >= 3) {
                alert("Maximum 3 numbers allowed per device!");
                return;
            }

            if (!db.users[phone]) {
                let initialPoints = (phone === "9569981484") ? 5000 : 50;
                db.users[phone] = { phone: phone, userid: userid, wallet: initialPoints };
                db.userIDs.push(userid);
                if (!devicePhones.includes(phone)) devicePhones.push(phone);
            } else {
                if (db.users[phone].userid !== userid) {
                    let idx = db.userIDs.indexOf(db.users[phone].userid);
                    if (idx !== -1) db.userIDs.splice(idx, 1);
                    db.userIDs.push(userid);
                    db.users[phone].userid = userid;
                }
                if (!devicePhones.includes(phone)) devicePhones.push(phone);
            }

            saveDB(db);
            currentUser = phone;
            localStorage.setItem("current_logged_user", currentUser);
            initDashboard();
        }

        function logout() {
            currentUser = null;
            localStorage.removeItem("current_logged_user");
            document.getElementById("login-section").classList.remove("hidden-section");
            document.getElementById("dashboard-section").classList.add("hidden-section");
            document.getElementById("nav-user-info").classList.add("hidden-section");
        }

        function initDashboard() {
            document.getElementById("login-section").classList.add("hidden-section");
            document.getElementById("dashboard-section").classList.remove("hidden-section");
            document.getElementById("nav-user-info").classList.remove("hidden-section");

            let db = getDB();
            let user = db.users[currentUser];

            document.getElementById("nav-phone").innerText = `📞 ${user.phone} (${user.userid})`;
            document.getElementById("nav-wallet").innerText = `💰 Wallet: ${user.wallet} Pts`;

            renderMatches();
            renderPointsTable();
            renderSubscriptionStatus();
            renderAdminManageMatches();
        }

        function switchTab(tabName) {
            let db = getDB();
            let now = new Date().getTime();
            let isAdminActive = db.subscription.activeUntil > now;

            if (tabName === 'admin' && !isAdminActive) {
                alert("Active subscription required to open Admin Panel!");
                return;
            }

            ['matches', 'points', 'subscription', 'admin'].forEach(t => {
                document.getElementById(`tab-${t}`).classList.add("hidden-section");
                document.getElementById(`btn-${t}`).classList.remove("bg-emerald-600", "text-white");
                document.getElementById(`btn-${t}`).classList.add("bg-gray-200", "text-gray-700");
            });

            document.getElementById(`tab-${tabName}`).classList.remove("hidden-section");
            document.getElementById(`btn-${tabName}`).classList.remove("bg-gray-200", "text-gray-700");
            document.getElementById(`btn-${tabName}`).classList.add("bg-emerald-600", "text-white");
            
            if(tabName === 'admin') {
                renderAdminManageMatches();
            }
        }

        function scheduleMatch() {
            let db = getDB();
            let now = new Date().getTime();
            if (db.subscription.activeUntil < now) {
                alert("Active subscription required to schedule matches!");
                return;
            }

            let editIndex = parseInt(document.getElementById("edit-match-index").value);
            let seriesType = document.getElementById("admin-series-type").value;
            let seriesName = document.getElementById("admin-series-name").value.trim();
            let matchLabel = document.getElementById("admin-match-label").value.trim() || "Match";
            let groupName = document.getElementById("admin-group-name").value.trim() || "General Group";
            let team1 = document.getElementById("admin-team1").value.trim();
            let team2 = document.getElementById("admin-team2").value.trim();
            let score1 = document.getElementById("admin-score1").value.trim() || "Yet to bat";
            let score2 = document.getElementById("admin-score2").value.trim() || "Yet to bat";
            let date = document.getElementById("admin-date").value;
            let time = document.getElementById("admin-time").value;
            let venue = document.getElementById("admin-venue").value.trim();

            if (!team1 || !team2 || !date || !venue || !seriesName) {
                alert("Please fill all required match details.");
                return;
            }

            let matchData = {
                seriesType,
                seriesName,
                matchLabel,
                groupName,
                team1,
                team2,
                score1,
                score2,
                date,
                time,
                venue
            };

            if (editIndex === -1) {
                db.matches.push(matchData);
                alert("Match scheduled successfully!");
            } else {
                db.matches[editIndex] = matchData;
                alert("Match updated successfully!");
                resetMatchForm();
            }

            if (!db.pointsTable[groupName]) {
                db.pointsTable[groupName] = [];
            }
            [team1, team2].forEach(tName => {
                if (!db.pointsTable[groupName].some(t => t.team.toLowerCase() === tName.toLowerCase())) {
                    db.pointsTable[groupName].push({ team: tName, p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0 });
                }
            });

            saveDB(db);
            renderMatches();
            renderPointsTable();
            renderAdminManageMatches();
            switchTab("matches");
        }

        function renderMatches() {
            let db = getDB();
            let container = document.getElementById("matches-list");
            let seriesTitleElem = document.getElementById("schedule-series-title");
            container.innerHTML = "";

            if (db.matches.length === 0) {
                seriesTitleElem.innerText = "Scheduled Matches";
                container.innerHTML = `<p class="text-gray-500">No matches scheduled yet.</p>`;
                return;
            }

            // Set main series heading from the latest series
            seriesTitleElem.innerText = db.matches[db.matches.length - 1].seriesName;

            let lastSeries = "";
            db.matches.forEach((m, idx) => {
                let showGap = m.seriesType === 'new' || (idx > 0 && m.seriesName !== lastSeries);
                lastSeries = m.seriesName;

                let html = "";
                if (showGap && idx > 0) {
                    html += `<div class="my-6 border-t-2 border-dashed border-emerald-500"></div>`;
                }

                html += `
                    <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                        <div class="flex justify-between items-center text-xs text-gray-500 mb-1">
                            <span class="font-bold text-emerald-800">${m.matchLabel}</span>
                            <span>📅 ${m.date} | ⏰ ${m.time}</span>
                        </div>
                        <div class="flex justify-between items-center my-2">
                            <div class="text-base font-bold text-gray-800">🏏 ${m.team1} <span class="text-xs font-normal text-gray-500">(${m.score1})</span></div>
                            <span class="text-sm font-bold text-gray-400">vs</span>
                            <div class="text-base font-bold text-gray-800 text-right"><span class="text-xs font-normal text-gray-500">(${m.score2})</span> ${m.team2} 🏏</div>
                        </div>
                        <p class="text-xs text-gray-600 mt-2">📍 Venue: ${m.venue}</p>
                    </div>
                `;
                container.innerHTML += html;
            });
        }

        function renderAdminManageMatches() {
            let db = getDB();
            let listContainer = document.getElementById("admin-matches-manage-list");
            listContainer.innerHTML = "";

            if (db.matches.length === 0) {
                listContainer.innerHTML = `<p class="text-xs text-gray-500">No matches available to manage.</p>`;
                return;
            }

            db.matches.forEach((m, idx) => {
                listContainer.innerHTML += `
                    <div class="flex justify-between items-center bg-gray-50 p-2 rounded border text-sm">
                        <div>
                            <span class="font-bold">${m.matchLabel}:</span> ${m.team1} vs ${m.team2} <span class="text-xs text-gray-500">(${m.seriesName})</span>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="editMatch(${idx})" class="bg-blue-500 text-white px-2 py-1 text-xs rounded hover:bg-blue-600">Edit</button>
                            <button onclick="deleteMatch(${idx})" class="bg-red-500 text-white px-2 py-1 text-xs rounded hover:bg-red-600">Delete</button>
                        </div>
                    </div>
                `;
            });
        }

        function editMatch(idx) {
            let db = getDB();
            let m = db.matches[idx];

            document.getElementById("edit-match-index").value = idx;
            document.getElementById("admin-series-type").value = m.seriesType;
            document.getElementById("admin-series-name").value = m.seriesName;
            document.getElementById("admin-match-label").value = m.matchLabel;
            document.getElementById("admin-group-name").value = m.groupName;
            document.getElementById("admin-date").value = m.date;
            document.getElementById("admin-time").value = m.time;
            document.getElementById("admin-team1").value = m.team1;
            document.getElementById("admin-score1").value = m.score1;
            document.getElementById("admin-team2").value = m.team2;
            document.getElementById("admin-score2").value = m.score2;
            document.getElementById("admin-venue").value = m.venue;

            document.getElementById("form-heading").innerText = "Edit Scheduled Match";
            document.getElementById("save-match-btn").innerText = "Update Match";
            document.getElementById("cancel-edit-btn").classList.remove("hidden-section");
        }

        function resetMatchForm() {
            document.getElementById("edit-match-index").value = "-1";
            document.getElementById("admin-series-name").value = "";
            document.getElementById("admin-match-label").value = "";
            document.getElementById("admin-group-name").value = "";
            document.getElementById("admin-date").value = "";
            document.getElementById("admin-time").value = "";
            document.getElementById("admin-team1").value = "";
            document.getElementById("admin-score1").value = "";
            document.getElementById("admin-team2").value = "";
            document.getElementById("admin-score2").value = "";
            document.getElementById("admin-venue").value = "";

            document.getElementById("form-heading").innerText = "Schedule New Match";
            document.getElementById("save-match-btn").innerText = "Publish / Schedule Match";
            document.getElementById("cancel-edit-btn").classList.add("hidden-section");
        }

        function deleteMatch(idx) {
            if (confirm("Are you sure you want to delete this match?")) {
                let db = getDB();
                db.matches.splice(idx, 1);
                saveDB(db);
                renderMatches();
                renderAdminManageMatches();
                alert("Match deleted successfully!");
            }
        }

        function updatePointsTable() {
            let db = getDB();
            let now = new Date().getTime();
            if (db.subscription.activeUntil < now) {
                alert("Active subscription required to update points!");
                return;
            }

            let group = document.getElementById("update-group-name").value.trim();
            let teamName = document.getElementById("update-team-name").value.trim();
            let result = document.getElementById("admin-match-result").value;
            let nrrChange = parseFloat(document.getElementById("admin-nrr-change").value) || 0.0;

            if (!group || !teamName) {
                alert("Please enter Group Name and Team Name.");
                return;
            }

            if (!db.pointsTable[group]) {
                db.pointsTable[group] = [];
            }

            let teamObj = db.pointsTable[group].find(t => t.team.toLowerCase() === teamName.toLowerCase());
            if (!teamObj) {
                teamObj = { team: teamName, p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0 };
                db.pointsTable[group].push(teamObj);
            }

            teamObj.p += 1;
            if (result === "won") {
                teamObj.w += 1;
                teamObj.pts += 2;
            } else if (result === "lost") {
                teamObj.l += 1;
            } else if (result === "tied") {
                teamObj.t += 1;
                teamObj.pts += 1;
            }
            teamObj.nrr = parseFloat((teamObj.nrr + nrrChange).toFixed(2));

            saveDB(db);
            alert("Points Table updated successfully!");
            renderPointsTable();
        }

        function renderPointsTable() {
            let db = getDB();
            let container = document.getElementById("points-tables-container");
            container.innerHTML = "";

            let groupKeys = Object.keys(db.pointsTable);
            if (groupKeys.length === 0) {
                container.innerHTML = `<p class="text-gray-500">No groups or points tables created yet.</p>`;
                return;
            }

            groupKeys.forEach(group => {
                let teams = db.pointsTable[group].sort((a, b) => b.pts - a.pts || b.nrr - a.nrr);
                let rows = "";
                teams.forEach((t, i) => {
                    rows += `
                        <tr class="border-b text-center">
                            <td class="p-2 text-left">${i + 1}. ${t.team}</td>
                            <td class="p-2">${t.p}</td>
                            <td class="p-2">${t.w}</td>
                            <td class="p-2">${t.l}</td>
                            <td class="p-2">${t.t}</td>
                            <td class="p-2 font-bold text-emerald-700">${t.pts}</td>
                            <td class="p-2">${t.nrr}</td>
                        </tr>
                    `;
                });

                container.innerHTML += `
                    <div class="bg-white rounded-lg shadow-md overflow-hidden mb-4">
                        <div class="bg-emerald-700 text-white p-3 font-bold">${group}</div>
                        <table class="w-full text-sm">
                            <tr class="bg-gray-100 border-b text-center text-xs text-gray-600">
                                <th class="p-2 text-left">Team</th>
                                <th class="p-2">P</th>
                                <th class="p-2">W</th>
                                <th class="p-2">L</th>
                                <th class="p-2">T</th>
                                <th class="p-2">Pts</th>
                                <th class="p-2">NRR</th>
                            </tr>
                            ${rows}
                        </table>
                    </div>
                `;
            });
        }

        function buySubscription(plan, cost) {
            let db = getDB();
            let user = db.users[currentUser];

            if (user.wallet < cost) {
                alert("Insufficient points in wallet! Please contact 9569981484 to purchase points.");
                return;
            }

            user.wallet -= cost;

            let durationMs = 0;
            if (plan === '30min') durationMs = 30 * 60 * 1000;
            else if (plan === 'half_monthly') durationMs = 15 * 24 * 60 * 60 * 1000;
            else if (plan === 'monthly') durationMs = 30 * 24 * 60 * 60 * 1000;
            else if (plan === 'half_yearly') durationMs = 182 * 24 * 60 * 60 * 1000;
            else if (plan === 'yearly') durationMs = 365 * 24 * 60 * 60 * 1000;

            let now = new Date().getTime();
            if (db.subscription.activeUntil > now) {
                db.subscription.activeUntil += durationMs;
            } else {
                db.subscription.activeUntil = now + durationMs;
            }

            saveDB(db);
            alert("Subscription activated successfully!");
            initDashboard();
        }

        function renderSubscriptionStatus() {
            let db = getDB();
            let now = new Date().getTime();
            let statusBox = document.getElementById("subscription-status");

            if (db.subscription.activeUntil > now) {
                let timeLeft = Math.ceil((db.subscription.activeUntil - now) / (1000 * 60));
                statusBox.innerHTML = `<p class="text-emerald-700 font-bold">Status: Active</p><p class="text-sm">Expires in approximately ${timeLeft} minutes.</p>`;
            } else {
                statusBox.innerHTML = `<p class="text-red-600 font-bold">Status: Inactive</p><p class="text-sm">Buy a subscription below to unlock the Admin Panel.</p>`;
            }
        }

        function checkRecipientUser() {
            let db = getDB();
            let recipientId = document.getElementById("admin-send-userid").value.trim();
            let statusSpan = document.getElementById("recipient-status");

            if (!recipientId) {
                statusSpan.innerText = "";
                return;
            }

            let foundUser = null;
            for (let ph in db.users) {
                if (db.users[ph].userid === recipientId) {
                    foundUser = db.users[ph];
                    break;
                }
            }

            if (foundUser) {
                statusSpan.className = "text-xs font-semibold mt-1 block text-emerald-600";
                statusSpan.innerText = `✅ Success: User found! Current Wallet: ${foundUser.wallet} Points`;
            } else {
                statusSpan.className = "text-xs font-semibold mt-1 block text-red-600";
                statusSpan.innerText = `❌ Error: User ID not logged in or doesn't exist.`;
            }
        }

        function adminSendPoints() {
            let db = getDB();
            let now = new Date().getTime();
            if (db.subscription.activeUntil < now) {
                alert("Active subscription required to send points!");
                return;
            }

            let recipientId = document.getElementById("admin-send-userid").value.trim();
            let amount = parseInt(document.getElementById("admin-send-points").value);

            if (!recipientId || isNaN(amount) || amount <= 0) {
                alert("Please enter a valid recipient User ID and points amount.");
                return;
            }

            let recipientPhone = null;
            for (let ph in db.users) {
                if (db.users[ph].userid === recipientId) {
                    recipientPhone = ph;
                    break;
                }
            }

            if (!recipientPhone) {
                alert("Error: This User ID is not logged in anywhere!");
                return;
            }

            db.users[recipientPhone].wallet += amount;
            saveDB(db);
            alert(`Successfully sent ${amount} points to User ID: ${recipientId}`);
            document.getElementById("admin-send-userid").value = "";
            document.getElementById("admin-send-points").value = "";
            document.getElementById("recipient-status").innerText = "";
        }
    </script>
</body>
</html>
