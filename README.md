<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative | بوابة العملاء الاحترافية</title>
    <style>
        :root {
            --bg-main: #090d16;
            --bg-card: #111827;
            --border-color: #1f2937;
            --accent: #38bdf8;
            --text-main: #f9fafb;
            --text-muted: #9ca3af;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Inter', 'Segoe UI', Tahoma, sans-serif; }
        body { background: var(--bg-main); color: var(--text-main); min-height: 100vh; display: flex; justify-content: center; align-items: center; padding: 20px; }

        .app-container { width: 100%; max-width: 440px; transition: all 0.3s ease; }
        .dashboard-layout { max-width: 1000px !important; display: none; width: 100%; }

        /* Login Card (Linear/Vercel Style) */
        .login-box {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            padding: 40px 30px;
            border-radius: 16px;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5), 0 8px 10px -6px rgba(0, 0, 0, 0.5);
            text-align: center;
        }
        .brand-logo { font-size: 22px; font-weight: 700; color: var(--text-main); margin-bottom: 8px; letter-spacing: -0.5px; }
        .brand-logo span { color: var(--accent); }
        .login-box p { color: var(--text-muted); font-size: 14px; margin-bottom: 30px; }
        
        .input-group { position: relative; margin-bottom: 20px; }
        input {
            width: 100%; padding: 14px 16px; background: #030712; border: 1px solid var(--border-color);
            border-radius: 10px; color: #fff; font-size: 18px; text-align: center; letter-spacing: 4px; outline: none; transition: 0.2s;
        }
        input:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(56, 189, 248, 0.15); }
        
        .btn-primary {
            width: 100%; padding: 12px; background: #f8fafc; border: none; border-radius: 10px;
            color: #030712; font-size: 15px; font-weight: 600; cursor: pointer; transition: 0.2s;
        }
        .btn-primary:hover { background: #e2e8f0; }
        .error-msg { color: #f87171; font-size: 13px; margin-top: 12px; display: none; }

        /* Dashboard UI (Modern SaaS Style) */
        .dashboard-header {
            display: flex; justify-content: space-between; align-items: center;
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 20px 24px; border-radius: 14px; margin-bottom: 24px;
        }
        .user-info h2 { font-size: 18px; font-weight: 600; color: var(--text-main); }
        .user-info span { font-size: 13px; color: var(--text-muted); }
        
        .btn-logout {
            background: transparent; border: 1px solid var(--border-color); color: #f87171;
            padding: 8px 14px; border-radius: 8px; font-size: 13px; cursor: pointer; transition: 0.2s;
        }
        .btn-logout:hover { background: rgba(248, 113, 113, 0.1); }

        .grid-stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 16px; margin-bottom: 24px; }
        .stat-card {
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 20px; border-radius: 14px; position: relative; overflow: hidden;
        }
        .stat-card title { font-size: 13px; color: var(--text-muted); display: block; margin-bottom: 8px; }
        .stat-card .value { font-size: 20px; font-weight: 600; color: var(--text-main); }
        
        .status-badge {
            display: inline-flex; align-items: center; gap: 6px; background: rgba(56, 189, 248, 0.1);
            color: var(--accent); padding: 4px 10px; border-radius: 20px; font-size: 13px; font-weight: 500;
        }

        .action-card {
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 24px; border-radius: 14px; display: flex; justify-content: space-between; align-items: center;
        }
        .action-card p { color: var(--text-muted); font-size: 14px; margin-bottom: 4px; }
        .btn-action {
            background: var(--accent); color: #030712; padding: 10px 20px; border-radius: 8px;
            text-decoration: none; font-weight: 600; font-size: 14px; transition: 0.2s;
        }
        .btn-action:hover { opacity: 0.9; }
    </style>
</head>
<body>

    <div id="appContainer" class="app-container">
        
        <!-- شاشة تسجيل الدخول -->
        <div id="loginSection" class="login-box">
            <div class="brand-logo">MK <span>Creative</span></div>
            <p>أدخل كود الوصول الخاص بك لمتابعة لوحة المشروع</p>
            
            <div class="input-group">
                <input type="text" id="clientCode" placeholder="M" maxlength="5">
            </div>
            
            <button class="btn-primary" onclick="login()">دخول للنظام</button>
            <div id="error" class="error-msg">الكود غير صحيح. يجدر استخدام الكود M.</div>
        </div>

        <!-- لوحة تحكم العميل -->
        <div id="dashboardSection" class="dashboard-layout">
            <div class="dashboard-header">
                <div class="user-info">
                    <h2 id="clientName">محمد عنتر</h2>
                    <span>MK Creative Agency Client</span>
                </div>
                <button class="btn-logout" onclick="logout()">تسجيل خروج</button>
            </div>

            <div class="grid-stats">
                <div class="stat-card">
                    <span style="font-size:13px; color:var(--text-muted);">المشروع النشط</span>
                    <div class="value" id="projectName" style="margin-top:5px; font-size:16px;">تطوير واجهات الوكالة</div>
                </div>
                <div class="stat-card">
                    <span style="font-size:13px; color:var(--text-muted);">حالة التنفيذ</span>
                    <div style="margin-top:8px;">
                        <span class="status-badge" id="projectStatus">● قيد التطوير النشط</span>
                    </div>
                </div>
            </div>

            <div class="action-card">
                <div>
                    <p>ملفات المعاينة والمصادر النهائية</p>
                    <strong style="color:var(--text-main); font-size:15px;">جاهز للمراجعة والمتابعة</strong>
                </div>
                <a href="https://github.com" id="projectLink" class="btn-action" target="_blank">فتح المستودع</a>
            </div>
        </div>

    </div>

    <script>
        const validCodes = {
            "M": { 
                name: "محمد عنتر", 
                project: "منظومة بوابة العملاء (Client Portal)", 
                status: "● نشط ومتقدم (95%)", 
                link: "https://github.com" 
            }
        };

        window.onload = function() {
            const saved = localStorage.getItem('mk_session');
            if (saved) showDashboard(JSON.parse(saved));
        };

        function login() {
            const code = document.getElementById('clientCode').value.trim().toUpperCase();
            if (validCodes[code]) {
                const data = validCodes[code];
                localStorage.setItem('mk_session', JSON.stringify(data));
                showDashboard(data);
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

        function showDashboard(data) {
            const container = document.getElementById('appContainer');
            container.classList.add('dashboard-layout');
            
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('dashboardSection').style.display = 'block';
            
            document.getElementById('clientName').innerText = data.name;
            document.getElementById('projectName').innerText = data.project;
            document.getElementById('projectStatus').innerText = data.status;
            document.getElementById('projectLink').href = data.link;
        }

        function logout() {
            localStorage.removeItem('mk_session');
            location.reload();
        }
    </script>
</body>
</html>
