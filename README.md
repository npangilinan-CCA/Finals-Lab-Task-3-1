<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Finals Lab Task 3-1 - Using MYSQL Clause</title>
    <link href="https://fonts.googleapis.com/css2?family=UnifrakturCook:wght@700&family=Playfair+Display:wght@500;700&display=swap" rel="stylesheet">
    <style>
        /* Custom Cursor */
        * {
            cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7,2 L17,12 L7,22 L7,2" fill="silver" stroke="white" stroke-width="1"/><text x="14" y="14" fill="white" font-size="8">♱</text></svg>') 7 12, auto;
        }

        /* Hover Cursor */
        a:hover, button:hover, .logo:hover, .frame-corner:hover, ul li:hover {
            cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7,2 L17,12 L7,22 L7,2" fill="white" stroke="silver" stroke-width="1"/><text x="14" y="14" fill="silver" font-size="8">♱</text></svg>') 7 12, pointer;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 12px;
            background: #000;
        }

        ::-webkit-scrollbar-track {
            background: linear-gradient(90deg, #000, #111);
            border: 1px solid rgba(192, 192, 192, 0.2);
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(45deg, #333, #666);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 6px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(45deg, #444, #777);
        }

        /* Root Variables */
        :root {
            --chrome-black: #000000;
            --chrome-silver: #C0C0C0;
            --chrome-white: #FFFFFF;
            --cross-pink: rgba(255, 182, 193, 0.8);
            --cross-blue: rgba(65, 105, 225, 0.8);
            --cross-yellow: rgba(255, 215, 0, 0.8);
            --cross-red: rgba(255, 99, 71, 0.8);
            --cross-green: rgba(144, 238, 144, 0.8);
        }

        body {
            margin: 0;
            padding: 2rem;
            font-family: 'Playfair Display', serif;
            color: white;
            background: black;
            line-height: 1.6;
            font-size: 18px;
            overflow-x: hidden;
        }

        /* Enhanced Title Styles */
        .title-container {
            position: relative;
            text-align: center;
            margin-bottom: 3rem;
            padding: 2rem;
            perspective: 1000px;
        }

        .main-title, .subtitle {
            font-family: 'UnifrakturCook', cursive;
            text-align: center;
            background: linear-gradient(45deg, 
                var(--cross-green), var(--cross-yellow), var(--cross-red),
                var(--cross-blue), var(--cross-pink)
            ) !important;
            background-size: 300% 300% !important;
            -webkit-background-clip: text !important;
            background-clip: text !important;
            -webkit-text-fill-color: transparent !important;
            transition: all 0.3s ease;
            padding: 1rem !important;
            margin: 0 !important;
            cursor: pointer;
            position: relative;
            animation: colorShift 10s infinite;
            text-shadow: 
                0 0 10px rgba(255,255,255,0.2),
                0 0 20px rgba(255,255,255,0.1),
                0 0 30px rgba(255,255,255,0.1);
        }

        .main-title {
            font-size: 3.5rem;
            letter-spacing: 2px;
        }

        .subtitle {
            font-size: 2rem;
            margin-top: 1rem;
        }

        /* Enhanced Loading Screen */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: black;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease-out;
        }

        .loading-content {
            text-align: center;
            position: relative;
        }

        .loading-content::before,
        .loading-content::after {
            content: '♱';
            position: absolute;
            font-size: 2rem;
            color: var(--chrome-silver);
            animation: rotateCross 4s linear infinite;
        }

        .loading-content::before {
            left: -50px;
            animation-delay: -2s;
        }

        .loading-content::after {
            right: -50px;
            animation-delay: -1s;
        }

        .loading-logo {
            font-family: 'UnifrakturCook', cursive;
            font-size: 4rem;
            margin-bottom: 2rem;
            background: linear-gradient(145deg, 
                #e0e0e0, #aaa, #f5f5f5, #888,
                #e0e0e0, #aaa, #f5f5f5, #888
            );
            background-size: 200% 200%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: loadingColorCycle 3s infinite;
            text-shadow: 
                0 0 20px rgba(255,255,255,0.2),
                0 0 40px rgba(255,255,255,0.1);
        }

        .loading-cross {
            font-size: 3rem;
            margin: 2rem 0;
            animation: loadingSpin 2s infinite linear;
            color: var(--chrome-silver);
            text-shadow: 0 0 10px var(--chrome-silver);
        }

        .loading-bar-container {
            width: 300px;
            height: 3px;
            background: rgba(192, 192, 192, 0.1);
            margin: 2rem auto;
            position: relative;
            overflow: hidden;
            border-radius: 2px;
            box-shadow: 0 0 10px rgba(0,0,0,0.5);
        }

        .loading-bar {
            position: absolute;
            top: 0;
            left: 0;
            height: 100%;
            width: 0%;
            background: linear-gradient(
                90deg,
                var(--chrome-silver),
                var(--chrome-white),
                var(--chrome-silver)
            );
            animation: loadingProgress 2s ease-out forwards;
            box-shadow: 0 0 15px var(--chrome-silver);
        }

        .loading-text {
            font-family: 'Playfair Display', serif;
            color: var(--chrome-silver);
            font-size: 1.2rem;
            letter-spacing: 5px;
            margin-top: 1rem;
            opacity: 0.8;
            animation: pulse 1.5s infinite;
        }
                /* Enhanced Section Styles */
        .section {
            margin: 3rem 0;
            padding: 2rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--chrome-silver);
            border-radius: 8px;
            transition: all 0.3s ease;
        }

        .section:hover {
            background: rgba(255, 255, 255, 0.08);
            box-shadow: 
                0 0 20px rgba(192, 192, 192, 0.2),
                0 0 40px rgba(192, 192, 192, 0.1);
        }

        .section-title {
            font-family: 'UnifrakturCook', cursive;
            font-size: 2.4rem;
            background: linear-gradient(45deg, 
                var(--cross-green), var(--cross-yellow), var(--cross-red),
                var(--cross-blue), var(--cross-pink)
            );
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            background-size: 300% 300%;
            animation: colorShift 10s infinite;
            margin: 2rem 0;
            padding-bottom: 0.8rem;
            border-bottom: 2px solid var(--chrome-silver);
        }

        .subsection-title {
            font-family: 'UnifrakturCook', cursive;
            font-size: 2rem;
            color: var(--chrome-silver);
            margin: 1.5rem 0;
            transition: all 0.3s ease;
        }

        /* Enhanced List Styles */
        ul, ol {
            list-style: none;
            padding-left: 1rem;
        }

        li {
            margin: 0.8rem 0;
            transition: all 0.3s ease;
            position: relative;
            padding-left: 25px;
        }

        li::before {
            content: '♱';
            position: absolute;
            left: 0;
            animation: colorShift 10s infinite;
            background: linear-gradient(45deg, 
                var(--cross-green), var(--cross-yellow), var(--cross-red),
                var(--cross-blue), var(--cross-pink)
            );
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            background-size: 300% 300%;
        }

        li:hover {
            transform: translateX(15px);
            background: linear-gradient(45deg, 
                rgba(144, 238, 144, 0.1),
                rgba(255, 215, 0, 0.1),
                rgba(255, 99, 71, 0.1),
                rgba(65, 105, 225, 0.1),
                rgba(255, 182, 193, 0.1)
            );
            background-size: 300% 300%;
            animation: colorShift 10s infinite;
            border-radius: 5px;
            padding: 10px 20px;
        }

        /* Enhanced Image Container */
        .image-container {
            margin: 2rem 0;
            position: relative;
        }

        .chrome-frame {
            position: relative;
            padding: 1.5rem;
            background: rgba(0, 0, 0, 0.9);
            border: 2px solid var(--chrome-silver);
            transition: all 0.4s ease;
        }

        .chrome-frame:hover {
            transform: scale(1.02);
            border-color: transparent;
            background: linear-gradient(45deg,
                var(--cross-green), var(--cross-yellow), var(--cross-red),
                var(--cross-blue), var(--cross-pink)
            );
            background-size: 300% 300%;
            animation: colorShift 10s infinite;
        }

        .chrome-frame img {
            width: 100%;
            height: auto;
            display: block;
            border: 1px solid rgba(255, 255, 255, 0.3);
            transition: all 0.4s ease;
        }

        /* Animations */
        @keyframes colorShift {
            0% {
                background-position: 0% 50%;
                filter: hue-rotate(0deg);
            }
            25% {
                background-position: 100% 50%;
                filter: hue-rotate(90deg);
            }
            50% {
                background-position: 50% 100%;
                filter: hue-rotate(180deg);
            }
            75% {
                background-position: 50% 0%;
                filter: hue-rotate(270deg);
            }
            100% {
                background-position: 0% 50%;
                filter: hue-rotate(360deg);
            }
        }

        @keyframes rotateCross {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes loadingSpin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        @keyframes loadingColorCycle {
            0% { background-position: 0% 50%; filter: hue-rotate(0deg); }
            50% { background-position: 100% 50%; filter: hue-rotate(180deg); }
            100% { background-position: 0% 50%; filter: hue-rotate(360deg); }
        }

        @keyframes loadingProgress {
            0% { width: 0%; }
            100% { width: 100%; }
        }

        @keyframes pulse {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 1; }
        }

        /* Container Styles */
        .container {
            max-width: 1200px;
            margin: auto;
            background: rgba(0, 0, 0, 0.7);
            padding: 40px;
            border: 2px solid var(--chrome-silver);
            box-shadow: 0 0 20px rgba(192, 192, 192, 0.3);
            position: relative;
            backdrop-filter: blur(5px);
            opacity: 0;
            transition: opacity 1s ease-in;
        }

        .container.loaded {
            opacity: 1;
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading-screen" id="loadingScreen">
        <div class="loading-content">
            <div class="loading-logo">Loading</div>
            <div class="loading-cross">♱</div>
            <div class="loading-bar-container">
                <div class="loading-bar"></div>
            </div>
            <div class="loading-text">LOADING...</div>
        </div>
    </div>

    <div class="container">
        <div class="title-container">
            <div class="main-title">Finals Lab Task 3-1</div>
            <div class="subtitle">Using MYSQL Clause</div>
        </div>

        <div class="section">
            <p class="description">
                This portfolio is a demonstration of applying MySQL clauses to solve common database query tasks. It showcases the use of SELECT, WHERE, GROUP BY, SUM, and ORDER BY statements to retrieve, group, filter, and sort data from a table of online courses. Each query addresses a specific scenario, such as identifying under-enrolled or fully enrolled courses, calculating total student enrollments by category and overall, and ordering data based on enrollment numbers.
            </p>

            <h2 class="section-title">Step by Step Process</h2>
            
            <h3 class="subsection-title">1.  Create a database named online course_DB</h3>
            
            <h3 class="subsection-title">2.  Copy and paste the initial query provided in the google classroom</h3>
            
            <h3 class="subsection-title">3. Retrieve all courses where students enrolled is less than the enrollment_limit</h3>
            <ul>
                <li>Use select and from statement to choose the courses table.</li>
                <li>Use where statement to choose the following values from courses table (students_enrolled and enrollment limit) and adding the '>' conditional statement to complete the process.</li>
            </ul>

            <h3 class="subsection-title"> 4. Group courses by category and calculate the total number of students enrolled for each category</h3>
            <ul>
                <li>Use the select statement to choose the category from the courses table.</li>
                <li>Use the sum statement to calculate the sum of  of students_enrolled followed by the as statement to give it an alias as total_students_enrolled.</li>
                <li>Use the group by statement to group the sum of students_enrolled within each group by category.</li>
            </ul>

            <h3 class="subsection-title">5. Retrieve the courses that are fully enrolled</h3>
            <ul>
                <li>Use the select statement followed by the from statement to choose the courses table.</li>
                <li>Use the where statement followed by inserting the values students_enrolled and enrollment_limit with the conditional statement '=' in between to filter courses that does not follow the condition.</li>
            </ul>
            
            <h3 class="subsection-title">6. Calculate the total number of students enrolled across all courses</h3>
            <ul>
                <li>Use the select statement to choose the students enrolled with the sum statement to calculate the sum.</li>
                <li>Use the as statement on student_enrolled to give it an alias as total_students_all_courses.</li>
                <li>Use the from statement to choose courses table.</li>
            </ul>
            
            <h3 class="subsection-title">Task 7. Sort courses by students_enrolled in ascending order</h3>
            <ul>
                <li>Use the select statement followed by from statement to choose the courses table.</li>
                <li>Use the order by statement followed by the asc statement to arrange the students_enrolled in ascending order.</li>
            </ul>
        </div>

        <div class="section">
            <h2 class="section-title">Query Statements and Table Structures</h2>
            
            <h3 class="subsection-title">Task 1</h3>
            <div class="image-container">
                <div class="chrome-frame">
                    <img src="https://github.com/user-attachments/assets/a9a0d529-6d6d-4e96-9995-45feeac7a11e" alt="Task 1">
                </div>
            </div>

            <h3 class="subsection-title">Task 2</h3>
            <div class="image-container">
                <div class="chrome-frame">
                    <img src="https://github.com/user-attachments/assets/78cd984f-0b47-4646-8ff8-2cdec6d6c6e0" alt="Task 2">
                </div>
            </div>

            <h3 class="subsection-title">Task 3</h3>
            <div class="image-container">
                <div class="chrome-frame">
                    <img src="https://github.com/user-attachments/assets/584bf376-b472-46bb-939a-dd0c33e27beb" alt="Task 3">
                </div>
            </div>

            <h3 class="subsection-title">Task 4</h3>
            <div class="image-container">
                <div class="chrome-frame">
                    <img src="https://github.com/user-attachments/assets/47f7b5f5-023b-4ce0-87a0-8596b55be6ed" alt="Task 4">
                </div>
            </div>
        </div>

        <div class="section">
            <h2 class="section-title">Task 5</h2>
            <div class="image-container">
                <div class="chrome-frame">
                    <img src="https://github.com/user-attachments/assets/acb78e5b-903d-4490-a2df-33dc89bfde62" alt="Task 5">
                </div>
            </div>
        </div>
    </div>

    <script>
        // Loading screen handler
        document.addEventListener('DOMContentLoaded', () => {
            const loadingScreen = document.getElementById('loadingScreen');
            const container = document.querySelector('.container');
            
            setTimeout(() => {
                loadingScreen.style.opacity = '0';
                container.classList.add('loaded');
                
                setTimeout(() => {
                    loadingScreen.style.display = 'none';
                }, 500);
            }, 2000);
        });

        // Enhanced title interaction with color shift
        document.querySelector('.title-container').addEventListener('mousemove', (e) => {
            const title = document.querySelector('.main-title');
            const subtitle = document.querySelector('.subtitle');
            const rect = e.currentTarget.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            const centerX = rect.width / 2;
            const centerY = rect.height / 2;
            
            const angleX = (y - centerY) / 20;
            const angleY = (centerX - x) / 20;
            
            const hueRotate = ((x / rect.width) * 360);
            
            title.style.transform = `perspective(1000px) rotateX(${angleX}deg) rotateY(${angleY}deg) scale(1.1)`;
            subtitle.style.transform = `perspective(1000px) rotateX(${angleX}deg) rotateY(${angleY}deg) scale(1.05)`;
            
            title.style.filter = `hue-rotate(${hueRotate}deg) brightness(1.2)`;
            subtitle.style.filter = `hue-rotate(${hueRotate}deg) brightness(1.2)`;
        });

        document.querySelector('.title-container').addEventListener('mouseleave', () => {
            const title = document.querySelector('.main-title');
            const subtitle = document.querySelector('.subtitle');
            title.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale(1)';
            subtitle.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale(1)';
            title.style.filter = '';
            subtitle.style.filter = '';
        });

        // Add interactive color effect to list items
        document.querySelectorAll('li').forEach(item => {
            item.addEventListener('mouseenter', function() {
                this.style.animation = 'colorShift 5s infinite';
            });

            item.addEventListener('mouseleave', function() {
                this.style.animation = '';
            });
        });
    </script>
</body>
</html>
