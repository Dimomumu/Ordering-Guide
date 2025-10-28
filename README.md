<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>卷烟订购新模式 - 价位段自选</title>
    <style>
        /* 基础样式 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Microsoft YaHei', Arial, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            color: #fff;
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        /* 头部样式 */
        header {
            text-align: center;
            padding: 30px 20px;
            background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
            color: white;
            position: relative;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        /* 语音控制区域 */
        .voice-controls {
            position: absolute;
            top: 20px;
            right: 20px;
            display: flex;
            gap: 10px;
        }
        
        .voice-btn {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }
        
        .voice-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.1);
        }
        
        .voice-btn.active {
            background: #4caf50;
            box-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
        }
        
        /* 进度条样式 */
        .progress-container {
            width: 100%;
            background: rgba(255, 255, 255, 0.2);
            height: 8px;
            margin: 20px 0 0;
            border-radius: 4px;
            overflow: hidden;
        }
        
        .progress-bar {
            height: 100%;
            background: #ffeb3b;
            width: 10%;
            border-radius: 4px;
            transition: width 0.5s ease;
        }
        
        /* 故事内容样式 */
        .story-content {
            padding: 30px;
            position: relative;
        }
        
        .story-text {
            font-size: 1.1rem;
            margin-bottom: 25px;
            line-height: 1.7;
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 10px;
        }
        
        /* 选择按钮样式 */
        .choices {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 15px;
            margin-top: 30px;
        }
        
        .choice-btn {
            background: linear-gradient(135deg, #4caf50 0%, #388e3c 100%);
            color: white;
            border: none;
            padding: 18px;
            border-radius: 10px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(76, 175, 80, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-weight: 500;
        }
        
        .choice-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(76, 175, 80, 0.4);
        }
        
        .choice-btn.red {
            background: linear-gradient(135deg, #f44336 0%, #d32f2f 100%);
            box-shadow: 0 4px 10px rgba(244, 67, 54, 0.3);
        }
        
        .choice-btn.red:hover {
            box-shadow: 0 6px 15px rgba(244, 67, 54, 0.4);
        }
        
        .choice-btn.blue {
            background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
            box-shadow: 0 4px 10px rgba(33, 150, 243, 0.3);
        }
        
        .choice-btn.blue:hover {
            box-shadow: 0 6px 15px rgba(33, 150, 243, 0.4);
        }
        
        /* 步骤说明样式 */
        .steps {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 20px;
            margin: 25px 0;
            border-left: 5px solid #2196f3;
        }
        
        .step {
            margin-bottom: 15px;
            padding-left: 15px;
            border-left: 3px solid #4caf50;
            padding-top: 5px;
            padding-bottom: 5px;
        }
        
        .step-number {
            display: inline-block;
            background: #4caf50;
            color: white;
            width: 28px;
            height: 28px;
            border-radius: 50%;
            text-align: center;
            line-height: 28px;
            margin-right: 10px;
            font-weight: bold;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .container {
                border-radius: 10px;
            }
            
            header {
                padding: 20px 15px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .story-content {
                padding: 20px;
            }
            
            .choices {
                grid-template-columns: 1fr;
            }
            
            .choice-btn {
                padding: 15px;
                font-size: 1rem;
            }
            
            .voice-controls {
                position: static;
                justify-content: center;
                margin-top: 15px;
            }
        }
        
        /* 动画效果 */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .fade-in {
            animation: fadeIn 0.6s ease-out;
        }
        
        /* 强调文本 */
        .highlight {
            background: rgba(33, 150, 243, 0.2);
            padding: 2px 6px;
            border-radius: 4px;
            font-weight: bold;
        }
        
        .quote {
            font-style: italic;
            padding: 15px;
            background: rgba(255, 255, 255, 0.05);
            border-left: 4px solid #4caf50;
            margin: 15px 0;
        }
        
        /* 语音播放指示器 */
        .speech-indicator {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 10px 15px;
            border-radius: 20px;
            display: none;
            align-items: center;
            gap: 10px;
            z-index: 100;
        }
        
        .speech-indicator.active {
            display: flex;
        }
        
        .pulse {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: #4caf50;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% {
                transform: scale(0.8);
                opacity: 0.7;
            }
            50% {
                transform: scale(1.2);
                opacity: 1;
            }
            100% {
                transform: scale(0.8);
                opacity: 0.7;
            }
        }
        
        /* 自动播放开关 */
        .auto-play-toggle {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 15px 0;
            color: #bbbbbb;
        }
        
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 24px;
        }
        
        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        
        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 24px;
        }
        
        .slider:before {
            position: absolute;
            content: "";
            height: 16px;
            width: 16px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }
        
        input:checked + .slider {
            background-color: #4caf50;
        }
        
        input:checked + .slider:before {
            transform: translateX(26px);
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>卷烟订购新模式 - 价位段自选</h1>
            <p class="subtitle">智能订货，省时省力</p>
            
            <div class="voice-controls">
                <button class="voice-btn" id="playVoice" title="播放语音">
                    🔊
                </button>
                <button class="voice-btn" id="stopVoice" title="停止语音">
                    ⏹️
                </button>
            </div>
            
            <div class="progress-container">
                <div class="progress-bar" id="progress"></div>
            </div>
        </header>
        
        <main class="story-content fade-in" id="story-content">
            <!-- 内容将通过JavaScript动态加载 -->
        </main>
    </div>
    
    <div class="speech-indicator" id="speechIndicator">
        <div class="pulse"></div>
        <span>正在朗读中...</span>
    </div>

    <script>
        // 语音合成对象
        let speechSynthesis = window.speechSynthesis;
        let currentUtterance = null;
        let autoPlayEnabled = false;

        // 故事场景数据
        const scenes = {
            1: {
                title: "新的订货方式来了！",
                content: `
                    <div class="story-text">
                        <p>客户经理小李兴冲冲走进店里告诉你：</p>
                        <div class="quote">"刘老板，好消息！订货系统升级了，现在可以按价位段自选，操作特别简单！"</div>
                        <p>面对这个新功能，你会：</p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn red" onclick="showScene(2)">
                            <span>🔴</span> 不理会 (心想:卖烟多年自己会订)
                        </button>
                        <button class="choice-btn green" onclick="showScene(3)">
                            <span>🟢</span> 学习新方法
                        </button>
                    </div>
                `,
                speechText: "客户经理小李兴冲冲走进店里告诉你：刘老板，好消息！订货系统升级了，现在可以按价位段自选，操作特别简单！面对这个新功能，你会选择不理会还是学习新方法？",
                progress: 10
            },
            2: {
                title: "不理会新方法",
                content: `
                    <div class="story-text">
                        <p>你自信满满：<span class="highlight">"卖烟这么多年，订货还用学？"</span></p>
                        <p>直接打开订货系统，按经验开始订货...</p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(4)">
                            进入传统订货模式
                        </button>
                    </div>
                `,
                speechText: "你自信满满地说：卖烟这么多年，订货还用学？直接打开订货系统，按经验开始订货。",
                progress: 20
            },
            3: {
                title: "学习新方法",
                content: `
                    <div class="story-text">
                        <p>你好奇地问：<span class="highlight">"价位段自选是什么？"</span></p>
                        <p>小王热情介绍："就是把卷烟按价格分成12个区间，像去餐馆点菜一样简单呢！"</p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(5)">
                            了解价位段自选
                        </button>
                    </div>
                `,
                speechText: "你好奇地问：价位段自选是什么？小王热情介绍：就是把卷烟按价格分成12个区间，像去餐馆点菜一样简单呢！",
                progress: 30
            },
            4: {
                title: "传统订货模式的困境",
                content: `
                    <div class="story-text">
                        <p>面对几百个卷烟和雪茄烟品规，你一个个浏览...</p>
                        <p>发现三分之二都是自己档位订不了的！</p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(8)">
                            继续硬着头皮挑选
                        </button>
                    </div>
                `,
                speechText: "面对几百个卷烟和雪茄烟品规，你一个个浏览，发现三分之二都是自己档位订不了的！",
                progress: 40
            },
            5: {
                title: "价位段自选是什么",
                content: `
                    <div class="story-text">
                        <p>根据含税批发价，在行业"五类八档"基础上将一至五档卷烟统一划分为12个价位段。</p>
                        <p>除新品、紧俏烟、雪茄烟、国产混合型卷烟、进口烟以及一些特殊商品外，一至五档所有卷烟规格均纳入按价位段自选投放。</p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(6)">
                            与传统订货区别是什么？
                        </button>
                    </div>
                `,
                speechText: "根据含税批发价，在行业五类八档基础上将一至五档卷烟统一划分为12个价位段。除新品、紧俏烟、雪茄烟、国产混合型卷烟、进口烟以及一些特殊商品外，一至五档所有卷烟规格均纳入按价位段自选投放。",
                progress: 50
            },
            6: {
                title: "与传统订货区别",
                content: `
                    <div class="story-text">
                        <p><strong>传统的按档位投放：</strong>是具体设置某个品规的订购量上限。</p>
                        <div class="quote">🟤 例如：玉溪(软)5条、玉溪(硬)5条、芙蓉王(硬)5条等。</div>
                        
                        <p><strong>按价位段自选投放：</strong>将价格相近的卷烟放在一起作为一个价位段区间，订货时，同一个价位段区间内的各规格，除了有各自的订购数量限制，总订购数量还需控制在该价位段的可订购总量以内。</p>
                        <div class="quote">🟤 例如：将玉溪(软)、玉溪(硬)、芙蓉王(硬)作为一个价位段组合，单个品规订购不超过5条，且这3个品规合计最多可订购10条，客户可自由选择所需品规——3条玉溪(软)、3条玉溪(硬)、4条芙蓉王(硬)等任意组合。</div>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(7)">
                            价位段自选订购怎么操作
                        </button>
                    </div>
                `,
                speechText: "传统的按档位投放是具体设置某个品规的订购量上限。例如：玉溪软5条、玉溪硬5条、芙蓉王硬5条等。按价位段自选投放是将价格相近的卷烟放在一起作为一个价位段区间，订货时，同一个价位段区间内的各规格，除了有各自的订购数量限制，总订购数量还需控制在该价位段的可订购总量以内。例如：将玉溪软、玉溪硬、芙蓉王硬作为一个价位段组合，单个品规订购不超过5条，且这3个品规合计最多可订购10条，客户可自由选择所需品规——3条玉溪软、3条玉溪硬、4条芙蓉王硬等任意组合。",
                progress: 60
            },
            7: {
                title: "价位段自选操作步骤",
                content: `
                    <div class="steps">
                        <div class="step">
                            <span class="step-number">1</span>
                            <strong>筛选锁定：</strong>先点击漏斗状图标选择：仅显示可订购卷烟，这样界面上就只显示您当前有资格订购的品规。
                        </div>
                        <div class="step">
                            <span class="step-number">2</span>
                            <strong>按段查看：</strong>从第1价位段开始顺序查看。直接在这个数字框内输入您想要的订购量（不能超过显示的数字）。合理订量后面显示的数字，就是当前可订的最大数量。
                        </div>
                        <div class="step">
                            <span class="step-number">3</span>
                            <strong>核对总量：</strong>所有品规选完后，检查"合理定量"总额是否等于"订购量"总额。如果不等，说明有品规数量未输入或输入有误，请返回核对。
                        </div>
                        <div class="step">
                            <span class="step-number">4</span>
                            <strong>补全常规品规：</strong>重要提醒：完成"价位段自选"后，不要忘记还有系统根据您的档位直接为您匹配的"按档位投放"的品规。检查常规订购区，一并加入订单，确保货源齐全。
                        </div>
                    </div>
                    
                    <div class="story-text">
                        <div class="quote" style="text-align: center; color: #4caf50;">"比传统方式快多了！"</div>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn green" onclick="showScene(11)">
                            开始体验
                        </button>
                    </div>
                `,
                speechText: "价位段自选操作步骤：第一步，筛选锁定：先点击漏斗状图标选择：仅显示可订购卷烟，这样界面上就只显示您当前有资格订购的品规。第二步，按段查看：从第1价位段开始顺序查看。直接在这个数字框内输入您想要的订购量。合理订量后面显示的数字，就是当前可订的最大数量。第三步，核对总量：所有品规选完后，检查合理定量总额是否等于订购量总额。如果不等，说明有品规数量未输入或输入有误，请返回核对。第四步，补全常规品规：重要提醒：完成价位段自选后，不要忘记还有系统根据您的档位直接为您匹配的按档位投放的品规。检查常规订购区，一并加入订单，确保货源齐全。比传统方式快多了！",
                progress: 70
            },
            8: {
                title: "传统模式的困扰",
                content: `
                    <div class="story-text">
                        <p>眼花缭乱地在众多规格中寻找能订的...</p>
                        <p>你选择了很久，时间一分一秒过去，效率极低。</p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(9)">
                            最终选择
                        </button>
                    </div>
                `,
                speechText: "眼花缭乱地在众多规格中寻找能订的，你选择了很久，时间一分一秒过去，效率极低。",
                progress: 80
            },
            9: {
                title: "传统模式的结果",
                content: `
                    <div class="story-text">
                        <p>忙活了半天，想订的没订到，不需要的订了一堆。</p>
                        <div class="quote" style="color: #f44336;">"唉，白白浪费了时间！"</div>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn red" onclick="showScene(10)">
                            ⚫️ 你懊恼地关闭系统
                        </button>
                        <button class="choice-btn green" onclick="showScene(3)">
                            🟢 学习新方法
                        </button>
                    </div>
                `,
                speechText: "忙活了半天，想订的没订到，不需要的订了一堆。唉，白白浪费了时间！",
                progress: 90
            },
            10: {
                title: "懊恼的结果",
                content: `
                    <div class="story-text">
                        <div class="quote" style="text-align: center; color: #f44336; font-size: 1.2rem;">
                            传统订货方式效率低下，浪费了大量时间却没有得到满意的结果。
                        </div>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn green" onclick="showScene(1)">
                            重新开始
                        </button>
                    </div>
                `,
                speechText: "传统订货方式效率低下，浪费了大量时间却没有得到满意的结果。",
                progress: 100
            },
            11: {
                title: "体验新方法",
                content: `
                    <div class="story-text">
                        <p>你尝试新方法：</p>
                        <p>筛选可订购卷烟 → 快速找到符合档位的品牌 → 精准满足订货需求！</p>
                        <div class="quote" style="color: #4caf50;">"这才是智能订货！省时省力还准确！"</div>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn green" onclick="showScene(12)">
                            满意收货
                        </button>
                    </div>
                `,
                speechText: "你尝试新方法：筛选可订购卷烟，快速找到符合档位的品牌，精准满足订货需求！这才是智能订货！省时省力还准确！",
                progress: 90
            },
            12: {
                title: "满意收货",
                content: `
                    <div class="story-text">
                        <div class="quote" style="text-align: center; color: #4caf50; font-size: 1.2rem;">
                            订货准确送达，都是你需要的规格。
                        </div>
                        <p style="text-align: center; font-weight: bold; margin-top: 20px;">
                            价位段自选让订货变得更简单、更高效！
                        </p>
                    </div>
                    
                    <div class="choices">
                        <button class="choice-btn blue" onclick="showScene(1)">
                            重新开始
                        </button>
                    </div>
                `,
                speechText: "订货准确送达，都是你需要的规格。价位段自选让订货变得更简单、更高效！",
                progress: 100
            }
        };

        // 语音朗读功能
        function speakText(text) {
            // 停止当前语音
            stopSpeech();
            
            // 创建新的语音对象
            currentUtterance = new SpeechSynthesisUtterance(text);
            
            // 设置语音参数
            currentUtterance.lang = 'zh-CN';
            currentUtterance.rate = 0.9; // 语速
            currentUtterance.pitch = 1; // 音调
            currentUtterance.volume = 1; // 音量
            
            // 显示语音播放指示器
            document.getElementById('speechIndicator').classList.add('active');
            
            // 语音结束时的回调
            currentUtterance.onend = function() {
                document.getElementById('speechIndicator').classList.remove('active');
                document.getElementById('playVoice').classList.remove('active');
            };
            
            // 语音错误时的回调
            currentUtterance.onerror = function() {
                document.getElementById('speechIndicator').classList.remove('active');
                document.getElementById('playVoice').classList.remove('active');
                alert('语音播放出现错误，请检查浏览器设置或尝试使用其他浏览器。');
            };
            
            // 开始语音合成
            speechSynthesis.speak(currentUtterance);
            document.getElementById('playVoice').classList.add('active');
        }
        
        // 停止语音
        function stopSpeech() {
            if (speechSynthesis.speaking) {
                speechSynthesis.cancel();
                document.getElementById('speechIndicator').classList.remove('active');
                document.getElementById('playVoice').classList.remove('active');
            }
        }
        
        // 显示场景函数
        function showScene(sceneId) {
            const scene = scenes[sceneId];
            if (!scene) return;
            
            const contentElement = document.getElementById('story-content');
            contentElement.innerHTML = `
                <h2 style="margin-bottom: 20px; color: #4fc3f7; text-align: center;">${scene.title}</h2>
                ${scene.content}
                <div class="auto-play-toggle">
                    <span>自动播放语音</span>
                    <label class="toggle-switch">
                        <input type="checkbox" id="autoPlayToggle" ${autoPlayEnabled ? 'checked' : ''}>
                        <span class="slider"></span>
                    </label>
                </div>
            `;
            
            // 更新进度条
            document.getElementById('progress').style.width = `${scene.progress}%`;
            
            // 添加淡入动画
            contentElement.classList.remove('fade-in');
            void contentElement.offsetWidth; // 触发重绘
            contentElement.classList.add('fade-in');
            
            // 滚动到顶部
            window.scrollTo({ top: 0, behavior: 'smooth' });
            
            // 如果启用了自动播放，则自动朗读
            if (autoPlayEnabled) {
                setTimeout(() => {
                    speakText(scene.speechText);
                }, 500);
            }
            
            // 绑定自动播放切换事件
            document.getElementById('autoPlayToggle').addEventListener('change', function() {
                autoPlayEnabled = this.checked;
            });
        }

        // 初始化页面
        document.addEventListener('DOMContentLoaded', function() {
            // 设置初始场景
            showScene(1);
            
            // 语音控制按钮事件
            document.getElementById('playVoice').addEventListener('click', function() {
                const currentSceneId = Object.keys(scenes).find(key => scenes[key].progress === parseInt(document.getElementById('progress').style.width));
                if (currentSceneId) {
                    speakText(scenes[currentSceneId].speechText);
                }
            });
            
            document.getElementById('stopVoice').addEventListener('click', function() {
                stopSpeech();
            });
        });
    </script>
</body>
</html>
