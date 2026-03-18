 
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Transmobility Excellence | VTC Prestige Vendée</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Syncopate:wght@400;700&family=Plus+Jakarta+Sans:wght@200;300;400;700;800&display=swap');

        :root {
            --electric-green: #00ff88;
            --deep-black: #050505;
            --gold-subtle: #d4af37;
        }

        body {
            background-color: var(--deep-black);
            color: #ffffff;
            font-family: 'Plus Jakarta Sans', sans-serif;
            overflow-x: hidden;
            line-height: 1.6;
        }

        .font-syncopate { font-family: 'Syncopate', sans-serif; }

        /* Curseur de luxe */
        #cursor {
            width: 12px;
            height: 12px;
            background: var(--electric-green);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 10000;
            transition: transform 0.15s ease-out;
            box-shadow: 0 0 15px var(--electric-green);
        }

        /* Effet de brillance sur le texte */
        .shimmer {
            background: linear-gradient(90deg, #fff 0%, #444 50%, #fff 100%);
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: shine 5s linear infinite;
        }

        @keyframes shine {
            to { background-position: 200% center; }
        }

        /* Glassmorphism Avancé */
        .glass-ultra {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(30px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        .text-outline {
            -webkit-text-stroke: 1px rgba(255,255,255,0.2);
            color: transparent;
            transition: all 0.5s ease;
        }
        
        .text-outline:hover {
            -webkit-text-stroke: 1px var(--electric-green);
        }

        /* Silhouettes Véhicules */
        .vehicle-silhouette {
            width: 100%;
            border-radius: 4rem;
            background: radial-gradient(circle at center, #111 0%, #050505 100%);
            aspect-ratio: 21 / 9;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid rgba(255,255,255,0.02);
            overflow: hidden;
        }

        .silhouette-icon {
            font-size: 10rem;
            color: rgba(255,255,255,0.02);
            filter: blur(1px);
        }

        /* Floating Booking Button */
        .float-book {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            z-index: 1000;
            background: var(--electric-green);
            color: black;
            padding: 1rem 1.5rem;
            border-radius: 50px;
            font-weight: 800;
            font-size: 0.75rem;
            letter-spacing: 1px;
            box-shadow: 0 10px 30px rgba(0, 255, 136, 0.3);
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .float-book:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 15px 40px rgba(0, 255, 136, 0.5);
        }

        /* Animations de chargement */
        #loader {
            position: fixed;
            inset: 0;
            background: var(--deep-black);
            z-index: 9999;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .star-active { color: var(--electric-green); text-shadow: 0 0 10px rgba(0, 255, 136, 0.5); }
    </style>
</head>
<body class="antialiased">

    <div id="loader" class="font-syncopate text-xs tracking-[10px] animate-pulse">TRANSMOBILITY</div>
    <div id="cursor" class="hidden md:block"></div>
    
    <!-- Bouton de réservation flottant -->
    <a href="https://wa.me/33665103118" class="float-book md:hidden">
        <i class="fab fa-whatsapp text-lg"></i> RÉSERVER
    </a>

    <!-- Menu Overlay -->
    <div id="menu-overlay" class="fixed inset-0 bg-black z-[150] flex items-center justify-center pointer-events-none opacity-0 transition-all duration-700" style="clip-path: circle(0% at 95% 5%);">
        <div class="text-center space-y-12">
            <a href="#services" class="nav-item close-menu text-4xl font-syncopate font-bold block hover:text-[#00ff88]">SERVICES</a>
            <a href="#flotte" class="nav-item close-menu text-4xl font-syncopate font-bold block hover:text-[#00ff88]">LA FLOTTE</a>
            <a href="#avis" class="nav-item close-menu text-4xl font-syncopate font-bold block hover:text-[#00ff88]">AVIS</a>
            <a href="#contact" class="nav-item close-menu text-4xl font-syncopate font-bold block hover:text-[#00ff88]">CONTACT</a>
        </div>
    </div>

    <!-- Header -->
    <header class="fixed w-full z-[200] px-10 py-8 flex justify-between items-center transition-all duration-500" id="main-header">
        <div class="text-2xl font-syncopate font-bold tracking-tighter mix-blend-difference">
            TRANS<span class="text-[#00ff88]">MOBILITY</span>
        </div>
        <div class="flex items-center gap-10">
             <a href="tel:0665103118" class="hidden lg:flex items-center gap-3 text-[10px] font-bold tracking-[4px] mix-blend-difference hover:text-[#00ff88] transition-colors">
                <span class="w-2 h-2 bg-[#00ff88] rounded-full animate-ping"></span>
                06 65 10 31 18
             </a>
             <button id="menu-toggle" class="glass-ultra p-5 rounded-full group relative z-[201] hover:bg-white/10 transition-all">
                <div id="bar1" class="w-6 h-0.5 bg-white mb-2 transition-all"></div>
                <div id="bar2" class="w-6 h-0.5 bg-white transition-all"></div>
            </button>
        </div>
    </header>

    <main>
        
        <!-- Hero Section Excellence -->
        <section class="min-h-screen flex items-center px-10 relative overflow-hidden">
            <div class="absolute -right-[10%] top-[20%] w-[60%] h-[60%] bg-[#00ff88]/5 rounded-full blur-[150px] pointer-events-none"></div>
            
            <div class="container mx-auto grid lg:grid-cols-12 gap-20 items-center">
                <div class="lg:col-span-7">
                    <div class="overflow-hidden mb-6">
                        <span class="text-[#00ff88] font-bold tracking-[10px] uppercase text-[11px] block hero-anim translate-y-full">Conciergerie & Transport Privé</span>
                    </div>
                    <h1 class="text-[clamp(3.5rem,9vw,8rem)] font-syncopate font-bold leading-[0.85] mb-12 hero-anim opacity-0">
                        L'ART DE <br> <span class="text-outline shimmer">VOYAGER</span>
                    </h1>
                    <div class="flex gap-10 items-center hero-anim opacity-0">
                        <div class="w-16 h-[2px] bg-[#00ff88]"></div>
                        <p class="text-gray-400 max-w-md text-xs uppercase tracking-[3px] font-medium leading-relaxed">
                            Chauffeur d'excellence en Vendée. Ponctualité, discrétion et véhicules de dernière génération.
                        </p>
                    </div>
                </div>

                <!-- Estimation de trajet Premium -->
                <div class="lg:col-span-5 hero-anim opacity-0">
                    <div class="glass-ultra p-12 rounded-[4rem] relative group">
                        <div class="absolute -inset-1 bg-gradient-to-r from-[#00ff88]/20 to-transparent rounded-[4rem] blur opacity-0 group-hover:opacity-100 transition duration-1000"></div>
                        <div class="relative">
                            <h3 class="text-sm font-bold mb-10 uppercase tracking-[6px] font-syncopate border-b border-white/10 pb-4">Réservation Express</h3>
                            <div class="space-y-8">
                                <div class="group/input">
                                    <label class="text-[9px] uppercase text-gray-500 font-black tracking-widest block mb-2 group-focus-within/input:text-[#00ff88] transition-colors">Type de Mission</label>
                                    <select class="w-full bg-transparent py-3 focus:outline-none text-sm appearance-none cursor-pointer border-b border-white/10">
                                        <option class="bg-black">Transfert Gare / Aéroport</option>
                                        <option class="bg-black">Arena / Vendée Espace</option>
                                        <option class="bg-black">Mise à disposition VIP</option>
                                        <option class="bg-black">Cérémonie & Mariage</option>
                                    </select>
                                </div>
                                <div class="group/input">
                                    <label class="text-[9px] uppercase text-gray-500 font-black tracking-widest block mb-2 group-focus-within/input:text-[#00ff88] transition-colors">Lieu de prise en charge</label>
                                    <input type="text" placeholder="Ex: La Roche-sur-Yon" class="w-full bg-transparent py-3 border-b border-white/10 focus:outline-none text-sm placeholder:text-white/20">
                                </div>
                                <button onclick="window.location.href='https://wa.me/33665103118'" class="w-full bg-white text-black py-5 rounded-full font-black text-[10px] tracking-[4px] uppercase hover:bg-[#00ff88] transition-all duration-500 transform hover:scale-[1.02]">
                                    Demander un devis
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Scroll Indicator -->
            <div class="absolute bottom-10 left-10 flex flex-col items-center gap-4 opacity-30">
                <span class="text-[8px] uppercase tracking-[4px] [writing-mode:vertical-lr]">Découvrir</span>
                <div class="w-px h-20 bg-gradient-to-b from-white to-transparent"></div>
            </div>
        </section>

        <!-- Section Témoignages Premium -->
        <section id="avis" class="py-40 border-t border-white/5 bg-black/50">
            <div class="container mx-auto px-10">
                <div class="text-center mb-24 reveal">
                    <span class="text-[#00ff88] font-bold tracking-[8px] uppercase text-[10px] mb-4 block">Confiance</span>
                    <h2 class="text-5xl md:text-7xl font-syncopate font-bold">ILS NOUS <br> <span class="text-outline">PLÉBISCITENT</span></h2>
                </div>

                <div class="grid lg:grid-cols-3 gap-10">
                    <div class="glass-ultra p-12 rounded-[3.5rem] reveal hover:border-[#00ff88]/30 transition-colors group">
                        <div class="flex gap-2 mb-8 group-hover:scale-110 transition-transform duration-500">
                            <i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i>
                        </div>
                        <p class="text-gray-300 text-sm leading-relaxed mb-10 font-light">"Une prestation d'une rare qualité. Le chauffeur était en avance, le véhicule Tesla impeccable. Un trajet silencieux et reposant vers Nantes."</p>
                        <div class="flex items-center gap-5">
                            <div class="w-12 h-12 rounded-full bg-gradient-to-br from-white/10 to-transparent flex items-center justify-center font-bold text-xs border border-white/10">AM</div>
                            <div>
                                <h5 class="text-xs font-bold uppercase tracking-widest">Alain M.</h5>
                                <p class="text-[9px] text-[#00ff88] uppercase tracking-widest mt-1">Dirigeant Entreprise</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="glass-ultra p-12 rounded-[3.5rem] reveal hover:border-[#00ff88]/30 transition-colors group" style="transition-delay: 0.2s">
                        <div class="flex gap-2 mb-8 group-hover:scale-110 transition-transform duration-500">
                            <i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i>
                        </div>
                        <p class="text-gray-300 text-sm leading-relaxed mb-10 font-light">"Nous avons utilisé le Van pour un événement à l'Arena des Sables. Organisation parfaite, chauffeur très courtois. L'excellence vendéenne."</p>
                        <div class="flex items-center gap-5">
                            <div class="w-12 h-12 rounded-full bg-gradient-to-br from-white/10 to-transparent flex items-center justify-center font-bold text-xs border border-white/10">CL</div>
                            <div>
                                <h5 class="text-xs font-bold uppercase tracking-widest">Claire L.</h5>
                                <p class="text-[9px] text-[#00ff88] uppercase tracking-widest mt-1">Événementiel</p>
                            </div>
                        </div>
                    </div>

                    <div class="glass-ultra p-12 rounded-[3.5rem] reveal hover:border-[#00ff88]/30 transition-colors group" style="transition-delay: 0.4s">
                        <div class="flex gap-2 mb-8 group-hover:scale-110 transition-transform duration-500">
                            <i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i><i class="fas fa-star star-active"></i>
                        </div>
                        <p class="text-gray-300 text-sm leading-relaxed mb-10 font-light">"Le service est d'une fiabilité totale. Réservation simple et confirmation immédiate. Je ne passe plus que par Transmobility."</p>
                        <div class="flex items-center gap-5">
                            <div class="w-12 h-12 rounded-full bg-gradient-to-br from-white/10 to-transparent flex items-center justify-center font-bold text-xs border border-white/10">DR</div>
                            <div>
                                <h5 class="text-xs font-bold uppercase tracking-widest">David R.</h5>
                                <p class="text-[9px] text-[#00ff88] uppercase tracking-widest mt-1">Client Fidèle</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section Services Haute Conciergerie -->
        <section id="services" class="py-40 relative">
            <div class="container mx-auto px-10">
                <div class="grid lg:grid-cols-4 gap-8">
                    <div class="lg:col-span-2 reveal">
                        <span class="text-[#00ff88] font-bold tracking-[6px] uppercase text-[10px] mb-4 block">Missions</span>
                        <h2 class="text-5xl font-syncopate font-bold leading-tight">NOS DOMAINES <br> DE <span class="text-outline">PRÉDILECTION</span></h2>
                    </div>
                    <div class="glass-ultra p-12 rounded-[3rem] reveal group hover:bg-white/5 transition-all">
                        <div class="text-[#00ff88] mb-8 text-2xl group-hover:rotate-12 transition-transform"><i class="fas fa-microphone-alt"></i></div>
                        <h4 class="text-lg font-bold font-syncopate mb-5 tracking-tighter">ARENA & V. ESPACE</h4>
                        <p class="text-gray-500 text-xs leading-relaxed uppercase tracking-widest">Logistique VIP pour vos concerts et matchs. Accès coupe-file et attente personnalisée.</p>
                    </div>
                    <div class="glass-ultra p-12 rounded-[3rem] reveal group hover:bg-white/5 transition-all" style="transition-delay: 0.2s">
                        <div class="text-[#00ff88] mb-8 text-2xl group-hover:rotate-12 transition-transform"><i class="fas fa-plane-arrival"></i></div>
                        <h4 class="text-lg font-bold font-syncopate mb-5 tracking-tighter">TRANSFERS HUB</h4>
                        <p class="text-gray-500 text-xs leading-relaxed uppercase tracking-widest">Connexions gares & aéroports (Nantes, La Rochelle). Accueil nominatif en zone réservée.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section Flotte Excellence -->
        <section id="flotte" class="py-32 bg-white text-black rounded-t-[6rem] shadow-[0_-30px_100px_rgba(0,0,0,0.5)]">
            <div class="container mx-auto px-10">
                <!-- TESLA -->
                <div class="flex flex-col lg:flex-row gap-20 items-center mb-40 reveal">
                    <div class="flex-1 order-2 lg:order-1">
                        <span class="text-gray-400 font-bold tracking-[8px] uppercase text-[10px] mb-4 block">Signature Électrique</span>
                        <h2 class="text-6xl font-syncopate font-bold mb-8">TESLA <br> MODEL 3</h2>
                        <p class="text-gray-500 mb-10 max-w-md leading-relaxed">L'alliance parfaite de la technologie et du silence. Pour vos déplacements urbains ou longue distance avec une empreinte carbone nulle.</p>
                        <div class="flex gap-4">
                            <span class="px-6 py-3 border border-black/10 rounded-full text-[9px] font-black uppercase tracking-widest">Toit Panoramique</span>
                            <span class="px-6 py-3 border border-black/10 rounded-full text-[9px] font-black uppercase tracking-widest">Cuir Premium</span>
                        </div>
                    </div>
                    <div class="flex-1 order-1 lg:order-2">
                        <div class="vehicle-silhouette group">
                            <i class="fas fa-car-side silhouette-icon group-hover:scale-110 transition-transform duration-1000"></i>
                            <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
                                <span class="text-[15rem] font-syncopate font-black opacity-[0.03] select-none">T3</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- MERCEDES EQV -->
                <div class="flex flex-col lg:flex-row gap-20 items-center reveal">
                    <div class="flex-1">
                        <div class="vehicle-silhouette group">
                            <i class="fas fa-shuttle-van silhouette-icon group-hover:scale-110 transition-transform duration-1000"></i>
                            <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
                                <span class="text-[15rem] font-syncopate font-black opacity-[0.03] select-none">EQV</span>
                            </div>
                        </div>
                    </div>
                    <div class="flex-1">
                        <span class="text-gray-400 font-bold tracking-[8px] uppercase text-[10px] mb-4 block">Lounge Mobile</span>
                        <h2 class="text-6xl font-syncopate font-bold mb-8">MERCEDES <br> VAN EQV</h2>
                        <p class="text-gray-500 mb-10 max-w-md leading-relaxed">Conçu pour les délégations et les familles exigeantes. Jusqu'à 7 passagers dans un confort de première classe.</p>
                        <div class="grid grid-cols-2 gap-6">
                            <div class="bg-gray-50 p-8 rounded-[2rem]">
                                <span class="block text-4xl font-black mb-1">07</span>
                                <span class="text-[9px] uppercase font-bold text-gray-400 tracking-[3px]">Passagers</span>
                            </div>
                            <div class="bg-gray-50 p-8 rounded-[2rem]">
                                <span class="block text-4xl font-black mb-1">VIP</span>
                                <span class="text-[9px] uppercase font-bold text-gray-400 tracking-[3px]">Service</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section Contact / Call to Action Final -->
        <section id="contact" class="py-40">
            <div class="container mx-auto px-10">
                <div class="glass-ultra rounded-[5rem] overflow-hidden p-1 bg-gradient-to-br from-[#00ff88]/20 to-transparent">
                    <div class="bg-[#050505] rounded-[4.9rem] p-16 md:p-24 flex flex-col lg:flex-row items-center gap-20">
                        <div class="flex-1 reveal">
                            <h2 class="text-5xl md:text-7xl font-syncopate font-bold mb-8 leading-tight">VOTRE <br> PROCHAINE <br> <span class="text-[#00ff88]">DESTINATION</span></h2>
                            <div class="flex items-center gap-10">
                                <div class="w-16 h-[1px] bg-white/20"></div>
                                <a href="tel:0665103118" class="text-3xl font-bold hover:text-[#00ff88] transition-colors">06 65 10 31 18</a>
                            </div>
                        </div>
                        <div class="reveal flex flex-col items-center gap-8">
                            <div class="bg-white p-10 rounded-[4rem] shadow-[0_0_100px_rgba(0,255,136,0.1)] group">
                                <img src="https://api.qrserver.com/v1/create-qr-code/?size=250x250&data=https://wa.me/33665103118&color=000000" alt="QR Code" class="w-48 h-48 group-hover:scale-105 transition-transform duration-500">
                            </div>
                            <span class="text-[10px] font-black uppercase tracking-[8px] text-[#00ff88] animate-pulse">Scan & Chat</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="py-20 border-t border-white/5 px-10">
        <div class="container mx-auto flex flex-col lg:flex-row justify-between items-center gap-10">
            <div class="text-lg font-syncopate font-bold tracking-tighter">TRANS<span class="text-[#00ff88]">MOBILITY</span></div>
            <div class="flex gap-10">
                <a href="#" class="text-[9px] uppercase tracking-[4px] opacity-40 hover:opacity-100 transition-opacity">Mentions Légales</a>
                <a href="#" class="text-[9px] uppercase tracking-[4px] opacity-40 hover:opacity-100 transition-opacity">Conditions de Transport</a>
            </div>
            <div class="text-[10px] font-medium text-gray-500">© 2024. EXCELLENCE VENDÉENNE.</div>
        </div>
    </footer>

    <script>
        // Loader
        window.addEventListener('load', () => {
            gsap.to("#loader", { opacity: 0, duration: 1, delay: 1, onComplete: () => {
                document.getElementById('loader').style.display = 'none';
                initAnimations();
            }});
        });

        // Curseur Custom
        const cursor = document.getElementById('cursor');
        document.addEventListener('mousemove', (e) => {
            cursor.style.left = e.clientX + 'px';
            cursor.style.top = e.clientY + 'px';
        });

        document.querySelectorAll('a, button').forEach(el => {
            el.addEventListener('mouseenter', () => cursor.style.transform = 'scale(4)');
            el.addEventListener('mouseleave', () => cursor.style.transform = 'scale(1)');
        });

        // Menu Toggle Logic
        const menuBtn = document.getElementById('menu-toggle');
        const menuOverlay = document.getElementById('menu-overlay');
        const b1 = document.getElementById('bar1');
        const b2 = document.getElementById('bar2');

        menuBtn.addEventListener('click', () => {
            const isActive = menuOverlay.style.clipPath.includes('150%');
            if (!isActive) {
                menuOverlay.style.clipPath = 'circle(150% at 95% 5%)';
                menuOverlay.style.opacity = '1';
                menuOverlay.style.pointerEvents = 'all';
                b1.style.transform = 'rotate(45deg) translateY(10px)';
                b2.style.transform = 'rotate(-45deg) translateY(-10px)';
            } else {
                closeMenu();
            }
        });

        function closeMenu() {
            menuOverlay.style.clipPath = 'circle(0% at 95% 5%)';
            menuOverlay.style.opacity = '0';
            menuOverlay.style.pointerEvents = 'none';
            b1.style.transform = 'none';
            b2.style.transform = 'none';
        }

        document.querySelectorAll('.close-menu').forEach(l => l.addEventListener('click', closeMenu));

        // GSAP Animations
        function initAnimations() {
            gsap.registerPlugin(ScrollTrigger);

            gsap.to(".hero-anim", {
                opacity: 1,
                y: 0,
                duration: 1.5,
                stagger: 0.2,
                ease: "expo.out"
            });

            gsap.utils.toArray('.reveal').forEach(el => {
                gsap.from(el, {
                    scrollTrigger: {
                        trigger: el,
                        start: "top 90%",
                    },
                    y: 80,
                    opacity: 0,
                    duration: 1.5,
                    ease: "power4.out"
                });
            });

            // Sticky Header Blur
            ScrollTrigger.create({
                start: "top -100",
                onUpdate: (self) => {
                    if (self.direction === 1) {
                        document.getElementById('main-header').classList.add('glass-ultra', 'py-4');
                    } else {
                        document.getElementById('main-header').classList.remove('glass-ultra', 'py-4');
                    }
                }
            });
        }
    </script>
</body>
</html>
