<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة إنشاء الملف المهني للمعلم</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700&family=Tajawal:wght@300;400;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #1abc9c;
            --light-color: #f8f9fa;
            --dark-color: #2c3e50;
            --success-color: #27ae60;
            --warning-color: #f39c12;
            --border-radius: 8px;
            --box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', 'Cairo', sans-serif;
        }

        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
            padding-top: 80px;
        }

        /* الهيدر العلوي للأداة */
        .tool-header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            z-index: 1000;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-container i {
            font-size: 28px;
            color: var(--accent-color);
        }

        .logo-text h1 {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 3px;
        }

        .logo-text p {
            font-size: 14px;
            opacity: 0.9;
        }

        .teacher-name-display {
            display: flex;
            align-items: center;
            gap: 10px;
            background-color: rgba(255, 255, 255, 0.15);
            padding: 8px 20px;
            border-radius: 50px;
            backdrop-filter: blur(5px);
        }

        .teacher-name-display i {
            color: var(--accent-color);
        }

        .teacher-name-input {
            background: transparent;
            border: none;
            color: white;
            font-size: 18px;
            font-weight: 600;
            width: 250px;
            outline: none;
            text-align: center;
        }

        .teacher-name-input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        /* شريط التنقل بين الأقسام */
        .section-navigator {
            position: sticky;
            top: 70px;
            background-color: white;
            padding: 15px 0;
            box-shadow: var(--box-shadow);
            z-index: 999;
            overflow-x: auto;
            white-space: nowrap;
            margin-bottom: 30px;
        }

        .nav-container {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 0 20px;
        }

        .nav-item {
            padding: 12px 20px;
            background-color: var(--light-color);
            border-radius: var(--border-radius);
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            border: 2px solid transparent;
            color: var(--primary-color);
            font-size: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .nav-item:hover {
            background-color: #e9ecef;
            transform: translateY(-2px);
        }

        .nav-item.active {
            background-color: var(--secondary-color);
            color: white;
            border-color: var(--secondary-color);
        }

        .nav-item i {
            font-size: 16px;
        }

        /* المحتوى الرئيسي */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px 40px;
        }

        .main-title {
            text-align: center;
            margin-bottom: 30px;
            color: var(--primary-color);
        }

        .main-title h2 {
            font-size: 28px;
            margin-bottom: 10px;
            position: relative;
            display: inline-block;
        }

        .main-title h2:after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background-color: var(--accent-color);
            border-radius: 2px;
        }

        /* أقسام النماذج */
        .sections-container {
            display: grid;
            grid-template-columns: 1fr;
            gap: 30px;
        }

        .section-form {
            background-color: white;
            border-radius: var(--border-radius);
            padding: 25px;
            box-shadow: var(--box-shadow);
            display: none;
        }

        .section-form.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f0f0;
        }

        .section-title {
            color: var(--primary-color);
            font-size: 22px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-title i {
            color: var(--secondary-color);
        }

        .ai-button {
            background-color: var(--accent-color);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: var(--border-radius);
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: var(--transition);
        }

        .ai-button:hover {
            background-color: #16a085;
            transform: translateY(-2px);
        }

        .section-content {
            margin-top: 20px;
        }

        .section-label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--primary-color);
            font-size: 16px;
        }

        .section-textarea {
            width: 100%;
            min-height: 200px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: var(--border-radius);
            font-size: 16px;
            line-height: 1.6;
            resize: vertical;
            transition: var(--transition);
            font-family: 'Cairo', sans-serif;
        }

        .section-textarea:focus {
            outline: none;
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }

        /* أزرار التصدير */
        .export-options {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 40px;
            flex-wrap: wrap;
        }

        .export-btn {
            padding: 15px 30px;
            border-radius: var(--border-radius);
            font-weight: 700;
            font-size: 17px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: var(--transition);
            border: none;
            min-width: 200px;
            justify-content: center;
        }

        .export-btn.html {
            background-color: var(--primary-color);
            color: white;
        }

        .export-btn.excel {
            background-color: var(--success-color);
            color: white;
        }

        .export-btn.preview {
            background-color: var(--warning-color);
            color: white;
        }

        .export-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }

        .export-btn.html:hover {
            background-color: #1a252f;
        }

        .export-btn.excel:hover {
            background-color: #219653;
        }

        .export-btn.preview:hover {
            background-color: #e67e22;
        }

        /* معاينة الملف المهني */
        .preview-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 1100;
            overflow-y: auto;
            padding: 20px;
        }

        .preview-content {
            background-color: white;
            max-width: 900px;
            margin: 30px auto;
            border-radius: var(--border-radius);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            overflow: hidden;
            animation: modalFadeIn 0.3s ease;
        }

        @keyframes modalFadeIn {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .preview-header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 25px;
            text-align: center;
        }

        .preview-header h3 {
            font-size: 28px;
            margin-bottom: 10px;
        }

        .preview-body {
            padding: 30px;
            max-height: 70vh;
            overflow-y: auto;
        }

        .preview-section {
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid #eee;
        }

        .preview-section:last-child {
            border-bottom: none;
        }

        .preview-section h4 {
            color: var(--primary-color);
            font-size: 20px;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 2px solid var(--accent-color);
            display: inline-block;
        }

        .preview-section p {
            line-height: 1.7;
            font-size: 16px;
            color: #444;
        }

        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            background-color: rgba(255, 255, 255, 0.2);
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            cursor: pointer;
            transition: var(--transition);
        }

        .modal-close:hover {
            background-color: rgba(255, 255, 255, 0.3);
            transform: rotate(90deg);
        }

        /* التكيف مع الأجهزة المحمولة */
        @media (max-width: 992px) {
            .nav-container {
                justify-content: flex-start;
            }
            
            .export-btn {
                min-width: 180px;
            }
        }

        @media (max-width: 768px) {
            .tool-header {
                flex-direction: column;
                gap: 15px;
                padding: 15px;
            }
            
            .teacher-name-input {
                width: 100%;
            }
            
            .section-navigator {
                top: 130px;
            }
            
            .section-header {
                flex-direction: column;
                gap: 15px;
                align-items: flex-start;
            }
            
            .export-options {
                flex-direction: column;
                align-items: center;
            }
            
            .export-btn {
                width: 100%;
                max-width: 300px;
            }
            
            body {
                padding-top: 150px;
            }
        }

        @media (max-width: 576px) {
            .nav-container {
                gap: 5px;
            }
            
            .nav-item {
                padding: 10px 15px;
                font-size: 14px;
            }
            
            .section-form {
                padding: 20px 15px;
            }
            
            .preview-content {
                margin: 10px auto;
            }
        }
    </style>
