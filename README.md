import React, { useState } from 'react';
import { 
  Image as ImageIcon, Send, Heart, MessageCircle, Share2, 
  MoreHorizontal, Camera, X, ArrowRight, Sparkles, 
  CheckCircle2, Trash2, Layers, Lock, LayoutDashboard, Globe 
} from 'lucide-react';

/**
 * SocialPostApp: Suman Saurabh version with Private Creator Studio.
 * Posting is restricted to the Admin View with a simple password.
 */
export default function App() {
  const [view, setView] = useState('landing'); // 'landing', 'feed', 'admin'
  const [isAdmin, setIsAdmin] = useState(false);
  const [toast, setToast] = useState({ show: false, message: "" });
  const [passwordInput, setPasswordInput] = useState("");
  
  // App state for Posts
  const [posts, setPosts] = useState([
    {
      id: 1,
      user: "Suman Saurabh",
      content: "Welcome to my private feed! Only I can post here from the Creator Studio. 🔐✨",
      images: [
        "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?auto=format&fit=crop&w=800&q=80"
      ],
      timestamp: "1 hour ago",
      likes: 56,
      isLiked: false,
      comments: [
        { id: 101, user: "Amit", text: "This private setup is great!", timestamp: "10 mins ago" }
      ],
      showComments: false
    }
  ]);

  const [inputText, setInputText] = useState("");
  const [previewUrls, setPreviewUrls] = useState([]);

  const showToast = (msg) => {
    setToast({ show: true, message: msg });
    setTimeout(() => setToast({ show: false, message: "" }), 3000);
  };

  // Admin Login Logic
  const handleLogin = () => {
    if (passwordInput === "1234") { // Simple Password
      setIsAdmin(true);
      setView('admin');
      setPasswordInput("");
      showToast("Welcome back, Suman! 🔓");
    } else {
      showToast("Incorrect Password! ❌");
    }
  };

  const handleImageChange = (e) => {
    const files = Array.from(e.target.files);
    if (files.length > 0) {
      const newPreviews = files.map(file => URL.createObjectURL(file));
      setPreviewUrls(prev => [...prev, ...newPreviews]);
    }
  };

  const removePreviewImage = (index) => {
    const updatedPreviews = [...previewUrls];
    updatedPreviews.splice(index, 1);
    setPreviewUrls(updatedPreviews);
  };

  const handlePostSubmit = () => {
    if (!inputText && previewUrls.length === 0) return;

    const newPost = {
      id: Date.now(),
      user: "Suman Saurabh",
      content: inputText,
      images: previewUrls,
      timestamp: "Just now",
      likes: 0,
      isLiked: false,
      comments: [],
      showComments: false
    };

    setPosts([newPost, ...posts]);
    setInputText("");
    setPreviewUrls([]);
    setView('feed'); // Go to feed after posting
    showToast("Post shared successfully! 🚀");
  };

  const deletePost = (postId) => {
    setPosts(posts.filter(post => post.id !== postId));
    showToast("Post deleted successfully!");
  };

  const toggleLike = (postId) => {
    setPosts(posts.map(post => {
      if (post.id === postId) {
        return {
          ...post,
          isLiked: !post.isLiked,
          likes: post.isLiked ? post.likes - 1 : post.likes + 1
        };
      }
      return post;
    }));
  };

  const toggleComments = (postId) => {
    setPosts(posts.map(post => {
      if (post.id === postId) {
        return { ...post, showComments: !post.showComments };
      }
      return post;
    }));
  };

  const addComment = (postId, text) => {
    if (!text.trim()) return;
    setPosts(posts.map(post => {
      if (post.id === postId) {
        const newComment = {
          id: Date.now(),
          user: "Guest User",
          text: text,
          timestamp: "Just now"
        };
        return {
          ...post,
          comments: [...post.comments, newComment]
        };
      }
      return post;
    }));
  };

  const handleShare = async (post) => {
    const shareText = `Check out this post: "${post.content}"`;
    if (navigator.share) {
      try { await navigator.share({ title: "MyFeed", text: shareText, url: window.location.href }); } 
      catch (err) { copyToClipboard(shareText); }
    } else { copyToClipboard(shareText); }
  };

  const copyToClipboard = (text) => {
    const el = document.createElement("textarea");
    el.value = text;
    document.body.appendChild(el);
    el.select();
    document.execCommand('copy');
    document.body.removeChild(el);
    showToast("Copied to clipboard!");
  };

  if (view === 'landing') return <LandingPage onEnter={() => setView('feed')} />;

  return (
    <div className="min-h-screen bg-[#f8fafc] font-sans text-gray-900">
      {toast.show && (
        <div className="fixed top-20 left-1/2 -translate-x-1/2 z-[100] animate-bounce">
          <div className="bg-gray-900 text-white px-6 py-3 rounded-full shadow-2xl flex items-center space-x-2 border border-white/10">
            <CheckCircle2 className="w-5 h-5 text-green-400" />
            <span className="font-medium">{toast.message}</span>
          </div>
        </div>
      )}

      {/* Navigation Header */}
      <header className="sticky top-0 z-50 bg-white/90 backdrop-blur-lg border-b border-gray-200 shadow-sm">
        <div className="max-w-4xl mx-auto px-4 h-16 flex items-center justify-between">
          <div className="flex items-center space-x-8">
            <h1 className="text-2xl font-black text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-600 tracking-tight cursor-pointer" onClick={() => setView('landing')}>
              MyFeed
            </h1>
            <nav className="hidden md:flex space-x-1">
              <button 
                onClick={() => setView('feed')}
                className={`flex items-center space-x-2 px-4 py-2 rounded-lg font-bold transition-all ${view === 'feed' ? 'bg-blue-50 text-blue-600' : 'text-gray-500 hover:bg-gray-50'}`}
              >
                <Globe className="w-4 h-4" />
                <span>Public Feed</span>
              </button>
              <button 
                onClick={() => isAdmin ? setView('admin') : setView('login')}
                className={`flex items-center space-x-2 px-4 py-2 rounded-lg font-bold transition-all ${view === 'admin' ? 'bg-indigo-50 text-indigo-600' : 'text-gray-500 hover:bg-gray-50'}`}
              >
                <LayoutDashboard className="w-4 h-4" />
                <span>Creator Studio</span>
              </button>
            </nav>
          </div>
          <div className="flex items-center space-x-3">
            <span className="hidden sm:inline text-sm font-semibold text-gray-600">Suman Saurabh</span>
            <div className="w-10 h-10 rounded-full bg-blue-600 flex items-center justify-center text-white font-bold shadow-md">S</div>
          </div>
        </div>
      </header>

      {/* Main Content Area */}
      <main className="max-w-2xl mx-auto py-8 px-4">
        
        {/* LOGIN VIEW */}
        {view === 'login' && (
          <div className="bg-white p-8 rounded-3xl shadow-xl border border-gray-100 text-center animate-in zoom-in duration-300">
            <div className="w-16 h-16 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center mx-auto mb-4">
              <Lock className="w-8 h-8" />
            </div>
            <h2 className="text-2xl font-black mb-2">Creator Login</h2>
            <p className="text-gray-500 mb-6 italic">Sirf Suman Saurabh hi post kar sakte hain.</p>
            <div className="space-y-4">
              <input 
                type="password" 
                placeholder="Enter Secret Key"
                className="w-full px-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 outline-none text-center font-bold"
                value={passwordInput}
                onChange={(e) => setPasswordInput(e.target.value)}
                onKeyDown={(e) => e.key === 'Enter' && handleLogin()}
              />
              <button 
                onClick={handleLogin}
                className="w-full py-3 bg-blue-600 text-white font-bold rounded-xl shadow-lg hover:bg-blue-700 transition-all active:scale-95"
              >
                Access Studio
              </button>
            </div>
          </div>
        )}

        {/* ADMIN/CREATOR STUDIO VIEW */}
        {view === 'admin' && (
          <div className="animate-in slide-in-from-right duration-500">
            <div className="flex items-center justify-between mb-6">
              <h2 className="text-2xl font-black flex items-center">
                <LayoutDashboard className="w-6 h-6 mr-2 text-indigo-600" />
                Creator Studio
              </h2>
              <button onClick={() => setView('feed')} className="text-sm font-bold text-gray-500 hover:text-gray-800 underline">Back to Feed</button>
            </div>

            <div className="bg-white rounded-2xl shadow-lg p-6 mb-8 border border-white">
              <div className="flex space-x-4">
                <div className="w-12 h-12 rounded-full bg-indigo-50 flex-shrink-0 flex items-center justify-center text-indigo-600 font-bold text-lg">S</div>
                <div className="flex-1">
                  <textarea
                    placeholder="Suman, what's on your mind today? (Hindi or English)"
                    className="w-full border-none focus:ring-0 text-xl resize-none min-h-[120px] py-2 placeholder:text-gray-300 font-medium"
                    value={inputText}
                    onChange={(e) => setInputText(e.target.value)}
                  />
                  
                  {previewUrls.length > 0 && (
                    <div className="grid grid-cols-2 gap-2 mt-4">
                      {previewUrls.map((url, index) => (
                        <div key={index} className="relative rounded-xl overflow-hidden shadow-md border border-gray-100 h-40">
                          <img src={url} alt={`Preview ${index}`} className="w-full h-full object-cover" />
                          <button onClick={() => removePreviewImage(index)} className="absolute top-2 right-2 bg-black/60 p-1.5 rounded-full text-white hover:bg-black"><X className="w-4 h-4" /></button>
                        </div>
                      ))}
                      <label className="border-2 border-dashed border-gray-200 rounded-xl flex flex-col items-center justify-center cursor-pointer hover:bg-gray-50 h-40 transition-all">
                        <Layers className="w-6 h-6 text-gray-400 mb-1" />
                        <span className="text-xs font-bold text-gray-400">Add More</span>
                        <input type="file" accept="image/*" multiple className="hidden" onChange={handleImageChange} />
                      </label>
                    </div>
                  )}

                  <div className="flex items-center justify-between mt-6 pt-4 border-t border-gray-50">
                    <label className="cursor-pointer px-5 py-2.5 rounded-xl hover:bg-gray-50 flex items-center space-x-2 transition-all border border-gray-200">
                      <Camera className="w-5 h-5 text-indigo-500" />
                      <span className="text-sm font-bold text-gray-600">Select Media</span>
                      <input type="file" accept="image/*" multiple className="hidden" onChange={handleImageChange} />
                    </label>
                    <button 
                      onClick={handlePostSubmit}
                      disabled={!inputText && previewUrls.length === 0}
                      className={`px-10 py-3 rounded-xl font-bold transition-all flex items-center space-x-2 ${
                        (inputText || previewUrls.length > 0) ? "bg-indigo-600 text-white shadow-xl shadow-indigo-100 hover:brightness-110 active:scale-95" : "bg-gray-100 text-gray-400"
                      }`}
                    >
                      <Send className="w-4 h-4" />
                      <span>Post Now</span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        )}

        {/* PUBLIC FEED VIEW */}
        {view === 'feed' && (
          <div className="space-y-6 pb-20 animate-in fade-in duration-500">
            <div className="flex items-center justify-between mb-2">
              <h2 className="text-2xl font-black italic">Recent Updates</h2>
              {!isAdmin && (
                <button 
                  onClick={() => setView('login')}
                  className="text-xs font-bold text-gray-400 hover:text-indigo-600 flex items-center"
                >
                  <Lock className="w-3 h-3 mr-1" />
                  Creator Login
                </button>
              )}
            </div>

            {posts.map((post) => (
              <div key={post.id} className="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden hover:shadow-md transition-shadow">
                <div className="p-4 flex items-center justify-between">
                  <div className="flex items-center space-x-3">
                    <div className="w-10 h-10 rounded-full bg-gradient-to-tr from-blue-500 to-indigo-500 flex items-center justify-center text-white font-bold">{post.user[0]}</div>
                    <div>
                      <h3 className="font-bold text-gray-900 leading-tight">{post.user}</h3>
                      <p className="text-[10px] font-bold text-gray-400 uppercase tracking-widest">{post.timestamp}</p>
                    </div>
                  </div>
                  <div className="flex items-center space-x-2">
                    {isAdmin && (
                      <button onClick={() => deletePost(post.id)} className="p-2 text-gray-300 hover:text-red-500 transition-colors">
                        <Trash2 className="w-4 h-4" />
                      </button>
                    )}
                    <MoreHorizontal className="w-5 h-5 text-gray-300 cursor-pointer" />
                  </div>
                </div>

                <div className="px-5 pb-3">
                  <p className="text-gray-800 whitespace-pre-wrap leading-relaxed text-[16px]">{post.content}</p>
                </div>

                {post.images && post.images.length > 0 && (
                  <div className={`grid gap-1 border-y border-gray-50 ${post.images.length === 1 ? 'grid-cols-1' : 'grid-cols-2'}`}>
                    {post.images.map((img, i) => (
                      <img key={i} src={img} alt="" className={`w-full object-cover ${post.images.length === 1 ? 'h-auto max-h-[550px]' : 'h-72'}`} />
                    ))}
                  </div>
                )}

                <div className="px-2 py-1 flex items-center justify-around">
                  <button onClick={() => toggleLike(post.id)} className={`flex items-center space-x-2 px-6 py-3 rounded-xl transition-all ${post.isLiked ? "text-red-500 bg-red-50" : "text-gray-600 hover:bg-gray-50"}`}>
                    <Heart className={`w-5 h-5 ${post.isLiked ? "fill-current" : ""}`} />
                    <span className="font-bold text-sm">{post.likes}</span>
                  </button>
                  <button onClick={() => toggleComments(post.id)} className={`flex items-center space-x-2 px-6 py-3 rounded-xl transition-all ${post.showComments ? "text-blue-600 bg-blue-50" : "text-gray-600 hover:bg-gray-50"}`}>
                    <MessageCircle className="w-5 h-5" />
                    <span className="font-bold text-sm">{post.comments.length}</span>
                  </button>
                  <button onClick={() => handleShare(post)} className="flex items-center space-x-2 px-6 py-3 rounded-xl text-gray-600 hover:bg-gray-50 transition-all">
                    <Share2 className="w-5 h-5" />
                    <span className="font-bold text-sm">Share</span>
                  </button>
                </div>

                {post.showComments && (
                  <div className="bg-gray-50/50 p-4 border-t border-gray-100">
                    <div className="space-y-4 mb-4 max-h-60 overflow-y-auto pr-2 custom-scrollbar">
                      {post.comments.map(comment => (
                        <div key={comment.id} className="flex space-x-3">
                          <div className="w-8 h-8 rounded-full bg-gray-200 flex-shrink-0 flex items-center justify-center text-xs font-bold text-gray-500">{comment.user[0]}</div>
                          <div className="flex-1 bg-white p-3 rounded-2xl shadow-sm border border-gray-100">
                            <span className="text-xs font-bold text-gray-900 block">{comment.user}</span>
                            <p className="text-sm text-gray-700">{comment.text}</p>
                          </div>
                        </div>
                      ))}
                      {post.comments.length === 0 && <p className="text-center text-xs text-gray-400 py-2">Feel free to leave a comment!</p>}
                    </div>
                    <div className="flex items-center space-x-2 mt-2">
                      <input 
                        type="text" 
                        placeholder="Add a comment..."
                        className="flex-1 bg-white border border-gray-200 rounded-full px-4 py-2 text-sm focus:ring-2 focus:ring-blue-500 outline-none"
                        onKeyDown={(e) => {
                          if (e.key === 'Enter') {
                            addComment(post.id, e.target.value);
                            e.target.value = "";
                          }
                        }}
                      />
                    </div>
                  </div>
                )}
              </div>
            ))}
            {posts.length === 0 && (
              <div className="text-center py-24">
                <p className="text-gray-400 font-bold italic">Waiting for Suman to post something special...</p>
              </div>
            )}
          </div>
        )}
      </main>

      {/* Mobile Nav */}
      <div className="md:hidden fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 px-6 py-3 flex justify-around items-center z-50">
        <button onClick={() => setView('feed')} className={`p-2 rounded-xl ${view === 'feed' ? 'bg-blue-50 text-blue-600' : 'text-gray-400'}`}>
          <Globe className="w-6 h-6" />
        </button>
        <button 
          onClick={() => isAdmin ? setView('admin') : setView('login')} 
          className={`p-2 rounded-xl ${view === 'admin' || view === 'login' ? 'bg-indigo-50 text-indigo-600' : 'text-gray-400'}`}
        >
          <LayoutDashboard className="w-6 h-6" />
        </button>
      </div>
    </div>
  );
}

