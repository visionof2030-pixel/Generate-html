<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منشئ الملف المهني للمعلمين</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #2c5aa0;
            --secondary-color: #4a90e2;
            --accent-color: #f8b739;
            --light-color: #f5f9ff;
            --dark-color: #2c3e50;
            --success-color: #28a745;
            --border-radius: 12px;
            --box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }

        .dark-mode {
            --primary-color: #4a90e2;
            --secondary-color: #6b9fe6;
            --accent-color: #ffcc5c;
            --light-color: #1e2a3a;
            --dark-color: #f8f9fa;
            --box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', sans-serif;
        }

        body {
            background-color: var(--light-color);
            color: var(--dark-color);
            line-height: 1.7;
            transition: var(--transition);
            padding-top: 120px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* الهيدر */
        header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 25px 0;
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .teacher-name-display {
            font-size: 2rem;
            font-weight: 800;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .teacher-name-display input {
            background: transparent;
            border: none;
            color: white;
            font-size: 2rem;
            font-weight: 800;
            width: 400px;
            max-width: 100%;
            outline: none;
            border-bottom: 2px solid rgba(255, 255, 255, 0.3);
            padding: 5px 0;
        }

        .teacher-name-display input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        .header-controls {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .control-btn {
            background: rgba(255, 255, 255, 0.15);
            border: none;
            color: white;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            transition: var(--transition);
        }

        .control-btn:hover {
            background: rgba(255, 255, 255, 0.25);
            transform: translateY(-2px);
        }

        /* شريط التنقل */
        nav {
            background-color: white;
            position: fixed;
            top: 90px;
            width: 100%;
            z-index: 999;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            border-bottom: 1px solid #eee;
        }

        .dark-mode nav {
            background-color: #2a3a4d;
            border-bottom: 1px solid #3a4a5d;
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            overflow-x: auto;
            padding: 0;
        }

        .nav-item {
            padding: 18px 25px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            transition: var(--transition);
            min-width: 120px;
            border-bottom: 3px solid transparent;
            text-decoration: none;
            color: var(--dark-color);
        }

        .dark-mode .nav-item {
            color: #e0e0e0;
        }

        .nav-item:hover, .nav-item.active {
            background-color: rgba(44, 90, 160, 0.05);
            border-bottom: 3px solid var(--accent-color);
        }

        .dark-mode .nav-item:hover, .dark-mode .nav-item.active {
            background-color: rgba(74, 144, 226, 0.1);
        }

        .nav-item i {
            font-size: 1.4rem;
            color: var(--primary-color);
        }

        .dark-mode .nav-item i {
            color: var(--secondary-color);
        }

        .nav-item span {
            font-size: 0.9rem;
            font-weight: 600;
            white-space: nowrap;
        }

        /* المحتوى الرئيسي */
        .main-content {
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 30px;
            margin: 40px 0;
        }

        @media (max-width: 1100px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }

        .section-content {
            background-color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            padding: 30px;
            margin-bottom: 30px;
            display: none;
        }

        .dark-mode .section-content {
            background-color: #2a3a4d;
        }

        .section-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f5ff;
        }

        .dark-mode .section-header {
            border-bottom: 2px solid #3a4a5d;
        }

        .section-title {
            color: var(--primary-color);
            font-size: 1.8rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .dark-mode .section-title {
            color: var(--secondary-color);
        }

        .section-actions {
            display: flex;
            gap: 10px;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: var(--border-radius);
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .btn-primary {
            background-color: var(--primary-color);
            color: white;
        }

        .btn-primary:hover {
            background-color: var(--secondary-color);
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(44, 90, 160, 0.2);
        }

        .btn-secondary {
            background-color: #e9f0ff;
            color: var(--primary-color);
            border: 1px solid #d0ddff;
        }

        .dark-mode .btn-secondary {
            background-color: #3a4a5d;
            color: #e0e0e0;
            border: 1px solid #4a5a6d;
        }

        .btn-secondary:hover {
            background-color: #dae5ff;
        }

        .dark-mode .btn-secondary:hover {
            background-color: #4a5a6d;
        }

        .btn-accent {
            background-color: var(--accent-color);
            color: #333;
        }

        .btn-accent:hover {
            background-color: #e6a429;
            transform: translateY(-2px);
        }

        .btn-success {
            background-color: var(--success-color);
            color: white;
        }

        .btn-success:hover {
            background-color: #218838;
            transform: translateY(-2px);
        }

        /* محتوى القسم */
        .ai-generated-content, .custom-content {
            margin-bottom: 30px;
        }

        .content-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .content-title {
            color: var(--dark-color);
            font-size: 1.3rem;
            font-weight: 600;
        }

        .dark-mode .content-title {
            color: #e0e0e0;
        }

        .ai-text-box, .custom-text-box {
            background-color: #f9fbff;
            border-radius: var(--border-radius);
            padding: 20px;
            border: 1px solid #e1e8f0;
            min-height: 150px;
            line-height: 1.8;
        }

        .dark-mode .ai-text-box, .dark-mode .custom-text-box {
            background-color: #3a4a5d;
            border: 1px solid #4a5a6d;
            color: #e0e0e0;
        }

        .custom-text-box {
            min-height: 200px;
            width: 100%;
            resize: vertical;
            border: 1px solid #e1e8f0;
            font-family: 'Tajawal', sans-serif;
            padding: 15px;
            font-size: 1rem;
            background-color: white;
            color: #333;
        }

        .dark-mode .custom-text-box {
            background-color: #3a4a5d;
            border: 1px solid #4a5a6d;
            color: #e0e0e0;
        }

        /* الشريط الجانبي */
        .sidebar {
            position: sticky;
            top: 150px;
            height: fit-content;
        }

        .progress-card, .preview-card, .actions-card {
            background-color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            padding: 25px;
            margin-bottom: 25px;
        }

        .dark-mode .progress-card, .dark-mode .preview-card, .dark-mode .actions-card {
            background-color: #2a3a4d;
        }

        .card-title {
            color: var(--primary-color);
            font-size: 1.4rem;
            font-weight: 700;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .dark-mode .card-title {
            color: var(--secondary-color);
        }

        .progress-bar {
            height: 12px;
            background-color: #e9ecef;
            border-radius: 6px;
            margin-bottom: 15px;
            overflow: hidden;
        }

        .dark-mode .progress-bar {
            background-color: #3a4a5d;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(to right, var(--primary-color), var(--secondary-color));
            border-radius: 6px;
            width: 0%;
            transition: width 1s ease;
        }

        .progress-text {
            display: flex;
            justify-content: space-between;
            font-weight: 600;
            color: var(--dark-color);
        }

        .dark-mode .progress-text {
            color: #e0e0e0;
        }

        .preview-content {
            background-color: #f9fbff;
            border-radius: var(--border-radius);
            padding: 20px;
            min-height: 300px;
            overflow-y: auto;
            border: 1px solid #e1e8f0;
        }

        .dark-mode .preview-content {
            background-color: #3a4a5d;
            border: 1px solid #4a5a6d;
        }

        .preview-section {
            margin-bottom: 20px;
            padding-bottom: 20px;
            border-bottom: 1px solid #eee;
        }

        .dark-mode .preview-section {
            border-bottom: 1px solid #4a5a6d;
        }

        .preview-section:last-child {
            border-bottom: none;
        }

        .preview-section h3 {
            color: var(--primary-color);
            margin-bottom: 10px;
            font-size: 1.2rem;
        }

        .dark-mode .preview-section h3 {
            color: var(--secondary-color);
        }

        .actions-card .btn {
            width: 100%;
            margin-bottom: 15px;
        }

        /* قسم الملفات */
        .file-upload-area {
            border: 2px dashed #d0ddff;
            border-radius: var(--border-radius);
            padding: 40px 20px;
            text-align: center;
            margin-bottom: 20px;
            transition: var(--transition);
            cursor: pointer;
        }

        .dark-mode .file-upload-area {
            border: 2px dashed #4a5a6d;
        }

        .file-upload-area:hover {
            border-color: var(--secondary-color);
            background-color: rgba(74, 144, 226, 0.05);
        }

        .file-upload-area i {
            font-size: 3rem;
            color: var(--secondary-color);
            margin-bottom: 15px;
        }

        .file-upload-area p {
            color: var(--dark-color);
            margin-bottom: 10px;
            font-weight: 600;
        }

        .dark-mode .file-upload-area p {
            color: #e0e0e0;
        }

        .file-upload-area span {
            color: #6c757d;
            font-size: 0.9rem;
        }

        .uploaded-files {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }

        .file-item {
            background-color: #f0f7ff;
            border-radius: var(--border-radius);
            padding: 15px;
            width: calc(50% - 8px);
            border: 1px solid #d6e6ff;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .dark-mode .file-item {
            background-color: #3a4a5d;
            border: 1px solid #4a5a6d;
        }

        .file-icon {
            width: 50px;
            height: 50px;
            background-color: var(--primary-color);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
        }

        .file-info h4 {
            color: var(--dark-color);
            margin-bottom: 5px;
            font-size: 1rem;
        }

        .dark-mode .file-info h4 {
            color: #e0e0e0;
        }

        .file-info span {
            color: #6c757d;
            font-size: 0.85rem;
        }

        /* قسم التواصل */
        .contact-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        .form-group label {
            color: var(--dark-color);
            margin-bottom: 8px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .dark-mode .form-group label {
            color: #e0e0e0;
        }

        .form-group input {
            padding: 15px;
            border: 1px solid #e1e8f0;
            border-radius: var(--border-radius);
            font-size: 1rem;
            transition: var(--transition);
            background-color: white;
            color: #333;
        }

        .dark-mode .form-group input {
            background-color: #3a4a5d;
            border: 1px solid #4a5a6d;
            color: #e0e0e0;
        }

        .form-group input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.2);
        }

        /* الزر الرئيسي */
        .generate-btn-container {
            text-align: center;
            margin: 50px 0;
        }

        .generate-btn {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 20px 50px;
            font-size: 1.3rem;
            font-weight: 700;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 10px 25px rgba(44, 90, 160, 0.3);
        }

        .generate-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(44, 90, 160, 0.4);
        }

        /* الإشعارات */
        .notification {
            position: fixed;
            bottom: 20px;
            left: 20px;
            padding: 15px 25px;
            border-radius: var(--border-radius);
            color: white;
            font-weight: 500;
            z-index: 1000;
            opacity: 0;
            transform: translateY(20px);
            transition: var(--transition);
            max-width: 400px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .notification.show {
            opacity: 1;
            transform: translateY(0);
        }

        .notification.success {
            background-color: var(--success-color);
        }

        .notification.error {
            background-color: #ff6b6b;
        }

        /* التجاوبية */
        @media (max-width: 768px) {
            body {
                padding-top: 160px;
            }
            
            nav {
                top: 130px;
            }
            
            .teacher-name-display input {
                width: 200px;
                font-size: 1.5rem;
            }
            
            .nav-container {
                padding: 0 10px;
            }
            
            .nav-item {
                min-width: 100px;
                padding: 15px;
            }
            
            .section-content {
                padding: 20px;
            }
            
            .file-item {
                width: 100%;
            }
            
            .generate-btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <!-- الهيدر -->
    <header>
        <div class="container header-content">
            <div class="teacher-name-display">
                <i class="fas fa-chalkboard-teacher"></i>
                <input type="text" id="teacherName" placeholder="أدخل اسمك هنا" maxlength="50">
            </div>
            <div class="header-controls">
                <button class="control-btn" id="languageToggle" title="تبديل اللغة">
                    <i class="fas fa-language"></i>
                </button>
                <button class="control-btn" id="themeToggle" title="الوضع الليلي/النهاري">
                    <i class="fas fa-moon"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- شريط التنقل -->
    <nav>
        <div class="container nav-container">
            <a href="#" class="nav-item active" data-section="about">
                <i class="fas fa-user"></i>
                <span>نبذة عني</span>
            </a>
            <a href="#" class="nav-item" data-section="vision">
                <i class="fas fa-eye"></i>
                <span>الرؤية التعليمية</span>
            </a>
            <a href="#" class="nav-item" data-section="experience">
                <i class="fas fa-briefcase"></i>
                <span>الخبرات</span>
            </a>
            <a href="#" class="nav-item" data-section="achievements">
                <i class="fas fa-trophy"></i>
                <span>الإنجازات</span>
            </a>
            <a href="#" class="nav-item" data-section="courses">
                <i class="fas fa-certificate"></i>
                <span>الدورات التدريبية</span>
            </a>
            <a href="#" class="nav-item" data-section="skills">
                <i class="fas fa-star"></i>
                <span>المهارات</span>
            </a>
            <a href="#" class="nav-item" data-section="certificates">
                <i class="fas fa-award"></i>
                <span>شواهد الأداء</span>
            </a>
            <a href="#" class="nav-item" data-section="portfolio">
                <i class="fas fa-images"></i>
                <span>معرض الأعمال</span>
            </a>
            <a href="#" class="nav-item" data-section="contact">
                <i class="fas fa-address-book"></i>
                <span>بيانات التواصل</span>
            </a>
        </div>
    </nav>

    <!-- المحتوى الرئيسي -->
    <div class="container main-content">
        <div class="sections-container">
            <!-- قسم نبذة عني -->
            <div class="section-content active" id="about-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-user"></i> نبذة عني</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateAbout">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiAboutText">
                        انقر على زر "توليد نص ذكي" لإنشاء نبذة احترافية عنك تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveAbout">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customAboutText" placeholder="أكتب النبذة الخاصة بك هنا..."></textarea>
                </div>
            </div>

            <!-- قسم الرؤية التعليمية -->
            <div class="section-content" id="vision-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-eye"></i> الرؤية التعليمية</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateVision">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiVisionText">
                        انقر على زر "توليد نص ذكي" لإنشاء رؤية تعليمية احترافية تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveVision">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customVisionText" placeholder="أكتب الرؤية التعليمية الخاصة بك هنا..."></textarea>
                </div>
            </div>

            <!-- قسم الخبرات -->
            <div class="section-content" id="experience-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-briefcase"></i> الخبرات التعليمية</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateExperience">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiExperienceText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص عن خبراتك التعليمية تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveExperience">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customExperienceText" placeholder="أكتب خبراتك التعليمية هنا..."></textarea>
                </div>
            </div>

            <!-- قسم الإنجازات -->
            <div class="section-content" id="achievements-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-trophy"></i> الإنجازات</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateAchievements">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiAchievementsText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص عن إنجازاتك تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveAchievements">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customAchievementsText" placeholder="أكتب إنجازاتك هنا..."></textarea>
                </div>
            </div>

            <!-- قسم الدورات التدريبية -->
            <div class="section-content" id="courses-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-certificate"></i> الدورات التدريبية</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateCourses">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiCoursesText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص عن دوراتك التدريبية تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveCourses">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customCoursesText" placeholder="أكتب دوراتك التدريبية هنا..."></textarea>
                </div>
            </div>

            <!-- قسم المهارات -->
            <div class="section-content" id="skills-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-star"></i> المهارات</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateSkills">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiSkillsText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص عن مهاراتك تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveSkills">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customSkillsText" placeholder="أكتب مهاراتك هنا..."></textarea>
                </div>
            </div>

            <!-- قسم شواهد الأداء -->
            <div class="section-content" id="certificates-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-award"></i> شواهد الأداء</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateCertificates">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiCertificatesText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص عن شواهد أدائك تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveCertificates">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customCertificatesText" placeholder="أكتب عن شواهد أدائك هنا..."></textarea>
                </div>
                
                <!-- رفع الملفات -->
                <div class="file-upload-area" id="certificatesUpload">
                    <i class="fas fa-cloud-upload-alt"></i>
                    <p>اسحب وأفلت الشهادات هنا أو انقر للرفع</p>
                    <span>يدعم PDF، JPG، PNG (حتى 5MB لكل ملف)</span>
                </div>
                <input type="file" id="certificatesInput" accept=".pdf,.jpg,.jpeg,.png" multiple style="display: none;">
                
                <div class="uploaded-files" id="certificatesList">
                    <!-- الملفات المرفوعة تظهر هنا -->
                </div>
            </div>

            <!-- قسم معرض الأعمال -->
            <div class="section-content" id="portfolio-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-images"></i> معرض الأعمال</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generatePortfolio">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiPortfolioText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص عن معرض أعمالك تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="savePortfolio">
                            <i class="fas fa-save"></i> حفظ النص
                        </button>
                    </div>
                    <textarea class="custom-text-box" id="customPortfolioText" placeholder="أكتب عن معرض أعمالك هنا..."></textarea>
                </div>
                
                <!-- رفع الملفات -->
                <div class="file-upload-area" id="portfolioUpload">
                    <i class="fas fa-cloud-upload-alt"></i>
                    <p>اسحب وأفلت ملفات معرض الأعمال هنا أو انقر للرفع</p>
                    <span>يدعم الصور، PDF، والملفات الأخرى (حتى 10MB لكل ملف)</span>
                </div>
                <input type="file" id="portfolioInput" accept=".pdf,.jpg,.jpeg,.png,.doc,.docx,.ppt,.pptx" multiple style="display: none;">
                
                <div class="uploaded-files" id="portfolioList">
                    <!-- الملفات المرفوعة تظهر هنا -->
                </div>
            </div>

            <!-- قسم بيانات التواصل -->
            <div class="section-content" id="contact-section">
                <div class="section-header">
                    <h2 class="section-title"><i class="fas fa-address-book"></i> بيانات التواصل</h2>
                    <div class="section-actions">
                        <button class="btn btn-accent" id="generateContact">
                            <i class="fas fa-robot"></i> توليد نص ذكي
                        </button>
                    </div>
                </div>
                
                <div class="ai-generated-content">
                    <div class="content-header">
                        <h3 class="content-title">النص المولد تلقائياً</h3>
                    </div>
                    <div class="ai-text-box" id="aiContactText">
                        انقر على زر "توليد نص ذكي" لإنشاء نص احترافي لبيانات التواصل تلقائياً.
                    </div>
                </div>
                
                <div class="custom-content">
                    <div class="content-header">
                        <h3 class="content-title">التعديل اليدوي</h3>
                        <button class="btn btn-success" id="saveContact">
                            <i class="fas fa-save"></i> حفظ البيانات
                        </button>
                    </div>
                    
                    <div class="contact-form">
                        <div class="form-group">
                            <label for="phone"><i class="fas fa-phone"></i> رقم الجوال</label>
                            <input type="text" id="phone" placeholder="مثال: 0551234567">
                        </div>
                        
                        <div class="form-group">
                            <label for="email"><i class="fas fa-envelope"></i> البريد الإلكتروني</label>
                            <input type="email" id="email" placeholder="مثال: name@example.com">
                        </div>
                        
                        <div class="form-group">
                            <label for="whatsapp"><i class="fab fa-whatsapp"></i> رابط الواتساب</label>
                            <input type="text" id="whatsapp" placeholder="مثال: https://wa.me/966551234567">
                        </div>
                        
                        <div class="form-group">
                            <label for="twitter"><i class="fab fa-twitter"></i> رابط تويتر (X)</label>
                            <input type="text" id="twitter" placeholder="مثال: https://twitter.com/username">
                        </div>
                        
                        <div class="form-group">
                            <label for="linkedin"><i class="fab fa-linkedin"></i> رابط LinkedIn</label>
                            <input type="text" id="linkedin" placeholder="مثال: https://linkedin.com/in/username">
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- الشريط الجانبي -->
        <div class="sidebar">
            <!-- تقدم الإكمال -->
            <div class="progress-card">
                <h3 class="card-title"><i class="fas fa-chart-line"></i> تقدم الإكمال</h3>
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill"></div>
                </div>
                <div class="progress-text">
                    <span>الإكمال</span>
                    <span id="progressPercent">0%</span>
                </div>
                <p style="margin-top: 15px; color: #6c757d; font-size: 0.9rem;">
                    أكمل جميع الأقسام لإنشاء ملف مهني متكامل
                </p>
            </div>

            <!-- معاينة سريعة -->
            <div class="preview-card">
                <h3 class="card-title"><i class="fas fa-eye"></i> معاينة سريعة</h3>
                <div class="preview-content" id="quickPreview">
                    <div class="preview-section">
                        <h3>الاسم</h3>
                        <p id="previewName">لم يتم إدخال الاسم بعد</p>
                    </div>
                    <div class="preview-section">
                        <h3>نبذة مختصرة</h3>
                        <p id="previewBio">لم يتم إدخال النبذة بعد</p>
                    </div>
                    <div class="preview-section">
                        <h3>بيانات التواصل</h3>
                        <p id="previewContact">لم يتم إدخال بيانات التواصل بعد</p>
                    </div>
                </div>
            </div>

            <!-- الإجراءات السريعة -->
            <div class="actions-card">
                <h3 class="card-title"><i class="fas fa-bolt"></i> إجراءات سريعة</h3>
                <button class="btn btn-primary" id="saveAllBtn">
                    <i class="fas fa-save"></i> حفظ كل البيانات
                </button>
                <button class="btn btn-secondary" id="loadSampleBtn">
                    <i class="fas fa-magic"></i> تحميل بيانات تجريبية
                </button>
                <button class="btn btn-secondary" id="resetAllBtn">
                    <i class="fas fa-trash-alt"></i> مسح كل البيانات
                </button>
                <button class="btn btn-success" id="exportDataBtn">
                    <i class="fas fa-download"></i> تصدير البيانات
                </button>
            </div>
        </div>
    </div>

    <!-- زر إنشاء الملف المهني -->
    <div class="container generate-btn-container">
        <button class="generate-btn" id="generatePortfolioBtn">
            <i class="fas fa-file-code"></i> إنشاء الملف المهني النهائي
        </button>
    </div>

    <!-- الإشعارات -->
    <div id="notification" class="notification"></div>

    <script>
        // ============== البيانات والمتغيرات ==============
        let teacherData = {
            name: '',
            about: { ai: '', custom: '' },
            vision: { ai: '', custom: '' },
            experience: { ai: '', custom: '' },
            achievements: { ai: '', custom: '' },
            courses: { ai: '', custom: '' },
            skills: { ai: '', custom: '' },
            certificates: { ai: '', custom: '', files: [] },
            portfolio: { ai: '', custom: '', files: [] },
            contact: { 
                ai: '', 
                custom: '',
                phone: '',
                email: '',
                whatsapp: '',
                twitter: '',
                linkedin: ''
            }
        };
        
        let currentLanguage = 'ar';
        let isDarkMode = false;
        let currentSection = 'about';
        
        // ============== عناصر DOM ==============
        const teacherNameInput = document.getElementById('teacherName');
        const languageToggle = document.getElementById('languageToggle');
        const themeToggle = document.getElementById('themeToggle');
        const navItems = document.querySelectorAll('.nav-item');
        const sections = document.querySelectorAll('.section-content');
        const generateButtons = document.querySelectorAll('[id^="generate"]');
        const saveButtons = document.querySelectorAll('[id^="save"]');
        const notification = document.getElementById('notification');
        const progressFill = document.getElementById('progressFill');
        const progressPercent = document.getElementById('progressPercent');
        const saveAllBtn = document.getElementById('saveAllBtn');
        const loadSampleBtn = document.getElementById('loadSampleBtn');
        const resetAllBtn = document.getElementById('resetAllBtn');
        const exportDataBtn = document.getElementById('exportDataBtn');
        const generatePortfolioBtn = document.getElementById('generatePortfolioBtn');
        
        // عناصر المعاينة السريعة
        const previewName = document.getElementById('previewName');
        const previewBio = document.getElementById('previewBio');
        const previewContact = document.getElementById('previewContact');
        
        // ============== تهيئة التطبيق ==============
        document.addEventListener('DOMContentLoaded', () => {
            // تحميل البيانات المحفوظة
            loadSavedData();
            
            // إضافة مستمعي الأحداث
            setupEventListeners();
            
            // تحديث المعاينة والتقدم
            updateProgress();
            updatePreview();
            
            // تفعيل الوضع الليلي إذا كان محفوظ
            if (localStorage.getItem('darkMode') === 'true') {
                toggleDarkMode();
            }
        });
        
        // ============== إعداد مستمعي الأحداث ==============
        function setupEventListeners() {
            // تبديل اللغة
            languageToggle.addEventListener('click', toggleLanguage);
            
            // تبديل الوضع الليلي
            themeToggle.addEventListener('click', toggleDarkMode);
            
            // تغيير اسم المعلم
            teacherNameInput.addEventListener('input', (e) => {
                teacherData.name = e.target.value;
                updatePreview();
                saveToLocalStorage();
            });
            
            // التنقل بين الأقسام
            navItems.forEach(item => {
                item.addEventListener('click', (e) => {
                    e.preventDefault();
                    const sectionId = item.getAttribute('data-section');
                    switchSection(sectionId);
                });
            });
            
            // أزرار التوليد التلقائي
            document.getElementById('generateAbout').addEventListener('click', () => generateAIText('about'));
            document.getElementById('generateVision').addEventListener('click', () => generateAIText('vision'));
            document.getElementById('generateExperience').addEventListener('click', () => generateAIText('experience'));
            document.getElementById('generateAchievements').addEventListener('click', () => generateAIText('achievements'));
            document.getElementById('generateCourses').addEventListener('click', () => generateAIText('courses'));
            document.getElementById('generateSkills').addEventListener('click', () => generateAIText('skills'));
            document.getElementById('generateCertificates').addEventListener('click', () => generateAIText('certificates'));
            document.getElementById('generatePortfolio').addEventListener('click', () => generateAIText('portfolio'));
            document.getElementById('generateContact').addEventListener('click', () => generateAIText('contact'));
            
            // أزرار الحفظ
            document.getElementById('saveAbout').addEventListener('click', () => saveCustomText('about'));
            document.getElementById('saveVision').addEventListener('click', () => saveCustomText('vision'));
            document.getElementById('saveExperience').addEventListener('click', () => saveCustomText('experience'));
            document.getElementById('saveAchievements').addEventListener('click', () => saveCustomText('achievements'));
            document.getElementById('saveCourses').addEventListener('click', () => saveCustomText('courses'));
            document.getElementById('saveSkills').addEventListener('click', () => saveCustomText('skills'));
            document.getElementById('saveCertificates').addEventListener('click', () => saveCustomText('certificates'));
            document.getElementById('savePortfolio').addEventListener('click', () => saveCustomText('portfolio'));
            document.getElementById('saveContact').addEventListener('click', saveContactData);
            
            // رفع الملفات
            document.getElementById('certificatesUpload').addEventListener('click', () => {
                document.getElementById('certificatesInput').click();
            });
            
            document.getElementById('portfolioUpload').addEventListener('click', () => {
                document.getElementById('portfolioInput').click();
            });
            
            document.getElementById('certificatesInput').addEventListener('change', (e) => handleFileUpload(e, 'certificates'));
            document.getElementById('portfolioInput').addEventListener('change', (e) => handleFileUpload(e, 'portfolio'));
            
            // الإجراءات السريعة
            saveAllBtn.addEventListener('click', saveAllData);
            loadSampleBtn.addEventListener('click', loadSampleData);
            resetAllBtn.addEventListener('click', resetAllData);
            exportDataBtn.addEventListener('click', exportData);
            generatePortfolioBtn.addEventListener('click', generateFinalPortfolio);
            
            // تحديث النصوص تلقائياً عند الكتابة
            document.querySelectorAll('.custom-text-box').forEach(textarea => {
                textarea.addEventListener('input', (e) => {
                    updatePreview();
                });
            });
            
            // تحديث بيانات التواصل عند الكتابة
            document.querySelectorAll('.contact-form input').forEach(input => {
                input.addEventListener('input', (e) => {
                    updatePreview();
                });
            });
        }
        
        // ============== وظائف التنقل ==============
        function switchSection(sectionId) {
            // تحديث القسم النشط في شريط التنقل
            navItems.forEach(item => {
                item.classList.remove('active');
                if (item.getAttribute('data-section') === sectionId) {
                    item.classList.add('active');
                }
            });
            
            // إظهار القسم المحدد وإخفاء الآخرين
            sections.forEach(section => {
                section.classList.remove('active');
                if (section.id === `${sectionId}-section`) {
                    section.classList.add('active');
                }
            });
            
            currentSection = sectionId;
        }
        
        // ============== توليد النصوص بالذكاء الاصطناعي ==============
        function generateAIText(section) {
            // في التطبيق الحقيقي، هنا سيتم استدعاء واجهة برمجة تطبيقات الذكاء الاصطناعي
            // لكننا سنستخدم نصوصاً مخزنة مسبقاً للعرض التوضيحي
            
            const aiTexts = {
                about: "أنا معلم متخصص في مجال التعليم، حاصل على شهادة الماجستير في التربية، وأملك خبرة تزيد عن 10 سنوات في التدريس. أؤمن بأهمية التعليم التفاعلي والتطوير المستمر للمناهج التعليمية. أسعى دائماً إلى إلهام طلابي وتحفيزهم للوصول إلى أقصى إمكاناتهم الأكاديمية والشخصية.",
                
                vision: "رؤيتي التعليمية تتمحور حول بناء جيل من المتعلمين المستقلين القادرين على التفكير النقدي والإبداعي. أهدف إلى خلق بيئة تعليمية محفزة تدمج بين التكنولوجيا الحديثة والطرق التعليمية التقليدية، مما يمكن الطلاب من اكتساب المعرفة والمهارات الحياتية اللازمة للنجاح في القرن الحادي والعشرين.",
                
                experience: "أملك خبرة واسعة في التدريس تشمل أكثر من 10 سنوات في مجال التعليم. عملت في عدة مدارس مرموقة وقمت بتدريس مختلف المواد الدراسية. قمت بتطوير مناهج تعليمية مبتكرة وحصلت على تقييمات متميزة من الطلاب والإدارة. كما أشرفت على تدريب المعلمين الجدد وشاركت في لجان تطوير المناهج التعليمية.",
                
                achievements: "من أبرز إنجازاتي: الحصول على جائزة المعلم المتميز على مستوى المنطقة ثلاث مرات، تطوير برنامج تعليمي مبتكر حصل على اعتماد وزارة التعليم، قيادة فريق تحسين نتائج الطلاب بنسبة 40% خلال ثلاث سنوات، نشر بحثين في مجلات تربوية محكمة، وتقديم ورش عمل للمعلمين على مستوى الوطن.",
                
                courses: "حضرت العديد من الدورات التدريبية المتميزة منها: دورة استراتيجيات التدريس الحديثة (120 ساعة)، دورة استخدام التكنولوجيا في التعليم (80 ساعة)، دورة التقييم التربوي الفعال (60 ساعة)، دورة التعامل مع صعوبات التعلم (90 ساعة)، دورة القيادة التربوية (100 ساعة)، ودورة الإبداع في تصميم الأنشطة الصفية (70 ساعة).",
                
                skills: "أتمتع بمهارات تعليمية وتقنية متعددة منها: إتقان استراتيجيات التعليم التفاعلي، تصميم المناهج التعليمية، استخدام التكنولوجيا في التعليم، إدارة الصف الفعالة، التقييم التربوي، التدريب والتوجيه، البحث التربوي، التواصل الفعال مع أولياء الأمور، العمل الجماعي، والتفكير الإبداعي في حل المشكلات التعليمية.",
                
                certificates: "حاصل على عدة شهادات أداء معتمدة منها: شهادة المعلم المتميز من وزارة التعليم، شهادة تقدير لأفضل أداء تعليمي، شهادة مشاركة في مؤتمر التطوير التربوي، شهادة إتمام برنامج القيادة التربوية، شهادة تقدير لتميز نتائج الطلاب، وشهادة مشاركة في تأليف كتاب تعليمي مساند للمنهج الدراسي.",
                
                portfolio: "يضم معرض أعمالي: تصميم منهج تعليمي متكامل للصف السادس، تطوير دليل المعلم للصفوف المتوسطة، إنشاء مكتبة رقمية للمصادر التعليمية، تصميم أنشطة تعليمية تفاعلية، إنتاج فيديوهات تعليمية لشرح الدروس الصعبة، وتصميم أدوات تقييم إلكترونية للطلاب.",
                
                contact: "يمكن التواصل معي عبر: رقم الجوال: 0551234567، البريد الإلكتروني: teacher@example.com، رابط الواتساب: https://wa.me/966551234567، حساب تويتر: @TeacherProfile، حساب LinkedIn: linkedin.com/in/teacherprofile. أنا متاح للإجابة على الاستفسارات والتعاون في المشاريع التعليمية."
            };
            
            // تحديث النص في الواجهة
            const aiTextBox = document.getElementById(`ai${capitalizeFirstLetter(section)}Text`);
            if (aiTextBox) {
                aiTextBox.textContent = aiTexts[section];
                teacherData[section].ai = aiTexts[section];
                showNotification('تم توليد النص بنجاح', 'success');
                saveToLocalStorage();
                updateProgress();
            }
        }
        
        // ============== حفظ النصوص المخصصة ==============
        function saveCustomText(section) {
            const textarea = document.getElementById(`custom${capitalizeFirstLetter(section)}Text`);
            if (textarea) {
                teacherData[section].custom = textarea.value;
                showNotification('تم حفظ النص بنجاح', 'success');
                saveToLocalStorage();
                updateProgress();
            }
        }
        
        // ============== حفظ بيانات التواصل ==============
        function saveContactData() {
            teacherData.contact.phone = document.getElementById('phone').value;
            teacherData.contact.email = document.getElementById('email').value;
            teacherData.contact.whatsapp = document.getElementById('whatsapp').value;
            teacherData.contact.twitter = document.getElementById('twitter').value;
            teacherData.contact.linkedin = document.getElementById('linkedin').value;
            
            showNotification('تم حفظ بيانات التواصل بنجاح', 'success');
            saveToLocalStorage();
            updateProgress();
        }
        
        // ============== رفع الملفات ==============
        function handleFileUpload(event, section) {
            const files = event.target.files;
            if (files.length > 0) {
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    const fileSize = (file.size / (1024 * 1024)).toFixed(2); // بالميغابايت
                    
                    // التحقق من حجم الملف
                    if (fileSize > (section === 'certificates' ? 5 : 10)) {
                        showNotification(`حجم الملف ${file.name} كبير جداً`, 'error');
                        continue;
                    }
                    
                    // إضافة الملف إلى البيانات
                    teacherData[section].files.push({
                        name: file.name,
                        size: fileSize + ' MB',
                        type: file.type,
                        date: new Date().toLocaleDateString('ar-SA')
                    });
                }
                
                // تحديث عرض الملفات
                updateFileList(section);
                showNotification(`تم رفع ${files.length} ملف بنجاح`, 'success');
                saveToLocalStorage();
                updateProgress();
            }
        }
        
        // ============== تحديث قائمة الملفات ==============
        function updateFileList(section) {
            const fileList = document.getElementById(`${section}List`);
            if (!fileList) return;
            
            fileList.innerHTML = '';
            
            teacherData[section].files.forEach((file, index) => {
                const fileItem = document.createElement('div');
                fileItem.className = 'file-item';
                fileItem.innerHTML = `
                    <div class="file-icon">
                        <i class="${getFileIcon(file.type)}"></i>
                    </div>
                    <div class="file-info">
                        <h4>${file.name}</h4>
                        <span>${file.size} • ${file.date}</span>
                    </div>
                `;
                fileList.appendChild(fileItem);
            });
        }
        
        // ============== تحديث التقدم ==============
        function updateProgress() {
            let filledSections = 0;
            const totalSections = 9; // عدد الأقسام الرئيسية
            
            // حساب الأقسام المكتملة
            if (teacherData.name.trim()) filledSections++;
            if (teacherData.about.custom.trim() || teacherData.about.ai.trim()) filledSections++;
            if (teacherData.vision.custom.trim() || teacherData.vision.ai.trim()) filledSections++;
            if (teacherData.experience.custom.trim() || teacherData.experience.ai.trim()) filledSections++;
            if (teacherData.achievements.custom.trim() || teacherData.achievements.ai.trim()) filledSections++;
            if (teacherData.courses.custom.trim() || teacherData.courses.ai.trim()) filledSections++;
            if (teacherData.skills.custom.trim() || teacherData.skills.ai.trim()) filledSections++;
            if (teacherData.contact.phone.trim() || teacherData.contact.email.trim()) filledSections++;
            if (teacherData.certificates.files.length > 0 || teacherData.portfolio.files.length > 0) filledSections++;
            
            // حساب النسبة المئوية
            const percentage = Math.round((filledSections / totalSections) * 100);
            
            // تحديث العرض
            progressFill.style.width = `${percentage}%`;
            progressPercent.textContent = `${percentage}%`;
        }
        
        // ============== تحديث المعاينة السريعة ==============
        function updatePreview() {
            // تحديث الاسم
            previewName.textContent = teacherNameInput.value || 'لم يتم إدخال الاسم بعد';
            
            // تحديث النبذة
            const aboutText = teacherData.about.custom || teacherData.about.ai || 
                             document.getElementById('customAboutText')?.value || 
                             'لم يتم إدخال النبذة بعد';
            previewBio.textContent = aboutText.length > 150 ? aboutText.substring(0, 150) + '...' : aboutText;
            
            // تحديث بيانات التواصل
            const phone = document.getElementById('phone')?.value || teacherData.contact.phone;
            const email = document.getElementById('email')?.value || teacherData.contact.email;
            
            let contactText = 'لم يتم إدخال بيانات التواصل بعد';
            if (phone || email) {
                contactText = '';
                if (phone) contactText += `هاتف: ${phone}`;
                if (email) contactText += `${phone ? '، ' : ''}بريد: ${email}`;
            }
            previewContact.textContent = contactText;
        }
        
        // ============== حفظ كل البيانات ==============
        function saveAllData() {
            // حفظ جميع النصوص المخصصة
            saveCustomText('about');
            saveCustomText('vision');
            saveCustomText('experience');
            saveCustomText('achievements');
            saveCustomText('courses');
            saveCustomText('skills');
            saveCustomText('certificates');
            saveCustomText('portfolio');
            saveContactData();
            
            showNotification('تم حفظ جميع البيانات بنجاح', 'success');
        }
        
        // ============== تحميل بيانات تجريبية ==============
        function loadSampleData() {
            if (confirm('هل تريد تحميل بيانات تجريبية؟ سيتم استبدال البيانات الحالية.')) {
                // تعبئة البيانات التجريبية
                teacherNameInput.value = 'أحمد محمد العلي';
                teacherData.name = 'أحمد محمد العلي';
                
                // تعبئة النصوص
                const sections = ['about', 'vision', 'experience', 'achievements', 'courses', 'skills', 'certificates', 'portfolio', 'contact'];
                sections.forEach(section => {
                    generateAIText(section);
                    
                    const textarea = document.getElementById(`custom${capitalizeFirstLetter(section)}Text`);
                    if (textarea) {
                        textarea.value = `هذا نص مخصص للقسم: ${section}. يمكنك تعديله كما تريد.`;
                        teacherData[section].custom = textarea.value;
                    }
                });
                
                // تعبئة بيانات التواصل
                document.getElementById('phone').value = '0551234567';
                document.getElementById('email').value = 'ahmed.ali@school.edu.sa';
                document.getElementById('whatsapp').value = 'https://wa.me/966551234567';
                document.getElementById('twitter').value = 'https://twitter.com/ahmed_ali_edu';
                document.getElementById('linkedin').value = 'https://linkedin.com/in/ahmed-ali-educator';
                
                saveContactData();
                
                // إضافة ملفات تجريبية
                teacherData.certificates.files = [
                    { name: 'شهادة المعلم المتميز.pdf', size: '2.4 MB', type: 'application/pdf', date: '2023-05-15' },
                    { name: 'شهادة التدريب.jpg', size: '1.8 MB', type: 'image/jpeg', date: '2023-08-22' }
                ];
                
                teacherData.portfolio.files = [
                    { name: 'تصميم المنهج التعليمي.docx', size: '3.2 MB', type: 'application/vnd.openxmlformats-officedocument.wordprocessingml.document', date: '2023-10-10' },
                    { name: 'عرض تقديمي للورشة.pptx', size: '4.5 MB', type: 'application/vnd.openxmlformats-officedocument.presentationml.presentation', date: '2023-11-05' }
                ];
                
                updateFileList('certificates');
                updateFileList('portfolio');
                
                showNotification('تم تحميل البيانات التجريبية بنجاح', 'success');
                updateProgress();
                updatePreview();
                saveToLocalStorage();
            }
        }
        
        // ============== مسح كل البيانات ==============
        function resetAllData() {
            if (confirm('هل أنت متأكد من مسح جميع البيانات؟ لا يمكن التراجع عن هذا الإجراء.')) {
                // إعادة تعيين جميع الحقول
                teacherNameInput.value = '';
                teacherData = {
                    name: '',
                    about: { ai: '', custom: '' },
                    vision: { ai: '', custom: '' },
                    experience: { ai: '', custom: '' },
                    achievements: { ai: '', custom: '' },
                    courses: { ai: '', custom: '' },
                    skills: { ai: '', custom: '' },
                    certificates: { ai: '', custom: '', files: [] },
                    portfolio: { ai: '', custom: '', files: [] },
                    contact: { 
                        ai: '', 
                        custom: '',
                        phone: '',
                        email: '',
                        whatsapp: '',
                        twitter: '',
                        linkedin: ''
                    }
                };
                
                // مسح جميع حقول النصوص
                document.querySelectorAll('.custom-text-box').forEach(textarea => {
                    textarea.value = '';
                });
                
                // مسح حقول التواصل
                document.querySelectorAll('.contact-form input').forEach(input => {
                    input.value = '';
                });
                
                // مسح النصوص المولدة
                document.querySelectorAll('.ai-text-box').forEach(div => {
                    div.textContent = 'انقر على زر "توليد نص ذكي" لإنشاء نص احترافي تلقائياً.';
                });
                
                // مسح قوائم الملفات
                document.getElementById('certificatesList').innerHTML = '';
                document.getElementById('portfolioList').innerHTML = '';
                
                // مسح التخزين المحلي
                localStorage.removeItem('teacherPortfolioData');
                
                showNotification('تم مسح جميع البيانات بنجاح', 'success');
                updateProgress();
                updatePreview();
            }
        }
        
        // ============== تصدير البيانات ==============
        function exportData() {
            const dataStr = JSON.stringify(teacherData, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            
            const exportFileDefaultName = `بيانات_الملف_المهني_${new Date().toISOString().slice(0,10)}.json`;
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
            
            showNotification('تم تصدير البيانات بنجاح', 'success');
        }
        
        // ============== إنشاء الملف المهني النهائي ==============
        function generateFinalPortfolio() {
            // التحقق من إدخال الاسم
            if (!teacherData.name.trim()) {
                showNotification('يرجى إدخال اسم المعلم أولاً', 'error');
                teacherNameInput.focus();
                return;
            }
            
            // حفظ جميع البيانات أولاً
            saveAllData();
            
            // إنشاء محتوى HTML للصفحة النهائية
            const htmlContent = createPortfolioHTML();
            
            // فتح النافذة لمعاينة الملف
            const newWindow = window.open();
            newWindow.document.write(htmlContent);
            newWindow.document.close();
            
            // توفير رابط للتنزيل
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `الملف_المهني_${teacherData.name.replace(/\s+/g, '_')}.html`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showNotification('تم إنشاء الملف المهني وتنزيله بنجاح', 'success');
        }
        
        // ============== إنشاء HTML للصفحة النهائية ==============
        function createPortfolioHTML() {
            const getContent = (section) => {
                return teacherData[section].custom || teacherData[section].ai || 'لم يتم إضافة محتوى';
            };
            
            return `<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الملف المهني - ${teacherData.name}</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #2c5aa0;
            --secondary-color: #4a90e2;
            --accent-color: #f8b739;
            --light-color: #f5f9ff;
            --dark-color: #2c3e50;
            --border-radius: 12px;
            --box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', sans-serif;
        }
        
        body {
            background-color: #f0f5ff;
            color: #333;
            line-height: 1.7;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .portfolio-header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 50px 40px;
            border-radius: var(--border-radius);
            text-align: center;
            margin-bottom: 40px;
            box-shadow: var(--box-shadow);
        }
        
        .teacher-name {
            font-size: 3rem;
            font-weight: 800;
            margin-bottom: 15px;
        }
        
        .teacher-title {
            font-size: 1.5rem;
            opacity: 0.9;
            margin-bottom: 25px;
        }
        
        .contact-info {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 25px;
            margin-top: 20px;
        }
        
        .contact-item {
            display: flex;
            align-items: center;
            gap: 10px;
            color: white;
            font-size: 1.05rem;
        }
        
        .contact-item i {
            color: var(--accent-color);
        }
        
        .portfolio-section {
            background-color: white;
            border-radius: var(--border-radius);
            padding: 35px;
            margin-bottom: 30px;
            box-shadow: var(--box-shadow);
        }
        
        .section-title {
            color: var(--primary-color);
            font-size: 1.8rem;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f5ff;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .section-title i {
            color: var(--accent-color);
        }
        
        .section-content {
            color: #555;
            line-height: 1.9;
            font-size: 1.1rem;
        }
        
        .files-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .file-card {
            background-color: #f9fbff;
            border-radius: var(--border-radius);
            padding: 20px;
            border: 1px solid #e1e8f0;
            display: flex;
            align-items: center;
            gap: 15px;
            transition: transform 0.3s ease;
        }
        
        .file-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
        }
        
        .file-icon {
            width: 60px;
            height: 60px;
            background-color: var(--primary-color);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.8rem;
        }
        
        .file-info h4 {
            color: var(--dark-color);
            margin-bottom: 5px;
            font-size: 1.1rem;
        }
        
        .file-info span {
            color: #6c757d;
            font-size: 0.9rem;
        }
        
        .footer-note {
            text-align: center;
            padding: 25px;
            background-color: #f0f7ff;
            border-radius: var(--border-radius);
            color: var(--dark-color);
            font-size: 0.95rem;
            margin-top: 50px;
        }
        
        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            
            .portfolio-header {
                padding: 30px 20px;
            }
            
            .teacher-name {
                font-size: 2.2rem;
            }
            
            .portfolio-section {
                padding: 25px 20px;
            }
            
            .contact-info {
                flex-direction: column;
                gap: 15px;
            }
        }
        
        @media print {
            body {
                background-color: white;
                padding: 0;
            }
            
            .portfolio-header {
                box-shadow: none;
            }
            
            .portfolio-section {
                box-shadow: none;
                page-break-inside: avoid;
            }
            
            .footer-note {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="portfolio-header">
            <h1 class="teacher-name">${teacherData.name}</h1>
            <p class="teacher-title">ملف مهني احترافي للمعلم</p>
            <div class="contact-info">
                ${teacherData.contact.phone ? `<div class="contact-item">
                    <i class="fas fa-phone"></i>
                    <span>${teacherData.contact.phone}</span>
                </div>` : ''}
                ${teacherData.contact.email ? `<div class="contact-item">
                    <i class="fas fa-envelope"></i>
                    <span>${teacherData.contact.email}</span>
                </div>` : ''}
                ${teacherData.contact.whatsapp ? `<div class="contact-item">
                    <i class="fab fa-whatsapp"></i>
                    <span>واتساب</span>
                </div>` : ''}
            </div>
        </div>
        
        ${getContent('about') ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-user"></i> نبذة عني</h2>
            <div class="section-content">${getContent('about').replace(/\n/g, '<br>')}</div>
        </div>` : ''}
        
        ${getContent('vision') ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-eye"></i> الرؤية التعليمية</h2>
            <div class="section-content">${getContent('vision').replace(/\n/g, '<br>')}</div>
        </div>` : ''}
        
        ${getContent('experience') ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-briefcase"></i> الخبرات التعليمية</h2>
            <div class="section-content">${getContent('experience').replace(/\n/g, '<br>')}</div>
        </div>` : ''}
        
        ${getContent('achievements') ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-trophy"></i> الإنجازات</h2>
            <div class="section-content">${getContent('achievements').replace(/\n/g, '<br>')}</div>
        </div>` : ''}
        
        ${getContent('courses') ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-certificate"></i> الدورات التدريبية</h2>
            <div class="section-content">${getContent('courses').replace(/\n/g, '<br>')}</div>
        </div>` : ''}
        
        ${getContent('skills') ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-star"></i> المهارات</h2>
            <div class="section-content">${getContent('skills').replace(/\n/g, '<br>')}</div>
        </div>` : ''}
        
        ${teacherData.certificates.files.length > 0 ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-award"></i> شواهد الأداء</h2>
            ${getContent('certificates') ? `<div class="section-content" style="margin-bottom: 25px;">${getContent('certificates').replace(/\n/g, '<br>')}</div>` : ''}
            <div class="files-grid">
                ${teacherData.certificates.files.map(file => `
                    <div class="file-card">
                        <div class="file-icon">
                            <i class="${getFileIcon(file.type)}"></i>
                        </div>
                        <div class="file-info">
                            <h4>${file.name}</h4>
                            <span>${file.size} • ${file.date}</span>
                        </div>
                    </div>
                `).join('')}
            </div>
        </div>` : ''}
        
        ${teacherData.portfolio.files.length > 0 ? `<div class="portfolio-section">
            <h2 class="section-title"><i class="fas fa-images"></i> معرض الأعمال</h2>
            ${getContent('portfolio') ? `<div class="section-content" style="margin-bottom: 25px;">${getContent('portfolio').replace(/\n/g, '<br>')}</div>` : ''}
            <div class="files-grid">
                ${teacherData.portfolio.files.map(file => `
                    <div class="file-card">
                        <div class="file-icon">
                            <i class="${getFileIcon(file.type)}"></i>
                        </div>
                        <div class="file-info">
                            <h4>${file.name}</h4>
                            <span>${file.size} • ${file.date}</span>
                        </div>
                    </div>
                `).join('')}
            </div>
        </div>` : ''}
        
        <div class="footer-note">
            <p>تم إنشاء هذا الملف المهني باستخدام أداة إنشاء الملف المهني للمعلمين - ${new Date().toLocaleDateString('ar-SA')}</p>
        </div>
    </div>
    
    <script>
        // إضافة زر الطباعة
        const printButton = document.createElement('button');
        printButton.innerHTML = '<i class="fas fa-print"></i> طباعة الملف';
        printButton.style.cssText = 'position: fixed; bottom: 20px; left: 20px; background: var(--primary-color); color: white; border: none; padding: 12px 25px; border-radius: 8px; font-family: inherit; font-size: 1rem; cursor: pointer; z-index: 1000; box-shadow: 0 4px 12px rgba(0,0,0,0.15);';
        printButton.addEventListener('click', function() {
            window.print();
        });
        document.body.appendChild(printButton);
    </script>
</body>
</html>`;
        }
        
        // ============== وظائف مساعدة ==============
        function capitalizeFirstLetter(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        }
        
        function getFileIcon(fileType) {
            if (fileType.includes('pdf')) return 'fas fa-file-pdf';
            if (fileType.includes('image')) return 'fas fa-file-image';
            if (fileType.includes('word') || fileType.includes('document')) return 'fas fa-file-word';
            if (fileType.includes('presentation') || fileType.includes('powerpoint')) return 'fas fa-file-powerpoint';
            if (fileType.includes('spreadsheet') || fileType.includes('excel')) return 'fas fa-file-excel';
            return 'fas fa-file';
        }
        
        function showNotification(message, type) {
            notification.textContent = message;
            notification.className = `notification ${type} show`;
            
            if (type === 'success') {
                notification.innerHTML = `<i class="fas fa-check-circle"></i> ${message}`;
            } else if (type === 'error') {
                notification.innerHTML = `<i class="fas fa-exclamation-circle"></i> ${message}`;
            }
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        function toggleLanguage() {
            currentLanguage = currentLanguage === 'ar' ? 'en' : 'ar';
            
            // في التطبيق الحقيقي، هنا سيتم تحويل جميع النصوص للغة الأخرى
            // لكن للعرض التوضيحي سنكتفي بتغيير النص على الزر
            const languageIcon = languageToggle.querySelector('i');
            if (currentLanguage === 'en') {
                languageIcon.className = 'fas fa-language';
                languageToggle.title = 'Switch to Arabic';
                showNotification('تم التبديل إلى اللغة الإنجليزية', 'success');
            } else {
                languageIcon.className = 'fas fa-language';
                languageToggle.title = 'التبديل إلى الإنجليزية';
                showNotification('تم التبديل إلى اللغة العربية', 'success');
            }
        }
        
        function toggleDarkMode() {
            isDarkMode = !isDarkMode;
            
            if (isDarkMode) {
                document.body.classList.add('dark-mode');
                themeToggle.querySelector('i').className = 'fas fa-sun';
                themeToggle.title = 'الوضع النهاري';
            } else {
                document.body.classList.remove('dark-mode');
                themeToggle.querySelector('i').className = 'fas fa-moon';
                themeToggle.title = 'الوضع الليلي';
            }
            
            localStorage.setItem('darkMode', isDarkMode);
        }
        
        function saveToLocalStorage() {
            localStorage.setItem('teacherPortfolioData', JSON.stringify(teacherData));
        }
        
        function loadSavedData() {
            const savedData = localStorage.getItem('teacherPortfolioData');
            if (savedData) {
                teacherData = JSON.parse(savedData);
                
                // تحميل اسم المعلم
                if (teacherData.name) {
                    teacherNameInput.value = teacherData.name;
                }
                
                // تحميل النصوص المخصصة
                const sections = ['about', 'vision', 'experience', 'achievements', 'courses', 'skills', 'certificates', 'portfolio'];
                sections.forEach(section => {
                    const textarea = document.getElementById(`custom${capitalizeFirstLetter(section)}Text`);
                    if (textarea && teacherData[section].custom) {
                        textarea.value = teacherData[section].custom;
                    }
                    
                    const aiBox = document.getElementById(`ai${capitalizeFirstLetter(section)}Text`);
                    if (aiBox && teacherData[section].ai) {
                        aiBox.textContent = teacherData[section].ai;
                    }
                });
                
                // تحميل بيانات التواصل
                if (teacherData.contact.phone) document.getElementById('phone').value = teacherData.contact.phone;
                if (teacherData.contact.email) document.getElementById('email').value = teacherData.contact.email;
                if (teacherData.contact.whatsapp) document.getElementById('whatsapp').value = teacherData.contact.whatsapp;
                if (teacherData.contact.twitter) document.getElementById('twitter').value = teacherData.contact.twitter;
                if (teacherData.contact.linkedin) document.getElementById('linkedin').value = teacherData.contact.linkedin;
                
                // تحميل قوائم الملفات
                updateFileList('certificates');
                updateFileList('portfolio');
                
                showNotification('تم تحميل البيانات المحفوظة بنجاح', 'success');
            }
        }
    </script>
</body>
</html>
