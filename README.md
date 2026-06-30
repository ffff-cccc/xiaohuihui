<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>智游 · 土地公智能旅行规划</title>
    <style>
        /* ========== 全部样式保持不变（已隐藏省略） ========== */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Microsoft YaHei', Arial, sans-serif; line-height: 1.6; color: #333; }
        .navbar { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 1rem 2rem; position: fixed; width: 100%; top: 0; z-index: 1000; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
        .nav-container { max-width: 1200px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; }
        .logo { font-size: 1.8rem; font-weight: bold; color: white; text-decoration: none; }
        .nav-links { display: flex; gap: 2rem; list-style: none; }
        .nav-links a { color: white; text-decoration: none; font-weight: 500; transition: opacity 0.3s; }
        .nav-links a:hover { opacity: 0.8; }
        .hero { background: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1920&q=80'); background-size: cover; background-position: center; background-attachment: fixed; height: 700px; display: flex; align-items: center; justify-content: center; text-align: center; color: white; margin-top: 60px; position: relative; }
        .chat-container { max-width: 900px; margin: 0 auto; width: 95%; }
        .chat-window { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); border-radius: 15px; box-shadow: 0 8px 32px rgba(0,0,0,0.3); overflow: hidden; height: 450px; display: flex; flex-direction: column; }
        .chat-header { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 1rem 1.5rem; display: flex; align-items: center; gap: 1rem; color: white; }
        .chat-avatar { width: 45px; height: 45px; background: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; overflow: hidden; }
        .chat-avatar img { width: 100%; height: 100%; object-fit: cover; }
        .chat-header-info h3 { font-size: 1.2rem; margin-bottom: 0.2rem; }
        .chat-header-info p { font-size: 0.85rem; opacity: 0.9; }
        .chat-messages { flex: 1; padding: 1.5rem; overflow-y: auto; background: #f8f9fa; }
        .message { margin-bottom: 1rem; display: flex; gap: 0.8rem; animation: messageSlide 0.3s ease-out; }
        @keyframes messageSlide { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .message.user { flex-direction: row-reverse; }
        .message-avatar { width: 35px; height: 35px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1.2rem; flex-shrink: 0; overflow: hidden; }
        .message.ai .message-avatar { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .message.user .message-avatar { background: #e0e0e0; }
        .message-content { max-width: 70%; padding: 0.8rem 1rem; border-radius: 15px; line-height: 1.5; font-size: 0.95rem; white-space: pre-wrap; word-break: break-word; }
        .message.ai .message-content { background: white; color: #333; border-bottom-left-radius: 5px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .message.user .message-content { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border-bottom-right-radius: 5px; }
        .chat-input-area { padding: 1rem 1.5rem; background: white; border-top: 1px solid #e0e0e0; display: flex; gap: 0.8rem; }
        .chat-input { flex: 1; padding: 0.8rem 1rem; border: 2px solid #e0e0e0; border-radius: 25px; font-size: 0.95rem; outline: none; transition: border-color 0.3s; }
        .chat-input:focus { border-color: #667eea; }
        .send-btn { width: 45px; height: 45px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border: none; border-radius: 50%; color: white; font-size: 1.2rem; cursor: pointer; transition: transform 0.3s, box-shadow 0.3s; display: flex; align-items: center; justify-content: center; }
        .send-btn:hover { transform: scale(1.1); box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4); }
        .send-btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }
        .typing-indicator { display: flex; gap: 0.3rem; padding: 0.5rem 0; }
        .typing-dot { width: 8px; height: 8px; background: #999; border-radius: 50%; animation: typing 1.4s infinite; }
        .typing-dot:nth-child(2) { animation-delay: 0.2s; }
        .typing-dot:nth-child(3) { animation-delay: 0.4s; }
        @keyframes typing { 0%, 60%, 100% { transform: translateY(0); } 30% { transform: translateY(-10px); } }
        .error-msg { background: #f8d7da; color: #721c24; padding: 0.5rem 1rem; border-radius: 5px; margin-top: 0.5rem; font-size: 0.9rem; }
        @media (max-width: 768px) { .hero { height: 600px; } .chat-window { height: 400px; } .nav-links { display: none; } }
    </style>
</head>
<body>
    <!-- 导航栏 -->
    <nav class="navbar">
        <div class="nav-container">
            <a href="#" class="logo">🌍 土地陪你旅个游</a>
            <ul class="nav-links">
                <li><a href="#home">首页</a></li>
                <li><a href="#destinations">目的地</a></li>
                <li><a href="#planner">行程规划</a></li>
                <li><a href="#features">特色服务</a></li>
                <li><a href="#contact">联系我们</a></li>
            </ul>
        </div>
    </nav>

    <!-- 主横幅 + 聊天窗口 -->
    <section class="hero" id="home">
        <div class="chat-container">
            <div class="chat-window">
                <div class="chat-header">
                    <div class="chat-avatar">
                        <img src="tudigong.png" alt="土地公" />
                    </div>
                    <div class="chat-header-info">
                        <h3>土地陪你旅个游</h3>
                        <p>在线 · 灵机一动，行程即来</p>
                    </div>
                </div>
                <div class="chat-messages" id="chatMessages">
                    <div class="message ai">
                        <div class="message-avatar">
                            <img src="tudigong.png" alt="土地公" />
                        </div>
                        <div class="message-content">
                            乡亲们！小神掐指一算，您这趟旅行缺个'活地图'！<br /><br />
                            快把时间（比如'2026年7月1日-3日'）、去哪儿（比如'杭州'）和同行的'小伙伴'（比如'爸妈+10岁娃'）报上来，小神好给您量身画个'平安符'似的行程~
                        </div>
                    </div>
                </div>
                <div class="chat-input-area">
                    <input type="text" class="chat-input" id="chatInput" placeholder="输入您的问题..." />
                    <button class="send-btn" id="sendBtn">➤</button>
                </div>
            </div>
        </div>
    </section>

    <script>
        (function() {
            'use strict';

            // ================= 配置区（请替换为你的真实信息）=================
            const COZE_API_KEY = 'pat_EgURkCDea7qtD5p15w9hcJQIBpPlPvzVATICDVkNccyJiob9ckzqF2ezcolUcm6v';          // 你的 Coze API Key
            const COZE_BOT_ID = '7656282947481731107';    // 你的 Bot ID
            const COZE_API_URL = 'https://api.coze.cn/open_api/v2/chat';
            // ============================================================

            const chatInput = document.getElementById('chatInput');
            const sendBtn = document.getElementById('sendBtn');
            const chatMessages = document.getElementById('chatMessages');

            // 用于多轮对话
            let conversationId = null;

            // ---------- 辅助函数 ----------
            function addMessage(text, isUser = false) {
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${isUser ? 'user' : 'ai'}`;

                const avatar = document.createElement('div');
                avatar.className = 'message-avatar';
                if (isUser) {
                    avatar.textContent = '👤';
                } else {
                    const img = document.createElement('img');
                    img.src = 'tudigong.png';
                    img.alt = '土地公';
                    avatar.appendChild(img);
                }

                const content = document.createElement('div');
                content.className = 'message-content';
                content.textContent = text;

                messageDiv.appendChild(avatar);
                messageDiv.appendChild(content);
                chatMessages.appendChild(messageDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }

            function showTypingIndicator() {
                const typingDiv = document.createElement('div');
                typingDiv.className = 'message ai';
                typingDiv.id = 'typingIndicator';

                const avatar = document.createElement('div');
                avatar.className = 'message-avatar';
                const img = document.createElement('img');
                img.src = 'tudigong.png';
                img.alt = '土地公';
                avatar.appendChild(img);

                const content = document.createElement('div');
                content.className = 'message-content';
                const dots = document.createElement('div');
                dots.className = 'typing-indicator';
                dots.innerHTML = '<div class="typing-dot"></div><div class="typing-dot"></div><div class="typing-dot"></div>';
                content.appendChild(dots);

                typingDiv.appendChild(avatar);
                typingDiv.appendChild(content);
                chatMessages.appendChild(typingDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }

            function removeTypingIndicator() {
                const indicator = document.getElementById('typingIndicator');
                if (indicator) indicator.remove();
            }

            function showError(msg) {
                const errorDiv = document.createElement('div');
                errorDiv.className = 'error-msg';
                errorDiv.textContent = '❌ ' + msg;
                chatMessages.appendChild(errorDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }

            // ---------- 提取 Coze 回复（适配 messages 结构）----------
            function extractReplyFromData(data) {
                if (data.messages && Array.isArray(data.messages)) {
                    for (let msg of data.messages) {
                        if (msg.type === 'answer' && msg.content) {
                            return msg.content;
                        }
                    }
                    const assistants = data.messages.filter(m => m.role === 'assistant' && m.content);
                    if (assistants.length > 0) {
                        return assistants[assistants.length - 1].content;
                    }
                }
                const direct = ['content', 'reply', 'output', 'text'];
                for (let f of direct) {
                    if (data[f] && typeof data[f] === 'string') return data[f];
                }
                if (data.data && typeof data.data === 'object') {
                    return extractReplyFromData(data.data);
                }
                return null;
            }

            // ---------- 调用 Coze V2 API ----------
            async function callCozeBot(userMessage, userId = 'landlord_user') {
                const payload = {
                    bot_id: COZE_BOT_ID,
                    user: userId,
                    query: userMessage,
                    stream: false
                };
                if (conversationId) {
                    payload.conversation_id = conversationId;
                }

                const response = await fetch(COZE_API_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${COZE_API_KEY}`
                    },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    const errorText = await response.text();
                    throw new Error(`HTTP ${response.status}: ${errorText}`);
                }

                const data = await response.json();
                if (data.conversation_id) {
                    conversationId = data.conversation_id;
                }
                const reply = extractReplyFromData(data);
                if (!reply) {
                    throw new Error('未能解析回复内容，请查看控制台数据：' + JSON.stringify(data));
                }
                return reply;
            }

            // ---------- 发送消息主流程 ----------
            async function sendMessage() {
                const message = chatInput.value.trim();
                if (!message) return;

                // 禁用按钮
                sendBtn.disabled = true;
                chatInput.disabled = true;

                // 显示用户消息
                addMessage(message, true);
                chatInput.value = '';

                // 显示土地公正在思考
                showTypingIndicator();

                try {
                    const reply = await callCozeBot(message);
                    removeTypingIndicator();
                    addMessage(reply);
                } catch (error) {
                    removeTypingIndicator();
                    showError('土地公打了个盹：' + error.message);
                    console.error(error);
                } finally {
                    sendBtn.disabled = false;
                    chatInput.disabled = false;
                    chatInput.focus();
                }
            }

            // ---------- 绑定事件 ----------
            sendBtn.addEventListener('click', sendMessage);
            chatInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') sendMessage();
            });

            console.log('🌍 土地公已上线，连接 Coze Bot ID:', COZE_BOT_ID);
        })();
    </script>
</body>
</html>