function LandingPage({ onEnter }) {
  return (
    <div className="min-h-screen w-full flex flex-col items-center justify-center overflow-hidden font-sans relative">
      <style>{`
        @keyframes gradientBG { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }
        @keyframes bounce-custom { 0%, 100% { transform: translateY(0) scale(1); } 50% { transform: translateY(-40px) scale(1.05); } }
        .animate-gradient { background: linear-gradient(-45deg, #4f46e5, #7c3aed, #db2777, #2563eb); background-size: 400% 400%; animation: gradientBG 15s ease infinite; }
        .cat-bounce { animation: bounce-custom 3s ease-in-out infinite; }
      `}</style>
      <div className="animate-gradient absolute inset-0 z-0"></div>
      <div className="z-10 text-center px-6">
        <div className="cat-bounce cursor-pointer relative group inline-block transform active:scale-90" onClick={onEnter}>
          <div className="absolute inset-0 bg-white/20 rounded-full blur-2xl group-hover:bg-white/40 transition-all duration-500 scale-150"></div>
          <div className="relative bg-white/10 backdrop-blur-md p-10 rounded-full border border-white/20 shadow-2xl">
            <span role="img" aria-label="cat" className="text-[140px] block drop-shadow-2xl select-none">🐱</span>
            <div className="absolute -bottom-2 -right-2 text-5xl transform rotate-12 drop-shadow-md">🐾</div>
          </div>
        </div>
        <div className="mt-12 text-white">
          <h1 className="text-5xl md:text-7xl font-black mb-4 tracking-tighter drop-shadow-lg italic">Suman's Feed</h1>
          <p className="text-xl md:text-2xl opacity-90 font-medium max-w-2xl mx-auto mb-10 leading-relaxed">The private collection of Suman Saurabh's moments.</p>
          <button onClick={onEnter} className="group relative inline-flex items-center px-10 py-5 font-bold text-white transition-all bg-white/10 backdrop-blur-md rounded-2xl border-2 border-white/50 hover:bg-white hover:text-indigo-600 shadow-xl">
            <Sparkles className="w-6 h-6 mr-3 text-yellow-300 group-hover:text-indigo-500" />
            <span className="text-xl">Enter Now</span>
            <ArrowRight className="ml-3 w-6 h-6 transform group-hover:translate-x-1 transition-transform" />
          </button>
        </div>
      </div>
      <div className="absolute bottom-8 text-white/40 text-[10px] font-bold tracking-[0.3em] uppercase">
        Personal Space • Protected with 1234
      </div>
    </div>
  );
}
