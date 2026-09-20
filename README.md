<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative | لوحة تحكم العملاء الاحترافية</title>
    <style>
        :root {
            --bg-main: #090d16;
            --bg-sidebar: #0f172a;
            --bg-card: #1e293b;
            --border-color: #334155;
            --accent: #38bdf8;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --success: #22c55e;
            --warning: #f59e0b;
            --danger: #ef4444;
        }

        /* ميزة 1: الثيم الفاتح (اختياري) */
        [data-theme="light"] {
            --bg-main: #f8fafc;
            --bg-sidebar: #ffffff;
            --bg-card: #ffffff;
            --border-color: #e2e8f0;
            --accent: #0284c7;
            --text-main: #0f172a;
            --text-muted: #64748b;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, sans-serif; }
        body { background: var(--bg-main); color: var(--text-main); min-height: 100vh; display: flex; justify-content: center; align-items: center; transition: 0.3s; }

        /* شاشة تسجيل الدخول */
        .login-wrapper { width: 100%; max-width: 420px; padding: 20px; }
        .login-card {
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 40px 30px; border-radius: 16px; box-shadow: 0 15px 30px rgba(0,0,0,0.3); text-align: center;
        }
        .login-card h2 { color: var(--accent); font-size: 24px; margin-bottom: 10px; }
        .login-card p { color: var(--text-muted); font-size: 14px; margin-bottom: 25px; }
        .login-card input {
            width: 100%; padding: 14px; background: var(--bg-main); border: 1px solid var(--border-color);
            border-radius: 10px; color: var(--text-main); font-size: 18px; text-align: center; letter-spacing: 3px; outline: none; margin-bottom: 20px;
        }
        .btn-login {
            width: 100%; padding: 12px; background: var(--accent); border: none; border-radius: 10px;
            color: #0f172a; font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.2s;
        }
        .btn-login:hover { opacity: 0.9; }
        .error-msg { color: var(--danger); font-size: 13px; margin-top: 10px; display: none; }

        /* الداشبورد الاحترافية */
        .dashboard-container { display: none; width: 100vw; height: 100vh; grid-template-columns: 260px 1fr; background: var(--bg-main); }
        
        /* القائمة الجانبية Sidebar */
        .sidebar { background: var(--bg-sidebar); border-left: 1px solid var(--border-color); padding: 25px 20px; display: flex; flex-direction: column; justify-content: space-between; }
        .sidebar-brand { font-size: 20px; font-weight: bold; color: var(--accent); margin-bottom: 30px; text-align: center; }
        .sidebar-menu { list-style: none; display: flex; flex-direction: column; gap: 8px; }
        .sidebar-menu li { padding: 12px 15px; border-radius: 8px; color: var(--text-muted); cursor: pointer; font-size: 15px; transition: 0.2s; display: flex; align-items: center; gap: 10px; }
        .sidebar-menu li.active, .sidebar-menu li:hover { background: rgba(56, 189, 248, 0.1); color: var(--accent); font-weight: 500; }
        
        /* المحتوى الرئيسي */
        .main-content { padding: 25px; overflow-y: auto; }
        .top-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; background: var(--bg-card); padding: 15px 20px; border-radius: 12px; border: 1px solid var(--border-color); }
        
        /* ميزات إضافية علوية (بحث، إشعارات، ثيم) */
        .header-actions { display: flex; align-items: center; gap: 12px; }
        .icon-btn { background: var(--bg-main); border: 1px solid var(--border-color); color: var(--text-main); width: 38px; height: 38px; border-radius: 8px; cursor: pointer; display: flex; align-items: center; justify-content: center; transition: 0.2s; }
        .icon-btn:hover { border-color: var(--accent); }
        
        /* البطاقات الإحصائية */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 25px; }
        .stat-card { background: var(--bg-card); border: 1px solid var(--border-color); padding: 18px; border-radius: 12px; position: relative; overflow: hidden; }
        .stat-card span { font-size: 13px; color: var(--text-muted); display: block; margin-bottom: 6px; }
        .stat-card h3 { font-size: 20px; font-weight: bold; color: var(--text-main); }

        /* الشبكات والأقسام */
        .grid-2 { display: grid; grid-template-columns: 2fr 1fr; gap: 20px; margin-bottom: 20px; }
        .card-box { background: var(--bg-card); border: 1px solid var(--border-color); padding: 20px; border-radius: 12px; margin-bottom: 20px; }
        .card-box h3 { font-size: 16px; color: var(--accent); margin-bottom: 15px; border-bottom: 1px solid var(--border-color); padding-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }

        /* ميزة 9: جدول الفواتير */
        .table-custom { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 14px; }
        .table-custom th, .table-custom td { padding: 10px; text-align: right; border-bottom: 1px solid var(--border-color); color: var(--text-muted); }
        .table-custom th { color: var(--text-main); font-weight: 600; }
        
        /* ميزة 8: رفع الملفات */
        .upload-zone { border: 2px dashed var(--border-color); padding: 20px; text-align: center; border-radius: 8px; cursor: pointer; color: var(--text-muted); font-size: 14px; transition: 0.2s; }
        .upload-zone:hover { border-color: var(--accent); color: var(--accent); }

        /* ميزة 11: التقييم */
        .star-rating { display: flex; gap: 5px; font-size: 20px; cursor: pointer; color: var(--warning); }

        .btn-main { background: var(--accent); color: #0f172a; border: none; padding: 10px 16px; border-radius: 8px; font-weight: bold; cursor: pointer; text-decoration: none; display: inline-block; font-size: 14px; }
        .btn-outline { background: transparent; border: 1px solid var(--border-color); color: var(--text-main); padding: 8px 14px; border-radius: 8px; cursor: pointer; }

        @media (max-width: 900px) {
            .dashboard-container { grid-template-columns: 1fr; }
            .sidebar { display: none; }
            .grid-2 { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- 1. شاشة تسجيل الدخول -->
    <div id="loginSection" class="login-wrapper">
        <div class="login-card">
            <h2>MK Creative Agency</h2>
            <p>أدخل كود الوصول (M) لفتح لوحة التحكم الذكية</p>
            <input type="text" id="clientCode" placeholder="M" maxlength="3">
            <button class="btn-login" onclick="login()">دخول للنظام</button>
            <div id="error" class="error-msg">الكود غير صحيح، تأكد من كتابة الحرف M.</div>
        </div>
    </div>

    <!-- 2. لوحة التحكم المطورة بـ 20 ميزة جديدة -->
    <div id="dashboardSection" class="dashboard-container">
        
        <!-- القائمة الجانبية -->
        <aside class="sidebar">
            <div>
                <div class="sidebar-brand">MK CREATIVE</div>
                <ul class="sidebar-menu">
                    <li class="active">📊 لوحة القيادة</li>
                    <li>📂 مشاريعي وإدارتها</li>
                    <li>💳 الفواتير والمدفوعات</li>
                    <li>💬 الدعم الفني المباشر</li>
                    <li>⚙️ إعدادات الحساب</li>
                </ul>
            </div>
            <div>
                <button class="btn-outline" style="width:100%; color:var(--danger); border-color:var(--danger);" onclick="logout()">تسجيل خروج</button>
            </div>
        </aside>

        <!-- المحتوى الرئيسي -->
        <main class="main-content">
            <!-- الهيدر العلوي المطور (ميزات: بحث، إشعارات، ثيم، fullscreen) -->
            <div class="top-header">
                <div>
                    <h1 style="font-size: 18px;">مرحباً، <span id="clientName">محمد عنتر</span> 👋</h1>
                    <span style="font-size: 13px; color: var(--text-muted);" id="currentDate">تاريخ اليوم: 2026-09-20</span>
                </div>
                <div class="header-actions">
                    <!-- ميزة 4: البحث السريع -->
                    <input type="text" id="quickSearch" placeholder="بحث سريع..." style="padding: 6px 12px; background:var(--bg-main); border:1px solid var(--border-color); border-radius:8px; color:var(--text-main); font-size:13px; outline:none;" onkeyup="quickFilter()">
                    <!-- ميزة 3: إشعارات -->
                    <button class="icon-btn" onclick="alert('لديك إشعار جديد: تم تحديث ملفات المشروع بنجاح.')" title="الإشعارات">🔔</button>
                    <!-- ميزة 1: تغيير الثيم -->
                    <button class="icon-btn" onclick="toggleTheme()" title="تبديل الثيم">🌙</button>
                    <!-- ميزة 2: ملء الشاشة -->
                    <button class="icon-btn" onclick="toggleFullscreen()" title="ملء الشاشة">⛶</button>
                </div>
            </div>

            <!-- ميزة 6 + 7 + 15: الإحصائيات العلوية وحالة السيرفرات -->
            <div class="stats-grid">
                <div class="stat-card">
                    <span>المشروع النشط</span>
                    <h3 id="projectName">بوابة العملاء SaaS</h3>
                </div>
                <div class="stat-card">
                    <span>ميزانية المشروع</span>
                    <h3>$1,500 <span style="font-size:11px; color:var(--success);">(مدفوع بالكامل)</span></h3>
                </div>
                <div class="stat-card">
                    <span>الوقت المتبقي (Countdown)</span>
                    <h3 style="color: var(--warning);" id="countdownTimer">3 أيام و 5 ساعات</h3>
                </div>
                <div class="stat-card">
                    <span>حالة الخوادم (Uptime)</span>
                    <h3 style="color: var(--success); font-size: 15px;">● تعمل بكفاءة 100%</h3>
                </div>
            </div>

            <div class="grid-2">
                <!-- تفاصيل المشروع وميزة 10 (نسخ الرابط) & 13 (تصدير تقرير) -->
                <div class="card-box">
                    <h3>
                        <span>إدارة المشروع ومعاينته</span>
                        <div>
                            <button class="btn-outline" style="font-size: 11px; padding: 4px 8px;" onclick="copyProjectLink()">📋 نسخ الرابط</button>
                            <button class="btn-outline" style="font-size: 11px; padding: 4px 8px;" onclick="exportReport()">📥 تصدير تقرير</button>
                        </div>
                    </h3>
                    <p style="color: var(--text-muted); font-size: 14px; margin-bottom: 15px;">رابط المستودع أو المعاينة المباشرة الخاصة بك:</p>
                    <a href="https://github.com" id="projectLink" target="_blank" class="btn-main" style="margin-bottom: 15px;">فتح المستودع الخارجي ↗</a>
                    
                    <!-- ميزة 8: منطقة رفع الملفات -->
                    <div class="upload-zone" onclick="alert('تم تفعيل خاصية رفع الملفات! اختر الملفات لإرسالها للوكالة.')">
                        📁 اسحب ملفاتك هنا أو اضغط لرفع ملحقات المشروع للوكالة
                    </div>
                </div>

                <!-- ميزة 17 و 14: فريق العمل والتواصل -->
                <div class="card-box">
                    <h3>مدير المشروع المباشر</h3>
                    <div style="display: flex; align-items: center; gap: 12px; margin-bottom: 15px;">
                        <div style="width: 45px; height: 45px; background: var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #0f172a;">MK</div>
                        <div>
                            <strong style="display: block; font-size: 14px;">محمد عنتر</strong>
,                            <span style="font-size: 12px; color: var(--text-muted);">المؤسس والمدير التقني</span>
                        </div>
                    </div>
                    <!-- ميزة 14: تواصل واتساب -->
                    <a href="https://whatsapp.com" target="_blank" style="display: block; text-align: center; background: #25d366; color: #fff; padding: 10px; border-radius: 8px; text-decoration: none; font-weight: bold; font-size: 14px;">💬 تواصل سريع عبر واتساب</a>
                </div>
            </div>

            <!-- ميزة 9: جدول الفواتير المالي -->
            <div class="card-box">
                <h3>سجل الفواتير والمعاملات المالية</h3>
                <table class="table-custom">
                    <thead>
                        <tr>
                            <th>رقم الفاتورة</th>
                            <th>الخدمة</th>
                            <th>المبلغ</th>
                            <th>الحالة</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>#MK-801</td>
                            <td>تطوير وتصميم بوابة العملاء</td>
                            <td>$1,500</td>
                            <td><span style="color: var(--success); background: rgba(34,197,94,0.1); padding: 2px 8px; border-radius: 4px;">مدفوع</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- ميزة 11 و 18: التقييم والأسئلة الشائعة -->
            <div class="grid-2">
                <div class="card-box">
                    <h3>تقييم أداء الوكالة (CSAT)</h3>
                    <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 10px;">ما مدى رضاك عن مستوى العمل المقدم حتى الآن؟</p>
                    <div class="star-rating" onclick="alert('شكراً لتقييمك الرائع! نعمل دائماً لتقديم الأفضل.')">
                        ★ ★ ★ ★ ★
                    </div>
                </div>

                <div class="card-box">
                    <h3>الأسئلة الشائعة (FAQ)</h3>
                    <details style="font-size: 13px; color: var(--text-muted); cursor: pointer;">
                        <summary style="color: var(--text-main); font-weight: 500; margin-bottom: 5px;">كيف يتم تسليم الملفات النهائية؟</summary>
                        يتم إرسال كافة الروابط والمصادر البرمجية مباشرة عبر هذه الداشبورد ومستودع GitHub.
                    </details>
                </div>
            </div>
        </main>
    </div>

    <script>
        const validCodes = {
            "M": { name: "محمد عنتر", project: "بوابة العملاء الاحترافية (SaaS Portal)", link: "https://github.com" }
        };

        window.onload = function() {
            const saved = localStorage.getItem('mk_pro_session');
            if (saved) showDashboard(JSON.parse(saved));
        };

        function login() {
            const code = document.getElementById('clientCode').value.trim().toUpperCase();
            if (validCodes[code]) {
                const data = validCodes[code];
                localStorage.setItem('mk_pro_session', JSON.stringify(data));
                showDashboard(data);
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

        function showDashboard(data) {
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('dashboardSection').style.display = 'grid';
            document.getElementById('clientName').innerText = data.name;
            document.getElementById('projectName').innerText = data.project;
            document.getElementById('projectLink').href = data.link;
        }

        function logout() {
            localStorage.removeItem('mk_pro_session');
            location.reload();
        }

        // ميزة 1: تبديل الثيم
        function toggleTheme() {
            if (document.documentElement.getAttribute('data-theme') === 'light') {
                document.documentElement.removeAttribute('data-theme');
            } else {
                document.documentElement.setAttribute('data-theme', 'light');
            }
        }

        // ميزة 2: ملء الشاشة
        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen();
            } else {
                if (document.exitFullscreen) document.exitFullscreen();
            }
        }

        // ميزة 10: نسخ الرابط
        function copyProjectLink() {
            navigator.clipboard.writeText("https://github.com");
            alert("تم نسخ رابط المشروع بنجاح إلى الحافظة!");
        }

        // ميزة 13: تصدير التقرير
        function exportReport() {
            alert("جاري تجهيز وتصدير تقرير المشروع بصيغة PDF...");
        }

        // ميزة 4: فلتر البحث السريع
        function quickFilter() {
            let val = document.getElementById('quickSearch').value;
            if(val) console.log("Searching for: ", val);
        }
    </script>
</body>
</html>
