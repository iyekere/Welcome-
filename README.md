# Welcome- 
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Virtual Numbers Dashboard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f6f9;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid #eee;
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        .nav-buttons {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        .btn {
            padding: 8px 16px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            border: none;
            font-size: 14px;
        }
        .deposit-btn { background-color: #007bff; color: white; }
        .deposit-btn:hover { background-color: #0056b3; }
        .auth-btn { background-color: #6c757d; color: white; }
        .auth-btn:hover { background-color: #5a6268; }
        .logout-btn { background-color: #dc3545; color: white; }
        .logout-btn:hover { background-color: #c82333; }

        /* Auth Forms */
        .auth-container {
            max-width: 400px;
            margin: 30px auto;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 8px;
            border: 1px solid #ddd;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            font-size: 14px;
        }
        .form-group input {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .submit-btn {
            width: 100%;
            background-color: #007bff;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 4px;
            font-weight: bold;
            cursor: pointer;
        }
        .toggle-text {
            text-align: center;
            margin-top: 15px;
            font-size: 14px;
        }
        .toggle-text a {
            color: #007bff;
            text-decoration: none;
            font-weight: bold;
        }

        /* Deposit Box */
        .deposit-section {
            display: none;
            background-color: #e9ecef;
            padding: 15px 20px;
            border-radius: 6px;
            border-left: 5px solid #007bff;
            margin-bottom: 25px;
        }
        .deposit-section h3 { margin-top: 0; color: #007bff; }
        .deposit-section p { margin: 6px 0; font-size: 15px; }

        /* Table & Scroll View */
        .table-wrapper {
            max-height: 550px;
            overflow-y: auto;
            border: 1px solid #ddd;
            border-radius: 6px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            text-align: left;
            padding: 12px;
            border-bottom: 1px solid #ddd;
        }
        th {
            background-color: #f8f9fa;
            position: sticky;
            top: 0;
            z-index: 1;
        }
        .buy-btn {
            background-color: #17a2b8;
            color: white;
            padding: 6px 14px;
            text-decoration: none;
            border-radius: 4px;
            font-size: 13px;
            display: inline-block;
        }
        .buy-btn:hover { background-color: #138496; }
        .wait-row {
            text-align: center;
            font-weight: bold;
            color: #6c757d;
            background-color: #f8f9fa;
            padding: 15px;
        }

        .hidden { display: none !important; }
    </style>
</head>
<body
 <!-- User Controls -->
            <button id="depositBtn" class="btn deposit-btn hidden" onclick="toggleDeposit()">Deposit</button>
            <button id="logoutBtn" class="btn logout-btn hidden" onclick="handleLogout()">Log Out</button>
        </div>
    </div>

    <!-- LOGIN FORM -->
    <div id="loginForm" class="auth-container">
        <h2>Log In</h2>
        <form onsubmit="handleLogin(event)">
            <div class="form-group">
                <label>Email Address</label>
                <input type="email" required placeholder="example@mail.com">
            </div>
            <div class="form-group">
                <label>Password</label>
                <input type="password" required placeholder="Enter password">
            </div>
            <button type="submit" class="submit-btn">Log In</button>
        </form>
        <div class="toggle-text">
            Don't have an account? <a href="#" onclick="showAuth('signup')">Sign Up</a>
        </div>
    </div>

    <!-- SIGN UP FORM -->
    <div id="signupForm" class="auth-container hidden">
        web    <h2>Sign Up</h2>
        <form onsubmit="handleSignup(event)">
            <div class="form-group">
                <label>Email Address</label>
                <input type="email" required placeholder="example@mail.com">
            </div>
            <div class="form-group">
                <label>Phone Number</label>
                <input type="tel" required placeholder="+234 800 000 0000">
            </div>
            <div class="form-group">
                <label>Password</label>
                <input type="password" required placeholder="Create password">
            </div>
            <button type="submit" class="submit-btn">Sign Up</button>
        </form>
        <div class="toggle-text">
            Already have an account? <a href="#" onclick="showAuth('login')">Log In</a>
        </div>
    </div>

    <!-- DASHBOARD CONTENT -->
    <div id="dashboardContent" class="hidden">
        
        <!-- Deposit Details Box -->
        <div id="depositBox" class="deposit-section">
            <h3>Payment Deposit Details</h3>
            <p><strong>Bank Name:</strong> Fairmoney Microfinance Bank LTD</p>
            <p><strong>Account Number:</strong> 2026457764</p>
            <p><strong>Account Name:</strong> Sheriff Ismail</p>
        </div>

        <h2>Available Virtual Numbers (100 Countries)</h2>
        <div class="table-wrapper">
            <table>
                <thead>
                    <tr>
                        <th>#</th>
                        <th>Country</th>
                        <th>Code</th>
                        <th>Price</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="numbersTableBody">
                    <!-- Javascript populates 100 countries dynamically below -->
                </tbody>
            </table>
        </div>
    </div>
</div>

<script>
    const countries = [
        { name: "United States 🇺🇸", code: "+1", price: "₦200" },
        { name: "United Kingdom 🇬🇧", code: "+44", price: "₦250" },
        { name: "Canada 🇨🇦", code: "+1", price: "₦220" },
        { name: "Germany 🇩🇪", code: "+49", price: "₦300" },
        { name: "France 🇫🇷", code: "+33", price: "₦280" },
        { name: "Netherlands 🇳🇱", code: "+31", price: "₦260" },
        { name: "Brazil 🇧🇷", code: "+55", price: "₦180" },
        { name: "India 🇮🇳", code: "+91", price: "₦150" },
        { name: "South Africa 🇿🇦", code: "+27", price: "₦230" },
        { name: "Nigeria 🇳🇬", code: "+234", price: "₦200" },
        { name: "Australia 🇦🇺", code: "+61", price: "₦290" },
        { name: "Spain 🇪🇸", code: "+34", price: "₦270" },
        { name: "Italy 🇮🇹", code: "+39", price: "₦270" },
        { name: "Poland 🇵🇱", code: "+48", price: "₦210" },
        { name: "Ukraine 🇺🇦", code: "+380", price: "₦190" },
        { name: "Russia 🇷🇺", code: "+7", price: "₦170" },
        { name: "China 🇨🇳", code: "+86", price: "₦240" },
        { name: "Japan 🇯🇵", code: "+81", price: "₦310" },
        { name: "South Korea 🇰🇷", code: "+82", price: "₦300" },
        { name: "Mexico 🇲🇽", code: "+52", price: "₦210" },
        { name: "Argentina 🇦🇷", code: "+54", price: "₦190" },
        { name: "Colombia 🇨🇴", code: "+57", price: "₦180" },
        { name: "Chile 🇨🇱", code: "+56", price: "₦200" },
        { name: "Peru 🇵🇪", code: "+51", price: "₦180" },
        { name: "Egypt 🇪🇬", code: "+20", price: "₦170" },
        { name: "Kenya 🇰🇪", code: "+254", price: "₦190" },
        { name: "Ghana 🇬🇭", code: "+233", price: "₦200" },
        { name: "Turkey 🇹🇷", code: "+90", price: "₦220" },
        { name: "Indonesia 🇮🇩", code: "+62", price: "₦160" },
        { name: "Philippines 🇵🇭", code: "+63", price: "₦170" },
        { name: "Vietnam 🇻🇳", code: "+84", price: "₦160" },
        { name: "Thailand 🇹🇭", code: "+66", price: "₦180" },
        { name: "Malaysia 🇲🇾", code: "+60", price: "₦200" },
        { name: "Singapore 🇸🇬", code: "+65", price: "₦320" },
        { name: "Saudi Arabia 🇸🇦", code: "+966", price: "₦280" },
        { name: "UAE 🇦🇪", code: "+971", price: "₦300" },
        { name: "Israel 🇮🇱", code: "+972", price: "₦270" },
        { name: "Pakistan 🇵🇰", code: "+92", price: "₦150" },
        { name: "Bangladesh 🇧🇩", code: "+880", price: "₦140" },
        { name: "Sweden 🇸🇪", code: "+46", price: "₦280" },
        { name: "Norway 🇳🇴", code: "+47", price: "₦290" },
        { name: "Denmark 🇩🇰", code: "+45", price: "₦280" },
        { name: "Finland 🇫🇮", code: "+358", price: "₦270" },
        { name: "Switzerland 🇨🇭", code: "+41", price: "₦350" },
        { name: "Austria 🇦🇹", code: "+43", price: "₦280" },
        { name: "Belgium 🇧🇪", code: "+32", price: "₦270" },
        { name: "Portugal 🇵🇹", code: "+351", price: "₦250" },
        { name: "Greece 🇬🇷", code: "+30", price: "₦240" },
        { name: "Romania 🇷🇴", code: "+40", price: "₦200" },
        { name: "Czechia 🇨🇿", code: "+420", price: "₦220" },
        { name: "Hungary 🇭🇺", code: "+36", price: "₦210" },
        { name: "Ireland 🇮🇪", code: "+353", price: "₦260" },
        { name: "New Zealand 🇳🇿", code: "+64", price: "₦290" },
        { name: "Morocco 🇲🇦", code: "+212", price: "₦200" },
        { name: "Algeria 🇩🇿", code: "+213", price: "₦190" },
        { name: "Uganda 🇺🇬", code: "+256", price: "₦180" },
        { name: "Tanzania 🇹🇿", code: "+255", price: "₦180" },
        { name: "Cameroon 🇨🇲", code: "+237", price: "₦210" },
        { name: "Ivory Coast 🇨🇮", code: "+225", price: "₦220" },
        { name: "Senegal 🇸🇳", code: "+221", price: "₦210" },
        { name: "Ecuador 🇪🇨", code: "+593", price: "₦190" },
        { name: "Venezuela 🇻🇪", code: "+58", price: "₦180" },
        { name: "Bolivia 🇧🇴", code: "+591", price: "₦170" },
        { name: "Paraguay 🇵🇾", code: "+595", price: "₦170" },
        { name: "Uruguay 🇺🇾", code: "+598", price: "₦210" },
        { name: "Costa Rica 🇨🇷", code: "+506", price: "₦220" },
        { name: "Panama 🇵🇦", code: "+507", price: "₦230" },
        { name: "Guatemala 🇬🇹", code: "+502", price: "₦190" },
        { name: "Jamaica 🇯🇲", code: "+1-876", price: "₦250" },
        { name: "Dominican Republic 🇩🇴", code: "+1-809", price: "₦210" },
        { name: "Sri Lanka 🇱🇰", code: "+94", price: "₦160" },
        { name: "Nepal 🇳🇵", code: "+977", price: "₦150" },
        { name: "Kazakhstan 🇰🇿", code: "+7", price: "₦180" },
        { name: "Uzbekistan 🇺🇿", code: "+998", price: "₦170" },
        { name: "Azerbaijan 🇦🇿", code: "+994", price: "₦190" },
        { name: "Georgia 🇬🇪", code: "+995", price: "₦200" },
        { name: "Armenia 🇦🇲", code: "+374", price: "₦190" },
        { name: "Jordan 🇯🇴", code: "+962", price: "₦230" },
        { name: "Lebanon 🇱🇧", code: "+961", price: "₦220" },
        { name: "Kuwait 🇰🇼", code: "+965", price: "₦310" },
        { name: "Qatar 🇶🇦", code: "+974", price: "₦320" },
        { name: "Oman 🇴🇲", code: "+968", price: "₦290" },
        { name: "Bahrain 🇧🇭", code: "+973", price: "₦280" },
        { name: "Iraq 🇮🇶", code: "+964", price: "₦200" },
        { name: "Croatia 🇭🇷", code: "+385", price: "₦230" },
        { name: "Serbia 🇷🇸", code: "+381", price: "₦220" },
        { name: "Bulgaria 🇧🇬", code: "+359", price: "₦210" },
        { name: "Slovakia 🇸🇰", code: "+421", price: "₦230" },
        { name: "Slovenia 🇸🇮", code: "+386", price: "₦240" },
        { name: "Estonia 🇪🇪", code: "+372", price: "₦250" },
        { name: "Latvia 🇱🇻", code: "+371", price: "₦240" },
        { name: "Lithuania 🇱🇹", code: "+370", price: "₦240" },
        { name: "Cyprus 🇨🇾", code: "+357", price: "₦250" },
        { name: "Malta 🇲🇹", code: "+356", price: "₦260" },
        { name: "Iceland 🇮🇸", code: "+354", price: "₦300" },
        { name: "Luxembourg 🇱🇺", code: "+352", price: "₦310" },
        { name: "Moldova 🇲🇩", code: "+373", price: "₦190" },
        { name: "Albania 🇦🇱", code: "+355", price: "₦200" },
        { name: "North Macedonia 🇲🇰", code: "+389", price: "₦200" },
        { name: "Zambia 🇿🇲", code: "+260", price: "₦180" }
    ];

    // Build Table Rows
    const tbody = document.getElementById('numbersTableBody');
    countries.forEach((c, index) => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td>${index + 1}</td>
            <td>${c.name}</td>
            <td>${c.code}</td>
            <td>${c.price}</td>
            <td><a href="#" class="buy-btn">Buy</a></td>
        `;
        tbody.appendChild(row);
    });

    // Add Wait Row at the bottom
    const waitRow = document.createElement('tr');
    waitRow.innerHTML = `<td colspan="5" class="wait-row">Wait for more...</td>`;
    tbody.appendChild(waitRow);

    function showAuth(type) {
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('signupForm').classList.add('hidden');
        if (type === 'login') {
            document.getElementById('loginForm').classList.remove('hidden');
        } else {
            document.getElementById('signupForm').classList.remove('hidden');
        }
    }

    function handleLogin(e) {
        e.preventDefault();
        enterDashboard();
    }

    function handleSignup(e) {
        e.preventDefault();
        enterDashboard();
    }

    function enterDashboard() {
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('signupForm').classList.add('hidden');
        document.getElementById('showLoginBtn').classList.add('hidden');
        document.getElementById('showSignupBtn').classList.add('hidden');
        
        document.getElementById('dashboardContent').classList.remove('hidden');
        document.getElementById('depositBtn').classList.remove('hidden');
        document.getElementById('logoutBtn').classList.remove('hidden');
    }

    function handleLogout() {
        document.getElementById('dashboardContent').classList.add('hidden');
        document.getElementById('depositBtn').classList.add('hidden');
        document.getElementById('logoutBtn').classList.add('hidden');
        
        document.getElementById('showLoginBtn').classList.remove('hidden');
        document.getElementById('showSignupBtn').classList.remove('hidden');
        document.getElementById('depositBox').style.display = "none";
        showAuth('login');
    }

    function toggleDeposit() {
        var box = document.getElementById("depositBox");
        if (box.style.display === "none" || box.style.display === "") {
            box.style.display = "block";
        } else {
            box.style.display = "none";
        }
    }
</script>

</body>
</html>
