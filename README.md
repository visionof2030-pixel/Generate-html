<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة إنشاء الملف المهني للمعلمين</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #1abc9c;
            --light-color: #ecf0f1;
            --dark-color: #2c3e50;
            --text-color: #333;
            --text-light: #7f8c8d;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --border-radius: 8px;
            --transition: all 0.3s ease;
        }
        
        body {
            background-color: #f8f9fa;
            color: var(--text-color);
            line-height: 1.6;
            padding-bottom: 40px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 2rem 0;
            text-align: center;
            border-radius: 0 0 20px 20px;
            box-shadow: var(--shadow);
            margin-bottom: 30px;
        }
        
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .main-container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
        }
        
        .input-section, .preview-section {
            flex: 1;
            min-width: 300px;
            background-color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            padding: 25px;
        }
        
        .section-title {
            color: var(--primary-color);
            border-bottom: 2px solid var(--accent-color);
            padding-bottom: 10px;
            margin-bottom: 20px;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            color: var(--accent-color);
        }
        
        .control-buttons {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: var(--border-radius);
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .btn-primary {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
        }
        
        .btn-secondary {
            background-color: var(--accent-color);
            color: white;
        }
        
        .btn-secondary:hover {
            background-color: #16a085;
            transform: translateY(-2px);
        }
        
        .btn-outline {
            background-color: transparent;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
        }
        
        .btn-outline:hover {
            background-color: var(--primary-color);
            color: white;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--primary-color);
        }
        
        input, textarea {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: var(--border-radius);
            font-size: 1rem;
            transition: var(--transition);
        }
        
        input:focus, textarea:focus {
            outline: none;
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.2);
        }
        
        textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        .skills-container, .courses-container, .certificates-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }
        
        .skill-tag, .course-tag, .certificate-tag {
            background-color: var(--light-color);
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .skill-tag i, .course-tag i, .certificate-tag i {
            cursor: pointer;
            color: var(--text-light);
        }
        
        .skill-tag i:hover, .course-tag i:hover, .certificate-tag i:hover {
            color: #e74c3c;
        }
        
        .add-item {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .add-item input {
            flex: 1;
        }
        
        .add-item button {
            padding: 0 15px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            transition: var(--transition);
        }
        
        .add-item button:hover {
            background-color: #16a085;
        }
        
        /* تصميم العرض */
        .teacher-profile {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            max-width: 900px;
            margin: 0 auto;
        }
        
        .profile-header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 40px;
            text-align: center;
            position: relative;
        }
        
        .profile-header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .profile-header .title {
            font-size: 1.3rem;
            opacity: 0.9;
        }
        
        .profile-content {
            padding: 30px;
        }
        
        .tab-buttons {
            display: flex;
            flex-wrap: wrap;
            border-bottom: 1px solid #eee;
            margin-bottom: 25px;
        }
        
        .tab-btn {
            padding: 12px 25px;
            background: none;
            border: none;
            font-size: 1rem;
            font-weight: 600;
            color: var(--text-light);
            cursor: pointer;
            transition: var(--transition);
            position: relative;
        }
        
        .tab-btn:hover {
            color: var(--primary-color);
        }
        
        .tab-btn.active {
            color: var(--secondary-color);
        }
        
        .tab-btn.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            right: 0;
            height: 3px;
            background-color: var(--secondary-color);
        }
        
        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .tab-content.active {
            display: block;
        }
        
        .about-content, .skills-content, .courses-content, .certificates-content, .contact-content {
            line-height: 1.8;
        }
        
        .skills-list, .courses-list, .certificates-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .skill-item, .course-item, .certificate-item {
            background-color: var(--light-color);
            padding: 15px;
            border-radius: var(--border-radius);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .skill-item i, .course-item i, .certificate-item i {
            color: var(--secondary-color);
            font-size: 1.2rem;
        }
        
        .contact-info {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 15px;
        }
        
        .contact-item {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .contact-item i {
            width: 40px;
            height: 40px;
            background-color: var(--light-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--secondary-color);
        }
        
        .actions {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #eee;
        }
        
        .code-output {
            margin-top: 30px;
            display: none;
        }
        
        .code-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .code-container {
            background-color: #2c3e50;
            color: #ecf0f1;
            padding: 20px;
            border-radius: var(--border-radius);
            max-height: 400px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            white-space: pre-wrap;
        }
        
        .toggle-preview {
            display: none;
        }
        
        @media (max-width: 768px) {
            .main-container {
                flex-direction: column;
            }
            
            .toggle-preview {
                display: block;
                width: 100%;
                margin-top: 20px;
            }
            
            .preview-section {
                display: none;
            }
            
            .preview-section.active {
                display: block;
            }
            
            .tab-buttons {
                justify-content: center;
            }
            
            .skills-list, .courses-list, .certificates-list {
                grid-template-columns: 1fr;
            }
            
            .control-buttons {
                flex-direction: column;
            }
        }
        
        .footer {
            text-align: center;
            margin-top: 40px;
            color: var(--text-light);
            font-size: 0.9rem;
            padding-top: 20px;
            border-top: 1px solid #eee;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1><i class="fas fa-chalkboard-teacher"></i> أداة الملف المهني للمعلمين</h1>
            <p>أنشئ ملفًا مهنيًا احترافيًا بطريقتين: الملء التلقائي أو اليدوي</p>
        </div>
    </header>
    
    <main class="container">
        <div class="control-buttons">
            <button class="btn btn-primary" id="autoFillBtn">
                <i class="fas fa-magic"></i> الملء التلقائي
            </button>
            <button class="btn btn-secondary" id="generateBtn">
                <i class="fas fa-file-code"></i> إنشاء الملف المهني
            </button>
            <button class="btn btn-outline" id="clearBtn">
                <i class="fas fa-broom"></i> تفريغ الحقول
            </button>
        </div>
        
        <div class="main-container">
            <section class="input-section">
                <h2 class="section-title"><i class="fas fa-edit"></i> إدخال البيانات</h2>
                
                <div class="form-group">
                    <label for="name"><i class="fas fa-user"></i> الاسم الكامل</label>
                    <input type="text" id="name" placeholder="أدخل اسمك الكامل">
                </div>
                
                <div class="form-group">
                    <label for="title"><i class="fas fa-graduation-cap"></i> المسمى الوظيفي</label>
                    <input type="text" id="title" placeholder="مثال: معلم لغة عربية - مدرسة النجاح">
                </div>
                
                <div class="form-group">
                    <label for="about"><i class="fas fa-info-circle"></i> نبذة عني</label>
                    <textarea id="about" placeholder="أكتب نبذة مختصرة عن نفسك، خبراتك، وأهدافك المهنية..."></textarea>
                </div>
                
                <div class="form-group">
                    <label><i class="fas fa-tools"></i> المهارات</label>
                    <div class="skills-container" id="skillsContainer">
                        <!-- سيتم إضافة المهارات هنا ديناميكيًا -->
                    </div>
                    <div class="add-item">
                        <input type="text" id="newSkill" placeholder="أضف مهارة جديدة">
                        <button id="addSkillBtn"><i class="fas fa-plus"></i></button>
                    </div>
                </div>
                
                <div class="form-group">
                    <label><i class="fas fa-certificate"></i> الدورات</label>
                    <div class="courses-container" id="coursesContainer">
                        <!-- سيتم إضافة الدورات هنا ديناميكيًا -->
                    </div>
                    <div class="add-item">
                        <input type="text" id="newCourse" placeholder="أضف دورة جديدة">
                        <button id="addCourseBtn"><i class="fas fa-plus"></i></button>
                    </div>
                </div>
                
                <div class="form-group">
                    <label><i class="fas fa-award"></i> الشهادات الوظيفية</label>
                    <div class="certificates-container" id="certificatesContainer">
                        <!-- سيتم إضافة الشهادات هنا ديناميكيًا -->
                    </div>
                    <div class="add-item">
                        <input type="text" id="newCertificate" placeholder="أضف شهادة جديدة">
                        <button id="addCertificateBtn"><i class="fas fa-plus"></i></button>
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="contact"><i class="fas fa-envelope"></i> وسيلة الاتصال</label>
                    <input type="text" id="contact" placeholder="البريد الإلكتروني أو رقم الهاتف">
                </div>
                
                <button class="btn btn-primary toggle-preview" id="togglePreviewBtn">
                    <i class="fas fa-eye"></i> عرض النتيجة
                </button>
            </section>
            
            <section class="preview-section">
                <h2 class="section-title"><i class="fas fa-eye"></i> معاينة الملف المهني</h2>
                
                <div id="profilePreview">
                    <!-- سيتم عرض المعاينة هنا -->
                    <div class="teacher-profile">
                        <div class="profile-header">
                            <h1>اسم المعلم</h1>
                            <p class="title">المسمى الوظيفي</p>
                        </div>
                        
                        <div class="profile-content">
                            <div class="tab-buttons">
                                <button class="tab-btn active" data-tab="about">نبذة عني</button>
                                <button class="tab-btn" data-tab="skills">المهارات</button>
                                <button class="tab-btn" data-tab="courses">الدورات</button>
                                <button class="tab-btn" data-tab="certificates">الشهادات</button>
                                <button class="tab-btn" data-tab="contact">التواصل</button>
                            </div>
                            
                            <div class="tab-content active" id="aboutTab">
                                <p>ستظهر النبذة هنا بعد إدخال البيانات.</p>
                            </div>
                            
                            <div class="tab-content" id="skillsTab">
                                <p>ستظهر المهارات هنا بعد إدخال البيانات.</p>
                            </div>
                            
                            <div class="tab-content" id="coursesTab">
                                <p>ستظهر الدورات هنا بعد إدخال البيانات.</p>
                            </div>
                            
                            <div class="tab-content" id="certificatesTab">
                                <p>ستظهر الشهادات هنا بعد إدخال البيانات.</p>
                            </div>
                            
                            <div class="tab-content" id="contactTab">
                                <p>ستظهر وسيلة الاتصال هنا بعد إدخال البيانات.</p>
                            </div>
                            
                            <div class="actions">
                                <button class="btn btn-outline" id="editProfileBtn">
                                    <i class="fas fa-edit"></i> تعديل البيانات
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="code-output" id="codeOutput">
                    <div class="code-header">
                        <h3 class="section-title"><i class="fas fa-code"></i> كود HTML الناتج</h3>
                        <button class="btn btn-secondary" id="copyCodeBtn">
                            <i class="fas fa-copy"></i> نسخ الكود
                        </button>
                    </div>
                    <div class="code-container" id="codeContainer">
                        <!-- سيتم عرض كود HTML هنا -->
                    </div>
                    <p style="margin-top: 10px; font-size: 0.9rem; color: var(--text-light);">
                        <i class="fas fa-info-circle"></i> يمكنك نسخ هذا الكود وحفظه في ملف .html ورفعه على GitHub Pages
                    </p>
                </div>
            </section>
        </div>
    </main>
    
    <footer class="container footer">
        <p>تم تطوير هذه الأداة لمساعدة المعلمين على إنشاء ملفات مهنية احترافية. جميع الحقوق محفوظة &copy; 2023</p>
    </footer>

    <script>
        // بيانات افتراضية للملء التلقائي
        const defaultData = {
            name: "أحمد محمد عبدالله",
            title: "معلم لغة عربية - مدرسة النجاح الثانوية",
            about: "معلم لغة عربية بخبرة تزيد عن 10 سنوات في التدريس. حاصل على ماجستير في اللغة العربية وآدابها. أسعى دائمًا لتطوير أساليب التدريس لتحقيق أفضل النتائج مع الطلاب. مؤمن بأن التعليم هو أساس تقدم الأمم، وأعمل على غرس حب اللغة العربية في نفوس الطلاب.",
            skills: ["تدريس اللغة العربية", "تصميم المناهج التعليمية", "التدريب على الخطابة", "استخدام التكنولوجيا في التعليم", "إدارة الصفوف المتفاوتة المستوى"],
            courses: ["دورة معايير الجودة في التعليم", "دورة التعلم النشط", "دورة استخدام التكنولوجيا في التعليم", "دورة تطوير المناهج الدراسية", "دورة إدارة الفصول الافتراضية"],
            certificates: ["شهادة المعلم المتميز 2022", "شهادة المدرب المعتمد", "شهادة الجودة في التعليم", "شهادة متابعة التطورات التربوية"],
            contact: "ahmed.teacher@example.com | +966 55 123 4567"
        };

        // العناصر الرئيسية
        const nameInput = document.getElementById('name');
        const titleInput = document.getElementById('title');
        const aboutInput = document.getElementById('about');
        const contactInput = document.getElementById('contact');
        const skillsContainer = document.getElementById('skillsContainer');
        const coursesContainer = document.getElementById('coursesContainer');
        const certificatesContainer = document.getElementById('certificatesContainer');
        const newSkillInput = document.getElementById('newSkill');
        const newCourseInput = document.getElementById('newCourse');
        const newCertificateInput = document.getElementById('newCertificate');
        const addSkillBtn = document.getElementById('addSkillBtn');
        const addCourseBtn = document.getElementById('addCourseBtn');
        const addCertificateBtn = document.getElementById('addCertificateBtn');
        const autoFillBtn = document.getElementById('autoFillBtn');
        const generateBtn = document.getElementById('generateBtn');
        const clearBtn = document.getElementById('clearBtn');
        const togglePreviewBtn = document.getElementById('togglePreviewBtn');
        const previewSection = document.querySelector('.preview-section');
        const profilePreview = document.getElementById('profilePreview');
        const codeOutput = document.getElementById('codeOutput');
        const codeContainer = document.getElementById('codeContainer');
        const copyCodeBtn = document.getElementById('copyCodeBtn');
        const editProfileBtn = document.getElementById('editProfileBtn');

        // المهارات والدورات والشهادات المخزنة
        let skills = [];
        let courses = [];
        let certificates = [];

        // تهيئة الصفحة
        function init() {
            loadFromLocalStorage();
            renderSkills();
            renderCourses();
            renderCertificates();
            updatePreview();
            
            // إضافة مستمعي الأحداث
            addSkillBtn.addEventListener('click', addSkill);
            addCourseBtn.addEventListener('click', addCourse);
            addCertificateBtn.addEventListener('click', addCertificate);
            
            newSkillInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') addSkill();
            });
            
            newCourseInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') addCourse();
            });
            
            newCertificateInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') addCertificate();
            });
            
            autoFillBtn.addEventListener('click', autoFill);
            generateBtn.addEventListener('click', generateProfile);
            clearBtn.addEventListener('click', clearFields);
            togglePreviewBtn.addEventListener('click', togglePreview);
            copyCodeBtn.addEventListener('click', copyCode);
            editProfileBtn.addEventListener('click', () => {
                codeOutput.style.display = 'none';
                profilePreview.style.display = 'block';
            });
            
            // تحديث المعاينة عند تغيير البيانات
            const inputs = [nameInput, titleInput, aboutInput, contactInput];
            inputs.forEach(input => {
                input.addEventListener('input', updatePreview);
            });
            
            // إضافة مستمعي الأحداث لأزرار التبويب
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const tabId = this.getAttribute('data-tab');
                    switchTab(tabId);
                });
            });
            
            // حفظ البيانات تلقائيًا عند التغيير
            setInterval(saveToLocalStorage, 2000);
        }

        // تحميل البيانات من التخزين المحلي
        function loadFromLocalStorage() {
            const savedData = localStorage.getItem('teacherProfileData');
            if (savedData) {
                const data = JSON.parse(savedData);
                nameInput.value = data.name || '';
                titleInput.value = data.title || '';
                aboutInput.value = data.about || '';
                contactInput.value = data.contact || '';
                skills = data.skills || [];
                courses = data.courses || [];
                certificates = data.certificates || [];
            }
        }

        // حفظ البيانات في التخزين المحلي
        function saveToLocalStorage() {
            const data = {
                name: nameInput.value,
                title: titleInput.value,
                about: aboutInput.value,
                contact: contactInput.value,
                skills: skills,
                courses: courses,
                certificates: certificates
            };
            localStorage.setItem('teacherProfileData', JSON.stringify(data));
        }

        // إضافة مهارة
        function addSkill() {
            const skill = newSkillInput.value.trim();
            if (skill && !skills.includes(skill)) {
                skills.push(skill);
                renderSkills();
                newSkillInput.value = '';
                updatePreview();
            }
        }

        // إزالة مهارة
        function removeSkill(index) {
            skills.splice(index, 1);
            renderSkills();
            updatePreview();
        }

        // عرض المهارات
        function renderSkills() {
            skillsContainer.innerHTML = '';
            skills.forEach((skill, index) => {
                const skillElement = document.createElement('div');
                skillElement.className = 'skill-tag';
                skillElement.innerHTML = `
                    ${skill}
                    <i class="fas fa-times" onclick="removeSkill(${index})"></i>
                `;
                skillsContainer.appendChild(skillElement);
            });
        }

        // إضافة دورة
        function addCourse() {
            const course = newCourseInput.value.trim();
            if (course && !courses.includes(course)) {
                courses.push(course);
                renderCourses();
                newCourseInput.value = '';
                updatePreview();
            }
        }

        // إزالة دورة
        function removeCourse(index) {
            courses.splice(index, 1);
            renderCourses();
            updatePreview();
        }

        // عرض الدورات
        function renderCourses() {
            coursesContainer.innerHTML = '';
            courses.forEach((course, index) => {
                const courseElement = document.createElement('div');
                courseElement.className = 'course-tag';
                courseElement.innerHTML = `
                    ${course}
                    <i class="fas fa-times" onclick="removeCourse(${index})"></i>
                `;
                coursesContainer.appendChild(courseElement);
            });
        }

        // إضافة شهادة
        function addCertificate() {
            const certificate = newCertificateInput.value.trim();
            if (certificate && !certificates.includes(certificate)) {
                certificates.push(certificate);
                renderCertificates();
                newCertificateInput.value = '';
                updatePreview();
            }
        }

        // إزالة شهادة
        function removeCertificate(index) {
            certificates.splice(index, 1);
            renderCertificates();
            updatePreview();
        }

        // عرض الشهادات
        function renderCertificates() {
            certificatesContainer.innerHTML = '';
            certificates.forEach((certificate, index) => {
                const certificateElement = document.createElement('div');
                certificateElement.className = 'certificate-tag';
                certificateElement.innerHTML = `
                    ${certificate}
                    <i class="fas fa-times" onclick="removeCertificate(${index})"></i>
                `;
                certificatesContainer.appendChild(certificateElement);
            });
        }

        // الملء التلقائي
        function autoFill() {
            nameInput.value = defaultData.name;
            titleInput.value = defaultData.title;
            aboutInput.value = defaultData.about;
            contactInput.value = defaultData.contact;
            skills = [...defaultData.skills];
            courses = [...defaultData.courses];
            certificates = [...defaultData.certificates];
            
            renderSkills();
            renderCourses();
            renderCertificates();
            updatePreview();
            
            // إظهار رسالة نجاح
            showMessage('تم الملء التلقائي للبيانات بنجاح!', 'success');
        }

        // تفريغ الحقول
        function clearFields() {
            if (confirm('هل أنت متأكد من تفريغ جميع الحقول؟')) {
                nameInput.value = '';
                titleInput.value = '';
                aboutInput.value = '';
                contactInput.value = '';
                skills = [];
                courses = [];
                certificates = [];
                
                renderSkills();
                renderCourses();
                renderCertificates();
                updatePreview();
                
                // إظهار رسالة نجاح
                showMessage('تم تفريغ جميع الحقول بنجاح!', 'success');
            }
        }

        // تبديل العرض (للهواتف المحمولة)
        function togglePreview() {
            previewSection.classList.toggle('active');
            togglePreviewBtn.innerHTML = previewSection.classList.contains('active') 
                ? '<i class="fas fa-times"></i> إغلاق المعاينة' 
                : '<i class="fas fa-eye"></i> عرض النتيجة';
        }

        // تحديث المعاينة
        function updatePreview() {
            const name = nameInput.value || 'اسم المعلم';
            const title = titleInput.value || 'المسمى الوظيفي';
            const about = aboutInput.value || 'ستظهر النبذة هنا بعد إدخال البيانات.';
            const contact = contactInput.value || 'ستظهر وسيلة الاتصال هنا بعد إدخال البيانات.';
            
            // تحديث الهيكل الرئيسي
            profilePreview.innerHTML = `
                <div class="teacher-profile">
                    <div class="profile-header">
                        <h1>${name}</h1>
                        <p class="title">${title}</p>
                    </div>
                    
                    <div class="profile-content">
                        <div class="tab-buttons">
                            <button class="tab-btn active" data-tab="about">نبذة عني</button>
                            <button class="tab-btn" data-tab="skills">المهارات</button>
                            <button class="tab-btn" data-tab="courses">الدورات</button>
                            <button class="tab-btn" data-tab="certificates">الشهادات</button>
                            <button class="tab-btn" data-tab="contact">التواصل</button>
                        </div>
                        
                        <div class="tab-content active" id="aboutTab">
                            <div class="about-content">
                                <p>${about}</p>
                            </div>
                        </div>
                        
                        <div class="tab-content" id="skillsTab">
                            <div class="skills-content">
                                ${skills.length > 0 ? 
                                    `<div class="skills-list">
                                        ${skills.map(skill => `
                                            <div class="skill-item">
                                                <i class="fas fa-check-circle"></i>
                                                <span>${skill}</span>
                                            </div>
                                        `).join('')}
                                    </div>` : 
                                    '<p>لم يتم إضافة مهارات بعد.</p>'
                                }
                            </div>
                        </div>
                        
                        <div class="tab-content" id="coursesTab">
                            <div class="courses-content">
                                ${courses.length > 0 ? 
                                    `<div class="courses-list">
                                        ${courses.map(course => `
                                            <div class="course-item">
                                                <i class="fas fa-certificate"></i>
                                                <span>${course}</span>
                                            </div>
                                        `).join('')}
                                    </div>` : 
                                    '<p>لم يتم إضافة دورات بعد.</p>'
                                }
                            </div>
                        </div>
                        
                        <div class="tab-content" id="certificatesTab">
                            <div class="certificates-content">
                                ${certificates.length > 0 ? 
                                    `<div class="certificates-list">
                                        ${certificates.map(certificate => `
                                            <div class="certificate-item">
                                                <i class="fas fa-award"></i>
                                                <span>${certificate}</span>
                                            </div>
                                        `).join('')}
                                    </div>` : 
                                    '<p>لم يتم إضافة شهادات بعد.</p>'
                                }
                            </div>
                        </div>
                        
                        <div class="tab-content" id="contactTab">
                            <div class="contact-content">
                                <div class="contact-info">
                                    <div class="contact-item">
                                        <i class="fas fa-envelope"></i>
                                        <div>
                                            <h4>وسيلة الاتصال</h4>
                                            <p>${contact}</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="actions">
                            <button class="btn btn-outline" id="editProfileBtn">
                                <i class="fas fa-edit"></i> تعديل البيانات
                            </button>
                        </div>
                    </div>
                </div>
            `;
            
            // إعادة إضافة مستمعي الأحداث لأزرار التبويب
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const tabId = this.getAttribute('data-tab');
                    switchTab(tabId);
                });
            });
            
            // إعادة إضافة مستمع الحدث لزر تعديل البيانات
            document.getElementById('editProfileBtn').addEventListener('click', () => {
                codeOutput.style.display = 'none';
                profilePreview.style.display = 'block';
            });
            
            saveToLocalStorage();
        }

        // تبديل التبويبات
        function switchTab(tabId) {
            // إزالة الفئة النشطة من جميع الأزرار والمحتويات
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // إضافة الفئة النشطة للزر والمحتوى المحدد
            document.querySelector(`.tab-btn[data-tab="${tabId}"]`).classList.add('active');
            document.getElementById(`${tabId}Tab`).classList.add('active');
        }

        // إنشاء الملف المهني النهائي
        function generateProfile() {
            updatePreview();
            
            const profileHTML = generateCompleteHTML();
            codeContainer.textContent = profileHTML;
            codeOutput.style.display = 'block';
            profilePreview.style.display = 'none';
            
            // التمرير إلى قسم الكود
            codeOutput.scrollIntoView({ behavior: 'smooth' });
            
            // إظهار رسالة نجاح
            showMessage('تم إنشاء الملف المهني بنجاح! يمكنك نسخ الكود الآن.', 'success');
        }

        // إنشاء كود HTML كامل
        function generateCompleteHTML() {
            const name = nameInput.value || 'اسم المعلم';
            const title = titleInput.value || 'المسمى الوظيفي';
            const about = aboutInput.value || 'لم يتم إضافة نبذة بعد.';
            const contact = contactInput.value || 'لم يتم إضافة وسيلة اتصال.';
            
            return `<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الملف المهني - ${name}</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #1abc9c;
            --light-color: #ecf0f1;
            --dark-color: #2c3e50;
            --text-color: #333;
            --text-light: #7f8c8d;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --border-radius: 8px;
            --transition: all 0.3s ease;
        }
        
        body {
            background-color: #f8f9fa;
            color: var(--text-color);
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .teacher-profile {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            max-width: 900px;
            width: 100%;
        }
        
        .profile-header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 40px;
            text-align: center;
            position: relative;
        }
        
        .profile-header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .profile-header .title {
            font-size: 1.3rem;
            opacity: 0.9;
        }
        
        .profile-content {
            padding: 30px;
        }
        
        .tab-buttons {
            display: flex;
            flex-wrap: wrap;
            border-bottom: 1px solid #eee;
            margin-bottom: 25px;
        }
        
        .tab-btn {
            padding: 12px 25px;
            background: none;
            border: none;
            font-size: 1rem;
            font-weight: 600;
            color: var(--text-light);
            cursor: pointer;
            transition: var(--transition);
            position: relative;
        }
        
        .tab-btn:hover {
            color: var(--primary-color);
        }
        
        .tab-btn.active {
            color: var(--secondary-color);
        }
        
        .tab-btn.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            right: 0;
            height: 3px;
            background-color: var(--secondary-color);
        }
        
        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .tab-content.active {
            display: block;
        }
        
        .about-content, .skills-content, .courses-content, .certificates-content, .contact-content {
            line-height: 1.8;
        }
        
        .skills-list, .courses-list, .certificates-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .skill-item, .course-item, .certificate-item {
            background-color: var(--light-color);
            padding: 15px;
            border-radius: var(--border-radius);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .skill-item i, .course-item i, .certificate-item i {
            color: var(--secondary-color);
            font-size: 1.2rem;
        }
        
        .contact-info {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 15px;
        }
        
        .contact-item {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .contact-item i {
            width: 40px;
            height: 40px;
            background-color: var(--light-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--secondary-color);
        }
        
        .footer {
            text-align: center;
            margin-top: 40px;
            color: var(--text-light);
            font-size: 0.9rem;
            padding-top: 20px;
            border-top: 1px solid #eee;
        }
        
        @media (max-width: 768px) {
            .profile-header {
                padding: 30px 20px;
            }
            
            .profile-header h1 {
                font-size: 2rem;
            }
            
            .profile-content {
                padding: 20px;
            }
            
            .tab-buttons {
                justify-content: center;
            }
            
            .skills-list, .courses-list, .certificates-list {
                grid-template-columns: 1fr;
            }
            
            body {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="teacher-profile">
        <div class="profile-header">
            <h1>${name}</h1>
            <p class="title">${title}</p>
        </div>
        
        <div class="profile-content">
            <div class="tab-buttons">
                <button class="tab-btn active" data-tab="about">نبذة عني</button>
                <button class="tab-btn" data-tab="skills">المهارات</button>
                <button class="tab-btn" data-tab="courses">الدورات</button>
                <button class="tab-btn" data-tab="certificates">الشهادات</button>
                <button class="tab-btn" data-tab="contact">التواصل</button>
            </div>
            
            <div class="tab-content active" id="aboutTab">
                <div class="about-content">
                    <p>${about}</p>
                </div>
            </div>
            
            <div class="tab-content" id="skillsTab">
                <div class="skills-content">
                    ${skills.length > 0 ? 
                        `<div class="skills-list">
                            ${skills.map(skill => `
                                <div class="skill-item">
                                    <i class="fas fa-check-circle"></i>
                                    <span>${skill}</span>
                                </div>
                            `).join('')}
                        </div>` : 
                        '<p>لم يتم إضافة مهارات بعد.</p>'
                    }
                </div>
            </div>
            
            <div class="tab-content" id="coursesTab">
                <div class="courses-content">
                    ${courses.length > 0 ? 
                        `<div class="courses-list">
                            ${courses.map(course => `
                                <div class="course-item">
                                    <i class="fas fa-certificate"></i>
                                    <span>${course}</span>
                                </div>
                            `).join('')}
                        </div>` : 
                        '<p>لم يتم إضافة دورات بعد.</p>'
                    }
                </div>
            </div>
            
            <div class="tab-content" id="certificatesTab">
                <div class="certificates-content">
                    ${certificates.length > 0 ? 
                        `<div class="certificates-list">
                            ${certificates.map(certificate => `
                                <div class="certificate-item">
                                    <i class="fas fa-award"></i>
                                    <span>${certificate}</span>
                                </div>
                            `).join('')}
                        </div>` : 
                        '<p>لم يتم إضافة شهادات بعد.</p>'
                    }
                </div>
            </div>
            
            <div class="tab-content" id="contactTab">
                <div class="contact-content">
                    <div class="contact-info">
                        <div class="contact-item">
                            <i class="fas fa-envelope"></i>
                            <div>
                                <h4>وسيلة الاتصال</h4>
                                <p>${contact}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="footer">
                <p>تم إنشاء هذا الملف المهني باستخدام أداة المعلمين المهنية</p>
            </div>
        </div>
    </div>
    
    <script>
        // تبديل التبويبات
        document.querySelectorAll('.tab-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                // إزالة الفئة النشطة من جميع الأزرار والمحتويات
                document.querySelectorAll('.tab-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
                
                document.querySelectorAll('.tab-content').forEach(content => {
                    content.classList.remove('active');
                });
                
                // إضافة الفئة النشطة للزر والمحتوى المحدد
                const tabId = this.getAttribute('data-tab');
                this.classList.add('active');
                document.getElementById(tabId + 'Tab').classList.add('active');
            });
        });
    </script>
</body>
</html>`;
        }

        // نسخ الكود
        function copyCode() {
            const code = codeContainer.textContent;
            navigator.clipboard.writeText(code).then(() => {
                showMessage('تم نسخ الكود بنجاح!', 'success');
                copyCodeBtn.innerHTML = '<i class="fas fa-check"></i> تم النسخ';
                setTimeout(() => {
                    copyCodeBtn.innerHTML = '<i class="fas fa-copy"></i> نسخ الكود';
                }, 2000);
            }).catch(err => {
                showMessage('حدث خطأ أثناء نسخ الكود', 'error');
                console.error('Error copying text: ', err);
            });
        }

        // عرض رسالة للمستخدم
        function showMessage(message, type) {
            // إنشاء عنصر الرسالة
            const messageElement = document.createElement('div');
            messageElement.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                padding: 15px 20px;
                border-radius: var(--border-radius);
                color: white;
                font-weight: 600;
                box-shadow: var(--shadow);
                z-index: 1000;
                animation: slideIn 0.3s ease;
            `;
            
            messageElement.style.backgroundColor = type === 'success' ? '#2ecc71' : '#e74c3c';
            
            messageElement.textContent = message;
            document.body.appendChild(messageElement);
            
            // إزالة الرسالة بعد 3 ثوان
            setTimeout(() => {
                messageElement.style.animation = 'slideOut 0.3s ease';
                setTimeout(() => {
                    document.body.removeChild(messageElement);
                }, 300);
            }, 3000);
            
            // إضافة أنماط الحركة
            const style = document.createElement('style');
            style.textContent = `
                @keyframes slideIn {
                    from { transform: translateX(100%); opacity: 0; }
                    to { transform: translateX(0); opacity: 1; }
                }
                @keyframes slideOut {
                    from { transform: translateX(0); opacity: 1; }
                    to { transform: translateX(100%); opacity: 0; }
                }
            `;
            document.head.appendChild(style);
        }

        // بدء التطبيق
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
