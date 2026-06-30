# xiaohuihui
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>智游 - 智能旅游规划平台</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Microsoft YaHei', Arial, sans-serif;
            line-height: 1.6;
            color: #333;
        }

        /* 导航栏 */
        .navbar {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 1rem 2rem;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: white;
            text-decoration: none;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            transition: opacity 0.3s;
        }

        .nav-links a:hover {
            opacity: 0.8;
        }

        /* 主横幅 */
        .hero {
            background: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), 
                        url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1920&q=80');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            height: 700px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            color: white;
            margin-top: 60px;
            position: relative;
        }

        .hero-content h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            animation: fadeInDown 1s ease-out;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .hero-content p {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
            animation: fadeInUp 1s ease-out 0.3s both;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* AI聊天窗口 */
        .chat-container {
            max-width: 900px;
            margin: 0 auto;
            animation: fadeInUp 1s ease-out 0.6s both;
        }

        .chat-window {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            overflow: hidden;
            height: 450px;
            display: flex;
            flex-direction: column;
        }

        .chat-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 1rem 1.5rem;
            display: flex;
            align-items: center;
            gap: 1rem;
            color: white;
        }

        .chat-avatar {
            width: 45px;
            height: 45px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        .chat-header-info h3 {
            font-size: 1.2rem;
            margin-bottom: 0.2rem;
        }

        .chat-header-info p {
            font-size: 0.85rem;
            opacity: 0.9;
        }

        .chat-messages {
            flex: 1;
            padding: 1.5rem;
            overflow-y: auto;
            background: #f8f9fa;
        }

        .message {
            margin-bottom: 1rem;
            display: flex;
            gap: 0.8rem;
            animation: messageSlide 0.3s ease-out;
        }

        @keyframes messageSlide {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message.user {
            flex-direction: row-reverse;
        }

        .message-avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            flex-shrink: 0;
        }

        .message.ai .message-avatar {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .message.user .message-avatar {
            background: #e0e0e0;
        }

        .message-content {
            max-width: 70%;
            padding: 0.8rem 1rem;
            border-radius: 15px;
            line-height: 1.5;
            font-size: 0.95rem;
        }

        .message.ai .message-content {
            background: white;
            color: #333;
            border-bottom-left-radius: 5px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .message.user .message-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-bottom-right-radius: 5px;
        }

        .chat-input-area {
            padding: 1rem 1.5rem;
            background: white;
            border-top: 1px solid #e0e0e0;
            display: flex;
            gap: 0.8rem;
        }

        .chat-input {
            flex: 1;
            padding: 0.8rem 1rem;
            border: 2px solid #e0e0e0;
            border-radius: 25px;
            font-size: 0.95rem;
            outline: none;
            transition: border-color 0.3s;
        }

        .chat-input:focus {
            border-color: #667eea;
        }

        .send-btn {
            width: 45px;
            height: 45px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border: none;
            border-radius: 50%;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .send-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }

        .typing-indicator {
            display: flex;
            gap: 0.3rem;
            padding: 0.5rem 0;
        }

        .typing-dot {
            width: 8px;
            height: 8px;
            background: #999;
            border-radius: 50%;
            animation: typing 1.4s infinite;
        }

        .typing-dot:nth-child(2) {
            animation-delay: 0.2s;
        }

        .typing-dot:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes typing {
            0%, 60%, 100% {
                transform: translateY(0);
            }
            30% {
                transform: translateY(-10px);
            }
        }

        /* 热门目的地 */
        .destinations {
            padding: 4rem 2rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 3rem;
            color: #333;
        }

        .destination-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .destination-card {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
        }

        .destination-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }

        .card-image {
            height: 200px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 3rem;
        }

        .card-content {
            padding: 1.5rem;
        }

        .card-content h3 {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
            color: #333;
        }

        .card-content p {
            color: #666;
            margin-bottom: 1rem;
        }

        .price-tag {
            color: #667eea;
            font-size: 1.3rem;
            font-weight: bold;
        }

        /* 行程规划工具 */
        .planner {
            background: #f7f9fc;
            padding: 4rem 2rem;
        }

        .planner-container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .planner-form {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: bold;
            color: #333;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid #e0e0e0;
            border-radius: 5px;
            font-size: 1rem;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
        }

        .submit-btn {
            width: 100%;
            padding: 1rem;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .submit-btn:hover {
            transform: translateY(-2px);
        }

        /* 特色服务 */
        .features {
            padding: 4rem 2rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .feature-card {
            text-align: center;
            padding: 2rem;
            border-radius: 10px;
            background: white;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }

        .feature-card:hover {
            transform: translateY(-5px);
        }

        .feature-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
        }

        .feature-card h3 {
            margin-bottom: 1rem;
            color: #333;
        }

        /* 页脚 */
        footer {
            background: #333;
            color: white;
            padding: 3rem 2rem 1rem;
        }

        .footer-content {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
        }

        .footer-section h3 {
            margin-bottom: 1rem;
            color: #667eea;
        }

        .footer-section ul {
            list-style: none;
        }

        .footer-section ul li {
            margin-bottom: 0.5rem;
        }

        .footer-section a {
            color: #ccc;
            text-decoration: none;
            transition: color 0.3s;
        }

        .footer-section a:hover {
            color: white;
        }

        .footer-bottom {
            text-align: center;
            margin-top: 2rem;
            padding-top: 2rem;
            border-top: 1px solid #555;
            color: #999;
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .hero-content h1 {
                font-size: 2rem;
            }

            .nav-links {
                display: none;
            }

            .search-form {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <!-- 导航栏 -->
    <nav class="navbar">
        <div class="nav-container">
            <a href="#" class="logo">🌍 智游</a>
            <ul class="nav-links">
                <li><a href="#home">首页</a></li>
                <li><a href="#destinations">目的地</a></li>
                <li><a href="#planner">行程规划</a></li>
                <li><a href="#features">特色服务</a></li>
                <li><a href="#contact">联系我们</a></li>
            </ul>
        </div>
    </nav>

    <!-- 主横幅 -->
    <section class="hero" id="home">
        <div class="hero-content">
            <h1>探索世界，从这里开始</h1>
            <p>智能规划您的完美旅程，让每一次旅行都成为美好回忆</p>
            
            <!-- AI聊天窗口 -->
            <div class="chat-container">
                <div class="chat-window">
                    <div class="chat-header">
                        <div class="chat-avatar">🤖</div>
                        <div class="chat-header-info">
                            <h3>智游AI助手</h3>
                            <p>在线 | 随时为您提供旅行建议</p>
                        </div>
                    </div>
                    
                    <div class="chat-messages" id="chatMessages">
                        <div class="message ai">
                            <div class="message-avatar">🤖</div>
                            <div class="message-content">
                                您好！我是智游AI助手，很高兴为您服务。😊<br><br>
                                我可以帮您：<br>
                                • 推荐旅游目的地<br>
                                • 规划旅行行程<br>
                                • 提供预算建议<br>
                                • 解答旅行相关问题<br><br>
                                请告诉我您的旅行需求吧！
                            </div>
                        </div>
                    </div>
                    
                    <div class="chat-input-area">
                        <input type="text" class="chat-input" id="chatInput" placeholder="输入您的问题...">
                        <button class="send-btn" id="sendBtn">➤</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 热门目的地 -->
    <section class="destinations" id="destinations">
        <h2 class="section-title">热门旅游目的地</h2>
        <div class="destination-grid">
            <div class="destination-card">
                <div class="card-image">🏔️</div>
                <div class="card-content">
                    <h3>云南大理</h3>
                    <p>苍山洱海，风花雪月，体验白族文化</p>
                    <div class="price-tag">¥2,999起</div>
                </div>
            </div>
            <div class="destination-card">
                <div class="card-image">🏖️</div>
                <div class="card-content">
                    <h3>海南三亚</h3>
                    <p>阳光沙滩，热带风情，度假天堂</p>
                    <div class="price-tag">¥3,599起</div>
                </div>
            </div>
            <div class="destination-card">
                <div class="card-image">🏯</div>
                <div class="card-content">
                    <h3>日本京都</h3>
                    <p>古都韵味，樱花盛开，禅意之旅</p>
                    <div class="price-tag">¥5,999起</div>
                </div>
            </div>
            <div class="destination-card">
                <div class="card-image">🗽</div>
                <div class="card-content">
                    <h3>法国巴黎</h3>
                    <p>浪漫之都，艺术殿堂，时尚中心</p>
                    <div class="price-tag">¥8,999起</div>
                </div>
            </div>
            <div class="destination-card">
                <div class="card-image">🦘</div>
                <div class="card-content">
                    <h3>澳大利亚悉尼</h3>
                    <p>海港城市，自然奇观，多元文化</p>
                    <div class="price-tag">¥7,599起</div>
                </div>
            </div>
            <div class="destination-card">
                <div class="card-image">🏝️</div>
                <div class="card-content">
                    <h3>马尔代夫</h3>
                    <p>碧海蓝天，水上别墅，蜜月圣地</p>
                    <div class="price-tag">¥12,999起</div>
                </div>
            </div>
        </div>
    </section>

    <!-- 行程规划工具 -->
    <section class="planner" id="planner">
        <div class="planner-container">
            <h2 class="section-title">智能行程规划</h2>
            <div class="planner-form">
                <form>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="destination">目的地</label>
                            <input type="text" id="destination" placeholder="输入您想去的城市或景点">
                        </div>
                        <div class="form-group">
                            <label for="days">旅行天数</label>
                            <select id="days">
                                <option value="1">1天</option>
                                <option value="2">2天</option>
                                <option value="3">3天</option>
                                <option value="5">5天</option>
                                <option value="7">7天</option>
                                <option value="10">10天以上</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="budget">预算范围</label>
                            <select id="budget">
                                <option value="low">经济型 (¥3000以下)</option>
                                <option value="medium">舒适型 (¥3000-8000)</option>
                                <option value="high">豪华型 (¥8000以上)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="travelers">出行人数</label>
                            <select id="travelers">
                                <option value="1">1人</option>
                                <option value="2">2人</option>
                                <option value="3-5">3-5人</option>
                                <option value="6+">6人以上</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="interests">兴趣偏好</label>
                        <textarea id="interests" rows="3" placeholder="例如：喜欢自然风光、历史文化、美食体验、购物等"></textarea>
                    </div>
                    <button type="submit" class="submit-btn">生成专属行程</button>
                </form>
            </div>
        </div>
    </section>

    <!-- 特色服务 -->
    <section class="features" id="features">
        <h2 class="section-title">我们的特色服务</h2>
        <div class="feature-grid">
            <div class="feature-card">
                <div class="feature-icon">🤖</div>
                <h3>AI智能规划</h3>
                <p>基于大数据和人工智能，为您定制最优旅行路线</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">💰</div>
                <h3>预算优化</h3>
                <p>智能比价，帮您找到性价比最高的住宿和交通方案</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">📱</div>
                <h3>实时助手</h3>
                <p>24小时在线客服，随时解答旅途中的问题</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">🎯</div>
                <h3>个性化推荐</h3>
                <p>根据您的喜好，推荐最适合的景点和活动</p>
            </div>
        </div>
    </section>

    <!-- 页脚 -->
    <footer id="contact">
        <div class="footer-content">
            <div class="footer-section">
                <h3>关于智游</h3>
                <p>智游是领先的智能旅游规划平台，致力于为用户提供个性化、智能化的旅行解决方案。</p>
            </div>
            <div class="footer-section">
                <h3>快速链接</h3>
                <ul>
                    <li><a href="#">热门目的地</a></li>
                    <li><a href="#">行程规划</a></li>
                    <li><a href="#">旅游攻略</a></li>
                    <li><a href="#">用户评价</a></li>
                </ul>
            </div>
            <div class="footer-section">
                <h3>联系方式</h3>
                <ul>
                    <li>📧 客服邮箱：service@zhiyou.com</li>
                    <li>📞 客服热线：400-888-9999</li>
                    <li>🕐 服务时间：9:00-21:00</li>
                </ul>
            </div>
            <div class="footer-section">
                <h3>关注我们</h3>
                <ul>
                    <li><a href="#">微信公众号</a></li>
                    <li><a href="#">微博</a></li>
                    <li><a href="#">抖音</a></li>
                    <li><a href="#">小红书</a></li>
                </ul>
            </div>
        </div>
        <div class="footer-bottom">
            <p>&copy; 2026 智游旅游规划平台. 保留所有权利.</p>
        </div>
    </footer>

    <script>
        // 平滑滚动
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth'
                    });
                }
            });
        });

        // AI聊天功能
        const chatInput = document.getElementById('chatInput');
        const sendBtn = document.getElementById('sendBtn');
        const chatMessages = document.getElementById('chatMessages');

        // 预设回复
        const responses = {
            '推荐': '根据您的喜好，我为您推荐以下几个目的地：\n\n🏔️ 云南大理 - 苍山洱海，风花雪月\n🏖️ 海南三亚 - 阳光沙滩，度假天堂\n🏯 日本京都 - 古都韵味，樱花盛开\n\n您对哪个感兴趣呢？',
            '预算': '旅行预算主要包含以下几个方面：\n\n💰 交通费：机票/火车票\n🏨 住宿费：酒店/民宿\n🍜 餐饮费：当地美食\n🎫 门票费：景点门票\n🛍️ 购物费：纪念品\n\n我可以帮您制定详细的预算计划！',
            '行程': '规划行程需要考虑：\n\n📅 旅行天数\n🎯 兴趣偏好（自然/文化/美食）\n💵 预算范围\n👥 出行人数\n\n请告诉我您的具体需求，我为您定制专属行程！',
            '天气': '出行前查看天气很重要！建议您：\n\n☀️ 提前7天查询天气预报\n🌧️ 准备雨具和防晒用品\n👕 根据气温准备衣物\n📱 下载天气APP实时关注\n\n需要我帮您查询某个目的地的天气吗？',
            '签证': '关于签证办理：\n\n📋 国内游：无需签证\n🌏 东南亚：部分国家落地签\n🇪🇺 欧洲：需申根签证\n🇺🇸 美国：需提前面签\n\n建议提前1-2个月办理，我可以提供详细指导！',
            'default': '感谢您的咨询！作为AI助手，我可以为您提供：\n\n• 目的地推荐和介绍\n• 行程规划和优化\n• 预算计算和建议\n• 旅行注意事项\n• 签证和交通信息\n\n请问还有什么可以帮您的吗？😊'
        };

        function addMessage(text, isUser = false) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${isUser ? 'user' : 'ai'}`;
            
            const avatar = document.createElement('div');
            avatar.className = 'message-avatar';
            avatar.textContent = isUser ? '👤' : '🤖';
            
            const content = document.createElement('div');
            content.className = 'message-content';
            content.textContent = text;
            
            messageDiv.appendChild(avatar);
            messageDiv.appendChild(content);
            chatMessages.appendChild(messageDiv);
            
            // 滚动到底部
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function showTypingIndicator() {
            const typingDiv = document.createElement('div');
            typingDiv.className = 'message ai';
            typingDiv.id = 'typingIndicator';
            
            const avatar = document.createElement('div');
            avatar.className = 'message-avatar';
            avatar.textContent = '🤖';
            
            const content = document.createElement('div');
            content.className = 'message-content';
            
            const typingDots = document.createElement('div');
            typingDots.className = 'typing-indicator';
            typingDots.innerHTML = '<div class="typing-dot"></div><div class="typing-dot"></div><div class="typing-dot"></div>';
            
            content.appendChild(typingDots);
            typingDiv.appendChild(avatar);
            typingDiv.appendChild(content);
            chatMessages.appendChild(typingDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function removeTypingIndicator() {
            const indicator = document.getElementById('typingIndicator');
            if (indicator) {
                indicator.remove();
            }
        }

        function getResponse(userMessage) {
            const lowerMsg = userMessage.toLowerCase();
            
            for (const [key, value] of Object.entries(responses)) {
                if (key !== 'default' && lowerMsg.includes(key)) {
                    return value;
                }
            }
            
            return responses['default'];
        }

        function sendMessage() {
            const message = chatInput.value.trim();
            if (!message) return;
            
            // 添加用户消息
            addMessage(message, true);
            chatInput.value = '';
            
            // 显示输入中提示
            showTypingIndicator();
            
            // 模拟AI回复延迟
            setTimeout(() => {
                removeTypingIndicator();
                const response = getResponse(message);
                addMessage(response);
            }, 1000 + Math.random() * 1000);
        }

        // 发送按钮点击事件
        sendBtn.addEventListener('click', sendMessage);

        // 回车键发送
        chatInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });

        // 目的地卡片点击效果
        document.querySelectorAll('.destination-card').forEach(card => {
            card.addEventListener('click', function() {
                const destination = this.querySelector('h3').textContent;
                alert(`即将跳转到 ${destination} 的详细页面`);
            });
        });

        // 行程规划表单提交
        document.querySelector('.planner-form form').addEventListener('submit', function(e) {
            e.preventDefault();
            alert('正在为您生成专属行程，请稍候...');
        });
    </script>
</body>
</html>
