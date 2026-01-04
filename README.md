<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Suman Saurabh | Premium Global Feed</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; scroll-behavior: smooth; }
        .page-transition { animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1); }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes mesh { 0% { transform: translate(0, 0) scale(1); } 33% { transform: translate(30px, -50px) scale(1.1); } 66% { transform: translate(-20px, 20px) scale(0.9); } 100% { transform: translate(0, 0) scale(1); } }
        .animate-mesh { animation: mesh 12s ease-in-out infinite; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.3); }
        .hidden-view { display: none; }
        .custom-scroll::-webkit-scrollbar { width: 4px; }
        .custom-scroll::-webkit-scrollbar-thumb { background: #e2e8f0; border-radius: 10px; }
        .feed-card { transition: all 0.3s ease; }
        .feed-card:hover { transform: translateY(-2px); }
    </style>
</head>
<body class="bg-[#F3F4F6] text-slate-900 overflow-x-hidden">

    <!-- Global Notifications -->
    <div id="toast" class="fixed top-6 left-1/2 -translate-x-1/2 z-[300] transition-all transform -translate-y-32 opacity-0 pointer-events-none">
        <div class="bg-slate-900 text-white px-6 py-4 rounded-2xl shadow-2xl flex items-center space-x-3 border border-white/10 min-w-[300px]">
            <div id="toast-icon" class="bg-blue-500/20 p-2 rounded-xl text-blue-400">
                <i data-lucide="info" class="w-5 h-5"></i>
            </div>
            <span id="toast-message" class="font-bold text-sm">Message</span>
        </div>
    </div>

    <!-- VIEW 1: LANDING (PREMIUM ENTRANCE) -->
    <section id="view-landing" class="relative min-h-screen w-full flex items-center justify-center overflow-hidden bg-[#0F172A]">
        <div class="absolute inset-0 z-0">
            <div class="absolute top-[-10%] left-[-10%] w-[60%] h-[60%] bg-indigo-600/30 blur-[150px] rounded-full animate-mesh"></div>
            <div class="absolute bottom-[-10%] right-[-10%] w-[60%] h-[60%] bg-blue-600/20 blur-[150px] rounded-full animate-mesh" style="animation-delay: -4s;"></div>
        </div>
        
        <div class="z-10 text-center px-6 page-transition">
            <div class="cursor-pointer relative group inline-block transform active:scale-90 transition-all duration-500" onclick="navigateTo('feed')">
                <div class="absolute inset-0 bg-white/10 rounded-[3rem] blur-3xl group-hover:bg-white/20 transition-all scale-125"></div>
                <div class="relative glass p-12 rounded-[4rem] shadow-2xl border border-white/10">
                    <span class="text-[160px] block select-none drop-shadow-2xl filter brightness-110">🐱</span>
                    <div class="absolute -bottom-6 -right-6 text-7xl transform rotate-12 drop-shadow-xl animate-bounce">🐾</div>
                </div>
                <div class="mt-10 text-white/40 text-[10px] font-black uppercase tracking-[0.8em] animate-pulse">Touch to enter</div>
            </div>

            <div class="mt-16 text-white max-w-2xl mx-auto">
                <h1 class="text-7xl md:text-9xl font-black mb-6 tracking-tighter italic leading-none">
                    SUMAN<span class="text-blue-500">.</span>
                </h1>
                <p class="text-lg md:text-xl text-slate-400 font-medium mb-12 tracking-tight">The ultimate global feed for Suman Saurabh's creations.</p>
                <button onclick="navigateTo('feed')" class="bg-white text-slate-950 px-12 py-5 rounded-2xl font-black text-xl hover:bg-blue-500 hover:text-white transition-all transform hover:-translate-y-1 shadow-2xl flex items-center mx-auto space-x-3">
                    <span>Explore Feed</span>
                    <i data-lucide="arrow-right-circle" class="w-6 h-6"></i>
                </button>
            </div>
        </div>
    </section>

    <!-- MAIN APP WRAPPER -->
    <div id="view-app" class="hidden-view min-h-screen">
        <!-- Persistent Header -->
        <header class="sticky top-0 z-50 glass border-b border-slate-200 h-20">
            <div class="max-w-6xl mx-auto px-6 h-full flex items-center justify-between">
                <div class="flex items-center space-x-10">
                    <h2 class="text-2xl font-black tracking-tighter cursor-pointer flex items-center" onclick="navigateTo('landing')">
                        MYFEED<span class="text-blue-600">.</span>
                    </h2>
                    <nav class="hidden md:flex items-center space-x-1">
                        <button onclick="navigateTo('feed')" class="nav-btn p-btn-feed px-5 py-2 rounded-xl font-black text-sm transition-all text-slate-400 hover:text-slate-900 flex items-center space-x-2">
                            <i data-lucide="layout-grid" class="w-4 h-4"></i> <span>Feed</span>
                        </button>
                        <button onclick="handleAdminEntry()" class="nav-btn p-btn-admin px-5 py-2 rounded-xl font-black text-sm transition-all text-slate-400 hover:text-slate-900 flex items-center space-x-2">
                            <i data-lucide="shield-check" class="w-4 h-4"></i> <span>Studio</span>
                        </button>
                    </nav>
                </div>
                
                <div class="flex items-center space-x-4">
                    <div class="text-right hidden sm:block">
                        <p class="text-xs font-black text-slate-400 uppercase tracking-widest">Creator</p>
                        <p class="text-sm font-bold">Suman Saurabh</p>
                    </div>
                    <div class="w-11 h-11 bg-slate-900 text-white rounded-2xl flex items-center justify-center font-black shadow-lg border-2 border-white">S</div>
                </div>
            </div>
        </header>

        <!-- Dynamic Content Area -->
        <main class="max-w-6xl mx-auto px-6 py-10 grid grid-cols-1 lg:grid-cols-12 gap-10">
            <!-- Sidebar (Left) -->
            <aside class="hidden lg:block lg:col-span-3 space-y-6">
                <div class="bg-white p-8 rounded-[2.5rem] border border-slate-200 shadow-sm">
                    <h4 class="text-[10px] font-black text-slate-400 uppercase tracking-[0.3em] mb-6">Menu</h4>
                    <ul class="space-y-2">
                        <li><button onclick="navigateTo('feed')" class="w-full flex items-center space-x-3 p-3 rounded-xl hover:bg-slate-50 font-bold text-slate-600"><i data-lucide="home" class="w-4 h-4"></i> <span>Home</span></button></li>
                        <li><button onclick="handleAdminEntry()" class="w-full flex items-center space-x-3 p-3 rounded-xl hover:bg-slate-50 font-bold text-slate-600"><i data-lucide="plus-circle" class="w-4 h-4"></i> <span>New Post</span></button></li>
                        <li><button class="w-full flex items-center space-x-3 p-3 rounded-xl hover:bg-slate-50 font-bold text-slate-600"><i data-lucide="trending-up" class="w-4 h-4"></i> <span>Trending</span></button></li>
                    </ul>
                </div>
            </aside>

            <!-- Main Stream -->
            <div id="subview-container" class="lg:col-span-6 space-y-8 pb-32">
                <!-- Posts or Admin Views Injected Here -->
            </div>

            <!-- Profile Widget (Right) -->
            <aside class="hidden lg:block lg:col-span-3">
                <div class="bg-white p-8 rounded-[2.5rem] border border-slate-200 shadow-sm sticky top-28">
                    <div class="text-center mb-6">
                        <div class="w-20 h-20 bg-indigo-600 mx-auto rounded-3xl flex items-center justify-center text-white text-3xl font-black mb-4 shadow-xl shadow-indigo-100">S</div>
                        <h4 class="font-black text-xl tracking-tight">Suman Saurabh</h4>
                        <p class="text-xs font-bold text-blue-600 uppercase tracking-widest mt-1">Prime Creator</p>
                    </div>
                    <div class="grid grid-cols-2 gap-4 pt-6 border-t border-slate-100">
                        <div class="text-center">
                            <p id="stat-posts" class="text-xl font-black">0</p>
                            <p class="text-[10px] font-bold text-slate-400 uppercase">Posts</p>
                        </div>
                        <div class="text-center">
                            <p id="stat-likes" class="text-xl font-black">0</p>
                            <p class="text-[10px] font-bold text-slate-400 uppercase">Total Likes</p>
                        </div>
                    </div>
                </div>
            </aside>
        </main>
    </div>

    <!-- VIEW: LOGIN -->
    <div id="view-login" class="hidden-view min-h-screen flex items-center justify-center bg-slate-950 px-6">
        <div class="w-full max-w-md bg-white p-12 rounded-[3.5rem] shadow-2xl text-center page-transition">
            <div class="w-20 h-20 bg-blue-50 text-blue-600 rounded-[2rem] flex items-center justify-center mx-auto mb-8 shadow-xl shadow-blue-50 border-4 border-white">
                <i data-lucide="lock" class="w-10 h-10"></i>
            </div>
            <h2 class="text-3xl font-black mb-2 text-slate-900 tracking-tight">Access Control</h2>
            <p class="text-slate-400 font-medium mb-12 text-sm italic">Enter secret key to manage posts.</p>
            <div class="space-y-4">
                <input type="password" id="admin-pass" placeholder="Secret Key" class="w-full px-8 py-5 bg-slate-50 border-2 border-slate-100 rounded-2xl focus:border-blue-500 outline-none text-center text-2xl font-black tracking-[0.5em] transition-all">
                <div class="flex space-x-3">
                    <button onclick="navigateTo('feed')" class="flex-1 py-5 bg-slate-100 text-slate-500 font-bold rounded-2xl hover:bg-slate-200 transition-all">Cancel</button>
                    <button onclick="login()" class="flex-[2] py-5 bg-blue-600 text-white font-black rounded-2xl shadow-xl hover:bg-blue-700 active:scale-95 transition-all">Unlock Studio</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Mobile Navigation -->
    <div id="mobile-nav" class="md:hidden fixed bottom-6 left-6 right-6 h-18 glass rounded-[2.5rem] shadow-2xl flex items-center justify-around px-4 z-50 border border-white/20">
        <button onclick="navigateTo('feed')" class="p-4 text-slate-400"><i data-lucide="layout-grid" class="w-7 h-7"></i></button>
        <button onclick="handleAdminEntry()" class="w-14 h-14 -mt-10 bg-slate-900 text-white rounded-full flex items-center justify-center shadow-2xl shadow-slate-300 border-4 border-white transition-transform active:scale-90">
            <i data-lucide="plus" class="w-8 h-8"></i>
        </button>
        <button onclick="handleAdminEntry()" class="p-4 text-slate-400"><i data-lucide="user-check" class="w-7 h-7"></i></button>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithCustomToken, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, setDoc, addDoc, updateDoc, deleteDoc, onSnapshot, increment, arrayUnion } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // --- SETUP ---
        const firebaseConfig = JSON.parse(__firebase_config);
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'suman-saurabh-feed';

        let state = {
            view: 'landing',
            isAdmin: false,
            currentUser: null,
            posts: [],
            pendingImages: []
        };

        // --- AUTH ---
        async function initAuth() {
            if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                await signInWithCustomToken(auth, __initial_auth_token);
            } else {
                await signInAnonymously(auth);
            }
            onAuthStateChanged(auth, (user) => {
                state.currentUser = user;
                if (user) startRealtimeSync();
            });
        }
        initAuth();

        // --- DATABASE SYNC ---
        function startRealtimeSync() {
            const postsCol = collection(db, 'artifacts', appId, 'public', 'data', 'posts');
            onSnapshot(postsCol, (snap) => {
                state.posts = snap.docs.map(d => ({ id: d.id, ...d.data() }));
                // Sort by creation time (desc)
                state.posts.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));
                
                // Update stats
                document.getElementById('stat-posts').innerText = state.posts.length;
                document.getElementById('stat-likes').innerText = state.posts.reduce((acc, p) => acc + (p.likes || 0), 0);
                
                if (state.view === 'feed') renderFeed();
                if (state.view === 'studio') renderStudio();
            });
        }

        // --- NAVIGATION ENGINE ---
        window.navigateTo = (target) => {
            state.view = target;
            const views = ['view-landing', 'view-app', 'view-login'];
            views.forEach(v => document.getElementById(v).classList.add('hidden-view'));
            
            if (target === 'landing') document.getElementById('view-landing').classList.remove('hidden-view');
            else if (target === 'login') document.getElementById('view-login').classList.remove('hidden-view');
            else {
                document.getElementById('view-app').classList.remove('hidden-view');
                if (target === 'feed') renderFeed();
                if (target === 'studio') renderStudio();
            }

            // Update Nav Active States
            const btns = document.querySelectorAll('.nav-btn');
            btns.forEach(b => b.classList.replace('bg-slate-900', 'text-slate-400'));
            btns.forEach(b => b.classList.remove('text-white'));

            const activeBtn = target === 'feed' ? document.querySelector('.p-btn-feed') : document.querySelector('.p-btn-admin');
            if(activeBtn && target !== 'landing') {
                activeBtn.classList.replace('text-slate-400', 'bg-slate-900');
                activeBtn.classList.add('text-white');
            }

            lucide.createIcons();
            window.scrollTo({ top: 0, behavior: 'smooth' });
        };

        window.handleAdminEntry = () => {
            if (state.isAdmin) window.navigateTo('studio');
            else window.navigateTo('login');
        };

        window.login = () => {
            const pass = document.getElementById('admin-pass').value;
            if (pass === "1234") {
                state.isAdmin = true;
                showToast("Access Granted. Welcome Suman!", "success");
                window.navigateTo('studio');
            } else {
                showToast("Invalid Secret Key!", "error");
                document.getElementById('admin-pass').value = '';
            }
        };

        // --- NOTIFICATIONS ---
        function showToast(msg, type = "info") {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = msg;
            toast.classList.remove('opacity-0', 'pointer-events-none', '-translate-y-32');
            toast.classList.add('opacity-100', 'translate-y-0');
            setTimeout(() => {
                toast.classList.add('opacity-0', 'pointer-events-none', '-translate-y-32');
                toast.classList.remove('opacity-100', 'translate-y-0');
            }, 3000);
        }

        // --- UI RENDERERS ---
        function renderFeed() {
            const container = document.getElementById('subview-container');
            container.innerHTML = `
                <div class="mb-6 flex items-center justify-between">
                    <h3 class="text-3xl font-black tracking-tight italic">Recent Stories</h3>
                    ${!state.isAdmin ? `<button onclick="handleAdminEntry()" class="text-xs font-bold text-blue-600 hover:underline">Log in as Creator</button>` : ''}
                </div>
                <div class="space-y-8" id="posts-list"></div>
            `;

            const list = document.getElementById('posts-list');
            if (state.posts.length === 0) {
                list.innerHTML = `<div class="text-center py-24 bg-white rounded-[3rem] border-2 border-dashed border-slate-200"><p class="text-slate-400 font-bold uppercase tracking-widest text-xs italic">Nothing posted yet...</p></div>`;
                return;
            }

            state.posts.forEach(post => {
                const card = document.createElement('div');
                card.className = "bg-white rounded-[2.5rem] shadow-xl shadow-slate-200/50 border border-slate-100 overflow-hidden feed-card page-transition";
                
                let imageHTML = '';
                if (post.images && post.images.length > 0) {
                    const grid = post.images.length === 1 ? 'grid-cols-1' : (post.images.length === 2 ? 'grid-cols-2' : 'grid-cols-2');
                    imageHTML = `
                        <div class="grid ${grid} gap-1 bg-slate-100">
                            ${post.images.map(img => `<img src="${img}" class="w-full h-full object-cover ${post.images.length > 1 ? 'aspect-square' : 'max-h-[600px]'}">`).join('')}
                        </div>
                    `;
                }

                card.innerHTML = `
                    <div class="p-6 flex items-center justify-between">
                        <div class="flex items-center space-x-4">
                            <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-blue-600 to-indigo-600 flex items-center justify-center text-white font-black shadow-md border-2 border-white">S</div>
                            <div>
                                <h4 class="font-extrabold text-slate-900 tracking-tight leading-none">${post.user}</h4>
                                <p class="text-[10px] font-black text-blue-500 uppercase tracking-widest mt-1">Global Update</p>
                            </div>
                        </div>
                        <div class="flex items-center space-x-2">
                            ${state.isAdmin ? `<button onclick="window.deletePost('${post.id}')" class="p-2.5 text-slate-300 hover:text-red-500 hover:bg-red-50 rounded-xl transition-all"><i data-lucide="trash-2" class="w-5 h-5"></i></button>` : ''}
                            <i data-lucide="more-horizontal" class="text-slate-300"></i>
                        </div>
                    </div>
                    <div class="px-7 pb-5"><p class="text-slate-700 font-medium text-[17px] leading-relaxed">${post.content}</p></div>
                    ${imageHTML}
                    <div class="p-3 flex items-center justify-around border-t border-slate-50">
                        <button onclick="window.likePost('${post.id}')" class="flex items-center space-x-2 px-8 py-3.5 rounded-2xl font-bold transition-all text-slate-500 hover:bg-slate-50">
                            <i data-lucide="heart" class="w-5 h-5"></i> <span>${post.likes || 0}</span>
                        </button>
                        <button onclick="window.toggleComments('${post.id}')" class="flex items-center space-x-2 px-8 py-3.5 rounded-2xl font-bold text-slate-500 hover:bg-slate-50">
                            <i data-lucide="message-square" class="w-5 h-5"></i> <span>${post.comments ? post.comments.length : 0}</span>
                        </button>
                        <button onclick="window.sharePost('${post.id}')" class="flex items-center space-x-2 px-8 py-3.5 rounded-2xl font-bold text-slate-500 hover:bg-slate-50">
                            <i data-lucide="send" class="w-5 h-5"></i> <span>Share</span>
                        </button>
                    </div>
                    <div id="comments-${post.id}" class="hidden-view bg-slate-50/50 p-6 border-t border-slate-100">
                        <div class="space-y-4 mb-6" id="comment-list-${post.id}">
                            ${(post.comments || []).map(c => `
                                <div class="flex space-x-3">
                                    <div class="w-8 h-8 rounded-xl bg-slate-200 flex-shrink-0 flex items-center justify-center text-[10px] font-black text-slate-500">U</div>
                                    <div class="flex-1 bg-white p-4 rounded-[1.5rem] shadow-sm border border-slate-100">
                                        <p class="text-sm text-slate-600 font-medium">${c.text}</p>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                        <div class="flex items-center space-x-3">
                            <input type="text" id="input-${post.id}" placeholder="Kuch likhein..." class="flex-1 bg-white border border-slate-200 rounded-2xl px-5 py-3 text-sm focus:ring-4 focus:ring-blue-100 outline-none transition-all">
                            <button onclick="window.addComment('${post.id}')" class="bg-blue-600 text-white p-3 rounded-2xl shadow-lg shadow-blue-100"><i data-lucide="corner-down-left" class="w-4 h-4"></i></button>
                        </div>
                    </div>
                `;
                list.appendChild(card);
            });
            lucide.createIcons();
        }

        function renderStudio() {
            const container = document.getElementById('subview-container');
            container.innerHTML = `
                <div class="mb-10 page-transition">
                    <h2 class="text-4xl font-black text-slate-900 tracking-tight">Global Creator Studio</h2>
                    <p class="text-slate-400 font-bold italic mt-1 uppercase tracking-widest text-xs">Publish your next big update</p>
                </div>

                <div class="bg-white rounded-[3rem] shadow-2xl p-10 border border-white page-transition">
                    <textarea id="studio-text" placeholder="Share your thoughts... (English or Hindi)" class="w-full border-none focus:ring-0 text-2xl font-bold min-h-[160px] placeholder:text-slate-200 text-slate-800"></textarea>
                    <div id="image-previews" class="grid grid-cols-3 gap-3 mt-8"></div>
                    
                    <div class="flex flex-col md:flex-row md:items-center justify-between mt-10 pt-8 border-t border-slate-100 space-y-4 md:space-y-0">
                        <label class="cursor-pointer px-8 py-4 bg-slate-50 rounded-2xl border-2 border-dashed border-slate-200 flex items-center justify-center space-x-3 hover:bg-slate-100 transition-all">
                            <i data-lucide="image-plus" class="w-5 h-5 text-blue-600"></i>
                            <span class="text-xs font-black text-slate-600 uppercase tracking-widest">Select Photos</span>
                            <input type="file" multiple accept="image/*" class="hidden" id="file-input">
                        </label>
                        <button onclick="window.publishPost()" class="px-12 py-5 bg-slate-900 text-white font-black rounded-2xl shadow-2xl hover:bg-blue-600 transition-all flex items-center justify-center space-x-3 text-lg">
                            <i data-lucide="globe" class="w-5 h-5"></i>
                            <span>Publish to World</span>
                        </button>
                    </div>
                </div>
            `;

            document.getElementById('file-input').onchange = (e) => {
                const files = Array.from(e.target.files);
                files.forEach(file => {
                    const reader = new FileReader();
                    reader.onload = (ev) => {
                        state.pendingImages.push(ev.target.result);
                        updatePreviews();
                    };
                    reader.readAsDataURL(file);
                });
            };

            function updatePreviews() {
                const grid = document.getElementById('image-previews');
                grid.innerHTML = state.pendingImages.map((img, i) => `
                    <div class="relative rounded-2xl overflow-hidden aspect-square border-4 border-white shadow-md">
                        <img src="${img}" class="w-full h-full object-cover">
                        <button onclick="window.removePending(${i})" class="absolute top-2 right-2 bg-red-500 text-white p-1 rounded-xl"><i data-lucide="x" class="w-4 h-4"></i></button>
                    </div>
                `).join('');
                lucide.createIcons();
            }

            window.removePending = (idx) => {
                state.pendingImages.splice(idx, 1);
                updatePreviews();
            };

            lucide.createIcons();
        }

        // --- GLOBAL ACTIONS ---
        window.publishPost = async () => {
            const text = document.getElementById('studio-text').value;
            if (!text && state.pendingImages.length === 0) return;
            
            showToast("Publishing post...", "info");
            try {
                const postsCol = collection(db, 'artifacts', appId, 'public', 'data', 'posts');
                await addDoc(postsCol, {
                    user: "Suman Saurabh",
                    content: text,
                    images: [...state.pendingImages],
                    likes: 0,
                    comments: [],
                    createdAt: Date.now()
                });
                state.pendingImages = [];
                showToast("Post is now LIVE! 🌍", "success");
                window.navigateTo('feed');
            } catch (e) {
                showToast("Upload failed!", "error");
            }
        };

        window.likePost = async (id) => {
            const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', id);
            await updateDoc(postRef, { likes: increment(1) });
        };

        window.deletePost = async (id) => {
            if (!state.isAdmin) return;
            await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'posts', id));
            showToast("Post removed from feed.");
        };

        window.addComment = async (id) => {
            const input = document.getElementById(`input-${id}`);
            const text = input.value.trim();
            if(!text) return;
            
            const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', id);
            await updateDoc(postRef, {
                comments: arrayUnion({ text: text, user: "Guest", createdAt: Date.now() })
            });
            input.value = '';
            showToast("Comment added!");
        };

        window.toggleComments = (id) => {
            const el = document.getElementById(`comments-${id}`);
            el.classList.toggle('hidden-view');
        };

        window.sharePost = (id) => {
            const p = state.posts.find(x => x.id === id);
            const text = `Suman Saurabh's Story: ${p.content}`;
            if(navigator.share) navigator.share({ text: text, url: window.location.href });
            else {
                const el = document.createElement('textarea');
                el.value = text; document.body.appendChild(el); el.select();
                document.execCommand('copy'); document.body.removeChild(el);
                showToast("Post link copied!");
            }
        };

        // Initialize Icons
        lucide.createIcons();
    </script>
</body>
</html>
