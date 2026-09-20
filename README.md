<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative | بوابة العملاء</title>
    <style>
        :root {
            --bg-main: #090d16;
            --bg-card: #111827;
            --border-color: #1f2937;
            --accent: #38bdf8;
            --text-main: #f9fafb;
            --text-muted: #9ca3af;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, sans-serif; }
        body { background: var(--bg-main); color: var(--text-main); min-height: 100vh; display: flex; justify-content: center; align-items: center; padding: 20px; }

        .container { width: 100%; max-width: 440px; }

        /* شاشة تسجيل الدخول */
        .login-box {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            padding: 40px 30px;
            border-radius: 16px;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5);
            text-align: center;
        }
        .brand-logo { font-size: 24px; font-weight: bold; color: var(--text-main); margin-bottom: 8px; }
        .brand-logo span { color: var(--accent); }
        .login-box p { color: var(--text-muted); font-size: 14px; margin-bottom: 25px; }
        
        .input-group { margin-bottom: 20px; }
        input {
            width: 100%; padding: 14px; background: #030712; border: 1px solid var(--border-color);
            border-radius: 10px; color: #fff; font-size: 20px; text-align: center; letter-spacing: 4px; outline: none;
        }
        input:focus { border-color: var(--accent); }
        
        .btn-primary {
            width: 100%; padding: 12px; background: var(--accent); border: none; border-radius: 10px;
            color: #030712; font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.2s;
        }
        .btn-primary:hover { opacity: 0.9; }
        .error-msg { color: #f87171; font-size: 13px; margin-top: 12px; display: none; }

        /* لوحة التحكم (مخفية حتى يتم تسجيل الدخول) */
        .dashboard-section { display: none; width: 100%; max-width: 600px; }
        
        .dashboard-header {
            display: flex; justify-content: space-between; align-items: center;
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 20px; border-radius: 12px; margin-bottom: 20px;
        }
        .user-info h2 { font-size: 18px; color: var(--text-main); }
        .user-info span { font-size: 13px; color: var(--text-muted); }
        
        .btn-logout {
            background: transparent; border: 1px solid #f87171; color: #f87171;
            padding: 6px 12px; border-radius: 6px; font-size: 13px; cursor: pointer;
        }
        
        .card {
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 24px; border-radius: 12px; margin-bottom: 16px;
        }
        .card h3 { font-size: 16px; color: var(--accent); margin-bottom: 12px; border-bottom: 1px solid var(--border-color); padding-bottom: 8px; }
        
        .info-row { display: flex; justify-content: space-between; margin-bottom: 10px; font-size: 15px; }
        .info-row span { color: var(--text-muted); }
        
        .status-badge {
            background: rgba(56, 189, 248, 0.1); color: var(--accent);
            padding: 4px 10px; border-radius: 20px; font-size: 13px; font-weight: 500;
        }
        
        .btn-action {
            display: inline-block; background: #22c55e; color: white; padding: 10px 20px;
            text-decoration: none; border-radius: 8px; font-weight: bold; font-size: 14px; margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- 1. شاشة تسجيل الدخول -->
        <div id="loginSection" class="login-box">
            <div class="brand-logo">MK <span>Creative</span></div>
            <p>أدخل كود الوصول (M) لمتابعة مشروعك</p>
            
            <div class="input-group">
                <input type="text" id="clientCode" placeholder="M" maxlength="3">
            </div>
            
            <button class="btn-primary" onclick="login()">دخول للنظام</button>
            <div id="error" class="error-msg">الكود غير صحيح. تأكد من كتابة الحرف M.</div>
        </div>

        <!-- 2. لوحة التحكم -->
        <div id="dashboardSection" class="dashboard-section">
            <div class="dashboard-header">
                <div class="user-info">
                    <h2 id="clientName">محمد عنتر</h2>
                    <span>عميل مميز - MK Creative</span>
                </div>
                <button class="btn-logout" onclick="logout()">خروج</button>
            </div>

            <div class="card">
                <h3>تفاصيل المشروع الحالي</h3>
                <div class="info-row">
                    <span>اسم المشروع:</span>
                    <strong id="projectName">بوابة العملاء (Client Portal)</strong>
                </div>
                <div class="info-row" style="margin-top: 12px;">
                    <span>الحالة:</span>
                    <span class="status-badge" id="projectStatus">● قيد التطوير النشط</span>
                </div>
            </div>

            <div class="card">
                <h3>الملفات والمتابعة</h3>
                <p style="color: var(--text-muted); font-size: 14px; margin-bottom: 10px;">روابط المعاينة والمصادر الخاصة بك:</p>
                <a href="https://github.com" id="projectLink" class="btn-action" target="_blank">فتح مستودع المشروع</a>
            </div>
        </div>
    </div>

    <script>
        const validCodes = {
            "M": { 
                name: "محمد عنتر", 
                project: "منظومة بوابة العملاء الاحترافية", 
                status: "● نشط ومتقدم (100%)", 
                link: "https://github.com" 
            }
        };

        window.onload = function() {
            const saved = localStorage.getItem('mk_session_data');
            if (saved) showDashboard(JSON.parse(saved));
        };

        function login() {
            const code = document.getElementById('clientCode').value.trim().toUpperCase();
            if (validCodes[code]) {
                const data = validCodes[code];
                localStorage.setItem('mk_session_data', JSON.stringify(data));
                showDashboard(data);
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

        function showDashboard(data) {
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('dashboardSection').style.display = 'block';
            
            document.getElementById('clientName').innerText = data.name;
            document.getElementById('projectName').innerText = data.project;
            document.getElementById('projectStatus').innerText = data.status;
            document.getElementById('projectLink').href = data.link;
        }

        function logout() {
            localStorage.removeItem('mk_session_data');
            location.reload();
        }
    </script>
</body>
</html> 