</head>
<body>
    <!-- هيدر الأداة -->
    <header class="tool-header">
        <div class="logo-container">
            <i class="fas fa-chalkboard-teacher"></i>
            <div class="logo-text">
                <h1>أداة الملف المهني للمعلم</h1>
                <p>أنشئ ملفك المهني باحترافية</p>
            </div>
        </div>
        
        <div class="teacher-name-display">
            <i class="fas fa-user-graduate"></i>
            <input type="text" id="teacherName" class="teacher-name-input" placeholder="أدخل اسمك هنا" maxlength="50">
        </div>
    </header>

    <!-- شريط التنقل بين الأقسام -->
    <nav class="section-navigator">
        <div class="nav-container">
            <div class="nav-item active" data-section="about">
                <i class="fas fa-user"></i>
                <span>نبذة عني</span>
            </div>
            <div class="nav-item" data-section="vision">
                <i class="fas fa-eye"></i>
                <span>الرؤية التعليمية</span>
            </div>
            <div class="nav-item" data-section="experience">
                <i class="fas fa-briefcase"></i>
                <span>الخبرات</span>
            </div>
            <div class="nav-item" data-section="achievements">
                <i class="fas fa-trophy"></i>
                <span>الإنجازات</span>
            </div>
            <div class="nav-item" data-section="courses">
                <i class="fas fa-certificate"></i>
                <span>الدورات التدريبية</span>
            </div>
            <div class="nav-item" data-section="skills">
                <i class="fas fa-star"></i>
                <span>المهارات</span>
            </div>
            <div class="nav-item" data-section="performance">
                <i class="fas fa-chart-line"></i>
                <span>شواهد الأداء</span>
            </div>
            <div class="nav-item" data-section="portfolio">
                <i class="fas fa-images"></i>
                <span>معرض الأعمال</span>
            </div>
            <div class="nav-item" data-section="contact">
                <i class="fas fa-address-card"></i>
                <span>بيانات التواصل</span>
            </div>
        </div>
    </nav>

    <!-- المحتوى الرئيسي -->
    <main class="container">
        <div class="main-title">
            <h2>أدخل بيانات الملف المهني</h2>
            <p>املأ الأقسام التالية لإنشاء ملفك المهني الاحترافي</p>
        </div>

        <!-- أقسام النماذج -->
        <div class="sections-container">
            <!-- قسم نبذة عني -->
            <div class="section-form active" id="about-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-user"></i> نبذة عني</h3>
                    <button class="ai-button" data-section="about">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اكتب نبذة مختصرة عن نفسك وخبراتك التعليمية</label>
                    <textarea class="section-textarea" id="about-text" placeholder="أنا معلم متخصص في [التخصص] مع أكثر من [عدد] سنوات من الخبرة في تدريس [المادة/المرحلة]، أحب تطوير أساليب التدريس وتبني استراتيجيات تعليمية تفاعلية تهدف إلى تحسين نتائج الطلاب وغرس حب التعلم لديهم..."></textarea>
                </div>
            </div>

            <!-- قسم الرؤية التعليمية -->
            <div class="section-form" id="vision-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-eye"></i> الرؤية التعليمية</h3>
                    <button class="ai-button" data-section="vision">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اكتب رؤيتك التعليمية وأهدافك التربوية</label>
                    <textarea class="section-textarea" id="vision-text" placeholder="أتطلع إلى إنشاء بيئة تعليمية محفزة تمكن الطلاب من اكتشاف قدراتهم الكامنة وتطوير مهارات التفكير النقدي والإبداعي لديهم. أؤمن بأن التعليم يجب أن يكون تجربة ممتعة وشاملة تركز على تنمية الشخصية وتقدير التعلم مدى الحياة..."></textarea>
                </div>
            </div>

            <!-- قسم الخبرات -->
            <div class="section-form" id="experience-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-briefcase"></i> الخبرات</h3>
                    <button class="ai-button" data-section="experience">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اذكر خبراتك التدريسية والعملية</label>
                    <textarea class="section-textarea" id="experience-text" placeholder="• معلم مادة [المادة] في [المدرسة] (2020 - حتى الآن)
