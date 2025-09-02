# LINL. DONI. VIPZEXNET 
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>برنامه لینکونی</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">
    <style>
        body {
            background-color: #f8f9fa;
            font-family: 'Vazir', sans-serif;
        }
        .navbar-brand {
            font-weight: bold;
        }
        .banner-container {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            border-radius: 10px;
            padding: 20px;
            color: white;
            margin-bottom: 20px;
        }
        .chat-container {
            height: 400px;
            overflow-y: auto;
            border: 1px solid #ddd;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 15px;
            background-color: #f9f9f9;
        }
        .message {
            padding: 10px;
            margin: 5px 0;
            border-radius: 10px;
            max-width: 80%;
        }
        .user-message {
            background-color: #d1ecf1;
            margin-left: auto;
            text-align: left;
        }
        .admin-message {
            background-color: #f8d7da;
            margin-right: auto;
            text-align: right;
        }
        .login-container {
            max-width: 400px;
            margin: 100px auto;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            background-color: white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .admin-panel {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .banner-card {
            transition: transform 0.3s;
        }
        .banner-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
    </style>
</head>
<body>
    <!-- نوار ناوبری -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
        <div class="container">
            <a class="navbar-brand" href="#">لینکونی</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav me-auto">
                    <li class="nav-item">
                        <a class="nav-link active" href="#" onclick="showPage('home')">صفحه اصلی</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" onclick="showPage('banner-register')">ثبت بنر</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" onclick="showPage('chat-room')">چت روم</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" onclick="showPage('message-inbox')">صندوق پیام</a>
                    </li>
                </ul>
                <div class="d-flex">
                    <button class="btn btn-outline-light" onclick="showPage('admin-login')">ورود ادمین</button>
                </div>
            </div>
        </div>
    </nav>

    <div class="container mt-4">
        <!-- صفحه اصلی -->
        <div id="home-page" class="page">
            <div class="banner-container text-center">
                <h2>به برنامه لینکونی خوش آمدید</h2>
                <p>سیستم مدیریت بنر و پیام</p>
            </div>
            
            <h4 class="mb-3">بنرهای کاربران</h4>
            <div id="banners-container" class="row">
                <!-- بنرها در اینجا نمایش داده می شوند -->
            </div>
        </div>

        <!-- صفحه ثبت بنر -->
        <div id="banner-register-page" class="page" style="display: none;">
            <div class="card">
                <div class="card-header bg-primary text-white">
                    <h5>ثبت بنر جدید</h5>
                </div>
                <div class="card-body">
                    <form id="banner-form">
                        <div class="mb-3">
                            <label for="banner-title" class="form-label">عنوان بنر</label>
                            <input type="text" class="form-control" id="banner-title" required>
                        </div>
                        <div class="mb-3">
                            <label for="banner-url" class="form-label">لینک بنر</label>
                            <input type="url" class="form-control" id="banner-url" required>
                        </div>
                        <div class="mb-3">
                            <label for="banner-image" class="form-label">آدرس تصویر بنر</label>
                            <input type="url" class="form-control" id="banner-image" required>
                        </div>
                        <button type="submit" class="btn btn-primary">ثبت بنر</button>
                    </form>
                </div>
            </div>
        </div>

        <!-- صفحه چت روم -->
        <div id="chat-room-page" class="page" style="display: none;">
            <div class="card">
                <div class="card-header bg-success text-white">
                    <h5>چت روم کاربران</h5>
                </div>
                <div class="card-body">
                    <div id="chat-messages" class="chat-container">
                        <!-- پیام های چت در اینجا نمایش داده می شوند -->
                    </div>
                    <div class="input-group">
                        <input type="text" id="chat-input" class="form-control" placeholder="پیام خود را بنویسید...">
                        <button class="btn btn-success" onclick="sendMessage()">ارسال</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- صفحه صندوق پیام -->
        <div id="message-inbox-page" class="page" style="display: none;">
            <div class="card">
                <div class="card-header bg-info text-white">
                    <h5>صندوق پیام ها</h5>
                </div>
                <div class="card-body">
                    <div id="messages-container">
                        <!-- پیام های ادمین در اینجا نمایش داده می شوند -->
                    </div>
                </div>
            </div>
        </div>

        <!-- صفحه ورود ادمین -->
        <div id="admin-login-page" class="page" style="display: none;">
            <div class="login-container">
                <h3 class="text-center mb-4">ورود ادمین</h3>
                <form id="admin-login-form">
                    <div class="mb-3">
                        <label for="admin-username" class="form-label">نام کاربری</label>
                        <input type="text" class="form-control" id="admin-username" required>
                    </div>
                    <div class="mb-3">
                        <label for="admin-password" class="form-label">رمز عبور</label>
                        <input type="password" class="form-control" id="admin-password" required>
                    </div>
                    <button type="submit" class="btn btn-primary w-100">ورود</button>
                </form>
            </div>
        </div>

        <!-- پنل ادمین -->
        <div id="admin-panel-page" class="page" style="display: none;">
            <div class="admin-panel">
                <div class="d-flex justify-content-between align-items-center mb-4">
                    <h4>پنل مدیریت ادمین</h4>
                    <button class="btn btn-danger" onclick="adminLogout()">خروج</button>
                </div>
                
                <div class="row">
                    <div class="col-md-6">
                        <div class="card mb-4">
                            <div class="card-header bg-warning">
                                <h5>ارسال پیام به همه کاربران</h5>
                            </div>
                            <div class="card-body">
                                <form id="admin-message-form">
                                    <div class="mb-3">
                                        <label for="admin-message" class="form-label">متن پیام</label>
                                        <textarea class="form-control" id="admin-message" rows="3" required></textarea>
                                    </div>
                                    <button type="submit" class="btn btn-warning">ارسال پیام</button>
                                </form>
                            </div>
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="card">
                            <div class="card-header bg-info">
                                <h5>مدیریت بنرها</h5>
                            </div>
                            <div class="card-body">
                                <div id="admin-banners-container">
                                    <!-- بنرها برای مدیریت در اینجا نمایش داده می شوند -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // داده های نمونه
        let banners = [
            { id: 1, title: "فروشگاه اینترنتی", url: "https://example.com", image: "https://via.placeholder.com/300x100?text=فروشگاه+اینترنتی", approved: true },
            { id: 2, title: "آموزش برنامه نویسی", url: "https://example.com", image: "https://via.placeholder.com/300x100?text=آموزش+برنامه+نویسی", approved: true }
        ];
        
        let adminMessages = [
            { id: 1, content: "به روزرسانی جدید سیستم انجام شد. لطفا مشکلات را گزارش دهید.", date: "1402/05/15" },
            { id: 2, content: "همایش بزرگ کاربران فردا برگزار خواهد شد.", date: "1402/05/10" }
        ];
        
        let chatMessages = [
            { user: "کاربر ۱", message: "سلام چطوری؟", time: "10:30" },
            { user: "کاربر ۲", message: "سلام خوبم ممنون. شما چطور؟", time: "10:32" },
            { user: "کاربر ۳", message: "کسی میتونه در مورد بنرها کمکم کنه؟", time: "10:35" }
        ];
        
        let isAdminLoggedIn = false;
        const adminCredentials = { username: "admin", password: "1234" };

        // نمایش صفحه مورد نظر و مخفی کردن بقیه
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.style.display = 'none';
            });
            
            if (pageId === 'home') {
                document.getElementById('home-page').style.display = 'block';
                loadBanners();
            } else if (pageId === 'banner-register') {
                document.getElementById('banner-register-page').style.display = 'block';
            } else if (pageId === 'chat-room') {
                document.getElementById('chat-room-page').style.display = 'block';
                loadChatMessages();
            } else if (pageId === 'message-inbox') {
                document.getElementById('message-inbox-page').style.display = 'block';
                loadAdminMessages();
            } else if (pageId === 'admin-login') {
                document.getElementById('admin-login-page').style.display = 'block';
            } else if (pageId === 'admin-panel' && isAdminLoggedIn) {
                document.getElementById('admin-panel-page').style.display = 'block';
                loadAdminBanners();
            }
        }

        // بارگذاری بنرها در صفحه اصلی
        function loadBanners() {
            const bannersContainer = document.getElementById('banners-container');
            bannersContainer.innerHTML = '';
            
            banners.filter(banner => banner.approved).forEach(banner => {
                const bannerElement = `
                    <div class="col-md-4 mb-4">
                        <div class="card banner-card">
                            <img src="${banner.image}" class="card-img-top" alt="${banner.title}">
                            <div class="card-body">
                                <h5 class="card-title">${banner.title}</h5>
                                <a href="${banner.url}" class="btn btn-primary btn-sm">مشاهده</a>
                            </div>
                        </div>
                    </div>
                `;
                bannersContainer.innerHTML += bannerElement;
            });
        }

        // بارگذاری پیام های ادمین
        function loadAdminMessages() {
            const messagesContainer = document.getElementById('messages-container');
            messagesContainer.innerHTML = '';
            
            adminMessages.forEach(msg => {
                const messageElement = `
                    <div class="card mb-3">
                        <div class="card-header">پیام مدیریت</div>
                        <div class="card-body">
                            <p class="card-text">${msg.content}</p>
                            <small class="text-muted">تاریخ: ${msg.date}</small>
                        </div>
                    </div>
                `;
                messagesContainer.innerHTML += messageElement;
            });
        }

        // بارگذاری پیام های چت
        function loadChatMessages() {
            const chatContainer = document.getElementById('chat-messages');
            chatContainer.innerHTML = '';
            
            chatMessages.forEach(msg => {
                const messageElement = `
                    <div class="message user-message">
                        <strong>${msg.user}:</strong> ${msg.message}
                        <div class="text-muted small">${msg.time}</div>
                    </div>
                `;
                chatContainer.innerHTML += messageElement;
            });
            
            // اسکرول به پایین
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }

        // ارسال پیام در چت
        function sendMessage() {
            const input = document.getElementById('chat-input');
            const message = input.value.trim();
            
            if (message) {
                const now = new Date();
                const time = `${now.getHours()}:${now.getMinutes()}`;
                
                chatMessages.push({
                    user: "شما",
                    message: message,
                    time: time
                });
                
                loadChatMessages();
                input.value = '';
            }
        }

        // مدیریت فرم ثبت بنر
        document.getElementById('banner-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const title = document.getElementById('banner-title').value;
            const url = document.getElementById('banner-url').value;
            const image = document.getElementById('banner-image').value;
            
            const newBanner = {
                id: banners.length + 1,
                title: title,
                url: url,
                image: image,
                approved: false // در حالت عادی نیاز به تایید ادمین دارد
            };
            
            banners.push(newBanner);
            
            alert('بنر شما با موفقیت ثبت شد و پس از تایید ادمین نمایش داده خواهد شد.');
            this.reset();
            showPage('home');
        });

        // مدیریت فرم ورود ادمین
        document.getElementById('admin-login-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const username = document.getElementById('admin-username').value;
            const password = document.getElementById('admin-password').value;
            
            if (username === adminCredentials.username && password === adminCredentials.password) {
                isAdminLoggedIn = true;
                showPage('admin-panel');
            } else {
                alert('نام کاربری یا رمز عبور اشتباه است.');
            }
        });

        // مدیریت فرم ارسال پیام توسط ادمین
        document.getElementById('admin-message-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const message = document.getElementById('admin-message').value;
            const now = new Date();
            const date = `${now.getFullYear()}/${now.getMonth() + 1}/${now.getDate()}`;
            
            adminMessages.unshift({
                id: adminMessages.length + 1,
                content: message,
                date: date
            });
            
            alert('پیام شما با موفقیت برای همه کاربران ارسال شد.');
            this.reset();
        });

        // بارگذاری بنرها در پنل ادمین
        function loadAdminBanners() {
            const adminBannersContainer = document.getElementById('admin-banners-container');
            adminBannersContainer.innerHTML = '';
            
            banners.forEach(banner => {
                const statusBadge = banner.approved ? 
                    '<span class="badge bg-success">تایید شده</span>' : 
                    '<span class="badge bg-warning">در انتظار تایید</span>';
                
                const bannerElement = `
                    <div class="card mb-2">
                        <div class="card-body">
                            <h6 class="card-title">${banner.title} ${statusBadge}</h6>
                            <div class="btn-group btn-group-sm">
                                <button class="btn btn-outline-success" onclick="approveBanner(${banner.id})">تایید</button>
                                <button class="btn btn-outline-danger" onclick="deleteBanner(${banner.id})">حذف</button>
                            </div>
                        </div>
                    </div>
                `;
                adminBannersContainer.innerHTML += bannerElement;
            });
        }

        // تایید بنر توسط ادمین
        function approveBanner(bannerId) {
            const banner = banners.find(b => b.id === bannerId);
            if (banner) {
                banner.approved = true;
                loadAdminBanners();
                alert('بنر تایید شد.');
            }
        }

        // حذف بنر توسط ادمین
        function deleteBanner(bannerId) {
            if (confirm('آیا از حذف این بنر اطمینان دارید؟')) {
                banners = banners.filter(b => b.id !== bannerId);
                loadAdminBanners();
                alert('بنر حذف شد.');
            }
        }

        // خروج ادمین
        function adminLogout() {
            isAdminLoggedIn = false;
            showPage('home');
        }

        // مقداردهی اولیه
        document.addEventListener('DOMContentLoaded', function() {
            showPage('home');
        });
    </script>
</body>
</html>
