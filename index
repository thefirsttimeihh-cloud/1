<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>感情が変わるボタン</title>
    <style>
        /* 画面全体のスタイル */
        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #2cece6; /* 画像1の鮮やかな水色 */
            transition: background-color 0.4s ease; /* 背景変化を滑らかに */
            overflow: hidden;
            font-family: sans-serif;
            position: relative;
        }

        /* 中央の顔文字ボタン */
        .emoji-btn {
            font-size: 5rem;
            background: none;
            border: none;
            cursor: pointer;
            outline: none;
            user-select: none;
            transition: transform 0.1s ease;
            z-index: 10;
        }

        /* ボタンを押したときの軽いへこみ演出 */
        .emoji-btn:active {
            transform: scale(0.9);
        }

        /* 飛び出す花火（絵文字）のスタイル */
        .firework-particle {
            position: absolute;
            font-size: 2.5rem;
            pointer-events: none;
            z-index: 5;
            animation: explode 0.8s ease-out forwards;
        }

        /* 花火が四方八方に飛び散って消えるアニメーション */
        @keyframes explode {
            0% {
                transform: translate(-50%, -50%) translate(0, 0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(-50%, -50%) translate(var(--x), var(--y)) scale(1.5);
                opacity: 0;
            }
        }
    </style>
</head>
<body>

    <button id="emojiBtn" class="emoji-btn">☺️</button>

    <script>
        const btn = document.getElementById('emojiBtn');
        
        /* クリックするたびに切り替わる「背景色」と「表情」のリスト。
           画像1（水色）と画像2（赤）を交互に行き来するように設定しています。
        */
        const states = [
            { bg: '#2cece6', emoji: '☺️' }, // 初期状態（水色）
            { bg: '#ff0000', emoji: '🤩' }, // クリック後（赤）
            { bg: '#ff00ee', emoji: '🥳' }, // おまけ：ピンク
            { bg: '#00ff66', emoji: '😎' }  // おまけ：緑
        ];
        
        let currentState = 0;

        btn.addEventListener('click', (e) => {
            // 1. 次の状態へ進める（最後の次は最初に戻る）
            currentState = (currentState + 1) % states.length;
            
            // 2. 背景色とボタンの絵文字を更新
            document.body.style.backgroundColor = states[currentState].bg;
            btn.textContent = states[currentState].emoji;

            // 3. クリックした位置から花火を打ち上げる
            createFireworks(e.clientX, e.clientY);
        });

        // 花火エフェクトを生成する関数
        function createFireworks(startX, startY) {
            const particles = ['🎆', '✨', '🎇', '💥', '🎉'];
            const particleCount = 15; // 1回に飛び出す絵文字の数

            for (let i = 0; i < particleCount; i++) {
                const span = document.createElement('span');
                span.classList.add('firework-particle');
                
                // ランダムに花火の絵文字をチョイス
                span.textContent = particles[Math.floor(Math.random() * particles.length)];
                
                // クリックされた座標に配置
                span.style.left = `${startX}px`;
                span.style.top = `${startY}px`;

                // 飛び散る方向（角度と距離）をランダムに計算
                const angle = Math.random() * Math.PI * 2; // 360度
                const distance = 60 + Math.random() * 140; // 飛び散る距離
                const x = Math.cos(angle) * distance;
                const y = Math.sin(angle) * distance;

                // CSSの変数（カスタムプロパティ）を使ってアニメーション先に数値を渡す
                span.style.setProperty('--x', `${x}px`);
                span.style.setProperty('--y', `${y}px`);

                document.body.appendChild(span);

                // アニメーション（0.8秒）が終わったら自動で要素を削除
                span.addEventListener('animationend', () => {
                    span.remove();
                });
            }
        }
    </script>
</body>
</html>
