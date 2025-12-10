<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة الملف المهني للمعلم</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        /* CSS Reset وتحسينات عامة */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', sans-serif;
        }

        :root {
            --primary-color: #4a6fa5;
            --primary-dark: #166088;
            --secondary-color: #17a2b8;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --danger-color: #dc3545;
            --light-color: #f8f9fa;
            --dark-color: #343a40;
            --text-color: #333;
            --text-light: #666;
            --border-color: #ddd;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 10px 30px rgba(0, 0, 0, 0.2);
            --transition: all 0.3s ease;
        }

        /* الوضع الليلي */
        body.dark-mode {
            --primary-color: #2d4059;
            --primary-dark: #1a1a2e;
            --secondary-color: #138496;
            --success-color: #218838;
            --warning-color: #e0a800;
            --light-color: #1a1a2e;
            --dark-color: #162447;
            --text-color: #f1f1f1;
            --text-light: #b0b0b0;
            --border-color: #2d4059;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            --shadow-lg: 0 10px 30px rgba(0, 0, 0, 0.4);
        }

        body {
            background-color: var(--light-color);
            color: var(--text-color);
            transition: var(--transition);
            min-height: 100vh;
            direction: rtl;
        }

        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* الهيدر الرئيسي */
        .tool-header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
            color: white;
            padding: 20px 0;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo i {
            font-size: 2rem;
        }

        .logo h1 {
            font-size: 1.5rem;
            font-weight: 700;
            margin: 0;
        }

        .header-controls {
            display: flex;
            gap: 10px;
        }

        .control-btn {
            background: rgba(255, 255, 255, 0.15);
            border: none;
            color: white;
            padding: 8px 16px;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9rem;
            transition: var(--transition);
        }

        .control-btn:hover {
            background: rgba(255, 255, 255, 0.25);
            transform: translateY(-2px);
        }

        .header-bottom {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }

        .teacher-input-section {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }

        .input-group {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .input-group label {
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: 600;
            font-size: 1rem;
        }

        #teacher-name {
            background: rgba(255, 255, 255, 0.9);
            border: none;
            color: var(--text-color);
            padding: 10px 15px;
            border-radius: 8px;
            font-size: 1rem;
            min-width: 250px;
            transition: var(--transition);
        }

        #teacher-name:focus {
            outline: none;
            box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.3);
        }

        .name-display-section {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .display-label {
            font-weight: 600;
            font-size: 1rem;
        }

        .display-value {
            background: rgba(255, 255, 255, 0.15);
            padding: 8px 16px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 1.1rem;
            min-width: 150px;
            text-align: center;
        }

        /* المحتوى الرئيسي */
        .main-content {
            padding: 30px 0;
        }

        /* شريط التنقل */
        .sections-nav {
            background-color: white;
            border-radius: 12px;
            padding: 10px;
            margin-bottom: 30px;
            box-shadow: var(--shadow);
            overflow-x: auto;
            position: sticky;
            top: 90px;
            z-index: 999;
        }

        .dark-mode .sections-nav {
            background-color: var(--dark-color);
        }

        .nav-list {
            display: flex;
            list-style: none;
            gap: 5px;
            min-width: 800px;
        }

        .nav-item {
            flex: 1;
        }

        .nav-link {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--text-color);
            padding: 12px 5px;
            border-radius: 8px;
            transition: var(--transition);
            background: transparent;
            border: none;
            width: 100%;
            cursor: pointer;
        }

        .nav-link.active {
            background-color: var(--primary-color);
            color: white;
        }

        .nav-link:not(.active):hover {
            background-color: rgba(74, 111, 165, 0.1);
        }

        .dark-mode .nav-link:not(.active):hover {
            background-color: rgba(255, 255, 255, 0.1);
        }

        .nav-link i {
            font-size: 1.3rem;
            margin-bottom: 8px;
        }

        .nav-text {
            font-size: 0.85rem;
            font-weight: 500;
            text-align: center;
            line-height: 1.2;
        }

        /* منطقة المحتوى */
        .content-area {
            background-color: white;
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: var(--shadow);
        }

        .dark-mode .content-area {
            background-color: var(--dark-color);
        }

        .content-section {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .content-section.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--border-color);
        }

        .section-title {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--primary-dark);
            font-size: 1.5rem;
            margin: 0;
        }

        .dark-mode .section-title {
            color: #64b5f6;
        }

        .generate-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9rem;
            transition: var(--transition);
        }

        .generate-btn:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .section-body {
            margin-top: 15px;
        }

        .section-textarea {
            width: 100%;
            min-height: 200px;
            padding: 15px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 1rem;
            line-height: 1.6;
            resize: vertical;
            transition: var(--transition);
            background-color: var(--light-color);
            color: var(--text-color);
        }

        .section-textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(74, 111, 165, 0.1);
        }

        .dark-mode .section-textarea:focus {
            border-color: #64b5f6;
            box-shadow: 0 0 0 3px rgba(100, 181, 246, 0.2);
        }

        /* أزرار التحكم */
        .action-controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }

        .action-btn {
            padding: 12px 25px;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: var(--transition);
            min-width: 180px;
            justify-content: center;
        }

        .preview-btn {
            background-color: var(--secondary-color);
            color: white;
        }

        .preview-btn:hover {
            background-color: #138496;
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(23, 162, 184, 0.2);
        }

        .export-html-btn {
            background-color: var(--success-color);
            color: white;
        }

        .export-html-btn:hover {
            background-color: #218838;
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(40, 167, 69, 0.2);
        }

        .export-excel-btn {
            background-color: var(--warning-color);
            color: #212529;
        }

        .export-excel-btn:hover {
            background-color: #e0a800;
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(255, 193, 7, 0.2);
        }

        /* نافذة المعاينة */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1100;
            overflow: auto;
            animation: fadeInModal 0.3s ease;
        }

        @keyframes fadeInModal {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-container {
            background-color: white;
            margin: 30px auto;
            width: 90%;
            max-width: 1000px;
            border-radius: 12px;
            box-shadow: var(--shadow-lg);
            animation: slideInModal 0.4s ease;
        }

        .dark-mode .modal-container {
            background-color: var(--dark-color);
        }

        @keyframes slideInModal {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            border-bottom: 1px solid var(--border-color);
        }

        .modal-title {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--primary-dark);
            margin: 0;
        }

        .dark-mode .modal-title {
            color: #64b5f6;
        }

        .modal-close-btn {
            background: none;
            border: none;
            font-size: 1.5rem;
            color: var(--text-light);
            cursor: pointer;
            transition: var(--transition);
            padding: 5px;
            border-radius: 5px;
        }

        .modal-close-btn:hover {
            color: var(--text-color);
            background-color: rgba(0, 0, 0, 0.05);
        }

        .modal-body {
            padding: 20px;
            max-height: 70vh;
            overflow-y: auto;
        }

        .modal-footer {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            padding: 20px;
            border-top: 1px solid var(--border-color);
        }

        .modal-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: var(--transition);
        }

        .secondary-btn {
            background-color: #6c757d;
            color: white;
        }

        .secondary-btn:hover {
            background-color: #5a6268;
        }

        .primary-btn {
            background-color: var(--success-color);
            color: white;
        }

        .primary-btn:hover {
            background-color: #218838;
        }

        /* محتوى المعاينة */
        .preview-content {
            font-family: 'Tajawal', sans-serif;
            line-height: 1.6;
        }

        .preview-document {
            background: white;
            color: #333;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.05);
        }

        .dark-mode .preview-document {
            background: var(--dark-color);
            color: var(--text-color);
        }

        .preview-header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px solid var(--primary-color);
        }

        .preview-header h1 {
            color: var(--primary-dark);
            font-size: 2.2rem;
            margin-bottom: 10px;
        }

        .dark-mode .preview-header h1 {
            color: #64b5f6;
        }

        .preview-section {
            margin-bottom: 25px;
            page-break-inside: avoid;
        }

        .preview-section h2 {
            color: var(--primary-dark);
            font-size: 1.5rem;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--border-color);
        }

        .dark-mode .preview-section h2 {
            color: #64b5f6;
        }

        .preview-text {
            white-space: pre-line;
            font-size: 1.1rem;
        }

        /* الإشعارات */
        .notification {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background-color: var(--success-color);
            color: white;
            padding: 15px 20px;
            border-radius: 8px;
            box-shadow: var(--shadow);
            display: none;
            align-items: center;
            gap: 10px;
            z-index: 1200;
            animation: slideInNotification 0.3s ease;
        }

        @keyframes slideInNotification {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .notification-content {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .notification-content i {
            font-size: 1.5rem;
        }

        /* التجاوبية */
        @media (max-width: 992px) {
            .header-top {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .header-controls {
                width: 100%;
                justify-content: flex-start;
            }
            
            .teacher-input-section {
                flex-direction: column;
                align-items: flex-start;
            }
            
            #teacher-name {
                min-width: 100%;
            }
            
            .nav-list {
                gap: 3px;
            }
            
            .nav-link {
                padding: 8px 3px;
            }
            
            .nav-text {
                font-size: 0.8rem;
            }
            
            .action-controls {
                flex-direction: column;
                align-items: center;
            }
            
            .action-btn {
                width: 100%;
                max-width: 300px;
            }
        }

        @media (max-width: 768px) {
            .container {
                padding: 0 15px;
            }
            
            .main-content {
                padding: 20px 0;
            }
            
            .section-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            
            .generate-btn {
                align-self: stretch;
            }
            
            .modal-container {
                width: 95%;
                margin: 15px auto;
            }
        }

        @media (max-width: 576px) {
            .tool-header {
                padding: 15px 0;
            }
            
            .logo h1 {
                font-size: 1.3rem;
            }
            
            .control-btn {
                padding: 6px 12px;
                font-size: 0.85rem;
            }
            
            .display-label,
            .input-group label {
                font-size: 0.9rem;
            }
            
            .display-value {
                font-size: 1rem;
                min-width: 120px;
            }
            
            .content-area {
                padding: 15px;
            }
            
            .section-title {
                font-size: 1.3rem;
            }
            
            .modal-header,
            .modal-body,
            .modal-footer {
                padding: 15px;
            }
            
            .notification {
                right: 15px;
                bottom: 15px;
                left: 15px;
                text-align: center;
            }
        }

        @media print {
            .tool-header,
            .sections-nav,
            .action-controls,
            .modal-overlay,
            .notification {
                display: none !important;
            }
            
            .main-content {
                padding: 0;
            }
            
            .content-area {
                box-shadow: none;
                padding: 0;
            }
            
            .preview-document {
                box-shadow: none;
                padding: 0;
            }
        }
    </style>
</head>
<body class="light-mode">
    <!-- الهيدر الرئيسي -->
    <header class="tool-header">
        <div class="container">
            <div class="header-top">
                <div class="logo">
                    <i class="fas fa-chalkboard-teacher"></i>
                    <h1 id="tool-title">أداة الملف المهني للمعلم</h1>
                </div>
                
                <div class="header-controls">
                    <div class="theme-toggle-wrapper">
                        <button id="theme-toggle" class="control-btn" title="تبديل الوضع الليلي">
                            <i class="fas fa-moon"></i>
                            <span class="btn-text">الوضع الليلي</span>
                        </button>
                    </div>
                    
                    <div class="language-toggle-wrapper">
                        <button id="language-toggle" class="control-btn" title="تبديل اللغة">
                            <i class="fas fa-language"></i>
                            <span class="btn-text">English</span>
                        </button>
                    </div>
                </div>
            </div>
            
            <div class="header-bottom">
                <div class="teacher-input-section">
                    <div class="input-group">
                        <label for="teacher-name">
                            <i class="fas fa-user"></i>
                            اسم المعلم:
                        </label>
                        <input type="text" id="teacher-name" placeholder="أدخل اسم المعلم هنا">
                    </div>
                    <div class="name-display-section">
                        <span class="display-label">الاسم المعروض:</span>
                        <span id="name-display" class="display-value">المعلم الفاضل</span>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- المحتوى الرئيسي -->
    <main class="main-content">
        <div class="container">
            <!-- شريط التنقل بين الأقسام -->
            <nav class="sections-nav" id="sections-nav">
                <ul class="nav-list">
                    <li class="nav-item">
                        <a href="#about-me" class="nav-link active" data-section="about-me">
                            <i class="fas fa-user-circle"></i>
                            <span class="nav-text">نبذة عني</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#vision" class="nav-link" data-section="vision">
                            <i class="fas fa-eye"></i>
                            <span class="nav-text">الرؤية التعليمية</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#experiences" class="nav-link" data-section="experiences">
                            <i class="fas fa-briefcase"></i>
                            <span class="nav-text">الخبرات</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#achievements" class="nav-link" data-section="achievements">
                            <i class="fas fa-trophy"></i>
                            <span class="nav-text">الإنجازات</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#courses" class="nav-link" data-section="courses">
                            <i class="fas fa-graduation-cap"></i>
                            <span class="nav-text">الدورات التدريبية</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#skills" class="nav-link" data-section="skills">
                            <i class="fas fa-tools"></i>
                            <span class="nav-text">المهارات</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#performance" class="nav-link" data-section="performance">
                            <i class="fas fa-chart-line"></i>
                            <span class="nav-text">شواهد الأداء</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#portfolio" class="nav-link" data-section="portfolio">
                            <i class="fas fa-images"></i>
                            <span class="nav-text">معرض الأعمال</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#contact" class="nav-link" data-section="contact">
                            <i class="fas fa-address-card"></i>
                            <span class="nav-text">بيانات التواصل</span>
                        </a>
                    </li>
                </ul>
            </nav>
            
            <!-- منطقة المحتوى الرئيسية -->
            <div class="content-area">
                <!-- قسم نبذة عني -->
                <section id="about-me" class="content-section active">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-user-circle"></i>
                            نبذة عني
                        </h2>
                        <button class="generate-btn" data-section="about-me">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="about-me" placeholder="أدخل نبذة مختصرة عنك، خبراتك التعليمية، تخصصك، وأهدافك المهنية...">معلم متخصص في مجال التعليم الابتدائي مع خبرة تزيد عن 10 سنوات في التدريس. حاصل على درجة الماجستير في التربية الخاصة وأعمل حاليًا كمشرف تربوي. أؤمن بأهمية تطوير أساليب التعليم لتنمية مهارات الطلاب الإبداعية والنقدية.</textarea>
                    </div>
                </section>
                
                <!-- قسم الرؤية التعليمية -->
                <section id="vision" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-eye"></i>
                            الرؤية التعليمية
                        </h2>
                        <button class="generate-btn" data-section="vision">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="vision" placeholder="أدخل رؤيتك التعليمية وفلسفتك في التدريس...">أسعى إلى تقديم تعليم متميز يواكب متطلبات العصر، ويساهم في بناء جيل قادر على التفكير النقدي والإبداعي. أعمل على تطوير بيئة تعليمية محفزة تشجع الطلاب على الاستكشاف والتعلّم الذاتي.</textarea>
                    </div>
                </section>
                
                <!-- قسم الخبرات -->
                <section id="experiences" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-briefcase"></i>
                            الخبرات
                        </h2>
                        <button class="generate-btn" data-section="experiences">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="experiences" placeholder="أدخل خبراتك المهنية والعملية...">- معلم لغة عربية للمرحلة الابتدائية (2015-2020)
- مشرف تربوي لمادة اللغة العربية (2020-2023)
- منسق برامج الموهوبين في المدرسة (2018-2023)
- عضو في لجنة تطوير المناهج المحلية (2021-2023)</textarea>
                    </div>
                </section>
                
                <!-- قسم الإنجازات -->
                <section id="achievements" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-trophy"></i>
                            الإنجازات
                        </h2>
                        <button class="generate-btn" data-section="achievements">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="achievements" placeholder="أدخل إنجازاتك المهنية والشخصية...">- الحصول على جائزة المعلم المتميز على مستوى المنطقة (2022)
- رفع نسبة نجاح الطلاب في مادة اللغة العربية بنسبة 30%
- تنظيم معرض للإبداعات الطلابية حصل على تغطية إعلامية محلية
- تصميم برنامج تقييم مبتكر تم تطبيقه على مستوى المدارس في المنطقة</textarea>
                    </div>
                </section>
                
                <!-- قسم الدورات التدريبية -->
                <section id="courses" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-graduation-cap"></i>
                            الدورات التدريبية
                        </h2>
                        <button class="generate-btn" data-section="courses">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="courses" placeholder="أدخل الدورات التدريبية التي حضرتها...">- دورة "التدريس التفاعلي" - مركز التدريب التربوي (2021)
- دورة "استراتيجيات التعلم النشط" - جامعة الملك سعود (2020)
- دورة "التقويم البديل" - وزارة التعليم (2022)
- دورة "تقنيات التعليم عن بعد" - أكاديمية التدريب الإلكتروني (2023)</textarea>
                    </div>
                </section>
                
                <!-- قسم المهارات -->
                <section id="skills" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-tools"></i>
                            المهارات
                        </h2>
                        <button class="generate-btn" data-section="skills">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="skills" placeholder="أدخل مهاراتك الشخصية والمهنية...">- إتقان استخدام تقنيات التعليم الحديثة
- مهارات التواصل الفعال مع الطلاب وأولياء الأمور
- القدرة على تصميم الأنشطة التعليمية التفاعلية
- مهارة تحليل النتائج والتقويم المستمر
- إتقان استخدام برامج Microsoft Office والتعليم الإلكتروني</textarea>
                    </div>
                </section>
                
                <!-- قسم شواهد الأداء -->
                <section id="performance" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-chart-line"></i>
                            شواهد الأداء
                        </h2>
                        <button class="generate-btn" data-section="performance">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="performance" placeholder="أدخل شواهد أدائك وتقارير التقييم...">- تقييم "متميز" في الأداء الوظيفي لثلاث سنوات متتالية
- شهادات شكر من إدارة التعليم للمبادرات الناجحة
- تقارير تقييم إيجابية من المشرفين التربويين
- نتائج رضا أولياء الأمور بنسبة 95% حسب استبيان المدرسة</textarea>
                    </div>
                </section>
                
                <!-- قسم معرض الأعمال -->
                <section id="portfolio" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-images"></i>
                            معرض الأعمال
                        </h2>
                        <button class="generate-btn" data-section="portfolio">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="portfolio" placeholder="أدخل أعمالك ومنجزاتك البارزة...">- تصميم وحدة تعليمية تفاعلية في النحو العربي
- إنتاج سلسلة فيديوهات تعليمية للطلاب ضعاف التحصيل
- تأليف كتيب "نشاطات لغوية" للمرحلة الابتدائية
- تصميم بوابة إلكترونية للأنشطة الصفية</textarea>
                    </div>
                </section>
                
                <!-- قسم بيانات التواصل -->
                <section id="contact" class="content-section">
                    <div class="section-header">
                        <h2 class="section-title">
                            <i class="fas fa-address-card"></i>
                            بيانات التواصل
                        </h2>
                        <button class="generate-btn" data-section="contact">
                            <i class="fas fa-robot"></i>
                            <span class="btn-text">إنشاء نص تلقائي</span>
                        </button>
                    </div>
                    <div class="section-body">
                        <textarea class="section-textarea" data-section="contact" placeholder="أدخل بيانات التواصل الخاصة بك...">البريد الإلكتروني: teacher@example.com
الهاتف: 0550123456
العنوان: الرياض، المملكة العربية السعودية
حساب LinkedIn: linkedin.com/in/teacher-name
حساب Twitter: @teacher_name</textarea>
                    </div>
                </section>
            </div>
            
            <!-- أزرار التحكم الرئيسية -->
            <div class="action-controls">
                <button id="preview-btn" class="action-btn preview-btn">
                    <i class="fas fa-eye"></i>
                    <span class="btn-text">معاينة الملف</span>
                </button>
                <button id="export-html-btn" class="action-btn export-html-btn">
                    <i class="fas fa-file-code"></i>
                    <span class="btn-text">تصدير HTML</span>
                </button>
                <button id="export-excel-btn" class="action-btn export-excel-btn">
                    <i class="fas fa-file-excel"></i>
                    <span class="btn-text">تصدير Excel</span>
                </button>
            </div>
        </div>
    </main>

    <!-- نافذة المعاينة -->
    <div id="preview-modal" class="modal-overlay">
        <div class="modal-container">
            <div class="modal-header">
                <h2 class="modal-title">
                    <i class="fas fa-file-alt"></i>
                    معاينة الملف المهني
                </h2>
                <button class="modal-close-btn" id="modal-close-btn">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="modal-body">
                <div id="preview-content" class="preview-content"></div>
            </div>
            <div class="modal-footer">
                <button id="close-preview-btn" class="modal-btn secondary-btn">
                    <i class="fas fa-times"></i>
                    <span>إغلاق</span>
                </button>
                <button id="download-preview-btn" class="modal-btn primary-btn">
                    <i class="fas fa-download"></i>
                    <span>تحميل HTML</span>
                </button>
            </div>
        </div>
    </div>

    <!-- إشعار النجاح -->
    <div id="success-notification" class="notification">
        <div class="notification-content">
            <i class="fas fa-check-circle"></i>
            <span id="notification-message">تم العملية بنجاح!</span>
        </div>
    </div>

    <script>
        // تطبيق أداة الملف المهني للمعلم
        document.addEventListener('DOMContentLoaded', function() {
            // الحالة الأساسية للتطبيق
            const appState = {
                teacherName: 'المعلم الفاضل',
                currentLanguage: 'ar',
                currentTheme: 'light-mode',
                sections: {
                    'about-me': '',
                    'vision': '',
                    'experiences': '',
                    'achievements': '',
                    'courses': '',
                    'skills': '',
                    'performance': '',
                    'portfolio': '',
                    'contact': ''
                },
                sectionNames: {
                    'ar': {
                        'about-me': 'نبذة عني',
                        'vision': 'الرؤية التعليمية',
                        'experiences': 'الخبرات',
                        'achievements': 'الإنجازات',
                        'courses': 'الدورات التدريبية',
                        'skills': 'المهارات',
                        'performance': 'شواهد الأداء',
                        'portfolio': 'معرض الأعمال',
                        'contact': 'بيانات التواصل'
                    },
                    'en': {
                        'about-me': 'About Me',
                        'vision': 'Educational Vision',
                        'experiences': 'Experiences',
                        'achievements': 'Achievements',
                        'courses': 'Training Courses',
                        'skills': 'Skills',
                        'performance': 'Performance Evidence',
                        'portfolio': 'Portfolio',
                        'contact': 'Contact Information'
                    }
                },
                uiTexts: {
                    'ar': {
                        'toolTitle': 'أداة الملف المهني للمعلم',
                        'teacherNamePlaceholder': 'أدخل اسم المعلم هنا',
                        'nameDisplayLabel': 'الاسم المعروض:',
                        'themeToggle': 'الوضع الليلي',
                        'languageToggle': 'English',
                        'generateText': 'إنشاء نص تلقائي',
                        'preview': 'معاينة الملف',
                        'exportHTML': 'تصدير HTML',
                        'exportExcel': 'تصدير Excel',
                        'previewTitle': 'معاينة الملف المهني',
                        'close': 'إغلاق',
                        'downloadHTML': 'تحميل HTML',
                        'notificationMessages': {
                            'htmlExported': 'تم تصدير ملف HTML بنجاح',
                            'excelExported': 'تم تصدير ملف Excel بنجاح',
                            'autoGenerated': 'تم إنشاء النص التلقائي بنجاح',
                            'dataSaved': 'تم حفظ البيانات'
                        }
                    },
                    'en': {
                        'toolTitle': 'Teacher Professional Portfolio Tool',
                        'teacherNamePlaceholder': 'Enter teacher name here',
                        'nameDisplayLabel': 'Display Name:',
                        'themeToggle': 'Dark Mode',
                        'languageToggle': 'العربية',
                        'generateText': 'Generate Auto Text',
                        'preview': 'Preview File',
                        'exportHTML': 'Export HTML',
                        'exportExcel': 'Export Excel',
                        'previewTitle': 'Professional File Preview',
                        'close': 'Close',
                        'downloadHTML': 'Download HTML',
                        'notificationMessages': {
                            'htmlExported': 'HTML file exported successfully',
                            'excelExported': 'Excel file exported successfully',
                            'autoGenerated': 'Auto text generated successfully',
                            'dataSaved': 'Data saved successfully'
                        }
                    }
                }
            };

            // عناصر DOM الرئيسية
            const DOM = {
                body: document.body,
                teacherNameInput: document.getElementById('teacher-name'),
                nameDisplay: document.getElementById('name-display'),
                themeToggle: document.getElementById('theme-toggle'),
                languageToggle: document.getElementById('language-toggle'),
                navLinks: document.querySelectorAll('.nav-link'),
                contentSections: document.querySelectorAll('.content-section'),
                generateButtons: document.querySelectorAll('.generate-btn'),
                textareas: document.querySelectorAll('.section-textarea'),
                previewBtn: document.getElementById('preview-btn'),
                exportHtmlBtn: document.getElementById('export-html-btn'),
                exportExcelBtn: document.getElementById('export-excel-btn'),
                previewModal: document.getElementById('preview-modal'),
                modalCloseBtn: document.getElementById('modal-close-btn'),
                closePreviewBtn: document.getElementById('close-preview-btn'),
                downloadPreviewBtn: document.getElementById('download-preview-btn'),
                previewContent: document.getElementById('preview-content'),
                successNotification: document.getElementById('success-notification'),
                notificationMessage: document.getElementById('notification-message')
            };

            // تهيئة التطبيق
            function initApp() {
                loadSavedData();
                setupEventListeners();
                updateUILanguage();
                
                // إضافة محتوى أولي للنصوص
                initializeTextareas();
            }

            // إعداد مستمعي الأحداث
            function setupEventListeners() {
                // اسم المعلم
                DOM.teacherNameInput.addEventListener('input', handleTeacherNameChange);
                
                // تبديل الوضع الليلي/النهاري
                DOM.themeToggle.addEventListener('click', toggleTheme);
                
                // تبديل اللغة
                DOM.languageToggle.addEventListener('click', toggleLanguage);
                
                // التنقل بين الأقسام
                DOM.navLinks.forEach(link => {
                    link.addEventListener('click', handleNavClick);
                });
                
                // إنشاء نص تلقائي
                DOM.generateButtons.forEach(btn => {
                    btn.addEventListener('click', handleAutoGenerate);
                });
                
                // تحديث النصوص
                DOM.textareas.forEach(textarea => {
                    textarea.addEventListener('input', handleTextareaChange);
                });
                
                // أزرار التحكم الرئيسية
                DOM.previewBtn.addEventListener('click', showPreview);
                DOM.exportHtmlBtn.addEventListener('click', exportToHTML);
                DOM.exportExcelBtn.addEventListener('click', exportToExcel);
                
                // إغلاق نافذة المعاينة
                DOM.modalCloseBtn.addEventListener('click', closePreviewModal);
                DOM.closePreviewBtn.addEventListener('click', closePreviewModal);
                DOM.downloadPreviewBtn.addEventListener('click', () => {
                    exportToHTML();
                    closePreviewModal();
                });
                
                // إغلاق النافذة عند النقر خارجها
                DOM.previewModal.addEventListener('click', (e) => {
                    if (e.target === DOM.previewModal) {
                        closePreviewModal();
                    }
                });
                
                // إغلاق الإشعار تلقائيًا
                DOM.successNotification.addEventListener('click', () => {
                    DOM.successNotification.style.display = 'none';
                });
            }

            // معالجة تغيير اسم المعلم
            function handleTeacherNameChange() {
                const name = DOM.teacherNameInput.value.trim();
                appState.teacherName = name || (appState.currentLanguage === 'ar' ? 'المعلم الفاضل' : 'Respected Teacher');
                DOM.nameDisplay.textContent = appState.teacherName;
                saveData();
                showNotification(appState.uiTexts[appState.currentLanguage].notificationMessages.dataSaved);
            }

            // تبديل الوضع الليلي/النهاري
            function toggleTheme() {
                if (DOM.body.classList.contains('dark-mode')) {
                    DOM.body.classList.remove('dark-mode');
                    DOM.body.classList.add('light-mode');
                    appState.currentTheme = 'light-mode';
                    updateThemeButton(false);
                } else {
                    DOM.body.classList.remove('light-mode');
                    DOM.body.classList.add('dark-mode');
                    appState.currentTheme = 'dark-mode';
                    updateThemeButton(true);
                }
                saveData();
            }

            // تحديث زر الوضع الليلي/النهاري
            function updateThemeButton(isDarkMode) {
                const themeText = appState.uiTexts[appState.currentLanguage].themeToggle;
                DOM.themeToggle.innerHTML = isDarkMode 
                    ? `<i class="fas fa-sun"></i><span class="btn-text">${themeText}</span>`
                    : `<i class="fas fa-moon"></i><span class="btn-text">${themeText}</span>`;
            }

            // تبديل اللغة
            function toggleLanguage() {
                appState.currentLanguage = appState.currentLanguage === 'ar' ? 'en' : 'ar';
                
                // تغيير اتجاه النص
                document.documentElement.dir = appState.currentLanguage === 'ar' ? 'rtl' : 'ltr';
                document.documentElement.lang = appState.currentLanguage;
                
                // تحديث واجهة المستخدم
                updateUILanguage();
                
                // تحديث زر اللغة
                updateLanguageButton();
                
                saveData();
            }

            // تحديث زر اللغة
            function updateLanguageButton() {
                const langText = appState.uiTexts[appState.currentLanguage].languageToggle;
                DOM.languageToggle.innerHTML = `<i class="fas fa-language"></i><span class="btn-text">${langText}</span>`;
            }

            // تحديث واجهة المستخدم حسب اللغة
            function updateUILanguage() {
                const texts = appState.uiTexts[appState.currentLanguage];
                
                // تحديث النصوص
                document.getElementById('tool-title').textContent = texts.toolTitle;
                DOM.teacherNameInput.placeholder = texts.teacherNamePlaceholder;
                
                // تحديث تسمية عرض الاسم
                document.querySelector('.display-label').textContent = texts.nameDisplayLabel;
                
                // تحديث أزرار التحكم
                updateThemeButton(DOM.body.classList.contains('dark-mode'));
                updateLanguageButton();
                
                // تحديث أزرار التنقل
                document.querySelectorAll('.nav-text').forEach((span, index) => {
                    const sectionId = Object.keys(appState.sectionNames[appState.currentLanguage])[index];
                    span.textContent = appState.sectionNames[appState.currentLanguage][sectionId];
                });
                
                // تحديث عناوين الأقسام
                document.querySelectorAll('.section-title').forEach((title, index) => {
                    const sectionId = Object.keys(appState.sectionNames[appState.currentLanguage])[index];
                    const icon = title.querySelector('i').outerHTML;
                    title.innerHTML = icon + appState.sectionNames[appState.currentLanguage][sectionId];
                });
                
                // تحديث أزرار إنشاء النص التلقائي
                document.querySelectorAll('.generate-btn .btn-text').forEach(span => {
                    span.textContent = texts.generateText;
                });
                
                // تحديث أزرار الإجراءات
                const actionBtns = document.querySelectorAll('.action-btn .btn-text');
                if (actionBtns.length >= 3) {
                    actionBtns[0].textContent = texts.preview;
                    actionBtns[1].textContent = texts.exportHTML;
                    actionBtns[2].textContent = texts.exportExcel;
                }
                
                // تحديث نافذة المعاينة
                document.querySelector('.modal-title').innerHTML = 
                    `<i class="fas fa-file-alt"></i>${texts.previewTitle}`;
                
                const closeBtn = document.querySelector('#close-preview-btn span');
                const downloadBtn = document.querySelector('#download-preview-btn span');
                
                if (closeBtn) closeBtn.textContent = texts.close;
                if (downloadBtn) downloadBtn.textContent = texts.downloadHTML;
            }

            // معالجة النقر على رابط التنقل
            function handleNavClick(e) {
                e.preventDefault();
                const sectionId = this.getAttribute('data-section');
                switchToSection(sectionId);
            }

            // التبديل إلى قسم معين
            function switchToSection(sectionId) {
                // إخفاء جميع الأقسام
                DOM.contentSections.forEach(section => {
                    section.classList.remove('active');
                });
                
                // إزالة النشاط من جميع روابط التنقل
                DOM.navLinks.forEach(link => {
                    link.classList.remove('active');
                });
                
                // إظهار القسم المحدد
                const targetSection = document.getElementById(sectionId);
                if (targetSection) {
                    targetSection.classList.add('active');
                }
                
                // تفعيل رابط التنقل المحدد
                const targetLink = document.querySelector(`.nav-link[data-section="${sectionId}"]`);
                if (targetLink) {
                    targetLink.classList.add('active');
                }
            }

            // معالجة إنشاء النص التلقائي
            function handleAutoGenerate() {
                const sectionId = this.getAttribute('data-section');
                generateAutoText(sectionId);
            }

            // إنشاء نص تلقائي
            function generateAutoText(sectionId) {
                const teacherName = appState.teacherName;
                const sectionName = appState.sectionNames[appState.currentLanguage][sectionId];
                let generatedText = '';
                
                // نصوص عربية
                const arabicTexts = {
                    'about-me': `أنا ${teacherName}، معلم متخصص في مجال التعليم مع خبرة تزيد عن 8 سنوات في التدريس. حاصل على درجة الماجستير في التربية وأعمل حاليًا كمشرف تربوي. أؤمن بأهمية تطوير أساليب التعليم لتنمية مهارات الطلاب الإبداعية والنقدية.`,
                    'vision': `رؤيتي التعليمية تتمثل في تقديم تعليم متميز يواكب متطلبات العصر، ويساهم في بناء جيل قادر على التفكير النقدي والإبداعي. أسعى إلى تطوير بيئة تعليمية محفزة تشجع الطلاب على الاستكشاف والتعلّم الذاتي.`,
                    'experiences': `- معلم مادة اللغة العربية للمرحلة المتوسطة (2017-2022)
- مشرف تربوي (2022-2024)
- منسق برامج الموهوبين في المدرسة (2020-2023)
- عضو في لجنة تطوير المناهج (2021-2023)`,
                    'achievements': `- الحصول على جائزة المعلم المتميز على مستوى المنطقة (2023)
- رفع نسبة نجاح الطلاب في المادة بنسبة 25%
- تنظيم معرض للإبداعات الطلابية حصل على تغطية إعلامية
- تصميم برنامج تقييم مبتكر تم تطبيقه على مستوى المنطقة`,
                    'courses': `- دورة "التدريس التفاعلي" - مركز التدريب التربوي (2022)
- دورة "استراتيجيات التعلم النشط" - جامعة الملك سعود (2021)
- دورة "التقويم البديل" - وزارة التعليم (2023)
- دورة "تقنيات التعليم عن بعد" - أكاديمية التدريب الإلكتروني (2023)`,
                    'skills': `- إتقان استخدام تقنيات التعليم الحديثة
- مهارات التواصل الفعال مع الطلاب وأولياء الأمور
- القدرة على تصميم الأنشطة التعليمية التفاعلية
- مهارة تحليل النتائج والتقويم المستمر
- إتقان استخدام برامج Microsoft Office والتعليم الإلكتروني`,
                    'performance': `- تقييم "متميز" في الأداء الوظيفي لثلاث سنوات متتالية
- شهادات شكر من إدارة التعليم للمبادرات الناجحة
- تقارير تقييم إيجابية من المشرفين التربويين
- نتائج رضا أولياء الأمور بنسبة 94% حسب استبيان المدرسة`,
                    'portfolio': `- تصميم وحدة تعليمية تفاعلية في النحو العربي
- إنتاج سلسلة فيديوهات تعليمية للطلاب ضعاف التحصيل
- تأليف كتيب "نشاطات لغوية" للمرحلة المتوسطة
- تصميم بوابة إلكترونية للأنشطة الصفية`,
                    'contact': `البريد الإلكتروني: teacher@example.com
الهاتف: 0550123456
العنوان: الرياض، المملكة العربية السعودية
LinkedIn: linkedin.com/in/teacher-name
Twitter: @teacher_name`
                };
                
                // نصوص إنجليزية
                const englishTexts = {
                    'about-me': `I am ${teacherName}, a teacher specialized in education with over 8 years of teaching experience. I hold a Master's degree in Education and currently work as an educational supervisor. I believe in the importance of developing teaching methods to cultivate students' creative and critical skills.`,
                    'vision': `My educational vision is to provide distinguished education that meets the requirements of the era and contributes to building a generation capable of critical and creative thinking. I seek to develop a stimulating educational environment that encourages students to explore and self-learn.`,
                    'experiences': `- Arabic language teacher for middle school (2017-2022)
- Educational supervisor (2022-2024)
- Coordinator of gifted student programs at school (2020-2023)
- Member of the curriculum development committee (2021-2023)`,
                    'achievements': `- Receiving the Distinguished Teacher Award at the regional level (2023)
- Increasing student success rates in the subject by 25%
- Organizing a student creativity exhibition that received media coverage
- Designing an innovative assessment program implemented at the regional level`,
                    'courses': `- "Interactive Teaching" course - Educational Training Center (2022)
- "Active Learning Strategies" course - King Saud University (2021)
- "Alternative Assessment" course - Ministry of Education (2023)
- "Distance Education Technologies" course - E-Learning Training Academy (2023)`,
                    'skills': `- Proficiency in using modern teaching technologies
- Effective communication skills with students and parents
- Ability to design interactive educational activities
- Skill in analyzing results and continuous assessment
- Proficiency in using Microsoft Office programs and e-learning`,
                    'performance': `- "Distinguished" evaluation in job performance for three consecutive years
- Certificates of thanks from the education administration for successful initiatives
- Positive evaluation reports from educational supervisors
- Parent satisfaction results of 94% according to the school survey`,
                    'portfolio': `- Designing an interactive educational unit in Arabic Grammar
- Producing a series of educational videos for low-achieving students
- Authoring a booklet "Language Activities" for middle school
- Designing an electronic portal for classroom activities`,
                    'contact': `Email: teacher@example.com
Phone: 0550123456
Address: Riyadh, Saudi Arabia
LinkedIn: linkedin.com/in/teacher-name
Twitter: @teacher_name`
                };
                
                generatedText = appState.currentLanguage === 'ar' ? arabicTexts[sectionId] : englishTexts[sectionId];
                
                // تحديث النص في الحقل
                const textarea = document.querySelector(`textarea[data-section="${sectionId}"]`);
                if (textarea) {
                    textarea.value = generatedText;
                }
                
                // تحديث الحالة
                appState.sections[sectionId] = generatedText;
                
                // حفظ البيانات
                saveData();
                
                // إظهار إشعار النجاح
                showNotification(appState.uiTexts[appState.currentLanguage].notificationMessages.autoGenerated);
            }

            // معالجة تغيير النص في الحقول
            function handleTextareaChange() {
                const sectionId = this.getAttribute('data-section');
                appState.sections[sectionId] = this.value;
                saveData();
            }

            // تهيئة النصوص في الحقول
            function initializeTextareas() {
                DOM.textareas.forEach(textarea => {
                    const sectionId = textarea.getAttribute('data-section');
                    if (textarea.value && !appState.sections[sectionId]) {
                        appState.sections[sectionId] = textarea.value;
                    }
                });
                saveData();
            }

            // عرض معاينة الملف
            function showPreview() {
                const previewHTML = createProfessionalPreview();
                DOM.previewContent.innerHTML = previewHTML;
                DOM.previewModal.style.display = 'block';
                document.body.style.overflow = 'hidden';
            }

            // إنشاء معاينة احترافية
            function createProfessionalPreview() {
                const isDarkMode = DOM.body.classList.contains('dark-mode');
                const direction = appState.currentLanguage === 'ar' ? 'rtl' : 'ltr';
                
                return `
                    <div class="preview-document" dir="${direction}">
                        <div class="preview-header">
                            <h1>${appState.teacherName}</h1>
                            <p>${appState.currentLanguage === 'ar' ? 'الملف المهني للمعلم' : 'Teacher Professional Portfolio'}</p>
                            <p>${new Date().toLocaleDateString(appState.currentLanguage === 'ar' ? 'ar-SA' : 'en-US', { 
                                year: 'numeric', 
                                month: 'long', 
                                day: 'numeric' 
                            })}</p>
                        </div>
                        
                        ${Object.keys(appState.sections).map(sectionId => `
                            <div class="preview-section">
                                <h2>${appState.sectionNames[appState.currentLanguage][sectionId]}</h2>
                                <div class="preview-text">${appState.sections[sectionId] || (appState.currentLanguage === 'ar' ? 'لا توجد بيانات' : 'No data available')}</div>
                            </div>
                        `).join('')}
                        
                        <div class="preview-section">
                            <h2>${appState.currentLanguage === 'ar' ? 'تم الإنشاء بواسطة' : 'Generated by'}</h2>
                            <div class="preview-text">
                                ${appState.currentLanguage === 'ar' 
                                    ? 'أداة الملف المهني للمعلم - جميع الحقوق محفوظة' 
                                    : 'Teacher Professional Portfolio Tool - All rights reserved'}
                            </div>
                        </div>
                    </div>
                `;
            }

            // إغلاق نافذة المعاينة
            function closePreviewModal() {
                DOM.previewModal.style.display = 'none';
                document.body.style.overflow = 'auto';
            }

            // تصدير إلى HTML
            function exportToHTML() {
                const teacherName = appState.teacherName.replace(/\s+/g, '_');
                const timestamp = new Date().toISOString().slice(0, 10).replace(/-/g, '');
                const filename = `Teacher_Portfolio_${teacherName}_${timestamp}.html`;
                
                const fullHTML = generateProfessionalHTML();
                
                // إنشاء ملف وتنزيله
                const blob = new Blob([fullHTML], { type: 'text/html;charset=utf-8' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = filename;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                // إظهار إشعار النجاح
                showNotification(appState.uiTexts[appState.currentLanguage].notificationMessages.htmlExported);
            }

            // إنشاء ملف HTML احترافي
            function generateProfessionalHTML() {
                const direction = appState.currentLanguage === 'ar' ? 'rtl' : 'ltr';
                const lang = appState.currentLanguage === 'ar' ? 'ar' : 'en';
                
                return `<!DOCTYPE html>
        <html lang="${lang}" dir="${direction}">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>${appState.teacherName} - ${appState.currentLanguage === 'ar' ? 'الملف المهني' : 'Professional Portfolio'}</title>
            <link rel="preconnect" href="https://fonts.googleapis.com">
            <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
            <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700&display=swap" rel="stylesheet">
            <style>
                * {
                    margin: 0;
                    padding: 0;
                    box-sizing: border-box;
                    font-family: 'Tajawal', sans-serif;
                }
                
                body {
                    background-color: #fff;
                    color: #333;
                    line-height: 1.6;
                    padding: 30px;
                    max-width: 1000px;
                    margin: 0 auto;
                }
                
                .document {
                    background: white;
                    box-shadow: 0 0 20px rgba(0,0,0,0.1);
                    padding: 40px;
                    border-radius: 8px;
                }
                
                .header {
                    text-align: center;
                    margin-bottom: 40px;
                    padding-bottom: 30px;
                    border-bottom: 3px solid #4a6fa5;
                }
                
                .header h1 {
                    color: #166088;
                    font-size: 2.5rem;
                    margin-bottom: 10px;
                }
                
                .header p {
                    color: #666;
                    font-size: 1.2rem;
                    margin-bottom: 5px;
                }
                
                .section {
                    margin-bottom: 30px;
                    page-break-inside: avoid;
                }
                
                .section h2 {
                    color: #166088;
                    font-size: 1.8rem;
                    margin-bottom: 15px;
                    padding-bottom: 10px;
                    border-bottom: 1px solid #eee;
                }
                
                .content {
                    font-size: 1.1rem;
                    white-space: pre-line;
                    margin-bottom: 10px;
                    line-height: 1.8;
                }
                
                .footer {
                    text-align: center;
                    margin-top: 50px;
                    padding-top: 20px;
                    border-top: 1px solid #eee;
                    color: #777;
                    font-size: 0.9rem;
                }
                
                @media print {
                    body {
                        padding: 0;
                    }
                    
                    .document {
                        box-shadow: none;
                        padding: 20px;
                    }
                    
                    .section {
                        page-break-inside: avoid;
                    }
                }
            </style>
        </head>
        <body>
            <div class="document">
                <div class="header">
                    <h1>${appState.teacherName}</h1>
                    <p>${appState.currentLanguage === 'ar' ? 'الملف المهني للمعلم' : 'Teacher Professional Portfolio'}</p>
                    <p>${new Date().toLocaleDateString(appState.currentLanguage === 'ar' ? 'ar-SA' : 'en-US', { 
                        year: 'numeric', 
                        month: 'long', 
                        day: 'numeric' 
                    })}</p>
                </div>
                
                ${Object.keys(appState.sections).map(sectionId => `
                    <div class="section">
                        <h2>${appState.sectionNames[appState.currentLanguage][sectionId]}</h2>
                        <div class="content">${appState.sections[sectionId] || (appState.currentLanguage === 'ar' ? 'لا توجد بيانات' : 'No data available')}</div>
                    </div>
                `).join('')}
                
                <div class="footer">
                    <p>${appState.currentLanguage === 'ar' 
                        ? 'تم الإنشاء بواسطة أداة الملف المهني للمعلم - جميع الحقوق محفوظة' 
                        : 'Generated by Teacher Professional Portfolio Tool - All rights reserved'}</p>
                </div>
            </div>
        </body>
        </html>`;
            }

            // تصدير إلى Excel
            function exportToExcel() {
                const teacherName = appState.teacherName.replace(/\s+/g, '_');
                const timestamp = new Date().toISOString().slice(0, 10).replace(/-/g, '');
                const filename = `Teacher_Portfolio_${teacherName}_${timestamp}.xlsx`;
                
                // إنشاء البيانات
                const data = [];
                
                // إضافة العناوين
                data.push([
                    appState.currentLanguage === 'ar' ? 'اسم القسم' : 'Section Name',
                    appState.currentLanguage === 'ar' ? 'المحتوى' : 'Content'
                ]);
                
                // إضافة بيانات كل قسم
                Object.keys(appState.sections).forEach(sectionId => {
                    const sectionTitle = appState.sectionNames[appState.currentLanguage][sectionId];
                    const content = appState.sections[sectionId] || (appState.currentLanguage === 'ar' ? 'لا توجد بيانات' : 'No data available');
                    data.push([sectionTitle, content]);
                });
                
                // إنشاء ورقة العمل
                const ws = XLSX.utils.aoa_to_sheet(data);
                
                // ضبط عرض الأعمدة
                const wscols = [
                    {wch: 25}, // عرض العمود الأول
                    {wch: 80}  // عرض العمود الثاني
                ];
                ws['!cols'] = wscols;
                
                // إنشاء المصنف وإضافة الورقة
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, appState.currentLanguage === 'ar' ? 'الملف المهني' : 'Portfolio');
                
                // حفظ الملف
                XLSX.writeFile(wb, filename);
                
                // إظهار إشعار النجاح
                showNotification(appState.uiTexts[appState.currentLanguage].notificationMessages.excelExported);
            }

            // إظهار إشعار
            function showNotification(message) {
                DOM.notificationMessage.textContent = message;
                DOM.successNotification.style.display = 'flex';
                
                // إخفاء الإشعار تلقائيًا بعد 3 ثوانٍ
                setTimeout(() => {
                    DOM.successNotification.style.display = 'none';
                }, 3000);
            }

            // حفظ البيانات
            function saveData() {
                const dataToSave = {
                    teacherName: appState.teacherName,
                    currentLanguage: appState.currentLanguage,
                    currentTheme: appState.currentTheme,
                    sections: appState.sections
                };
                
                try {
                    localStorage.setItem('teacherPortfolioData', JSON.stringify(dataToSave));
                } catch (e) {
                    console.error('Error saving data:', e);
                }
            }

            // تحميل البيانات المحفوظة
            function loadSavedData() {
                try {
                    const savedData = localStorage.getItem('teacherPortfolioData');
                    
                    if (savedData) {
                        const data = JSON.parse(savedData);
                        
                        // تحميل اسم المعلم
                        if (data.teacherName) {
                            appState.teacherName = data.teacherName;
                            DOM.teacherNameInput.value = data.teacherName;
                            DOM.nameDisplay.textContent = data.teacherName;
                        }
                        
                        // تحميل اللغة
                        if (data.currentLanguage) {
                            appState.currentLanguage = data.currentLanguage;
                            document.documentElement.dir = appState.currentLanguage === 'ar' ? 'rtl' : 'ltr';
                            document.documentElement.lang = appState.currentLanguage;
                        }
                        
                        // تحميل الوضع
                        if (data.currentTheme) {
                            appState.currentTheme = data.currentTheme;
                            DOM.body.classList.remove('light-mode', 'dark-mode');
                            DOM.body.classList.add(data.currentTheme);
                        }
                        
                        // تحميل بيانات الأقسام
                        if (data.sections) {
                            appState.sections = data.sections;
                            
                            // تحديث الحقول
                            Object.keys(data.sections).forEach(sectionId => {
                                const textarea = document.querySelector(`textarea[data-section="${sectionId}"]`);
                                if (textarea && data.sections[sectionId]) {
                                    textarea.value = data.sections[sectionId];
                                }
                            });
                        }
                    }
                } catch (e) {
                    console.error('Error loading saved data:', e);
                }
            }

            // بدء تشغيل التطبيق
            initApp();
        });
    </script>
</body>
</html>
