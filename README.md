# gic-investment-app[index.html](https://github.com/user-attachments/files/26605563/index.html)
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GIC Global Investment</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        .page { display: none; min-height: 100vh; padding-bottom: 90px; }
        .page.active { display: block; }
        .bg-gic { background-color: #002D5F; }
        .text-gic { color: #002D5F; }
        .captcha-box { background: #f8fafc; letter-spacing: 4px; border: 1px dashed #cbd5e1; cursor: pointer; }
        ::-webkit-scrollbar { width: 0px; }
        .vip-card { transition: all 0.3s ease; }
        .vip-card:active { transform: scale(0.98); }
    </style>
</head>
<body class="bg-gray-50 font-sans text-slate-800">

    <div id="login-page" class="page active bg-white p-8">
        <div class="flex flex-col items-center mt-10">
            <h1 class="text-4xl font-black text-gic italic">GIC</h1>
            <p class="text-[10px] text-gray-400 uppercase tracking-[4px] mb-12 font-bold">Investment Club</p>
            <div class="w-full space-y-4">
                <input type="text" id="login-phone" placeholder="Số điện thoại" class="w-full p-4 bg-gray-50 border rounded-2xl outline-none">
                <input type="password" id="login-pass" placeholder="Mật khẩu" class="w-full p-4 bg-gray-50 border rounded-2xl outline-none">
                <button onclick="handleLogin()" class="w-full bg-blue-600 text-white py-4 rounded-2xl font-bold uppercase shadow-lg">Đăng nhập</button>
                <button onclick="showPage('register-page')" class="w-full text-blue-600 font-bold text-sm mt-2 italic">Tạo tài khoản mới</button>
            </div>
        </div>
    </div>

    <div id="register-page" class="page bg-white p-8">
        <div class="flex flex-col items-center">
            <h1 class="text-3xl font-black text-gic italic mb-8 uppercase">Đăng ký</h1>
            <div class="w-full space-y-4">
                <input type="text" id="reg-phone" maxlength="10" placeholder="Số điện thoại" class="w-full p-4 bg-gray-50 border rounded-2xl outline-none">
                <input type="password" id="reg-pass" placeholder="Mật khẩu" class="w-full p-4 bg-gray-50 border rounded-2xl outline-none">
                <input type="text" id="reg-invite" placeholder="Mã mời (SĐT)" class="w-full p-4 bg-blue-50 border rounded-2xl outline-none">
                <div class="flex gap-2 items-center">
                    <input type="text" id="reg-captcha-input" placeholder="Captcha" class="flex-1 p-4 bg-gray-50 border rounded-2xl outline-none">
                    <div id="captcha-code" onclick="generateCaptcha()" class="captcha-box px-4 py-3 rounded-2xl font-bold text-blue-600 italic"></div>
                </div>
                <button onclick="handleRegister()" class="w-full bg-blue-600 text-white py-4 rounded-2xl font-bold uppercase shadow-lg">Đăng ký ngay</button>
                <button onclick="showPage('login-page')" class="w-full text-gray-400 text-sm">Quay lại đăng nhập</button>
            </div>
        </div>
    </div>

    <div id="home" class="page">
        <div class="p-4 bg-white flex justify-between items-center border-b font-bold text-gic italic sticky top-0 z-20">
            <span>GIC INVESTMENT</span>
            <i class="fas fa-bell text-gray-400"></i>
        </div>
        <div class="p-4">
            <div class="bg-gic rounded-[2rem] p-6 text-white shadow-xl mb-6 relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[10px] opacity-60 font-bold mb-1 uppercase tracking-widest">Số dư khả dụng</p>
                    <p class="text-3xl font-black italic mb-4">₫ <span id="home-balance">0</span></p>
                    <div class="flex gap-2">
                        <button onclick="showPage('deposit-page')" class="flex-1 bg-white text-gic py-2.5 rounded-xl text-[10px] font-bold uppercase">Nạp tiền</button>
                        <button onclick="showPage('withdraw-page')" class="flex-1 bg-white/20 text-white py-2.5 rounded-xl text-[10px] font-bold uppercase border border-white/20">Rút tiền</button>
                    </div>
                </div>
                <div class="absolute -right-4 -bottom-4 text-white/5 text-8xl rotate-12"><i class="fas fa-wallet"></i></div>
            </div>

            <h3 class="font-bold mb-4 text-xs border-l-4 border-blue-600 pl-2 uppercase">Gói đầu tư (7 Ngày)</h3>
            <div class="grid grid-cols-1 gap-4">
                <div class="bg-white p-5 rounded-3xl border flex justify-between items-center vip-card shadow-sm">
                    <div>
                        <p class="text-blue-500 font-bold text-[10px] uppercase">Gói VIP 1</p>
                        <p class="text-xl font-black text-gic italic">₫100,000</p>
                        <p class="text-[10px] text-green-600 font-bold mt-1">Lãi: 40,000đ / ngày</p>
                    </div>
                    <button onclick="buyPackage(100000, 40000, 'VIP 1')" class="bg-gic text-white px-5 py-3 rounded-2xl font-bold text-[10px] uppercase italic">Đầu tư</button>
                </div>
                <div class="bg-white p-5 rounded-3xl border flex justify-between items-center vip-card shadow-sm">
                    <div>
                        <p class="text-blue-600 font-bold text-[10px] uppercase">Gói VIP 2</p>
                        <p class="text-xl font-black text-gic italic">₫200,000</p>
                        <p class="text-[10px] text-green-600 font-bold mt-1">Lãi: 80,000đ / ngày</p>
                    </div>
                    <button onclick="buyPackage(200000, 80000, 'VIP 2')" class="bg-gic text-white px-5 py-3 rounded-2xl font-bold text-[10px] uppercase italic">Đầu tư</button>
                </div>
                <div class="bg-white p-5 rounded-3xl border border-blue-100 flex justify-between items-center vip-card shadow-sm">
                    <div>
                        <p class="text-orange-500 font-bold text-[10px] uppercase">Gói VIP 3</p>
                        <p class="text-xl font-black text-gic italic">₫500,000</p>
                        <p class="text-[10px] text-orange-600 font-bold mt-1">Lãi: 200,000đ / ngày</p>
                    </div>
                    <button onclick="buyPackage(500000, 200000, 'VIP 3')" class="bg-orange-600 text-white px-5 py-3 rounded-2xl font-bold text-[10px] uppercase italic">Đầu tư</button>
                </div>
                <div class="bg-white p-5 rounded-3xl border border-red-100 flex justify-between items-center vip-card shadow-sm">
                    <div>
                        <p class="text-red-600 font-bold text-[10px] uppercase">Gói VIP 4</p>
                        <p class="text-xl font-black text-gic italic">₫1,000,000</p>
                        <p class="text-[10px] text-red-600 font-bold mt-1">Lãi: 450,000đ / ngày</p>
                    </div>
                    <button onclick="buyPackage(1000000, 450000, 'VIP 4')" class="bg-red-600 text-white px-5 py-3 rounded-2xl font-bold text-[10px] uppercase italic shadow-lg shadow-red-100">Đầu tư</button>
                </div>
            </div>
        </div>
    </div>

    <div id="income-page" class="page">
        <div class="p-4 bg-white border-b text-center font-bold text-sm tracking-widest">KHO TÀI SẢN</div>
        <div class="p-4 space-y-4" id="investment-list"></div>
    </div>

    <div id="deposit-page" class="page p-6 bg-white">
        <div class="flex items-center mb-6" onclick="showPage('home')"><i class="fas fa-arrow-left mr-4"></i><h1 class="font-bold">Nạp tiền</h1></div>
        <div class="bg-blue-50 p-4 rounded-2xl mb-6 text-[10px] text-blue-700 leading-relaxed font-bold">
            <i class="fas fa-info-circle mr-1"></i> Sau khi chuyển khoản, Admin sẽ phê duyệt lệnh nạp trong 5-10 phút.
        </div>
        <input type="number" id="dep-amt" placeholder="Nhập số tiền nạp" class="w-full p-5 border rounded-3xl text-center text-2xl font-black mb-6 outline-none bg-gray-50 focus:bg-white focus:border-blue-600">
        <button onclick="requestDeposit()" class="w-full bg-blue-600 text-white py-4 rounded-3xl font-bold uppercase shadow-xl active:scale-95 transition-all">Tạo lệnh nạp tiền</button>
        
        <div id="qr-area" class="hidden mt-8 text-center p-8 border-2 border-dashed rounded-[2.5rem] bg-slate-50 relative">
            <div id="qr-img" class="flex justify-center mb-4"></div>
            <p class="text-xs">Nội dung chuyển khoản:</p>
            <p id="qr-memo" class="text-xl text-red-600 font-black mb-4"></p>
            <div class="p-3 bg-yellow-100 rounded-xl text-[9px] font-bold text-yellow-800 uppercase tracking-tighter italic animate-pulse">Đang chờ Admin duyệt tiền...</div>
        </div>
    </div>

    <div id="withdraw-page" class="page p-6 bg-white">
        <div class="flex items-center mb-6" onclick="showPage('home')"><i class="fas fa-arrow-left mr-4"></i><h1 class="font-bold">Rút tiền</h1></div>
        <div class="bg-gic p-8 rounded-[2.5rem] text-white text-center mb-8 shadow-2xl">
            <p class="text-[10px] opacity-60 uppercase font-bold tracking-widest">Ví khả dụng</p>
            <p class="text-4xl font-black italic">₫ <span id="wd-balance">0</span></p>
        </div>
        <div class="space-y-6">
            <div>
                <label class="text-[10px] font-black text-gray-400 uppercase ml-2">Số tiền muốn rút (Min 30k)</label>
                <input type="number" id="wd-input" placeholder="0" class="w-full p-4 border-b-4 text-3xl font-black outline-none focus:border-blue-600 transition-all">
            </div>
            <button onclick="handleWithdraw()" class="w-full bg-blue-600 text-white py-5 rounded-3xl font-bold uppercase shadow-xl active:scale-95 transition-all">Xác nhận rút tiền</button>
        </div>
        <div class="mt-12">
            <h3 class="font-bold text-xs mb-4 text-gray-400 uppercase tracking-widest">Lịch sử giao dịch</h3>
            <div id="wd-history" class="space-y-3"></div>
        </div>
    </div>

    <div id="profile-page" class="page bg-slate-50">
        <div class="bg-gic p-10 text-white rounded-b-[3.5rem] shadow-2xl flex items-center gap-5">
            <div class="w-16 h-16 bg-white/10 rounded-full flex items-center justify-center border border-white/20 text-3xl"><i class="fas fa-user-circle"></i></div>
            <div>
                <p id="prof-phone" class="font-black text-xl tracking-tight">09********</p>
                <span class="text-[9px] bg-green-500/20 text-green-400 px-2 py-0.5 rounded font-bold uppercase border border-green-500/30">Đã xác minh</span>
            </div>
        </div>
        <div class="p-5 space-y-4">
            <div class="bg-white rounded-[2rem] border shadow-sm overflow-hidden">
                <div onclick="showPage('bank-settings')" class="flex items-center p-5 border-b text-sm active:bg-gray-50"><i class="fas fa-credit-card text-green-500 w-10 text-lg"></i><span>Liên kết ngân hàng</span><i class="fas fa-chevron-right ml-auto text-gray-200"></i></div>
                <div onclick="showPage('invite-page')" class="flex items-center p-5 border-b text-sm active:bg-gray-50"><i class="fas fa-users-viewfinder text-blue-500 w-10 text-lg"></i><span>Đội ngũ & Hoa hồng</span><i class="fas fa-chevron-right ml-auto text-gray-200"></i></div>
                <div onclick="showPage('change-pass-page')" class="flex items-center p-5 text-sm active:bg-gray-50"><i class="fas fa-key text-orange-500 w-10 text-lg"></i><span>Bảo mật tài khoản</span><i class="fas fa-chevron-right ml-auto text-gray-200"></i></div>
            </div>
            <button onclick="location.reload()" class="w-full py-5 text-red-500 font-bold bg-white rounded-3xl border shadow-sm mt-4 uppercase text-xs tracking-widest">Đăng xuất tài khoản</button>
        </div>
    </div>

    <div id="bank-settings" class="page p-6 bg-white">
        <div class="flex items-center mb-6" onclick="showPage('profile-page')"><i class="fas fa-arrow-left mr-4"></i><h1 class="font-bold">Cài đặt thanh toán</h1></div>
        <div class="space-y-4">
            <select id="bank-name" class="w-full p-4 border rounded-2xl bg-gray-50 outline-none font-bold">
                <option>Vietcombank</option><option>MB Bank</option><option>BIDV</option><option>Agribank</option>
                <option>Techcombank</option><option>ACB</option><option>TPBank</option><option>VPBank</option><option>Momo</option>
            </select>
            <input type="text" id="bank-num" placeholder="Số tài khoản / Số ví" class="w-full p-4 border rounded-2xl bg-gray-50 outline-none">
            <input type="text" id="bank-user" placeholder="Tên chủ thẻ (VIẾT HOA KHÔNG DẤU)" class="w-full p-4 border rounded-2xl bg-gray-50 outline-none uppercase font-bold">
            <button onclick="saveBank()" class="w-full bg-gic text-white py-4 rounded-3xl font-bold uppercase mt-6 shadow-xl">Lưu thông tin</button>
        </div>
    </div>

    <div id="invite-page" class="page p-6 bg-white">
        <div class="flex items-center mb-6" onclick="showPage('profile-page')"><i class="fas fa-arrow-left mr-4"></i><h1 class="font-bold">Mời bạn bè</h1></div>
        <div class="bg-gradient-to-br from-blue-700 to-blue-900 rounded-[3rem] p-12 text-white text-center shadow-2xl relative overflow-hidden">
            <p class="text-[10px] uppercase font-bold opacity-60 mb-3 tracking-widest">Mã mời cá nhân</p>
            <p id="my-invite-code" class="text-4xl font-black tracking-widest italic relative z-10">000000</p>
            <p class="mt-8 text-[11px] leading-relaxed opacity-80 font-medium italic">Bạn nhận được <b class="text-yellow-400">30% hoa hồng</b> giá trị tiền nạp của cấp dưới khi Admin phê duyệt lệnh nạp.</p>
            <div class="absolute top-0 right-0 p-4 opacity-10 text-6xl"><i class="fas fa-coins"></i></div>
        </div>
    </div>

    <div id="change-pass-page" class="page p-6 bg-white">
        <div class="flex items-center mb-6" onclick="showPage('profile-page')"><i class="fas fa-arrow-left mr-4"></i><h1 class="font-bold">Đổi mật khẩu</h1></div>
        <div class="space-y-4">
            <input type="password" id="old-pass" placeholder="Mật khẩu cũ" class="w-full p-4 border rounded-2xl bg-gray-50">
            <input type="password" id="new-pass" placeholder="Mật khẩu mới" class="w-full p-4 border rounded-2xl bg-gray-50">
            <button onclick="handleSavePass()" class="w-full bg-gic text-white py-4 rounded-2xl font-bold uppercase">Cập nhật mật khẩu</button>
        </div>
    </div>

    <div id="bottom-nav" class="fixed bottom-0 left-0 right-0 bg-white border-t flex justify-around py-3 text-gray-400 text-[10px] z-50">
        <div class="flex flex-col items-center nav-btn" onclick="showPage('home')"><i class="fas fa-home text-lg mb-1"></i><span>Trang chủ</span></div>
        <div class="flex flex-col items-center nav-btn" onclick="showPage('income-page')"><i class="fas fa-chart-line text-lg mb-1"></i><span>Thu nhập</span></div>
        <div class="flex flex-col items-center nav-btn" onclick="showPage('profile-page')"><i class="fas fa-user-circle text-lg mb-1"></i><span>Của tôi</span></div>
    </div>

    <script>
        let db_users = []; 
        let currentUser = null;
        let currentCaptcha = "";

        function showPage(pageId) {
            if (['home', 'profile-page', 'income-page', 'withdraw-page', 'deposit-page', 'invite-page', 'bank-settings', 'change-pass-page'].includes(pageId) && !currentUser) {
                pageId = 'login-page';
            }
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');

            if (currentUser) {
                document.getElementById('home-balance').innerText = currentUser.balance.toLocaleString();
                document.getElementById('wd-balance').innerText = currentUser.balance.toLocaleString();
                document.getElementById('prof-phone').innerText = currentUser.phone.replace(currentUser.phone.substring(3,7), "****");
                document.getElementById('my-invite-code').innerText = currentUser.phone;
                if(pageId === 'income-page') renderInvestments();
                if(pageId === 'withdraw-page') renderWithdrawHistory();
            }
            document.getElementById('bottom-nav').style.display = (['home', 'income-page', 'profile-page'].includes(pageId)) ? 'flex' : 'none';
        }

        function generateCaptcha() {
            currentCaptcha = Math.floor(1000 + Math.random() * 9000).toString();
            document.getElementById('captcha-code').innerText = currentCaptcha;
        }

        function handleRegister() {
            const p = document.getElementById('reg-phone').value;
            const pass = document.getElementById('reg-pass').value;
            const inv = document.getElementById('reg-invite').value;
            const cap = document.getElementById('reg-captcha-input').value;

            if(p.length < 10) return alert("SĐT phải đủ 10 chữ số!");
            if(cap !== currentCaptcha) return alert("Sai mã Captcha!");
            if(db_users.find(u => u.phone === p)) return alert("Tài khoản đã tồn tại!");

            db_users.push({ 
                phone: p, pass: pass, balance: 0, invitedBy: inv, 
                investments: [], withdrawHistory: [], bank: null 
            });
            alert("Đăng ký thành công!");
            showPage('login-page');
        }

        function handleLogin() {
            const p = document.getElementById('login-phone').value;
            const pass = document.getElementById('login-pass').value;
            const user = db_users.find(u => u.phone === p && u.pass === pass);
            if(user) { currentUser = user; showPage('home'); } 
            else alert("SĐT hoặc Mật khẩu không đúng!");
        }

        // --- HỆ THỐNG NẠP TIỀN CHỜ DUYỆT ---
        function requestDeposit() {
            const amt = parseInt(document.getElementById('dep-amt').value);
            if(!amt || amt < 10000) return alert("Nạp tối thiểu 10,000đ");

            document.getElementById('qr-area').classList.remove('hidden');
            document.getElementById('qr-memo').innerText = "GIC " + currentUser.phone;
            document.getElementById('qr-img').innerHTML = `<img src="https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=DEPOSIT_${amt}_${currentUser.phone}" class="w-44 h-44 rounded-xl border p-2">`;
            
            console.log(`[ADMIN] Duyệt nạp ${amt} cho ${currentUser.phone}: adminApproveDeposit(${amt})`);
            alert("Yêu cầu đã gửi! Vui lòng chuyển khoản và chờ Admin duyệt.");
        }

        // Lệnh giả lập cho Admin
        window.adminApproveDeposit = function(amount) {
            if(!currentUser) return;
            currentUser.balance += amount;
            if(currentUser.invitedBy) {
                const boss = db_users.find(u => u.phone === currentUser.invitedBy);
                if(boss) boss.balance += (amount * 0.3);
            }
            alert(`ADMIN: Phê duyệt ₫${amount.toLocaleString()} thành công!`);
            showPage('home');
        };

        // RÚT TIỀN MIN 30K
        function handleWithdraw() {
            const amt = parseInt(document.getElementById('wd-input').value);
            if(!amt || amt < 30000) return alert("Hạn mức rút tối thiểu là 40,000đ");
            if(amt > currentUser.balance) return alert("Số dư khả dụng không đủ!");
            if(!currentUser.bank) return alert("Bạn chưa liên kết tài khoản ngân hàng!");

            currentUser.balance -= amt;
            currentUser.withdrawHistory.unshift({ 
                time: new Date().toLocaleString('vi-VN'), 
                amt: amt, 
                status: "Đang duyệt" 
            });
            alert("Yêu cầu rút tiền đang được xử lý!");
            showPage('home');
        }

        // MUA GÓI 7 NGÀY
        function buyPackage(price, profit, name) {
            if(currentUser.balance < price) return alert("Số dư không đủ! Hãy nạp thêm và chờ duyệt.");
            currentUser.balance -= price;
            currentUser.investments.push({
                id: Date.now(),
                name: name,
                daily: profit,
                daysLeft: 7,
                lastClaim: null
            });
            alert(`Kích hoạt thành công ${name}. Lãi sẽ nhận mỗi ngày!`);
            showPage('income-page');
        }

        function renderInvestments() {
            const box = document.getElementById('investment-list');
            if(currentUser.investments.length === 0) {
                box.innerHTML = `<div class="text-center py-24 text-gray-300 italic text-xs uppercase tracking-widest">Không có máy đang chạy</div>`;
                return;
            }
            const today = new Date().toLocaleDateString('vi-VN');
            box.innerHTML = currentUser.investments.map(inv => {
                const canClaim = inv.lastClaim !== today && inv.daysLeft > 0;
                return `
                <div class="bg-white p-7 rounded-[2.5rem] border-2 border-gray-50 shadow-sm relative overflow-hidden">
                    <div class="flex justify-between items-center mb-6">
                        <span class="text-xs font-black text-blue-800 uppercase tracking-tighter">${inv.name}</span>
                        <div class="px-3 py-1 bg-blue-600 text-white rounded-full text-[9px] font-bold">CÒN ${inv.daysLeft} NGÀY</div>
                    </div>
                    <div class="flex justify-between items-end mb-8">
                        <div><p class="text-[9px] text-gray-400 uppercase font-bold">Lãi nhận hôm nay</p><p class="text-2xl font-black italic text-green-600">₫${inv.daily.toLocaleString()}</p></div>
                        <div class="text-right"><p class="text-[9px] text-gray-400 uppercase font-bold">Tổng chu kỳ</p><p class="text-xs font-bold">₫${(inv.daily * 7).toLocaleString()}</p></div>
                    </div>
                    <button onclick="claimProfit(${inv.id})" ${!canClaim ? 'disabled' : ''} 
                        class="w-full py-4 rounded-2xl font-bold uppercase text-[10px] tracking-widest transition-all ${canClaim ? 'bg-gic text-white shadow-lg active:scale-95' : 'bg-gray-100 text-gray-300'}">
                        ${inv.daysLeft <= 0 ? 'ĐÃ KẾT THÚC' : (canClaim ? 'NHẬN TIỀN LÃI' : 'HẸN NGÀY MAI')}
                    </button>
                    ${inv.daysLeft > 0 && !canClaim ? '<p class="text-center text-[8px] mt-2 text-blue-500 font-bold italic">Bạn đã nhận tiền hôm nay rồi</p>' : ''}
                </div>`;
            }).join('');
        }

        function claimProfit(id) {
            const inv = currentUser.investments.find(i => i.id === id);
            const today = new Date().toLocaleDateString('vi-VN');
            if(inv.daysLeft <= 0 || inv.lastClaim === today) return;
            
            currentUser.balance += inv.daily;
            inv.lastClaim = today;
            inv.daysLeft -= 1;
            alert(`Chúc mừng! Bạn nhận được ₫${inv.daily.toLocaleString()}`);
            renderInvestments();
        }

        function renderWithdrawHistory() {
            const box = document.getElementById('wd-history');
            if(currentUser.withdrawHistory.length === 0) {
                box.innerHTML = `<p class="text-center text-gray-300 py-10 italic text-xs">Chưa có dữ liệu</p>`;
                return;
            }
            box.innerHTML = currentUser.withdrawHistory.map(h => `
                <div class="flex justify-between p-5 bg-gray-50 rounded-3xl border border-gray-100">
                    <div><p class="text-[9px] text-gray-400 font-bold uppercase">${h.time}</p><p class="font-black text-xs uppercase">Rút tiền mặt</p></div>
                    <div class="text-right"><p class="font-black text-gic italic text-xs">₫${h.amt.toLocaleString()}</p><p class="text-[8px] text-orange-500 font-bold uppercase">${h.status}</p></div>
                </div>
            `).join('');
        }

        function saveBank() {
            const name = document.getElementById('bank-name').value;
            const num = document.getElementById('bank-num').value;
            const user = document.getElementById('bank-user').value;
            if(!num || !user) return alert("Vui lòng nhập đầy đủ!");
            currentUser.bank = { name, num, user };
            alert("Đã lưu thông tin tài khoản!");
            showPage('profile-page');
        }

        function handleSavePass() {
            const old = document.getElementById('old-pass').value;
            const n = document.getElementById('new-pass').value;
            if(old !== currentUser.pass) return alert("Mật khẩu cũ không đúng!");
            currentUser.pass = n;
            alert("Đã đổi mật khẩu!");
            showPage('profile-page');
        }

        window.onload = generateCaptcha;
    </script>
</body>
</html>
