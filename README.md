<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>室內設計風格測驗</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #f5f1eb 0%, #f0e8d8 100%);
            min-height: 100vh;
            color: #8b7355;
            line-height: 1.6;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }

        .welcome-screen {
            text-align: center;
            padding: 60px 20px;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(139, 115, 85, 0.1);
            backdrop-filter: blur(10px);
        }

        .welcome-screen h1 {
            font-size: 2.5em;
            color: #8b7355;
            margin-bottom: 20px;
            font-weight: 300;
        }

        .welcome-screen p {
            font-size: 1.2em;
            margin-bottom: 30px;
            color: #a68b5b;
        }

        .ig-follow {
            background: linear-gradient(45deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            margin-bottom: 20px;
            text-decoration: none;
            display: inline-block;
        }

        .ig-follow:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(139, 115, 85, 0.2);
        }

        .start-btn {
            background: #c4a484;
            color: white;
            padding: 15px 40px;
            border: none;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            opacity: 0.5;
            pointer-events: none;
        }

        .start-btn.active {
            opacity: 1;
            pointer-events: auto;
        }

        .start-btn.active:hover {
            background: #b8966f;
            transform: translateY(-2px);
        }

        .quiz-container {
            display: none;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 15px 40px rgba(139, 115, 85, 0.1);
            backdrop-filter: blur(10px);
        }

        .progress-bar {
            background: #e8ddd0;
            height: 6px;
            border-radius: 3px;
            margin-bottom: 30px;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(90deg, #c4a484, #d4b896);
            height: 100%;
            transition: width 0.5s ease;
            border-radius: 3px;
        }

        .question {
            margin-bottom: 30px;
        }

        .question h3 {
            font-size: 1.4em;
            color: #8b7355;
            margin-bottom: 25px;
            font-weight: 400;
        }

        .options {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
        }

        .option {
            background: rgba(255, 255, 255, 0.7);
            border: 2px solid #e8ddd0;
            border-radius: 12px;
            padding: 15px 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.95em;
        }

        .option:hover {
            background: rgba(196, 164, 132, 0.1);
            border-color: #c4a484;
            transform: translateY(-2px);
        }

        .option.selected {
            background: rgba(196, 164, 132, 0.2);
            border-color: #c4a484;
            color: #8b7355;
        }

        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 40px;
        }

        .nav-btn {
            background: #c4a484;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s ease;
        }

        .nav-btn:hover {
            background: #b8966f;
            transform: translateY(-2px);
        }

        .nav-btn:disabled {
            background: #d4c2a8;
            cursor: not-allowed;
            transform: none;
        }

        .result-screen {
            display: none;
            text-align: center;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 15px 40px rgba(139, 115, 85, 0.1);
        }

        .result-image {
            width: 300px;
            height: 200px;
            object-fit: cover;
            border-radius: 15px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(139, 115, 85, 0.2);
        }

        .result-image-placeholder {
            width: 300px;
            height: 200px;
            background: transparent;
            border-radius: 15px;
            margin: 20px 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .result-icon {
            font-size: 4em;
            margin-bottom: 10px;
        }

        .result-style-text {
            font-size: 1.2em;
            color: #8b7355;
            font-weight: 500;
        }

        .image-link {
            display: inline-block;
            background: #c4a484;
            color: white;
            padding: 10px 20px;
            border-radius: 20px;
            text-decoration: none;
            margin: 10px 0;
            transition: all 0.3s ease;
        }

        .image-link:hover {
            background: #b8966f;
            transform: translateY(-2px);
        }

        .result-title {
            font-size: 2.2em;
            color: #8b7355;
            margin-bottom: 15px;
            font-weight: 300;
        }

        .result-description {
            font-size: 1.1em;
            color: #a68b5b;
            margin-bottom: 30px;
            line-height: 1.8;
        }

        .restart-btn {
            background: #c4a484;
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 20px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .restart-btn:hover {
            background: #b8966f;
            transform: translateY(-2px);
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .welcome-screen, .quiz-container, .result-screen {
                padding: 30px 20px;
            }
            
            .welcome-screen h1 {
                font-size: 2em;
            }
            
            .result-image-placeholder {
                width: 250px;
                height: 160px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 歡迎畫面 -->
        <div class="welcome-screen" id="welcomeScreen">
            <h1>測完想立刻重裝潢!10題找出你的命定設計風格🏡✨</h1>
            <p>透過10個問題，發現最適合你的室內設計風格</p>
            <p>請先追蹤我們的Instagram，即可開始免費測驗</p>
            <a href="https://www.instagram.com/gui.special.one" target="_blank" class="ig-follow" id="igFollow">
                📸 追蹤 @gui.special.one
            </a>
            <br><br>
            <button class="start-btn" id="startBtn">開始測驗</button>
        </div>

        <!-- 測驗畫面 -->
        <div class="quiz-container" id="quizContainer">
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
            
            <div class="question" id="questionContainer">
                <!-- 問題會動態載入 -->
            </div>
            
            <div class="nav-buttons">
                <button class="nav-btn" id="prevBtn">上一題</button>
                <button class="nav-btn" id="nextBtn">下一題</button>
            </div>
        </div>

        <!-- 結果畫面 -->
        <div class="result-screen" id="resultScreen">
            <h2 class="result-title" id="resultTitle"></h2>
            <div class="result-image-placeholder" id="resultImagePlaceholder">
                <div class="result-icon" id="resultIcon"></div>
                <div class="result-style-text" id="resultStyleText"></div>
            </div>
            <a class="image-link" id="imageLink" target="_blank">📸 點擊查看風格圖片</a>
            <p class="result-description" id="resultDescription"></p>
            <button class="restart-btn" id="restartBtn">重新測驗</button>
        </div>
    </div>

    <script>
        // 問題數據
        const questions = [
            {
                question: "你偏好的牆面材質或塗裝是？",
                options: [
                    { text: "奶油色乳膠漆，溫潤質感", style: "creamy" },
                    { text: "全白＋霧面塗料，俐落純粹", style: "modern" },
                    { text: "微水泥或木質牆板，自然感強", style: "nordic" },
                    { text: "線板造型牆＋中性色塗裝", style: "french" },
                    { text: "仿舊木皮＋壁燈或壁畫點綴", style: "midcentury" },
                    { text: "義大利灰、米灰大理石面材", style: "italian" },
                    { text: "土色礦物塗料＋灰泥牆", style: "wabisabi" },
                    { text: "色塊幾何圖案或彩色磁磚牆", style: "bauhaus" }
                ]
            },
            {
                question: "如果要鋪設地板，你會選擇？",
                options: [
                    { text: "淺奶茶色 SPC / 木地板", style: "creamy" },
                    { text: "霧灰或無接縫地坪", style: "modern" },
                    { text: "自然木紋＋裸感觸感面", style: "nordic" },
                    { text: "原木色橡木＋人字拼或框線感", style: "french" },
                    { text: "仿舊橡木 / 實木復古色", style: "midcentury" },
                    { text: "石材拼接地坪＋隱藏踢腳線", style: "italian" },
                    { text: "榻榻米＋低飽和木地板", style: "wabisabi" },
                    { text: "黑白格子、拼接跳色地毯", style: "bauhaus" }
                ]
            },
            {
                question: "你最喜歡的沙發樣式是？",
                options: [
                    { text: "圓潤軟墊、奶白色、低椅背", style: "creamy" },
                    { text: "直線條、模組化收納型", style: "modern" },
                    { text: "淺色布沙發＋實木底座", style: "nordic" },
                    { text: "有雕花腿或古典扶手設計", style: "french" },
                    { text: "絨面復古色系＋弧形造型", style: "midcentury" },
                    { text: "義式高背＋皮革／卡其灰布面", style: "italian" },
                    { text: "麻布＋厚實坐墊、無明顯裝飾", style: "wabisabi" },
                    { text: "拼接撞色、管狀結構、特殊比例", style: "bauhaus" }
                ]
            },
            {
                question: "空間中的燈光配置，你偏好？",
                options: [
                    { text: "間接光源＋溫暖色溫燈泡", style: "creamy" },
                    { text: "軌道燈＋崁燈，明確照明功能", style: "modern" },
                    { text: "桌燈＋自然採光，簡單不過曝", style: "nordic" },
                    { text: "水晶燈／吊燈為主體，重氛圍", style: "french" },
                    { text: "球狀燈、造型燈飾＋黃光", style: "midcentury" },
                    { text: "藏燈光源＋洗牆＋照射燈帶", style: "italian" },
                    { text: "陶土燈罩、原木吊燈，自然柔和", style: "wabisabi" },
                    { text: "幾何／異材質造型燈具，強視覺感", style: "bauhaus" }
                ]
            },
            {
                question: "你傾向的收納設計是？",
                options: [
                    { text: "隱藏式＋整體奶油色櫃面", style: "creamy" },
                    { text: "全平面立櫃＋無把手設計", style: "modern" },
                    { text: "局部開放層板＋木盒／藤編籃", style: "nordic" },
                    { text: "展示＋收納混搭，有對稱感", style: "french" },
                    { text: "收納櫃結合書桌或展示櫃，有老件混搭", style: "midcentury" },
                    { text: "薄型立面收納＋高低差配置", style: "italian" },
                    { text: "地台＋層架＋簡化儲物", style: "wabisabi" },
                    { text: "暗櫃＋開放＋造型突顯，兼具設計", style: "bauhaus" }
                ]
            },
            {
                question: "在空間色彩中你偏好的基底色是？",
                options: [
                    { text: "奶油白、杏色、米卡其", style: "creamy" },
                    { text: "黑、灰、白三原無彩色", style: "modern" },
                    { text: "淺木色＋淺灰＋自然白", style: "nordic" },
                    { text: "米白、米黃＋深木混搭", style: "french" },
                    { text: "焦糖、深綠、木橘、白灰", style: "midcentury" },
                    { text: "深灰、岩白、大地米金色", style: "italian" },
                    { text: "土灰、裸膚、木質棕", style: "wabisabi" },
                    { text: "藍、黃、磚紅、綠、黑白撞色", style: "bauhaus" }
                ]
            },
            {
                question: "你最欣賞的空間動線設計是？",
                options: [
                    { text: "開放式連貫但不失區隔感", style: "creamy" },
                    { text: "分區明確、走線精準有系統", style: "modern" },
                    { text: "流動自由、貼近生活節奏", style: "nordic" },
                    { text: "視覺對稱、有明確進場路線", style: "french" },
                    { text: "中心混搭、展現生活感", style: "midcentury" },
                    { text: "與建築比例一體設計、轉折利落", style: "italian" },
                    { text: "少動線、多留白、保有靜感", style: "wabisabi" },
                    { text: "趣味不規則，動線像展覽空間", style: "bauhaus" }
                ]
            },
            {
                question: "家具風格你最喜歡哪種特質？",
                options: [
                    { text: "柔軟圓潤、包覆感強", style: "creamy" },
                    { text: "機能強、極簡直線、無裝飾", style: "modern" },
                    { text: "手作感、自然紋理、簡潔實用", style: "nordic" },
                    { text: "古典混現代、有雕刻細節", style: "french" },
                    { text: "復古比例＋金屬或木混搭", style: "midcentury" },
                    { text: "高級訂製感、比例細膩", style: "italian" },
                    { text: "簡素、偏原始、自然手感", style: "wabisabi" },
                    { text: "強烈造型＋色彩存在感", style: "bauhaus" }
                ]
            },
            {
                question: "如果放藝術品或擺飾，你會選？",
                options: [
                    { text: "溫潤陶器、奶白造型燭台", style: "creamy" },
                    { text: "黑白線條畫、霧灰雕塑品", style: "modern" },
                    { text: "花瓶、木藝品、小型植栽", style: "nordic" },
                    { text: "古典雕像、金屬邊框畫作", style: "french" },
                    { text: "復古書、雕花鏡、老件相框", style: "midcentury" },
                    { text: "義式玻璃花器、異材搭配", style: "italian" },
                    { text: "石材、乾燥花枝、原陶", style: "wabisabi" },
                    { text: "拼貼畫、色塊畫、復古玩具", style: "bauhaus" }
                ]
            },
            {
                question: "如果只能留下一項設計元素，你最捨不得的是？",
                options: [
                    { text: "柔和的燈光氛圍", style: "creamy" },
                    { text: "系統化的櫃體收納", style: "modern" },
                    { text: "木材與自然紋理材質", style: "nordic" },
                    { text: "儀式感的吊燈與壁線細節", style: "french" },
                    { text: "特殊比例的家具造型", style: "midcentury" },
                    { text: "高級石材與隱藏設計", style: "italian" },
                    { text: "手感材質與留白空間", style: "wabisabi" },
                    { text: "色彩與結構的趣味搭配", style: "bauhaus" }
                ]
            }
        ];

        // 風格資訊
        const styles = {
            creamy: {
                name: "奶油風 Creamy Style",
                image: "https://postimg.cc/8sRR3t89",
                icon: "🏡",
                description: "您適合溫潤如奶油般的居家風格！偏好柔和色調與圓潤線條，注重舒適與放鬆的氛圍。這種風格強調自然光線與溫暖色溫，創造出如擁抱般的居住感受。"
            },
            modern: {
                name: "現代簡約 Modern Minimal",
                image: "https://postimg.cc/w1KJ7ymK",
                icon: "🔳",
                description: "您偏愛極簡主義的現代風格！追求功能性與簡潔美學，喜歡乾淨的線條與中性色彩。這種風格強調空間的開闊感與物品的實用性，創造出井然有序的生活環境。"
            },
            nordic: {
                name: "北歐風 Nordic",
                image: "https://postimg.cc/6722fCG5",
                icon: "🌲",
                description: "您鍾情於北歐式的自然簡約！偏好天然材質與淺色調，追求與自然的連結。這種風格注重採光與通風，融合實用性與美感，營造出清新舒適的居住氛圍。"
            },
            french: {
                name: "輕法式 Light French",
                image: "https://postimg.cc/dD2YTDDM",
                icon: "🌸",
                description: "您適合優雅的法式風情！喜歡精緻的線條與古典元素，追求浪漫與典雅的氛圍。這種風格融合了傳統工藝與現代生活，創造出充滿魅力的居住空間。"
            },
            midcentury: {
                name: "中古奶油風 Mid-Century Creamy",
                image: "https://postimg.cc/m1ws0Z56",
                icon: "🎨",
                description: "您偏愛復古與現代的完美結合！喜歡中世紀的設計元素與溫暖色調，追求個性化的居住體驗。這種風格強調獨特的造型與質感，展現出時尚與懷舊的雙重魅力。"
            },
            italian: {
                name: "義式低奢風 Italian Quiet Luxury",
                image: "https://postimg.cc/sGDWFx2M",
                icon: "💎",
                description: "您追求低調奢華的義式風格！偏好高品質材質與精緻工藝，注重細節與質感。這種風格強調內斂的豪華感，透過優質材料與考究設計，創造出充滿品味的居住環境。"
            },
            wabisabi: {
                name: "侘寂風 Wabi-Sabi",
                image: "https://postimg.cc/crVLNC9r",
                icon: "🌿",
                description: "您欣賞日式的侘寂美學！偏好不完美中的完美，追求寧靜與簡樸的生活哲學。這種風格強調自然材質的原始美感，營造出禪意十足的居住空間。"
            },
            bauhaus: {
                name: "包浩斯風 Bauhaus",
                image: "https://postimg.cc/PLqXWDNV",
                icon: "🔺",
                description: "您鍾愛包浩斯的設計理念！追求功能與美學的完美結合，喜歡大膽的色彩與幾何造型。這種風格強調實用性與藝術性並重，創造出充滿創意與活力的居住環境。"
            }
        };

        // 洗牌函數
        function shuffleArray(array) {
            const shuffled = [...array];
            for (let i = shuffled.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
            }
            return shuffled;
        }

        // 為每個問題洗牌選項
        questions.forEach(question => {
            question.options = shuffleArray(question.options);
        });

        // 全域變數
        let currentQuestion = 0;
        let answers = [];
        let followedIG = false;

        // DOM 元素
        const welcomeScreen = document.getElementById('welcomeScreen');
        const quizContainer = document.getElementById('quizContainer');
        const resultScreen = document.getElementById('resultScreen');
        const igFollow = document.getElementById('igFollow');
        const startBtn = document.getElementById('startBtn');
        const questionContainer = document.getElementById('questionContainer');
        const progressFill = document.getElementById('progressFill');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const resultTitle = document.getElementById('resultTitle');
        const resultIcon = document.getElementById('resultIcon');
        const resultStyleText = document.getElementById('resultStyleText');
        const imageLink = document.getElementById('imageLink');
        const resultDescription = document.getElementById('resultDescription');
        const restartBtn = document.getElementById('restartBtn');

        // 事件監聽器
        igFollow.addEventListener('click', () => {
            followedIG = true;
            startBtn.classList.add('active');
        });

        startBtn.addEventListener('click', () => {
            if (followedIG) {
                startQuiz();
            }
        });

        prevBtn.addEventListener('click', () => {
            if (currentQuestion > 0) {
                currentQuestion--;
                displayQuestion();
            }
        });

        nextBtn.addEventListener('click', () => {
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                displayQuestion();
            } else {
                showResult();
            }
        });

        restartBtn.addEventListener('click', () => {
            resetQuiz();
        });

        // 開始測驗
        function startQuiz() {
            welcomeScreen.style.display = 'none';
            quizContainer.style.display = 'block';
            displayQuestion();
        }

        // 顯示問題
        function displayQuestion() {
            const question = questions[currentQuestion];
            
            questionContainer.innerHTML = `
                <h3>Q${currentQuestion + 1}. ${question.question}</h3>
                <div class="options">
                    ${question.options.map((option, index) => `
                        <div class="option ${answers[currentQuestion] === index ? 'selected' : ''}" 
                             onclick="selectOption(${index})">
                            ${String.fromCharCode(65 + index)}. ${option.text}
                        </div>
                    `).join('')}
                </div>
            `;

            // 更新進度條
            const progress = ((currentQuestion + 1) / questions.length) * 100;
            progressFill.style.width = progress + '%';

            // 更新按鈕狀態
            prevBtn.disabled = currentQuestion === 0;
            nextBtn.textContent = currentQuestion === questions.length - 1 ? '完成測驗' : '下一題';
            nextBtn.disabled = answers[currentQuestion] === undefined;
        }

        // 選擇選項
        function selectOption(optionIndex) {
            answers[currentQuestion] = optionIndex;
            displayQuestion();
        }

        // 顯示結果
        function showResult() {
            // 計算各風格分數
            const scores = {};
            Object.keys(styles).forEach(style => {
                scores[style] = 0;
            });

            questions.forEach((question, qIndex) => {
                const selectedOptionIndex = answers[qIndex];
                if (selectedOptionIndex !== undefined) {
                    const selectedOption = question.options[selectedOptionIndex];
                    scores[selectedOption.style]++;
                }
            });

            // 找出最高分的風格
            const maxScore = Math.max(...Object.values(scores));
            const topStyles = Object.keys(scores).filter(style => scores[style] === maxScore);
            const resultStyle = topStyles[Math.floor(Math.random() * topStyles.length)];

            // 顯示結果
            const styleInfo = styles[resultStyle];
            resultTitle.textContent = styleInfo.name;
            resultIcon.textContent = styleInfo.icon;
            resultStyleText.textContent = styleInfo.name;
            imageLink.href = styleInfo.image;
            resultDescription.textContent = styleInfo.description;

            quizContainer.style.display = 'none';
            resultScreen.style.display = 'block';
        }

        // 重置測驗
        function resetQuiz() {
            currentQuestion = 0;
            answers = [];
            followedIG = false;
            startBtn.classList.remove('active');
            
            resultScreen.style.display = 'none';
            welcomeScreen.style.display = 'block';
            
            // 重新洗牌所有問題的選項
            questions.forEach(question => {
                question.options = shuffleArray(question.options);
            });
        }

        // 初始化
        displayQuestion();
    </script>
</body>
</html>
