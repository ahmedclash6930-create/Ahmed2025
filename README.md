<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>قراصنة الدراسة - نظام الجدولة المتقدم</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&display=swap');
        
        :root {
            --straw-hat: #FF6B00;
            --navy-blue: #00308F;
            --gold: #FFD700;
            --red: #DC2626;
            --sea: #00B4D8;
            --green: #10B981;
            --purple: #8B5CF6;
            --pink: #EC4899;
            --cyan: #06D6A0;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Cairo', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        /* الهيدر المتحرك */
        header {
            text-align: center;
            padding: 30px;
            background: linear-gradient(135deg, var(--navy-blue), var(--purple));
            border-radius: 20px;
            margin-bottom: 30px;
            border: 4px solid var(--gold);
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        
        .header-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.1;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><text x="50%" y="50%" font-size="30" fill="%23FFD700">🏴‍☠️</text></svg>');
        }
        
        h1 {
            font-size: 3.5em;
            color: var(--gold);
            text-shadow: 4px 4px 0 var(--red);
            margin-bottom: 10px;
            position: relative;
        }
        
        .subtitle {
            font-size: 1.4em;
            color: white;
            margin-bottom: 15px;
            font-weight: 300;
        }
        
        /* التبويبات */
        .tabs {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 30px;
        }
        
        .tab-btn {
            padding: 15px 30px;
            background: rgba(255,255,255,0.2);
            border: none;
            border-radius: 50px;
            color: white;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            border: 2px solid transparent;
        }
        
        .tab-btn.active {
            background: var(--gold);
            color: var(--navy-blue);
            border-color: white;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(255,215,0,0.4);
        }
        
        .tab-btn:hover:not(.active) {
            background: rgba(255,255,255,0.3);
            transform: translateY(-2px);
        }
        
        /* المحتوى الرئيسي */
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        .section-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            padding: 30px;
            border-radius: 20px;
            border: 3px solid;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }
        
        .section-card:hover {
            transform: translateY(-5px);
        }
        
        .upload-section {
            border-color: var(--sea);
        }
        
        .schedule-section {
            border-color: var(--green);
        }
        
        .section-title {
            font-size: 1.8em;
            color: var(--navy-blue);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            color: var(--straw-hat);
        }
        
        /* منطقة رفع الملفات */
        .upload-area {
            border: 3px dashed var(--sea);
            border-radius: 15px;
            padding: 40px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 20px;
            background: rgba(0, 180, 216, 0.05);
        }
        
        .upload-area:hover {
            background: rgba(0, 180, 216, 0.1);
            border-color: var(--cyan);
            transform: scale(1.02);
        }
        
        .upload-icon {
            font-size: 70px;
            margin-bottom: 15px;
            color: var(--sea);
        }
        
        /* إدخال المواد يدوياً */
        .manual-input {
            margin-top: 25px;
        }
        
        .input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .input-group input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: var(--sea);
            box-shadow: 0 0 0 3px rgba(0, 180, 216, 0.1);
        }
        
        .add-btn {
            padding: 12px 20px;
            background: var(--green);
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .add-btn:hover {
            background: #059669;
            transform: scale(1.05);
        }
        
        /* قائمة المواد */
        .subjects-list {
            margin-top: 20px;
            max-height: 200px;
            overflow-y: auto;
        }
        
        .subject-item {
            background: linear-gradient(135deg, #f8fafc, #e2e8f0);
            padding: 12px 15px;
            margin: 8px 0;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 4px solid var(--straw-hat);
            transition: all 0.3s ease;
        }
        
        .subject-item:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .subject-actions {
            display: flex;
            gap: 8px;
        }
        
        .delete-btn {
            background: var(--red);
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .delete-btn:hover {
            background: #b91c1c;
            transform: scale(1.1);
        }
        
        /* إعدادات الجدول */
        .settings-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin: 20px 0;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            color: var(--navy-blue);
            font-weight: 600;
        }
        
        input, select {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: var(--sea);
            box-shadow: 0 0 0 3px rgba(0, 180, 216, 0.1);
        }
        
        /* أزرار العمل */
        .action-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 25px;
        }
        
        .btn {
            padding: 15px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--straw-hat), var(--red));
            color: white;
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, var(--navy-blue), var(--purple));
            color: white;
        }
        
        .btn-success {
            background: linear-gradient(135deg, var(--green), var(--cyan));
            color: white;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.2);
        }
        
        /* عرض الجدول */
        .schedule-display {
            margin-top: 20px;
            background: white;
            border-radius: 15px;
            padding: 20px;
            max-height: 500px;
            overflow-y: auto;
            border: 2px solid #e2e8f0;
        }
        
        .day-schedule {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 15px 0;
            padding: 20px;
            border-radius: 15px;
            color: white;
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
            border-left: 5px solid var(--gold);
        }
        
        .day-header {
            color: var(--gold);
            font-weight: bold;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 1.3em;
            padding-bottom: 10px;
            border-bottom: 2px solid rgba(255,255,255,0.3);
        }
        
        .schedule-item {
            background: rgba(255, 255, 255, 0.15);
            padding: 12px 15px;
            margin: 10px 0;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            backdrop-filter: blur(10px);
            border-right: 3px solid;
            transition: all 0.3s ease;
        }
        
        .schedule-item:hover {
            transform: translateX(5px);
            background: rgba(255, 255, 255, 0.25);
        }
        
        .schedule-item.study {
            border-right-color: var(--cyan);
        }
        
        .schedule-item.break {
            border-right-color: var(--gold);
            background: rgba(255, 215, 0, 0.2);
        }
        
        .time-badge {
            background: rgba(255,255,255,0.2);
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: bold;
        }
        
        /* أزرار التحميل */
        .download-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }
        
        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #6b7280;
        }
        
        .empty-state i {
            font-size: 60px;
            margin-bottom: 15px;
            color: #d1d5db;
        }
        
        /* التكيف مع الشاشات الصغيرة */
        @media (max-width: 1024px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .settings-grid {
                grid-template-columns: 1fr;
            }
            
            .action-buttons {
                grid-template-columns: 1fr;
            }
            
            .download-section {
                grid-template-columns: 1fr;
            }
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5em;
            }
            
            .tabs {
                flex-direction: column;
            }
            
            .section-card {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-bg"></div>
            <h1><i class="fas fa-skull-crossbones"></i> قراصنة الدراسة <i class="fas fa-skull-crossbones"></i></h1>
            <div class="subtitle">اكتشف كنز المعرفة مع طاقم قبعات القش!</div>
        </header>
        
        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('upload')">
                <i class="fas fa-upload"></i> رفع الملفات
            </button>
            <button class="tab-btn" onclick="switchTab('manual')">
                <i class="fas fa-edit"></i> إدخال المواد
            </button>
        </div>
        
        <div class="main-content">
            <!-- قسم الإدخال -->
            <div class="section-card upload-section">
                <h2 class="section-title"><i class="fas fa-file-upload"></i> إدخال المواد الدراسية</h2>
                
                <!-- تبويب رفع الملفات -->
                <div id="uploadTab" class="tab-content">
                    <div class="upload-area" id="uploadArea">
                        <div class="upload-icon">
                            <i class="fas fa-cloud-upload-alt"></i>
                        </div>
                        <div style="font-size: 1.2em; margin-bottom: 10px; font-weight: bold;">اسحب وأفلت الملفات هنا</div>
                        <div style="font-size: 0.9em; color: #6b7280;">
                            أو انقر لاختيار الملفات (PDF, Word, PowerPoint, الصور)
                        </div>
                    </div>
                    
                    <div class="file-list" id="fileList">
                        <!-- الملفات المرفوعة تظهر هنا -->
                    </div>
                </div>
                
                <!-- تبويب الإدخال اليدوي -->
                <div id="manualTab" class="tab-content" style="display: none;">
                    <div class="manual-input">
                        <div class="input-group">
                            <input type="text" id="subjectInput" placeholder="أدخل اسم المادة...">
                            <button class="add-btn" onclick="addManualSubject()">
                                <i class="fas fa-plus"></i> إضافة
                            </button>
                        </div>
                        
                        <div class="subjects-list" id="subjectsList">
                            <!-- المواد المضافة تظهر هنا -->
                        </div>
                    </div>
                </div>
                
                <!-- إعدادات الجدول -->
                <div class="settings-grid">
                    <div class="form-group">
                        <label for="studyDays"><i class="fas fa-calendar-day"></i> عدد أيام الدراسة:</label>
                        <input type="number" id="studyDays" min="1" max="90" value="7">
                    </div>
                    
                    <div class="form-group">
                        <label for="dailyHours"><i class="fas fa-clock"></i> ساعات الدراسة اليومية:</label>
                        <select id="dailyHours">
                            <option value="2">2 ساعات</option>
                            <option value="3" selected>3 ساعات</option>
                            <option value="4">4 ساعات</option>
                            <option value="5">5 ساعات</option>
                            <option value="6">6 ساعات</option>
                            <option value="8">8 ساعات</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="startTime"><i class="fas fa-play"></i> وقت البدء:</label>
                        <select id="startTime">
                            <option value="8">8:00 صباحاً</option>
                            <option value="9" selected>9:00 صباحاً</option>
                            <option value="10">10:00 صباحاً</option>
                            <option value="14">2:00 مساءً</option>
                            <option value="16">4:00 مساءً</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="breakTime"><i class="fas fa-coffee"></i> مدة الاستراحة:</label>
                        <select id="breakTime">
                            <option value="10">10 دقائق</option>
                            <option value="15" selected>15 دقيقة</option>
                            <option value="20">20 دقيقة</option>
                            <option value="30">30 دقيقة</option>
                        </select>
                    </div>
                </div>
                
                <div class="action-buttons">
                    <button class="btn btn-primary" onclick="generateSchedule()">
                        <i class="fas fa-magic"></i> إنشاء الجدول
                    </button>
                    <button class="btn btn-secondary" onclick="clearAll()">
                        <i class="fas fa-trash"></i> مسح الكل
                    </button>
                </div>
            </div>
            
            <!-- قسم عرض الجدول -->
            <div class="section-card schedule-section">
                <h2 class="section-title"><i class="fas fa-calendar-alt"></i> جدول الدراسة</h2>
                
                <div class="schedule-display" id="scheduleDisplay">
                    <div class="empty-state">
                        <i class="fas fa-calendar-plus"></i>
                        <div style="font-size: 1.2em; margin-bottom: 10px;">لا يوجد جدول حالياً</div>
                        <div>قم بإضافة المواد وإنشاء الجدول لعرضه هنا</div>
                    </div>
                </div>
                
                <div class="download-section">
                    <button class="btn btn-success" onclick="downloadPDF()">
                        <i class="fas fa-file-pdf"></i> تحميل PDF
                    </button>
                    <button class="btn btn-secondary" onclick="downloadJSON()">
                        <i class="fas fa-file-code"></i> تحميل JSON
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // تهيئة jsPDF
        const { jsPDF } = window.jspdf;
        
        let uploadedFiles = [];
        let manualSubjects = [];
        let currentSchedule = [];
        let currentTab = 'upload';
        
        // تبديل التبويبات
        function switchTab(tabName) {
            currentTab = tabName;
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.style.display = 'none');
            
            event.target.classList.add('active');
            document.getElementById(tabName + 'Tab').style.display = 'block';
        }
        
        // نظام رفع الملفات
        const uploadArea = document.getElementById('uploadArea');
        const fileList = document.getElementById('fileList');
        
        uploadArea.addEventListener('click', () => {
            const input = document.createElement('input');
            input.type = 'file';
            input.multiple = true;
            input.accept = '.pdf,.doc,.docx,.ppt,.pptx,.jpg,.jpeg,.png,.txt';
            input.onchange = handleFileSelect;
            input.click();
        });
        
        uploadArea.addEventListener('dragover', (e) => {
            e.preventDefault();
            uploadArea.style.background = 'rgba(0, 180, 216, 0.1)';
            uploadArea.style.borderColor = 'var(--cyan)';
        });
        
        uploadArea.addEventListener('dragleave', () => {
            uploadArea.style.background = '';
            uploadArea.style.borderColor = 'var(--sea)';
        });
        
        uploadArea.addEventListener('drop', (e) => {
            e.preventDefault();
            uploadArea.style.background = '';
            uploadArea.style.borderColor = 'var(--sea)';
            handleFiles(e.dataTransfer.files);
        });
        
        function handleFileSelect(e) {
            handleFiles(e.target.files);
        }
        
        function handleFiles(files) {
            for (let file of files) {
                uploadedFiles.push({
                    name: file.name.replace(/\.[^/.]+$/, ""), // إزالة الامتداد
                    size: file.size,
                    type: file.type,
                    originalName: file.name
                });
            }
            updateFileList();
        }
        
        function updateFileList() {
            fileList.innerHTML = '';
            uploadedFiles.forEach((file, index) => {
                const fileItem = document.createElement('div');
                fileItem.className = 'subject-item';
                fileItem.innerHTML = `
                    <span>${file.name}</span>
                    <div class="subject-actions">
                        <span style="color: #6b7280; font-size: 0.9em;">${formatFileSize(file.size)}</span>
                        <button class="delete-btn" onclick="removeFile(${index})">
                            <i class="fas fa-times"></i>
                        </button>
                    </div>
                `;
                fileList.appendChild(fileItem);
            });
        }
        
        function removeFile(index) {
            uploadedFiles.splice(index, 1);
            updateFileList();
        }
        
        // نظام الإدخال اليدوي
        function addManualSubject() {
            const input = document.getElementById('subjectInput');
            const subjectName = input.value.trim();
            
            if (subjectName) {
                manualSubjects.push({
                    name: subjectName,
                    type: 'manual'
                });
                input.value = '';
                updateSubjectsList();
            }
        }
        
        function updateSubjectsList() {
            const subjectsList = document.getElementById('subjectsList');
            subjectsList.innerHTML = '';
            
            manualSubjects.forEach((subject, index) => {
                const subjectItem = document.createElement('div');
                subjectItem.className = 'subject-item';
                subjectItem.innerHTML = `
                    <span>${subject.name}</span>
                    <button class="delete-btn" onclick="removeManualSubject(${index})">
                        <i class="fas fa-times"></i>
                    </button>
                `;
                subjectsList.appendChild(subjectItem);
            });
        }
        
        function removeManualSubject(index) {
            manualSubjects.splice(index, 1);
            updateSubjectsList();
        }
        
        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }
        
        // نظام إنشاء الجدول
        function generateSchedule() {
            let subjects = [];
            
            if (currentTab === 'upload') {
                subjects = uploadedFiles.map(file => file.name);
            } else {
                subjects = manualSubjects.map(subject => subject.name);
            }
            
            if (subjects.length === 0) {
                alert('🏴‍☠️ يا رفيق! تحتاج لإضافة بعض المواد أولاً!');
                return;
            }
            
            const studyDays = parseInt(document.getElementById('studyDays').value);
            const dailyHours = parseInt(document.getElementById('dailyHours').value);
            const startTime = parseInt(document.getElementById('startTime').value);
            const breakTime = parseInt(document.getElementById('breakTime').value);
            
            const scheduleDisplay = document.getElementById('scheduleDisplay');
            scheduleDisplay.innerHTML = '';
            
            currentSchedule = [];
            const subjectsPerDay = Math.ceil(subjects.length / studyDays);
            const studyMinutes = dailyHours * 60;
            const minutesPerSubject = Math.floor(studyMinutes / subjectsPerDay);
            
            for (let day = 1; day <= studyDays; day++) {
                const daySchedule = {
                    day: day,
                    hours: dailyHours,
                    items: []
                };
                
                const dayElement = document.createElement('div');
                dayElement.className = 'day-schedule';
                
                const dayHeader = document.createElement('div');
                dayHeader.className = 'day-header';
                dayHeader.innerHTML = `
                    <span>اليوم ${day}</span>
                    <span>${dailyHours} ساعات دراسة</span>
                `;
                dayElement.appendChild(dayHeader);
                
                const startIndex = (day - 1) * subjectsPerDay;
                const endIndex = Math.min(startIndex + subjectsPerDay, subjects.length);
                
                let currentTime = startTime * 60; // تحويل إلى دقائق
                
                for (let i = startIndex; i < endIndex; i++) {
                    if (i >= subjects.length) break;
                    
                    const subjectTime = Math.max(30, Math.min(120, minutesPerSubject));
                    const startTimeStr = formatTime(currentTime);
                    const endTimeStr = formatTime(currentTime + subjectTime);
                    
                    // إضافة مادة الدراسة
                    daySchedule.items.push({
                        type: 'study',
                        subject: subjects[i],
                        startTime: startTimeStr,
                        endTime: endTimeStr,
                        duration: subjectTime
                    });
                    
                    const studyElement = document.createElement('div');
                    studyElement.className = 'schedule-item study';
                    studyElement.innerHTML = `
                        <div>
                            <i class="fas fa-book"></i>
                            <strong>${subjects[i]}</strong>
                        </div>
                        <div class="time-badge">
                            ${startTimeStr} - ${endTimeStr}
                        </div>
                    `;
                    dayElement.appendChild(studyElement);
                    
                    currentTime += subjectTime;
                    
                    // إضافة استراحة بعد كل مادتين
                    if ((i - startIndex + 1) % 2 === 0 && (i - startIndex + 1) < (endIndex - startIndex)) {
                        const breakStart = formatTime(currentTime);
                        const breakEnd = formatTime(currentTime + breakTime);
                        
                        daySchedule.items.push({
                            type: 'break',
                            description: 'استراحة',
                            startTime: breakStart,
                            endTime: breakEnd,
                            duration: breakTime
                        });
                        
                        const breakElement = document.createElement('div');
                        breakElement.className = 'schedule-item break';
                        breakElement.innerHTML = `
                            <div>
                                <i class="fas fa-coffee"></i>
                                <span>استراحة</span>
                            </div>
                            <div class="time-badge">
                                ${breakStart} - ${breakEnd}
                            </div>
                        `;
                        dayElement.appendChild(breakElement);
                        
                        currentTime += breakTime;
                    }
                }
                
                currentSchedule.push(daySchedule);
                scheduleDisplay.appendChild(dayElement);
            }
        }
        
        function formatTime(minutes) {
            const hours = Math.floor(minutes / 60);
            const mins = minutes % 60;
            const period = hours >= 12 ? 'مساءً' : 'صباحاً';
            const displayHours = hours > 12 ? hours - 12 : hours;
            return `${displayHours.toString().padStart(2, '0')}:${mins.toString().padStart(2, '0')} ${period}`;
        }
        
        // تحميل PDF
        async function downloadPDF() {
            if (currentSchedule.length === 0) {
                alert('🏴‍☠️ تحتاج لإنشاء جدول أولاً يا رفيق!');
                return;
            }
            
            try {
                const doc = new jsPDF();
                
                // ترويسة الوثيقة
                doc.setFillColor(26, 42, 108);
                doc.rect(0, 0, 210, 50, 'F');
                
                doc.setFont('helvetica', 'bold');
                doc.setFontSize(25);
                doc.setTextColor(255, 215, 0);
                doc.text('جدول الدراسة - قراصنة المعرفة', 105, 20, null, null, 'center');
                
                doc.setFontSize(12);
                doc.setTextColor(255, 255, 255);
                doc.text(`تم الإنشاء في: ${new Date().toLocaleDateString('ar-EG')}`, 105, 35, null, null, 'center');
                
                let yPosition = 60;
                
                // إضافة الجدول
                currentSchedule.forEach((day, dayIndex) => {
                    if (yPosition > 250) {
                        doc.addPage();
                        yPosition = 20;
                    }
                    
                    // عنوان اليوم
                    doc.setFontSize(16);
                    doc.setTextColor(255, 107, 0);
                    doc.text(`اليوم ${day.day} - ${day.hours} ساعات دراسة`, 20, yPosition);
                    yPosition += 12;
                    
                    // خط فاصل
                    doc.setDrawColor(255, 107, 0);
                    doc.line(20, yPosition, 190, yPosition);
                    yPosition += 10;
                    
                    // عناصر الجدول
                    doc.setFontSize(10);
                    day.items.forEach((item, itemIndex) => {
                        if (yPosition > 280) {
                            doc.addPage();
                            yPosition = 20;
                        }
                        
                        if (item.type === 'study') {
                            doc.setTextColor(0, 0, 0);
                            doc.text(`📚 ${item.subject}`, 25, yPosition);
                            doc.setTextColor(255, 107, 0);
                            doc.text(`${item.startTime} - ${item.endTime}`, 180, yPosition, null, null, 'right');
                        } else {
                            doc.setTextColor(100, 100, 100);
                            doc.text(`☕ ${item.description}`, 25, yPosition);
                            doc.setTextColor(255, 107, 0);
                            doc.text(`${item.startTime} - ${item.endTime}`, 180, yPosition, null, null, 'right');
                        }
                        yPosition += 8;
                    });
                    
                    yPosition += 15;
                });
                
                // تذييل
                doc.setFontSize(8);
                doc.setTextColor(150, 150, 150);
                doc.text('⚓ صنع بفخر من قبل قراصنة الدراسة 🏴‍☠️', 105, 290, null, null, 'center');
                
                doc.save('جدول_الدراسة_المثالي.pdf');
                
            } catch (error) {
                console.error('Error generating PDF:', error);
                alert('❌ حدث خطأ في إنشاء PDF. حاول مرة أخرى!');
            }
        }
        
        // تحميل JSON
        function downloadJSON() {
            if (currentSchedule.length === 0) {
                alert('🏴‍☠️ تحتاج لإنشاء جدول أولاً يا رفيق!');
                return;
            }
            
            const scheduleData = {
                subjects: currentTab === 'upload' ? uploadedFiles : manualSubjects,
                schedule: currentSchedule,
                settings: {
                    days: document.getElementById('studyDays').value,
                    hours: document.getElementById('dailyHours').value,
                    startTime: document.getElementById('startTime').value,
                    breakTime: document.getElementById('breakTime').value
                },
                generatedAt: new Date().toLocaleString(),
                theme: "ون بيس - قراصنة الدراسة"
            };
            
            const blob = new Blob([JSON.stringify(scheduleData, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'جدول_الدراسة_قراصنة.json';
            a.click();
            URL.revokeObjectURL(url);
        }
        
        // مسح الكل
        function clearAll() {
            uploadedFiles = [];
            manualSubjects = [];
            currentSchedule = [];
            updateFileList();
            updateSubjectsList();
            document.getElementById('scheduleDisplay').innerHTML = `
                <div class="empty-state">
                    <i class="fas fa-calendar-plus"></i>
                    <div style="font-size: 1.2em; margin-bottom: 10px;">لا يوجد جدول حالياً</div>
                    <div>قم بإضافة المواد وإنشاء الجدول لعرضه هنا</div>
                </div>
            `;
        }
        
        // السماح بإضافة المواد بالضغط على Enter
        document.getElementById('subjectInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addManualSubject();
            }
        });
    </script>
</body>
</html>
