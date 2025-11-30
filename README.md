# amazing-website-HTML-CSS-JS
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Hackers Website</title>
        <link
            rel="stylesheet"
            href="https://public.codepenassets.com/css/normalize-5.0.0.min.css"
        />
        <style> 
            * {
                box-sizing: border-box;
            }

            :root {
                --on: 0;
                --bg: hsl(
                    calc(200 - (var(--on) * 160)),
                    calc((20 + (var(--on) * 50)) * 1%),
                    calc((20 + (var(--on) * 60)) * 1%)
                );
                --cord: hsl(0, 0%, calc((60 - (var(--on) * 50)) * 1%));
                --stroke: hsl(0, 0%, calc((60 - (var(--on) * 50)) * 1%));
                --shine: hsla(0, 0%, 100%, calc(0.75 - (var(--on) * 0.5)));
                --cap: hsl(0, 0%, calc((40 + (var(--on) * 30)) * 1%));
                --filament: hsl(
                    45,
                    calc(var(--on) * 80%),
                    calc((25 + (var(--on) * 75)) * 1%)
                );
            }

            body {
                margin: 0;
                padding: 0;
                font-family: "Arial", sans-serif;
                background: var(--bg);
                transition: background 0.3s ease;
                overflow-x: hidden;
            }

            .light-bulb-container {
                position: fixed;
                top: 20px;
                right: 20px;
                z-index: 1000;
                width: 120px;
                height: 300px;
            }

            .toggle-scene {
                overflow: visible !important;
                width: 100%;
                height: 100%;
                position: absolute;
            }

            .toggle-scene__cord {
                stroke: var(--cord);
                cursor: move;
            }

            .toggle-scene__cord:nth-of-type(1) {
                display: none;
            }

            .toggle-scene__cord:nth-of-type(2),
            .toggle-scene__cord:nth-of-type(3),
            .toggle-scene__cord:nth-of-type(4),
            .toggle-scene__cord:nth-of-type(5) {
                display: none;
            }

            .toggle-scene__cord-end {
                stroke: var(--cord);
                fill: var(--cord);
            }

            .toggle-scene__dummy-cord {
                stroke-width: 6;
                stroke: var(--cord);
            }

            .bulb__filament {
                stroke: var(--filament);
            }

            .bulb__shine {
                stroke: var(--shine);
            }

            .bulb__flash {
                stroke: #f5e0a3;
                display: none;
            }

            .bulb__bulb {
                stroke: var(--stroke);
                fill: hsla(
                    calc(180 - (95 * var(--on))),
                    80%,
                    80%,
                    calc(0.1 + (0.4 * var(--on)))
                );
            }

            .bulb__cap {
                fill: var(--cap);
            }

            .bulb__cap-shine {
                fill: var(--shine);
            }

            .bulb__cap-outline {
                stroke: var(--stroke);
            }

            .website-content {
                opacity: 0;
                visibility: hidden;
                transition: opacity 0.5s ease, visibility 0.5s ease;
            }

            .website-content.visible {
                opacity: 1;
                visibility: visible;
            }

            .section {
                min-height: 100vh;
                padding: 80px 20px;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                text-align: center;
                position: relative;
            }

            .hero {
                background: linear-gradient(135deg, #e96828 0%, #a29f4b 100%);
                color: white;
            }

            .hero h1 {
                font-size: clamp(2.5rem, 8vw, 6rem);
                margin-bottom: 1rem;
                font-weight: bold;
                text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            }

            .hero p {
                font-size: clamp(1.2rem, 3vw, 2rem);
                margin-bottom: 2rem;
                max-width: 800px;
            }

            .cta-button {
                padding: 15px 30px;
                font-size: 1.2rem;
                background: rgba(255, 255, 255, 0.2);
                color: white;
                border: 2px solid white;
                border-radius: 50px;
                cursor: pointer;
                transition: all 0.3s ease;
                text-decoration: none;
                display: inline-block;
            }

            .cta-button:hover {
                background: white;
                color: #667eea;
                transform: translateY(-2px);
            }

            .about {
                background: #f8f9fa;
                color: #333;
            }

            .about h2 {
                font-size: clamp(2rem, 6vw, 4rem);
                margin-bottom: 2rem;
                color: #2c3e50;
            }

            .about-grid {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                gap: 2rem;
                max-width: 1200px;
                margin-top: 3rem;
            }

            .feature-card {
                background: white;
                padding: 2rem;
                border-radius: 15px;
                box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
                transition: transform 0.3s ease;
            }

            .feature-card:hover {
                transform: translateY(-5px);
            }

            .feature-card h3 {
                color: #667eea;
                font-size: 1.5rem;
                margin-bottom: 1rem;
            }

            .services {
                background: linear-gradient(45deg, #ff6b6b, #feca57);
                color: white;
            }

            .services h2 {
                font-size: clamp(2rem, 6vw, 4rem);
                margin-bottom: 2rem;
            }

            .services-grid {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
                gap: 2rem;
                max-width: 1000px;
                margin-top: 3rem;
            }

            .service-item {
                background: rgba(255, 255, 255, 0.1);
                padding: 2rem;
                border-radius: 15px;
                backdrop-filter: blur(10px);
                border: 1px solid rgba(255, 255, 255, 0.2);
            }

            .service-item h3 {
                font-size: 1.3rem;
                margin-bottom: 1rem;
            }

            .contact {
                background: #2c3e50;
                color: white;
            }

            .contact h2 {
                font-size: clamp(2rem, 6vw, 4rem);
                margin-bottom: 2rem;
            }

            .contact-form {
                max-width: 600px;
                width: 100%;
                margin-top: 2rem;
            }

            .form-group {
                margin-bottom: 1.5rem;
                text-align: left;
            }

            .form-group label {
                display: block;
                margin-bottom: 0.5rem;
                font-weight: bold;
            }

            .form-group input,
            .form-group textarea {
                width: 100%;
                padding: 12px;
                border: none;
                border-radius: 8px;
                font-size: 1rem;
                background: rgba(255, 255, 255, 0.9);
            }

            .form-group textarea {
                height: 120px;
                resize: vertical;
            }

            .submit-btn {
                background: #3498db;
                color: white;
                padding: 15px 30px;
                border: none;
                border-radius: 8px;
                font-size: 1.1rem;
                cursor: pointer;
                transition: background 0.3s ease;
                width: 100%;
            }

            .submit-btn:hover {
                background: #2980b9;
            }

            .floating-elements {
                position: absolute;
                width: 100%;
                height: 100%;
                overflow: hidden;
                pointer-events: none;
            }

            .floating-circle {
                position: absolute;
                border-radius: 50%;
                background: rgba(255, 255, 255, 0.1);
                animation: float 6s ease-in-out infinite;
            }

            .floating-circle:nth-child(1) {
                width: 80px;
                height: 80px;
                top: 20%;
                left: 10%;
                animation-delay: 0s;
            }

            .floating-circle:nth-child(2) {
                width: 120px;
                height: 120px;
                top: 60%;
                right: 15%;
                animation-delay: 2s;
            }

            .floating-circle:nth-child(3) {
                width: 60px;
                height: 60px;
                bottom: 20%;
                left: 20%;
                animation-delay: 4s;
            }

            @keyframes float {
                0%,
                100% {
                    transform: translateY(0px) rotate(0deg);
                }
                50% {
                    transform: translateY(-20px) rotate(180deg);
                }
            }

            .dark-overlay {
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.9);
                z-index: 500;
                display: flex;
                align-items: center;
                justify-content: center;
                color: white;
                font-size: 1.5rem;
                text-align: center;
                opacity: 1;
                visibility: visible;
                transition: opacity 0.5s ease, visibility 0.5s ease;
            }

            .dark-overlay.hidden {
                opacity: 0;
                visibility: hidden;
            }

            @media (max-width: 768px) {
                .light-bulb-container {
                    width: 80px;
                    height: 200px;
                    top: 10px;
                    right: 10px;
                }

                .section {
                    padding: 60px 15px;
                }

                .about-grid {
                    grid-template-columns: 1fr;
                    gap: 1.5rem;
                }

                .services-grid {
                    grid-template-columns: 1fr;
                    gap: 1.5rem;
                }
            }
        </style>
    </head>
    <body>
        <div class="dark-overlay" id="darkOverlay"></div>

        <div class="light-bulb-container">
            <svg
                class="toggle-scene"
                xmlns="http://www.w3.org/2000/svg"
                preserveaspectratio="xMinYMin"
                viewBox="0 0 197.451 481.081"
            >
                <defs>
                    <marker
                        id="e"
                        orient="auto"
                        overflow="visible"
                        refx="0"
                        refy="0"
                    >
                        <path
                            class="toggle-scene__cord-end"
                            fill-rule="evenodd"
                            stroke-width=".2666"
                            d="M.98 0a1 1 0 11-2 0 1 1 0 012 0z"
                        ></path>
                    </marker>
                    <marker
                        id="d"
                        orient="auto"
                        overflow="visible"
                        refx="0"
                        refy="0"
                    >
                        <path
                            class="toggle-scene__cord-end"
                            fill-rule="evenodd"
                            stroke-width=".2666"
                            d="M.98 0a1 1 0 11-2 0 1 1 0 012 0z"
                        ></path>
                    </marker>
                    <marker
                        id="c"
                        orient="auto"
                        overflow="visible"
                        refx="0"
                        refy="0"
                    >
                        <path
                            class="toggle-scene__cord-end"
                            fill-rule="evenodd"
                            stroke-width=".2666"
                            d="M.98 0a1 1 0 11-2 0 1 1 0 012 0z"
                        ></path>
                    </marker>
                    <marker
                        id="b"
                        orient="auto"
                        overflow="visible"
                        refx="0"
                        refy="0"
                    >
                        <path
                            class="toggle-scene__cord-end"
                            fill-rule="evenodd"
                            stroke-width=".2666"
                            d="M.98 0a1 1 0 11-2 0 1 1 0 012 0z"
                        ></path>
                    </marker>
                    <marker
                        id="a"
                        orient="auto"
                        overflow="visible"
                        refx="0"
                        refy="0"
                    >
                        <path
                            class="toggle-scene__cord-end"
                            fill-rule="evenodd"
                            stroke-width=".2666"
                            d="M.98 0a1 1 0 11-2 0 1 1 0 012 0z"
                        ></path>
                    </marker>
                    <clippath id="g" clippathunits="userSpaceOnUse">
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="4.677"
                            d="M-774.546 827.629s12.917-13.473 29.203-13.412c16.53.062 29.203 13.412 29.203 13.412v53.6s-8.825 16-29.203 16c-21.674 0-29.203-16-29.203-16z"
                        ></path>
                    </clippath>
                    <clippath id="f" clippathunits="userSpaceOnUse">
                        <path
                            d="M-868.418 945.051c-4.188 73.011 78.255 53.244 150.216 52.941 82.387-.346 98.921-19.444 98.921-47.058 0-27.615-4.788-42.55-73.823-42.55-69.036 0-171.436-30.937-175.314 36.667z"
                        ></path>
                    </clippath>
                </defs>
                <g class="toggle-scene__cords">
                    <path
                        class="toggle-scene__cord"
                        marker-end="url(#a)"
                        fill="none"
                        stroke-linecap="square"
                        stroke-width="6"
                        d="M123.228-28.56v150.493"
                        transform="translate(-24.503 256.106)"
                    ></path>
                    <path
                        class="toggle-scene__cord"
                        marker-end="url(#a)"
                        fill="none"
                        stroke-linecap="square"
                        stroke-width="6"
                        d="M123.228-28.59s28 8.131 28 19.506-18.667 13.005-28 19.507c-9.333 6.502-28 8.131-28 19.506s28 19.507 28 19.507"
                        transform="translate(-24.503 256.106)"
                    ></path>
                    <path
                        class="toggle-scene__cord"
                        marker-end="url(#a)"
                        fill="none"
                        stroke-linecap="square"
                        stroke-width="6"
                        d="M123.228-28.575s-20 16.871-20 28.468c0 11.597 13.333 18.978 20 28.468 6.667 9.489 20 16.87 20 28.467 0 11.597-20 28.468-20 28.468"
                        transform="translate(-24.503 256.106)"
                    ></path>
                    <path
                        class="toggle-scene__cord"
                        marker-end="url(#a)"
                        fill="none"
                        stroke-linecap="square"
                        stroke-width="6"
                        d="M123.228-28.569s16 20.623 16 32.782c0 12.16-10.667 21.855-16 32.782-5.333 10.928-16 20.623-16 32.782 0 12.16 16 32.782 16 32.782"
                        transform="translate(-24.503 256.106)"
                    ></path>
                    <path
                        class="toggle-scene__cord"
                        marker-end="url(#a)"
                        fill="none"
                        stroke-linecap="square"
                        stroke-width="6"
                        d="M123.228-28.563s-10 24.647-10 37.623c0 12.977 6.667 25.082 10 37.623 3.333 12.541 10 24.647 10 37.623 0 12.977-10 37.623-10 37.623"
                        transform="translate(-24.503 256.106)"
                    ></path>
                    <g class="line toggle-scene__dummy-cord">
                        <line
                            marker-end="url(#a)"
                            x1="98.7255"
                            x2="98.7255"
                            y1="240.5405"
                            y2="380.5405"
                        ></line>
                    </g>
                    <circle
                        class="toggle-scene__hit-spot"
                        cx="98.7255"
                        cy="380.5405"
                        r="60"
                        fill="transparent"
                    ></circle>
                </g>
                <g
                    class="toggle-scene__bulb bulb"
                    transform="translate(844.069 -645.213)"
                >
                    <path
                        class="bulb__cap"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="4.677"
                        d="M-774.546 827.629s12.917-13.473 29.203-13.412c16.53.062 29.203 13.412 29.203 13.412v53.6s-8.825 16-29.203 16c-21.674 0-29.203-16-29.203-16z"
                    ></path>
                    <path
                        class="bulb__cap-shine"
                        d="M-778.379 802.873h25.512v118.409h-25.512z"
                        clip-path="url(#g)"
                        transform="matrix(.52452 0 0 .90177 -368.282 82.976)"
                    ></path>
                    <path
                        class="bulb__cap"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="4"
                        d="M-774.546 827.629s12.917-13.473 29.203-13.412c16.53.062 29.203 13.412 29.203 13.412v0s-8.439 10.115-28.817 10.115c-21.673 0-29.59-10.115-29.59-10.115z"
                    ></path>
                    <path
                        class="bulb__cap-outline"
                        fill="none"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="4.677"
                        d="M-774.546 827.629s12.917-13.473 29.203-13.412c16.53.062 29.203 13.412 29.203 13.412v53.6s-8.825 16-29.203 16c-21.674 0-29.203-16-29.203-16z"
                    ></path>
                    <g
                        class="bulb__filament"
                        fill="none"
                        stroke-linecap="round"
                        stroke-width="5"
                    >
                        <path d="M-752.914 823.875l-8.858-33.06"></path>
                        <path d="M-737.772 823.875l8.858-33.06"></path>
                    </g>
                    <path
                        class="bulb__bulb"
                        stroke-linecap="round"
                        stroke-width="5"
                        d="M-783.192 803.855c5.251 8.815 5.295 21.32 13.272 27.774 12.299 8.045 36.46 8.115 49.127 0 7.976-6.454 8.022-18.96 13.273-27.774 3.992-6.7 14.408-19.811 14.408-19.811 8.276-11.539 12.769-24.594 12.769-38.699 0-35.898-29.102-65-65-65-35.899 0-65 29.102-65 65 0 13.667 4.217 26.348 12.405 38.2 0 0 10.754 13.61 14.746 20.31z"
                    ></path>
                    <circle
                        class="bulb__flash"
                        cx="-745.343"
                        cy="743.939"
                        r="83.725"
                        fill="none"
                        stroke-dasharray="10,30"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="10"
                    ></circle>
                    <path
                        class="bulb__shine"
                        fill="none"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="12"
                        d="M-789.19 757.501a45.897 45.897 0 013.915-36.189 45.897 45.897 0 0129.031-21.957"
                    ></path>
                </g>
            </svg>
        </div>

        <div class="website-content" id="websiteContent">
            <section class="section hero">
                <div class="floating-elements">
                    <div class="floating-circle"></div>
                    <div class="floating-circle"></div>
                    <div class="floating-circle"></div>
                </div>
                <h1>Welcome to Amazing Website</h1>
                <p>
                    Please subscribe my YouTube channel
                </p>
                <a href="https://www.youtube.com/@coding_professor" class="cta-button">subscribe Now</a>
            </section>

            <section class="section about" id="about">
                <h2>About Our Vision</h2>
                <p
                    style="
                        font-size: 1.2rem;
                        max-width: 800px;
                        line-height: 1.6;
                    "
                >
                    We believe in the power of illumination - both literal and
                    metaphorical. Our journey began with a simple idea:
                    sometimes the most profound experiences come from the
                    simplest interactions.
                </p>

                <div class="about-grid">
                    <div class="feature-card">
                        <h3>🎨 Creative Design</h3>
                        <p>
                            Every pixel crafted with precision and purpose,
                            creating experiences that captivate and inspire
                            users across all platforms.
                        </p>
                    </div>
                    <div class="feature-card">
                        <h3>⚡ Interactive Elements</h3>
                        <p>
                            Bringing websites to life through meaningful
                            interactions that engage users and create memorable
                            digital experiences.
                        </p>
                    </div>
                    <div class="feature-card">
                        <h3>📱 Responsive Innovation</h3>
                        <p>
                            Ensuring seamless experiences across all devices,
                            from desktop to mobile, with adaptive design
                            principles at the core.
                        </p>
                    </div>
                </div>
            </section>

            <section class="section services">
                <h2>Our Services</h2>
                <p
                    style="
                        font-size: 1.2rem;
                        max-width: 800px;
                        line-height: 1.6;
                    "
                >
                    We offer comprehensive digital solutions that light up your
                    brand's potential and illuminate the path to success.
                </p>

                <div class="services-grid">
                    <div class="service-item">
                        <h3>🌐 Web Development</h3>
                        <p>
                            Custom websites that perform beautifully and
                            function flawlessly across all platforms and
                            devices.
                        </p>
                    </div>
                    <div class="service-item">
                        <h3>🎯 Digital Strategy</h3>
                        <p>
                            Strategic planning and execution to maximize your
                            digital presence and achieve measurable results.
                        </p>
                    </div>
                    <div class="service-item">
                        <h3>🚀 Performance Optimization</h3>
                        <p>
                            Lightning-fast loading times and optimal user
                            experiences through advanced optimization
                            techniques.
                        </p>
                    </div>
                    <div class="service-item">
                        <h3>💡 Creative Solutions</h3>
                        <p>
                            Innovative approaches to complex challenges,
                            bringing fresh perspectives to every project.
                        </p>
                    </div>
                </div>
            </section>

            <section class="section contact">
                <h2>Get In Touch</h2>
                <p
                    style="
                        font-size: 1.2rem;
                        max-width: 600px;
                        line-height: 1.6;
                    "
                >
                    Ready to illuminate your digital presence? Let's start a
                    conversation about bringing your vision to life.
                </p>

                <form class="contact-form">
                    <div class="form-group">
                        <label for="name">Name</label>
                        <input type="text" id="name" name="name" required />
                    </div>
                    <div class="form-group">
                        <label for="email">Email</label>
                        <input type="email" id="email" name="email" required />
                    </div>
                    <div class="form-group">
                        <label for="message">Message</label>
                        <textarea
                            id="message"
                            name="message"
                            required
                            placeholder="Tell us about your project..."
                        ></textarea>
                    </div>
                    <button type="submit" class="submit-btn">
                        Send Message
                    </button>
                </form>
            </section>
        </div>

        <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/Draggable.min.js"></script>

        <script>
            // Simple morphing animation without MorphSVGPlugin
            const { set, to, timeline } = gsap;

            // Used to calculate distance of "tug"
            let startX;
            let startY;

            const AUDIO = {
                CLICK: new Audio("https://assets.codepen.io/605876/click.mp3"),
            };

            const STATE = {
                ON: false,
            };

            const CORD_DURATION = 0.1;

            const CORDS = document.querySelectorAll(".toggle-scene__cord");
            const HIT = document.querySelector(".toggle-scene__hit-spot");
            const DUMMY = document.querySelector(".toggle-scene__dummy-cord");
            const DUMMY_CORD = document.querySelector(
                ".toggle-scene__dummy-cord line"
            );
            const PROXY = document.createElement("div");
            const WEBSITE_CONTENT = document.getElementById("websiteContent");
            const DARK_OVERLAY = document.getElementById("darkOverlay");

            // set init position
            const ENDX = DUMMY_CORD.getAttribute("x2");
            const ENDY = DUMMY_CORD.getAttribute("y2");

            const RESET = () => {
                set(PROXY, {
                    x: ENDX,
                    y: ENDY,
                });
            };

            RESET();

            const CORD_TL = timeline({
                paused: true,
                onStart: () => {
                    STATE.ON = !STATE.ON;
                    set(document.documentElement, { "--on": STATE.ON ? 1 : 0 });
                    set([DUMMY, HIT], { display: "none" });
                    set(CORDS[0], { display: "block" });

                    // Toggle website visibility
                    if (STATE.ON) {
                        WEBSITE_CONTENT.classList.add("visible");
                        DARK_OVERLAY.classList.add("hidden");
                    } else {
                        WEBSITE_CONTENT.classList.remove("visible");
                        DARK_OVERLAY.classList.remove("hidden");
                    }

                    AUDIO.CLICK.play();
                },
                onComplete: () => {
                    set([DUMMY, HIT], { display: "block" });
                    set(CORDS[0], { display: "none" });
                    RESET();
                },
            });

            // Simple cord animation without morphing
            for (let i = 1; i < CORDS.length; i++) {
                CORD_TL.add(
                    to(CORDS[0], {
                        opacity: 0.5,
                        duration: CORD_DURATION,
                        repeat: 1,
                        yoyo: true,
                    })
                );
            }

            gsap.registerPlugin(Draggable);

            Draggable.create(PROXY, {
                trigger: HIT,
                type: "x,y",
                onPress: (e) => {
                    startX = e.x;
                    startY = e.y;
                },
                onDrag: function () {
                    set(DUMMY_CORD, {
                        attr: {
                            x2: this.x,
                            y2: this.y,
                        },
                    });
                },
                onRelease: function (e) {
                    const DISTX = Math.abs(e.x - startX);
                    const DISTY = Math.abs(e.y - startY);
                    const TRAVELLED = Math.sqrt(DISTX * DISTX + DISTY * DISTY);
                    to(DUMMY_CORD, {
                        attr: { x2: ENDX, y2: ENDY },
                        duration: CORD_DURATION,
                        onComplete: () => {
                            if (TRAVELLED > 50) {
                                CORD_TL.restart();
                            } else {
                                RESET();
                            }
                        },
                    });
                },
            });

            // Smooth scrolling for navigation links
            document.addEventListener("click", function (e) {
                if (
                    e.target.getAttribute("href") &&
                    e.target.getAttribute("href").startsWith("#")
                ) {
                    e.preventDefault();
                    const target = document.querySelector(
                        e.target.getAttribute("href")
                    );
                    if (target) {
                        target.scrollIntoView({ behavior: "smooth" });
                    }
                }
            });

            // Form submission handler
            document
                .querySelector(".contact-form")
                .addEventListener("submit", function (e) {
                    e.preventDefault();
                    alert(
                        "Thank you for your message! We'll get back to you soon."
                    );
                    this.reset();
                });
        </script>
    </body>
</html>
