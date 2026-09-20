<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative Agency - بوابة العملاء</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background: #0f172a; color: #f8fafc; display: flex; justify-content: center; align-items: center; min-height: 100vh; padding: 20px; }
        
        .container { width: 100%; max-width: 500px; }
        
        /* كارد تسجيل الدخول */
        .login-card { background: #1e293b; padding: 40px; border-radius: 16px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); text-align: center; border: 1px solid #334155; }
        .login-card h2 { margin-bottom: 10px; color: #38bdf8; font-size: 24px; }
        .login-card p { color: #94a3b8; margin-bottom: 25px; font-size: 14px; }
        
        input { width: 100%; padding: 12px 16px; margin-bottom: 20px; background: #0f172a; border: 1px solid #475569; border-radius: 8px; color: #fff; font-size: 16px; text-align: center; letter-spacing: 2px; text-transform: uppercase; }
        input:focus { outline: none; border-color: #38bdf8; }
        
        button { width: 100%; padding: 12px; background: #38bdf8; border: none; border-radius: 8px; color: #0f172a; font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.3s; }
        button:hover { background: #0ea5e9; }
        
        .error-msg { color: #f87171; font-size: 13px; margin-bottom: 15px; display: none; }
        
        /* لوحة التحكم (مخفية لحين تسجيل الدخول) */
        .dashboard-section { display: none; }
        .header { display: flex; justify-content: space-between; align-items: center; background: #1e293b; padding: 20px; border-radius: 12px; border: 1px solid #334155; margin-bottom: 20px; }
        .header h2 { color: #38bdf8; font-size: 20px; }
        .logout { background: #f87171; border: none; padding: 6px 14px; color: white; border-radius: 6px; cursor: pointer; font-weight: bold; font-size: 14px; }
        
        .card { background: #1e293b; padding: 25px; border-radius: 12px; border: 1px solid #334155; margin-bottom: 20px; }
        .card h3 { margin-bottom: 15px; color: #cbd5e1; border-bottom: 1px solid #334155; padding-bottom: 10px; font-size: 18px; }
        .info-row { display: flex; justify-content: space-between; margin-bottom: 12px; font-size: 15px; }
        .info-row span { color: #94a3b8; }
        .badge { background: #0ea5e9; color: #fff; padding: 4px 12px; border-radius: 20px; font-size: 13px; }
        .btn-download { display: inline-block; background: #22c55e; color: white; padding: 10px 20px; text-decoration: none; border-radius: 8px; font-weight: bold; margin-top: 15px; font-size: 14px; }
        .btn-download:hover { background: #16a34a; }
    </style>
</head>
<body>

    <div class="container">
        <!-- 1. شاشة تسجيل الدخول -->
        <div id="loginSection" class="login-card">
            <h2>MK Creative | بوابة العملاء</h2>
            <p>أدخل الكود (M) لمتابعة المشروع</p>
            <div id="error" class="error-msg">الكود غير صحيح، تأكد من كتابة الحرف M بشكل صحيح.</div>
            <input type="text" id="clientCode" placeholder="اكتب M هنا" maxlength="5">
            <button onclick="login()">دخول للمشروع</button>
        </div>

        <!-- 2. لوحة تحكم العميل (تظهر بعد الدخول) -->
        <div id="dashboardSection" class="dashboard-section">
            <div class="header">
                <h2>مرحباً، <span id="clientName">عزيزنا العميل</span></h2>
                <button class="logout" onclick="logout()">خروج</button>
            </div>

            <div class="card">
                <h3>تفاصيل مشروعك الحالي</h3>
                <div class="info-row">
                    <span>اسم المشروع:</span>
                    <strong id="projectName">مشروع وكالة MK Creative</strong>
                </div>
                <div class="info-row" style="margin-top: 10px;">
                    <span>حالة التنفيذ:</span>
                    <span class="badge" id="projectStatus">جارٍ العمل عليه</span>
                </div>
            </div>

            <div class="card">
                <h3>الملفات والروابط النهائية</h3>
                <p style="color: #94a3b8; margin-bottom: 10px; font-size: 14px;">روابط معاينة العمل الخاصة بك:</p>
                <a href="https://github.com" id="projectLink" class="btn-download" target="_blank">تحميل / معاينة الملفات</a>
            </div>
        </div>
    </div>

    <script>
        // قاعدة البيانات المعرفة لكود M فقط
        const validCodes = {
            "M": { 
                name: "محمد عنتر (عميل مميز)", 
                project: "تطوير واجهات ونظام الوكالة", 
                status: "نشط وقيد التحديث (100%)", 
                link: "https://github.com" 
            }
        };

        // التحقق من حالة تسجيل الدخول مسبقاً
        window.onload = function() {
            const savedClient = localStorage.getItem('mk_current_client');
            if (savedClient) {
                showDashboard(JSON.parse(savedClient));
            }
        };

        function login() {
            const code = document.getElementById('clientCode').value.trim().toUpperCase();
            
            if (validCodes[code]) {
                const client = validCodes[code];
                localStorage.setItem('mk_current_client', JSON.stringify(client));
                showDashboard(client);
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

        function showDashboard(client) {
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('dashboardSection').style.display = 'block';
            
            document.getElementById('clientName').innerText = client.name;
            document.getElementById('projectName').innerText = client.project;
            document.getElementById('projectStatus').innerText = client.status;
            document.getElementById('projectLink').href = client.link;
        }

        function logout() {
            localStorage.removeItem('mk_current_client');
            document.getElementById('dashboardSection').style.display = 'none';
            document.getElementById('loginSection').style.display = 'block';
            document.getElementById('clientCode').value = '';
            document.getElementById('error').style.display = 'none';
        }
    </script>
</body>
</html>
