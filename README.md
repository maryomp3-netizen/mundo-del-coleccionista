[intex.html.html](https://github.com/user-attachments/files/29170484/intex.html.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Mundo del Coleccionista</title>
<link rel="manifest" href="/manifest.json">
<meta name="theme-color" content="#ffd93d">
<meta name="description" content="Identifica y cataloga toda clase de coleccionables con ayuda de la comunidad">
<meta name="application-name" content="Mundo del Coleccionista">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Coleccionista">
<link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0f0e17; --surface: #1a1828; --card: #221f35;
    --accent1: #ff6b6b; --accent2: #ffd93d; --accent3: #6bcb77;
    --accent4: #4d96ff; --accent5: #c77dff; --text: #fffffe; --muted: #a7a9be; --radius: 20px;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body { font-family:'Nunito',sans-serif; background:var(--bg); color:var(--text); min-height:100vh; max-width:430px; margin:0 auto; }
  .screen { display:none; flex-direction:column; min-height:100vh; animation:fadeIn 0.3s ease; }
  .screen.active { display:flex; }
  @keyframes fadeIn { from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)} }
  .topbar { padding:16px 20px 10px; display:flex; align-items:center; justify-content:space-between; }
  .logo { font-family:'Fredoka One',cursive; font-size:22px; background:linear-gradient(135deg,var(--accent2),var(--accent1)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
  .logo span { background:linear-gradient(135deg,var(--accent4),var(--accent5)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
  .user-btn { width:36px; height:36px; background:linear-gradient(135deg,var(--accent5),var(--accent4)); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:16px; cursor:pointer; border:none; }
  .search-wrap { padding:0 20px 14px; }
  .search-bar { background:var(--card); border:1.5px solid #2e2b45; border-radius:14px; padding:11px 14px; display:flex; align-items:center; gap:8px; color:var(--muted); font-size:14px; font-weight:600; }
  #search-input { background:none; border:none; outline:none; color:var(--text); font-family:'Nunito',sans-serif; font-size:14px; font-weight:600; width:100%; }
  #search-input::placeholder { color:var(--muted); }
  .pills { display:flex; gap:8px; padding:0 20px 16px; overflow-x:auto; scrollbar-width:none; }
  .pills::-webkit-scrollbar { display:none; }
  .pill { padding:7px 14px; border-radius:50px; font-size:12px; font-weight:800; white-space:nowrap; cursor:pointer; border:1.5px solid #2e2b45; background:var(--card); color:var(--muted); transition:all 0.2s; }
  .pill.sel { background:linear-gradient(135deg,var(--accent2),var(--accent1)); color:#1a1200; border-color:transparent; }
  .section-title { padding:0 20px 10px; font-size:16px; font-weight:800; display:flex; justify-content:space-between; align-items:center; }
  .grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; padding:0 20px 100px; }
  .col-card { background:var(--card); border-radius:var(--radius); overflow:hidden; cursor:pointer; border:1.5px solid #2e2b45; transition:transform 0.2s; position:relative; }
  .col-card:hover { transform:translateY(-3px); }
  .col-card-img { width:100%; aspect-ratio:1; display:flex; align-items:center; justify-content:center; font-size:48px; position:relative; overflow:hidden; }
  .col-badge { position:absolute; top:7px; right:7px; font-size:9px; font-weight:800; padding:2px 7px; border-radius:20px; text-transform:uppercase; background:var(--accent4); color:#fff; }
  .lock-overlay { position:absolute; inset:0; background:rgba(15,14,23,0.7); display:flex; align-items:center; justify-content:center; font-size:28px; }
  .col-card-info { padding:9px 11px 11px; }
  .col-card-name { font-size:12px; font-weight:800; margin-bottom:2px; }
  .col-card-meta { font-size:10px; color:var(--muted); font-weight:600; display:flex; align-items:center; gap:4px; }
  .rdot { width:6px; height:6px; border-radius:50%; display:inline-block; }
  .empty { text-align:center; padding:60px 20px; color:var(--muted); grid-column:span 2; }
  .empty .big { font-size:56px; margin-bottom:12px; }
  .bottom-nav { position:fixed; bottom:0; left:50%; transform:translateX(-50%); width:100%; max-width:430px; background:var(--card); border-top:1.5px solid #2e2b45; display:flex; padding:10px 0 18px; z-index:100; }
  .nav-btn { flex:1; display:flex; flex-direction:column; align-items:center; gap:3px; font-size:10px; font-weight:700; color:var(--muted); cursor:pointer; background:none; border:none; font-family:'Nunito',sans-serif; transition:color 0.2s; }
  .nav-btn.active { color:var(--accent2); }
  .nav-btn span:first-child { font-size:20px; }
  .back-row { display:flex; align-items:center; gap:10px; padding:14px 20px 10px; }
  .back-btn { width:34px; height:34px; background:var(--card); border:none; border-radius:11px; font-size:15px; cursor:pointer; color:var(--text); display:flex; align-items:center; justify-content:center; }
  .detail-wrap { padding:0 20px 100px; flex:1; }
  .detail-hero { background:var(--card); border-radius:var(--radius); margin-bottom:16px; height:180px; display:flex; align-items:center; justify-content:center; font-size:80px; border:1.5px solid #2e2b45; overflow:hidden; }
  .detail-name { font-family:'Fredoka One',cursive; font-size:26px; margin-bottom:3px; }
  .detail-sub { color:var(--muted); font-size:12px; font-weight:600; margin-bottom:14px; }
  .tags { display:flex; gap:7px; flex-wrap:wrap; margin-bottom:14px; }
  .tag { padding:4px 11px; border-radius:20px; font-size:10px; font-weight:800; text-transform:uppercase; }
  .stats-row { display:grid; grid-template-columns:1fr 1fr 1fr; gap:8px; margin-bottom:14px; }
  .stat-box { background:var(--card); border-radius:13px; padding:11px; text-align:center; border:1.5px solid #2e2b45; }
  .stat-val { font-family:'Fredoka One',cursive; font-size:18px; color:var(--accent2); }
  .stat-lbl { font-size:9px; color:var(--muted); font-weight:700; text-transform:uppercase; }
  .desc-box { background:var(--card); border-radius:14px; padding:13px; font-size:13px; line-height:1.6; color:#ccc; border:1.5px solid #2e2b45; margin-bottom:14px; }
  .owner-box { background:var(--card); border-radius:14px; padding:12px; display:flex; align-items:center; gap:10px; border:1.5px solid #2e2b45; margin-bottom:14px; }
  .owner-avatar { width:38px; height:38px; background:linear-gradient(135deg,var(--accent1),var(--accent5)); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:18px; }
  .upload-wrap { padding:0 20px 100px; flex:1; display:flex; flex-direction:column; }
  .upload-title { font-family:'Fredoka One',cursive; font-size:22px; margin-bottom:4px; padding-top:4px; }
  .upload-sub { color:var(--muted); font-size:12px; font-weight:600; margin-bottom:16px; }
  .upload-zone { background:var(--card); border:2px dashed #3e3b55; border-radius:var(--radius); height:140px; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:6px; margin-bottom:14px; cursor:pointer; transition:border-color 0.2s; position:relative; overflow:hidden; }
  .upload-zone:hover { border-color:var(--accent4); }
  #img-preview { width:100%; height:100%; object-fit:cover; position:absolute; top:0; left:0; display:none; }
  #file-input { display:none; }
  .form-field { margin-bottom:12px; }
  .form-label { font-size:11px; font-weight:800; text-transform:uppercase; letter-spacing:0.5px; color:var(--muted); margin-bottom:5px; display:block; }
  .form-input { width:100%; background:var(--card); border:1.5px solid #2e2b45; border-radius:13px; padding:11px 13px; font-size:13px; font-family:'Nunito',sans-serif; color:var(--text); outline:none; font-weight:600; transition:border-color 0.2s; }
  .form-input:focus { border-color:var(--accent4); }
  .form-select { width:100%; background:var(--card); border:1.5px solid #2e2b45; border-radius:13px; padding:11px 13px; font-size:13px; font-family:'Nunito',sans-serif; color:var(--text); outline:none; font-weight:600; appearance:none; }
  .submit-btn { width:100%; padding:15px; background:linear-gradient(135deg,var(--accent2),var(--accent1)); border:none; border-radius:15px; font-family:'Fredoka One',cursive; font-size:17px; color:#1a1200; cursor:pointer; transition:transform 0.2s; margin-top:8px; }
  .submit-btn:hover { transform:translateY(-2px); }
  .submit-btn:disabled { opacity:0.5; cursor:not-allowed; transform:none; }
  /* PLANES */
  .planes-wrap { padding:0 20px 100px; flex:1; }
  .plan-card { border-radius:var(--radius); padding:20px; margin-bottom:14px; border:2px solid #2e2b45; position:relative; overflow:hidden; }
  .plan-free { background:var(--card); }
  .plan-premium { background:linear-gradient(135deg,#1a2a1a,#0d1a0d); border-color:var(--accent3); }
  .plan-pro { background:linear-gradient(135deg,#1a1060,#2d1b69); border-color:var(--accent5); }
  .plan-badge { position:absolute; top:14px; right:14px; font-size:10px; font-weight:800; padding:3px 10px; border-radius:20px; text-transform:uppercase; }
  .plan-title { font-family:'Fredoka One',cursive; font-size:24px; margin-bottom:4px; }
  .plan-price { font-size:28px; font-weight:800; margin-bottom:14px; }
  .plan-price span { font-size:14px; color:var(--muted); font-weight:600; }
  .plan-features { list-style:none; display:flex; flex-direction:column; gap:8px; margin-bottom:18px; }
  .plan-features li { font-size:13px; font-weight:600; display:flex; align-items:flex-start; gap:8px; }
  .plan-btn { width:100%; padding:13px; border:none; border-radius:14px; font-family:'Fredoka One',cursive; font-size:16px; cursor:pointer; transition:transform 0.2s; }
  .plan-btn:hover { transform:translateY(-2px); }
  /* AUTH */
  .auth-wrap { flex:1; display:flex; flex-direction:column; align-items:center; justify-content:center; padding:40px 24px; text-align:center; gap:16px; }
  .auth-icon { font-size:64px; }
  .auth-title { font-family:'Fredoka One',cursive; font-size:28px; background:linear-gradient(135deg,var(--accent2),var(--accent1)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
  .auth-sub { color:var(--muted); font-size:13px; font-weight:600; max-width:260px; line-height:1.6; }
  .auth-btn { width:100%; padding:14px; border-radius:14px; font-family:'Fredoka One',cursive; font-size:17px; cursor:pointer; border:none; transition:transform 0.2s; }
  .auth-btn:hover { transform:translateY(-2px); }
  .btn-google { background:#fff; color:#333; display:flex; align-items:center; justify-content:center; gap:10px; font-size:15px; }
  .btn-primary { background:linear-gradient(135deg,var(--accent2),var(--accent1)); color:#1a1200; }
  .auth-divider { color:var(--muted); font-size:12px; font-weight:700; }
  .auth-form { width:100%; display:flex; flex-direction:column; gap:10px; }
  .auth-toggle { color:var(--accent4); font-size:13px; font-weight:700; cursor:pointer; }
  /* PROFILE */
  .profile-wrap { padding:0 20px 100px; flex:1; }
  .profile-hero { display:flex; flex-direction:column; align-items:center; padding:20px 0 16px; gap:8px; }
  .profile-avatar { width:68px; height:68px; background:linear-gradient(135deg,var(--accent1),var(--accent5)); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:30px; border:3px solid #2e2b45; }
  .profile-name { font-family:'Fredoka One',cursive; font-size:20px; }
  .profile-email { color:var(--muted); font-size:12px; font-weight:600; }
  .profile-stats { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:16px; }
  .logout-btn { width:100%; padding:13px; background:var(--card); border:1.5px solid #ff6b6b; border-radius:14px; color:var(--accent1); font-family:'Fredoka One',cursive; font-size:16px; cursor:pointer; }
  .plan-chip { display:inline-flex; align-items:center; gap:6px; padding:5px 12px; border-radius:20px; font-size:12px; font-weight:800; margin-bottom:16px; }
  .toast { position:fixed; bottom:90px; left:50%; transform:translateX(-50%); background:#333; color:#fff; padding:10px 20px; border-radius:30px; font-size:13px; font-weight:700; z-index:999; opacity:0; transition:opacity 0.3s; pointer-events:none; white-space:nowrap; }
  .toast.show { opacity:1; }
  .loading { display:flex; align-items:center; justify-content:center; padding:40px; grid-column:span 2; }
  .spinner { width:30px; height:30px; border:3px solid #2e2b45; border-top-color:var(--accent4); border-radius:50%; animation:spin 0.8s linear infinite; }
  @keyframes spin { to{transform:rotate(360deg)} }
  .comments-wrap { margin-top:14px; }
  .comment-item { background:var(--card); border-radius:14px; padding:11px 13px; margin-bottom:8px; border:1.5px solid #2e2b45; }
  .comment-author { font-size:12px; font-weight:800; color:var(--accent4); margin-bottom:3px; }
  .comment-text { font-size:13px; color:#ccc; }
  .like-btn { display:flex; align-items:center; gap:6px; background:var(--card); border:1.5px solid #2e2b45; border-radius:12px; padding:8px 14px; font-size:13px; font-weight:700; cursor:pointer; color:var(--text); font-family:'Nunito',sans-serif; transition:all 0.2s; }
  .like-btn.liked { border-color:var(--accent1); color:var(--accent1); }
  /* CHAT */
  .chat-list { display:flex; flex-direction:column; gap:2px; padding:0 0 100px; flex:1; overflow-y:auto; }
  .chat-item { display:flex; align-items:center; gap:12px; padding:12px 20px; cursor:pointer; transition:background 0.2s; border-bottom:1px solid #1e1c2e; }
  .chat-item:hover { background:var(--card); }
  .chat-avatar { width:48px; height:48px; border-radius:50%; background:linear-gradient(135deg,var(--accent1),var(--accent5)); display:flex; align-items:center; justify-content:center; font-size:20px; flex-shrink:0; overflow:hidden; }
  .chat-info { flex:1; min-width:0; }
  .chat-name { font-size:14px; font-weight:800; margin-bottom:2px; }
  .chat-preview { font-size:12px; color:var(--muted); font-weight:600; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
  .chat-time { font-size:10px; color:var(--muted); font-weight:700; flex-shrink:0; }
  .chat-unread { background:var(--accent1); color:#fff; border-radius:50%; width:18px; height:18px; font-size:10px; font-weight:800; display:flex; align-items:center; justify-content:center; flex-shrink:0; }
  /* MESSAGES */
  .messages-wrap { flex:1; overflow-y:auto; padding:14px 16px 80px; display:flex; flex-direction:column; gap:8px; scrollbar-width:none; }
  .messages-wrap::-webkit-scrollbar { display:none; }
  .msg-bubble { max-width:75%; padding:10px 14px; border-radius:18px; font-size:13px; font-weight:600; line-height:1.5; word-break:break-word; }
  .msg-bubble.sent { background:linear-gradient(135deg,var(--accent4),#1a5a9a); color:#fff; align-self:flex-end; border-bottom-right-radius:4px; }
  .msg-bubble.recv { background:var(--card); color:var(--text); align-self:flex-start; border-bottom-left-radius:4px; border:1.5px solid #2e2b45; }
  .msg-time { font-size:10px; color:var(--muted); font-weight:600; margin-top:2px; }
  .msg-time.sent { text-align:right; }
  .chat-input-bar { position:fixed; bottom:0; left:50%; transform:translateX(-50%); width:100%; max-width:430px; background:var(--surface); border-top:1.5px solid #2e2b45; padding:10px 14px 20px; display:flex; gap:8px; z-index:100; }
  .chat-input { flex:1; background:var(--card); border:1.5px solid #2e2b45; border-radius:22px; padding:10px 16px; font-size:13px; font-family:'Nunito',sans-serif; color:var(--text); outline:none; font-weight:600; }
  .chat-input:focus { border-color:var(--accent4); }
  .chat-send-btn { width:42px; height:42px; background:linear-gradient(135deg,var(--accent4),#1a5a9a); border:none; border-radius:50%; color:#fff; font-size:18px; cursor:pointer; display:flex; align-items:center; justify-content:center; flex-shrink:0; }
  .chat-header-user { display:flex; align-items:center; gap:10px; flex:1; }
  .chat-header-avatar { width:36px; height:36px; border-radius:50%; background:linear-gradient(135deg,var(--accent1),var(--accent5)); display:flex; align-items:center; justify-content:center; font-size:16px; overflow:hidden; }
  .chat-header-name { font-size:15px; font-weight:800; }
  .chat-header-status { font-size:11px; color:var(--accent3); font-weight:600; }
  .empty-chat { display:flex; flex-direction:column; align-items:center; justify-content:center; flex:1; gap:12px; padding:40px; text-align:center; color:var(--muted); }
  /* PHOTO VIEWER */
  #photo-viewer { position:fixed; inset:0; background:rgba(0,0,0,0.95); z-index:999; display:none; align-items:center; justify-content:center; flex-direction:column; gap:16px; }
  #photo-viewer.open { display:flex; }
  #photo-viewer img { max-width:95vw; max-height:80vh; object-fit:contain; border-radius:12px; }
  #photo-viewer-close { position:absolute; top:20px; right:20px; background:rgba(255,255,255,0.1); border:none; color:#fff; font-size:24px; width:44px; height:44px; border-radius:50%; cursor:pointer; display:flex; align-items:center; justify-content:center; }
  /* MULTI PHOTO GALLERY */
  .photo-gallery { display:flex; gap:8px; margin-bottom:16px; overflow-x:auto; scrollbar-width:none; }
  .photo-gallery::-webkit-scrollbar { display:none; }
  .photo-thumb { width:80px; height:80px; border-radius:12px; object-fit:cover; cursor:pointer; border:2px solid transparent; transition:border-color 0.2s; flex-shrink:0; }
  .photo-thumb.active { border-color:var(--accent2); }
  /* EDIT FORM */
  #screen-edit { background:var(--bg); }
  /* MSG BUTTON */
  .msg-btn { display:flex; align-items:center; gap:6px; background:linear-gradient(135deg,#1e2a3a,#1a3a5a); border:1.5px solid var(--accent4); border-radius:12px; padding:8px 14px; font-size:13px; font-weight:700; cursor:pointer; color:var(--accent4); font-family:'Nunito',sans-serif; transition:all 0.2s; }
  /* CHAT */
  .chat-list { display:flex; flex-direction:column; gap:10px; padding:0 20px 100px; flex:1; }
  .chat-item { background:var(--card); border-radius:16px; padding:14px; display:flex; align-items:center; gap:12px; border:1.5px solid #2e2b45; cursor:pointer; transition:transform 0.2s; }
  .chat-item:hover { transform:translateY(-2px); }
  .chat-item-avatar { width:46px; height:46px; border-radius:50%; background:linear-gradient(135deg,var(--accent1),var(--accent5)); display:flex; align-items:center; justify-content:center; font-size:20px; flex-shrink:0; overflow:hidden; }
  .chat-item-info { flex:1; min-width:0; }
  .chat-item-name { font-size:14px; font-weight:800; margin-bottom:3px; }
  .chat-item-preview { font-size:12px; color:var(--muted); font-weight:600; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
  .chat-item-time { font-size:10px; color:var(--muted); font-weight:700; flex-shrink:0; }
  .chat-unread { background:var(--accent1); color:#fff; border-radius:50%; width:18px; height:18px; font-size:10px; font-weight:800; display:flex; align-items:center; justify-content:center; flex-shrink:0; }
  /* CHAT ROOM */
  .chat-messages { flex:1; overflow-y:auto; padding:14px 20px; display:flex; flex-direction:column; gap:10px; padding-bottom:80px; }
  .msg-bubble { max-width:78%; padding:10px 14px; border-radius:18px; font-size:13px; font-weight:600; line-height:1.5; word-wrap:break-word; }
  .msg-mine { background:linear-gradient(135deg,var(--accent4),#2d6aff); color:#fff; align-self:flex-end; border-bottom-right-radius:4px; }
  .msg-theirs { background:var(--card); color:var(--text); align-self:flex-start; border-bottom-left-radius:4px; border:1.5px solid #2e2b45; }
  .msg-time { font-size:10px; opacity:0.7; margin-top:3px; }
  .msg-sender { font-size:10px; color:var(--muted); font-weight:800; margin-bottom:3px; }
  .chat-input-bar { position:fixed; bottom:0; left:50%; transform:translateX(-50%); width:100%; max-width:430px; background:var(--surface); border-top:1.5px solid #2e2b45; padding:10px 14px 24px; display:flex; gap:8px; z-index:100; }
  .chat-input { flex:1; background:var(--card); border:1.5px solid #2e2b45; border-radius:24px; padding:10px 16px; font-size:14px; font-family:'Nunito',sans-serif; color:var(--text); outline:none; font-weight:600; }
  .chat-send-btn { width:42px; height:42px; background:linear-gradient(135deg,var(--accent4),#2d6aff); border:none; border-radius:50%; font-size:18px; cursor:pointer; display:flex; align-items:center; justify-content:center; flex-shrink:0; }
  /* SPLASH */
  #screen-splash { background:var(--bg); align-items:center; justify-content:center; flex-direction:column; gap:20px; }
  .splash-logo { font-family:"Fredoka One",cursive; font-size:42px; text-align:center; background:linear-gradient(135deg,var(--accent2),var(--accent1)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
  .splash-icon { font-size:90px; animation:bounce 1s ease infinite; }
  @keyframes bounce { 0%,100%{transform:translateY(0)}50%{transform:translateY(-12px)} }
  .splash-sub { color:var(--muted); font-size:14px; font-weight:700; }
  /* ONBOARDING */
  #screen-onboarding { background:var(--bg); }
  .ob-slides { flex:1; position:relative; overflow:hidden; }
  .ob-slide { position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center; padding:30px; text-align:center; gap:18px; transition:transform 0.4s ease,opacity 0.4s ease; }
  .ob-slide.left { transform:translateX(-100%); opacity:0; }
  .ob-slide.right { transform:translateX(100%); opacity:0; }
  .ob-slide.show { transform:translateX(0); opacity:1; }
  .ob-emoji { font-size:90px; }
  .ob-title { font-family:"Fredoka One",cursive; font-size:30px; line-height:1.2; }
  .ob-desc { color:var(--muted); font-size:14px; font-weight:600; line-height:1.7; max-width:300px; }
  .ob-feats { display:flex; flex-direction:column; gap:8px; width:100%; }
  .ob-feat { background:var(--card); border-radius:13px; padding:11px 14px; display:flex; align-items:center; gap:10px; border:1.5px solid #2e2b45; text-align:left; }
  .ob-feat-icon { font-size:22px; flex-shrink:0; }
  .ob-feat-txt { font-size:12px; font-weight:700; }
  .ob-dots { display:flex; gap:8px; justify-content:center; padding:16px; }
  .ob-dot { width:8px; height:8px; border-radius:50%; background:#2e2b45; transition:all 0.3s; }
  .ob-dot.on { background:var(--accent2); width:24px; border-radius:4px; }
  .ob-nav { display:flex; gap:10px; padding:0 20px 36px; }
  .ob-skip { flex:1; padding:13px; background:var(--card); border:1.5px solid #2e2b45; border-radius:13px; color:var(--muted); font-family:"Fredoka One",cursive; font-size:15px; cursor:pointer; }
  .ob-next { flex:2; padding:13px; background:linear-gradient(135deg,var(--accent2),var(--accent1)); border:none; border-radius:13px; color:#1a1200; font-family:"Fredoka One",cursive; font-size:16px; cursor:pointer; transition:transform 0.2s; }
  .ob-next:hover { transform:translateY(-2px); }
</style>
</head>
<body>

<!-- SPLASH -->
<div class="screen active" id="screen-splash">
  <div class="splash-icon">🏆</div>
  <div class="splash-logo">Mundo del<br>Coleccionista</div>
  <div class="splash-sub">Cargando tu colección...</div>
  <div style="width:40px;height:4px;background:var(--card);border-radius:4px;overflow:hidden;margin-top:10px">
    <div id="splash-bar" style="height:100%;background:linear-gradient(135deg,var(--accent2),var(--accent1));width:0%;transition:width 1.5s ease;border-radius:4px"></div>
  </div>
</div>

<!-- ONBOARDING -->
<div class="screen" id="screen-onboarding">
  <div class="ob-slides">
    <div class="ob-slide show" id="ob-0">
      <div class="ob-emoji">🔵⭕🃏</div>
      <div class="ob-title" style="background:linear-gradient(135deg,var(--accent2),var(--accent1));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text">Bienvenido a Mundo del Coleccionista</div>
      <div class="ob-desc">La comunidad más grande de coleccionables en español. ¡Identifica, cataloga e intercambia!</div>
      <div class="ob-feats">
        <div class="ob-feat"><div class="ob-feat-icon">🔵</div><div class="ob-feat-txt">Canicas, tazos, cartas y más de 25 categorías</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">👥</div><div class="ob-feat-txt">Miles de coleccionistas como tú</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">🆓</div><div class="ob-feat-txt">Empieza gratis, sin tarjeta de crédito</div></div>
      </div>
    </div>
    <div class="ob-slide right" id="ob-1">
      <div class="ob-emoji">📷</div>
      <div class="ob-title" style="color:var(--accent4)">Aporta tus piezas</div>
      <div class="ob-desc">Sube fotos de tus coleccionables y ayuda a identificarlos. ¡La comunidad te lo agradecerá!</div>
      <div class="ob-feats">
        <div class="ob-feat"><div class="ob-feat-icon">📸</div><div class="ob-feat-txt">Sube fotos de alta calidad</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">📝</div><div class="ob-feat-txt">Agrega descripción, rareza y año</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">⭐</div><div class="ob-feat-txt">Gana puntos por cada aporte</div></div>
      </div>
    </div>
    <div class="ob-slide right" id="ob-2">
      <div class="ob-emoji">🔄</div>
      <div class="ob-title" style="color:var(--accent3)">Intercambia y vende</div>
      <div class="ob-desc">Con el Plan Premium puedes intercambiar piezas con otros usuarios. ¡Encuentra lo que buscas!</div>
      <div class="ob-feats">
        <div class="ob-feat"><div class="ob-feat-icon">🔄</div><div class="ob-feat-txt">Sistema de intercambio entre usuarios</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">💬</div><div class="ob-feat-txt">Chat directo para coordinar</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">🏪</div><div class="ob-feat-txt">Vende tus piezas con Plan Pro</div></div>
      </div>
    </div>
    <div class="ob-slide right" id="ob-3">
      <div class="ob-emoji">🏆</div>
      <div class="ob-title" style="color:var(--accent5)">¡Empieza ahora!</div>
      <div class="ob-desc">Únete a la comunidad gratis y comienza a construir tu colección digital hoy mismo.</div>
      <div class="ob-feats">
        <div class="ob-feat"><div class="ob-feat-icon">🆓</div><div class="ob-feat-txt">Plan Gratis — 3 aportes/mes</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">⭐</div><div class="ob-feat-txt">Premium $1.99/mes — Ilimitado</div></div>
        <div class="ob-feat"><div class="ob-feat-icon">👑</div><div class="ob-feat-txt">Pro $4.99/mes — Todo incluido</div></div>
      </div>
    </div>
  </div>
  <div class="ob-dots">
    <div class="ob-dot on" id="dot-0"></div>
    <div class="ob-dot" id="dot-1"></div>
    <div class="ob-dot" id="dot-2"></div>
    <div class="ob-dot" id="dot-3"></div>
  </div>
  <div class="ob-nav">
    <button class="ob-skip" onclick="finishOnboarding()">Saltar</button>
    <button class="ob-next" id="ob-next-btn" onclick="nextSlide()">Siguiente →</button>
  </div>
</div>

<!-- HOME -->
<div class="screen" id="screen-home">
  <div class="topbar">
    <div class="logo">Mundo del <span>Coleccionista</span></div>
    <button class="user-btn" onclick="goProfile()">😎</button>
  </div>
  <div class="search-wrap">
    <div class="search-bar">
      <span>🔍</span>
      <input id="search-input" type="text" placeholder="Buscar en el catálogo…" oninput="filterItems()">
    </div>
  </div>
  <div class="pills" id="cat-pills"></div>
  <div class="section-title">
    <span id="items-count">Cargando…</span>
    <span style="font-size:12px;color:var(--accent4);cursor:pointer" onclick="showScreen('screen-planes')">✨ Premium</span>
  </div>
  <div class="grid" id="items-grid">
    <div class="loading"><div class="spinner"></div></div>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn active" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn" onclick="goChats()"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- DETAIL -->
<div class="screen" id="screen-detail">
  <div class="back-row">
    <button class="back-btn" onclick="showScreen('screen-home')">←</button>
    <span style="font-weight:800;font-size:15px">Detalle</span>
  </div>
  <div class="detail-wrap">
    <div class="detail-hero" id="d-hero" onclick="openPhotoViewer(0)" style="cursor:pointer">🔵</div>
    <div class="photo-gallery" id="d-gallery" style="display:none"></div>
    <div style="display:flex;gap:8px;margin-bottom:14px" id="d-action-btns">
      <button class="msg-btn" id="btn-msg" onclick="msgOwner()" style="display:none">💬 Mensaje</button>
      <button class="msg-btn" id="btn-edit-aporte" onclick="openEdit()" style="display:none;border-color:var(--accent2);color:var(--accent2)">✏️ Editar</button>
    </div>
    <div class="detail-name" id="d-name">—</div>
    <div class="detail-sub" id="d-sub">—</div>
    <div id="d-location-wrap" style="margin-bottom:6px;display:none"><span style="background:var(--card);border:1.5px solid #2e2b45;border-radius:20px;padding:4px 12px;font-size:11px;font-weight:800;color:var(--accent3)"></span></div>
    <div id="d-marca-wrap" style="margin-bottom:10px;display:none"><span id="d-marca" style="background:var(--card);border:1.5px solid #2e2b45;border-radius:20px;padding:4px 12px;font-size:11px;font-weight:800;color:var(--accent2)"></span></div>
    <div class="tags" id="d-tags"></div>
    <div class="stats-row">
      <div class="stat-box"><div class="stat-val" id="d-views">0</div><div class="stat-lbl">Vistos</div></div>
      <div class="stat-box"><div class="stat-val" id="d-likes">0</div><div class="stat-lbl">Likes</div></div>
      <div class="stat-box"><div class="stat-val" id="d-year">—</div><div class="stat-lbl">Año</div></div>
    </div>
    <div class="desc-box" id="d-desc">—</div>
    <div style="display:flex;gap:10px;margin-bottom:14px">
      <button class="like-btn" id="btn-like" onclick="toggleLike()">❤️ <span id="like-label">Me gusta</span></button>
    </div>
    <div style="font-size:14px;font-weight:800;margin-bottom:8px">Aportado por</div>
    <div class="owner-box" id="owner-box-link" onclick="openPublicProfile()" style="cursor:pointer">
      <div class="owner-avatar" id="d-owner-avatar">😊</div>
      <div>
        <div style="font-size:13px;font-weight:800" id="d-owner">—</div>
        <div style="font-size:11px;color:var(--muted);font-weight:600" id="d-date">—</div>
      </div>
      <span style="margin-left:auto;color:var(--muted);font-size:18px">›</span>
    </div>
    <div class="comments-wrap">
      <div style="font-size:14px;font-weight:800;margin-bottom:10px">Comentarios</div>
      <div id="comments-list"></div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <input class="form-input" id="comment-input" placeholder="Escribe un comentario…" style="flex:1">
        <button onclick="addComment()" style="padding:11px 16px;background:var(--accent4);border:none;border-radius:13px;color:#fff;font-weight:800;cursor:pointer;font-family:'Nunito',sans-serif">→</button>
      </div>
    </div>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn" onclick="goChats()"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- UPLOAD -->
<div class="screen" id="screen-upload">
  <div class="topbar">
    <div class="logo">Aportar <span>Pieza</span></div>
    <button class="back-btn" onclick="showScreen('screen-home')" style="background:var(--card);border:none;border-radius:11px;width:34px;height:34px;font-size:15px;cursor:pointer;color:var(--text)">✕</button>
  </div>
  <div class="upload-wrap">
    <div class="upload-title">¡Comparte tu hallazgo!</div>
    <div class="upload-sub">Ayuda a la comunidad a identificar más piezas</div>
    <div style="margin-bottom:14px">
      <label class="form-label">Fotos (hasta 3)</label>
      <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px">
        <div class="upload-zone" style="aspect-ratio:1;height:auto;margin-bottom:0" onclick="document.getElementById('file-input-0').click()">
          <img id="img-preview-0" alt="preview" style="width:100%;height:100%;object-fit:cover;position:absolute;inset:0;display:none;border-radius:var(--radius)">
          <span style="font-size:24px">📷</span>
          <p style="font-size:10px;color:var(--muted);font-weight:700">Foto 1</p>
          <input type="file" id="file-input-0" accept="image/*" onchange="previewImgMulti(event,0)" style="display:none">
        </div>
        <div class="upload-zone" style="aspect-ratio:1;height:auto;margin-bottom:0" onclick="document.getElementById('file-input-1').click()">
          <img id="img-preview-1" alt="preview" style="width:100%;height:100%;object-fit:cover;position:absolute;inset:0;display:none;border-radius:var(--radius)">
          <span style="font-size:24px">➕</span>
          <p style="font-size:10px;color:var(--muted);font-weight:700">Foto 2</p>
          <input type="file" id="file-input-1" accept="image/*" onchange="previewImgMulti(event,1)" style="display:none">
        </div>
        <div class="upload-zone" style="aspect-ratio:1;height:auto;margin-bottom:0" onclick="document.getElementById('file-input-2').click()">
          <img id="img-preview-2" alt="preview" style="width:100%;height:100%;object-fit:cover;position:absolute;inset:0;display:none;border-radius:var(--radius)">
          <span style="font-size:24px">➕</span>
          <p style="font-size:10px;color:var(--muted);font-weight:700">Foto 3</p>
          <input type="file" id="file-input-2" accept="image/*" onchange="previewImgMulti(event,2)" style="display:none">
        </div>
      </div>
    </div>

    <div class="form-field">
      <label class="form-label">Nombre de la pieza</label>
      <input class="form-input" id="f-nombre" type="text" placeholder="Ej: Canica ojo de gato verde">
    </div>
    <div class="form-field">
      <label class="form-label">Categoría</label>
      <select class="form-select" id="f-categoria" onchange="updateMarcas()"></select>
    </div>
    <div class="form-field" id="marca-field">
      <label class="form-label">Marca / Serie</label>
      <select class="form-select" id="f-marca">
        <option value="">Selecciona categoría primero</option>
      </select>
      <input class="form-input" id="f-marca-custom" type="text" placeholder="Escribe la marca..." style="display:none;margin-top:8px">
    </div>
    <div class="form-field">
      <label class="form-label">Rareza</label>
      <select class="form-select" id="f-rareza">
        <option value="Común">Común</option>
        <option value="Poco común">Poco común</option>
        <option value="Rara">Rara</option>
        <option value="Legendaria">Legendaria</option>
      </select>
    </div>
    <div class="form-field">
      <label class="form-label">Año aproximado</label>
      <input class="form-input" id="f-año" type="text" placeholder="Ej: 1990s, 2000, Desconocido">
    </div>
    <div class="form-field">
      <label class="form-label">Descripción</label>
      <textarea class="form-input" id="f-desc" rows="3" placeholder="Materiales, características especiales…" style="resize:none"></textarea>
    </div>
    <div class="form-field">
      <label class="form-label">📍 Ubicación (opcional)</label>
      <input class="form-input" id="f-ubicacion" type="text" placeholder="Ej: Ciudad de México, Guadalajara, Monterrey…">
    </div>
    <button class="submit-btn" id="btn-submit" onclick="submitPieza()">Publicar aporte 🚀</button>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn active"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn" onclick="goChats()"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- PLANES -->
<div class="screen" id="screen-planes">
  <div class="topbar">
    <div class="logo">Elige tu <span>Plan</span></div>
    <button class="back-btn" onclick="showScreen('screen-home')" style="background:var(--card);border:none;border-radius:11px;width:34px;height:34px;font-size:15px;cursor:pointer;color:var(--text)">✕</button>
  </div>
  <div class="planes-wrap">

    <div class="plan-card plan-free">
      <div class="plan-badge" style="background:#2e2b45;color:var(--muted)">GRATIS</div>
      <div class="plan-title">Plan Gratis</div>
      <div class="plan-price">$0 <span>/mes</span></div>
      <ul class="plan-features">
        <li>✅ Ver catálogo completo gratis</li>
        <li>✅ Comentar y reaccionar</li>
        <li>✅ 10 aportes por mes</li>
        <li>✅ Categorías: Canicas, Tazos, Cartas, Cochesitos, Dinosaurios, Peluches, Muñecas, Figuras de acción, Pokémon/Yu-Gi-Oh/Magic</li>
        <li>❌ Con anuncios</li>
      </ul>
      <button class="plan-btn" style="background:var(--card);color:var(--muted);border:1.5px solid #2e2b45" onclick="showToast('Ya tienes el plan gratis ✅')">Plan actual</button>
    </div>

    <div class="plan-card plan-premium">
      <div class="plan-badge" style="background:var(--accent3);color:#0a1a0a">⭐ POPULAR</div>
      <div class="plan-title" style="color:var(--accent3)">Plan Premium</div>
      <div class="plan-price" style="color:var(--accent3)">$1.99 <span>/mes</span></div>
      <ul class="plan-features">
        <li>✅ Todo lo del plan gratis</li>
        <li>✅ Sin anuncios</li>
        <li>✅ Aportes ilimitados</li>
        <li>✅ Sistema de intercambio entre usuarios</li>
        <li>✅ Categorías extra: Monedas, Tenis/Zapatos, Gorras, Ropa, Perfumes, Relojes, Funkos, Legos, Videojuegos, Tazas, Máscaras, Encendedores</li>
        <li>✅ Insignia Premium ⭐</li>
      </ul>
      <button class="plan-btn" style="background:var(--accent3);color:#0a1a0a" onclick="activarPlan('premium')">Obtener Premium ⭐</button>
    </div>

    <div class="plan-card plan-pro">
      <div class="plan-badge" style="background:var(--accent5);color:#fff">👑 PRO</div>
      <div class="plan-title" style="color:var(--accent5)">Plan Pro</div>
      <div class="plan-price" style="color:var(--accent5)">$4.99 <span>/mes</span></div>
      <ul class="plan-features">
        <li>✅ Todo lo del plan Premium</li>
        <li>✅ Estadísticas de tu colección</li>
        <li>✅ Exportar colección en PDF</li>
        <li>✅ Venta de piezas via chat</li>
        <li>✅ Catálogo privado</li>
        <li>✅ Insignia de Vendedor 🏪 y Aportador 🏆</li>
        <li>✅ Categorías exclusivas: Automóviles, Arte, Piedras/Minerales, Bebidas coleccionables</li>
      </ul>
      <button class="plan-btn" style="background:var(--accent5);color:#fff" onclick="activarPlan('pro')">Obtener Pro 👑</button>
    </div>

  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn active"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- CHATS LIST -->
<div class="screen" id="screen-chats">
  <div class="topbar">
    <div class="logo">Mis <span>Mensajes</span></div>
  </div>
  <div id="chats-list" class="chat-list"></div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn active"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- CHAT MESSAGES -->
<div class="screen" id="screen-chat-messages">
  <div class="topbar" style="padding-bottom:10px">
    <button class="back-btn" onclick="showScreen('screen-chats')" style="background:var(--card);border:none;border-radius:11px;width:34px;height:34px;font-size:15px;cursor:pointer;color:var(--text)">←</button>
    <div class="chat-header-user">
      <div class="chat-header-avatar" id="chat-header-avatar">😊</div>
      <div>
        <div class="chat-header-name" id="chat-header-name">—</div>
        <div class="chat-header-status">Coleccionista</div>
      </div>
    </div>
  </div>
  <div class="messages-wrap" id="messages-wrap"></div>
  <div class="chat-input-bar">
    <input class="chat-input" id="chat-msg-input" placeholder="Escribe un mensaje…" onkeypress="if(event.key==='Enter')sendMessage()">
    <button class="chat-send-btn" onclick="sendMessage()">➤</button>
  </div>
</div>

<!-- AUTH -->
<div class="screen" id="screen-auth">
  <div class="auth-wrap">
    <div class="auth-icon">🏆</div>
    <div class="auth-title">Únete a la comunidad</div>
    <div class="auth-sub">Crea tu cuenta para aportar piezas y construir tu colección</div>
    <button class="auth-btn btn-google" onclick="loginGoogle()">
      <svg width="18" height="18" viewBox="0 0 48 48"><path fill="#EA4335" d="M24 9.5c3.54 0 6.71 1.22 9.21 3.6l6.85-6.85C35.9 2.38 30.47 0 24 0 14.62 0 6.51 5.38 2.56 13.22l7.98 6.19C12.43 13.72 17.74 9.5 24 9.5z"/><path fill="#4285F4" d="M46.98 24.55c0-1.57-.15-3.09-.38-4.55H24v9.02h12.94c-.58 2.96-2.26 5.48-4.78 7.18l7.73 6c4.51-4.18 7.09-10.36 7.09-17.65z"/><path fill="#FBBC05" d="M10.53 28.59c-.48-1.45-.76-2.99-.76-4.59s.27-3.14.76-4.59l-7.98-6.19C.92 16.46 0 20.12 0 24c0 3.88.92 7.54 2.56 10.78l7.97-6.19z"/><path fill="#34A853" d="M24 48c6.48 0 11.93-2.13 15.89-5.81l-7.73-6c-2.18 1.48-4.97 2.35-8.16 2.35-6.26 0-11.57-4.22-13.47-9.91l-7.98 6.19C6.51 42.62 14.62 48 24 48z"/></svg>
      Continuar con Google
    </button>
    <div class="auth-divider">— o con correo —</div>
    <div class="auth-form">
      <input class="form-input" id="auth-email" type="email" placeholder="tu@correo.com">
      <input class="form-input" id="auth-pass" type="password" placeholder="Contraseña">
      <input class="form-input" id="auth-name" type="text" placeholder="Tu nombre o apodo" style="display:none">
      <button class="auth-btn btn-primary" id="btn-auth-action" onclick="authAction()">Iniciar sesión</button>
      <div class="auth-toggle" id="auth-toggle" onclick="toggleAuthMode()">¿No tienes cuenta? Regístrate</div>
    </div>
  </div>
</div>

<!-- PROFILE -->
<div class="screen" id="screen-profile">
  <div class="topbar">
    <div class="logo">Mi <span>Perfil</span></div>
  </div>
  <div class="profile-wrap">
    <div class="profile-hero">
      <div style="position:relative;display:inline-block">
        <div class="profile-avatar" id="p-avatar" style="overflow:hidden;cursor:pointer" onclick="document.getElementById('avatar-input').click()">😎</div>
        <div style="position:absolute;bottom:0;right:0;background:var(--accent4);border-radius:50%;width:22px;height:22px;display:flex;align-items:center;justify-content:center;font-size:12px;cursor:pointer" onclick="document.getElementById('avatar-input').click()">📷</div>
        <input type="file" id="avatar-input" accept="image/*" style="display:none" onchange="uploadAvatar(event)">
      </div>
      <div style="font-size:10px;color:var(--muted);font-weight:600">Toca para cambiar foto</div>
      <div class="profile-name" id="p-name">—</div>
      <div class="profile-email" id="p-email">—</div>
      <div class="plan-chip" id="p-plan-chip" style="background:#2e2b45;color:var(--muted)">🆓 Plan Gratis</div>
    </div>
    <div class="profile-stats">
      <div class="stat-box"><div class="stat-val" id="p-aportes">0</div><div class="stat-lbl">Mis aportes</div></div>
      <div class="stat-box"><div class="stat-val" id="p-total">0</div><div class="stat-lbl">Comunidad</div></div>
    </div>
    <div style="font-size:14px;font-weight:800;margin-bottom:10px">Mis aportes recientes</div>
    <div id="my-items-list" style="display:flex;flex-direction:column;gap:8px;margin-bottom:16px"></div>
    <button class="submit-btn" style="margin-bottom:10px" onclick="showScreen('screen-planes')">⭐ Ver planes Premium</button>
    <button class="logout-btn" onclick="logout()">Cerrar sesión 👋</button>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn" onclick="goChats()"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn active"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- CHATS LIST -->
<div class="screen" id="screen-chats">
  <div class="topbar">
    <div class="logo">Mis <span>Chats</span></div>
    <div id="chats-unread-badge" style="display:none;background:var(--accent1);color:#fff;border-radius:20px;padding:3px 10px;font-size:11px;font-weight:800">0</div>
  </div>
  <div id="chats-empty" style="display:none;text-align:center;padding:60px 20px;color:var(--muted)">
    <div style="font-size:56px;margin-bottom:12px">💬</div>
    <p style="font-weight:700">Sin chats aún</p>
    <p style="font-size:12px;margin-top:6px">Toca el botón 💬 en cualquier pieza para iniciar una conversación</p>
  </div>
  <div class="chat-list" id="chats-list"></div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn active"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- CHAT ROOM -->
<div class="screen" id="screen-chat-room">
  <div class="back-row" style="border-bottom:1.5px solid #2e2b45;padding-bottom:14px">
    <button class="back-btn" onclick="showScreen('screen-chats')">←</button>
    <div id="chat-room-avatar" style="width:34px;height:34px;border-radius:50%;background:linear-gradient(135deg,var(--accent1),var(--accent5));display:flex;align-items:center;justify-content:center;font-size:16px;overflow:hidden;flex-shrink:0"></div>
    <div style="flex:1">
      <div style="font-weight:800;font-size:14px" id="chat-room-name">—</div>
      <div style="font-size:11px;color:var(--muted);font-weight:600" id="chat-room-sub">—</div>
    </div>
  </div>
  <div class="chat-messages" id="chat-messages"></div>
  <div class="chat-input-bar">
    <input class="chat-input" id="chat-msg-input" placeholder="Escribe un mensaje…" onkeydown="if(event.key==='Enter')sendChatMsg()">
    <button class="chat-send-btn" onclick="sendChatMsg()">➤</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<!-- PHOTO VIEWER -->
<div id="photo-viewer">
  <button id="photo-viewer-close" onclick="closePhotoViewer()">✕</button>
  <img id="photo-viewer-img" src="" alt="foto">
</div>

<!-- EDIT SCREEN -->
<div class="screen" id="screen-edit">
  <div class="back-row">
    <button class="back-btn" onclick="showScreen('screen-detail')">←</button>
    <span style="font-weight:800;font-size:15px">Editar aporte</span>
  </div>
  <div class="upload-wrap">
    <div class="form-field">
      <label class="form-label">Nombre de la pieza</label>
      <input class="form-input" id="edit-nombre" type="text">
    </div>
    <div class="form-field">
      <label class="form-label">Rareza</label>
      <select class="form-select" id="edit-rareza">
        <option value="Común">Común</option>
        <option value="Poco común">Poco común</option>
        <option value="Rara">Rara</option>
        <option value="Legendaria">Legendaria</option>
      </select>
    </div>
    <div class="form-field">
      <label class="form-label">Año aproximado</label>
      <input class="form-input" id="edit-año" type="text">
    </div>
    <div class="form-field">
      <label class="form-label">Descripción</label>
      <textarea class="form-input" id="edit-desc" rows="3" style="resize:none"></textarea>
    </div>
    <div class="form-field">
      <label class="form-label">📍 Ubicación</label>
      <input class="form-input" id="edit-ubicacion" type="text">
    </div>
    <button class="submit-btn" id="btn-edit-submit" onclick="saveEdit()">Guardar cambios ✅</button>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<!-- PUBLIC PROFILE -->
<div class="screen" id="screen-public-profile">
  <div class="back-row">
    <button class="back-btn" onclick="showScreen('screen-detail')">←</button>
    <span style="font-weight:800;font-size:15px">Perfil del coleccionista</span>
  </div>
  <div class="profile-wrap">
    <div class="profile-hero">
      <div class="profile-avatar" id="pp-avatar">😎</div>
      <div class="profile-name" id="pp-name">—</div>
      <div class="plan-chip" id="pp-plan-chip" style="background:#2e2b45;color:var(--muted)">🆓 Plan Gratis</div>
    </div>
    <div class="profile-stats">
      <div class="stat-box"><div class="stat-val" id="pp-aportes">0</div><div class="stat-lbl">Aportes</div></div>
      <div class="stat-box"><div class="stat-val" id="pp-likes">0</div><div class="stat-lbl">Likes totales</div></div>
    </div>
    <div style="display:flex;gap:8px;margin-bottom:16px" id="pp-action-btns">
      <button class="msg-btn" id="pp-btn-msg" onclick="msgFromProfile()">💬 Enviar mensaje</button>
    </div>
    <div style="font-size:14px;font-weight:800;margin-bottom:10px">Catálogo público</div>
    <div class="grid" id="pp-items-grid" style="padding:0 0 100px"></div>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="showScreen('screen-home')"><span>🏠</span><span>Inicio</span></button>
    <button class="nav-btn" onclick="showScreen('screen-upload')"><span>➕</span><span>Aportar</span></button>
    <button class="nav-btn" onclick="goChats()"><span>💬</span><span>Chats</span></button>
    <button class="nav-btn" onclick="showScreen('screen-planes')"><span>⭐</span><span>Planes</span></button>
    <button class="nav-btn" onclick="goProfile()"><span>👤</span><span>Perfil</span></button>
  </nav>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getFirestore, collection, addDoc, getDocs, doc, updateDoc, increment, query, orderBy, serverTimestamp, getDoc, setDoc, arrayUnion, arrayRemove, where, onSnapshot } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
import { getAuth, signInWithPopup, GoogleAuthProvider, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged, updateProfile } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";

const firebaseConfig = {
  apiKey: "AIzaSyCRdeRJWOC-Cf2CGqd4mqEO8s7_8cHF79g",
  authDomain: "mundo-del-coleccionista.firebaseapp.com",
  projectId: "mundo-del-coleccionista",
  storageBucket: "mundo-del-coleccionista.firebasestorage.app",
  messagingSenderId: "590307203433",
  appId: "1:590307203433:web:db880bae039bf61d5485f8",
  measurementId: "G-MFXDW8EKL2"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);
const provider = new GoogleAuthProvider();

// ── CATEGORÍAS ──
const CATS_FREE = [
  {id:'todos', label:'🌟 Todos'},
  {id:'canica', label:'🔵 Canicas'},
  {id:'tazo', label:'⭕ Tazos'},
  {id:'carta', label:'🃏 Cartas TCG'},
  {id:'auto_escala', label:'🚗 Autos a Escala'},
  {id:'dinosaurio', label:'🦕 Dinosaurios'},
  {id:'peluche', label:'🧸 Peluches'},
  {id:'muneca', label:'👧 Muñecas/Figuras'},
  {id:'figura', label:'🦸 Figuras de Acción'},
  {id:'tazo', label:'⭕ Tazos'},
  {id:'planta', label:'🌱 Plantas'},
];

const CATS_PREMIUM = [
  {id:'moneda', label:'🪙 Monedas Coleccionables'},
  {id:'tenis', label:'👟 Tenis/Zapatos'},
  {id:'gorra', label:'🧢 Gorras'},
  {id:'ropa', label:'👕 Ropa'},
  {id:'perfume', label:'🌸 Perfumes'},
  {id:'reloj', label:'⌚ Relojes'},
  {id:'funko', label:'🎭 Funkos'},
  {id:'lego', label:'🧱 Legos'},
  {id:'videojuego', label:'🎮 Videojuegos'},
  {id:'taza', label:'☕ Tazas'},
  {id:'mascara', label:'🎭 Máscaras'},
  {id:'encendedor', label:'🔥 Encendedores'},
];

const CATS_PRO = [
  {id:'automovil', label:'🚘 Automóviles'},
  {id:'arte', label:'🎨 Arte'},
  {id:'mineral', label:'💎 Piedras/Minerales'},
  {id:'bebida', label:'🍺 Bebidas coleccionables'},
];

const ALL_CATS = [...CATS_FREE, ...CATS_PREMIUM, ...CATS_PRO];

// ── MARCAS POR CATEGORÍA ──
const MARCAS = {
  canica: ['Agaclate','Vitro','Peltier','Jabo','Vacor','Otra marca'],
  carta: ['Pokémon TCG','Yu-Gi-Oh!','Magic: The Gathering','Dragon Ball Super Card','One Piece TCG','Digimon TCG','Otra marca'],
  auto_escala: ['Hot Wheels','Matchbox','Maisto','Micro Machines','Johnny Lightning','Greenlight','Bburago','Jada Toys','Otra marca'],
  tazo: ['Sabritas/Frito-Lay','Matutano','Pokémon Tazos','Disney Tazos','Dragon Ball Tazos','Marvel Tazos','Otro'],
  dinosaurio: ['Schleich','Safari Ltd','Papo','CollectA','PNSO','Otra marca'],
  peluche: ['Ty Beanie Babies','Build-A-Bear','Disney','Squishmallow','Jellycat','Otro'],
  muneca: ['Barbie','Bratz','Monster High','LOL Surprise','Polly Pocket','My Little Pony','Otra marca'],
  figura: ['NECA','McFarlane','Hasbro','Bandai','Funko','S.H.Figuarts','Marvel Legends','DC Multiverse','Otra marca'],
  moneda: ['Casa de Moneda de México','Casa de Moneda de España','U.S. Mint','Royal Mint','Otra ceca'],
  tenis: ['Nike','Adidas','Jordan','New Balance','Vans','Converse','Yeezy','Otra marca'],
  gorra: ['New Era','Mitchell & Ness','47 Brand','Flexfit','Supreme','Otra marca'],
  ropa: ['Supreme','Bape','Off-White','Nike','Adidas','Stüssy','Otra marca'],
  perfume: ['Chanel','Dior','Versace','Calvin Klein','Hugo Boss','Tom Ford','Otra marca'],
  reloj: ['Casio G-Shock','Swatch','Seiko','Citizen','Fossil','Invicta','Otra marca'],
  funko: ['Funko Pop','Funko Soda','Funko Bitty Pop','Funko Vinyl Soda','Otro'],
  lego: ['LEGO City','LEGO Technic','LEGO Star Wars','LEGO Harry Potter','LEGO Marvel','LEGO Disney','Otro set'],
  videojuego: ['Nintendo','PlayStation','Xbox','Sega','Atari','Game Boy','Otro'],
  taza: ['Starbucks','Disney','Marvel','Star Wars','Anime','Personalizada','Otra'],
  mascara: ['Luchador Mexicano','Lucha AAA','WWE','Halloween','Otro'],
  encendedor: ['Zippo','Bic','Dupont','Ronson','Otro'],
  automovil: ['Hot Wheels Premium','Johnny Lightning','Greenlight Collectibles','AutoArt','Spark Model','Minichamps','Otro'],
  arte: ['Pintura al óleo','Acuarela','Escultura','Litografía','Serigrafía','Otro'],
  mineral: ['Amatista','Cuarzo','Obsidiana','Turquesa','Malaquita','Pirita','Otro'],
  bebida: ['Cerveza','Vino','Whisky','Tequila','Mezcal','Licor','Otro'],
  cochesito: ['Hot Wheels','Matchbox','Maisto','Micro Machines','Otra marca'],
  pokemon: ['Pokémon TCG','Yu-Gi-Oh!','Magic: The Gathering','Dragon Ball','Otra'],
  planta: ['Suculentas','Cactus','Helechos','Orquídeas','Bonsái','Plantas carnívoras','Bromelias','Crasas','Otra especie'],
  otro: ['Otro'],
};



const EMOJIS = {canica:'🔵',tazo:'⭕',carta:'🃏',auto_escala:'🚗',cochesito:'🚗',planta:'🌱',dinosaurio:'🦕',peluche:'🧸',muneca:'👧',figura:'🦸',pokemon:'⚡',moneda:'🪙',tenis:'👟',gorra:'🧢',ropa:'👕',perfume:'🌸',reloj:'⌚',funko:'🎭',lego:'🧱',videojuego:'🎮',taza:'☕',mascara:'😷',encendedor:'🔥',automovil:'🚘',arte:'🎨',mineral:'💎',bebida:'🍺',otro:'🎴'};
const COLORS = {canica:'#4d96ff',tazo:'#6bcb77',carta:'#c77dff',auto_escala:'#ff6b6b',cochesito:'#ff6b6b',planta:'#6bcb77',dinosaurio:'#6bcb77',peluche:'#ffd93d',muneca:'#ff6b6b',figura:'#c77dff',pokemon:'#ffd93d',moneda:'#ffd93d',tenis:'#4d96ff',gorra:'#6bcb77',ropa:'#ff6b6b',perfume:'#c77dff',reloj:'#4d96ff',funko:'#c77dff',lego:'#ffd93d',videojuego:'#4d96ff',taza:'#ff6b6b',mascara:'#c77dff',encendedor:'#ff6b6b',automovil:'#4d96ff',arte:'#c77dff',mineral:'#6bcb77',bebida:'#ffd93d',otro:'#a7a9be'};

// ── STATE ──
let currentUser = null;
let userPlan = 'free'; // free | premium | pro
let allItems = [];
let currentCat = 'todos';
let isRegister = false;
let selectedFile = null;
let currentDetailId = null;

// ── BUILD PILLS ──
function buildPills() {
  const wrap = document.getElementById('cat-pills');
  const cats = userPlan === 'pro' ? ALL_CATS : userPlan === 'premium' ? [...CATS_FREE, ...CATS_PREMIUM] : CATS_FREE;
  wrap.innerHTML = cats.map(c => `<button class="pill${c.id===currentCat?' sel':''}" onclick="filterCat('${c.id}',this)">${c.label}</button>`).join('');
}

// ── BUILD UPLOAD SELECT ──
function buildUploadSelect() {
  const sel = document.getElementById('f-categoria');
  const cats = userPlan === 'pro' ? ALL_CATS.slice(1) : userPlan === 'premium' ? [...CATS_FREE, ...CATS_PREMIUM].slice(1) : CATS_FREE.slice(1);
  sel.innerHTML = cats.map(c => `<option value="${c.id}">${c.label}</option>`).join('');
  updateMarcas();
}

window.updateMarcas = () => {
  const cat = document.getElementById('f-categoria').value;
  const marcas = MARCAS[cat] || ['Otra marca'];
  const sel = document.getElementById('f-marca');
  sel.innerHTML = marcas.map(m => `<option value="${m}">${m}</option>`).join('');
  document.getElementById('f-marca-custom').style.display = 'none';
  sel.onchange = () => {
    const custom = document.getElementById('f-marca-custom');
    custom.style.display = sel.value === 'Otra marca' || sel.value === 'Otro' ? '' : 'none';
  };
};

// ── AUTH STATE ──
onAuthStateChanged(auth, async user => {
  currentUser = user;
  if (user) {
    // Load user plan from Firestore
    try {
      const uDoc = await getDoc(doc(db, 'usuarios', user.uid));
      if (uDoc.exists()) userPlan = uDoc.data().plan || 'free';
      else userPlan = 'free';
    } catch(e) { userPlan = 'free'; }
    document.getElementById('p-name').textContent = user.displayName || 'Coleccionista';
    document.getElementById('p-email').textContent = user.email;
    // Load avatar
    try {
      const uDoc = await getDoc(doc(db, 'usuarios', user.uid));
      if (uDoc.exists() && uDoc.data().avatarUrl) {
        const av = uDoc.data().avatarUrl;
        document.getElementById('p-avatar').innerHTML = `<img src="${av}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
        document.querySelector('.user-btn').innerHTML = `<img src="${av}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
      }
    } catch(e) {}
    updatePlanChip();
  } else {
    userPlan = 'free';
  }
  buildPills();
  buildUploadSelect();
});

function updatePlanChip() {
  const chip = document.getElementById('p-plan-chip');
  if (userPlan === 'pro') { chip.style.background='#2d1b69'; chip.style.color='#c77dff'; chip.textContent='👑 Plan Pro'; }
  else if (userPlan === 'premium') { chip.style.background='#1a2a1a'; chip.style.color='#6bcb77'; chip.textContent='⭐ Plan Premium'; }
  else { chip.style.background='#2e2b45'; chip.style.color='var(--muted)'; chip.textContent='🆓 Plan Gratis'; }
}

// ── LOAD ITEMS ──
async function loadItems() {
  try {
    const q = query(collection(db, 'piezas'), orderBy('createdAt', 'desc'));
    const snap = await getDocs(q);
    allItems = snap.docs.map(d => ({ id: d.id, ...d.data() }));
    renderItems(allItems);
  } catch(e) {
    document.getElementById('items-grid').innerHTML = '<div style="grid-column:span 2;text-align:center;padding:40px;color:var(--muted);font-weight:700">Error cargando datos.</div>';
  }
}

function renderItems(items) {
  const grid = document.getElementById('items-grid');
  document.getElementById('items-count').textContent = `${items.length} pieza${items.length!==1?'s':''} encontrada${items.length!==1?'s':''}`;
  if (!items.length) {
    grid.innerHTML = '<div class="empty"><div class="big">🔍</div><p>No hay piezas aún.<br>¡Sé el primero en aportar!</p></div>';
    return;
  }
  // Check if category is locked for user
  const allowedCats = userPlan==='pro' ? ALL_CATS.map(c=>c.id) : userPlan==='premium' ? [...CATS_FREE,...CATS_PREMIUM].map(c=>c.id) : CATS_FREE.map(c=>c.id);
  grid.innerHTML = items.map(item => {
    const locked = !allowedCats.includes(item.categoria);
    return `
    <div class="col-card" onclick="${locked?`showToast('🔒 Necesitas Premium para ver esta categoría')`:  `openDetail('${item.id}')`}">
      <div class="col-card-img" style="background:linear-gradient(135deg,#1a1828,#221f35)">
        ${item.imageUrl ? `<img src="${item.imageUrl}" style="width:100%;height:100%;object-fit:cover;position:absolute;inset:0">` : `<span style="font-size:48px">${EMOJIS[item.categoria]||'🎴'}</span>`}
        <div class="col-badge" style="background:${COLORS[item.categoria]||'#4d96ff'}">${item.categoria||'otro'}</div>
        ${locked?'<div class="lock-overlay">🔒</div>':''}
      </div>
      <div class="col-card-info">
        <div class="col-card-name">${locked?'🔒 '+item.nombre:item.nombre}</div>
        <div class="col-card-meta">
          <span class="rdot" style="background:${COLORS[item.categoria]||'#4d96ff'}"></span>
          ${item.marca ? item.marca+' · ' : ''}${item.rareza||'—'}
        </div>
      </div>
    </div>`}).join('');
}

// ── FILTER ──
window.filterCat = (cat, btn) => {
  currentCat = cat;
  document.querySelectorAll('.pill').forEach(p => p.classList.remove('sel'));
  btn.classList.add('sel');
  applyFilters();
};
window.filterItems = () => applyFilters();
function applyFilters() {
  const search = document.getElementById('search-input').value.toLowerCase();
  let filtered = allItems;
  if (currentCat !== 'todos') filtered = filtered.filter(i => i.categoria === currentCat);
  if (search) filtered = filtered.filter(i => i.nombre.toLowerCase().includes(search)||(i.descripcion||'').toLowerCase().includes(search));
  renderItems(filtered);
}

// ── DETAIL ──
window.openDetail = async (id) => {
  const item = allItems.find(i => i.id === id);
  if (!item) return;
  currentDetailId = id;
  try { await updateDoc(doc(db, 'piezas', id), { vistas: increment(1) }); } catch(e) {}
  const allPhotos = item.imageUrls && item.imageUrls.length ? item.imageUrls : (item.imageUrl ? [item.imageUrl] : []);
  window._currentPhotos = allPhotos;
  document.getElementById('d-hero').innerHTML = allPhotos.length
    ? `<img src="${allPhotos[0]}" style="width:100%;height:100%;object-fit:cover">`
    : `<span style="font-size:80px">${EMOJIS[item.categoria]||'🎴'}</span>`;
  // Gallery thumbnails
  const gallery = document.getElementById('d-gallery');
  if (allPhotos.length > 1) {
    gallery.style.display = 'flex';
    gallery.innerHTML = allPhotos.map((url,i) => 
      `<img class="photo-thumb${i===0?' active':''}" src="${url}" onclick="switchPhoto(${i})" alt="foto ${i+1}">`
    ).join('');
  } else { gallery.style.display = 'none'; }
  // Show edit/msg buttons
  const isOwner = currentUser && item.autorId === currentUser.uid;
  document.getElementById('btn-edit-aporte').style.display = isOwner ? '' : 'none';
  document.getElementById('btn-msg').style.display = (!isOwner && currentUser) ? '' : 'none';
  document.getElementById('d-name').textContent = item.nombre;
  if (item.marca) {
    document.getElementById('d-marca').textContent = '🏷️ ' + item.marca;
    document.getElementById('d-marca-wrap').style.display = '';
  } else {
    document.getElementById('d-marca-wrap').style.display = 'none';
  }
  document.getElementById('d-sub').textContent = `${item.categoria||'—'} · ${item.año||'—'}`;
  document.getElementById('d-views').textContent = (item.vistas||0)+1;
  document.getElementById('d-likes').textContent = (item.likes||0);
  document.getElementById('d-year').textContent = item.año||'—';
  // Show location if available
  const locWrap = document.getElementById('d-location-wrap');
  if (locWrap) {
    if (item.ubicacion) { locWrap.style.display=''; locWrap.querySelector('span').textContent = '📍 '+item.ubicacion; }
    else locWrap.style.display='none';
  }
  document.getElementById('d-desc').textContent = item.descripcion||'Sin descripción.';
  document.getElementById('d-owner').textContent = item.autorNombre||'Anónimo';
  document.getElementById('d-date').textContent = item.createdAt?.toDate ? timeAgo(item.createdAt.toDate()) : 'Recientemente';
  // Load owner avatar
  document.getElementById('d-owner-avatar').innerHTML = (item.autorNombre||'?')[0]?.toUpperCase() || '😊';
  if (item.autorId) {
    getDoc(doc(db, 'usuarios', item.autorId)).then(uDoc => {
      if (uDoc.exists() && uDoc.data().avatarUrl) {
        document.getElementById('d-owner-avatar').innerHTML = `<img src="${uDoc.data().avatarUrl}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
      }
    }).catch(()=>{});
  }
  document.getElementById('d-tags').innerHTML = `
    <span class="tag" style="background:#1e1e2e;color:${COLORS[item.categoria]||'#4d96ff'}">${item.categoria||'otro'}</span>
    <span class="tag" style="background:#1e1e2e;color:var(--accent2)">${item.rareza||'—'}</span>`;
  // Check if liked
  const liked = currentUser && (item.likedBy||[]).includes(currentUser.uid);
  document.getElementById('btn-like').className = `like-btn${liked?' liked':''}`;
  document.getElementById('like-label').textContent = liked ? 'Te gustó' : 'Me gusta';
  // Load comments
  loadComments(id);
  showScreen('screen-detail');
};

async function loadComments(itemId) {
  const list = document.getElementById('comments-list');
  try {
    const snap = await getDocs(query(collection(db, 'piezas', itemId, 'comentarios'), orderBy('createdAt')));
    if (snap.empty) { list.innerHTML = '<div style="color:var(--muted);font-size:12px;font-weight:600;margin-bottom:8px">Sin comentarios aún. ¡Sé el primero!</div>'; return; }
    list.innerHTML = snap.docs.map(d => `
      <div class="comment-item">
        <div class="comment-author">${d.data().autorNombre||'Anónimo'}</div>
        <div class="comment-text">${d.data().texto}</div>
      </div>`).join('');
  } catch(e) { list.innerHTML = ''; }
}

window.addComment = async () => {
  if (!currentUser) { showToast('Inicia sesión para comentar'); return; }
  const texto = document.getElementById('comment-input').value.trim();
  if (!texto) return;
  const btn = document.querySelector('#comments-list + div button');
  try {
    document.getElementById('comment-input').value = '';
    await addDoc(collection(db, 'piezas', currentDetailId, 'comentarios'), {
      texto, autorNombre: currentUser.displayName||currentUser.email.split('@')[0],
      autorId: currentUser.uid, createdAt: serverTimestamp()
    });
    await loadComments(currentDetailId);
    showToast('Comentario publicado ✅');
    // Scroll to comments
    document.querySelector('.comments-wrap').scrollIntoView({behavior:'smooth',block:'end'});
  } catch(e) { showToast('Error al comentar'); }
};

window.toggleLike = async () => {
  if (!currentUser) { showToast('Inicia sesión para dar like'); return; }
  const item = allItems.find(i => i.id === currentDetailId);
  if (!item) return;
  const liked = (item.likedBy||[]).includes(currentUser.uid);
  try {
    await updateDoc(doc(db, 'piezas', currentDetailId), {
      likes: increment(liked ? -1 : 1),
      likedBy: liked ? arrayRemove(currentUser.uid) : arrayUnion(currentUser.uid)
    });
    item.likes = (item.likes||0) + (liked ? -1 : 1);
    item.likedBy = liked ? (item.likedBy||[]).filter(x=>x!==currentUser.uid) : [...(item.likedBy||[]), currentUser.uid];
    document.getElementById('d-likes').textContent = item.likes;
    document.getElementById('btn-like').className = `like-btn${!liked?' liked':''}`;
    document.getElementById('like-label').textContent = !liked ? 'Te gustó' : 'Me gusta';
    // 1000 likes bonus
    if (!liked && item.likes === 1000) {
      showToast('🎉 ¡1,000 likes! El autor gana un aporte extra');
      try {
        const uRef = doc(db, 'usuarios', item.autorId);
        const uDoc = await getDoc(uRef);
        const bonus = (uDoc.exists() ? uDoc.data().bonusAportes||0 : 0) + 1;
        await updateDoc(uRef, { bonusAportes: bonus });
      } catch(e) {}
    }
  } catch(e) { showToast('Error'); }
};

// ── UPLOAD ──
let selectedFiles = [null, null, null];
let aiSuggestion = null;
window.previewImgMulti = (e, idx) => {
  const file = e.target.files[0];
  if (!file) return;
  selectedFiles[idx] = file;
  const preview = document.getElementById('img-preview-' + idx);
  preview.src = URL.createObjectURL(file);
  preview.style.display = 'block';

};

window.submitPieza = async () => {
  if (!currentUser) { showToast('Inicia sesión primero 👆'); showScreen('screen-auth'); return; }
  const nombre = document.getElementById('f-nombre').value.trim();
  if (!nombre) { showToast('Escribe el nombre de la pieza'); return; }
  // Check upload limit for free plan
  if (userPlan === 'free') {
    const myItems = allItems.filter(i => i.autorId === currentUser.uid);
    const thisMonth = myItems.filter(i => { if (!i.createdAt?.toDate) return false; const d = i.createdAt.toDate(); const now = new Date(); return d.getMonth()===now.getMonth() && d.getFullYear()===now.getFullYear(); });
    if (thisMonth.length >= 10) { showToast('Plan Gratis: máx 10 aportes/mes. ¡Mejora tu plan!'); showScreen('screen-planes'); return; }
  }
  const btn = document.getElementById('btn-submit');
  btn.disabled = true; btn.textContent = 'Publicando…';
  try {
    const imageUrls = [];
    for (let i = 0; i < 3; i++) {
      if (selectedFiles[i]) {
        const url = await fileToBase64Small(selectedFiles[i]);
        imageUrls.push(url);
      }
    }
    const imageUrl = imageUrls[0] || '';
    await addDoc(collection(db, 'piezas'), {
      nombre, categoria: document.getElementById('f-categoria').value,
      marca: (document.getElementById('f-marca').value === 'Otra marca' || document.getElementById('f-marca').value === 'Otro') 
        ? (document.getElementById('f-marca-custom').value.trim() || 'Otra') 
        : document.getElementById('f-marca').value,
      imageUrls,
      ubicacion: document.getElementById('f-ubicacion').value.trim(),
      rareza: document.getElementById('f-rareza').value,
      año: document.getElementById('f-año').value.trim()||'Desconocido',
      descripcion: document.getElementById('f-desc').value.trim(),
      imageUrl, autorId: currentUser.uid,
      autorNombre: currentUser.displayName||currentUser.email.split('@')[0],
      vistas: 0, likes: 0, likedBy: [], createdAt: serverTimestamp()
    });
    showToast('¡Pieza publicada! 🎉');
    document.getElementById('f-nombre').value = '';
    document.getElementById('f-desc').value = '';
    document.getElementById('f-año').value = '';
    for(let i=0;i<3;i++){
      document.getElementById('img-preview-'+i).style.display='none';
      document.getElementById('file-input-'+i).value='';
    }
    selectedFiles = [null,null,null];
    document.getElementById('f-ubicacion').value='';
    await loadItems();
    showScreen('screen-home');
  } catch(e) { showToast('Error al publicar.'); }
  btn.disabled = false; btn.textContent = 'Publicar aporte 🚀';
};

async function fileToBase64Small(file) {
  return new Promise(res => {
    const canvas = document.createElement('canvas');
    const img = new Image();
    img.onload = () => {
      const size = 400;
      const ratio = Math.min(size/img.width, size/img.height);
      canvas.width = img.width*ratio; canvas.height = img.height*ratio;
      canvas.getContext('2d').drawImage(img,0,0,canvas.width,canvas.height);
      res(canvas.toDataURL('image/jpeg',0.7));
    };
    img.src = URL.createObjectURL(file);
  });
}

// ── PLANES ──
window.activarPlan = async (plan) => {
  if (!currentUser) { showToast('Inicia sesión primero'); showScreen('screen-auth'); return; }
  try {
    await setDoc(doc(db, 'usuarios', currentUser.uid), { plan, email: currentUser.email, nombre: currentUser.displayName }, { merge: true });
    userPlan = plan;
    updatePlanChip();
    buildPills();
    buildUploadSelect();
    showToast(plan==='pro' ? '👑 ¡Plan Pro activado!' : '⭐ ¡Plan Premium activado!');
    showScreen('screen-home');
  } catch(e) { showToast('Error al activar plan'); }
};

// ── AUTH ──
window.loginGoogle = async () => {
  try { await signInWithPopup(auth, provider); showToast('¡Bienvenido! 🎉'); showScreen('screen-home'); }
  catch(e) { showToast('Error al iniciar con Google'); }
};
window.authAction = async () => {
  const email = document.getElementById('auth-email').value.trim();
  const pass = document.getElementById('auth-pass').value;
  if (!email||!pass) { showToast('Llena todos los campos'); return; }
  try {
    if (isRegister) {
      const name = document.getElementById('auth-name').value.trim()||'Coleccionista';
      const cred = await createUserWithEmailAndPassword(auth, email, pass);
      await updateProfile(cred.user, { displayName: name });
      showToast('¡Cuenta creada! 🎉');
    } else { await signInWithEmailAndPassword(auth, email, pass); showToast('¡Bienvenido de vuelta!'); }
    showScreen('screen-home');
  } catch(e) {
    const msgs = {'auth/email-already-in-use':'Correo ya registrado','auth/wrong-password':'Contraseña incorrecta','auth/user-not-found':'Correo no encontrado','auth/weak-password':'Contraseña muy débil'};
    showToast(msgs[e.code]||'Error de autenticación');
  }
};
window.toggleAuthMode = () => {
  isRegister = !isRegister;
  document.getElementById('auth-name').style.display = isRegister?'':'none';
  document.getElementById('btn-auth-action').textContent = isRegister?'Crear cuenta':'Iniciar sesión';
  document.getElementById('auth-toggle').textContent = isRegister?'¿Ya tienes cuenta? Inicia sesión':'¿No tienes cuenta? Regístrate';
};
window.logout = async () => { await signOut(auth); currentUser=null; userPlan='free'; showToast('Sesión cerrada 👋'); showScreen('screen-home'); };

// ── PROFILE ──
window.goProfile = () => {
  if (!currentUser) { showScreen('screen-auth'); return; }
  const myItems = allItems.filter(i => i.autorId===currentUser.uid);
  document.getElementById('p-aportes').textContent = myItems.length;
  document.getElementById('p-total').textContent = allItems.length;
  const list = document.getElementById('my-items-list');
  list.innerHTML = myItems.slice(0,5).map(item => `
    <div style="background:var(--card);border-radius:14px;padding:11px 13px;display:flex;align-items:center;gap:10px;border:1.5px solid #2e2b45;cursor:pointer" onclick="openDetail('${item.id}')">
      <div style="font-size:26px">${EMOJIS[item.categoria]||'🎴'}</div>
      <div style="flex:1"><div style="font-size:13px;font-weight:800">${item.nombre}</div><div style="font-size:11px;color:var(--muted);font-weight:600">${item.categoria} · ${item.rareza}</div></div>
      <span style="color:var(--muted)">›</span>
    </div>`).join('')||'<div style="color:var(--muted);font-size:13px;font-weight:600;text-align:center;padding:20px">Aún no has aportado piezas</div>';
  updatePlanChip();
  showScreen('screen-profile');
};

// ── HELPERS ──
// ── AI IDENTIFY ──
window.identificarConIA = async () => {
  const file = selectedFiles[0];
  if (!file) return;
  const btn = document.getElementById('btn-ai');
  const btnText = document.getElementById('btn-ai-text');
  btnText.textContent = 'Analizando…';
  btn.disabled = true;
  try {
    // Convert image to base64 for vision API
    const base64full = await new Promise(res => {
      const r = new FileReader();
      r.onload = () => res(r.result.split(',')[1]);
      r.readAsDataURL(file);
    });
    const mediaType = file.type || 'image/jpeg';
    
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'anthropic-dangerous-direct-browser-access': 'true'
      },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 600,
        messages: [{
          role: 'user',
          content: [
            { 
              type: 'image', 
              source: { type: 'base64', media_type: mediaType, data: base64full }
            },
            { 
              type: 'text', 
              text: 'Analiza esta imagen de un objeto coleccionable. Responde SOLO con un objeto JSON válido, sin texto adicional, sin markdown, sin explicaciones. Usa exactamente este formato: {"nombre":"nombre descriptivo corto","categoria":"una de estas exactas: canica|carta|auto_escala|tazo|figura|muneca|peluche|dinosaurio|planta|funko|lego|moneda|otro","marca":"marca o fabricante","año":"año o década aproximada","rareza":"una de: Común|Poco común|Rara|Legendaria","descripcion":"descripción de 1 oración"}' 
            }
          ]
        }]
      })
    });
    
    if (!response.ok) {
      throw new Error('API error: ' + response.status);
    }
    
    const data = await response.json();
    const text = (data.content||[]).map(c => c.text||'').join('').trim();
    // Clean any potential markdown
    const clean = text.replace(/^```json?\s*/,'').replace(/\s*```$/,'').trim();
    aiSuggestion = JSON.parse(clean);
    
    document.getElementById('ai-result-text').innerHTML = 
      `<b>Nombre:</b> ${aiSuggestion.nombre}<br>
       <b>Categoría:</b> ${aiSuggestion.categoria}<br>
       <b>Marca:</b> ${aiSuggestion.marca||'No identificada'}<br>
       <b>Año:</b> ${aiSuggestion.año||'Desconocido'}<br>
       <b>Rareza:</b> ${aiSuggestion.rareza}<br>
       <b>Descripción:</b> ${aiSuggestion.descripcion}`;
    document.getElementById('ai-result').style.display = '';
    showToast('🤖 ¡IA identificó tu pieza!');
  } catch(e) {
    console.error('AI Error:', e);
    // Fallback: smart suggestions based on filename/type
    showToast('⚠️ IA no disponible — llena los datos o intenta de nuevo');
  }
  btnText.textContent = 'Identificar con IA 🤖';
  btn.disabled = false;
};

window.aplicarSugerenciaIA = () => {
  if (!aiSuggestion) return;
  if (aiSuggestion.nombre) document.getElementById('f-nombre').value = aiSuggestion.nombre;
  if (aiSuggestion.descripcion) document.getElementById('f-desc').value = aiSuggestion.descripcion;
  if (aiSuggestion.año) document.getElementById('f-año').value = aiSuggestion.año;
  if (aiSuggestion.rareza) document.getElementById('f-rareza').value = aiSuggestion.rareza;
  if (aiSuggestion.categoria) {
    const sel = document.getElementById('f-categoria');
    for (let opt of sel.options) { if (opt.value === aiSuggestion.categoria) { sel.value = aiSuggestion.categoria; break; } }
    updateMarcas();
    if (aiSuggestion.marca) {
      setTimeout(() => {
        const msel = document.getElementById('f-marca');
        let found = false;
        for (let opt of msel.options) { if (opt.value.toLowerCase().includes(aiSuggestion.marca.toLowerCase()) || aiSuggestion.marca.toLowerCase().includes(opt.value.toLowerCase())) { msel.value = opt.value; found = true; break; } }
        if (!found) { msel.value = msel.options[msel.options.length-1].value; document.getElementById('f-marca-custom').style.display=''; document.getElementById('f-marca-custom').value = aiSuggestion.marca; }
      }, 100);
    }
  }
  showToast('✅ Sugerencias aplicadas');
  document.getElementById('ai-result').style.display = 'none';
};

// ── PHOTO VIEWER ──
window.openPhotoViewer = (idx) => {
  const photos = window._currentPhotos || [];
  if (!photos.length) return;
  document.getElementById('photo-viewer-img').src = photos[idx] || photos[0];
  document.getElementById('photo-viewer').classList.add('open');
};
window.closePhotoViewer = () => {
  document.getElementById('photo-viewer').classList.remove('open');
};
window.switchPhoto = (idx) => {
  const photos = window._currentPhotos || [];
  document.getElementById('d-hero').innerHTML = `<img src="${photos[idx]}" style="width:100%;height:100%;object-fit:cover">`;
  document.querySelectorAll('.photo-thumb').forEach((t,i) => t.className = 'photo-thumb' + (i===idx?' active':''));
};

// ── EDIT ──
window.openEdit = () => {
  const item = allItems.find(i => i.id === currentDetailId);
  if (!item) return;
  document.getElementById('edit-nombre').value = item.nombre || '';
  document.getElementById('edit-rareza').value = item.rareza || 'Común';
  document.getElementById('edit-año').value = item.año || '';
  document.getElementById('edit-desc').value = item.descripcion || '';
  document.getElementById('edit-ubicacion').value = item.ubicacion || '';
  showScreen('screen-edit');
};
window.saveEdit = async () => {
  const btn = document.getElementById('btn-edit-submit');
  btn.disabled = true; btn.textContent = 'Guardando…';
  try {
    const updates = {
      nombre: document.getElementById('edit-nombre').value.trim(),
      rareza: document.getElementById('edit-rareza').value,
      año: document.getElementById('edit-año').value.trim(),
      descripcion: document.getElementById('edit-desc').value.trim(),
      ubicacion: document.getElementById('edit-ubicacion').value.trim(),
    };
    await updateDoc(doc(db, 'piezas', currentDetailId), updates);
    const item = allItems.find(i => i.id === currentDetailId);
    if (item) Object.assign(item, updates);
    showToast('¡Aporte actualizado! ✅');
    showScreen('screen-detail');
    openDetail(currentDetailId);
  } catch(e) { showToast('Error al guardar'); }
  btn.disabled = false; btn.textContent = 'Guardar cambios ✅';
};

// ── AVATAR UPLOAD ──
window.uploadAvatar = async (e) => {
  const file = e.target.files[0];
  if (!file || !currentUser) return;
  showToast('Subiendo foto de perfil…');
  try {
    const base64 = await fileToBase64Small(file);
    // Save to Firestore
    await setDoc(doc(db, 'usuarios', currentUser.uid), { 
      avatarUrl: base64,
      nombre: currentUser.displayName || currentUser.email.split('@')[0],
      email: currentUser.email
    }, { merge: true });
    // Update avatar display
    const avatar = document.getElementById('p-avatar');
    avatar.innerHTML = `<img src="${base64}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
    // Update topbar button
    document.querySelector('.user-btn').innerHTML = `<img src="${base64}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
    showToast('¡Foto de perfil actualizada! 📸');
  } catch(e) { showToast('Error al subir foto'); }
};

// ── MESSAGE OWNER ──
window.msgOwner = () => {
  if (!currentUser) { showToast('Inicia sesión para enviar mensajes'); showScreen('screen-auth'); return; }
  const item = allItems.find(i => i.id === currentDetailId);
  if (!item) return;
  openChat(item.autorId, item.autorNombre, null);
};

// ── PUBLIC PROFILE ──
let publicProfileUid = null;
let publicProfileName = null;

window.openPublicProfile = async () => {
  const item = allItems.find(i => i.id === currentDetailId);
  if (!item) return;
  publicProfileUid = item.autorId;
  publicProfileName = item.autorNombre || 'Anónimo';

  document.getElementById('pp-name').textContent = publicProfileName;
  document.getElementById('pp-avatar').innerHTML = publicProfileName[0]?.toUpperCase() || '😎';

  // Hide message button if it's your own profile
  document.getElementById('pp-action-btns').style.display = (currentUser && currentUser.uid === publicProfileUid) ? 'none' : '';

  // Load user data (plan + avatar)
  try {
    const uDoc = await getDoc(doc(db, 'usuarios', publicProfileUid));
    if (uDoc.exists()) {
      const udata = uDoc.data();
      const plan = udata.plan || 'free';
      const chip = document.getElementById('pp-plan-chip');
      if (plan === 'pro') { chip.style.background='#2d1b69'; chip.style.color='#c77dff'; chip.textContent='👑 Plan Pro'; }
      else if (plan === 'premium') { chip.style.background='#1a2a1a'; chip.style.color='#6bcb77'; chip.textContent='⭐ Plan Premium'; }
      else { chip.style.background='#2e2b45'; chip.style.color='var(--muted)'; chip.textContent='🆓 Plan Gratis'; }
      if (udata.avatarUrl) {
        document.getElementById('pp-avatar').innerHTML = `<img src="${udata.avatarUrl}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
      }
    }
  } catch(e) {}

  // Load this user's items
  const userItems = allItems.filter(i => i.autorId === publicProfileUid);
  document.getElementById('pp-aportes').textContent = userItems.length;
  const totalLikes = userItems.reduce((sum, i) => sum + (i.likes || 0), 0);
  document.getElementById('pp-likes').textContent = totalLikes;

  const grid = document.getElementById('pp-items-grid');
  if (!userItems.length) {
    grid.innerHTML = '<div class="empty"><div class="big">📦</div><p>Sin aportes públicos aún</p></div>';
  } else {
    grid.innerHTML = userItems.map(it => `
      <div class="col-card" onclick="openDetail('${it.id}')">
        <div class="col-card-img" style="background:linear-gradient(135deg,#1a1828,#221f35)">
          ${it.imageUrl ? `<img src="${it.imageUrl}" style="width:100%;height:100%;object-fit:cover;position:absolute;inset:0">` : `<span style="font-size:48px">${EMOJIS[it.categoria]||'🎴'}</span>`}
          <div class="col-badge" style="background:${COLORS[it.categoria]||'#4d96ff'}">${it.categoria||'otro'}</div>
        </div>
        <div class="col-card-info">
          <div class="col-card-name">${it.nombre}</div>
          <div class="col-card-meta"><span class="rdot" style="background:${COLORS[it.categoria]||'#4d96ff'}"></span>${it.rareza||'—'}</div>
        </div>
      </div>`).join('');
  }

  showScreen('screen-public-profile');
};

window.msgFromProfile = () => {
  if (!currentUser) { showToast('Inicia sesión para enviar mensajes'); showScreen('screen-auth'); return; }
  if (currentUser.uid === publicProfileUid) { showToast('No puedes enviarte mensajes a ti mismo'); return; }
  openChat(publicProfileUid, publicProfileName, null);
};

// ── CHAT FUNCTIONS ──
let currentChatId = null;
let currentChatUserId = null;
let chatUnsubscribe = null;

function getChatId(uid1, uid2) {
  return [uid1, uid2].sort().join('_');
}

window.goChats = async () => {
  if (!currentUser) { showScreen('screen-auth'); return; }
  showScreen('screen-chats');
  loadChatList();
};

async function loadChatList() {
  const list = document.getElementById('chats-list');
  list.innerHTML = '<div style="display:flex;align-items:center;justify-content:center;padding:40px"><div class="spinner"></div></div>';
  try {
    const snap = await getDocs(query(collection(db, 'chats'), where('participantes', 'array-contains', currentUser.uid), orderBy('ultimoMensaje', 'desc')));
    if (snap.empty) {
      list.innerHTML = '<div class="empty-chat"><div style="font-size:56px">💬</div><p style="font-weight:700;font-size:15px">Sin mensajes aún</p><p style="font-size:13px">Toca el botón 💬 en cualquier pieza para iniciar una conversación</p></div>';
      return;
    }
    list.innerHTML = snap.docs.map(d => {
      const data = d.data();
      const otherId = data.participantes.find(p => p !== currentUser.uid);
      const otherName = data.nombres?.[otherId] || 'Coleccionista';
      const preview = data.ultimoTexto || '...';
      const time = data.ultimoMensaje?.toDate ? timeAgo(data.ultimoMensaje.toDate()) : '';
      const unread = data.noLeidos?.[currentUser.uid] || 0;
      return `<div class="chat-item" onclick="openChat('${otherId}','${otherName}','${d.id}')">
        <div class="chat-avatar">😊</div>
        <div class="chat-info">
          <div class="chat-name">${otherName}</div>
          <div class="chat-preview">${preview}</div>
        </div>
        <div style="display:flex;flex-direction:column;align-items:flex-end;gap:4px">
          <div class="chat-time">${time}</div>
          ${unread > 0 ? `<div class="chat-unread">${unread}</div>` : ''}
        </div>
      </div>`;
    }).join('');
  } catch(e) { list.innerHTML = '<div style="text-align:center;padding:40px;color:var(--muted)">Error cargando chats</div>'; }
}

window.openChat = async (otherUserId, otherName, existingChatId) => {
  if (!currentUser) { showScreen('screen-auth'); return; }
  currentChatUserId = otherUserId;
  currentChatId = existingChatId || getChatId(currentUser.uid, otherUserId);
  document.getElementById('chat-header-name').textContent = otherName;
  document.getElementById('messages-wrap').innerHTML = '<div style="display:flex;align-items:center;justify-content:center;padding:40px"><div class="spinner"></div></div>';
  showScreen('screen-chat-messages');
  // Load avatar
  try {
    const uDoc = await getDoc(doc(db, 'usuarios', otherUserId));
    if (uDoc.exists() && uDoc.data().avatarUrl) {
      document.getElementById('chat-header-avatar').innerHTML = `<img src="${uDoc.data().avatarUrl}" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
    }
  } catch(e) {}
  // Subscribe to messages
  if (chatUnsubscribe) chatUnsubscribe();
  const msgsRef = collection(db, 'chats', currentChatId, 'mensajes');
  chatUnsubscribe = onSnapshot(query(msgsRef, orderBy('createdAt')), (snap) => {
    const wrap = document.getElementById('messages-wrap');
    if (snap.empty) {
      wrap.innerHTML = `<div class="empty-chat"><div style="font-size:44px">👋</div><p style="font-weight:700">¡Di hola a ${otherName}!</p><p style="font-size:12px">Inicia la conversación</p></div>`;
      return;
    }
    wrap.innerHTML = snap.docs.map(d => {
      const m = d.data();
      const isSent = m.autorId === currentUser.uid;
      const time = m.createdAt?.toDate ? m.createdAt.toDate().toLocaleTimeString('es', {hour:'2-digit',minute:'2-digit'}) : '';
      return `<div style="display:flex;flex-direction:column;align-items:${isSent?'flex-end':'flex-start'}">
        <div class="msg-bubble ${isSent?'sent':'recv'}">${m.texto}</div>
        <div class="msg-time ${isSent?'sent':''}">${time}</div>
      </div>`;
    }).join('');
    wrap.scrollTop = wrap.scrollHeight;
  });
  // Mark as read
  try {
    await setDoc(doc(db, 'chats', currentChatId), {
      participantes: [currentUser.uid, otherUserId],
      nombres: { [currentUser.uid]: currentUser.displayName||currentUser.email.split('@')[0], [otherUserId]: otherName },
      [`noLeidos.${currentUser.uid}`]: 0
    }, { merge: true });
  } catch(e) {}
};

window.sendMessage = async () => {
  const input = document.getElementById('chat-msg-input');
  const texto = input.value.trim();
  if (!texto || !currentChatId || !currentUser) return;
  input.value = '';
  try {
    await addDoc(collection(db, 'chats', currentChatId, 'mensajes'), {
      texto, autorId: currentUser.uid,
      autorNombre: currentUser.displayName||currentUser.email.split('@')[0],
      createdAt: serverTimestamp()
    });
    await setDoc(doc(db, 'chats', currentChatId), {
      ultimoTexto: texto,
      ultimoMensaje: serverTimestamp(),
      participantes: [currentUser.uid, currentChatUserId],
      [`noLeidos.${currentChatUserId}`]: 999
    }, { merge: true });
  } catch(e) { showToast('Error al enviar'); }
};

window.showScreen = (id) => {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0,0);
  if (screenHistory[screenHistory.length-1] !== id) {
    screenHistory.push(id);
    history.pushState({screen: id}, '', window.location.href);
  }
};
window.showToast = (msg) => {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2500);
};
function timeAgo(date) {
  const diff = Date.now()-date.getTime(), mins = Math.floor(diff/60000);
  if (mins<1) return 'Ahora mismo';
  if (mins<60) return `Hace ${mins} min`;
  const hrs = Math.floor(mins/60);
  if (hrs<24) return `Hace ${hrs}h`;
  return `Hace ${Math.floor(hrs/24)} día${Math.floor(hrs/24)>1?'s':''}`;
}


// ── HARDWARE BACK BUTTON ──
let screenHistory = ['screen-home'];
window.addEventListener('popstate', (e) => {
  if (screenHistory.length > 1) {
    screenHistory.pop();
    const prev = screenHistory[screenHistory.length - 1];
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.getElementById(prev).classList.add('active');
    window.scrollTo(0,0);
  } else {
    // Let the app minimize instead of closing
    history.pushState(null, '', window.location.href);
  }
});

// ── SPLASH & ONBOARDING ──
let obSlide = 0;
const TOTAL_SLIDES = 4;

function initApp() {
  // Show splash
  const bar = document.getElementById('splash-bar');
  setTimeout(() => { if(bar) bar.style.width = '100%'; }, 100);
  setTimeout(() => {
    const seen = localStorage.getItem('mdc_onboarding_done');
    if (seen) {
      showScreen('screen-home');
    } else {
      showScreen('screen-onboarding');
    }
  }, 2000);
}

window.nextSlide = () => {
  if (obSlide >= TOTAL_SLIDES - 1) { finishOnboarding(); return; }
  const curr = document.getElementById('ob-' + obSlide);
  curr.className = 'ob-slide left';
  obSlide++;
  const next = document.getElementById('ob-' + obSlide);
  next.className = 'ob-slide show';
  // Update dots
  document.querySelectorAll('.ob-dot').forEach((d,i) => d.className = 'ob-dot' + (i===obSlide?' on':''));
  // Update button
  if (obSlide === TOTAL_SLIDES - 1) document.getElementById('ob-next-btn').textContent = '¡Comenzar! 🚀';
};

window.finishOnboarding = () => {
  localStorage.setItem('mdc_onboarding_done', '1');
  showScreen('screen-home');
};

// ── INIT ──
buildPills();
buildUploadSelect();
loadItems();
initApp();
</script>
</body>
</html>
