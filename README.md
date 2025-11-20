<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة علوم - الفرقة الأولى</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            padding: 20px;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .nav {
            background: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-links {
            display: flex;
            justify-content: center;
            list-style: none;
            gap: 20px;
            flex-wrap: wrap;
        }

        .nav-links a {
            text-decoration: none;
            color: #667eea;
            font-weight: 600;
            padding: 8px 16px;
            border-radius: 6px;
            transition: all 0.3s ease;
        }

        .nav-links a:hover {
            background: #667eea;
            color: white;
        }

        .subject-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .subject-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
            border-left: 5px solid #667eea;
        }

        .subject-card:hover {
            transform: translateY(-5px);
        }

        .subject-card h3 {
            color: #333;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }

        .subject-card p {
            color: #666;
            margin-bottom: 15px;
            line-height: 1.6;
        }

        .btn {
            background: #667eea;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            display: inline-block;
            font-weight: 600;
            transition: background 0.3s ease;
        }

        .btn:hover {
            background: #5a6fd8;
        }

        .quiz-section {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            margin-bottom: 30px;
        }

        .quiz-section h2 {
            color: #333;
            margin-bottom: 20px;
            text-align: center;
        }

        .quiz-container {
            max-width: 600px;
            margin: 0 auto;
        }

        .question {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .option {
            padding: 12px;
            background: white;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .option:hover {
            border-color: #667eea;
            background: #f8f9ff;
        }

        .option.selected {
            border-color: #667eea;
            background: #667eea;
            color: white;
        }

        .quiz-controls {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e9ecef;
            border-radius: 4px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress {
            height: 100%;
            background: #667eea;
            width: 0%;
            transition: width 0.3s ease;
        }

        .subject-category {
            margin: 30px 0 20px 0;
            color: white;
            font-size: 1.5rem;
            text-align: center;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .feature-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .feature-card h4 {
            color: #667eea;
            margin-bottom: 10px;
        }

        @media (max-width: 768px) {
            .nav-links {
                flex-direction: column;
                align-items: center;
            }
            
            .subject-grid {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header Section -->
        <div class="header">
            <h1>🏫 منصة العلوم - الفرقة الأولى</h1>
            <p>موقع تعليمي متكامل لطلاب كلية العلوم - مواد السنة الأولى</p>
        </div>

        <!-- Navigation -->
        <nav class="nav">
            <ul class="nav-links">
                <li><a href="#biology">المواد البيولوجية</a></li>
                <li><a href="#math">المواد الرياضية</a></li>
                <li><a href="#other">مواد أخرى</a></li>
                <li><a href="#quizzes">الاختبارات</a></li>
                <li><a href="#features">المميزات</a></li>
            </ul>
        </nav>

        <!-- Features Section -->
        <div class="features-grid" id="features">
            <div class="feature-card">
                <h4>📚 محاضرات شاملة</h4>
                <p>شرح مفصل لجميع المواد مع أمثلة عملية</p>
            </div>
            <div class="feature-card">
                <h4>🎯 اختبارات تفاعلية</h4>
                <p>تقيم مستواك الفوري مع تحليل النتائج</p>
            </div>
            <div class="feature-card">
                <h4>📊 تتبع التقدم</h4>
                <p>مراقبة تطورك الدراسي بشكل مستمر</p>
            </div>
            <div class="feature-card">
                <h4>💬 منتدى النقاش</h4>
                <p>تفاعل مع الزملاء والأساتذة</p>
            </div>
        </div>

        <!-- Biology Subjects -->
        <h3 class="subject-category" id="biology">🔬 المواد البيولوجية</h3>
        <div class="subject-grid">
            <div class="subject-card">
                <h3>علم الخلية (Cytology)</h3>
                <p>دراسة تركيب ووظائف الخلية الحية ومكوناتها الأساسية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>الفسيولوجي (Physiology)</h3>
                <p>دراسة الوظائف الحيوية لأعضاء الكائنات الحية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>علم الأنسجة (Histology)</h3>
                <p>دراسة الأنسجة الحيوية وتركيبها المجهري</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>علم الأجنة (Embryology)</h3>
                <p>تطور الجنين من الإخصاب حتى الولادة</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>علم التشكل (Morphology)</h3>
                <p>دراسة الشكل والتركيب الخارجي للكائنات الحية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>النبات (Plant Kingdom)</h3>
                <p>تصنيف ودراسة مملكة النباتات بأنواعها</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
        </div>

        <!-- Math Subjects -->
        <h3 class="subject-category" id="math">📐 المواد الرياضية</h3>
        <div class="subject-grid">
            <div class="subject-card">
                <h3>التفاضل (Differential)</h3>
                <p>دراسة معدلات التغير والاشتقاقات الرياضية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>التكامل (Integration)</h3>
                <p>دراسة المساحات والحجوم والتكاملات</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
        </div>

        <!-- Other Subjects -->
        <h3 class="subject-category" id="other">⚗ مواد أخرى</h3>
        <div class="subject-grid">
            <div class="subject-card">
                <h3>الفيزياء (Physics)</h3>
                <p>المبادئ الأساسية للفيزياء والتطبيقات العملية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>الكيمياء (Chemistry)</h3>
                <p>المركبات والتفاعلات الكيميائية الأساسية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>تكنولوجيا المعلومات (IT)</h3>
                <p>أساسيات الحاسب الآلي وتطبيقاته العلمية</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
            
            <div class="subject-card">
                <h3>حقوق الإنسان (Human Rights)</h3>
                <p>المبادئ الأساسية لحقوق الإنسان والتشريعات</p>
                <a href="#" class="btn">بدء التعلم</a>
            </div>
        </div>

        <!-- Quiz Section -->
        <div class="quiz-section" id="quizzes">
            <h2>🎯 اختبار تفاعلي - علم الخلية</h2>
            <div class="quiz-container">
                <div class="progress-bar">
                    <div class="progress" id="quizProgress"></div>
                </div>
                
                <div class="question">
                    <h4 id="questionText">ما هي العضية المسؤولة عن إنتاج الطاقة في الخلية؟</h4>
                </div>
                
                <div class="options" id="optionsContainer">
                    <!-- Options will be filled by JavaScript -->
                </div>
                
                <div class="quiz-controls">
                    <button class="btn" onclick="previousQuestion()">السابق</button>
                    <button class="btn" onclick="nextQuestion()">التالي</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Quiz Data
        const quizData = [
            {
                question: "ما هي العضية المسؤولة عن إنتاج الطاقة في الخلية؟",
                options: ["النواة", "الميتوكوندريا", "الشبكة الإندوبلازمية", "الريبوسوم"],
                correct: 1
            },
            {
                question: "أي من الآتي يعد وظيفة للجدار الخلوي في الخلية النباتية؟",
                options: [
                    "التحكم في دخول وخروج المواد",
                    "توفير الدعم الهيكلي",
                    "تصنيع البروتينات",
                    "تخزين المعلومات الوراثية"
                ],
                correct: 1
            },
            {
                question: "في أي جزء من الخلية يتم تخزين المعلومات الوراثية؟",
                options: ["الميتوكوندريا", "النواة", "البلاستيدات الخضراء", "جهاز جولجي"],
                correct: 1
            }
        ];

        let currentQuestion = 0;
        let selectedOption = null;

        function initializeQuiz() {
            showQuestion();
            updateProgress();
        }

        function showQuestion() {
            const question = quizData[currentQuestion];
            document.getElementById('questionText').textContent = question.question;
            
            const optionsContainer = document.getElementById('optionsContainer');
            optionsContainer.innerHTML = '';
            
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.className = 'option';
                optionElement.textContent = option;
                optionElement.onclick = () => selectOption(index);
                optionsContainer.appendChild(optionElement);
            });
            
            selectedOption = null;
        }

        function selectOption(index) {
            // Remove selected class from all options
            document.querySelectorAll('.option').forEach(opt => {
                opt.classList.remove('selected');
            });
            
            // Add selected class to clicked option
            document.querySelectorAll('.option')[index].classList.add('selected');
            selectedOption = index;
        }

        function nextQuestion() {
            if (currentQuestion < quizData.length - 1) {
                currentQuestion++;
                showQuestion();
                updateProgress();
            } else {
                alert('🎉 انتهى الاختبار! شكراً للمشاركة');
            }
        }

        function previousQuestion() {
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion();
                updateProgress();
            }
        }

        function updateProgress() {
            const progress = ((currentQuestion + 1) / quizData.length) * 100;
            document.getElementById('quizProgress').style.width = progress + '%';
        }

        // Initialize the quiz when page loads
        document.addEventListener('DOMContentLoaded', initializeQuiz);

        // Smooth scroll for navigation links
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    targetElement.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>