• معلم مساعد في [المؤسسة التعليمية] (2018 - 2020)
• مشرف نادي القراءة والنشاط الثقافي (2019 - حتى الآن)
• عضو في فريق تطوير المناهج بالمدرسة (2021)
• مشارك في برنامج التطوير المهني للمعلمين (2022)"></textarea>
                </div>
            </div>

            <!-- قسم الإنجازات -->
            <div class="section-form" id="achievements-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-trophy"></i> الإنجازات</h3>
                    <button class="ai-button" data-section="achievements">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اذكر أبرز إنجازاتك المهنية</label>
                    <textarea class="section-textarea" id="achievements-text" placeholder="• الحصول على جائزة المعلم المتميز على مستوى المنطقة (2023)
• تحقيق أعلى نسبة نجاح في مادة [المادة] بالمدرسة (2022)
• تطوير برنامج تعليمي تفاعلي حاز على إشادة الإدارة التعليمية
• تدريب 15 معلماً جديداً على استراتيجيات التعلم النشط
• تنظيم معرض لإبداعات الطلاب بمشاركة 200 طالب"></textarea>
                </div>
            </div>

            <!-- قسم الدورات التدريبية -->
            <div class="section-form" id="courses-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-certificate"></i> الدورات التدريبية</h3>
                    <button class="ai-button" data-section="courses">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اذخر الدورات والبرامج التدريبية التي حضرتها</label>
                    <textarea class="section-textarea" id="courses-text" placeholder="• دورة استراتيجيات التعلم النشط - مركز التدريب التربوي (2023)
• برنامج دمج التقنية في التعليم - وزارة التعليم (2022)
• دورة التخطيط للدرس وفق المنهج المطور (40 ساعة) - 2021
• ورشة بناء الاختبارات التحصيلية - إدارة التعليم (2020)
• دورة الإسعافات الأولية في البيئة المدرسية (2019)"></textarea>
                </div>
            </div>

            <!-- قسم المهارات -->
            <div class="section-form" id="skills-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-star"></i> المهارات</h3>
                    <button class="ai-button" data-section="skills">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اذكر مهاراتك الشخصية والمهنية</label>
                    <textarea class="section-textarea" id="skills-text" placeholder="• التخطيط للدروس وإعداد المواد التعليمية
• استخدام التقنية في التعليم (منصات التعلم الإلكتروني، التطبيقات التعليمية)
• إدارة الصف وتنظيم بيئة تعليمية محفزة
• التواصل الفعال مع أولياء الأمور والزملاء
• تطبيق استراتيجيات التعلم النشط والتعلم التعاوني
• تحليل نتائج الطلاب وتقييم أدائهم
• اللغة الإنجليزية (مستوى متقدم)"></textarea>
                </div>
            </div>

            <!-- قسم شواهد الأداء -->
            <div class="section-form" id="performance-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-chart-line"></i> شواهد الأداء</h3>
                    <button class="ai-button" data-section="performance">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">اذكر تقييمات أدائك وشهادات التقدير</label>
                    <textarea class="section-textarea" id="performance-text" placeholder="• تقييم أداء ممتاز من قائد المدرسة للعام الدراسي 2022/2023
• شهادة تقدير من إدارة التعليم لتميز الطلاب في الاختبارات الوطنية
• تقييم إيجابي من أولياء الأمور بنسبة 95% وفق استبيان الرضا
• شهادة شكر من مدير التعليم للمشاركة الفاعلة في البرامج التربوية
• تقييم مرتفع في أداء المعلمين من المشرف التربوي (4.8/5)"></textarea>
                </div>
            </div>

            <!-- قسم معرض الأعمال -->
            <div class="section-form" id="portfolio-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-images"></i> معرض الأعمال</h3>
                    <button class="ai-button" data-section="portfolio">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">صف مشاريعك وأعمالك المميزة</label>
                    <textarea class="section-textarea" id="portfolio-text" placeholder="• تصميم دليل تعليمي تفاعلي لطلاب الصف [الصف] في مادة [المادة]
