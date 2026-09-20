<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative | لوحة تحكم العملاء</title>
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

        .login-wrapper { width: 100%; max-width: 420px; padding: 20px; }
        .login-card {
            background: var(--bg-card); border: 1px solid var(--border-color);
            padding: 40px 30px; border-radius: 16px; box-shadow: 0 15px 30px rgba(0,0,0,0.3); text-align: center;
        }
        .login-card h2 { color: var(--accent); font-size: 24px; margin-bottom: 10px; }
        .login-card p { color: var(--text-muted); font-size: 14px; margin-bottom: 25px; }
        .login-card input {
            width: 100%; padding: 12px 14px; background: var(--bg-main); border: 1px solid var(--border-color);
            border-radius: 10px; color: var(--text-main); font-size: 15px; outline: none; margin-bottom: 15px; text-align: right;
        }
        .btn-login {
            width: 100%; padding: 12px; background: var(--accent); border: none; border-radius: 10px;
            color: #0f172a; font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.2s;
        }
        .btn-login:hover { opacity: 0.9; }
        .error-msg { color: var(--danger); font-size: 13px; margin-top: 10px; display: none; }

        .dashboard-container { display: none; width: 100vw; height: 100vh; grid-template-columns: 260px 1fr; background: var(--bg-main); position: relative; }
        
        .sidebar { background: var(--bg-sidebar); border-left: 1px solid var(--border-color); padding: 25px 20px; display: flex; flex-direction: column; justify-content: space-between; transition: 0.3s; z-index: 100; }
        .sidebar-brand { font-size: 20px; font-weight: bold; color: var(--accent); margin-bottom: 30px; text-align: center; }
        .sidebar-menu { list-style: none; display: flex; flex-direction: column; gap: 8px; }
        .sidebar-menu li { padding: 12px 15px; border-radius: 8px; color: var(--text-muted); cursor: pointer; font-size: 15px; transition: 0.2s; display: flex; align-items: center; gap: 10px; }
        .sidebar-menu li.active, .sidebar-menu li:hover { background: rgba(56, 189, 248, 0.1); color: var(--accent); font-weight: 500; }
        
        .main-content { padding: 25px; overflow-y: auto; width: 100%; }
        .top-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; background: var(--bg-card); padding: 15px 20px; border-radius: 12px; border: 1px solid var(--border-color); }
        
        .header-actions { display: flex; align-items: center; gap: 12px; }
        .icon-btn { background: var(--bg-main); border: 1px solid var(--border-color); color: var(--text-main); width: 38px; height: 38px; border-radius: 8px; cursor: pointer; display: flex; align-items: center; justify-content: center; transition: 0.2s; }
        .icon-btn:hover { border-color: var(--accent); }
        
        .menu-toggle { display: none; background: transparent; border: none; color: var(--text-main); font-size: 22px; cursor: pointer; }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px; margin-bottom: 25px; }
        .stat-card { background: var(--bg-card); border: 1px solid var(--border-color); padding: 18px; border-radius: 12px; }
        .stat-card span { font-size: 13px; color: var(--text-muted); display: block; margin-bottom: 6px; }
        .stat-card h3 { font-size: 18px; font-weight: bold; color: var(--text-main); }

        .grid-2 { display: grid; grid-template-columns: 2fr 1fr; gap: 20px; margin-bottom: 20px; }
        .card-box { background: var(--bg-card); border: 1px solid var(--border-color); padding: 20px; border-radius: 12px; margin-bottom: 20px; }
        .card-box h3 { font-size: 16px; color: var(--accent); margin-bottom: 15px; border-bottom: 1px solid var(--border-color); padding-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }

        .upload-zone { border: 2px dashed var(--border-color); padding: 20px; text-align: center; border-radius: 8px; cursor: pointer; color: var(--text-muted); font-size: 14px; transition: 0.2s; }
        .upload-zone:hover { border-color: var(--accent); color: var(--accent); }

        .star-rating { display: flex; gap: 5px; font-size: 20px; cursor: pointer; color: var(--warning); }

        .faq-item { margin-bottom: 12px; border-bottom: 1px solid var(--border-color); padding-bottom: 10px; }
        .faq-item summary { color: var(--text-main); font-weight: 500; font-size: 14px; cursor: pointer; margin-bottom: 4px; }
        .faq-item p { font-size: 13px; color: var(--text-muted); line-height: 1.5; }

        .content-section { display: none; }
        .content-section.active-section { display: block; }

        .btn-main { background: var(--accent); color: #0f172a; border: none; padding: 10px 16px; border-radius: 8px; font-weight: bold; cursor: pointer; text-decoration: none; display: inline-block; font-size: 14px; text-align: center; }
        .btn-outline { background: transparent; border: 1px solid var(--border-color); color: var(--text-main); padding: 8px 14px; border-radius: 8px; cursor: pointer; }
        
        .whatsapp-btn { background: #25d366; color: #fff; text-decoration: none; display: block; text-align: center; padding: 12px; border-radius: 8px; font-weight: bold; font-size: 14px; transition: 0.2s; }
        .whatsapp-btn:hover { opacity: 0.9; }

        /* تعديلات الموبايل ووضع الاستجابة */
        @media (max-width: 900px) {
            .dashboard-container { grid-template-columns: 1fr; }
            .sidebar { position: fixed; right: -280px; top: 0; height: 100vh; width: 260px; box-shadow: -5px 0 25px rgba(0,0,0,0.5); }
            .sidebar.mobile-open { right: 0; }
            .menu-toggle { display: flex; align-items: center; justify-content: center; }
            .grid-2 { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- 1. شاشة تسجيل الدخول وإدخال بيانات العميل الحقيقية -->
    <div id="loginSection" class="login-wrapper">
        <div class="login-card">
            <h2>MK Creative Agency</h2>
            <p>أدخل بياناتك الحقيقية وكود الدخول (M) للبدء</p>
            <input type="text" id="clientNameInput" placeholder="اسمك الكريم (مثال: محمد عنتر)">
            <input type="email" id="clientEmailInput" placeholder="البريد الإلكتروني">
            <input type="tel" id="clientPhoneInput" placeholder="رقم الهاتف">
            <input type="text" id="clientCode" placeholder="كود الوصول (M)" maxlength="3" style="letter-spacing: 2px; text-align: center;">
            <button class="btn-login" onclick="login()">دخول للنظام</button>
            <div id="error" class="error-msg">الرجاء إدخال كافة البيانات وتأكد أن الكود M.</div>
        </div>
    </div>

    <!-- 2. لوحة التحكم -->
    <div id="dashboardSection" class="dashboard-container">
        
        <!-- القائمة الجانبية -->
        <aside class="sidebar" id="sidebarMenu">
            <div>
                <div class="sidebar-brand">MK CREATIVE</div>
                <ul class="sidebar-menu">
                    <li class="active" onclick="switchSection('dashboard', this)">📊 لوحة القيادة</li>
                    <li onclick="switchSection('projects', this)">📂 مشاريعي</li>
                    <li onclick="switchSection('support', this)">💬 الدعم والأسئلة</li>
                    <li onclick="switchSection('estimator', this)">🧮 حاسبة المشاريع <span style="font-size:10px; background:var(--accent); color:#0f172a; padding:2px 5px; border-radius:4px; font-weight:bold;">جديد</span></li>
                    <li onclick="switchSection('settings', this)">⚙️ الإعدادات</li>
                </ul>
            </div>
            <div>
                <button class="btn-outline" style="width:100%; color:var(--danger); border-color:var(--danger);" onclick="logout()">تسجيل خروج</button>
            </div>
        </aside>

        <!-- المحتوى الرئيسي -->
        <main class="main-content">
            <div class="top-header">
                <div style="display: flex; align-items: center; gap: 15px;">
                    <button class="menu-toggle" onclick="toggleMobileSidebar()">☰</button>
                    <div>
                        <h1 style="font-size: 18px;">مرحباً، <span id="clientNameDisplay">عزيزي العميل</span> 👋</h1>
                        <span style="font-size: 13px; color: var(--text-muted);">متابعة مشاريع وخدمات وكالة MK Creative</span>
                    </div>
                </div>
                <div class="header-actions">
                    <button class="icon-btn" onclick="toggleTheme()" title="تبديل الثيم">🌙</button>
                    <button class="icon-btn" onclick="toggleFullscreen()" title="ملء الشاشة">⛶</button>
                </div>
            </div>

            <!-- القسم 1: لوحة القيادة -->
            <div id="section-dashboard" class="content-section active-section">
                <div class="stats-grid">
                    <div class="stat-card">
                        <span>المشروع الحالي</span>
                        <h3>لا يوجد مشروع نشط</h3>
                    </div>
                    <div class="stat-card">
                        <span>حالة الحساب</span>
                        <h3 style="color: var(--success);">نشط ومعتمد</h3>
                    </div>
                    <div class="stat-card">
                        <span>حالة الأنظمة</span>
                        <h3 style="color: var(--success);">تعمل بكفاءة عالية</h3>
                    </div>
                </div>

                <div class="grid-2">
                    <div class="card-box">
                        <h3>إضافة 1: سجل النشاط الحي للجلسة</h3>
                        <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 12px;">تتبع تفاعلاتك الأخيرة داخل المنصة:</p>
                        <div id="activityLogBox" style="background: var(--bg-main); padding: 12px; border-radius: 8px; border: 1px solid var(--border-color); font-size: 12px; color: var(--text-muted); display: flex; flex-direction: column; gap: 6px;">
                            <span>• تم تسجيل الدخول بنجاح إلى النظام.</span>
                        </div>
                    </div>

                    <div class="card-box">
                        <h3>إضافة 2: التواصل والنسخ السريع</h3>
                        <div style="display: flex; align-items: center; gap: 12px; margin-bottom: 12px;">
                            <div style="width: 40px; height: 40px; background: var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #0f172a; font-size: 13px;">MK</div>
                            <div>
                                <strong style="display: block; font-size: 14px;">محمد عنتر</strong>
                                <span style="font-size: 12px; color: var(--text-muted);">إدارة وكالة MK Creative</span>
                            </div>
                        </div>
                        <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 10px;" id="contactInfoText">📧 moamedantar8@gmail.com | 📱 01559719175</p>
                        <button class="btn-outline" style="width:100%; margin-bottom: 10px; font-size: 13px;" onclick="copyContactInfo()">📋 نسخ بيانات التواصل السريعة</button>
                        <a href="https://wa.me/201559719175?text=مرحباً%20محمد،%20أرغب%20في%20الاستفسار%20عن%20خدمات%20الوكالة" target="_blank" class="whatsapp-btn">💬 تواصل مباشر عبر واتساب</a>
                    </div>
                </div>

                <div class="card-box">
                    <h3>إضافة 3: مساحة الملاحظات السريعة للعميل</h3>
                    <textarea id="quickClientNote" placeholder="اكتب أي ملاحظة أو فكرة ترغب في إرسالها للوكالة هنا..." style="width:100%; background:var(--bg-main); border:1px solid var(--border-color); color:var(--text-main); padding:12px; border-radius:8px; font-size:14px; outline:none; margin-bottom:10px; height:80px; resize:none;"></textarea>
                    <button class="btn-main" onclick="saveClientNote()">حفظ الملاحظة محلياً</button>
                </div>
            </div>

            <!-- القسم 2: مشاريعي (لا توجد مشاريع حالياً + طلب مشروع عبر الواتس) -->
            <div id="section-projects" class="content-section">
                <div class="card-box" style="text-align: center; padding: 40px 20px;">
                    <div style="font-size: 48px; margin-bottom: 15px;">📂</div>
                    <h3 style="justify-content: center; border: none; font-size: 20px; margin-bottom: 10px;">لا توجد مشاريع حاليا</h3>
                    <p style="color: var(--text-muted); font-size: 14px; margin-bottom: 25px; max-width: 400px; margin-left: auto; margin-right: auto;">يبدو أنك لم تقم ببدء أي مشروع برمجى أو إبداعي معنا حتى الآن. جاهز لتحويل فكرتك إلى واقع؟</p>
                    <a href="https://wa.me/201559719175?text=السلام%20عليكم%20محمد،%20أرغب%20في%20طلب%20مشروع%20جديد%20مع%20وكالة%20MK%20Creative" target="_blank" class="whatsapp-btn" style="max-width: 250px; margin: 0 auto;">🚀 طلب مشروع جديد عبر واتساب</a>
                </div>
            </div>

            <!-- القسم 3: الدعم الفني والأسئلة الشائعة -->
            <div id="section-support" class="content-section">
                <div class="card-box">
                    <h3>الأسئلة الشائعة (FAQ)</h3>
                    
                    <details class="faq-item">
                        <summary>كيف تبدأ العمل معنا على مشروعك الجديد؟</summary>
                        <p>بكل بساطة يمكنك الضغط على زر "طلب مشروع جديد" وتواصل معنا مباشرة عبر الواتساب لتحديد المتطلبات والأهداف.</p>
                    </details>

                    <details class="faq-item">
                        <summary>ما هي المدة الزمنية المتوقعة لتنفيذ المشاريع؟</summary>
                        <p>تختلف المدة حسب حجم وتعقيد المشروع، وعادة تتراوح المشاريع المصغرة بين أيام قليلة إلى أسبوعين.</p>
                    </details>

                    <details class="faq-item">
                        <summary>هل أحصل على الكود المصدري كاملاً بعد الانتهاء؟</summary>
                        <p>نعم، يتم تسليمك كافة ملفات الكود المصدري (Source Code) والروابط الخاصة بالمشروع بالكامل.</p>
                    </details>

                    <details class="faq-item">
                        <summary>هل تقدمون صيانة ودعم فني بعد التسليم؟</summary>
                        <p>بالتأكيد، نوفر الدعم المستمر وصيانة الأكواد لضمان عمل المنصة بأعلى كفاءة ممكنة.</p>
                    </details>

                    <details class="faq-item">
                        <summary>كيف يمكنني متابعة حالة التحديثات؟</summary>
                        <p>يمكنك متابعة التحديثات عبر لوحة القيادة الخاصة بك أو من خلال التواصل المباشر مع فريق الوكالة.</p>
                    </details>

                    <details class="faq-item">
                        <summary>ما هي طرق الدفع المتاحة للخدمات؟</summary>
                        <p>نقبل التحويلات البنكية ومحافظ الهاتف المحمول وطرق الدفع الإلكترونية المتاحة.</p>
                    </details>
                </div>
            </div>

            <!-- القسم 4: حاسبة المشاريع التقديرية (إضافة تفاعلية) -->
            <div id="section-estimator" class="content-section">
                <div class="card-box">
                    <h3>🧮 حاسبة التقدير الأولي للمشروع</h3>
                    <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 15px;">اختر نوع الخدمة المطلوبة لمعرفة التقدير المبدئي:</p>
                    <select id="projectTypeSelect" style="width:100%; padding:12px; background:var(--bg-main); border:1px solid var(--border-color); color:var(--text-main); border-radius:8px; margin-bottom:15px; outline:none;">
                        <option value="landing">موقع تعريفى / هبوط (Landing Page)</option>
                        <option value="webapp">تطبيق ويب تفاعلى (Web App)</option>
                        <option value="agency">تصميم هوية وتطوير وكالة (Agency Branding)</option>
                    </select>
                    <button class="btn-main" onclick="calculateEstimate()">احسب التقدير المبدئي</button>
                    <div id="estimateResult" style="margin-top: 15px; font-weight: bold; color: var(--accent); font-size: 15px;"></div>
                </div>
            </div>

            <!-- القسم 5: الإعدادات ومعلومات الحساب الحقيقية -->
            <div id="section-settings" class="content-section">
                <div class="card-box">
                    <h3>إعدادات الحساب ومعلوماتك الشخصية</h3>
                    <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 15px;">البيانات المسجلة حالياً في جلستك:</p>
                    <div style="font-size: 14px; color: var(--text-main); display: flex; flex-direction: column; gap: 10px; margin-bottom: 20px; background: var(--bg-main); padding: 15px; border-radius: 8px; border: 1px solid var(--border-color);">
                        <div>👤 الاسم: <strong id="settingsName">-</strong></div>
                        <div>📧 البريد الإلكتروني: <strong id="settingsEmail">-</strong></div>
                        <div>📱 رقم الهاتف: <strong id="settingsPhone">-</strong></div>
                    </div>
                    <button class="btn-outline" style="color:var(--danger); border-color:var(--danger);" onclick="logout()">حذف الجلسة وتسجيل الخروج</button>
                </div>
            </div>

        </main>
    </div>

    <script>
        window.onload = function() {
            const saved = localStorage.getItem('mk_user_session');
            if (saved) {
                showDashboard(JSON.parse(saved));
            }
        };

        function login() {
            const name = document.getElementById('clientNameInput').value.trim();
            const email = document.getElementById('clientEmailInput').value.trim();
            const phone = document.getElementById('clientPhoneInput').value.trim();
            const code = document.getElementById('clientCode').value.trim().toUpperCase();

            if (name && email && phone && code === "M") {
                const data = { name, email, phone };
                localStorage.setItem('mk_user_session', JSON.stringify(data));
                showDashboard(data);
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

        function showDashboard(data) {
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('dashboardSection').style.display = 'grid';
            document.getElementById('clientNameDisplay').innerText = data.name;
            document.getElementById('settingsName').innerText = data.name;
            document.getElementById('settingsEmail').innerText = data.email;
            document.getElementById('settingsPhone').innerText = data.phone;
        }

        function logout() {
            localStorage.removeItem('mk_user_session');
            location.reload();
        }

        // تبديل الأقسام وإغلاق قائمة الموبايل تلقائياً
        function switchSection(sectionId, element) {
            document.querySelectorAll('.content-section').forEach(sec => {
                sec.classList.remove('active-section');
            });
            document.querySelectorAll('.sidebar-menu li').forEach(li => {
                li.classList.remove('active');
            });
            document.getElementById('section-' + sectionId).classList.add('active-section');
            element.classList.add('active');

            // إغلاق القائمة الجانبية تلقائياً في الموبايل عند اختيار قسم
            document.getElementById('sidebarMenu').classList.remove('mobile-open');
            
            logActivity("تم الانتقال إلى قسم: " + element.innerText);
        }

        function toggleMobileSidebar() {
            document.getElementById('sidebarMenu').classList.toggle('mobile-open');
        }

        function toggleTheme() {
            if (document.documentElement.getAttribute('data-theme') === 'light') {
                document.documentElement.removeAttribute('data-theme');
                logActivity("تم تفعيل الثيم الداكن.");
            } else {
                document.documentElement.setAttribute('data-theme', 'light');
                logActivity("تم تفعيل الثيم الفاتح.");
            }
        }

        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen();
            } else {
                if (document.exitFullscreen) document.exitFullscreen();
            }
        }

        function copyContactInfo() {
            navigator.clipboard.writeText("moamedantar8@gmail.com - 01559719175");
            alert("تم نسخ بيانات التواصل بنجاح!");
            logActivity("تم نسخ بيانات التواصل السريعة.");
        }

        function saveClientNote() {
            const note = document.getElementById('quickClientNote').value.trim();
            if(note) {
                alert("تم حفظ الملاحظة محلياً بنجاح!");
                logActivity("تم إضافة ملاحظة جديدة.");
                document.getElementById('quickClientNote').value = "";
            } else {
                alert("الرجاء كتابة ملاحظة أولاً.");
            }
        }

        function calculateEstimate() {
            const type = document.getElementById('projectTypeSelect').value;
            let cost = "التكلفة التقديرية تتراوح بين 100$ - 300$ حسب التفاصيل.";
            if(type === "webapp") cost = "التكلفة التقديرية تتراوح بين 300$ - 800$ حسب المتطلبات.";
            if(type === "agency") cost = "التكلفة التقديرية تبدأ من 500$ شاملة الهوية البرمجية.";
            document.getElementById('estimateResult').innerText = cost;
            logActivity("تم استخدام حاسبة التقديرات.");
        }

        function logActivity(text) {
            const box = document.getElementById('activityLogBox');
            const span = document.createElement('span');
            span.innerText = "• " + text;
            box.prepend(span);
        }
    </script>
</body>
</html>
