<!DOCTYPE html>
<html lang="ar" dir="rtl" id="htmlRoot">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creative | Client Dashboard</title>
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
            border-radius: 10px; color: var(--text-main); font-size: 15px; outline: none; margin-bottom: 15px; 
        }
        .btn-login {
            width: 100%; padding: 12px; background: var(--accent); border: none; border-radius: 10px;
            color: #0f172a; font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.2s;
        }
        .btn-login:hover { opacity: 0.9; }
        .error-msg { color: var(--danger); font-size: 13px; margin-top: 10px; display: none; }

        .dashboard-container { display: none; width: 100vw; height: 100vh; grid-template-columns: 260px 1fr; background: var(--bg-main); position: relative; }
        
        .sidebar { background: var(--bg-sidebar); border-color: var(--border-color); padding: 25px 20px; display: flex; flex-direction: column; justify-content: space-between; transition: 0.3s; z-index: 100; }
        html[dir="rtl"] .sidebar { border-left: 1px solid var(--border-color); }
        html[dir="ltr"] .sidebar { border-right: 1px solid var(--border-color); }

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

        .faq-item { margin-bottom: 12px; border-bottom: 1px solid var(--border-color); padding-bottom: 10px; }
        .faq-item summary { color: var(--text-main); font-weight: 500; font-size: 14px; cursor: pointer; margin-bottom: 4px; }
        .faq-item p { font-size: 13px; color: var(--text-muted); line-height: 1.5; }

        .content-section { display: none; }
        .content-section.active-section { display: block; }

        .btn-main { background: var(--accent); color: #0f172a; border: none; padding: 10px 16px; border-radius: 8px; font-weight: bold; cursor: pointer; text-decoration: none; display: inline-block; font-size: 14px; text-align: center; }
        .btn-outline { background: transparent; border: 1px solid var(--border-color); color: var(--text-main); padding: 8px 14px; border-radius: 8px; cursor: pointer; }
        
        .whatsapp-btn { background: #25d366; color: #fff; text-decoration: none; display: block; text-align: center; padding: 12px; border-radius: 8px; font-weight: bold; font-size: 14px; transition: 0.2s; }
        .whatsapp-btn:hover { opacity: 0.9; }

        @media (max-width: 900px) {
            .dashboard-container { grid-template-columns: 1fr; }
            .sidebar { position: fixed; top: 0; height: 100vh; width: 260px; box-shadow: 0 0 25px rgba(0,0,0,0.5); }
            html[dir="rtl"] .sidebar { right: -280px; }
            html[dir="rtl"] .sidebar.mobile-open { right: 0; }
            html[dir="ltr"] .sidebar { left: -280px; }
            html[dir="ltr"] .sidebar.mobile-open { left: 0; }
            .menu-toggle { display: flex; align-items: center; justify-content: center; }
            .grid-2 { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- 1. شاشة تسجيل الدخول -->
    <div id="loginSection" class="login-wrapper">
        <div class="login-card">
            <h2 data-i18n="agencyName">MK Creative Agency</h2>
            <p data-i18n="loginDesc">أدخل بياناتك الحقيقية وكود الدخول (M) للبدء</p>
            <input type="text" id="clientNameInput" data-i18n-placeholder="namePlaceholder" placeholder="اسمك الكريم (مثال: محمد عنتر)">
            <input type="email" id="clientEmailInput" data-i18n-placeholder="emailPlaceholder" placeholder="البريد الإلكتروني">
            <input type="tel" id="clientPhoneInput" data-i18n-placeholder="phonePlaceholder" placeholder="رقم الهاتف">
            <input type="text" id="clientCode" data-i18n-placeholder="codePlaceholder" placeholder="كود الوصول (M)" maxlength="3" style="letter-spacing: 2px; text-align: center;">
            <button class="btn-login" onclick="login()" data-i18n="loginBtn">دخول للنظام</button>
            <div id="error" class="error-msg" data-i18n="errorMsg">الرجاء إدخال كافة البيانات وتأكد أن الكود M.</div>
        </div>
    </div>

    <!-- 2. لوحة التحكم -->
    <div id="dashboardSection" class="dashboard-container">
        
        <!-- القائمة الجانبية -->
        <aside class="sidebar" id="sidebarMenu">
            <div>
                <div class="sidebar-brand">MK CREATIVE</div>
                <ul class="sidebar-menu">
                    <li class="active" onclick="switchSection('dashboard', this)">📊 <span data-i18n="menuDashboard">لوحة القيادة</span></li>
                    <li onclick="switchSection('projects', this)">📂 <span data-i18n="menuProjects">مشاريعي</span></li>
                    <li onclick="switchSection('support', this)">💬 <span data-i18n="menuSupport">الدعم والأسئلة</span></li>
                    <li onclick="switchSection('estimator', this)">🧮 <span data-i18n="menuEstimator">حاسبة المشاريع</span> <span style="font-size:10px; background:var(--accent); color:#0f172a; padding:2px 5px; border-radius:4px; font-weight:bold;" data-i18n="newTag">جديد</span></li>
                    <li onclick="switchSection('settings', this)">⚙️ <span data-i18n="menuSettings">الإعدادات</span></li>
                </ul>
            </div>
            <div>
                <button class="btn-outline" style="width:100%; color:var(--danger); border-color:var(--danger);" onclick="logout()" data-i18n="logoutBtn">تسجيل خروج</button>
            </div>
        </aside>

        <!-- المحتوى الرئيسي -->
        <main class="main-content">
            <div class="top-header">
                <div style="display: flex; align-items: center; gap: 15px;">
                    <button class="menu-toggle" onclick="toggleMobileSidebar()">☰</button>
                    <div>
                        <h1 style="font-size: 18px;"><span data-i18n="welcomeMsg">مرحباً،</span> <span id="clientNameDisplay">عزيزي العميل</span> 👋</h1>
                        <span style="font-size: 13px; color: var(--text-muted);" data-i18n="subWelcome">متابعة مشاريع وخدمات وكالة MK Creative</span>
                    </div>
                </div>
                <div class="header-actions">
                    <button class="icon-btn" onclick="toggleLanguage()" title="Change Language / تغيير اللغة" style="font-weight: bold; font-size: 13px;" id="langBtn">EN</button>
                    <button class="icon-btn" onclick="toggleTheme()" title="تبديل الثيم">🌙</button>
                    <button class="icon-btn" onclick="toggleFullscreen()" title="ملء الشاشة">⛶</button>
                </div>
            </div>

            <!-- القسم 1: لوحة القيادة -->
            <div id="section-dashboard" class="content-section active-section">
                <div class="stats-grid">
                    <div class="stat-card">
                        <span data-i18n="stat1Title">المشروع الحالي</span>
                        <h3 data-i18n="stat1Val">لا يوجد مشروع نشط</h3>
                    </div>
                    <div class="stat-card">
                        <span data-i18n="stat2Title">حالة الحساب</span>
                        <h3 style="color: var(--success);" data-i18n="stat2Val">نشط ومعتمد</h3>
                    </div>
                    <div class="stat-card">
                        <span data-i18n="stat3Title">حالة الأنظمة</span>
                        <h3 style="color: var(--success);" data-i18n="stat3Val">تعمل بكفاءة عالية</h3>
                    </div>
                </div>

                <div class="grid-2">
                    <div class="card-box">
                        <h3 data-i18n="box1Title">إضافة 1: سجل النشاط الحي للجلسة</h3>
                        <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 12px;" data-i18n="box1Desc">تتبع تفاعلاتك الأخيرة داخل المنصة:</p>
                        <div id="activityLogBox" style="background: var(--bg-main); padding: 12px; border-radius: 8px; border: 1px solid var(--border-color); font-size: 12px; color: var(--text-muted); display: flex; flex-direction: column; gap: 6px;">
                            <span data-i18n="logInit">• تم تسجيل الدخول بنجاح إلى النظام.</span>
                        </div>
                    </div>

                    <div class="card-box">
                        <h3 data-i18n="box2Title">إضافة 2: التواصل والنسخ السريع</h3>
                        <div style="display: flex; align-items: center; gap: 12px; margin-bottom: 12px;">
                            <div style="width: 40px; height: 40px; background: var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #0f172a; font-size: 13px;">MK</div>
                            <div>
                                <strong style="display: block; font-size: 14px;" data-i18n="ownerName">محمد عنتر</strong>
                                <span style="font-size: 12px; color: var(--text-muted);" data-i18n="ownerRole">إدارة وكالة MK Creative</span>
                            </div>
                        </div>
                        <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 10px;">📧 moamedantar8@gmail.com | 📱 01559719175</p>
                        <button class="btn-outline" style="width:100%; margin-bottom: 10px; font-size: 13px;" onclick="copyContactInfo()" data-i18n="copyBtn">📋 نسخ بيانات التواصل السريعة</button>
                        <a href="https://wa.me/201559719175?text=مرحباً%20محمد،%20أرغب%20في%20الاستفسار%20عن%20خدمات%20الوكالة" target="_blank" class="whatsapp-btn" data-i18n="waBtn">💬 تواصل مباشر عبر واتساب</a>
                    </div>
                </div>

                <div class="card-box">
                    <h3 data-i18n="box3Title">إضافة 3: مساحة الملاحظات السريعة للعميل</h3>
                    <textarea id="quickClientNote" data-i18n-placeholder="notePlaceholder" placeholder="اكتب أي ملاحظة أو فكرة ترغب في إرسالها للوكالة هنا..." style="width:100%; background:var(--bg-main); border:1px solid var(--border-color); color:var(--text-main); padding:12px; border-radius:8px; font-size:14px; outline:none; margin-bottom:10px; height:80px; resize:none;"></textarea>
                    <button class="btn-main" onclick="saveClientNote()" data-i18n="saveNoteBtn">حفظ الملاحظة محلياً</button>
                </div>
            </div>

            <!-- القسم 2: مشاريعي -->
            <div id="section-projects" class="content-section">
                <div class="card-box" style="text-align: center; padding: 40px 20px;">
                    <div style="font-size: 48px; margin-bottom: 15px;">📂</div>
                    <h3 style="justify-content: center; border: none; font-size: 20px; margin-bottom: 10px;" data-i18n="noProjectsTitle">لا توجد مشاريع حاليا</h3>
                    <p style="color: var(--text-muted); font-size: 14px; margin-bottom: 25px; max-width: 400px; margin-left: auto; margin-right: auto;" data-i18n="noProjectsDesc">يبدو أنك لم تقم ببدء أي مشروع برمجى أو إبداعي معنا حتى الآن. جاهز لتحويل فكرتك إلى واقع؟</p>
                    <a href="https://wa.me/201559719175?text=السلام%20عليكم%20محمد،%20أرغب%20في%20طلب%20مشروع%20جديد%20مع%20وكالة%20MK%20Creative" target="_blank" class="whatsapp-btn" style="max-width: 250px; margin: 0 auto;" data-i18n="reqProjectBtn">🚀 طلب مشروع جديد عبر واتساب</a>
                </div>
            </div>

            <!-- القسم 3: الدعم الفني -->
            <div id="section-support" class="content-section">
                <div class="card-box">
                    <h3 data-i18n="faqTitle">الأسئلة الشائعة (FAQ)</h3>
                    <details class="faq-item">
                        <summary data-i18n="faq1Q">كيف تبدأ العمل معنا على مشروعك الجديد؟</summary>
                        <p data-i18n="faq1A">بكل بساطة يمكنك الضغط على زر "طلب مشروع جديد" وتواصل معنا مباشرة عبر الواتساب لتحديد المتطلبات والأهداف.</p>
                    </details>
                    <details class="faq-item">
                        <summary data-i18n="faq2Q">ما هي المدة الزمنية المتوقعة لتنفيذ المشاريع؟</summary>
                        <p data-i18n="faq2A">تختلف المدة حسب حجم وتعقيد المشروع، وعادة تتراوح المشاريع المصغرة بين أيام قليلة إلى أسبوعين.</p>
                    </details>
                    <details class="faq-item">
                        <summary data-i18n="faq3Q">هل أحصل على الكود المصدري كاملاً بعد الانتهاء؟</summary>
                        <p data-i18n="faq3A">نعم، يتم تسليمك كافة ملفات الكود المصدري والروابط الخاصة بالمشروع بالكامل.</p>
                    </details>
                </div>
            </div>

            <!-- القسم 4: حاسبة المشاريع -->
            <div id="section-estimator" class="content-section">
                <div class="card-box">
                    <h3 data-i18n="estTitle">🧮 حاسبة التقدير الأولي للمشروع</h3>
                    <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 15px;" data-i18n="estDesc">اختر نوع الخدمة المطلوبة لمعرفة التقدير المبدئي:</p>
                    <select id="projectTypeSelect" style="width:100%; padding:12px; background:var(--bg-main); border:1px solid var(--border-color); color:var(--text-main); border-radius:8px; margin-bottom:15px; outline:none;">
                        <option value="landing" data-i18n="opt1">موقع تعريفى / هبوط (Landing Page)</option>
                        <option value="webapp" data-i18n="opt2">تطبيق ويب تفاعلى (Web App)</option>
                        <option value="agency" data-i18n="opt3">تصميم هوية وتطوير وكالة (Agency Branding)</option>
                    </select>
                    <button class="btn-main" onclick="calculateEstimate()" data-i18n="calcBtn">احسب التقدير المبدئي</button>
                    <div id="estimateResult" style="margin-top: 15px; font-weight: bold; color: var(--accent); font-size: 15px;"></div>
                </div>
            </div>

            <!-- القسم 5: الإعدادات -->
            <div id="section-settings" class="content-section">
                <div class="card-box">
                    <h3 data-i18n="settingsTitle">إعدادات الحساب ومعلوماتك الشخصية</h3>
                    <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 15px;" data-i18n="settingsDesc">البيانات المسجلة حالياً في جلستك:</p>
                    <div style="font-size: 14px; color: var(--text-main); display: flex; flex-direction: column; gap: 10px; margin-bottom: 20px; background: var(--bg-main); padding: 15px; border-radius: 8px; border: 1px solid var(--border-color);">
                        <div>👤 <span data-i18n="setName">الاسم:</span> <strong id="settingsName">-</strong></div>
                        <div>📧 <span data-i18n="setEmail">البريد الإلكتروني:</span> <strong id="settingsEmail">-</strong></div>
                        <div>📱 <span data-i18n="setPhone">رقم الهاتف:</span> <strong id="settingsPhone">-</strong></div>
                    </div>
                    <button class="btn-outline" style="color:var(--danger); border-color:var(--danger);" onclick="logout()" data-i18n="logoutSessionBtn">حذف الجلسة وتسجيل الخروج</button>
                </div>
            </div>

        </main>
    </div>

    <script>
        // قاموس اللغات (عربي / إنجليزي)
        const translations = {
            ar: {
                agencyName: "MK Creative Agency",
                loginDesc: "أدخل بياناتك الحقيقية وكود الدخول (M) للبدء",
                namePlaceholder: "اسمك الكريم (مثال: محمد عنتر)",
                emailPlaceholder: "البريد الإلكتروني",
                phonePlaceholder: "رقم الهاتف",
                codePlaceholder: "كود الوصول (M)",
                loginBtn: "دخول للنظام",
                errorMsg: "الرجاء إدخال كافة البيانات وتأكد أن الكود M.",
                menuDashboard: "لوحة القيادة",
                menuProjects: "مشاريعي",
                menuSupport: "الدعم والأسئلة",
                menuEstimator: "حاسبة المشاريع",
                newTag: "جديد",
                menuSettings: "الإعدادات",
                logoutBtn: "تسجيل خروج",
                welcomeMsg: "مرحباً،",
                subWelcome: "متابعة مشاريع وخدمات وكالة MK Creative",
                stat1Title: "المشروع الحالي",
                stat1Val: "لا يوجد مشروع نشط",
                stat2Title: "حالة الحساب",
                stat2Val: "نشط ومعتمد",
                stat3Title: "حالة الأنظمة",
                stat3Val: "تعمل بكفاءة عالية",
                box1Title: "إضافة 1: سجل النشاط الحي للجلسة",
                box1Desc: "تتبع تفاعلاتك الأخيرة داخل المنصة:",
                logInit: "• تم تسجيل الدخول بنجاح إلى النظام.",
                box2Title: "إضافة 2: التواصل والنسخ السريع",
                ownerName: "محمد عنتر",
                ownerRole: "إدارة وكالة MK Creative",
                copyBtn: "📋 نسخ بيانات التواصل السريعة",
                waBtn: "💬 تواصل مباشر عبر واتساب",
                box3Title: "إضافة 3: مساحة الملاحظات السريعة للعميل",
                notePlaceholder: "اكتب أي ملاحظة أو فكرة ترغب في إرسالها للوكالة هنا...",
                saveNoteBtn: "حفظ الملاحظة محلياً",
                noProjectsTitle: "لا توجد مشاريع حاليا",
                noProjectsDesc: "يبدو أنك لم تقم ببدء أي مشروع برمجى أو إبداعي معنا حتى الآن. جاهز لتحويل فكرتك إلى واقع؟",
                reqProjectBtn: "🚀 طلب مشروع جديد عبر واتساب",
                faqTitle: "الأسئلة الشائعة (FAQ)",
                faq1Q: "كيف تبدأ العمل معنا على مشروعك الجديد؟",
                faq1A: "بكل بساطة يمكنك الضغط على زر \"طلب مشروع جديد\" وتواصل معنا مباشرة عبر الواتساب لتحديد المتطلبات والأهداف.",
                faq2Q: "ما هي المدة الزمنية المتوقعة لتنفيذ المشاريع؟",
                faq2A: "تختلف المدة حسب حجم وتعقيد المشروع، وعادة تتراوح المشاريع المصغرة بين أيام قليلة إلى أسبوعين.",
                faq3Q: "هل أحصل على الكود المصدري كاملاً بعد الانتهاء؟",
                faq3A: "نعم، يتم تسليمك كافة ملفات الكود المصدري والروابط الخاصة بالمشروع بالكامل.",
                estTitle: "🧮 حاسبة التقدير الأولي للمشروع",
                estDesc: "اختر نوع الخدمة المطلوبة لمعرفة التقدير المبدئي:",
                opt1: "موقع تعريفى / هبوط (Landing Page)",
                opt2: "تطبيق ويب تفاعلى (Web App)",
                opt3: "تصميم هوية وتطوير وكالة (Agency Branding)",
                calcBtn: "احسب التقدير المبدئي",
                settingsTitle: "إعدادات الحساب ومعلوماتك الشخصية",
                settingsDesc: "البيانات المسجلة حالياً في جلستك:",
                setName: "الاسم:",
                setEmail: "البريد الإلكتروني:",
                setPhone: "رقم الهاتف:",
                logoutSessionBtn: "حذف الجلسة وتسجيل الخروج"
            },
            en: {
                agencyName: "MK Creative Agency",
                loginDesc: "Enter your real info and access code (M) to start",
                namePlaceholder: "Your Name (e.g. Mohamed Antar)",
                emailPlaceholder: "Email Address",
                phonePlaceholder: "Phone Number",
                codePlaceholder: "Access Code (M)",
                loginBtn: "Login to System",
                errorMsg: "Please fill all fields and make sure the code is M.",
                menuDashboard: "Dashboard",
                menuProjects: "My Projects",
                menuSupport: "Support & FAQ",
                menuEstimator: "Project Estimator",
                newTag: "NEW",
                menuSettings: "Settings",
                logoutBtn: "Logout",
                welcomeMsg: "Welcome,",
                subWelcome: "Tracking MK Creative projects and services",
                stat1Title: "Current Project",
                stat1Val: "No active project",
                stat2Title: "Account Status",
                stat2Val: "Active & Verified",
                stat3Title: "Systems Status",
                stat3Val: "High Performance",
                box1Title: "Addition 1: Live Session Activity Log",
                box1Desc: "Track your recent platform interactions:",
                logInit: "• Successfully logged in to the system.",
                box2Title: "Addition 2: Quick Contact & Copy",
                ownerName: "Mohamed Antar",
                ownerRole: "MK Creative Management",
                copyBtn: "📋 Copy Quick Contact Details",
                waBtn: "💬 Direct Contact via WhatsApp",
                box3Title: "Addition 3: Client Quick Notes",
                notePlaceholder: "Write any note or idea you want to send to the agency here...",
                saveNoteBtn: "Save Note Locally",
                noProjectsTitle: "No Projects At The Moment",
                noProjectsDesc: "It looks like you haven't started any software or creative project with us yet. Ready to turn your idea into reality?",
                reqProjectBtn: "🚀 Request New Project via WhatsApp",
                faqTitle: "Frequently Asked Questions (FAQ)",
                faq1Q: "How to start working with us on your new project?",
                faq1A: "Simply click 'Request New Project' and contact us directly via WhatsApp to define requirements and goals.",
                faq2Q: "What is the expected timeline for projects?",
                faq2A: "Duration varies based on complexity, usually ranging from a few days to two weeks for small projects.",
                faq3Q: "Do I get the full source code after completion?",
                faq3A: "Yes, you will be provided with all source code files and project links completely.",
                estTitle: "🧮 Initial Project Estimator",
                estDesc: "Select the required service type to see an initial estimate:",
                opt1: "Landing Page",
                opt2: "Interactive Web App",
                opt3: "Agency Branding & Development",
                calcBtn: "Calculate Estimate",
                settingsTitle: "Account Settings & Personal Info",
                settingsDesc: "Currently registered data in your session:",
                setName: "Name:",
                setEmail: "Email:",
                setPhone: "Phone:",
                logoutSessionBtn: "Delete Session & Logout"
            }
        };

        let currentLang = localStorage.getItem('mk_lang') || 'ar';

        window.onload = function() {
            setLanguage(currentLang);
            const saved = localStorage.getItem('mk_user_session');
            if (saved) {
                showDashboard(JSON.parse(saved));
            }
        };

        function toggleLanguage() {
            currentLang = currentLang === 'ar' ? 'en' : 'ar';
            localStorage.setItem('mk_lang', currentLang);
            setLanguage(currentLang);
        }

        function setLanguage(lang) {
            const html = document.getElementById('htmlRoot');
            html.setAttribute('lang', lang);
            html.setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');
            document.getElementById('langBtn').innerText = lang === 'ar' ? 'EN' : 'AR';

            // ترجمة العناصر النصية
            document.querySelectorAll('[data-i18n]').forEach(el => {
                const key = el.getAttribute('data-i18n');
                if(translations[lang][key]) {
                    el.innerText = translations[lang][key];
                }
            });

            // ترجمة الـ placeholders
            document.querySelectorAll('[data-i18n-placeholder]').forEach(el => {
                const key = el.getAttribute('data-i18n-placeholder');
                if(translations[lang][key]) {
                    el.placeholder = translations[lang][key];
                }
            });
        }

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

        function switchSection(sectionId, element) {
            document.querySelectorAll('.content-section').forEach(sec => sec.classList.remove('active-section'));
            document.querySelectorAll('.sidebar-menu li').forEach(li => li.classList.remove('active'));
            document.getElementById('section-' + sectionId).classList.add('active-section');
            element.classList.add('active');
            document.getElementById('sidebarMenu').classList.remove('mobile-open');
            logActivity(currentLang === 'ar' ? "تم الانتقال إلى القسم المحدد." : "Switched to section.");
        }

        function toggleMobileSidebar() {
            document.getElementById('sidebarMenu').classList.toggle('mobile-open');
        }

        function toggleTheme() {
            if (document.documentElement.getAttribute('data-theme') === 'light') {
                document.documentElement.removeAttribute('data-theme');
            } else {
                document.documentElement.setAttribute('data-theme', 'light');
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
            alert(currentLang === 'ar' ? "تم نسخ بيانات التواصل بنجاح!" : "Contact details copied successfully!");
        }

        function saveClientNote() {
            const note = document.getElementById('quickClientNote').value.trim();
            if(note) {
                alert(currentLang === 'ar' ? "تم حفظ الملاحظة محلياً بنجاح!" : "Note saved locally!");
                document.getElementById('quickClientNote').value = "";
            } else {
                alert(currentLang === 'ar' ? "الرجاء كتابة ملاحظة أولاً." : "Please write a note first.");
            }
        }

        function calculateEstimate() {
            const type = document.getElementById('projectTypeSelect').value;
            let cost = currentLang === 'ar' ? "التكلفة التقديرية تتراوح بين 100$ - 300$ حسب التفاصيل." : "Estimated cost ranges between $100 - $300.";
            if(type === "webapp") cost = currentLang === 'ar' ? "التكلفة التقديرية تتراوح بين 300$ - 800$ حسب المتطلبات." : "Estimated cost ranges between $300 - $800.";
            if(type === "agency") cost = currentLang === 'ar' ? "التكلفة التقديرية تبدأ من 500$ شاملة الهوية البرمجية." : "Estimated cost starts from $500 including branding.";
            document.getElementById('estimateResult').innerText = cost;
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
