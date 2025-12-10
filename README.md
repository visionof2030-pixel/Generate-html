<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة إنشاء الملف المهني للمعلم</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        :root {
            --primary: #3498DB;
            --primary-dark: #2980B9;
            --primary-light: #5DADE2;
            --secondary: #2ECC71;
            --secondary-dark: #27AE60;
            --secondary-light: #58D68D;
            --accent: #E74C3C;
            --accent-dark: #C0392B;
            --accent-light: #EC7063;
            --tertiary: #9B59B6;
            --tertiary-dark: #8E44AD;
            --tertiary-light: #BB8FCE;
            --yellow: #F1C40F;
            --yellow-dark: #F39C12;
            --yellow-light: #F7DC6F;
            
            --text: #2C3E50;
            --text-secondary: #566573;
            --text-muted: #7F8C8D;
            --bg: #F8F9FA;
            --card-bg: #FFFFFF;
            --border: #E9ECEF;
            --shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
            --shadow-hover: 0 10px 30px rgba(0, 0, 0, 0.12);
            --gradient-primary: linear-gradient(135deg, #3498DB, #5DADE2);
            --gradient-secondary: linear-gradient(135deg, #2ECC71, #58D68D);
            --gradient-accent: linear-gradient(135deg, #E74C3C, #EC7063);
            --gradient-tertiary: linear-gradient(135deg, #9B59B6, #BB8FCE);
            --gradient-yellow: linear-gradient(135deg, #F1C40F, #F7DC6F);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', sans-serif;
        }

        body {
            background: var(--bg);
            color: var(--text);
            line-height: 1.7;
            overflow-x: hidden;
            font-weight: 400;
        }

        /* ========== TOOL HEADER ========== */
        .tool-header {
            background: white;
            box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
            padding: 1rem 1.5rem;
            position: sticky;
            top: 0;
            z-index: 1000;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 80px;
        }

        .tool-logo {
            display: flex;
            align-items: center;
            gap: 0.8rem;
            text-decoration: none;
        }

        .tool-icon {
            width: 45px;
            height: 45px;
            background: var(--gradient-primary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.2rem;
            border: 3px solid white;
            box-shadow: 0 3px 10px rgba(52, 152, 219, 0.3);
        }

        .tool-info h1 {
            font-size: 1.3rem;
            font-weight: 800;
            color: var(--primary);
            margin-bottom: 0.2rem;
        }

        .tool-info p {
            font-size: 0.85rem;
            color: var(--text-secondary);
            font-weight: 500;
        }

        /* ========== TEACHER NAME INPUT ========== */
        .teacher-name-section {
            display: flex;
            align-items: center;
            gap: 1rem;
            background: rgba(52, 152, 219, 0.1);
            padding: 0.8rem 1.5rem;
            border-radius: 15px;
            border: 2px solid rgba(52, 152, 219, 0.2);
        }

        .teacher-name-section i {
            color: var(--primary);
            font-size: 1.2rem;
        }

        .teacher-name-input {
            background: transparent;
            border: none;
            color: var(--text);
            font-size: 1.1rem;
            font-weight: 600;
            width: 250px;
            outline: none;
            text-align: right;
        }

        .teacher-name-input::placeholder {
            color: var(--text-muted);
        }

        /* ========== SECTIONS NAVIGATOR ========== */
        .sections-nav-container {
            background: white;
            border-radius: 15px;
            padding: 1rem;
            box-shadow: 0 3px 15px rgba(0, 0, 0, 0.08);
            border: 1px solid var(--border);
            margin: 1.5rem auto;
            max-width: 1200px;
        }

        .sections-nav {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 0.8rem;
        }

        .section-nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 1rem;
            text-decoration: none;
            border-radius: 12px;
            transition: all 0.3s ease;
            cursor: pointer;
            border: 2px solid transparent;
        }

        .section-nav-item:hover {
            background: rgba(52, 152, 219, 0.1);
            transform: translateY(-3px);
        }

        .section-nav-item.active {
            background: var(--gradient-primary);
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.2);
            border-color: var(--primary);
        }

        .section-nav-icon {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 0.6rem;
            color: var(--primary);
            font-size: 1.3rem;
            background: rgba(52, 152, 219, 0.1);
            border-radius: 10px;
            transition: all 0.3s ease;
        }

        .section-nav-item.active .section-nav-icon {
            background: rgba(255, 255, 255, 0.9);
            color: var(--primary);
            transform: scale(1.1);
        }

        .section-nav-label {
            font-size: 0.85rem;
            font-weight: 700;
            color: var(--text-secondary);
            text-align: center;
        }

        .section-nav-item.active .section-nav-label {
            color: white;
        }

        /* ========== SECTIONS CONTAINER ========== */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1.5rem 3rem;
        }

        .section-form {
            background: white;
            border-radius: 20px;
            padding: 2.5rem;
            box-shadow: var(--shadow);
            margin-bottom: 2rem;
            border: 1px solid var(--border);
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .section-form.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ========== SECTION HEADER ========== */
        .section-form-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1.5rem;
            border-bottom: 3px solid var(--border);
            position: relative;
        }

        .section-form-header::after {
            content: '';
            position: absolute;
            bottom: -3px;
            right: 0;
            width: 80px;
            height: 3px;
            background: var(--gradient-primary);
            border-radius: 3px;
        }

        .section-form-title {
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 0.8rem;
        }

        .section-form-title i {
            color: var(--primary);
        }

        .ai-generate-btn {
            background: var(--gradient-secondary);
            color: white;
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 12px;
            font-weight: 700;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.6rem;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .ai-generate-btn:hover {
            background: var(--secondary-dark);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(46, 204, 113, 0.3);
        }

        .ai-generate-btn i {
            font-size: 1rem;
        }

        /* ========== SECTION CONTENT ========== */
        .section-content {
            margin-top: 1.5rem;
        }

        .section-label {
            display: block;
            margin-bottom: 1rem;
            font-weight: 700;
            color: var(--primary);
            font-size: 1.1rem;
        }

        .section-textarea {
            width: 100%;
            min-height: 250px;
            padding: 1.5rem;
            border: 2px solid var(--border);
            border-radius: 15px;
            font-size: 1rem;
            line-height: 1.8;
            resize: vertical;
            transition: all 0.3s ease;
            font-family: 'Tajawal', sans-serif;
            background: rgba(248, 249, 250, 0.5);
        }

        .section-textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 4px rgba(52, 152, 219, 0.2);
            background: white;
        }

        .section-hint {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 0.8rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .section-hint i {
            color: var(--primary);
        }

        /* ========== EXPORT OPTIONS ========== */
        .export-section {
            background: white;
            border-radius: 20px;
            padding: 2.5rem;
            box-shadow: var(--shadow);
            margin-top: 2rem;
            text-align: center;
            border: 2px dashed var(--border);
        }

        .export-title {
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--primary);
            margin-bottom: 1rem;
        }

        .export-subtitle {
            color: var(--text-secondary);
            margin-bottom: 2rem;
            max-width: 700px;
            margin-right: auto;
            margin-left: auto;
        }

        .export-options {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            flex-wrap: wrap;
        }

        .export-btn {
            padding: 1.2rem 2.5rem;
            border-radius: 15px;
            font-weight: 800;
            font-size: 1.1rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.8rem;
            transition: all 0.3s ease;
            border: none;
            min-width: 220px;
            justify-content: center;
        }

        .export-btn.html {
            background: var(--gradient-primary);
            color: white;
        }

        .export-btn.excel {
            background: var(--gradient-secondary);
            color: white;
        }

        .export-btn.preview {
            background: var(--gradient-yellow);
            color: white;
        }

        .export-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }

        .export-btn.html:hover {
            background: var(--primary-dark);
        }

        .export-btn.excel:hover {
            background: var(--secondary-dark);
        }

        .export-btn.preview:hover {
            background: var(--yellow-dark);
        }

        .export-btn i {
            font-size: 1.3rem;
        }

        /* ========== PREVIEW MODAL ========== */
        .preview-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.85);
            z-index: 2000;
            overflow-y: auto;
            padding: 1rem;
        }

        .preview-content {
            background-color: white;
            max-width: 1000px;
            margin: 2rem auto;
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
            overflow: hidden;
            animation: modalFadeIn 0.4s ease;
        }

        @keyframes modalFadeIn {
            from { opacity: 0; transform: translateY(-40px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .preview-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1.5rem 2rem;
            background: white;
            border-bottom: 1px solid var(--border);
        }

        .preview-title {
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--primary);
        }

        .preview-close {
            background: var(--gradient-accent);
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
        }

        .preview-close:hover {
            background: var(--accent-dark);
            transform: rotate(90deg);
        }

        .preview-body {
            padding: 0;
            max-height: 75vh;
            overflow-y: auto;
        }

        /* ========== RESPONSIVE DESIGN ========== */
        @media (max-width: 992px) {
            .tool-header {
                flex-direction: column;
                height: auto;
                padding: 1rem;
                gap: 1rem;
            }
            
            .teacher-name-section {
                width: 100%;
                justify-content: center;
            }
            
            .teacher-name-input {
                width: 100%;
                text-align: center;
            }
            
            .sections-nav {
                grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
            }
            
            .export-options {
                flex-direction: column;
                align-items: center;
            }
            
            .export-btn {
                width: 100%;
                max-width: 350px;
            }
        }

        @media (max-width: 768px) {
            .section-form-header {
                flex-direction: column;
                gap: 1.5rem;
                align-items: flex-start;
            }
            
            .ai-generate-btn {
                align-self: flex-start;
            }
            
            .section-form {
                padding: 1.8rem 1.5rem;
            }
            
            .section-form-title {
                font-size: 1.5rem;
            }
            
            .export-section {
                padding: 2rem 1.5rem;
            }
            
            .export-title {
                font-size: 1.5rem;
            }
            
            .sections-nav {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 0 1rem 2rem;
            }
            
            .sections-nav {
                grid-template-columns: 1fr;
            }
            
            .section-nav-item {
                flex-direction: row;
                justify-content: flex-start;
                padding: 1rem;
            }
            
            .section-nav-icon {
                margin-bottom: 0;
                margin-left: 1rem;
            }
            
            .export-btn {
                min-width: auto;
                padding: 1rem 1.5rem;
            }
            
            .section-textarea {
                min-height: 200px;
                padding: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <!-- هيدر الأداة -->
    <header class="tool-header">
        <div class="tool-logo">
            <div class="tool-icon pulse">
                <i class="fas fa-chalkboard-teacher"></i>
            </div>
            <div class="tool-info">
                <h1>أداة إنشاء الملف المهني</h1>
                <p>أنشئ ملفك المهني بتصميم احترافي</p>
            </div>
        </div>
        
        <div class="teacher-name-section">
            <i class="fas fa-user-graduate"></i>
            <input type="text" id="teacherName" class="teacher-name-input" placeholder="أدخل اسمك هنا" maxlength="50" value="المعلم أحمد محمد">
        </div>
    </header>

    <!-- شريط التنقل بين الأقسام -->
    <div class="sections-nav-container">
        <nav class="sections-nav">
            <div class="section-nav-item active" data-section="home">
                <div class="section-nav-icon">
                    <i class="fas fa-home"></i>
                </div>
                <div class="section-nav-label">الرئيسية</div>
            </div>
            
            <div class="section-nav-item" data-section="about">
                <div class="section-nav-icon">
                    <i class="fas fa-user"></i>
                </div>
                <div class="section-nav-label">نبذة عني</div>
            </div>
            
            <div class="section-nav-item" data-section="experience">
                <div class="section-nav-icon">
                    <i class="fas fa-graduation-cap"></i>
                </div>
                <div class="section-nav-label">المؤهلات والخبرات</div>
            </div>
            
            <div class="section-nav-item" data-section="achievements">
                <div class="section-nav-icon">
                    <i class="fas fa-trophy"></i>
                </div>
                <div class="section-nav-label">الإنجازات</div>
            </div>
            
            <div class="section-nav-item" data-section="methods">
                <div class="section-nav-icon">
                    <i class="fas fa-lightbulb"></i>
                </div>
                <div class="section-nav-label">المنهجية التعليمية</div>
            </div>
            
            <div class="section-nav-item" data-section="students">
                <div class="section-nav-icon">
                    <i class="fas fa-users"></i>
                </div>
                <div class="section-nav-label">طلاب متميزون</div>
            </div>
            
            <div class="section-nav-item" data-section="performance">
                <div class="section-nav-icon">
                    <i class="fas fa-chart-line"></i>
                </div>
                <div class="section-nav-label">شواهد الأداء</div>
            </div>
            
            <div class="section-nav-item" data-section="portfolio">
                <div class="section-nav-icon">
                    <i class="fas fa-images"></i>
                </div>
                <div class="section-nav-label">معرض الأعمال</div>
            </div>
            
            <div class="section-nav-item" data-section="contact">
                <div class="section-nav-icon">
                    <i class="fas fa-address-card"></i>
                </div>
                <div class="section-nav-label">بيانات التواصل</div>
            </div>
        </nav>
    </div>

    <!-- المحتوى الرئيسي -->
    <main class="container">
        <!-- قسم الرئيسية -->
        <div class="section-form active" id="home-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-home"></i> الصفحة الرئيسية</h3>
                <button class="ai-generate-btn" data-section="home">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">اكتب وصفاً مختصراً يعرض في الصفحة الرئيسية</label>
                <textarea class="section-textarea" id="home-text" placeholder="مرحباً في الملف التعليمي للمعلم...">مرحباً في الملف التعليمي - المعلم أحمد محمد - رحلة تعليمية مميزة في خدمة اللغة العربية والطلاب. أستاذ لغة عربية ومتخصص في المناهج التعليمية الحديثة مع أكثر من 15 عاماً من الخبرة في تدريس اللغة العربية وتطوير المناهج التعليمية.</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>يمكنك كتابة وصف مختصر وجذاب يظهر في الصفحة الرئيسية للملف المهني</span>
                </div>
            </div>
        </div>

        <!-- قسم نبذة عني -->
        <div class="section-form" id="about-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-user"></i> نبذة عني</h3>
                <button class="ai-generate-btn" data-section="about">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">اكتب نبذة مختصرة عن نفسك وخبراتك التعليمية</label>
                <textarea class="section-textarea" id="about-text" placeholder="أنا معلم متميز في مجال اللغة العربية...">معلم متميز في مجال اللغة العربية، أمضيت أكثر من 15 عاماً في خدمة التعليم والطلاب. تخصصت في تطوير مناهج اللغة العربية الحديثة التي تجمع بين الأصالة والمعاصرة. أسعى دائماً إلى إثراء العملية التعليمية بطرق مبتكرة تجعل تعلم اللغة العربية تجربة ممتعة وفعالة للطلاب.

مؤمن بأن المعلم الناجح هو من يخلق بيئة تعليمية محفزة، ويواكب التطورات الحديثة في طرق التدريس، ويساهم في بناء جيل قادر على التعبير بلغته الأم بفصاحة وطلاقة.</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>اذكر سيرتك الذاتية وخبراتك التعليمية والمهنية</span>
                </div>
            </div>
        </div>

        <!-- قسم المؤهلات والخبرات -->
        <div class="section-form" id="experience-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-graduation-cap"></i> المؤهلات والخبرات</h3>
                <button class="ai-generate-btn" data-section="experience">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">اذكر مؤهلاتك الأكاديمية وخبراتك العملية</label>
                <textarea class="section-textarea" id="experience-text" placeholder="• دكتوراه في اللغة العربية - جامعة الملك سعود (2015)...">• دكتوراه في اللغة العربية - جامعة الملك سعود (2015)
• ماجستير في المناهج وطرق التدريس - جامعة القاهرة (2010)
• بكالوريوس اللغة العربية - جامعة الأزهر (2005)

• أستاذ مساعد - اللغة العربية، كلية التربية - جامعة الملك خالد (2020 - الآن)
• معلم أول - اللغة العربية، المدرسة الثانوية النموذجية - الرياض (2015 - 2020)
• معلم - اللغة العربية، مدرسة النهضة المتوسطة - جدة (2008 - 2015)</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>استخدم النقاط لتنظيم المؤهلات والخبرات بشكل واضح</span>
                </div>
            </div>
        </div>

        <!-- قسم الإنجازات -->
        <div class="section-form" id="achievements-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-trophy"></i> الإنجازات والتكريمات</h3>
                <button class="ai-generate-btn" data-section="achievements">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">اذكر أبرز إنجازاتك المهنية والتكريمات</label>
                <textarea class="section-textarea" id="achievements-text" placeholder="• جائزة التميز في التدريس - 2023...">• جائزة التميز في التدريس - وزارة التعليم (2023)
• جائزة البحث العلمي - أفضل بحث علمي في تعليم اللغة العربية (2022)
• وسام التربية والتعليم - تكريم من أمير منطقة الرياض (2021)
• جائزة الإبداع التعليمي - مركز التميز البحثي في التعليم (2020)
• جائزة المعلم المتميز على مستوى المنطقة (2019, 2018)
• شهادة التقدير من إدارة التعليم لتميز الطلاب (2017)</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>رتب الإنجازات من الأحدث إلى الأقدم مع ذكر السنة</span>
                </div>
            </div>
        </div>

        <!-- قسم المنهجية التعليمية -->
        <div class="section-form" id="methods-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-lightbulb"></i> المنهجية التعليمية</h3>
                <button class="ai-generate-btn" data-section="methods">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">صف منهجيتك وأساليبك في التدريس</label>
                <textarea class="section-textarea" id="methods-text" placeholder="• التعلم باللعب: استخدام الألعاب التعليمية...">• التعلم باللعب: استخدام الألعاب التعليمية التفاعلية لجعل تعلم اللغة العربية تجربة ممتعة وتفاعلية.
• التقنية في التعليم: توظيف التطبيقات والبرامج التعليمية في شرح الدروس، واستخدام الواقع المعزز.
• التعلم التعاوني: تشجيع الطلاب على العمل في مجموعات صغيرة لحل المشكلات اللغوية.
• خرائط المفاهيم: استخدام خرائط المفاهيم الذهنية لربط القواعد النحوية والصرفية.
• التكامل بين المهارات: دمج مهارات الاستماع والتحدث والقراءة والكتابة في دروس متكاملة.
• التقييم المستمر: استخدام أساليب تقييم متنوعة تركز على نمو الطالب ومهاراته.</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>اذكر الأساليب والطرق المبتكرة التي تستخدمها في التدريس</span>
                </div>
            </div>
        </div>

        <!-- قسم طلاب متميزون -->
        <div class="section-form" id="students-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-users"></i> طلاب متميزون</h3>
                <button class="ai-generate-btn" data-section="students">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">اذكر أبرز الطلاب المتميزين تحت إشرافك</label>
                <textarea class="section-textarea" id="students-text" placeholder="• خالد أحمد: الأول على مستوى المملكة (2023)...">• خالد أحمد: الأول على مستوى المملكة في اللغة العربية (2023) - "الأستاذ أحمد غيّر نظرتي للغة العربية من مادة صعبة إلى عالم من الجمال والأدب"
• نورة محمد: جائزة القصة القصيرة على مستوى المملكة (2022) - "بفضل أستاذي أحمد، اكتشفت موهبتي في الكتابة الإبداعية"
• فهد سعد: مبتكر تطبيق تعليمي للغة العربية (2021) - "استفدت من منهجية الأستاذ في استخدام التقنية فطورت تطبيقاً لتعليم النحو"
• سارة علي: الحاصلة على المركز الثاني في مسابقة الخط العربي (2020)
• محمد خالد: ممثل المملكة في أولمبياد اللغة العربية الدولي (2019)</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>اذكر أسماء الطلاب المتميزين وإنجازاتهم مع اقتباسات إن وجدت</span>
                </div>
            </div>
        </div>

        <!-- قسم شواهد الأداء -->
        <div class="section-form" id="performance-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-chart-line"></i> شواهد الأداء</h3>
                <button class="ai-generate-btn" data-section="performance">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">اذكر تقييمات أدائك وشواهد التميز</label>
                <textarea class="section-textarea" id="performance-text" placeholder="• تقييم أداء ممتاز من قائد المدرسة...">• تقييم أداء ممتاز من قائد المدرسة للعام الدراسي 2022/2023
• تقييم "متميز" من الإدارة التعليمية لمدة 3 سنوات متتالية
• تقييم إيجابي من أولياء الأمور بنسبة 95% وفق استبيان الرضا
• تقييم مرتفع في أداء المعلمين من المشرف التربوي (4.8/5)
• شهادة شكر من مدير التعليم للمشاركة الفاعلة في البرامج التربوية
• تقييم عالي من الطلاب في استبيانات الرضا عن التدريس</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>اذكر التقييمات الرسمية وشواهد التميز في أدائك</span>
                </div>
            </div>
        </div>

        <!-- قسم معرض الأعمال -->
        <div class="section-form" id="portfolio-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-images"></i> معرض الأعمال</h3>
                <button class="ai-generate-btn" data-section="portfolio">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">صف مشاريعك وأعمالك المميزة</label>
                <textarea class="section-textarea" id="portfolio-text" placeholder="• تصميم دليل تعليمي تفاعلي...">• تصميم دليل تعليمي تفاعلي لطلاب الصف الأول الثانوي في النحو العربي
• إنشاء قناة يوتيوب تعليمية تحتوي على 50 فيديو تعليمي للغة العربية
• تطوير نشاط "رحلة معرفية" حاز على المركز الأول على مستوى المدارس
• تصميم أنشطة تقويمية إلكترونية باستخدام منصة Nearpod
• إعداد معرض "إبداعات طلابية" ضم 75 عملاً فنياً وأدبياً
• تأليف كتاب "النحو الميسر" للطلاب المبتدئين
• تطوير منهج إثرائي في الأدب العربي لطلاب الموهوبين</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>اذكر مشاريعك التعليمية والأعمال التي أنجزتها</span>
                </div>
            </div>
        </div>

        <!-- قسم بيانات التواصل -->
        <div class="section-form" id="contact-form">
            <div class="section-form-header">
                <h3 class="section-form-title"><i class="fas fa-address-card"></i> بيانات التواصل</h3>
                <button class="ai-generate-btn" data-section="contact">
                    <i class="fas fa-robot"></i> توليد نص بالذكاء الاصطناعي
                </button>
            </div>
            <div class="section-content">
                <label class="section-label">أدخل بيانات التواصل الخاصة بك</label>
                <textarea class="section-textarea" id="contact-text" placeholder="البريد الإلكتروني: ...">البريد الإلكتروني: ahmed.teacher@edu.sa
رقم الهاتف: +966 50 123 4567
حساب تويتر: @ahmed_teacher
حساب لينكد إن: linkedin.com/in/ahmedteacher
المدينة: الرياض، المملكة العربية السعودية
المدرسة: المدرسة الثانوية النموذجية
التخصص: اللغة العربية والمناهج التعليمية</textarea>
                <div class="section-hint">
                    <i class="fas fa-lightbulb"></i>
                    <span>أدخل جميع وسائل التواصل التي تريد إضافتها للملف</span>
                </div>
            </div>
        </div>

        <!-- قسم خيارات التصدير -->
        <div class="export-section">
            <h2 class="export-title">تصدير الملف المهني</h2>
            <p class="export-subtitle">بعد تعبئة جميع الأقسام، يمكنك تصدير ملفك المهني بتنسيق HTML أو Excel أو معاينته قبل التصدير</p>
            
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
        </div>
    </main>

    <!-- نافذة معاينة الملف المهني -->
    <div class="preview-modal" id="previewModal">
        <div class="preview-content">
            <div class="preview-header">
                <h3 class="preview-title">معاينة الملف المهني</h3>
                <button class="preview-close" id="closePreview">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="preview-body" id="previewBody">
                <!-- سيتم تعبئة المحتوى هنا بالجافاسكريبت -->
            </div>
        </div>
    </div>

    <script>
        // بيانات النصوص الافتراضية لكل قسم
        const defaultTexts = {
            home: "مرحباً في الملف التعليمي - المعلم أحمد محمد - رحلة تعليمية مميزة في خدمة اللغة العربية والطلاب. أستاذ لغة عربية ومتخصص في المناهج التعليمية الحديثة مع أكثر من 15 عاماً من الخبرة في تدريس اللغة العربية وتطوير المناهج التعليمية.",
            about: "معلم متميز في مجال اللغة العربية، أمضيت أكثر من 15 عاماً في خدمة التعليم والطلاب. تخصصت في تطوير مناهج اللغة العربية الحديثة التي تجمع بين الأصالة والمعاصرة. أسعى دائماً إلى إثراء العملية التعليمية بطرق مبتكرة تجعل تعلم اللغة العربية تجربة ممتعة وفعالة للطلاب.\n\nمؤمن بأن المعلم الناجح هو من يخلق بيئة تعليمية محفزة، ويواكب التطورات الحديثة في طرق التدريس، ويساهم في بناء جيل قادر على التعبير بلغته الأم بفصاحة وطلاقة.",
            experience: "• دكتوراه في اللغة العربية - جامعة الملك سعود (2015)\n• ماجستير في المناهج وطرق التدريس - جامعة القاهرة (2010)\n• بكالوريوس اللغة العربية - جامعة الأزهر (2005)\n\n• أستاذ مساعد - اللغة العربية، كلية التربية - جامعة الملك خالد (2020 - الآن)\n• معلم أول - اللغة العربية، المدرسة الثانوية النموذجية - الرياض (2015 - 2020)\n• معلم - اللغة العربية، مدرسة النهضة المتوسطة - جدة (2008 - 2015)",
            achievements: "• جائزة التميز في التدريس - وزارة التعليم (2023)\n• جائزة البحث العلمي - أفضل بحث علمي في تعليم اللغة العربية (2022)\n• وسام التربية والتعليم - تكريم من أمير منطقة الرياض (2021)\n• جائزة الإبداع التعليمي - مركز التميز البحثي في التعليم (2020)\n• جائزة المعلم المتميز على مستوى المنطقة (2019, 2018)\n• شهادة التقدير من إدارة التعليم لتميز الطلاب (2017)",
            methods: "• التعلم باللعب: استخدام الألعاب التعليمية التفاعلية لجعل تعلم اللغة العربية تجربة ممتعة وتفاعلية.\n• التقنية في التعليم: توظيف التطبيقات والبرامج التعليمية في شرح الدروس، واستخدام الواقع المعزز.\n• التعلم التعاوني: تشجيع الطلاب على العمل في مجموعات صغيرة لحل المشكلات اللغوية.\n• خرائط المفاهيم: استخدام خرائط المفاهيم الذهنية لربط القواعد النحوية والصرفية.\n• التكامل بين المهارات: دمج مهارات الاستماع والتحدث والقراءة والكتابة في دروس متكاملة.\n• التقييم المستمر: استخدام أساليب تقييم متنوعة تركز على نمو الطالب ومهاراته.",
            students: "• خالد أحمد: الأول على مستوى المملكة في اللغة العربية (2023) - \"الأستاذ أحمد غيّر نظرتي للغة العربية من مادة صعبة إلى عالم من الجمال والأدب\"\n• نورة محمد: جائزة القصة القصيرة على مستوى المملكة (2022) - \"بفضل أستاذي أحمد، اكتشفت موهبتي في الكتابة الإبداعية\"\n• فهد سعد: مبتكر تطبيق تعليمي للغة العربية (2021) - \"استفدت من منهجية الأستاذ في استخدام التقنية فطورت تطبيقاً لتعليم النحو\"\n• سارة علي: الحاصلة على المركز الثاني في مسابقة الخط العربي (2020)\n• محمد خالد: ممثل المملكة في أولمبياد اللغة العربية الدولي (2019)",
            performance: "• تقييم أداء ممتاز من قائد المدرسة للعام الدراسي 2022/2023\n• تقييم \"متميز\" من الإدارة التعليمية لمدة 3 سنوات متتالية\n• تقييم إيجابي من أولياء الأمور بنسبة 95% وفق استبيان الرضا\n• تقييم مرتفع في أداء المعلمين من المشرف التربوي (4.8/5)\n• شهادة شكر من مدير التعليم للمشاركة الفاعلة في البرامج التربوية\n• تقييم عالي من الطلاب في استبيانات الرضا عن التدريس",
            portfolio: "• تصميم دليل تعليمي تفاعلي لطلاب الصف الأول الثانوي في النحو العربي\n• إنشاء قناة يوتيوب تعليمية تحتوي على 50 فيديو تعليمي للغة العربية\n• تطوير نشاط \"رحلة معرفية\" حاز على المركز الأول على مستوى المدارس\n• تصميم أنشطة تقويمية إلكترونية باستخدام منصة Nearpod\n• إعداد معرض \"إبداعات طلابية\" ضم 75 عملاً فنياً وأدبياً\n• تأليف كتاب \"النحو الميسر\" للطلاب المبتدئين\n• تطوير منهج إثرائي في الأدب العربي لطلاب الموهوبين",
            contact: "البريد الإلكتروني: ahmed.teacher@edu.sa\nرقم الهاتف: +966 50 123 4567\nحساب تويتر: @ahmed_teacher\nحساب لينكد إن: linkedin.com/in/ahmedteacher\nالمدينة: الرياض، المملكة العربية السعودية\nالمدرسة: المدرسة الثانوية النموذجية\nالتخصص: اللغة العربية والمناهج التعليمية"
        };

        // نص الذكاء الاصطناعي (محاكاة)
        const aiGeneratedTexts = {
            home: "مرحباً بكم في الملف التعليمي للمعلم أحمد محمد، أستاذ اللغة العربية المتميز والمتخصص في تطوير المناهج التعليمية. بفضل خبرة تمتد لأكثر من 15 عاماً في مجال التدريس، أسعى إلى تقديم تعليم عالي الجودة يجمع بين الأصالة والمعاصرة، ويهدف إلى تنمية مهارات الطلاب اللغوية والأدبية.",
            about: "أحمل شغفاً كبيراً باللغة العربية وآدابها، وأعمل بجد لتطوير طرق تدريسها لتتناسب مع متطلبات العصر. أؤمن بأن المعلم ليس مجرد ناقل للمعلومة، بل هو صانع للتجارب التعليمية التي تثري عقول الطلاب وتنمي شخصياتهم. أهدف إلى تخريج جيل متمكن من لغته، فخور بتراثه، قادر على الإبداع والتعبير.",
            experience: "• دكتوراه في اللسانيات التطبيقية - جامعة الملك عبدالعزيز (2018)\n• ماجستير في الأدب العربي - جامعة الإمام محمد بن سعود (2013)\n• بكالوريوس تعليم اللغة العربية - جامعة الطائف (2008)\n\n• رئيس قسم اللغة العربية - إدارة التعليم (2021 - الآن)\n• مشرف تربوي للغة العربية - وزارة التعليم (2017 - 2021)\n• معلم متميز - مدارس التربية النموذجية (2010 - 2017)",
            achievements: "• جائزة الملك سلمان للمعلم المتميز (2023)\n• درع التميز في البحث التربوي - جامعة القصيم (2022)\n• جائزة أفضل مبادرة تعليمية - منتدى التعليم (2021)\n• تكريم من وزير التعليم للإسهامات المميزة (2020)\n• جائزة التميز التربوي على مستوى المنطقة (2019)\n• شهادة تقدير للمشاركة في تأليف المناهج الوطنية (2018)",
            methods: "• التعليم القائم على المشاريع: حيث يطور الطلاب مشاريع لغوية عملية.\n• الفصول المقلوبة: تعزيز التعلم الذاتي والاستفادة من وقت الحصة في التطبيق.\n• التعلم القائم على حل المشكلات: تحفيز التفكير النقدي والإبداعي.\n• استخدام الوسائط المتعددة: دمج الصور والفيديو والصوت في التعليم.\n• التقييم التكويني: متابعة تقدم الطلاب وتقديم تغذية راجعة مستمرة.\n• التكيف مع أنماط التعلم: مراعاة الفروق الفردية بين الطلاب.",
            students: "• ليان عبدالله: الفائزة بجائزة الشاعر الصغير (2023) - \"معلمي علمني أن الشعر ليس مجرد كلمات، بل هو روح وحياة\"\n• ريان الغامدي: مبتكر لعبة تعليمية للنحو (2022) - \"من حصص الأستاذ أحمد استلهمت فكرة اللعبة التعليمية\"\n• لمى السعدي: ممثلة المملكة في مؤتمر اللغة العربية العالمي (2021)\n• بدر ناصر: الحاصل على المركز الأول في مسابقة الإملاء (2020)\n• جواهر القحطاني: كاتبة قصة قصيرة نُشرت في مجلة تعليمية (2019)",
            performance: "• تقييم \"متفوق\" في الأداء الوظيفي لمدة 5 سنوات متتالية\n• نسبة رضا الطلاب 97% وفق استطلاعات الرسمية\n• تقييم \"متميز\" من المشرفين التربويين في جميع الزيارات\n• شهادات شكر وتقدير من أولياء أمور الطلاب\n• تقارير إيجابية من إدارة المدرسة حول التأثير الإيجابي على البيئة التعليمية",
            portfolio: "• تطوير منصة إلكترونية لتعليم النحو العربي عن بعد\n• تأليف سلسلة كتب \"العربية بين يديك\" لثلاثة مستويات\n• إنتاج برنامج تلفزيوني تعليمي للغة العربية\n• تصميم حقيبة تدريبية للمعلمين الجدد في اللغة العربية\n• تنفيذ مبادرة \"اقرأ وارتقِ\" لتعزيز القراءة الحرة\n• إنشاء متحف افتراضي للتراث اللغوي العربي",
            contact: "البريد الإلكتروني: professional.teacher@edu.sa\nالهاتف: +966 55 987 6543\nتويتر: @arabic_teacher\nانستقرام: @teacher_portfolio\nلينكد إن: linkedin.com/in/arabicteacher\nالموقع الإلكتروني: www.arabic-teacher.com\nالعنوان: جدة، المملكة العربية السعودية"
        };

        // تهيئة التطبيق
        document.addEventListener('DOMContentLoaded', function() {
            // عناصر DOM الرئيسية
            const teacherNameInput = document.getElementById('teacherName');
            const navItems = document.querySelectorAll('.section-nav-item');
            const sectionForms = document.querySelectorAll('.section-form');
            const aiButtons = document.querySelectorAll('.ai-generate-btn');
            const exportHtmlBtn = document.getElementById('exportHtml');
            const exportExcelBtn = document.getElementById('exportExcel');
            const previewBtn = document.getElementById('previewBtn');
            const previewModal = document.getElementById('previewModal');
            const closePreview = document.getElementById('closePreview');
            const previewBody = document.getElementById('previewBody');
            
            // تعيين النصوص الافتراضية
            Object.keys(defaultTexts).forEach(sectionId => {
                const textarea = document.getElementById(`${sectionId}-text`);
                if (textarea) {
                    textarea.value = defaultTexts[sectionId];
                }
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
                    
                    // التمرير إلى أعلى القسم
                    window.scrollTo({ top: 0, behavior: 'smooth' });
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
                const teacherName = teacherNameInput.value.trim() || "المعلم أحمد محمد";
                const teacherTitle = "أستاذ لغة عربية ومتخصص في المناهج التعليمية";
                
                // جمع البيانات من جميع الأقسام
                const sectionsData = {};
                Object.keys(defaultTexts).forEach(sectionId => {
                    const textarea = document.getElementById(`${sectionId}-text`);
                    if (textarea) {
                        sectionsData[sectionId] = textarea.value;
                    }
                });
                
                // إنشاء محتوى المعاينة بنفس تصميم الملف المطلوب
                previewBody.innerHTML = generatePreviewContent(teacherName, teacherTitle, sectionsData);
                
                // إضافة JavaScript للمعاينة
                addPreviewScript();
            }
            
            // دالة إنشاء محتوى المعاينة
            function generatePreviewContent(teacherName, teacherTitle, sectionsData) {
                const sections = [
                    { id: 'home', title: 'الرئيسية', icon: 'home' },
                    { id: 'about', title: 'نبذة عني', icon: 'user' },
                    { id: 'experience', title: 'المؤهلات والخبرات', icon: 'graduation-cap' },
                    { id: 'achievements', title: 'الإنجازات', icon: 'trophy' },
                    { id: 'methods', title: 'المنهجية التعليمية', icon: 'lightbulb' },
                    { id: 'students', title: 'طلاب متميزون', icon: 'users' },
                    { id: 'performance', title: 'شواهد الأداء', icon: 'chart-line' },
                    { id: 'portfolio', title: 'معرض الأعمال', icon: 'images' },
                    { id: 'contact', title: 'بيانات التواصل', icon: 'address-card' }
                ];
                
                let previewHTML = `
                <!DOCTYPE html>
                <html lang="ar" dir="rtl">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>الملف التعليمي | ${teacherName}</title>
                    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
                    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
                    <style>
                        :root {
                            --primary: #3498DB;
                            --primary-dark: #2980B9;
                            --primary-light: #5DADE2;
                            --secondary: #2ECC71;
                            --secondary-dark: #27AE60;
                            --secondary-light: #58D68D;
                            --accent: #E74C3C;
                            --accent-dark: #C0392B;
                            --accent-light: #EC7063;
                            --tertiary: #9B59B6;
                            --tertiary-dark: #8E44AD;
                            --tertiary-light: #BB8FCE;
                            --yellow: #F1C40F;
                            --yellow-dark: #F39C12;
                            --yellow-light: #F7DC6F;
                            
                            --text: #2C3E50;
                            --text-secondary: #566573;
                            --text-muted: #7F8C8D;
                            --bg: #F8F9FA;
                            --card-bg: #FFFFFF;
                            --border: #E9ECEF;
                            --shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
                            --shadow-hover: 0 10px 30px rgba(0, 0, 0, 0.12);
                            --gradient-primary: linear-gradient(135deg, #3498DB, #5DADE2);
                            --gradient-secondary: linear-gradient(135deg, #2ECC71, #58D68D);
                            --gradient-accent: linear-gradient(135deg, #E74C3C, #EC7063);
                            --gradient-tertiary: linear-gradient(135deg, #9B59B6, #BB8FCE);
                            --gradient-yellow: linear-gradient(135deg, #F1C40F, #F7DC6F);
                        }

                        * {
                            margin: 0;
                            padding: 0;
                            box-sizing: border-box;
                            font-family: 'Tajawal', sans-serif;
                        }

                        body {
                            background: var(--bg);
                            color: var(--text);
                            line-height: 1.7;
                            overflow-x: hidden;
                            font-weight: 400;
                        }

                        /* ========== COMPACT HEADER ========== */
                        .compact-header {
                            background: white;
                            box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
                            padding: 0.8rem 1.5rem;
                            position: sticky;
                            top: 0;
                            z-index: 1000;
                            display: flex;
                            justify-content: space-between;
                            align-items: center;
                            height: 70px;
                        }

                        .teacher-brand {
                            display: flex;
                            align-items: center;
                            gap: 0.8rem;
                            text-decoration: none;
                        }

                        .teacher-avatar {
                            width: 45px;
                            height: 45px;
                            background: var(--gradient-primary);
                            border-radius: 50%;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            color: white;
                            font-size: 1.2rem;
                            border: 3px solid white;
                            box-shadow: 0 3px 10px rgba(52, 152, 219, 0.3);
                        }

                        .teacher-info h1 {
                            font-size: 1.2rem;
                            font-weight: 800;
                            color: var(--primary);
                            margin-bottom: 0.2rem;
                        }

                        .teacher-info p {
                            font-size: 0.8rem;
                            color: var(--text-secondary);
                            font-weight: 500;
                        }

                        /* ========== ICON NAVIGATION ========== */
                        .icon-nav-container {
                            background: white;
                            border-radius: 12px;
                            padding: 0.5rem;
                            box-shadow: 0 3px 15px rgba(0, 0, 0, 0.08);
                            border: 1px solid var(--border);
                        }

                        .icon-nav {
                            display: flex;
                            gap: 0.3rem;
                        }

                        .nav-icon-item {
                            display: flex;
                            flex-direction: column;
                            align-items: center;
                            padding: 0.7rem 1rem;
                            text-decoration: none;
                            border-radius: 10px;
                            transition: all 0.3s ease;
                            min-width: 80px;
                            position: relative;
                            cursor: pointer;
                        }

                        .nav-icon-item:hover {
                            background: rgba(52, 152, 219, 0.1);
                            transform: translateY(-2px);
                        }

                        .nav-icon-item.active {
                            background: var(--gradient-primary);
                            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.2);
                        }

                        .icon-wrapper {
                            width: 35px;
                            height: 35px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin-bottom: 0.4rem;
                            color: var(--primary);
                            font-size: 1.1rem;
                            background: rgba(52, 152, 219, 0.1);
                            border-radius: 8px;
                            transition: all 0.3s ease;
                        }

                        .nav-icon-item.active .icon-wrapper {
                            background: rgba(255, 255, 255, 0.9);
                            color: var(--primary);
                            transform: scale(1.1);
                        }

                        .icon-label {
                            font-size: 0.75rem;
                            font-weight: 600;
                            color: var(--text-secondary);
                            text-align: center;
                        }

                        .nav-icon-item.active .icon-label {
                            color: white;
                            font-weight: 700;
                        }

                        .indicator {
                            position: absolute;
                            top: -3px;
                            right: 50%;
                            transform: translateX(50%);
                            width: 5px;
                            height: 5px;
                            background: var(--accent);
                            border-radius: 50%;
                            opacity: 0;
                            transition: opacity 0.3s ease;
                        }

                        .nav-icon-item.active .indicator {
                            opacity: 1;
                        }

                        /* ========== CONTENT AREA ========== */
                        .content-wrapper {
                            padding: 1.5rem;
                            max-width: 1200px;
                            margin: 0 auto;
                        }

                        .page {
                            display: none;
                            animation: fadeIn 0.5s ease;
                        }

                        .page.active {
                            display: block;
                        }

                        @keyframes fadeIn {
                            from { opacity: 0; transform: translateY(20px); }
                            to { opacity: 1; transform: translateY(0); }
                        }

                        /* ========== PAGE HEADERS ========== */
                        .page-header {
                            text-align: center;
                            margin-bottom: 2.5rem;
                            padding-bottom: 1.5rem;
                            border-bottom: 3px solid var(--border);
                            position: relative;
                        }

                        .page-header::after {
                            content: '';
                            position: absolute;
                            bottom: -3px;
                            right: 50%;
                            transform: translateX(50%);
                            width: 80px;
                            height: 3px;
                            background: var(--gradient-primary);
                            border-radius: 3px;
                        }

                        .page-title {
                            font-size: 2.2rem;
                            font-weight: 800;
                            margin-bottom: 0.8rem;
                            color: var(--primary);
                        }

                        .page-subtitle {
                            font-size: 1.1rem;
                            color: var(--text-secondary);
                            max-width: 600px;
                            margin: 0 auto;
                        }

                        /* ========== HOME PAGE ========== */
                        .teacher-hero {
                            background: linear-gradient(135deg, rgba(52, 152, 219, 0.1), rgba(46, 204, 113, 0.1));
                            border-radius: 20px;
                            padding: 3rem;
                            text-align: center;
                            margin-bottom: 3rem;
                            box-shadow: var(--shadow);
                            border: 1px solid rgba(52, 152, 219, 0.2);
                        }

                        .hero-title {
                            font-size: 2.8rem;
                            font-weight: 800;
                            margin-bottom: 1rem;
                            background: var(--gradient-primary);
                            -webkit-background-clip: text;
                            -webkit-text-fill-color: transparent;
                        }

                        .hero-subtitle {
                            font-size: 1.3rem;
                            color: var(--text-secondary);
                            margin-bottom: 2rem;
                            max-width: 700px;
                            margin-left: auto;
                            margin-right: auto;
                        }

                        .teacher-tagline {
                            display: inline-block;
                            background: var(--gradient-secondary);
                            color: white;
                            padding: 0.8rem 2rem;
                            border-radius: 50px;
                            font-weight: 700;
                            font-size: 1.1rem;
                            margin-top: 1rem;
                            box-shadow: 0 5px 15px rgba(46, 204, 113, 0.2);
                        }

                        .achievement-stats {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
                            gap: 1.5rem;
                            margin-top: 3rem;
                        }

                        .achievement-card {
                            background: white;
                            padding: 1.8rem;
                            border-radius: 15px;
                            text-align: center;
                            box-shadow: var(--shadow);
                            border-top: 4px solid var(--primary);
                            transition: all 0.3s ease;
                        }

                        .achievement-card:hover {
                            transform: translateY(-5px);
                            box-shadow: var(--shadow-hover);
                        }

                        .achievement-icon {
                            width: 60px;
                            height: 60px;
                            margin: 0 auto 1rem;
                            background: var(--gradient-primary);
                            border-radius: 50%;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            color: white;
                            font-size: 1.5rem;
                        }

                        .achievement-number {
                            font-size: 2.2rem;
                            font-weight: 800;
                            color: var(--primary);
                            display: block;
                            margin-bottom: 0.5rem;
                        }

                        .achievement-label {
                            color: var(--text-secondary);
                            font-size: 0.95rem;
                            font-weight: 600;
                        }

                        /* ========== ABOUT PAGE ========== */
                        .profile-section {
                            display: grid;
                            grid-template-columns: 300px 1fr;
                            gap: 3rem;
                            background: white;
                            padding: 2.5rem;
                            border-radius: 20px;
                            box-shadow: var(--shadow);
                            margin-bottom: 3rem;
                            border: 1px solid var(--border);
                        }

                        .profile-image {
                            text-align: center;
                        }

                        .profile-avatar {
                            width: 250px;
                            height: 250px;
                            background: var(--gradient-primary);
                            border-radius: 20px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            color: white;
                            font-size: 5rem;
                            margin-bottom: 1.5rem;
                            box-shadow: 0 10px 25px rgba(52, 152, 219, 0.3);
                        }

                        .teacher-qualifications {
                            background: rgba(52, 152, 219, 0.1);
                            padding: 1.5rem;
                            border-radius: 15px;
                            border-right: 4px solid var(--primary);
                        }

                        .qualification-item {
                            margin-bottom: 1rem;
                            padding-bottom: 1rem;
                            border-bottom: 1px solid rgba(52, 152, 219, 0.2);
                        }

                        .qualification-item:last-child {
                            margin-bottom: 0;
                            padding-bottom: 0;
                            border-bottom: none;
                        }

                        .qualification-title {
                            font-weight: 700;
                            color: var(--primary);
                            margin-bottom: 0.3rem;
                        }

                        .qualification-desc {
                            color: var(--text-secondary);
                            font-size: 0.9rem;
                        }

                        .profile-details h2 {
                            font-size: 2rem;
                            color: var(--primary);
                            margin-bottom: 0.5rem;
                        }

                        .profile-title {
                            color: var(--secondary);
                            font-size: 1.2rem;
                            font-weight: 600;
                            margin-bottom: 1.5rem;
                        }

                        .profile-description {
                            color: var(--text);
                            line-height: 1.8;
                            margin-bottom: 2rem;
                        }

                        /* ========== EXPERIENCE PAGE ========== */
                        .education-timeline {
                            position: relative;
                            max-width: 800px;
                            margin: 0 auto;
                        }

                        .timeline-item {
                            background: white;
                            padding: 2rem;
                            border-radius: 15px;
                            margin-bottom: 2rem;
                            box-shadow: var(--shadow);
                            border-right: 4px solid var(--secondary);
                            position: relative;
                            transition: all 0.3s ease;
                        }

                        .timeline-item:hover {
                            transform: translateX(-10px);
                            box-shadow: var(--shadow-hover);
                        }

                        .timeline-header {
                            display: flex;
                            justify-content: space-between;
                            align-items: center;
                            margin-bottom: 1rem;
                            flex-wrap: wrap;
                            gap: 1rem;
                        }

                        .timeline-title {
                            font-size: 1.4rem;
                            font-weight: 700;
                            color: var(--primary);
                        }

                        .timeline-period {
                            background: var(--gradient-accent);
                            color: white;
                            padding: 0.5rem 1.2rem;
                            border-radius: 20px;
                            font-size: 0.9rem;
                            font-weight: 600;
                        }

                        .timeline-school {
                            color: var(--secondary);
                            font-weight: 600;
                            margin-bottom: 1rem;
                            font-size: 1.1rem;
                        }

                        .timeline-achievements {
                            list-style: none;
                            margin-top: 1rem;
                        }

                        .timeline-achievements li {
                            margin-bottom: 0.8rem;
                            color: var(--text);
                            display: flex;
                            align-items: flex-start;
                            gap: 0.8rem;
                        }

                        .timeline-achievements li i {
                            color: var(--secondary);
                            margin-top: 0.3rem;
                        }

                        /* ========== ACHIEVEMENTS PAGE ========== */
                        .awards-grid {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                            gap: 2rem;
                        }

                        .award-card {
                            background: white;
                            padding: 2rem;
                            border-radius: 15px;
                            box-shadow: var(--shadow);
                            border-top: 4px solid var(--yellow);
                            transition: all 0.3s ease;
                            text-align: center;
                        }

                        .award-card:hover {
                            transform: translateY(-8px);
                            box-shadow: var(--shadow-hover);
                        }

                        .award-icon {
                            width: 70px;
                            height: 70px;
                            background: var(--gradient-yellow);
                            border-radius: 50%;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin: 0 auto 1.5rem;
                            color: white;
                            font-size: 1.8rem;
                        }

                        .award-title {
                            font-size: 1.3rem;
                            font-weight: 700;
                            margin-bottom: 0.8rem;
                            color: var(--text);
                        }

                        .award-year {
                            color: var(--accent);
                            font-weight: 700;
                            margin-bottom: 1rem;
                            font-size: 1.1rem;
                        }

                        .award-description {
                            color: var(--text-secondary);
                            line-height: 1.6;
                        }

                        /* ========== METHODS PAGE ========== */
                        .methods-grid {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                            gap: 2rem;
                        }

                        .method-card {
                            background: white;
                            padding: 2rem;
                            border-radius: 15px;
                            box-shadow: var(--shadow);
                            border-left: 4px solid var(--tertiary);
                            transition: all 0.3s ease;
                        }

                        .method-card:hover {
                            transform: translateY(-5px);
                            box-shadow: var(--shadow-hover);
                        }

                        .method-icon {
                            width: 60px;
                            height: 60px;
                            background: var(--gradient-tertiary);
                            border-radius: 12px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin-bottom: 1.5rem;
                            color: white;
                            font-size: 1.5rem;
                        }

                        .method-title {
                            font-size: 1.3rem;
                            font-weight: 700;
                            margin-bottom: 1rem;
                            color: var(--primary);
                        }

                        .method-description {
                            color: var(--text-secondary);
                            line-height: 1.7;
                        }

                        /* ========== STUDENTS PAGE ========== */
                        .students-grid {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                            gap: 2rem;
                        }

                        .student-card {
                            background: white;
                            padding: 2rem;
                            border-radius: 15px;
                            box-shadow: var(--shadow);
                            border-bottom: 4px solid var(--secondary);
                            transition: all 0.3s ease;
                            text-align: center;
                        }

                        .student-card:hover {
                            transform: translateY(-5px);
                            box-shadow: var(--shadow-hover);
                        }

                        .student-avatar {
                            width: 80px;
                            height: 80px;
                            background: var(--gradient-secondary);
                            border-radius: 50%;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin: 0 auto 1.5rem;
                            color: white;
                            font-size: 2rem;
                        }

                        .student-name {
                            font-size: 1.3rem;
                            font-weight: 700;
                            margin-bottom: 0.5rem;
                            color: var(--primary);
                        }

                        .student-achievement {
                            color: var(--accent);
                            font-weight: 600;
                            margin-bottom: 1rem;
                            font-size: 1rem;
                        }

                        .student-quote {
                            color: var(--text-secondary);
                            font-style: italic;
                            line-height: 1.6;
                            border-top: 1px solid var(--border);
                            padding-top: 1rem;
                            margin-top: 1rem;
                        }

                        /* ========== PERFORMANCE PAGE ========== */
                        .performance-grid {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                            gap: 2rem;
                        }

                        .performance-card {
                            background: white;
                            padding: 2rem;
                            border-radius: 15px;
                            box-shadow: var(--shadow);
                            border-bottom: 4px solid var(--accent);
                            transition: all 0.3s ease;
                            text-align: center;
                        }

                        .performance-card:hover {
                            transform: translateY(-5px);
                            box-shadow: var(--shadow-hover);
                        }

                        .performance-icon {
                            width: 70px;
                            height: 70px;
                            background: var(--gradient-accent);
                            border-radius: 15px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin: 0 auto 1.5rem;
                            color: white;
                            font-size: 1.8rem;
                        }

                        .performance-title {
                            font-size: 1.3rem;
                            font-weight: 700;
                            margin-bottom: 0.8rem;
                            color: var(--text);
                        }

                        .performance-description {
                            color: var(--text-secondary);
                            line-height: 1.6;
                        }

                        /* ========== PORTFOLIO PAGE ========== */
                        .portfolio-grid {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                            gap: 2rem;
                        }

                        .portfolio-card {
                            background: white;
                            padding: 2rem;
                            border-radius: 15px;
                            box-shadow: var(--shadow);
                            border-left: 4px solid var(--tertiary);
                            transition: all 0.3s ease;
                        }

                        .portfolio-card:hover {
                            transform: translateY(-5px);
                            box-shadow: var(--shadow-hover);
                        }

                        .portfolio-icon {
                            width: 60px;
                            height: 60px;
                            background: var(--gradient-tertiary);
                            border-radius: 12px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin-bottom: 1.5rem;
                            color: white;
                            font-size: 1.5rem;
                        }

                        .portfolio-title {
                            font-size: 1.3rem;
                            font-weight: 700;
                            margin-bottom: 1rem;
                            color: var(--primary);
                        }

                        .portfolio-description {
                            color: var(--text-secondary);
                            line-height: 1.7;
                        }

                        /* ========== CONTACT PAGE ========== */
                        .contact-container {
                            display: grid;
                            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                            gap: 2rem;
                        }

                        .contact-card {
                            background: white;
                            padding: 2.5rem;
                            border-radius: 15px;
                            box-shadow: var(--shadow);
                            text-align: center;
                            transition: all 0.3s ease;
                            border: 1px solid var(--border);
                        }

                        .contact-card:hover {
                            transform: translateY(-5px);
                            box-shadow: var(--shadow-hover);
                        }

                        .contact-icon {
                            width: 70px;
                            height: 70px;
                            background: var(--gradient-primary);
                            border-radius: 15px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            margin: 0 auto 1.5rem;
                            color: white;
                            font-size: 1.8rem;
                        }

                        .contact-title {
                            font-size: 1.3rem;
                            font-weight: 700;
                            margin-bottom: 0.8rem;
                            color: var(--primary);
                        }

                        .contact-info {
                            color: var(--text-secondary);
                            margin-bottom: 1.5rem;
                            font-size: 1.1rem;
                            line-height: 1.8;
                        }

                        .contact-btn {
                            display: inline-block;
                            padding: 0.8rem 2rem;
                            background: var(--gradient-primary);
                            color: white;
                            border-radius: 25px;
                            text-decoration: none;
                            font-weight: 600;
                            font-size: 0.95rem;
                            transition: all 0.3s ease;
                        }

                        .contact-btn:hover {
                            transform: translateY(-3px);
                            box-shadow: 0 8px 20px rgba(52, 152, 219, 0.3);
                        }

                        /* ========== FOOTER ========== */
                        .footer {
                            background: white;
                            padding: 2rem;
                            margin-top: 3rem;
                            border-top: 1px solid var(--border);
                            text-align: center;
                        }

                        .social-links {
                            display: flex;
                            justify-content: center;
                            gap: 1rem;
                            margin-bottom: 1.5rem;
                        }

                        .social-link {
                            width: 45px;
                            height: 45px;
                            background: var(--bg);
                            border-radius: 10px;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            color: var(--primary);
                            text-decoration: none;
                            transition: all 0.3s ease;
                            border: 1px solid var(--border);
                        }

                        .social-link:hover {
                            background: var(--gradient-primary);
                            color: white;
                            transform: translateY(-3px);
                            border-color: transparent;
                        }

                        .copyright {
                            color: var(--text-muted);
                            font-size: 0.9rem;
                        }

                        /* ========== TEXT FORMATTING ========== */
                        .formatted-text {
                            white-space: pre-line;
                            line-height: 1.8;
                            color: var(--text);
                        }

                        .formatted-text ul {
                            list-style: none;
                            padding-right: 1.5rem;
                            margin-top: 1rem;
                        }

                        .formatted-text li {
                            margin-bottom: 0.8rem;
                            padding-right: 1.5rem;
                            position: relative;
                        }

                        .formatted-text li:before {
                            content: "•";
                            color: var(--primary);
                            font-size: 1.5rem;
                            position: absolute;
                            right: 0;
                            top: -0.2rem;
                        }

                        /* ========== RESPONSIVE DESIGN ========== */
                        @media (max-width: 1024px) {
                            .profile-section {
                                grid-template-columns: 1fr;
                                text-align: center;
                            }
                            
                            .teacher-qualifications {
                                max-width: 500px;
                                margin: 0 auto;
                            }
                        }

                        @media (max-width: 768px) {
                            .compact-header {
                                flex-direction: column;
                                height: auto;
                                padding: 1rem;
                                gap: 1rem;
                            }
                            
                            .icon-nav {
                                flex-wrap: wrap;
                                justify-content: center;
                            }
                            
                            .hero-title {
                                font-size: 2.2rem;
                            }
                            
                            .page-title {
                                font-size: 1.8rem;
                            }
                            
                            .achievement-stats {
                                grid-template-columns: repeat(2, 1fr);
                            }
                            
                            .awards-grid,
                            .methods-grid,
                            .students-grid,
                            .performance-grid,
                            .portfolio-grid {
                                grid-template-columns: 1fr;
                            }
                        }

                        @media (max-width: 480px) {
                            .content-wrapper {
                                padding: 1rem;
                            }
                            
                            .teacher-hero {
                                padding: 2rem 1rem;
                            }
                            
                            .hero-title {
                                font-size: 1.8rem;
                            }
                            
                            .achievement-stats {
                                grid-template-columns: 1fr;
                            }
                            
                            .nav-icon-item {
                                min-width: 70px;
                                padding: 0.6rem 0.8rem;
                            }
                            
                            .icon-wrapper {
                                width: 30px;
                                height: 30px;
                                font-size: 1rem;
                            }
                            
                            .icon-label {
                                font-size: 0.7rem;
                            }
                            
                            .contact-container {
                                grid-template-columns: 1fr;
                            }
                        }

                        /* ========== ANIMATIONS ========== */
                        @keyframes float {
                            0%, 100% {
                                transform: translateY(0);
                            }
                            50% {
                                transform: translateY(-10px);
                            }
                        }

                        .floating {
                            animation: float 3s ease-in-out infinite;
                        }

                        .pulse {
                            animation: pulse 2s infinite;
                        }

                        @keyframes pulse {
                            0% {
                                box-shadow: 0 0 0 0 rgba(52, 152, 219, 0.4);
                            }
                            70% {
                                box-shadow: 0 0 0 10px rgba(52, 152, 219, 0);
                            }
                            100% {
                                box-shadow: 0 0 0 0 rgba(52, 152, 219, 0);
                            }
                        }
                    </style>
                </head>
                <body>
                    <!-- Compact Header -->
                    <header class="compact-header">
                        <a href="#" class="teacher-brand">
                            <div class="teacher-avatar pulse">
                                <i class="fas fa-chalkboard-teacher"></i>
                            </div>
                            <div class="teacher-info">
                                <h1>${teacherName}</h1>
                                <p>${teacherTitle}</p>
                            </div>
                        </a>

                        <!-- Icon Navigation -->
                        <div class="icon-nav-container">
                            <nav class="icon-nav">`;
                
                // إضافة عناصر التنقل
                sections.forEach((section, index) => {
                    const activeClass = index === 0 ? 'active' : '';
                    previewHTML += `
                                <a href="#${section.id}" class="nav-icon-item ${activeClass}" data-page="${section.id}">
                                    <div class="indicator"></div>
                                    <div class="icon-wrapper">
                                        <i class="fas fa-${section.icon}"></i>
                                    </div>
                                    <div class="icon-label">${section.title}</div>
                                </a>`;
                });
                
                previewHTML += `
                            </nav>
                        </div>
                    </header>

                    <!-- Content Area -->
                    <main class="content-wrapper">`;
                
                // إضافة صفحات المحتوى
                sections.forEach((section, index) => {
                    const activeClass = index === 0 ? 'active' : '';
                    const content = formatTextForPreview(sectionsData[section.id] || '');
                    
                    previewHTML += `
                        <!-- ${section.title} Page -->
                        <section id="${section.id}-page" class="page ${activeClass}">
                            <div class="page-header">
                                <h1 class="page-title">${section.title}</h1>
                                <p class="page-subtitle">
                                    ${getSectionSubtitle(section.id)}
                                </p>
                            </div>
                            
                            ${generatePageContent(section.id, content)}
                        </section>`;
                });
                
                previewHTML += `
                    </main>

                    <!-- Footer -->
                    <footer class="footer">
                        <div class="social-links">
                            <a href="#" class="social-link">
                                <i class="fab fa-twitter"></i>
                            </a>
                            <a href="#" class="social-link">
                                <i class="fab fa-linkedin-in"></i>
                            </a>
                            <a href="#" class="social-link">
                                <i class="fab fa-youtube"></i>
                            </a>
                            <a href="#" class="social-link">
                                <i class="fab fa-researchgate"></i>
                            </a>
                        </div>
                        <p class="copyright">© ${new Date().getFullYear()} جميع الحقوق محفوظة | الملف التعليمي لـ ${teacherName}</p>
                    </footer>
                </body>
                </html>`;
                
                return previewHTML;
            }
            
            // دالة تنسيق النص للمعاينة
            function formatTextForPreview(text) {
                return text;
            }
            
            // دالة إنشاء محتوى الصفحة
            function generatePageContent(sectionId, content) {
                let pageContent = '';
                
                switch(sectionId) {
                    case 'home':
                        pageContent = `
                            <div class="teacher-hero">
                                <h2 class="hero-title">${teacherNameInput.value.trim() || "المعلم أحمد محمد"}</h2>
                                <p class="hero-subtitle">
                                    ${content}
                                </p>
                                <div class="teacher-tagline">"العلم نور واللغة العربية جوهرة هذا النور"</div>
                            </div>

                            <div class="achievement-stats">
                                <div class="achievement-card floating" style="animation-delay: 0s;">
                                    <div class="achievement-icon">
                                        <i class="fas fa-user-graduate"></i>
                                    </div>
                                    <span class="achievement-number">15+</span>
                                    <span class="achievement-label">سنة خبرة تعليمية</span>
                                </div>

                                <div class="achievement-card floating" style="animation-delay: 0.2s;">
                                    <div class="achievement-icon" style="background: var(--gradient-secondary);">
                                        <i class="fas fa-book"></i>
                                    </div>
                                    <span class="achievement-number">50+</span>
                                    <span class="achievement-label">بحث ومنشور علمي</span>
                                </div>

                                <div class="achievement-card floating" style="animation-delay: 0.4s;">
                                    <div class="achievement-icon" style="background: var(--gradient-accent);">
                                        <i class="fas fa-award"></i>
                                    </div>
                                    <span class="achievement-number">25+</span>
                                    <span class="achievement-label">جائزة وتكريم</span>
                                </div>

                                <div class="achievement-card floating" style="animation-delay: 0.6s;">
                                    <div class="achievement-icon" style="background: var(--gradient-tertiary);">
                                        <i class="fas fa-users"></i>
                                    </div>
                                    <span class="achievement-number">2000+</span>
                                    <span class="achievement-label">طالب تخرجوا تحت إشرافي</span>
                                </div>
                            </div>`;
                        break;
                        
                    case 'about':
                        pageContent = `
                            <div class="profile-section">
                                <div class="profile-image">
                                    <div class="profile-avatar floating">
                                        <i class="fas fa-chalkboard-teacher"></i>
                                    </div>
                                    <div class="teacher-qualifications">
                                        <div class="qualification-item">
                                            <div class="qualification-title">دكتوراه في اللغة العربية</div>
                                            <div class="qualification-desc">جامعة الملك سعود - 2015</div>
                                        </div>
                                        <div class="qualification-item">
                                            <div class="qualification-title">ماجستير في المناهج وطرق التدريس</div>
                                            <div class="qualification-desc">جامعة القاهرة - 2010</div>
                                        </div>
                                        <div class="qualification-item">
                                            <div class="qualification-title">بكالوريوس اللغة العربية</div>
                                            <div class="qualification-desc">جامعة الأزهر - 2005</div>
                                        </div>
                                    </div>
                                </div>

                                <div class="profile-details">
                                    <h2>${teacherNameInput.value.trim() || "المعلم أحمد محمد"}</h2>
                                    <p class="profile-title">أستاذ اللغة العربية - متخصص في تطوير المناهج التعليمية</p>
                                    
                                    <div class="formatted-text">${content}</div>
                                </div>
                            </div>`;
                        break;
                        
                    case 'experience':
                        pageContent = `
                            <div class="education-timeline">
                                <div class="formatted-text">${content}</div>
                            </div>`;
                        break;
                        
                    case 'achievements':
                        pageContent = `
                            <div class="awards-grid">
                                <div class="award-card">
                                    <div class="award-icon">
                                        <i class="fas fa-medal"></i>
                                    </div>
                                    <h3 class="award-title">جائزة التميز في التدريس</h3>
                                    <div class="award-year">2023</div>
                                    <p class="award-description">
                                        جائزة وزارة التعليم للمعلم المتميز على مستوى المملكة، نظير الإسهامات 
                                        المميزة في تطوير طرق تدريس اللغة العربية.
                                    </p>
                                </div>

                                <div class="award-card">
                                    <div class="award-icon">
                                        <i class="fas fa-trophy"></i>
                                    </div>
                                    <h3 class="award-title">جائزة البحث العلمي</h3>
                                    <div class="award-year">2022</div>
                                    <p class="award-description">
                                        جائزة أفضل بحث علمي في مجال تعليم اللغة العربية، عن بحث "تطوير منهج 
                                        النحو العربي باستخدام التقنيات الحديثة".
                                    </p>
                                </div>

                                <div class="award-card">
                                    <div class="award-icon">
                                        <i class="fas fa-star"></i>
                                    </div>
                                    <h3 class="award-title">وسام التربية والتعليم</h3>
                                    <div class="award-year">2021</div>
                                    <p class="award-description">
                                        تكريم من صاحب السمو الملكي أمير منطقة الرياض لجهودي في تطوير 
                                        التعليم والمساهمة في رفع مستوى التحصيل الدراسي.
                                    </p>
                                </div>
                            </div>
                            <div class="formatted-text" style="margin-top: 2rem;">${content}</div>`;
                        break;
                        
                    case 'methods':
                        pageContent = `
                            <div class="methods-grid">
                                <div class="method-card">
                                    <div class="method-icon">
                                        <i class="fas fa-gamepad"></i>
                                    </div>
                                    <h3 class="method-title">التعلم باللعب</h3>
                                    <p class="method-description">
                                        استخدام الألعاب التعليمية التفاعلية لجعل تعلم اللغة العربية تجربة ممتعة 
                                        وتفاعلية، مما يزيد من دافعية الطلاب ويحسن استيعابهم للمفاهيم.
                                    </p>
                                </div>

                                <div class="method-card">
                                    <div class="method-icon">
                                        <i class="fas fa-laptop-code"></i>
                                    </div>
                                    <h3 class="method-title">التقنية في التعليم</h3>
                                    <p class="method-description">
                                        توظيف التطبيقات والبرامج التعليمية في شرح الدروس، واستخدام الواقع 
                                        المعزز لتعليم النحو والصرف بطريقة مرئية مبسطة.
                                    </p>
                                </div>
                            </div>
                            <div class="formatted-text" style="margin-top: 2rem;">${content}</div>`;
                        break;
                        
                    case 'students':
                        pageContent = `
                            <div class="students-grid">
                                <div class="student-card">
                                    <div class="student-avatar">
                                        <i class="fas fa-user-graduate"></i>
                                    </div>
                                    <h3 class="student-name">خالد أحمد</h3>
                                    <div class="student-achievement">الأول على مستوى المملكة 2023</div>
                                    <p class="student-quote">
                                        "الأستاذ أحمد غيّر نظرتي للغة العربية من مادة صعبة إلى عالم من الجمال والأدب"
                                    </p>
                                </div>

                                <div class="student-card">
                                    <div class="student-avatar">
                                        <i class="fas fa-user-graduate"></i>
                                    </div>
                                    <h3 class="student-name">نورة محمد</h3>
                                    <div class="student-achievement">جائزة القصة القصيرة 2022</div>
                                    <p class="student-quote">
                                        "بفضل أستاذي أحمد، اكتشفت موهبتي في الكتابة الإبداعية وشاركت في مسابقات عديدة"
                                    </p>
                                </div>
                            </div>
                            <div class="formatted-text" style="margin-top: 2rem;">${content}</div>`;
                        break;
                        
                    case 'performance':
                        pageContent = `
                            <div class="performance-grid">
                                <div class="performance-card">
                                    <div class="performance-icon">
                                        <i class="fas fa-chart-line"></i>
                                    </div>
                                    <h3 class="performance-title">تقييم الأداء</h3>
                                    <p class="performance-description">
                                        تقييم أداء ممتاز من قائد المدرسة للعام الدراسي 2022/2023
                                    </p>
                                </div>

                                <div class="performance-card">
                                    <div class="performance-icon">
                                        <i class="fas fa-award"></i>
                                    </div>
                                    <h3 class="performance-title">تكريم الإدارة</h3>
                                    <p class="performance-description">
                                        تقييم "متميز" من الإدارة التعليمية لمدة 3 سنوات متتالية
                                    </p>
                                </div>
                            </div>
                            <div class="formatted-text" style="margin-top: 2rem;">${content}</div>`;
                        break;
                        
                    case 'portfolio':
                        pageContent = `
                            <div class="portfolio-grid">
                                <div class="portfolio-card">
                                    <div class="portfolio-icon">
                                        <i class="fas fa-book"></i>
                                    </div>
                                    <h3 class="portfolio-title">دليل تعليمي تفاعلي</h3>
                                    <p class="portfolio-description">
                                        تصميم دليل تعليمي تفاعلي لطلاب الصف الأول الثانوي في النحو العربي
                                    </p>
                                </div>

                                <div class="portfolio-card">
                                    <div class="portfolio-icon">
                                        <i class="fas fa-video"></i>
                                    </div>
                                    <h3 class="portfolio-title">قناة يوتيوب تعليمية</h3>
                                    <p class="portfolio-description">
                                        إنشاء قناة يوتيوب تعليمية تحتوي على 50 فيديو تعليمي للغة العربية
                                    </p>
                                </div>
                            </div>
                            <div class="formatted-text" style="margin-top: 2rem;">${content}</div>`;
                        break;
                        
                    case 'contact':
                        const contactLines = content.split('\n');
                        let contactCards = '';
                        
                        contactLines.forEach(line => {
                            if (line.trim()) {
                                const parts = line.split(':');
                                if (parts.length >= 2) {
                                    const title = parts[0].trim();
                                    const info = parts.slice(1).join(':').trim();
                                    const icon = getContactIcon(title);
                                    
                                    contactCards += `
                                <div class="contact-card">
                                    <div class="contact-icon">
                                        <i class="fas fa-${icon}"></i>
                                    </div>
                                    <h3 class="contact-title">${title}</h3>
                                    <p class="contact-info">${info}</p>
                                    <a href="${getContactLink(title, info)}" class="contact-btn">${getContactButtonText(title)}</a>
                                </div>`;
                                }
                            }
                        });
                        
                        pageContent = `
                            <div class="contact-container">
                                ${contactCards}
                            </div>`;
                        break;
                        
                    default:
                        pageContent = `<div class="formatted-text">${content}</div>`;
                }
                
                return pageContent;
            }
            
            // دالة الحصول على أيقونة الاتصال
            function getContactIcon(title) {
                if (title.includes('بريد') || title.includes('إلكتروني')) return 'envelope';
                if (title.includes('هاتف') || title.includes('رقم')) return 'phone';
                if (title.includes('تويتر')) return 'twitter';
                if (title.includes('لينكد')) return 'linkedin-in';
                if (title.includes('موقع')) return 'map-marker-alt';
                return 'address-card';
            }
            
            // دالة الحصول على رابط الاتصال
            function getContactLink(title, info) {
                if (title.includes('بريد') || title.includes('إلكتروني')) return `mailto:${info}`;
                if (title.includes('هاتف') || title.includes('رقم')) return `tel:${info.replace(/\s+/g, '')}`;
                if (title.includes('تويتر')) return `https://twitter.com/${info.replace('@', '')}`;
                if (title.includes('لينكد')) return `https://${info}`;
                return '#';
            }
            
            // دالة الحصول على نص زر الاتصال
            function getContactButtonText(title) {
                if (title.includes('بريد') || title.includes('إلكتروني')) return 'إرسال بريد';
                if (title.includes('هاتف') || title.includes('رقم')) return 'اتصال هاتفي';
                if (title.includes('تويتر')) return 'زيارة الملف';
                if (title.includes('لينكد')) return 'عرض الملف';
                if (title.includes('موقع')) return 'عرض الموقع';
                return 'اتصل الآن';
            }
            
            // دالة الحصول على اسم القسم
            function getSectionName(sectionId) {
                const sectionNames = {
                    home: 'الصفحة الرئيسية',
                    about: 'نبذة عني',
                    experience: 'المؤهلات والخبرات',
                    achievements: 'الإنجازات',
                    methods: 'المنهجية التعليمية',
                    students: 'طلاب متميزون',
                    performance: 'شواهد الأداء',
                    portfolio: 'معرض الأعمال',
                    contact: 'بيانات التواصل'
                };
                
                return sectionNames[sectionId] || 'القسم';
            }
            
            // دالة الحصول على وصف القسم
            function getSectionSubtitle(sectionId) {
                const subtitles = {
                    home: 'الملف التعليمي للمعلم - رحلة تعليمية مميزة في خدمة اللغة العربية والطلاب',
                    about: 'السيرة الذاتية والمعلومات الشخصية والتعليمية',
                    experience: 'المسيرة التعليمية والتجارب العملية في مجال التدريس',
                    achievements: 'الجوائز والتكريمات التي حصلت عليها خلال المسيرة التعليمية',
                    methods: 'الأساليب والطرق المبتكرة في تدريس اللغة العربية',
                    students: 'نماذج من الطلاب الذين حققوا تميزاً تحت إشرافي',
                    performance: 'تقييمات الأداء وشواهد التميز في العملية التعليمية',
                    portfolio: 'المشاريع والأعمال التعليمية المميزة',
                    contact: 'للاستشارات التعليمية أو المشاركة في ورش العمل والتدريبات'
                };
                
                return subtitles[sectionId] || 'محتوى القسم';
            }
            
            // دالة إضافة JavaScript للمعاينة
            function addPreviewScript() {
                const previewIframe = previewBody.querySelector('iframe');
                if (previewIframe && previewIframe.contentWindow) {
                    const script = previewIframe.contentWindow.document.createElement('script');
                    script.textContent = `
                        // Page Navigation
                        document.querySelectorAll('.nav-icon-item').forEach(item => {
                            item.addEventListener('click', function(e) {
                                e.preventDefault();
                                
                                const pageId = this.getAttribute('data-page');
                                
                                // Remove active class from all items
                                document.querySelectorAll('.nav-icon-item').forEach(el => {
                                    el.classList.remove('active');
                                });
                                
                                // Add active class to clicked item
                                this.classList.add('active');
                                
                                // Hide all pages
                                document.querySelectorAll('.page').forEach(page => {
                                    page.classList.remove('active');
                                });
                                
                                // Show selected page
                                document.getElementById(pageId + '-page').classList.add('active');
                                
                                // Update page title
                                const pageTitle = this.querySelector('.icon-label').textContent;
                                document.title = 'الملف التعليمي | ' + pageTitle;
                            });
                        });

                        // Add animations to elements when page is shown
                        const observer = new IntersectionObserver((entries) => {
                            entries.forEach(entry => {
                                if (entry.isIntersecting) {
                                    entry.target.classList.add('animated');
                                }
                            });
                        }, { threshold: 0.1 });

                        // Observe all cards for animation
                        document.querySelectorAll('.achievement-card, .award-card, .method-card, .student-card, .contact-card, .performance-card, .portfolio-card').forEach(card => {
                            observer.observe(card);
                        });

                        // Initialize first page
                        document.addEventListener('DOMContentLoaded', () => {
                            document.querySelector('.nav-icon-item.active').click();
                            
                            // Add floating animation to timeline items with delay
                            document.querySelectorAll('.timeline-item').forEach((item, index) => {
                                item.style.animationDelay = (index * 0.2) + 's';
                            });
                        });

                        // Smooth scroll for any anchor links
                        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                            anchor.addEventListener('click', function(e) {
                                e.preventDefault();
                                
                                const pageId = this.getAttribute('href').substring(1);
                                const navItem = document.querySelector('[data-page="' + pageId + '"]');
                                
                                if (navItem) {
                                    navItem.click();
                                    window.scrollTo({ top: 0, behavior: 'smooth' });
                                }
                            });
                        });

                        // Add hover effects to cards
                        document.querySelectorAll('.card, .achievement-card, .award-card, .method-card, .student-card, .contact-card, .performance-card, .portfolio-card').forEach(card => {
                            card.addEventListener('mouseenter', function() {
                                this.style.transition = 'all 0.3s ease';
                            });
                        });
                    `;
                    previewIframe.contentWindow.document.body.appendChild(script);
                }
            }
            
            // دالة إنشاء ملف HTML
            function generateHtmlFile() {
                const teacherName = teacherNameInput.value.trim() || "المعلم أحمد محمد";
                const teacherTitle = "أستاذ لغة عربية ومتخصص في المناهج التعليمية";
                
                // جمع البيانات من جميع الأقسام
                const sectionsData = {};
                Object.keys(defaultTexts).forEach(sectionId => {
                    const textarea = document.getElementById(`${sectionId}-text`);
                    if (textarea) {
                        sectionsData[sectionId] = textarea.value;
                    }
                });
                
                // إنشاء محتوى ملف HTML كامل
                const htmlContent = generateHtmlFileContent(teacherName, teacherTitle, sectionsData);
                
                // إنشاء ملف HTML قابل للتحميل
                const blob = new Blob([htmlContent], { type: 'text/html' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `الملف_التعليمي_${teacherName.replace(/\s+/g, '_')}.html`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                showNotification(`تم إنشاء ملف HTML لـ ${teacherName} بنجاح`);
            }
            
            // دالة إنشاء محتوى ملف HTML كامل
            function generateHtmlFileContent(teacherName, teacherTitle, sectionsData) {
                // استخدام نفس دالة إنشاء محتوى المعاينة ولكن بدون الحاوية الخارجية
                const content = generatePreviewContent(teacherName, teacherTitle, sectionsData);
                return content;
            }
            
            // دالة إنشاء ملف Excel
            function generateExcelFile() {
                const teacherName = teacherNameInput.value.trim() || "المعلم أحمد محمد";
                
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
                    ["الملف التعليمي للمعلم", teacherName],
                    ["تاريخ الإنشاء", new Date().toLocaleDateString('ar-SA')],
                    [""],
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
                    {wch: 25},
                    {wch: 80}
                ];
                ws['!cols'] = wscols;
                
                // إنشاء مصنف وإضافة الورقة
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "الملف التعليمي");
                
                // تصدير الملف
                XLSX.writeFile(wb, `الملف_التعليمي_${teacherName.replace(/\s+/g, '_')}.xlsx`);
                
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
                    background-color: var(--secondary);
                    color: white;
                    padding: 15px 25px;
                    border-radius: 12px;
                    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
                    z-index: 2000;
                    font-weight: 700;
                    animation: fadeInOut 3s ease;
                    display: flex;
                    align-items: center;
                    gap: 10px;
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
                
                notification.innerHTML = `<i class="fas fa-check-circle"></i> ${message}`;
                document.body.appendChild(notification);
                
                // إزالة الإشعار بعد 3 ثواني
                setTimeout(() => {
                    document.body.removeChild(notification);
                    document.head.removeChild(style);
                }, 3000);
            }
            
            // إضافة تأثير النبض للرمز
            const style = document.createElement('style');
            style.textContent = `
                @keyframes pulse {
                    0% { box-shadow: 0 0 0 0 rgba(52, 152, 219, 0.4); }
                    70% { box-shadow: 0 0 0 10px rgba(52, 152, 219, 0); }
                    100% { box-shadow: 0 0 0 0 rgba(52, 152, 219, 0); }
                }
                .pulse {
                    animation: pulse 2s infinite;
                }
            `;
            document.head.appendChild(style);
            
            // إظهار رسالة ترحيب
            showNotification("مرحباً! يمكنك الآن البدء في إنشاء ملفك المهني");
        });
    </script>
</body>
</html>
