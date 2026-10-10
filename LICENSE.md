<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Metz Project</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Inter:wght@300;400;500;600;700;800&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: #0a0e17;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
            color: white;
        }

        .app-container {
            width: 100%;
            max-width: 480px;
            height: 100vh;
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .bg-image {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background-image: 
                linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.6)),
                url('https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=800');
            background-size: cover;
            background-position: center;
            z-index: 0;
            filter: grayscale(100%) brightness(0.5);
        }

        .bg-overlay {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: linear-gradient(180deg, 
                rgba(10, 20, 40, 0.85) 0%, 
                rgba(10, 20, 40, 0.7) 40%,
                rgba(10, 14, 23, 0.95) 100%);
            z-index: 1;
        }

        /* === HEADER === */
        .header {
            position: relative;
            z-index: 10;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            background: linear-gradient(180deg, rgba(20, 40, 80, 0.9), rgba(20, 40, 80, 0.5));
            backdrop-filter: blur(10px);
            transition: 0.3s;
        }

        .menu-icon {
            font-size: 22px;
            color: white;
            cursor: pointer;
            padding: 5px;
            transition: 0.3s;
            user-select: none;
        }

        .menu-icon:hover { color: #00c6ff; transform: scale(1.1); }

        .app-logo {
            font-family: 'Orbitron', sans-serif;
            font-size: 18px;
            font-weight: 900;
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 2px;
        }

        .header-actions { display: flex; gap: 10px; align-items: center; }

        .action-btn {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid rgba(255, 255, 255, 0.2);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 16px;
            cursor: pointer;
            transition: 0.3s;
            backdrop-filter: blur(10px);
        }

        .action-btn:hover {
            background: rgba(0, 198, 255, 0.3);
            transform: scale(1.1);
        }

        .avatar-small {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ff6b6b, #ffa500);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            cursor: pointer;
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        /* === SIDEBAR === */
        .sidebar-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(3px);
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: 0.3s;
        }

        .sidebar-overlay.active { opacity: 1; visibility: visible; }

        .sidebar {
            position: fixed;
            top: 0; left: -300px;
            width: 280px;
            height: 100%;
            background: linear-gradient(180deg, #0a1428, #060a12);
            border-right: 1px solid rgba(0, 150, 255, 0.3);
            z-index: 2001;
            transition: 0.3s;
            display: flex;
            flex-direction: column;
            box-shadow: 5px 0 30px rgba(0, 0, 0, 0.5);
        }

        .sidebar.active { left: 0; }

        .sidebar-header {
            padding: 25px 20px;
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            position: relative;
            overflow: hidden;
        }

        .sidebar-header-content {
            position: relative;
            z-index: 1;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .sidebar-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            border: 2px solid rgba(255, 255, 255, 0.5);
        }

        .sidebar-user-info .name {
            font-family: 'Orbitron', sans-serif;
            font-size: 14px;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: 1px;
        }

        .sidebar-user-info .role {
            font-size: 10px;
            color: rgba(255, 255, 255, 0.9);
            letter-spacing: 1px;
            margin-top: 2px;
        }

        .sidebar-menu {
            flex: 1;
            overflow-y: auto;
            padding: 15px 0;
            scrollbar-width: none;
        }

        .sidebar-menu::-webkit-scrollbar { display: none; }

        .sidebar-section-title {
            font-size: 9px;
            color: #6b8cae;
            text-transform: uppercase;
            letter-spacing: 2px;
            padding: 12px 20px 8px;
            font-weight: 700;
        }

        .sidebar-item {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 14px 20px;
            cursor: pointer;
            transition: 0.3s;
            border-left: 3px solid transparent;
            color: #d0e4ff;
            font-size: 13px;
            font-weight: 500;
        }

        .sidebar-item:hover {
            background: rgba(0, 198, 255, 0.1);
            border-left-color: #00c6ff;
            color: #ffffff;
        }

        .sidebar-item.active {
            background: rgba(0, 198, 255, 0.15);
            border-left-color: #00c6ff;
            color: #00c6ff;
        }

        .sidebar-item-icon { font-size: 18px; width: 24px; text-align: center; }

        .sidebar-footer {
            padding: 15px 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            text-align: center;
            font-size: 10px;
            color: #4a6a8a;
            letter-spacing: 1px;
        }

        /* === MAIN CONTENT === */
        .main-content {
            position: relative;
            z-index: 5;
            flex: 1;
            overflow-y: auto;
            padding: 15px;
            scrollbar-width: none;
            padding-bottom: 100px;
        }
        .main-content::-webkit-scrollbar { display: none; }

        .page-content { display: none; animation: fadeIn 0.3s ease; }
        .page-content.active { display: block; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* === PROFILE CARD === */
        .profile-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(20px);
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 15px;
            border: 1px solid rgba(255, 255, 255, 0.15);
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
        }

        .profile-top {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 15px;
        }

        .profile-left { display: flex; gap: 12px; align-items: center; }

        .profile-avatar {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ff6b6b, #ffa500);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 28px;
            border: 3px solid rgba(0, 255, 100, 0.6);
            position: relative;
            box-shadow: 0 0 20px rgba(0, 255, 100, 0.3);
        }

        .profile-avatar::after {
            content: '';
            position: absolute;
            bottom: 0; right: 0;
            width: 14px; height: 14px;
            background: #00ff64;
            border-radius: 50%;
            border: 2px solid #0a0e17;
        }

        .profile-info { display: flex; flex-direction: column; gap: 3px; }
        .greeting { font-size: 11px; color: #a0b8d0; font-weight: 500; }

        .profile-name {
            font-family: 'Orbitron', sans-serif;
            font-size: 20px;
            font-weight: 900;
            color: #ffffff;
            letter-spacing: 1px;
        }

        .profile-badge {
            display: inline-flex;
            align-items: center;
            gap: 5px;
            background: rgba(255, 255, 255, 0.9);
            color: #0a0e17;
            padding: 4px 12px;
            border-radius: 12px;
            font-size: 9px;
            font-weight: 800;
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 1.5px;
            margin-top: 5px;
            width: fit-content;
        }

        .weather-badge {
            background: rgba(255, 255, 255, 0.9);
            color: #0a0e17;
            padding: 6px 12px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .dots-container { display: flex; justify-content: center; gap: 5px; margin: 12px 0; }

        .dot {
            width: 20px; height: 3px;
            border-radius: 2px;
            background: rgba(255, 255, 255, 0.3);
            transition: 0.3s;
        }
        .dot.active { background: #ffffff; width: 30px; }

        .server-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 12px;
        }

        .server-card {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 14px;
            padding: 12px;
        }

        .server-header { display: flex; align-items: center; gap: 6px; margin-bottom: 6px; }
        .server-icon { font-size: 14px; }

        .server-name {
            font-size: 10px;
            font-weight: 700;
            color: #ffffff;
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 0.5px;
        }

        .server-detail { font-size: 9px; color: #a0b8d0; line-height: 1.5; }
        .server-detail span { color: #ffffff; font-weight: 600; }

        .stats-bug-card {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 14px;
            padding: 12px 15px;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 15px;
            cursor: pointer;
            transition: 0.3s;
        }

        .stats-bug-card:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateY(-2px);
        }

        .stats-bug-icon {
            width: 40px; height: 40px;
            border-radius: 12px;
            background: rgba(0, 198, 255, 0.2);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
            border: 1px solid rgba(0, 198, 255, 0.3);
        }

        .stats-bug-content { flex: 1; }

        .stats-bug-title {
            font-size: 12px;
            font-weight: 700;
            font-family: 'Orbitron', sans-serif;
            color: #ffffff;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 3px;
        }

        .live-badge {
            background: rgba(0, 255, 100, 0.2);
            color: #00ff64;
            padding: 2px 8px;
            border-radius: 8px;
            font-size: 8px;
            font-weight: 700;
            letter-spacing: 1px;
        }

        .stats-bug-desc { font-size: 9px; color: #a0b8d0; }

        .buka-btn {
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: #ffffff;
            padding: 6px 12px;
            border-radius: 10px;
            font-size: 10px;
            font-weight: 700;
            font-family: 'Orbitron', sans-serif;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .bottom-stats { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; }
        .bottom-stat { text-align: center; }

        .bottom-stat-icon {
            width: 50px; height: 50px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 22px;
            margin: 0 auto 8px;
            position: relative;
        }

        .bottom-stat-icon.online::after {
            content: '';
            position: absolute;
            top: 0; right: 0;
            width: 12px; height: 12px;
            background: #00ff64;
            border-radius: 50%;
            border: 2px solid #0a0e17;
        }

        .bottom-stat-value {
            font-family: 'Orbitron', sans-serif;
            font-size: 18px;
            font-weight: 900;
            color: #ffffff;
            margin-bottom: 2px;
        }

        .bottom-stat-label {
            font-size: 9px;
            color: #a0b8d0;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .live-tag {
            background: rgba(0, 255, 100, 0.2);
            color: #00ff64;
            padding: 2px 8px;
            border-radius: 8px;
            font-size: 8px;
            font-weight: 700;
            letter-spacing: 1px;
            margin-top: 4px;
            display: inline-block;
        }

        /* === MENU GRID === */
        .menu-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 20px;
        }

        .menu-card {
            border-radius: 20px;
            padding: 25px 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.15);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        .menu-card:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
        }

        .menu-card:active { transform: scale(0.97); }

        .menu-card.blue { background: linear-gradient(135deg, #0d47a1, #1976d2); }
        .menu-card.purple { background: linear-gradient(135deg, #6a1b9a, #9c27b0); }
        .menu-card.green { background: linear-gradient(135deg, #1b5e20, #2e7d32); }
        .menu-card.light-blue { background: linear-gradient(135deg, #0277bd, #0288d1); }
        .menu-card.red { background: linear-gradient(135deg, #b71c1c, #e53935); }
        .menu-card.orange { background: linear-gradient(135deg, #e65100, #fb8c00); }
        .menu-card.teal { background: linear-gradient(135deg, #004d40, #00897b); }

        .menu-card-icon {
            font-size: 36px;
            margin-bottom: 12px;
            position: relative;
            z-index: 1;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
        }

        .menu-card-name {
            font-family: 'Orbitron', sans-serif;
            font-size: 13px;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: 1.5px;
            position: relative;
            z-index: 1;
        }

        .menu-card-desc {
            font-size: 9px;
            color: rgba(255, 255, 255, 0.7);
            margin-top: 4px;
            position: relative;
            z-index: 1;
        }

        /* === NEWS === */
        .news-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        .news-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 14px;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: 1.5px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .news-count {
            background: rgba(255, 255, 255, 0.15);
            color: #ffffff;
            padding: 4px 12px;
            border-radius: 10px;
            font-size: 10px;
            font-weight: 600;
        }

        .news-card {
            border-radius: 16px;
            overflow: hidden;
            position: relative;
            height: 120px;
            cursor: pointer;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }

        .news-card img { width: 100%; height: 100%; object-fit: cover; filter: brightness(0.7); }

        .news-card-overlay {
            position: absolute;
            bottom: 0; left: 0; right: 0;
            padding: 12px;
            background: linear-gradient(transparent, rgba(0, 0, 0, 0.9));
            display: flex;
            justify-content: flex-end;
        }

        .news-read-btn {
            background: rgba(255, 255, 255, 0.95);
            color: #0a0e17;
            padding: 6px 14px;
            border-radius: 10px;
            font-size: 10px;
            font-weight: 800;
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        /* === BUG TOOLS === */
        .bug-header {
            background: linear-gradient(180deg, #0b1120, #060a12);
            border-radius: 20px;
            padding: 20px 15px;
            position: relative;
            overflow: hidden;
            margin-bottom: 15px;
            border: 1px solid rgba(0, 150, 255, 0.15);
            text-align: center;
        }

        .bug-header-top {
            font-family: 'Orbitron', sans-serif;
            font-size: 14px;
            font-weight: 700;
            color: #b0d4ff;
            letter-spacing: 4px;
            position: relative;
            z-index: 2;
        }

        .bug-logo-text {
            font-family: 'Orbitron', sans-serif;
            font-size: 26px;
            font-weight: 900;
            background: linear-gradient(180deg, #ffffff, #6db3f2, #1e5799);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 2px;
            position: relative;
            z-index: 2;
            margin: 10px 0;
        }

        .bug-header-info {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            position: relative;
            z-index: 2;
            font-size: 11px;
        }

        .bug-info-left, .bug-info-right { display: flex; flex-direction: column; gap: 2px; }
        .bug-info-right { align-items: flex-end; }

        .bug-info-label { color: #6b8cae; font-size: 9px; letter-spacing: 1px; text-transform: uppercase; }

        .bug-info-value {
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            font-size: 12px;
            color: #d0e4ff;
        }

        .bug-info-username {
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            font-size: 13px;
            color: #ffffff;
            text-align: center;
        }

        .bug-session-card {
            background: linear-gradient(135deg, #1a2a6c, #2a4a9c);
            border-radius: 16px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 15px;
        }

        .bug-session-icon {
            width: 40px; height: 40px;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
        }

        .bug-session-text { flex: 1; }

        .bug-session-text .title { font-size: 12px; font-weight: 600; margin-bottom: 3px; }

        .bug-session-text .status {
            font-size: 10px;
            color: #ff6b6b;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .bug-stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 10px;
            margin-bottom: 15px;
        }

        .bug-stat-card {
            background: linear-gradient(135deg, #1a2a6c, #2a4a9c);
            border-radius: 16px;
            padding: 15px 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }

        .bug-stat-icon {
            width: 36px; height: 36px;
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            margin-bottom: 8px;
            background: rgba(255, 255, 255, 0.1);
        }

        .bug-stat-icon.green { background: rgba(0, 255, 100, 0.2); }
        .bug-stat-icon.yellow { background: rgba(255, 200, 0, 0.2); }
        .bug-stat-icon.blue { background: rgba(0, 150, 255, 0.2); }

        .bug-stat-label {
            font-size: 9px;
            color: #a0b8d0;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 3px;
        }

        .bug-stat-value {
            font-family: 'Orbitron', sans-serif;
            font-size: 14px;
            font-weight: 700;
            color: #ffffff;
        }

        .bug-form-card {
            background: linear-gradient(135deg, #1a2a6c, #2a4a9c);
            border-radius: 20px;
            padding: 20px 15px;
            margin-bottom: 15px;
        }

        .bug-section-title {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 14px;
            font-weight: 700;
            margin-bottom: 15px;
            color: #ffffff;
        }

        .bug-section-title .icon-box {
            width: 30px; height: 30px;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 8px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 15px;
        }

        .bug-input-wrapper { position: relative; margin-bottom: 10px; }

        .bug-input-wrapper .input-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 16px;
            color: #6db3f2;
        }

        .bug-input-wrapper input {
            width: 100%;
            padding: 15px 15px 15px 45px;
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 12px;
            color: white;
            font-size: 14px;
            outline: none;
            transition: 0.3s;
        }

        .bug-input-wrapper input:focus {
            border-color: #00c6ff;
            box-shadow: 0 0 15px rgba(0, 198, 255, 0.2);
        }

        .bug-input-hint {
            font-size: 10px;
            color: #8aa4c0;
            margin-top: 5px;
            padding-left: 5px;
        }

        .bug-type-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .bug-badge-active {
            background: rgba(0, 150, 255, 0.2);
            border: 1px solid rgba(0, 150, 255, 0.5);
            color: #6db3f2;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 10px;
            font-weight: 600;
        }

        .bug-selector {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 16px;
            padding: 5px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .bug-arrow-btn {
            width: 35px; height: 35px;
            border-radius: 50%;
            background: rgba(0, 0, 0, 0.4);
            border: none;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            font-size: 14px;
            flex-shrink: 0;
        }

        .bug-option {
            flex: 1;
            display: flex;
            align-items: center;
            gap: 12px;
            background: rgba(255, 255, 255, 0.08);
            border-radius: 12px;
            padding: 12px;
            border: 2px solid rgba(0, 198, 255, 0.5);
        }

        .bug-option .bug-icon-wrap {
            width: 40px; height: 40px;
            background: rgba(0, 200, 100, 0.2);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
        }

        .bug-option .bug-info-wrap { flex: 1; }

        .bug-option .bug-name { font-size: 13px; font-weight: 600; color: #ffffff; margin-bottom: 2px; }
        .bug-option .bug-id { font-size: 10px; color: #8aa4c0; }

        .bug-check-icon {
            width: 22px; height: 22px;
            border-radius: 50%;
            background: #00c6ff;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #0a0e17;
            font-size: 12px;
            font-weight: 900;
            flex-shrink: 0;
        }

        .bug-dots { display: flex; justify-content: center; gap: 6px; margin-top: 12px; }

        .bug-dot {
            width: 6px; height: 6px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            transition: 0.3s;
        }

        .bug-dot.active { background: #00c6ff; width: 20px; border-radius: 4px; }

        .bug-send-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(90deg, #00d2ff, #0072ff);
            border: none;
            border-radius: 50px;
            color: white;
            font-family: 'Orbitron', sans-serif;
            font-size: 15px;
            font-weight: 700;
            letter-spacing: 2px;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            box-shadow: 0 0 20px rgba(0, 198, 255, 0.4);
            margin-bottom: 20px;
        }

        /* === TOOLS === */
        .tools-header {
            background: linear-gradient(135deg, #004d40, #00897b);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 15px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }

        .tools-header h2 {
            font-family: 'Orbitron', sans-serif;
            font-size: 20px;
            font-weight: 900;
            color: #ffffff;
            letter-spacing: 2px;
            margin-bottom: 5px;
        }

        .tools-header p { font-size: 11px; color: rgba(255, 255, 255, 0.8); }

        .tools-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 20px;
        }

        .tool-card {
            border-radius: 20px;
            padding: 20px 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            border: 1px solid rgba(255, 255, 255, 0.15);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        .tool-card:hover { transform: translateY(-5px) scale(1.02); }

        .tool-card.teal { background: linear-gradient(135deg, #004d40, #00897b); }
        .tool-card.orange { background: linear-gradient(135deg, #e65100, #fb8c00); }
        .tool-card.indigo { background: linear-gradient(135deg, #1a237e, #3f51b5); }
        .tool-card.pink { background: linear-gradient(135deg, #880e4f, #e91e63); }
        .tool-card.cyan { background: linear-gradient(135deg, #006064, #00acc1); }
        .tool-card.lime { background: linear-gradient(135deg, #33691e, #8bc34a); }
        .tool-card.deep-purple { background: linear-gradient(135deg, #4a148c, #7b1fa2); }
        .tool-card.brown { background: linear-gradient(135deg, #3e2723, #795548); }
        .tool-card.blue-grey { background: linear-gradient(135deg, #263238, #607d8b); }
        .tool-card.amber { background: linear-gradient(135deg, #ff6f00, #ffc107); }
        .tool-card.red-dark { background: linear-gradient(135deg, #b71c1c, #f44336); }
        .tool-card.green-dark { background: linear-gradient(135deg, #1b5e20, #4caf50); }

        .tool-card-icon { font-size: 40px; margin-bottom: 10px; }

        .tool-card-name {
            font-family: 'Orbitron', sans-serif;
            font-size: 12px;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: 1px;
        }

        .tool-card-desc {
            font-size: 9px;
            color: rgba(255, 255, 255, 0.7);
            margin-top: 4px;
        }

        /* === BOTTOM NAVIGATION === */
        .bottom-nav {
            position: absolute;
            bottom: 0; left: 0; right: 0;
            background: linear-gradient(180deg, rgba(20, 40, 80, 0.95), rgba(10, 20, 40, 0.98));
            backdrop-filter: blur(20px);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            justify-content: space-around;
            align-items: center;
            padding: 10px 0 15px;
            z-index: 100;
            border-radius: 30px 30px 0 0;
            box-shadow: 0 -10px 30px rgba(0, 0, 0, 0.5);
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            padding: 5px 15px;
            transition: 0.3s;
            position: relative;
        }

        .nav-item.active {
            background: linear-gradient(180deg, #00c6ff, #0072ff);
            border-radius: 50%;
            width: 55px; height: 55px;
            justify-content: center;
            margin-top: -25px;
            box-shadow: 0 5px 20px rgba(0, 198, 255, 0.5);
            border: 3px solid rgba(255, 255, 255, 0.2);
        }

        .nav-icon { font-size: 18px; color: #a0b8d0; transition: 0.3s; }
        .nav-item.active .nav-icon { font-size: 24px; color: #ffffff; }

        .nav-label {
            font-size: 9px;
            color: #a0b8d0;
            font-weight: 600;
        }

        .nav-item.active .nav-label { display: none; }

        /* === MODAL === */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 2500;
            padding: 20px;
        }

        .modal-overlay.active { display: flex; }

        .modal-content {
            background: linear-gradient(135deg, #1a2a6c, #0a0e17);
            border-radius: 24px;
            padding: 25px 20px;
            width: 100%;
            max-width: 400px;
            max-height: 85vh;
            overflow-y: auto;
            border: 1px solid rgba(0, 198, 255, 0.3);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.6);
            scrollbar-width: none;
            animation: modalIn 0.3s ease;
        }

        .modal-content::-webkit-scrollbar { display: none; }

        @keyframes modalIn {
            from { opacity: 0; transform: scale(0.9) translateY(20px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 16px;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .modal-close {
            width: 32px; height: 32px;
            border-radius: 50%;
            background: rgba(255, 50, 50, 0.2);
            border: 1px solid rgba(255, 50, 50, 0.4);
            color: #ff6b6b;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            font-size: 14px;
        }

        /* === TOOL MODAL CONTENT === */
        .tool-input-group { margin-bottom: 12px; }

        .tool-input-group label {
            display: block;
            font-size: 10px;
            color: #8aa4c0;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 6px;
            font-weight: 600;
        }

        .tool-input-group input,
        .tool-input-group textarea,
        .tool-input-group select {
            width: 100%;
            padding: 12px 15px;
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 12px;
            color: white;
            font-size: 13px;
            outline: none;
            transition: 0.3s;
            font-family: 'Inter', sans-serif;
        }

        .tool-input-group input:focus,
        .tool-input-group textarea:focus,
        .tool-input-group select:focus {
            border-color: #00c6ff;
            box-shadow: 0 0 15px rgba(0, 198, 255, 0.2);
        }

        .tool-input-group textarea {
            resize: vertical;
            min-height: 80px;
        }

        .tool-result {
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid rgba(0, 198, 255, 0.3);
            border-radius: 12px;
            padding: 15px;
            margin-top: 12px;
            font-size: 12px;
            color: #d0e4ff;
            word-break: break-all;
            max-height: 200px;
            overflow-y: auto;
            scrollbar-width: none;
            line-height: 1.6;
            white-space: pre-wrap;
        }

        .tool-result::-webkit-scrollbar { display: none; }

        .tool-result.success {
            border-color: rgba(0, 255, 100, 0.5);
            background: rgba(0, 255, 100, 0.1);
        }

        .tool-result.error {
            border-color: rgba(255, 50, 50, 0.5);
            background: rgba(255, 50, 50, 0.1);
            color: #ff6b6b;
        }

        .tool-action-btn {
            width: 100%;
            padding: 13px;
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            border: none;
            border-radius: 12px;
            color: white;
            font-family: 'Orbitron', sans-serif;
            font-size: 12px;
            font-weight: 700;
            letter-spacing: 1px;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
            transition: 0.3s;
            margin-top: 12px;
        }

        .tool-action-btn:hover {
            transform: scale(1.02);
            box-shadow: 0 0 20px rgba(0, 198, 255, 0.5);
        }

        .tool-action-btn:active { transform: scale(0.98); }

        .tool-action-btn.secondary {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .tool-badge {
            display: inline-block;
            background: rgba(0, 198, 255, 0.2);
            color: #00c6ff;
            padding: 3px 10px;
            border-radius: 8px;
            font-size: 10px;
            font-weight: 600;
            margin-bottom: 10px;
        }

        /* QR Code display */
        .qr-display {
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            background: white;
            border-radius: 12px;
            margin-top: 12px;
        }

        .qr-display img {
            width: 200px;
            height: 200px;
        }

        /* Prayer */
        .prayer-location {
            background: rgba(0, 198, 255, 0.1);
            border: 1px solid rgba(0, 198, 255, 0.3);
            border-radius: 12px;
            padding: 12px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .prayer-location-icon { font-size: 20px; }

        .prayer-location-text .label {
            font-size: 9px;
            color: #6b8cae;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 2px;
        }

        .prayer-location-text .value {
            font-size: 13px;
            font-weight: 600;
            color: #ffffff;
        }

        .prayer-date {
            text-align: center;
            font-size: 11px;
            color: #a0b8d0;
            margin-bottom: 15px;
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 1px;
        }

        .prayer-list {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-bottom: 15px;
        }

        .prayer-item {
            background: rgba(255, 255, 255, 0.08);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 12px 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .prayer-item.next {
            background: linear-gradient(135deg, rgba(0, 198, 255, 0.3), rgba(0, 114, 255, 0.3));
            border-color: rgba(0, 198, 255, 0.6);
        }

        .prayer-name {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 13px;
            font-weight: 600;
            color: #ffffff;
        }

        .prayer-name .prayer-icon {
            width: 32px; height: 32px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 16px;
        }

        .prayer-time {
            font-family: 'Orbitron', sans-serif;
            font-size: 15px;
            font-weight: 700;
            color: #00c6ff;
            letter-spacing: 1px;
        }

        .prayer-countdown {
            text-align: center;
            background: rgba(0, 198, 255, 0.1);
            border: 1px solid rgba(0, 198, 255, 0.3);
            border-radius: 12px;
            padding: 12px;
            margin-bottom: 10px;
        }

        .prayer-countdown .label {
            font-size: 9px;
            color: #6b8cae;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
        }

        .prayer-countdown .time {
            font-family: 'Orbitron', sans-serif;
            font-size: 22px;
            font-weight: 900;
            color: #00c6ff;
            letter-spacing: 2px;
        }

        /* Games */
        .games-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 15px;
        }

        .game-card {
            background: rgba(255, 255, 255, 0.08);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 16px;
            padding: 20px 10px;
            text-align: center;
            cursor: pointer;
            transition: 0.3s;
        }

        .game-card:hover {
            background: rgba(0, 198, 255, 0.15);
            transform: translateY(-3px);
            border-color: rgba(0, 198, 255, 0.5);
        }

        .game-card-icon { font-size: 32px; margin-bottom: 8px; }

        .game-card-name {
            font-family: 'Orbitron', sans-serif;
            font-size: 11px;
            font-weight: 700;
            color: #ffffff;
            letter-spacing: 1px;
        }

        .game-card-desc { font-size: 9px; color: #a0b8d0; margin-top: 3px; }

        .game-area {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 15px;
            min-height: 250px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .game-score {
            font-family: 'Orbitron', sans-serif;
            font-size: 14px;
            color: #00c6ff;
            margin-bottom: 15px;
            letter-spacing: 1px;
        }

        .game-message {
            text-align: center;
            font-size: 13px;
            color: #a0b8d0;
            margin-top: 15px;
            line-height: 1.6;
        }

        .game-btn {
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            border: none;
            border-radius: 12px;
            color: white;
            padding: 12px 24px;
            font-family: 'Orbitron', sans-serif;
            font-size: 12px;
            font-weight: 700;
            letter-spacing: 1px;
            cursor: pointer;
            margin-top: 15px;
        }

        /* Calculator */
        .calc-display {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 12px;
            padding: 20px;
            text-align: right;
            margin-bottom: 15px;
            font-family: 'Orbitron', sans-serif;
            font-size: 24px;
            font-weight: 700;
            color: #ffffff;
            min-height: 60px;
            word-break: break-all;
            border: 1px solid rgba(0, 198, 255, 0.2);
        }

        .calc-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 8px;
        }

        .calc-btn {
            padding: 18px 10px;
            border-radius: 12px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.15);
            color: #ffffff;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            font-family: 'Orbitron', sans-serif;
        }

        .calc-btn.operator { background: rgba(0, 198, 255, 0.2); color: #00c6ff; }
        .calc-btn.equal { background: linear-gradient(135deg, #00c6ff, #0072ff); }
        .calc-btn.clear { background: rgba(255, 50, 50, 0.3); color: #ff6b6b; }

        /* === RAT / TEMA === */
        .page-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 18px;
            font-weight: 800;
            color: #00c6ff;
            margin-bottom: 15px;
            letter-spacing: 1px;
        }

        /* === TOAST === */
        .toast {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: rgba(0, 0, 0, 0.9);
            border: 1px solid #00c6ff;
            color: white;
            padding: 12px 24px;
            border-radius: 12px;
            font-size: 13px;
            z-index: 5000;
            opacity: 0;
            transition: 0.3s;
            backdrop-filter: blur(10px);
            display: flex;
            align-items: center;
            gap: 8px;
            max-width: 90%;
        }

        .toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

        /* === LOADING === */
        .loading-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 4000;
            flex-direction: column;
            gap: 15px;
        }

        .loading-overlay.active { display: flex; }

        .spinner {
            width: 50px; height: 50px;
            border: 3px solid rgba(0, 198, 255, 0.2);
            border-top-color: #00c6ff;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin { to { transform: rotate(360deg); } }

        .loading-text {
            font-family: 'Orbitron', sans-serif;
            font-size: 14px;
            color: #6db3f2;
            letter-spacing: 2px;
        }

        /* === LOGIN === */
        #loginPage {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: #0a0e17;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease, visibility 0.5s;
        }

        .login-box {
            background: rgba(20, 30, 55, 0.9);
            border: 1px solid rgba(0, 150, 255, 0.3);
            border-radius: 20px;
            padding: 40px 30px;
            width: 90%;
            max-width: 400px;
            text-align: center;
            backdrop-filter: blur(10px);
            box-shadow: 0 0 30px rgba(0, 150, 255, 0.15);
        }

        .login-box h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 26px;
            font-weight: 900;
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 30px;
            letter-spacing: 2px;
        }

        .login-box input {
            width: 100%;
            padding: 14px 18px;
            margin-bottom: 15px;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid rgba(0, 150, 255, 0.3);
            border-radius: 12px;
            color: white;
            font-size: 14px;
            outline: none;
            transition: 0.3s;
        }

        .login-box input:focus {
            border-color: #00c6ff;
            box-shadow: 0 0 15px rgba(0, 198, 255, 0.3);
        }

        .login-box button {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            border: none;
            border-radius: 12px;
            color: white;
            font-weight: 700;
            font-size: 16px;
            cursor: pointer;
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 1px;
        }

        .login-error {
            color: #ff4d4d;
            font-size: 13px;
            margin-top: 10px;
            display: none;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-8px); }
            75% { transform: translateX(8px); }
        }
    </style>
</head>
<body>

    <!-- === LOGIN PAGE === -->
    <div id="loginPage">
        <div class="login-box">
            <h1>METZ PROJECT</h1>
            <input type="text" id="usernameInput" placeholder="Username" autocomplete="off">
            <input type="password" id="passwordInput" placeholder="Password" autocomplete="off">
            <button onclick="handleLogin()">MASUK</button>
            <div class="login-error" id="loginError">Username atau Password salah!</div>
        </div>
    </div>

    <!-- === SIDEBAR OVERLAY === -->
    <div class="sidebar-overlay" id="sidebarOverlay" onclick="closeSidebar()"></div>

    <!-- === SIDEBAR === -->
    <div class="sidebar" id="sidebar">
        <div class="sidebar-header">
            <div class="sidebar-header-content">
                <div class="sidebar-avatar">👨‍💻</div>
                <div class="sidebar-user-info">
                    <div class="name">METZ</div>
                    <div class="role">⭐ DEVELOPER</div>
                </div>
            </div>
        </div>
        <div class="sidebar-menu">
            <div class="sidebar-section-title">MENU UTAMA</div>
            <div class="sidebar-item active" onclick="sidebarNav('beranda', this)">
                <div class="sidebar-item-icon">🏠</div> Beranda
            </div>
            <div class="sidebar-item" onclick="sidebarNav('menu', this)">
                <div class="sidebar-item-icon">🐛</div> Bug Tools
            </div>
            <div class="sidebar-item" onclick="sidebarNav('tools', this)">
                <div class="sidebar-item-icon">🔧</div> Tools
            </div>
            <div class="sidebar-item" onclick="sidebarNav('rat', this)">
                <div class="sidebar-item-icon">📡</div> RAT Panel
            </div>
            <div class="sidebar-item" onclick="sidebarNav('tema', this)">
                <div class="sidebar-item-icon">🎨</div> Tema
            </div>
            <div class="sidebar-section-title">MANAJEMEN</div>
            <div class="sidebar-item" onclick="openAccountModal(); closeSidebar();">
                <div class="sidebar-item-icon">👥</div> Akun Pengguna
            </div>
            <div class="sidebar-item" onclick="contactWhatsApp(); closeSidebar();">
                <div class="sidebar-item-icon">💬</div> Hubungi Kami
            </div>
            <div class="sidebar-section-title">LAINNYA</div>
            <div class="sidebar-item" onclick="showToast('Tentang Metz Project v2.0', 'ℹ️'); closeSidebar();">
                <div class="sidebar-item-icon">ℹ️</div> Tentang
            </div>
            <div class="sidebar-item" onclick="handleLogout(); closeSidebar();">
                <div class="sidebar-item-icon">🚪</div> Logout
            </div>
        </div>
        <div class="sidebar-footer">© 2024 METZ PROJECT v2.0</div>
    </div>

    <!-- === APP CONTAINER === -->
    <div class="app-container" id="appContainer" style="display:none;">
        <div class="bg-image"></div>
        <div class="bg-overlay"></div>

        <!-- HEADER -->
        <div class="header" id="mainHeader">
            <div class="menu-icon" onclick="openSidebar()">☰</div>
            <div class="app-logo">METZ PROJECT</div>
            <div class="header-actions">
                <div class="action-btn" onclick="showToast('Fitur notifikasi', '🔔')">🔔</div>
                <div class="action-btn" onclick="showToast('Fitur pesan', '💬')">💬</div>
                <div class="avatar-small">👤</div>
            </div>
        </div>

        <!-- MAIN CONTENT -->
        <div class="main-content" id="mainContent">

            <!-- === PAGE: BERANDA === -->
            <div class="page-content active" id="page-beranda">
                <div class="profile-card">
                    <div class="profile-top">
                        <div class="profile-left">
                            <div class="profile-avatar">👨‍💻</div>
                            <div class="profile-info">
                                <div class="greeting">Ahlan Wa Sahlan,</div>
                                <div class="profile-name">Metz</div>
                                <div class="profile-badge">⭐ DEVELOPER</div>
                            </div>
                        </div>
                        <div class="weather-badge">🌤️ 27°C</div>
                    </div>
                    <div class="dots-container">
                        <div class="dot active"></div>
                        <div class="dot"></div>
                        <div class="dot"></div>
                    </div>
                    <div class="server-stats">
                        <div class="server-card">
                            <div class="server-header">
                                <span class="server-icon">🖥️</span>
                                <span class="server-name">VPS SYAM</span>
                            </div>
                            <div class="server-detail">
                                RAM: <span>4.8GB/17.6GB</span><br>
                                CPU: <span>8.16</span>
                            </div>
                        </div>
                        <div class="server-card">
                            <div class="server-header">
                                <span class="server-icon">🖥️</span>
                                <span class="server-name">VPS RAT</span>
                            </div>
                            <div class="server-detail">
                                Status: <span>ONLINE</span><br>
                                Uptime: <span>99.9%</span>
                            </div>
                        </div>
                    </div>
                    <div class="stats-bug-card" onclick="goToMenu()">
                        <div class="stats-bug-icon">📊</div>
                        <div class="stats-bug-content">
                            <div class="stats-bug-title">STATISTIK BUG <span class="live-badge">LIVE</span></div>
                            <div class="stats-bug-desc">Total kirim • success rate • pool server realtime</div>
                        </div>
                        <div class="buka-btn">BUKA ❯</div>
                    </div>
                    <div class="bottom-stats">
                        <div class="bottom-stat">
                            <div class="bottom-stat-icon online">👥</div>
                            <div class="bottom-stat-value">963</div>
                            <div class="bottom-stat-label">Online Users</div>
                            <div class="live-tag">LIVE</div>
                        </div>
                        <div class="bottom-stat">
                            <div class="bottom-stat-icon">🔗</div>
                            <div class="bottom-stat-value">0</div>
                            <div class="bottom-stat-label">Sender</div>
                        </div>
                        <div class="bottom-stat">
                            <div class="bottom-stat-icon">📅</div>
                            <div class="bottom-stat-value" style="font-size:11px;">11/10/2026</div>
                            <div class="bottom-stat-label">Expired</div>
                        </div>
                    </div>
                </div>

                <div class="menu-grid">
                    <div class="menu-card blue" onclick="showToast('Membuka Pusat Guide', '📖')">
                        <div class="menu-card-icon">📖</div>
                        <div class="menu-card-name">PUSAT GUIDE</div>
                    </div>
                    <div class="menu-card purple" onclick="showToast('Membuka Tutorial', '🎓')">
                        <div class="menu-card-icon">🎓</div>
                        <div class="menu-card-name">TUTORIAL</div>
                    </div>
                    <div class="menu-card green" onclick="showToast('Membuka Musik', '🎵')">
                        <div class="menu-card-icon">🎵</div>
                        <div class="menu-card-name">MUSIK</div>
                    </div>
                    <div class="menu-card light-blue" onclick="contactWhatsApp()">
                        <div class="menu-card-icon">📱</div>
                        <div class="menu-card-name">KONTAK</div>
                    </div>
                </div>

                <div class="news-header">
                    <div class="news-title">📰 BERITA TERKINI</div>
                    <div class="news-count">31 Berita</div>
                </div>
                <div class="news-card" onclick="showToast('Membuka berita', '📰')">
                    <img src="https://images.unsplash.com/photo-1504711434969-e33886168f5c?w=600" alt="News">
                    <div class="news-card-overlay">
                        <div class="news-read-btn">📖 BACA</div>
                    </div>
                </div>
            </div>

            <!-- === PAGE: MENU (BUG TOOLS) === -->
            <div class="page-content" id="page-menu">
                <div class="bug-header">
                    <div class="bug-header-top">METZ PROJECT</div>
                    <div class="bug-logo-text">X-Metz</div>
                    <div class="bug-header-info">
                        <div class="bug-info-left">
                            <span class="bug-info-label">EXP</span>
                            <span class="bug-info-value">2032-04-19</span>
                        </div>
                        <div class="bug-info-username">metz</div>
                        <div class="bug-info-right">
                            <span class="bug-info-label">ROLE</span>
                            <span class="bug-info-value">DEVELOPER</span>
                        </div>
                    </div>
                </div>

                <div class="bug-session-card">
                    <div class="bug-session-icon">📍</div>
                    <div class="bug-session-text">
                        <div class="title">Anda akan menggunakan session pribadi</div>
                        <div class="status">❌ Sender tidak ada</div>
                    </div>
                </div>

                <div class="bug-stats-grid">
                    <div class="bug-stat-card">
                        <div class="bug-stat-icon green">🐛</div>
                        <div class="bug-stat-label">Total Bug</div>
                        <div class="bug-stat-value">10</div>
                    </div>
                    <div class="bug-stat-card">
                        <div class="bug-stat-icon yellow">⚡</div>
                        <div class="bug-stat-label">Function</div>
                        <div class="bug-stat-value">GACOR</div>
                    </div>
                    <div class="bug-stat-card">
                        <div class="bug-stat-icon blue">🖥️</div>
                        <div class="bug-stat-label">Server</div>
                        <div class="bug-stat-value">ON</div>
                    </div>
                </div>

                <div class="bug-form-card">
                    <div class="bug-section-title">
                        <div class="icon-box">📞</div> Target Number
                    </div>
                    <div class="bug-input-wrapper">
                        <span class="input-icon">🌐</span>
                        <input type="tel" id="targetNumber" placeholder="e.g. 628xxxxx" autocomplete="off">
                    </div>
                    <div class="bug-input-hint">ⓘ Use international format without 0 or + (e.g., 628xxxxx)</div>
                </div>

                <div class="bug-form-card">
                    <div class="bug-type-header">
                        <div class="bug-section-title" style="margin-bottom:0;">
                            <div class="icon-box">🐛</div> Bug Type
                        </div>
                        <div class="bug-badge-active" id="badgeActive">✖ Buldo Crash delay</div>
                    </div>
                    <div class="bug-selector">
                        <button class="bug-arrow-btn" onclick="prevBug()">❮</button>
                        <div class="bug-option">
                            <div class="bug-icon-wrap" id="bugIcon">💬</div>
                            <div class="bug-info-wrap">
                                <div class="bug-name" id="bugName">✖ Buldo Crash delay</div>
                                <div class="bug-id" id="bugId">ID: buldo</div>
                            </div>
                            <div class="bug-check-icon">✓</div>
                        </div>
                        <button class="bug-arrow-btn" onclick="nextBug()">❯</button>
                    </div>
                    <div class="bug-dots" id="dotsContainer"></div>
                </div>

                <button class="bug-send-btn" onclick="sendBug()">
                    <span>✈</span> SEND BUG <span>→</span>
                </button>
            </div>

            <!-- === PAGE: TOOLS === -->
            <div class="page-content" id="page-tools">
                <div class="tools-header">
                    <h2>🔧 TOOLS</h2>
                    <p>Kumpulan alat bantu lengkap</p>
                </div>

                <div class="tools-grid">
                    <div class="tool-card teal" onclick="openPrayerTime()">
                        <div class="tool-card-icon">🕌</div>
                        <div class="tool-card-name">WAKTU SHOLAT</div>
                        <div class="tool-card-desc">Jadwal sholat realtime</div>
                    </div>
                    <div class="tool-card orange" onclick="openGames()">
                        <div class="tool-card-icon">🎮</div>
                        <div class="tool-card-name">PERMAINAN</div>
                        <div class="tool-card-desc">Mini games seru</div>
                    </div>
                    <div class="tool-card indigo" onclick="openCalculator()">
                        <div class="tool-card-icon">🧮</div>
                        <div class="tool-card-name">KALKULATOR</div>
                        <div class="tool-card-desc">Hitung cepat</div>
                    </div>
                    <div class="tool-card pink" onclick="openQrGenerator()">
                        <div class="tool-card-icon">📱</div>
                        <div class="tool-card-name">QR CODE</div>
                        <div class="tool-card-desc">Generator QR</div>
                    </div>
                    <div class="tool-card cyan" onclick="openPasswordGen()">
                        <div class="tool-card-icon">🔐</div>
                        <div class="tool-card-name">PASSWORD</div>
                        <div class="tool-card-desc">Generator aman</div>
                    </div>
                    <div class="tool-card lime" onclick="openBmiCalc()">
                        <div class="tool-card-icon">⚖️</div>
                        <div class="tool-card-name">BMI</div>
                        <div class="tool-card-desc">Cek berat badan</div>
                    </div>
                    <div class="tool-card deep-purple" onclick="openAgeCalc()">
                        <div class="tool-card-icon">🎂</div>
                        <div class="tool-card-name">USIA</div>
                        <div class="tool-card-desc">Hitung umur</div>
                    </div>
                    <div class="tool-card brown" onclick="openUnitConverter()">
                        <div class="tool-card-icon">📏</div>
                        <div class="tool-card-name">KONVERSI</div>
                        <div class="tool-card-desc">Satuan panjang</div>
                    </div>
                    <div class="tool-card blue-grey" onclick="openTextTools()">
                        <div class="tool-card-icon">📝</div>
                        <div class="tool-card-name">TEXT TOOLS</div>
                        <div class="tool-card-desc">Ubah teks</div>
                    </div>
                    <div class="tool-card amber" onclick="openColorPicker()">
                        <div class="tool-card-icon">🎨</div>
                        <div class="tool-card-name">WARNA</div>
                        <div class="tool-card-desc">Color picker</div>
                    </div>
                    <div class="tool-card red-dark" onclick="openStopwatch()">
                        <div class="tool-card-icon">⏱️</div>
                        <div class="tool-card-name">STOPWATCH</div>
                        <div class="tool-card-desc">Timer & stopwatch</div>
                    </div>
                    <div class="tool-card green-dark" onclick="openRandomPicker()">
                        <div class="tool-card-icon">🎲</div>
                        <div class="tool-card-name">RANDOM</div>
                        <div class="tool-card-desc">Angka acak</div>
                    </div>
                </div>
            </div>

            <!-- === PAGE: RAT === -->
            <div class="page-content" id="page-rat">
                <div class="profile-card">
                    <h2 class="page-title">📡 RAT PANEL</h2>
                    <div class="server-stats">
                        <div class="server-card">
                            <div class="server-header">
                                <span class="server-icon">🖥️</span>
                                <span class="server-name">VPS RAT 1</span>
                            </div>
                            <div class="server-detail">
                                Status: <span>ONLINE</span><br>
                                Devices: <span>12</span>
                            </div>
                        </div>
                        <div class="server-card">
                            <div class="server-header">
                                <span class="server-icon">🖥️</span>
                                <span class="server-name">VPS RAT 2</span>
                            </div>
                            <div class="server-detail">
                                Status: <span>ONLINE</span><br>
                                Devices: <span>8</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- === PAGE: TEMA === -->
            <div class="page-content" id="page-tema">
                <div class="profile-card">
                    <h2 class="page-title">🎨 TEMA</h2>
                    <div class="menu-grid">
                        <div class="menu-card blue" onclick="showToast('Tema Default', '🎨')">
                            <div class="menu-card-icon">🌙</div>
                            <div class="menu-card-name">DEFAULT</div>
                        </div>
                        <div class="menu-card purple" onclick="showToast('Tema Neon', '🎨')">
                            <div class="menu-card-icon">✨</div>
                            <div class="menu-card-name">NEON</div>
                        </div>
                        <div class="menu-card green" onclick="showToast('Tema Matrix', '🎨')">
                            <div class="menu-card-icon">🟢</div>
                            <div class="menu-card-name">MATRIX</div>
                        </div>
                        <div class="menu-card red" onclick="showToast('Tema Dark', '🎨')">
                            <div class="menu-card-icon">🔴</div>
                            <div class="menu-card-name">DARK</div>
                        </div>
                    </div>
                </div>
            </div>

        </div>

        <!-- BOTTOM NAVIGATION -->
        <div class="bottom-nav">
            <div class="nav-item active" onclick="switchNav(this, 'beranda')">
                <div class="nav-icon">🏠</div>
                <div class="nav-label">Beranda</div>
            </div>
            <div class="nav-item" onclick="switchNav(this, 'menu')">
                <div class="nav-icon">📋</div>
                <div class="nav-label">Menu</div>
            </div>
            <div class="nav-item" onclick="switchNav(this, 'rat')">
                <div class="nav-icon">📡</div>
                <div class="nav-label">RAT</div>
            </div>
            <div class="nav-item" onclick="switchNav(this, 'tools')">
                <div class="nav-icon">🔧</div>
                <div class="nav-label">Tools</div>
            </div>
            <div class="nav-item" onclick="switchNav(this, 'tema')">
                <div class="nav-icon">🎨</div>
                <div class="nav-label">Tema</div>
            </div>
        </div>
    </div>

    <!-- === MODAL: AKUN === -->
    <div class="modal-overlay" id="accountModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">👥 MANAJEMEN AKUN</div>
                <div class="modal-close" onclick="closeModal('accountModal')">✕</div>
            </div>
            <div class="account-list" id="accountList" style="display:flex;flex-direction:column;gap:10px;margin-bottom:15px;max-height:300px;overflow-y:auto;"></div>
            <button class="tool-action-btn" onclick="showAddAccountForm()">➕ TAMBAH AKUN BARU</button>
            <div id="addAccountForm" style="display:none;margin-top:15px;padding-top:15px;border-top:1px solid rgba(255,255,255,0.1);">
                <div class="tool-input-group">
                    <label>Username</label>
                    <input type="text" id="newUsername" placeholder="Masukkan username" autocomplete="off">
                </div>
                <div class="tool-input-group">
                    <label>Password</label>
                    <input type="text" id="newPassword" placeholder="Masukkan password" autocomplete="off">
                </div>
                <div style="display:flex;gap:8px;">
                    <button class="tool-action-btn" onclick="saveNewAccount()" style="flex:1;">✅ SIMPAN</button>
                    <button class="tool-action-btn secondary" onclick="hideAddAccountForm()" style="flex:0.5;">❌ BATAL</button>
                </div>
            </div>
        </div>
    </div>

    <!-- === MODAL: WAKTU SHOLAT === -->
    <div class="modal-overlay" id="prayerModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🕌 WAKTU SHOLAT</div>
                <div class="modal-close" onclick="closeModal('prayerModal')">✕</div>
            </div>
            <div class="prayer-location">
                <div class="prayer-location-icon">📍</div>
                <div class="prayer-location-text">
                    <div class="label">Lokasi</div>
                    <div class="value">Jakarta, Indonesia</div>
                </div>
            </div>
            <div class="prayer-date" id="prayerDate">-</div>
            <div class="prayer-list" id="prayerList"></div>
            <div class="prayer-countdown">
                <div class="label">MENUJU SHOLAT BERIKUTNYA</div>
                <div class="time" id="prayerCountdown">--:--:--</div>
            </div>
        </div>
    </div>

    <!-- === MODAL: GAMES === -->
    <div class="modal-overlay" id="gamesModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🎮 PERMAINAN</div>
                <div class="modal-close" onclick="closeModal('gamesModal')">✕</div>
            </div>
            <div class="games-grid" id="gamesGrid">
                <div class="game-card" onclick="startGame('clicker')">
                    <div class="game-card-icon">👆</div>
                    <div class="game-card-name">CLICKER</div>
                    <div class="game-card-desc">Klik target 30 detik</div>
                </div>
                <div class="game-card" onclick="startGame('reaction')">
                    <div class="game-card-icon">⚡</div>
                    <div class="game-card-name">REACTION</div>
                    <div class="game-card-desc">Tes refleks</div>
                </div>
                <div class="game-card" onclick="startGame('guess')">
                    <div class="game-card-icon">🎯</div>
                    <div class="game-card-name">TEBAK ANGKA</div>
                    <div class="game-card-desc">1 - 100</div>
                </div>
                <div class="game-card" onclick="startGame('math')">
                    <div class="game-card-icon">🧮</div>
                    <div class="game-card-name">MATEMATIKA</div>
                    <div class="game-card-desc">Hitung cepat</div>
                </div>
            </div>
            <div class="game-area" id="gameArea" style="display:none;">
                <div class="game-score" id="gameScore">Skor: 0</div>
                <div id="gameContent"></div>
                <div class="game-message" id="gameMessage"></div>
                <button class="game-btn" id="gameRestartBtn" onclick="restartGame()" style="display:none;">🔄 MAIN LAGI</button>
            </div>
        </div>
    </div>

    <!-- === MODAL: CALCULATOR === -->
    <div class="modal-overlay" id="calcModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🧮 KALKULATOR</div>
                <div class="modal-close" onclick="closeModal('calcModal')">✕</div>
            </div>
            <div class="calc-display" id="calcDisplay">0</div>
            <div class="calc-grid">
                <button class="calc-btn clear" onclick="calcClear()">C</button>
                <button class="calc-btn clear" onclick="calcDelete()">⌫</button>
                <button class="calc-btn operator" onclick="calcInput('%')">%</button>
                <button class="calc-btn operator" onclick="calcInput('/')">÷</button>
                <button class="calc-btn" onclick="calcInput('7')">7</button>
                <button class="calc-btn" onclick="calcInput('8')">8</button>
                <button class="calc-btn" onclick="calcInput('9')">9</button>
                <button class="calc-btn operator" onclick="calcInput('*')">×</button>
                <button class="calc-btn" onclick="calcInput('4')">4</button>
                <button class="calc-btn" onclick="calcInput('5')">5</button>
                <button class="calc-btn" onclick="calcInput('6')">6</button>
                <button class="calc-btn operator" onclick="calcInput('-')">−</button>
                <button class="calc-btn" onclick="calcInput('1')">1</button>
                <button class="calc-btn" onclick="calcInput('2')">2</button>
                <button class="calc-btn" onclick="calcInput('3')">3</button>
                <button class="calc-btn operator" onclick="calcInput('+')">+</button>
                <button class="calc-btn" onclick="calcInput('0')" style="grid-column:span 2;">0</button>
                <button class="calc-btn" onclick="calcInput('.')">.</button>
                <button class="calc-btn equal" onclick="calcEqual()">=</button>
            </div>
        </div>
    </div>

    <!-- === MODAL: QR GENERATOR === -->
    <div class="modal-overlay" id="qrModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">📱 QR CODE GENERATOR</div>
                <div class="modal-close" onclick="closeModal('qrModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Masukkan Teks / URL</label>
                <textarea id="qrInput" placeholder="Contoh: https://metzproject.id"></textarea>
            </div>
            <button class="tool-action-btn" onclick="generateQR()">🔲 GENERATE QR</button>
            <div id="qrResult"></div>
        </div>
    </div>

    <!-- === MODAL: PASSWORD GENERATOR === -->
    <div class="modal-overlay" id="passwordModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🔐 PASSWORD GENERATOR</div>
                <div class="modal-close" onclick="closeModal('passwordModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Panjang Password</label>
                <input type="number" id="passLength" value="16" min="4" max="64">
            </div>
            <div style="display:flex;gap:8px;margin-bottom:12px;flex-wrap:wrap;">
                <label style="display:flex;align-items:center;gap:5px;font-size:11px;color:#d0e4ff;cursor:pointer;">
                    <input type="checkbox" id="passUpper" checked> Huruf Besar
                </label>
                <label style="display:flex;align-items:center;gap:5px;font-size:11px;color:#d0e4ff;cursor:pointer;">
                    <input type="checkbox" id="passLower" checked> Huruf Kecil
                </label>
                <label style="display:flex;align-items:center;gap:5px;font-size:11px;color:#d0e4ff;cursor:pointer;">
                    <input type="checkbox" id="passNum" checked> Angka
                </label>
                <label style="display:flex;align-items:center;gap:5px;font-size:11px;color:#d0e4ff;cursor:pointer;">
                    <input type="checkbox" id="passSym" checked> Simbol
                </label>
            </div>
            <button class="tool-action-btn" onclick="generatePassword()">🔑 GENERATE</button>
            <div id="passResult"></div>
        </div>
    </div>

    <!-- === MODAL: BMI CALCULATOR === -->
    <div class="modal-overlay" id="bmiModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">⚖️ BMI CALCULATOR</div>
                <div class="modal-close" onclick="closeModal('bmiModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Berat Badan (kg)</label>
                <input type="number" id="bmiWeight" placeholder="Contoh: 65" step="0.1">
            </div>
            <div class="tool-input-group">
                <label>Tinggi Badan (cm)</label>
                <input type="number" id="bmiHeight" placeholder="Contoh: 170" step="0.1">
            </div>
            <button class="tool-action-btn" onclick="calculateBMI()">📊 HITUNG BMI</button>
            <div id="bmiResult"></div>
        </div>
    </div>

    <!-- === MODAL: AGE CALCULATOR === -->
    <div class="modal-overlay" id="ageModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🎂 USIA CALCULATOR</div>
                <div class="modal-close" onclick="closeModal('ageModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Tanggal Lahir</label>
                <input type="date" id="birthDate">
            </div>
            <button class="tool-action-btn" onclick="calculateAge()">🎈 HITUNG USIA</button>
            <div id="ageResult"></div>
        </div>
    </div>

    <!-- === MODAL: UNIT CONVERTER === -->
    <div class="modal-overlay" id="unitModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">📏 KONVERSI SATUAN</div>
                <div class="modal-close" onclick="closeModal('unitModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Nilai</label>
                <input type="number" id="unitValue" placeholder="Contoh: 100" step="0.01">
            </div>
            <div class="tool-input-group">
                <label>Dari</label>
                <select id="unitFrom">
                    <option value="m">Meter (m)</option>
                    <option value="km">Kilometer (km)</option>
                    <option value="cm">Centimeter (cm)</option>
                    <option value="mm">Millimeter (mm)</option>
                    <option value="mi">Mile (mi)</option>
                    <option value="yd">Yard (yd)</option>
                    <option value="ft">Feet (ft)</option>
                    <option value="in">Inch (in)</option>
                </select>
            </div>
            <div class="tool-input-group">
                <label>Ke</label>
                <select id="unitTo">
                    <option value="km">Kilometer (km)</option>
                    <option value="m">Meter (m)</option>
                    <option value="cm">Centimeter (cm)</option>
                    <option value="mm">Millimeter (mm)</option>
                    <option value="mi">Mile (mi)</option>
                    <option value="yd">Yard (yd)</option>
                    <option value="ft">Feet (ft)</option>
                    <option value="in">Inch (in)</option>
                </select>
            </div>
            <button class="tool-action-btn" onclick="convertUnit()">🔄 KONVERSI</button>
            <div id="unitResult"></div>
        </div>
    </div>

    <!-- === MODAL: TEXT TOOLS === -->
    <div class="modal-overlay" id="textModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">📝 TEXT TOOLS</div>
                <div class="modal-close" onclick="closeModal('textModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Masukkan Teks</label>
                <textarea id="textInput" placeholder="Ketik teks di sini..."></textarea>
            </div>
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;">
                <button class="tool-action-btn" onclick="textUpper()">🔠 UPPERCASE</button>
                <button class="tool-action-btn" onclick="textLower()">🔡 lowercase</button>
                <button class="tool-action-btn" onclick="textReverse()">🔃 REVERSE</button>
                <button class="tool-action-btn" onclick="textCount()">🔢 HITUNG</button>
                <button class="tool-action-btn" onclick="textCopy()">📋 COPY</button>
                <button class="tool-action-btn" onclick="textClear()">🗑️ CLEAR</button>
            </div>
            <div id="textResult"></div>
        </div>
    </div>

    <!-- === MODAL: COLOR PICKER === -->
    <div class="modal-overlay" id="colorModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🎨 COLOR PICKER</div>
                <div class="modal-close" onclick="closeModal('colorModal')">✕</div>
            </div>
            <div class="tool-input-group">
                <label>Pilih Warna</label>
                <input type="color" id="colorInput" value="#00c6ff" style="height:80px;cursor:pointer;">
            </div>
            <div id="colorResult"></div>
        </div>
    </div>

    <!-- === MODAL: STOPWATCH === -->
    <div class="modal-overlay" id="stopwatchModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">⏱️ STOPWATCH & TIMER</div>
                <div class="modal-close" onclick="closeModal('stopwatchModal')">✕</div>
            </div>
            <div class="tool-badge">STOPWATCH</div>
            <div class="calc-display" id="stopwatchDisplay" style="text-align:center;font-size:32px;">00:00:00</div>
            <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;">
                <button class="tool-action-btn" onclick="startStopwatch()" id="swStartBtn">▶️ START</button>
                <button class="tool-action-btn secondary" onclick="stopStopwatch()">⏸️ STOP</button>
                <button class="tool-action-btn secondary" onclick="resetStopwatch()">🔄 RESET</button>
            </div>

            <div style="margin-top:20px;padding-top:20px;border-top:1px solid rgba(255,255,255,0.1);">
                <div class="tool-badge">TIMER (menit)</div>
                <div class="tool-input-group">
                    <input type="number" id="timerMinutes" placeholder="Masukkan menit" min="1" max="60" value="5">
                </div>
                <div class="calc-display" id="timerDisplay" style="text-align:center;font-size:32px;">05:00</div>
                <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;">
                    <button class="tool-action-btn" onclick="startTimer()">▶️ START TIMER</button>
                    <button class="tool-action-btn secondary" onclick="stopTimer()">⏸️ STOP</button>
                </div>
            </div>
        </div>
    </div>

    <!-- === MODAL: RANDOM PICKER === -->
    <div class="modal-overlay" id="randomModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🎲 RANDOM GENERATOR</div>
                <div class="modal-close" onclick="closeModal('randomModal')">✕</div>
            </div>
            <div class="tool-badge">ANGKA ACAK</div>
            <div class="tool-input-group">
                <label>Minimum</label>
                <input type="number" id="randMin" value="1">
            </div>
            <div class="tool-input-group">
                <label>Maximum</label>
                <input type="number" id="randMax" value="100">
            </div>
            <button class="tool-action-btn" onclick="generateRandom()">🎲 GENERATE ANGKA</button>
            <div id="randResult"></div>

            <div style="margin-top:20px;padding-top:20px;border-top:1px solid rgba(255,255,255,0.1);">
                <div class="tool-badge">PILIH DARI DAFTAR</div>
                <div class="tool-input-group">
                    <label>Daftar (pisahkan dengan koma)</label>
                    <textarea id="randList" placeholder="Contoh: Apel, Jeruk, Mangga"></textarea>
                </div>
                <button class="tool-action-btn" onclick="pickFromList()">🎯 PILIH ACAK</button>
                <div id="listResult"></div>
            </div>
        </div>
    </div>

    <!-- Toast -->
    <div class="toast" id="toast">
        <span id="toastIcon">✅</span>
        <span id="toastMessage">Pesan</span>
    </div>

    <!-- Loading -->
    <div class="loading-overlay" id="loadingOverlay">
        <div class="spinner"></div>
        <div class="loading-text">MENGIRIM BUG...</div>
    </div>

    <script>
        // === DATA ===
        const bugList = [
            { name: '✖ Buldo Crash delay', id: 'buldo', icon: '💬' },
            { name: '⚡ Hard Crash', id: 'hardcrash', icon: '⚡' },
            { name: '💥 Infinite Loop', id: 'loop', icon: '💥' },
            { name: '🔒 Freeze System', id: 'freeze', icon: '🔒' },
            { name: '📵 Force Close', id: 'forceclose', icon: '📵' },
            { name: '🔥 Blank Screen', id: 'blank', icon: '🔥' },
            { name: '📡 Network Crash', id: 'netcrash', icon: '📡' },
            { name: '⏳ Delay Spam', id: 'delayspam', icon: '⏳' },
            { name: '🔄 Restart Loop', id: 'restart', icon: '🔄' },
            { name: '💀 Deadlock', id: 'deadlock', icon: '💀' }
        ];

        let currentBugIndex = 0;

        let accounts = [{ username: 'Metz', password: '1', isMain: true }];

        // === LOAD/SAVE ACCOUNTS ===
        function loadAccounts() {
            try {
                const saved = localStorage.getItem('metz_accounts');
                if (saved) {
                    accounts = JSON.parse(saved);
                    if (!accounts.find(a => a.username === 'Metz' && a.password === '1')) {
                        accounts.unshift({ username: 'Metz', password: '1', isMain: true });
                    }
                }
            } catch (e) {}
        }

        function saveAccounts() {
            try { localStorage.setItem('metz_accounts', JSON.stringify(accounts)); } catch (e) {}
        }

        // === LOGIN ===
        function handleLogin() {
            const user = document.getElementById('usernameInput').value.trim();
            const pass = document.getElementById('passwordInput').value.trim();
            const error = document.getElementById('loginError');
            const found = accounts.find(a => a.username === user && a.password === pass);

            if (found) {
                error.style.display = 'none';
                document.getElementById('loginPage').style.opacity = '0';
                document.getElementById('loginPage').style.visibility = 'hidden';
                setTimeout(() => { document.getElementById('appContainer').style.display = 'flex'; }, 300);
                showToast(`Login berhasil! Selamat datang, ${found.username}.`, '✅');
            } else {
                error.style.display = 'block';
                error.textContent = 'Username atau Password salah!';
                const box = document.querySelector('.login-box');
                box.style.animation = 'none';
                box.offsetHeight;
                box.style.animation = 'shake 0.3s';
            }
        }

        document.getElementById('passwordInput').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') handleLogin();
        });
        document.getElementById('usernameInput').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') document.getElementById('passwordInput').focus();
        });

        function handleLogout() {
            if (confirm('Yakin ingin logout?')) {
                document.getElementById('appContainer').style.display = 'none';
                const lp = document.getElementById('loginPage');
                lp.style.opacity = '1';
                lp.style.visibility = 'visible';
                document.getElementById('usernameInput').value = '';
                document.getElementById('passwordInput').value = '';
                showToast('Anda telah logout.', '👋');
            }
        }

        // === SIDEBAR ===
        function openSidebar() {
            document.getElementById('sidebar').classList.add('active');
            document.getElementById('sidebarOverlay').classList.add('active');
        }

        function closeSidebar() {
            document.getElementById('sidebar').classList.remove('active');
            document.getElementById('sidebarOverlay').classList.remove('active');
        }

        function sidebarNav(page, element) {
            document.querySelectorAll('.sidebar-item').forEach(item => item.classList.remove('active'));
            element.classList.add('active');
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            const navMap = { 'beranda': 0, 'menu': 1, 'rat': 2, 'tools': 3, 'tema': 4 };
            if (navMap[page] !== undefined) document.querySelectorAll('.nav-item')[navMap[page]].classList.add('active');
            document.querySelectorAll('.page-content').forEach(p => p.classList.remove('active'));
            document.getElementById('page-' + page).classList.add('active');
            document.getElementById('mainContent').scrollTop = 0;
            if (page === 'menu') renderBug();
            closeSidebar();
        }

        // === ACCOUNT MANAGEMENT ===
        function openAccountModal() {
            renderAccounts();
            openModal('accountModal');
        }

        function renderAccounts() {
            const list = document.getElementById('accountList');
            list.innerHTML = '';
            accounts.forEach((acc, index) => {
                const item = document.createElement('div');
                item.style.cssText = 'background:rgba(255,255,255,0.08);border:1px solid rgba(255,255,255,0.15);border-radius:14px;padding:12px 15px;display:flex;align-items:center;gap:12px;';
                item.innerHTML = `
                    <div style="width:40px;height:40px;border-radius:50%;background:linear-gradient(135deg,#00c6ff,#0072ff);display:flex;justify-content:center;align-items:center;font-size:18px;font-weight:700;color:#fff;flex-shrink:0;">${acc.username.charAt(0).toUpperCase()}</div>
                    <div style="flex:1;min-width:0;">
                        <div style="font-family:'Orbitron';font-size:13px;font-weight:700;color:#fff;margin-bottom:2px;">${acc.username} ${acc.isMain ? '👑' : ''}</div>
                        <div style="font-size:11px;color:#8aa4c0;font-family:monospace;" data-idx="${index}"><span>••••••</span></div>
                    </div>
                    <div style="display:flex;gap:6px;">
                        <button onclick="togglePassword(${index})" style="width:30px;height:30px;border-radius:8px;border:1px solid rgba(255,255,255,0.15);background:rgba(255,255,255,0.08);color:#fff;display:flex;justify-content:center;align-items:center;cursor:pointer;font-size:13px;">👁️</button>
                        ${!acc.isMain ? `<button onclick="deleteAccount(${index})" style="width:30px;height:30px;border-radius:8px;border:1px solid rgba(255,50,50,0.3);background:rgba(255,50,50,0.15);color:#ff6b6b;display:flex;justify-content:center;align-items:center;cursor:pointer;font-size:13px;">🗑️</button>` : ''}
                    </div>
                `;
                list.appendChild(item);
            });
        }

        function togglePassword(index) {
            const el = document.querySelector(`[data-idx="${index}"]`);
            if (!el) return;
            const acc = accounts[index];
            if (el.innerHTML.includes('••••••')) {
                el.innerHTML = `<span style="color:#00c6ff;">${acc.password}</span>`;
            } else {
                el.innerHTML = `<span>••••••</span>`;
            }
        }

        function deleteAccount(index) {
            if (accounts[index].isMain) { showToast('Akun utama tidak bisa dihapus!', '⚠️'); return; }
            if (confirm(`Hapus akun "${accounts[index].username}"?`)) {
                accounts.splice(index, 1);
                saveAccounts();
                renderAccounts();
                showToast('Akun berhasil dihapus!', '🗑️');
            }
        }

        function showAddAccountForm() {
            document.getElementById('addAccountForm').style.display = 'block';
            document.getElementById('newUsername').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('newUsername').focus();
        }

        function hideAddAccountForm() {
            document.getElementById('addAccountForm').style.display = 'none';
        }

        function saveNewAccount() {
            const username = document.getElementById('newUsername').value.trim();
            const password = document.getElementById('newPassword').value.trim();
            if (!username || !password) { showToast('Username dan password harus diisi!', '⚠️'); return; }
            if (username.length < 3) { showToast('Username minimal 3 karakter!', '⚠️'); return; }
            if (accounts.find(a => a.username.toLowerCase() === username.toLowerCase())) {
                showToast('Username sudah digunakan!', '⚠️'); return;
            }
            accounts.push({ username, password, isMain: false });
            saveAccounts();
            renderAccounts();
            hideAddAccountForm();
            showToast(`Akun "${username}" berhasil ditambahkan!`, '✅');
        }

        // === MODAL ===
        function openModal(id) {
            document.getElementById(id).classList.add('active');
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
            if (id === 'gamesModal') stopAllGames();
            if (id === 'prayerModal') clearInterval(prayerInterval);
        }

        document.querySelectorAll('.modal-overlay').forEach(overlay => {
            overlay.addEventListener('click', (e) => {
                if (e.target === overlay) {
                    overlay.classList.remove('active');
                    if (overlay.id === 'gamesModal') stopAllGames();
                    if (overlay.id === 'prayerModal') clearInterval(prayerInterval);
                }
            });
        });

        // === NAVIGATION ===
        function switchNav(element, page) {
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            element.classList.add('active');
            document.querySelectorAll('.page-content').forEach(p => p.classList.remove('active'));
            document.getElementById('page-' + page).classList.add('active');
            document.getElementById('mainContent').scrollTop = 0;
            if (page === 'menu') renderBug();
        }

        function goToMenu() {
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.nav-item')[1].classList.add('active');
            document.querySelectorAll('.page-content').forEach(p => p.classList.remove('active'));
            document.getElementById('page-menu').classList.add('active');
            document.getElementById('mainContent').scrollTop = 0;
            renderBug();
        }

        // === BUG ===
        function renderBug() {
            const bug = bugList[currentBugIndex];
            document.getElementById('bugName').textContent = bug.name;
            document.getElementById('bugId').textContent = 'ID: ' + bug.id;
            document.getElementById('bugIcon').textContent = bug.icon;
            document.getElementById('badgeActive').textContent = bug.name;
            const dotsContainer = document.getElementById('dotsContainer');
            if (dotsContainer) {
                dotsContainer.innerHTML = '';
                bugList.forEach((_, i) => {
                    const dot = document.createElement('div');
                    dot.className = 'bug-dot' + (i === currentBugIndex ? ' active' : '');
                    dotsContainer.appendChild(dot);
                });
            }
        }

        function nextBug() { currentBugIndex = (currentBugIndex + 1) % bugList.length; renderBug(); }
        function prevBug() { currentBugIndex = (currentBugIndex - 1 + bugList.length) % bugList.length; renderBug(); }

        function sendBug() {
            const target = document.getElementById('targetNumber').value.trim();
            if (!target) { showToast('Masukkan target number terlebih dahulu!', '⚠️'); return; }
            if (target.length < 8) { showToast('Format nomor tidak valid!', '⚠️'); return; }
            const bug = bugList[currentBugIndex];
            document.getElementById('loadingOverlay').classList.add('active');
            setTimeout(() => {
                document.getElementById('loadingOverlay').classList.remove('active');
                showToast(`Bug "${bug.name}" berhasil dikirim ke ${target}!`, '🚀');
            }, 2000);
        }

        // === WHATSAPP ===
        function contactWhatsApp() {
            const phoneNumber = '6288905090028';
            const message = encodeURIComponent('Halo Metz Project, saya ingin bertanya.');
            const waUrl = `https://wa.me/${phoneNumber}?text=${message}`;
            showToast('Membuka WhatsApp...', '💬');
            setTimeout(() => window.open(waUrl, '_blank'), 500);
        }

        // === WAKTU SHOLAT ===
        const prayerTimes = { Subuh: '04:30', Dzuhur: '11:45', Ashar: '15:00', Maghrib: '17:55', Isya: '19:10' };
        let prayerInterval;

        function openPrayerTime() {
            openModal('prayerModal');
            updatePrayerDisplay();
            clearInterval(prayerInterval);
            prayerInterval = setInterval(updatePrayerDisplay, 1000);
        }

        function updatePrayerDisplay() {
            const now = new Date();
            const days = ['Minggu', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu'];
            const months = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
            document.getElementById('prayerDate').textContent = `${days[now.getDay()]}, ${now.getDate()} ${months[now.getMonth()]} ${now.getFullYear()}`;
            const icons = { Subuh: '🌙', Dzuhur: '☀️', Ashar: '🌤️', Maghrib: '🌆', Isya: '🌃' };
            const list = document.getElementById('prayerList');
            const nowMin = now.getHours() * 60 + now.getMinutes();
            let nextPrayer = null, nextTime = null;
            for (const [name, time] of Object.entries(prayerTimes)) {
                const [h, m] = time.split(':').map(Number);
                if (h * 60 + m > nowMin) { nextPrayer = name; nextTime = time; break; }
            }
            if (!nextPrayer) { nextPrayer = 'Subuh'; nextTime = prayerTimes.Subuh; }
            list.innerHTML = '';
            for (const [name, time] of Object.entries(prayerTimes)) {
                const isNext = name === nextPrayer;
                const item = document.createElement('div');
                item.className = 'prayer-item' + (isNext ? ' next' : '');
                item.innerHTML = `<div class="prayer-name"><div class="prayer-icon">${icons[name]}</div>${name}</div><div class="prayer-time">${time}</div>`;
                list.appendChild(item);
            }
            const [nh, nm] = nextTime.split(':').map(Number);
            const nextDate = new Date();
            nextDate.setHours(nh, nm, 0, 0);
            if (nextDate < now) nextDate.setDate(nextDate.getDate() + 1);
            const diff = nextDate - now;
            const h = Math.floor(diff / 3600000), m = Math.floor((diff % 3600000) / 60000), s = Math.floor((diff % 60000) / 1000);
            document.getElementById('prayerCountdown').textContent = `${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
        }

        // === GAMES ===
        let gameState = { active: false, type: null, score: 0, timer: null, interval: null, targetNum: 0, reactionStart: 0, startTime: 0 };

        function openGames() {
            openModal('gamesModal');
            document.getElementById('gamesGrid').style.display = 'grid';
            document.getElementById('gameArea').style.display = 'none';
        }

        function startGame(type) {
            gameState = { active: true, type, score: 0, timer: null, interval: null, targetNum: 0, reactionStart: 0, startTime: Date.now() };
            document.getElementById('gamesGrid').style.display = 'none';
            document.getElementById('gameArea').style.display = 'flex';
            document.getElementById('gameRestartBtn').style.display = 'none';
            document.getElementById('gameMessage').textContent = '';
            document.getElementById('gameScore').textContent = 'Skor: 0';
            if (type === 'clicker') startClicker();
            else if (type === 'reaction') startReaction();
            else if (type === 'guess') startGuess();
            else if (type === 'math') startMath();
        }

        function stopAllGames() {
            if (gameState.interval) clearInterval(gameState.interval);
            if (gameState.timer) clearTimeout(gameState.timer);
            gameState.active = false;
        }

        function restartGame() { if (gameState.type) startGame(gameState.type); }

        function startClicker() {
            gameState.score = 0;
            gameState.startTime = Date.now();
            const duration = 30000;
            document.getElementById('gameContent').innerHTML = `<div id="clickTarget" onclick="clickTarget()" style="width:80px;height:80px;border-radius:50%;background:linear-gradient(135deg,#00c6ff,#0072ff);display:flex;justify-content:center;align-items:center;font-size:36px;cursor:pointer;user-select:none;box-shadow:0 0 30px rgba(0,198,255,0.5);">🎯</div>`;
            document.getElementById('gameMessage').textContent = 'Klik target sebanyak mungkin!';
            gameState.interval = setInterval(() => {
                const elapsed = Date.now() - gameState.startTime;
                const remaining = Math.max(0, Math.ceil((duration - elapsed) / 1000));
                document.getElementById('gameScore').textContent = `Skor: ${gameState.score} | Waktu: ${remaining}s`;
                if (elapsed >= duration) {
                    clearInterval(gameState.interval);
                    gameState.active = false;
                    document.getElementById('gameMessage').innerHTML = `⏰ Waktu habis!<br>Skor akhir: <strong style="color:#00c6ff; font-size:18px;">${gameState.score}</strong>`;
                    document.getElementById('gameRestartBtn').style.display = 'inline-block';
                    document.getElementById('gameContent').innerHTML = '';
                }
            }, 100);
        }

        function clickTarget() {
            if (!gameState.active) return;
            gameState.score++;
            const target = document.getElementById('clickTarget');
            if (target) {
                target.style.position = 'relative';
                target.style.left = (Math.random() * 200 - 100) + 'px';
                target.style.top = (Math.random() * 100 - 50) + 'px';
                target.textContent = ['🎯', '💥', '⚡', '🔥', '💎'][Math.floor(Math.random() * 5)];
            }
        }

        function startReaction() {
            gameState.score = 0;
            document.getElementById('gameScore').textContent = 'Bersiaplah...';
            document.getElementById('gameContent').innerHTML = `<div style="font-size:60px;">⏳</div>`;
            document.getElementById('gameMessage').textContent = 'Tunggu warna hijau, lalu klik!';
            const waitTime = 2000 + Math.random() * 3000;
            gameState.timer = setTimeout(() => {
                if (!gameState.active) return;
                document.getElementById('gameContent').innerHTML = `<div id="reactTarget" onclick="reactionClick()" style="width:80px;height:80px;border-radius:50%;background:linear-gradient(135deg,#00ff64,#00aa44);display:flex;justify-content:center;align-items:center;font-size:36px;cursor:pointer;user-select:none;box-shadow:0 0 30px rgba(0,255,100,0.5);">⚡</div>`;
                document.getElementById('gameScore').textContent = 'KLIK SEKARANG!';
                gameState.reactionStart = Date.now();
            }, waitTime);
        }

        function reactionClick() {
            if (!gameState.active || !gameState.reactionStart) return;
            const elapsed = Date.now() - gameState.reactionStart;
            gameState.active = false;
            document.getElementById('gameScore').textContent = `${elapsed} ms`;
            document.getElementById('gameMessage').innerHTML = `⚡ Waktu reaksi: <strong style="color:#00c6ff; font-size:20px;">${elapsed} ms</strong><br>${elapsed < 250 ? '🔥 Luar biasa!' : elapsed < 400 ? '👍 Bagus!' : '😅 Perlu latihan lagi'}`;
            document.getElementById('gameRestartBtn').style.display = 'inline-block';
            document.getElementById('gameContent').innerHTML = '';
        }

        function startGuess() {
            gameState.targetNum = Math.floor(Math.random() * 100) + 1;
            gameState.score = 0;
            gameState.active = true;
            document.getElementById('gameScore').textContent = 'Tebak angka 1-100';
            document.getElementById('gameContent').innerHTML = `<input type="number" id="guessInput" placeholder="Masukkan angka" style="width:100%;padding:15px;border-radius:12px;background:rgba(0,0,0,0.4);border:1px solid rgba(0,198,255,0.3);color:white;font-size:16px;text-align:center;outline:none;margin-bottom:10px;"><button onclick="submitGuess()" class="game-btn" style="width:100%;margin-top:0;">TEBAK</button>`;
            document.getElementById('gameMessage').textContent = 'Masukkan angka antara 1 sampai 100';
        }

        function submitGuess() {
            const input = document.getElementById('guessInput');
            const val = parseInt(input.value);
            if (isNaN(val) || val < 1 || val > 100) { document.getElementById('gameMessage').textContent = '⚠️ Masukkan angka 1-100!'; return; }
            gameState.score++;
            document.getElementById('gameScore').textContent = `Percobaan: ${gameState.score}`;
            if (val === gameState.targetNum) {
                gameState.active = false;
                document.getElementById('gameMessage').innerHTML = `🎉 BENAR! Angka: <strong style="color:#00c6ff;">${gameState.targetNum}</strong><br>Percobaan: <strong>${gameState.score}</strong>`;
                document.getElementById('gameContent').innerHTML = '';
                document.getElementById('gameRestartBtn').style.display = 'inline-block';
            } else if (val < gameState.targetNum) {
                document.getElementById('gameMessage').textContent = '⬆️ Terlalu kecil!';
                input.value = ''; input.focus();
            } else {
                document.getElementById('gameMessage').textContent = '⬇️ Terlalu besar!';
                input.value = ''; input.focus();
            }
        }

        function startMath() { gameState.score = 0; gameState.active = true; nextMathQuestion(); }

        function nextMathQuestion() {
            const a = Math.floor(Math.random() * 20) + 1;
            const b = Math.floor(Math.random() * 20) + 1;
            const ops = ['+', '-', '×'];
            const op = ops[Math.floor(Math.random() * ops.length)];
            let answer;
            if (op === '+') answer = a + b; else if (op === '-') answer = a - b; else answer = a * b;
            gameState.targetNum = answer;
            document.getElementById('gameContent').innerHTML = `<div style="font-family:'Orbitron';font-size:36px;font-weight:900;color:#00c6ff;margin-bottom:15px;">${a} ${op} ${b} = ?</div><input type="number" id="mathInput" placeholder="Jawaban" style="width:100%;padding:15px;border-radius:12px;background:rgba(0,0,0,0.4);border:1px solid rgba(0,198,255,0.3);color:white;font-size:16px;text-align:center;outline:none;margin-bottom:10px;"><button onclick="submitMath()" class="game-btn" style="width:100%;margin-top:0;">JAWAB</button>`;
            document.getElementById('gameMessage').textContent = 'Hitung dengan cepat!';
            setTimeout(() => { const inp = document.getElementById('mathInput'); if (inp) inp.focus(); }, 100);
        }

        function submitMath() {
            const input = document.getElementById('mathInput');
            const val = parseInt(input.value);
            if (isNaN(val)) return;
            if (val === gameState.targetNum) {
                gameState.score++;
                document.getElementById('gameScore').textContent = `Skor: ${gameState.score}`;
                document.getElementById('gameMessage').textContent = '✅ Benar!';
                nextMathQuestion();
            } else {
                gameState.active = false;
                document.getElementById('gameMessage').innerHTML = `❌ Salah! Jawaban: <strong style="color:#00c6ff;">${gameState.targetNum}</strong><br>Skor akhir: <strong>${gameState.score}</strong>`;
                document.getElementById('gameContent').innerHTML = '';
                document.getElementById('gameRestartBtn').style.display = 'inline-block';
            }
        }

        // === CALCULATOR ===
        let calcValue = '0';
        function openCalculator() { openModal('calcModal'); calcValue = '0'; updateCalcDisplay(); }
        function updateCalcDisplay() { document.getElementById('calcDisplay').textContent = calcValue; }

        function calcInput(val) {
            if (calcValue === '0' && !isNaN(val) && val !== '.') calcValue = val;
            else if (['+', '-', '*', '/', '%'].includes(val)) {
                if (['+', '-', '*', '/', '%'].includes(calcValue.slice(-1))) calcValue = calcValue.slice(0, -1) + val;
                else calcValue += val;
            } else calcValue += val;
            updateCalcDisplay();
        }

        function calcClear() { calcValue = '0'; updateCalcDisplay(); }
        function calcDelete() { calcValue = calcValue.length > 1 ? calcValue.slice(0, -1) : '0'; updateCalcDisplay(); }

        function calcEqual() {
            try {
                let expr = calcValue.replace(/×/g, '*').replace(/÷/g, '/');
                calcValue = String(eval(expr));
                updateCalcDisplay();
            } catch (e) {
                calcValue = 'Error';
                updateCalcDisplay();
                setTimeout(() => { calcValue = '0'; updateCalcDisplay(); }, 1500);
            }
        }

        // === QR GENERATOR ===
        function openQrGenerator() {
            openModal('qrModal');
            document.getElementById('qrInput').value = '';
            document.getElementById('qrResult').innerHTML = '';
        }

        function generateQR() {
            const input = document.getElementById('qrInput').value.trim();
            if (!input) { showToast('Masukkan teks atau URL!', '⚠️'); return; }
            const qrUrl = `https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=${encodeURIComponent(input)}`;
            document.getElementById('qrResult').innerHTML = `<div class="qr-display"><img src="${qrUrl}" alt="QR Code"></div>`;
            showToast('QR Code berhasil dibuat!', '✅');
        }

        // === PASSWORD GENERATOR ===
        function openPasswordGen() {
            openModal('passwordModal');
            document.getElementById('passResult').innerHTML = '';
        }

        function generatePassword() {
            const length = parseInt(document.getElementById('passLength').value) || 16;
            const useUpper = document.getElementById('passUpper').checked;
            const useLower = document.getElementById('passLower').checked;
            const useNum = document.getElementById('passNum').checked;
            const useSym = document.getElementById('passSym').checked;

            let chars = '';
            if (useUpper) chars += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            if (useLower) chars += 'abcdefghijklmnopqrstuvwxyz';
            if (useNum) chars += '0123456789';
            if (useSym) chars += '!@#$%^&*()_+-=[]{}|;:,.<>?';

            if (!chars) { showToast('Pilih minimal satu jenis karakter!', '⚠️'); return; }

            let password = '';
            for (let i = 0; i < length; i++) {
                password += chars.charAt(Math.floor(Math.random() * chars.length));
            }

            // Strength
            let strength = 'Lemah', color = '#ff6b6b';
            if (length >= 12 && (useUpper + useLower + useNum + useSym) >= 3) { strength = 'Kuat'; color = '#00ff64'; }
            else if (length >= 8 && (useUpper + useLower + useNum + useSym) >= 2) { strength = 'Sedang'; color = '#ffc107'; }

            document.getElementById('passResult').innerHTML = `
                <div class="tool-result success" style="font-family:monospace;font-size:14px;text-align:center;letter-spacing:1px;">
                    ${password}
                </div>
                <div style="text-align:center;margin-top:10px;font-size:11px;color:${color};">
                    Kekuatan: <strong>${strength}</strong>
                </div>
            `;
            showToast('Password berhasil dibuat!', '🔑');
        }

        // === BMI CALCULATOR ===
        function openBmiCalc() {
            openModal('bmiModal');
            document.getElementById('bmiWeight').value = '';
            document.getElementById('bmiHeight').value = '';
            document.getElementById('bmiResult').innerHTML = '';
        }

        function calculateBMI() {
            const weight = parseFloat(document.getElementById('bmiWeight').value);
            const height = parseFloat(document.getElementById('bmiHeight').value) / 100;
            if (!weight || !height) { showToast('Isi berat dan tinggi badan!', '⚠️'); return; }

            const bmi = weight / (height * height);
            let category = '', color = '';
            if (bmi < 18.5) { category = 'Kurus'; color = '#00c6ff'; }
            else if (bmi < 25) { category = 'Normal'; color = '#00ff64'; }
            else if (bmi < 30) { category = 'Gemuk'; color = '#ffc107'; }
            else { category = 'Obesitas'; color = '#ff6b6b'; }

            document.getElementById('bmiResult').innerHTML = `
                <div class="tool-result success" style="text-align:center;">
                    <div style="font-family:'Orbitron';font-size:32px;font-weight:900;color:${color};">${bmi.toFixed(1)}</div>
                    <div style="font-size:13px;margin-top:5px;color:${color};font-weight:600;">${category}</div>
                </div>
            `;
        }

        // === AGE CALCULATOR ===
        function openAgeCalc() {
            openModal('ageModal');
            document.getElementById('birthDate').value = '';
            document.getElementById('ageResult').innerHTML = '';
        }

        function calculateAge() {
            const birth = document.getElementById('birthDate').value;
            if (!birth) { showToast('Pilih tanggal lahir!', '⚠️'); return; }
            const birthDate = new Date(birth);
            const today = new Date();
            let years = today.getFullYear() - birthDate.getFullYear();
            let months = today.getMonth() - birthDate.getMonth();
            let days = today.getDate() - birthDate.getDate();

            if (days < 0) { months--; days += new Date(today.getFullYear(), today.getMonth(), 0).getDate(); }
            if (months < 0) { years--; months += 12; }

            const totalDays = Math.floor((today - birthDate) / (1000 * 60 * 60 * 24));

            document.getElementById('ageResult').innerHTML = `
                <div class="tool-result success" style="text-align:center;">
                    <div style="font-family:'Orbitron';font-size:24px;font-weight:900;color:#00c6ff;">${years} Tahun</div>
                    <div style="font-size:12px;margin-top:5px;color:#d0e4ff;">${months} Bulan ${days} Hari</div>
                    <div style="font-size:11px;margin-top:8px;color:#8aa4c0;">Total: ${totalDays.toLocaleString()} hari</div>
                </div>
            `;
        }

        // === UNIT CONVERTER ===
        const unitRates = { m: 1, km: 1000, cm: 0.01, mm: 0.001, mi: 1609.344, yd: 0.9144, ft: 0.3048, in: 0.0254 };

        function openUnitConverter() {
            openModal('unitModal');
            document.getElementById('unitValue').value = '';
            document.getElementById('unitResult').innerHTML = '';
        }

        function convertUnit() {
            const val = parseFloat(document.getElementById('unitValue').value);
            const from = document.getElementById('unitFrom').value;
            const to = document.getElementById('unitTo').value;
            if (isNaN(val)) { showToast('Masukkan nilai yang valid!', '⚠️'); return; }
            const result = val * unitRates[from] / unitRates[to];
            document.getElementById('unitResult').innerHTML = `
                <div class="tool-result success" style="text-align:center;">
                    <div style="font-size:12px;color:#8aa4c0;">${val} ${from} =</div>
                    <div style="font-family:'Orbitron';font-size:22px;font-weight:900;color:#00c6ff;margin-top:5px;">${result.toFixed(4)} ${to}</div>
                </div>
            `;
        }

        // === TEXT TOOLS ===
        function openTextTools() {
            openModal('textModal');
            document.getElementById('textInput').value = '';
            document.getElementById('textResult').innerHTML = '';
        }

        function textUpper() {
            const t = document.getElementById('textInput').value;
            document.getElementById('textResult').innerHTML = `<div class="tool-result">${t.toUpperCase()}</div>`;
        }

        function textLower() {
            const t = document.getElementById('textInput').value;
            document.getElementById('textResult').innerHTML = `<div class="tool-result">${t.toLowerCase()}</div>`;
        }

        function textReverse() {
            const t = document.getElementById('textInput').value;
            document.getElementById('textResult').innerHTML = `<div class="tool-result">${t.split('').reverse().join('')}</div>`;
        }

        function textCount() {
            const t = document.getElementById('textInput').value;
            const chars = t.length;
            const words = t.trim() ? t.trim().split(/\s+/).length : 0;
            const lines = t.split('\n').length;
            document.getElementById('textResult').innerHTML = `
                <div class="tool-result success">
                    <div>📝 Karakter: <strong>${chars}</strong></div>
                    <div>📄 Kata: <strong>${words}</strong></div>
                    <div>📋 Baris: <strong>${lines}</strong></div>
                </div>
            `;
        }

        function textCopy() {
            const t = document.getElementById('textInput').value;
            if (!t) { showToast('Teks kosong!', '⚠️'); return; }
            navigator.clipboard.writeText(t).then(() => showToast('Teks disalin!', '📋'));
        }

        function textClear() {
            document.getElementById('textInput').value = '';
            document.getElementById('textResult').innerHTML = '';
        }

        // === COLOR PICKER ===
        function openColorPicker() {
            openModal('colorModal');
            updateColorDisplay();
            document.getElementById('colorInput').oninput = updateColorDisplay;
        }

        function updateColorDisplay() {
            const c = document.getElementById('colorInput').value;
            const r = parseInt(c.substr(1, 2), 16);
            const g = parseInt(c.substr(3, 2), 16);
            const b = parseInt(c.substr(5, 2), 16);
            document.getElementById('colorResult').innerHTML = `
                <div style="background:${c};height:80px;border-radius:12px;margin-bottom:12px;box-shadow:0 0 30px ${c};"></div>
                <div class="tool-result">
                    <div>HEX: <strong style="color:#00c6ff;">${c.toUpperCase()}</strong></div>
                    <div>RGB: <strong style="color:#00c6ff;">rgb(${r}, ${g}, ${b})</strong></div>
                </div>
            `;
        }

        // === STOPWATCH ===
        let swInterval = null, swTime = 0, swRunning = false;
        let timerInterval = null, timerTime = 0, timerRunning = false;

        function openStopwatch() {
            openModal('stopwatchModal');
            resetStopwatch();
            updateTimerDisplay();
        }

        function startStopwatch() {
            if (swRunning) return;
            swRunning = true;
            document.getElementById('swStartBtn').textContent = '⏸️ PAUSE';
            swInterval = setInterval(() => {
                swTime += 10;
                updateStopwatchDisplay();
            }, 10);
        }

        function stopStopwatch() {
            if (!swRunning) return;
            swRunning = false;
            clearInterval(swInterval);
            document.getElementById('swStartBtn').textContent = '▶️ START';
        }

        function resetStopwatch() {
            clearInterval(swInterval);
            swRunning = false;
            swTime = 0;
            document.getElementById('swStartBtn').textContent = '▶️ START';
            updateStopwatchDisplay();
        }

        function updateStopwatchDisplay() {
            const ms = Math.floor((swTime % 1000) / 10);
            const s = Math.floor(swTime / 1000) % 60;
            const m = Math.floor(swTime / 60000) % 60;
            const h = Math.floor(swTime / 3600000);
            document.getElementById('stopwatchDisplay').textContent = 
                `${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}.${String(ms).padStart(2,'0')}`;
        }

        function startTimer() {
            const mins = parseInt(document.getElementById('timerMinutes').value) || 5;
            if (timerRunning) return;
            timerRunning = true;
            timerTime = mins * 60;
            timerInterval = setInterval(() => {
                if (timerTime <= 0) {
                    clearInterval(timerInterval);
                    timerRunning = false;
                    showToast('⏰ Waktu habis!', '🔔');
                    return;
                }
                timerTime--;
                updateTimerDisplay();
            }, 1000);
        }

        function stopTimer() {
            clearInterval(timerInterval);
            timerRunning = false;
        }

        function updateTimerDisplay() {
            const m = Math.floor(timerTime / 60);
            const s = timerTime % 60;
            document.getElementById('timerDisplay').textContent = `${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
        }

        // === RANDOM ===
        function openRandomPicker() {
            openModal('randomModal');
            document.getElementById('randResult').innerHTML = '';
            document.getElementById('listResult').innerHTML = '';
        }

        function generateRandom() {
            const min = parseInt(document.getElementById('randMin').value) || 1;
            const max = parseInt(document.getElementById('randMax').value) || 100;
            if (min >= max) { showToast('Min harus lebih kecil dari Max!', '⚠️'); return; }
            const result = Math.floor(Math.random() * (max - min + 1)) + min;
            document.getElementById('randResult').innerHTML = `
                <div class="tool-result success" style="text-align:center;">
                    <div style="font-family:'Orbitron';font-size:36px;font-weight:900;color:#00c6ff;">${result}</div>
                    <div style="font-size:11px;color:#8aa4c0;margin-top:5px;">Antara ${min} - ${max}</div>
                </div>
            `;
        }

        function pickFromList() {
            const list = document.getElementById('randList').value;
            if (!list.trim()) { showToast('Masukkan daftar terlebih dahulu!', '⚠️'); return; }
            const items = list.split(',').map(i => i.trim()).filter(i => i);
            if (items.length === 0) { showToast('Daftar kosong!', '⚠️'); return; }
            const picked = items[Math.floor(Math.random() * items.length)];
            document.getElementById('listResult').innerHTML = `
                <div class="tool-result success" style="text-align:center;">
                    <div style="font-family:'Orbitron';font-size:22px;font-weight:900;color:#00c6ff;">${picked}</div>
                    <div style="font-size:11px;color:#8aa4c0;margin-top:5px;">Dari ${items.length} pilihan</div>
                </div>
            `;
        }

        // === TOAST ===
        let toastTimeout;
        function showToast(message, icon = '✅') {
            const toast = document.getElementById('toast');
            document.getElementById('toastMessage').textContent = message;
            document.getElementById('toastIcon').textContent = icon;
            toast.classList.add('show');
            clearTimeout(toastTimeout);
            toastTimeout = setTimeout(() => toast.classList.remove('show'), 2500);
        }

        // === AUTO-HIDE HEADER ===
        const mainContent = document.getElementById('mainContent');
        let lastScrollTop = 0;
        mainContent.addEventListener('scroll', () => {
            const scrollTop = mainContent.scrollTop;
            const header = document.getElementById('mainHeader');
            if (scrollTop > lastScrollTop && scrollTop > 100) header.style.transform = 'translateY(-100%)';
            else header.style.transform = 'translateY(0)';
            lastScrollTop = scrollTop;
        });

        // === KEYBOARD ===
        document.addEventListener('keydown', (e) => {
            if (document.getElementById('page-menu').classList.contains('active')) {
                if (e.key === 'ArrowRight') nextBug();
                if (e.key === 'ArrowLeft') prevBug();
            }
        });

        // === INIT ===
        loadAccounts();
    </script>

</body>
</html>