• إنشاء قناة يوتيوب تعليمية تحتوي على 50 فيديو تعليمي
• تطوير نشاط 'رحلة معرفية' حاز على المركز الأول على مستوى المدارس
• تصميم أنشطة تقويمية إلكترونية باستخدام منصة Nearpod
• إعداد معرض 'إبداعات طلابية' ضم 75 عملاً فنياً وأدبياً"></textarea>
                </div>
            </div>

            <!-- قسم بيانات التواصل -->
            <div class="section-form" id="contact-form">
                <div class="section-header">
                    <h3 class="section-title"><i class="fas fa-address-card"></i> بيانات التواصل</h3>
                    <button class="ai-button" data-section="contact">
                        <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                    </button>
                </div>
                <div class="section-content">
                    <label class="section-label">أدخل بيانات التواصل الخاصة بك</label>
                    <textarea class="section-textarea" id="contact-text" placeholder="البريد الإلكتروني: teacher@example.com
رقم الهاتف: +966 55 123 4567
حساب تويتر: @teacher_profile
حساب لينكد إن: linkedin.com/in/teacherprofile
المدينة: الرياض، المملكة العربية السعودية"></textarea>
                </div>
            </div>
        </div>

        <!-- أزرار التصدير -->
        <div class="export-options">
            <button class="export-btn html" id="exportHtml">
                <i class="fas fa-file-code"></i> إنشاء ملف HTML
            </button>
            <button class="export-btn excel" id="exportExcel">
                <i class="fas fa-file-excel"></i> تصدير كملف Excel
            </button>
            <button class="export-btn preview" id="previewBtn">
                <i class="fas fa-eye"></i> معاينة قبل التصدير
            </button>
        </div>
    </main>

    <!-- نافذة معاينة الملف المهني -->
    <div class="preview-modal" id="previewModal">
        <div class="modal-close" id="closePreview">
            <i class="fas fa-times"></i>
        </div>
        <div class="preview-content">
            <div class="preview-header">
                <h3 id="previewTeacherName">اسم المعلم</h3>
                <p>الملف المهني الاحترافي</p>
            </div>
            <div class="preview-body" id="previewBody">
                <!-- سيتم تعبئة المحتوى هنا بالجافاسكريبت -->
            </div>
        </div>
    </div>

    <script>
        // بيانات النصوص الافتراضية لكل قسم
        const defaultTexts = {
            about: "أنا معلم متخصص في [التخصص] مع أكثر من [عدد] سنوات من الخبرة في تدريس [المادة/المرحلة]، أحب تطوير أساليب التدريس وتبني استراتيجيات تعليمية تفاعلية تهدف إلى تحسين نتائج الطلاب وغرس حب التعلم لديهم. أسعى دائمًا لتطوير ذاتي مهنيًا والمشاركة في البرامج التدريبية التي تثري خبراتي التعليمية.",
            vision: "أتطلع إلى إنشاء بيئة تعليمية محفزة تمكن الطلاب من اكتشاف قدراتهم الكامنة وتطوير مهارات التفكير النقدي والإبداعي لديهم. أؤمن بأن التعليم يجب أن يكون تجربة ممتعة وشاملة تركز على تنمية الشخصية وتقدير التعلم مدى الحياة، وليس مجرد نقل للمعلومات.",
            experience: "• معلم مادة [المادة] في [المدرسة] (2020 - حتى الآن)\n• معلم مساعد في [المؤسسة التعليمية] (2018 - 2020)\n• مشرف نادي القراءة والنشاط الثقافي (2019 - حتى الآن)\n• عضو في فريق تطوير المناهج بالمدرسة (2021)\n• مشارك في برنامج التطوير المهني للمعلمين (2022)",
            achievements: "• الحصول على جائزة المعلم المتميز على مستوى المنطقة (2023)\n• تحقيق أعلى نسبة نجاح في مادة [المادة] بالمدرسة (2022)\n• تطوير برنامج تعليمي تفاعلي حاز على إشادة الإدارة التعليمية\n• تدريب 15 معلماً جديداً على استراتيجيات التعلم النشط\n• تنظيم معرض لإبداعات الطلاب بمشاركة 200 طالب",
            courses: "• دورة استراتيجيات التعلم النشط - مركز التدريب التربوي (2023)\n• برنامج دمج التقنية في التعليم - وزارة التعليم (2022)\n• دورة التخطيط للدرس وفق المنهج المطور (40 ساعة) - 2021\n• ورشة بناء الاختبارات التحصيلية - إدارة التعليم (2020)\n• دورة الإسعافات الأولية في البيئة المدرسية (2019)",
            skills: "• التخطيط للدروس وإعداد المواد التعليمية\n• استخدام التقنية في التعليم (منصات التعلم الإلكتروني، التطبيقات التعليمية)\n• إدارة الصف وتنظيم بيئة تعليمية محفزة\n• التواصل الفعال مع أولياء الأمور والزملاء\n• تطبيق استراتيجيات التعلم النشط والتعلم التعاوني\n• تحليل نتائج الطلاب وتقييم أدائهم\n• اللغة الإنجليزية (مستوى متقدم)",
            performance: "• تقييم أداء ممتاز من قائد المدرسة للعام الدراسي 2022/2023\n• شهادة تقدير من إدارة التعليم لتميز الطلاب في الاختبارات الوطنية\n• تقييم إيجابي من أولياء الأمور بنسبة 95% وفق استبيان الرضا\n• شهادة شكر من مدير التعليم للمشاركة الفاعلة في البرامج التربوية\n• تقييم مرتفع في أداء المعلمين من المشرف التربوي (4.8/5)",
            portfolio: "• تصميم دليل تعليمي تفاعلي لطلاب الصف [الصف] في مادة [المادة]\n• إنشاء قناة يوتيوب تعليمية تحتوي على 50 فيديو تعليمي\n• تطوير نشاط 'رحلة معرفية' حاز على المركز الأول على مستوى المدارس\n• تصميم أنشطة تقويمية إلكترونية باستخدام منصة Nearpod\n• إعداد معرض 'إبداعات طلابية' ضم 75 عملاً فنياً وأدبياً",
            contact: "البريد الإلكتروني: teacher@example.com\nرقم الهاتف: +966 55 123 4567\nحساب تويتر: @teacher_profile\nحساب لينكد إن: linkedin.com/in/teacherprofile\nالمدينة: الرياض، المملكة العربية السعودية"
        };

        // نص الذكاء الاصطناعي (محاكاة)
        const aiGeneratedTexts = {
            about: "معلم متخصص في العلوم التربوية مع أكثر من 10 سنوات من الخبرة في تدريس المرحلة الثانوية. أسعى دائمًا لتطوير بيئة تعليمية محفزة للإبداع والتفكير النقدي، مع التركيز على التعلم القائم على المشاريع والتجارب العملية التي تربط المعرفة بالحياة الواقعية.",
            vision: "أطمح إلى تمكين الطلاب من أن يصبحوا متعلمين مستقلين ومواطنين فاعلين في المجتمع. أركز على بناء شخصياتهم وتعزيز الثقة بالنفس من خلال منهجية تعليمية شاملة تجمع بين المعرفة الأكاديمية والمهارات الحياتية.",
            experience: "• معلم مادة الرياضيات في ثانوية النخبة (2018 - حتى الآن)\n• منسق النشاط العلمي بالمدرسة (2020 - حتى الآن)\n• عضو في لجنة التطوير المهني للمعلمين (2021 - حتى الآن)\n• مدرب معتمد في استراتيجيات التعلم النشط (2022)",
            achievements: "• جائزة التميز التعليمي على مستوى المنطقة (2022)\n• تطوير منهج إثرائي في الرياضيات لطلاب الموهوبين\n• قيادة فريق تحسين نتائج الطلاب في الاختبارات الدولية\n• تنظيم مؤتمر علمي مدرسي شارك فيه 300 طالب",
            courses: "• دورة معلمي القرن الحادي والعشرين - مؤسسة التطوير المهني (2023)\n• برنامج التقييم التربوي الفعال - جامعة الملك سعود (2022)\n• دورة التعلم القائم على المشاريع - منصة إدراك (2021)\n• ورشة تصميم الأنشطة التفاعلية - مركز التميز (2020)",
            skills: "• تصميم الدروس التفاعلية باستخدام التقنية\n• إدارة الفصول الدراسية المقلوبة (Flipped Classroom)\n• تطبيق استراتيجيات التعلم التعاوني\n• تحليل البيانات التعليمية لتحسين الأداء\n• التدريب والتوجيه للمعلمين الجدد\n• التواصل مع ذوي الاحتياجات التعليمية الخاصة",
            performance: "• تقييم 'متميز' من الإدارة لمدة 3 سنوات متتالية\n• شهادات تقدير من أولياء أمور الطلاب\n• تقييمات عالية من الطلاب في استبيانات الرضا\n• إشادة من المشرف التربوي بجودة التحضير والتنفيذ",
            portfolio: "• تصميم موقع إلكتروني تعليمي للرياضيات\n• إنتاج سلسلة فيديوهات تعليمية نالت أكثر من 50,000 مشاهدة\n• تطوير تطبيق تعليمي للهواتف الذكية\n• إعداد أبحاث علمية مع طلاب الموهوبين",
            contact: "البريد الإلكتروني: professional.teacher@edu.sa\nرقم الهاتف: +966 50 123 4567\nحساب تويتر: @edu_innovator\nحساب إنستغرام: @teacher_portfolio\nالمدينة: جدة، المملكة العربية السعودية"
        };

        // تهيئة التطبيق
        document.addEventListener('DOMContentLoaded', function() {
            // عناصر DOM الرئيسية
            const teacherNameInput = document.getElementById('teacherName');
            const navItems = document.querySelectorAll('.nav-item');
            const sectionForms = document.querySelectorAll('.section-form');
            const aiButtons = document.querySelectorAll('.ai-button');
            const exportHtmlBtn = document.getElementById('exportHtml');
            const exportExcelBtn = document.getElementById('exportExcel');
            const previewBtn = document.getElementById('previewBtn');
            const previewModal = document.getElementById('previewModal');
            const closePreview = document.getElementById('closePreview');
            
            // تعيين النصوص الافتراضية
            Object.keys(defaultTexts).forEach(sectionId => {
                const textarea = document.getElementById(`${sectionId}-text`);
                if (textarea) {
                    textarea.value = defaultTexts[sectionId];
                }
            });
            
            // تحديث اسم المعلم في الهيدر عند الكتابة
            teacherNameInput.addEventListener('input', function() {
                const name = this.value.trim() || "المعلم";
                this.value = this.value;
            });
            
            // التنقل بين الأقسام
            navItems.forEach(item => {
                item.addEventListener('click', function() {
                    const sectionId = this.getAttribute('data-section');
                    
                    // تحديث العناصر النشطة في شريط التنقل
                    navItems.forEach(navItem => {
                        navItem.classList.remove('active');
                    });
                    this.classList.add('active');
                    
                    // إظهار القسم المحدد وإخفاء الآخرين
                    sectionForms.forEach(form => {
                        form.classList.remove('active');
                    });
                    
                    document.getElementById(`${sectionId}-form`).classList.add('active');
                });
            });
            
            // زر توليد النص بالذكاء الاصطناعي
            aiButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const sectionId = this.getAttribute('data-section');
                    const textarea = document.getElementById(`${sectionId}-text`);
                    
                    if (textarea) {
                        // عرض رسالة تحميل
                        const originalText = this.innerHTML;
                        this.innerHTML = '<i class="fas fa-spinner fa-spin"></i> جاري التوليد...';
                        this.disabled = true;
                        
                        // محاكاة اتصال بالذكاء الاصطناعي
                        setTimeout(() => {
                            textarea.value = aiGeneratedTexts[sectionId];
                            this.innerHTML = originalText;
                            this.disabled = false;
                            
                            // عرض رسالة نجاح
                            showNotification(`تم توليد نص ${getSectionName(sectionId)} بنجاح باستخدام الذكاء الاصطناعي`);
                        }, 800);
                    }
                });
            });
            
            // زر معاينة الملف المهني
            previewBtn.addEventListener('click', function() {
                updatePreview();
                previewModal.style.display = 'block';
                document.body.style.overflow = 'hidden';
            });
            
            // إغلاق نافذة المعاينة
            closePreview.addEventListener('click', function() {
                previewModal.style.display = 'none';
                document.body.style.overflow = 'auto';
            });
            
            // إغلاق النافذة عند النقر خارج المحتوى
            previewModal.addEventListener('click', function(e) {
                if (e.target === previewModal) {
                    previewModal.style.display = 'none';
                    document.body.style.overflow = 'auto';
                }
            });
            
            // زر إنشاء ملف HTML
            exportHtmlBtn.addEventListener('click', function() {
                generateHtmlFile();
            });
            
            // زر تصدير كملف Excel
            exportExcelBtn.addEventListener('click', function() {
                generateExcelFile();
            });
            
            // دالة تحديث المعاينة
            function updatePreview() {
                const teacherName = document.getElementById('teacherName').value.trim() || "المعلم";
                const previewTeacherName = document.getElementById('previewTeacherName');
                const previewBody = document.getElementById('previewBody');
                
                previewTeacherName.textContent = teacherName;
                
                // إنشاء محتوى المعاينة
                let previewContent = '';
                
                const sections = [
                    { id: 'about', title: 'نبذة عني', icon: 'user' },
                    { id: 'vision', title: 'الرؤية التعليمية', icon: 'eye' },
                    { id: 'experience', title: 'الخبرات', icon: 'briefcase' },
                    { id: 'achievements', title: 'الإنجازات', icon: 'trophy' },
                    { id: 'courses', title: 'الدورات التدريبية', icon: 'certificate' },
                    { id: 'skills', title: 'المهارات', icon: 'star' },
                    { id: 'performance', title: 'شواهد الأداء', icon: 'chart-line' },
                    { id: 'portfolio', title: 'معرض الأعمال', icon: 'images' },
                    { id: 'contact', title: 'بيانات التواصل', icon: 'address-card' }
                ];
                
                sections.forEach(section => {
                    const text = document.getElementById(`${section.id}-text`).value;
                    if (text.trim()) {
                        previewContent += `
                            <div class="preview-section">
                                <h4><i class="fas fa-${section.icon}"></i> ${section.title}</h4>
                                <p>${formatPreviewText(text)}</p>
                            </div>
                        `;
                    }
                });
                
                previewBody.innerHTML = previewContent;
            }
            
            // دالة تنسيق النص للمعاينة
            function formatPreviewText(text) {
                return text.replace(/\n/g, '<br>').replace(/\•/g, '•');
            }
            
            // دالة الحصول على اسم القسم
            function getSectionName(sectionId) {
                const sectionNames = {
                    about: 'نبذة عني',
                    vision: 'الرؤية التعليمية',
                    experience: 'الخبرات',
                    achievements: 'الإنجازات',
                    courses: 'الدورات التدريبية',
                    skills: 'المهارات',
                    performance: 'شواهد الأداء',
                    portfolio: 'معرض الأعمال',
                    contact: 'بيانات التواصل'
                };
                
                return sectionNames[sectionId] || 'القسم';
            }
            
            // دالة إنشاء ملف HTML
            function generateHtmlFile() {
                const teacherName = document.getElementById('teacherName').value.trim() || "المعلم";
                
                // جمع البيانات من جميع الأقسام
                const sectionsData = {};
                Object.keys(defaultTexts).forEach(sectionId => {
                    const textarea = document.getElementById(`${sectionId}-text`);
                    if (textarea) {
                        sectionsData[sectionId] = textarea.value;
                    }
                });
                
                // إنشاء محتوى ملف HTML
                const htmlContent = `
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الملف المهني - ${teacherName}</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700&family=Tajawal:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', 'Cairo', sans-serif;
        }
        
        body {
            background-color: #f9f9f9;
            color: #333;
            line-height: 1.7;
            padding: 20px;
            max-width: 1000px;
            margin: 0 auto;
        }
        
        .professional-header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 40px 30px;
            border-radius: 12px;
            margin-bottom: 40px;
            text-align: center;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }
        
        .professional-header h1 {
            font-size: 36px;
            margin-bottom: 10px;
            font-weight: 700;
        }
        
        .professional-header p {
            font-size: 18px;
            opacity: 0.9;
        }
        
        .section {
            background-color: white;
            border-radius: 10px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            border-right: 5px solid #1abc9c;
        }
        
        .section-title {
            color: #2c3e50;
            font-size: 24px;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #f0f0f0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            color: #3498db;
        }
        
        .section-content {
            font-size: 17px;
            color: #444;
            line-height: 1.8;
        }
        
        .section-content ul {
            padding-right: 20px;
            margin-top: 10px;
        }
        
        .section-content li {
            margin-bottom: 8px;
        }
        
        .contact-info {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .contact-item {
            background-color: #f8f9fa;
            padding: 12px 15px;
            border-radius: 8px;
            border-right: 3px solid #3498db;
        }
        
        .footer {
            text-align: center;
            margin-top: 50px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #777;
            font-size: 14px;
        }
        
        @media (max-width: 768px) {
            .professional-header h1 {
                font-size: 28px;
            }
            
            .section {
                padding: 20px;
            }
            
            .section-title {
                font-size: 22px;
            }
        }
        
        @media print {
            body {
                padding: 10px;
            }
            
            .section {
                box-shadow: none;
                border: 1px solid #ddd;
                page-break-inside: avoid;
            }
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <header class="professional-header">
        <h1>${teacherName}</h1>
        <p>الملف المهني الاحترافي للمعلم</p>
    </header>
    
    <main>
        ${generateHtmlSections(sectionsData)}
    </main>
    
    <footer class="footer">
        <p>تم إنشاء هذا الملف المهني باستخدام أداة الملف المهني للمعلم • ${new Date().toLocaleDateString('ar-SA')}</p>
    </footer>
</body>
</html>`;
                
                // إنشاء ملف HTML قابل للتحميل
                const blob = new Blob([htmlContent], { type: 'text/html' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `الملف_المهني_${teacherName.replace(/\s+/g, '_')}.html`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                showNotification(`تم إنشاء ملف HTML لـ ${teacherName} بنجاح`);
            }
            
            // دالة إنشاء أقسام HTML
            function generateHtmlSections(sectionsData) {
                const sections = [
                    { id: 'about', title: 'نبذة عني', icon: 'user' },
                    { id: 'vision', title: 'الرؤية التعليمية', icon: 'eye' },
                    { id: 'experience', title: 'الخبرات', icon: 'briefcase' },
                    { id: 'achievements', title: 'الإنجازات', icon: 'trophy' },
                    { id: 'courses', title: 'الدورات التدريبية', icon: 'certificate' },
                    { id: 'skills', title: 'المهارات', icon: 'star' },
                    { id: 'performance', title: 'شواهد الأداء', icon: 'chart-line' },
                    { id: 'portfolio', title: 'معرض الأعمال', icon: 'images' },
                    { id: 'contact', title: 'بيانات التواصل', icon: 'address-card' }
                ];
                
                let htmlSections = '';
                
                sections.forEach(section => {
                    const content = sectionsData[section.id];
                    if (content && content.trim()) {
                        let formattedContent = content.replace(/\n/g, '<br>');
                        
                        // إذا كان القسم يحتوي على نقاط (قوائم)
                        if (content.includes('•')) {
                            const lines = content.split('\n');
                            formattedContent = '';
                            lines.forEach(line => {
                                if (line.trim().startsWith('•')) {
                                    formattedContent += `<li>${line.trim().substring(1).trim()}</li>`;
                                } else if (line.trim()) {
                                    formattedContent += `<p>${line.trim()}</p>`;
                                }
                            });
                            formattedContent = `<ul>${formattedContent}</ul>`;
                        }
                        
                        // معالجة خاصة لقسم بيانات التواصل
                        if (section.id === 'contact') {
                            const lines = content.split('\n');
                            let contactItems = '';
                            lines.forEach(line => {
                                if (line.trim()) {
                                    contactItems += `<div class="contact-item">${line.trim()}</div>`;
                                }
                            });
                            formattedContent = `<div class="contact-info">${contactItems}</div>`;
                        }
                        
                        htmlSections += `
        <section class="section">
            <h2 class="section-title"><i class="fas fa-${section.icon}"></i> ${section.title}</h2>
            <div class="section-content">${formattedContent}</div>
        </section>`;
                    }
                });
                
                return htmlSections;
            }
            
            // دالة إنشاء ملف Excel
            function generateExcelFile() {
                const teacherName = document.getElementById('teacherName').value.trim() || "المعلم";
                
                // جمع البيانات من جميع الأقسام
                const sectionsData = [];
                Object.keys(defaultTexts).forEach(sectionId => {
                    const textarea = document.getElementById(`${sectionId}-text`);
                    if (textarea) {
                        sectionsData.push({
                            section: getSectionName(sectionId),
                            content: textarea.value
                        });
                    }
                });
                
                // إنشاء مصفوفة البيانات
                const data = [
                    ["الملف المهني للمعلم", teacherName],
                    ["تاريخ الإنشاء", new Date().toLocaleDateString('ar-SA')],
                    [""], // سطر فارغ
                    ["القسم", "المحتوى"]
                ];
                
                // إضافة بيانات الأقسام
                sectionsData.forEach(section => {
                    data.push([section.section, section.content]);
                });
                
                // إنشاء ورقة عمل
                const ws = XLSX.utils.aoa_to_sheet(data);
                
                // تحديد عرض الأعمدة
                const wscols = [
                    {wch: 20}, // عرض عمود القسم
                    {wch: 80}  // عرض عمود المحتوى
                ];
                ws['!cols'] = wscols;
                
                // إنشاء مصنف وإضافة الورقة
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "الملف المهني");
                
                // تصدير الملف
                XLSX.writeFile(wb, `الملف_المهني_${teacherName.replace(/\s+/g, '_')}.xlsx`);
                
                showNotification(`تم إنشاء ملف Excel لـ ${teacherName} بنجاح`);
            }
            
            // دالة عرض الإشعارات
            function showNotification(message) {
                // إنشاء عنصر الإشعار
                const notification = document.createElement('div');
                notification.style.cssText = `
                    position: fixed;
                    top: 20px;
                    left: 50%;
                    transform: translateX(-50%);
                    background-color: #27ae60;
                    color: white;
                    padding: 15px 25px;
                    border-radius: 8px;
                    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
                    z-index: 2000;
                    font-weight: 600;
                    animation: fadeInOut 3s ease;
                `;
                
                // إضافة أنميشن
                const style = document.createElement('style');
                style.textContent = `
                    @keyframes fadeInOut {
                        0% { opacity: 0; transform: translateX(-50%) translateY(-20px); }
                        15% { opacity: 1; transform: translateX(-50%) translateY(0); }
                        85% { opacity: 1; transform: translateX(-50%) translateY(0); }
                        100% { opacity: 0; transform: translateX(-50%) translateY(-20px); }
                    }
                `;
                document.head.appendChild(style);
                
                notification.textContent = message;
                document.body.appendChild(notification);
                
                // إزالة الإشعار بعد 3 ثواني
                setTimeout(() => {
                    document.body.removeChild(notification);
                    document.head.removeChild(style);
                }, 3000);
            }
            
            // تعيين اسم افتراضي للمعلم
            teacherNameInput.value = "أحمد محمد";
            showNotification("مرحبًا! يمكنك الآن البدء في إنشاء ملفك المهني");
        });
    </script>
</body>
</html>
