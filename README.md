# Waste-Segregation-in-healthcare-using-Ai-assistant
you can find which waste should go in rigth bin 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MediWaste Guide — Healthcare Waste Segregation</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --yellow: #F5C518;
    --red: #E63946;
    --blue: #1D7FDB;
    --green: #2DC653;
    --black: #111827;
    --white: #FAFAF8;
    --grey: #6B7280;
    --light: #F3F4F6;
    --card-bg: #FFFFFF;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--white);
    color: var(--black);
    overflow-x: hidden;
  }

  /* ===== NAV ===== */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 18px 48px;
    background: rgba(250,250,248,0.92);
    backdrop-filter: blur(16px);
    border-bottom: 1.5px solid rgba(0,0,0,0.07);
  }
  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-weight: 800; font-size: 1.25rem;
    letter-spacing: -0.5px;
    display: flex; align-items: center; gap: 10px;
    text-decoration: none; color: var(--black);
  }
  .nav-logo span { color: var(--red); }
  .logo-dot {
    width: 10px; height: 10px; border-radius: 50%;
    background: var(--red); display: inline-block;
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%,100% { transform: scale(1); opacity:1; }
    50% { transform: scale(1.4); opacity:0.6; }
  }
  .nav-links {
    display: flex; gap: 32px; list-style: none;
  }
  .nav-links a {
    text-decoration: none; color: var(--grey);
    font-size: 0.9rem; font-weight: 500;
    transition: color 0.2s;
  }
  .nav-links a:hover, .nav-links a.active { color: var(--black); }
  .nav-cta {
    background: var(--black); color: var(--white) !important;
    padding: 10px 22px; border-radius: 50px;
    font-weight: 500 !important; font-size: 0.85rem !important;
    transition: background 0.2s !important;
  }
  .nav-cta:hover { background: var(--red) !important; color: var(--white) !important; }

  /* ===== PAGES ===== */
  .page { display: none; padding-top: 80px; min-height: 100vh; }
  .page.active { display: block; }

  /* ===== PAGE 1: HERO ===== */
  .hero {
    min-height: calc(100vh - 80px);
    display: grid; grid-template-columns: 1fr 1fr;
    align-items: center; gap: 0;
    padding: 60px 48px 60px;
    position: relative; overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; top: -200px; right: -200px;
    width: 600px; height: 600px; border-radius: 50%;
    background: radial-gradient(circle, rgba(230,57,70,0.08), transparent 70%);
    pointer-events: none;
  }
  .hero-left { max-width: 560px; }
  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(230,57,70,0.08); color: var(--red);
    border: 1px solid rgba(230,57,70,0.2);
    padding: 6px 16px; border-radius: 50px;
    font-size: 0.8rem; font-weight: 600;
    letter-spacing: 0.5px; margin-bottom: 28px;
    text-transform: uppercase;
  }
  .hero-badge::before { content: '🏥'; font-size: 0.9rem; }
  .hero h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.8rem, 5vw, 4rem);
    font-weight: 800; line-height: 1.08;
    letter-spacing: -2px; margin-bottom: 24px;
  }
  .hero h1 .accent { color: var(--red); }
  .hero p {
    font-size: 1.1rem; color: var(--grey);
    line-height: 1.7; margin-bottom: 40px;
    font-weight: 300; max-width: 440px;
  }
  .hero-actions { display: flex; gap: 16px; flex-wrap: wrap; }
  .btn-primary {
    background: var(--black); color: var(--white);
    padding: 16px 32px; border-radius: 50px;
    font-size: 0.95rem; font-weight: 500;
    border: none; cursor: pointer;
    transition: all 0.25s; letter-spacing: 0.3px;
    display: inline-flex; align-items: center; gap: 8px;
  }
  .btn-primary:hover { background: var(--red); transform: translateY(-2px); box-shadow: 0 12px 32px rgba(230,57,70,0.25); }
  .btn-secondary {
    background: transparent; color: var(--black);
    padding: 16px 32px; border-radius: 50px;
    font-size: 0.95rem; font-weight: 500;
    border: 2px solid rgba(0,0,0,0.15); cursor: pointer;
    transition: all 0.25s;
    display: inline-flex; align-items: center; gap: 8px;
  }
  .btn-secondary:hover { border-color: var(--black); transform: translateY(-2px); }

  /* Bin Illustration */
  .hero-right {
    display: flex; align-items: center; justify-content: center;
    position: relative;
  }
  .bins-showcase {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 20px; transform: rotate(-3deg);
  }
  .bin-card {
    border-radius: 24px; padding: 28px 24px;
    text-align: center; position: relative;
    overflow: hidden; cursor: pointer;
    transition: transform 0.3s, box-shadow 0.3s;
    animation: float 3s ease-in-out infinite;
  }
  .bin-card:nth-child(2) { animation-delay: 0.5s; margin-top: 30px; }
  .bin-card:nth-child(3) { animation-delay: 1s; }
  .bin-card:nth-child(4) { animation-delay: 1.5s; margin-top: 30px; }
  @keyframes float {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }
  .bin-card:hover { transform: translateY(-12px) scale(1.04); box-shadow: 0 20px 60px rgba(0,0,0,0.15); }
  .bin-card.yellow { background: #FFF8E1; border: 2px solid #F5C518; }
  .bin-card.red { background: #FFEBEE; border: 2px solid #E63946; }
  .bin-card.blue { background: #E3F2FD; border: 2px solid #1D7FDB; }
  .bin-card.green { background: #E8F5E9; border: 2px solid #2DC653; }
  .bin-icon { font-size: 2.8rem; margin-bottom: 10px; display: block; }
  .bin-label {
    font-family: 'Syne', sans-serif;
    font-weight: 700; font-size: 0.8rem;
    letter-spacing: 0.5px; text-transform: uppercase;
  }
  .bin-card.yellow .bin-label { color: #B8860B; }
  .bin-card.red .bin-label { color: var(--red); }
  .bin-card.blue .bin-label { color: var(--blue); }
  .bin-card.green .bin-label { color: #1a7a35; }

  /* Stats */
  .hero-stats {
    display: flex; gap: 48px; margin-top: 48px;
    padding-top: 40px; border-top: 1px solid rgba(0,0,0,0.08);
  }
  .stat-item { }
  .stat-number {
    font-family: 'Syne', sans-serif;
    font-size: 2rem; font-weight: 800;
    letter-spacing: -1px;
  }
  .stat-label { font-size: 0.8rem; color: var(--grey); margin-top: 2px; }

  /* ===== PAGE 2: GUIDE ===== */
  .guide-header {
    background: var(--black); color: var(--white);
    padding: 80px 48px 60px;
    position: relative; overflow: hidden;
  }
  .guide-header::before {
    content: 'GUIDE';
    position: absolute; right: -20px; top: 50%;
    transform: translateY(-50%);
    font-family: 'Syne', sans-serif; font-size: 12rem;
    font-weight: 800; color: rgba(255,255,255,0.04);
    letter-spacing: -5px; pointer-events: none;
  }
  .guide-header h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3.2rem);
    font-weight: 800; letter-spacing: -1.5px;
    max-width: 600px; line-height: 1.1;
  }
  .guide-header p {
    color: rgba(255,255,255,0.6); margin-top: 16px;
    font-size: 1rem; max-width: 500px; line-height: 1.6;
  }

  .bins-grid {
    display: grid; grid-template-columns: repeat(2, 1fr);
    gap: 2px; background: rgba(0,0,0,0.08);
  }
  .bin-section {
    background: var(--white);
    padding: 56px 48px; position: relative;
    overflow: hidden;
  }
  .bin-section::before {
    content: attr(data-color-label);
    position: absolute; right: -30px; bottom: -20px;
    font-family: 'Syne', sans-serif; font-size: 8rem;
    font-weight: 800; opacity: 0.04; letter-spacing: -3px;
    color: var(--black); pointer-events: none;
  }
  .bin-section-header {
    display: flex; align-items: center; gap: 20px;
    margin-bottom: 36px;
  }
  .bin-icon-large {
    width: 72px; height: 72px; border-radius: 20px;
    display: flex; align-items: center; justify-content: center;
    font-size: 2.2rem; flex-shrink: 0;
  }
  .bin-section.yellow-sec .bin-icon-large { background: #FFF8E1; border: 2px solid #F5C518; }
  .bin-section.red-sec .bin-icon-large { background: #FFEBEE; border: 2px solid #E63946; }
  .bin-section.blue-sec .bin-icon-large { background: #E3F2FD; border: 2px solid #1D7FDB; }
  .bin-section.green-sec .bin-icon-large { background: #E8F5E9; border: 2px solid #2DC653; }

  .bin-section-title {
    font-family: 'Syne', sans-serif;
    font-weight: 800; font-size: 1.5rem;
    letter-spacing: -0.5px;
  }
  .bin-color-tag {
    display: inline-block; padding: 4px 14px;
    border-radius: 50px; font-size: 0.72rem;
    font-weight: 700; text-transform: uppercase;
    letter-spacing: 1px; margin-top: 6px;
  }
  .yellow-sec .bin-color-tag { background: #FFF8E1; color: #B8860B; border: 1px solid #F5C518; }
  .red-sec .bin-color-tag { background: #FFEBEE; color: var(--red); border: 1px solid #E63946; }
  .blue-sec .bin-color-tag { background: #E3F2FD; color: var(--blue); border: 1px solid #1D7FDB; }
  .green-sec .bin-color-tag { background: #E8F5E9; color: #1a7a35; border: 1px solid #2DC653; }

  .waste-list { list-style: none; }
  .waste-item {
    display: flex; align-items: flex-start; gap: 14px;
    padding: 14px 0; border-bottom: 1px solid rgba(0,0,0,0.06);
  }
  .waste-item:last-child { border-bottom: none; }
  .waste-dot {
    width: 8px; height: 8px; border-radius: 50%;
    flex-shrink: 0; margin-top: 7px;
  }
  .yellow-sec .waste-dot { background: #F5C518; }
  .red-sec .waste-dot { background: #E63946; }
  .blue-sec .waste-dot { background: #1D7FDB; }
  .green-sec .waste-dot { background: #2DC653; }
  .waste-text { font-size: 0.92rem; line-height: 1.5; color: var(--black); }
  .waste-text small { color: var(--grey); font-size: 0.8rem; display: block; margin-top: 2px; }

  /* ===== PAGE 3: FINDER ===== */
  .finder-section { padding: 60px 48px; }
  .finder-section h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800; letter-spacing: -1.5px;
    margin-bottom: 12px;
  }
  .finder-section > p { color: var(--grey); margin-bottom: 48px; font-size: 1rem; }

  .search-box {
    position: relative; max-width: 600px; margin-bottom: 48px;
  }
  .search-input {
    width: 100%; padding: 20px 60px 20px 24px;
    border-radius: 50px; border: 2px solid rgba(0,0,0,0.1);
    font-size: 1rem; font-family: 'DM Sans', sans-serif;
    background: var(--white); color: var(--black);
    outline: none; transition: border 0.2s, box-shadow 0.2s;
  }
  .search-input:focus { border-color: var(--black); box-shadow: 0 0 0 4px rgba(0,0,0,0.05); }
  .search-btn {
    position: absolute; right: 8px; top: 50%;
    transform: translateY(-50%);
    background: var(--black); color: var(--white);
    border: none; border-radius: 50px;
    padding: 12px 24px; cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem; font-weight: 500;
    transition: background 0.2s;
  }
  .search-btn:hover { background: var(--red); }

  .categories-tabs {
    display: flex; gap: 12px; flex-wrap: wrap; margin-bottom: 40px;
  }
  .cat-tab {
    padding: 10px 22px; border-radius: 50px;
    border: 1.5px solid rgba(0,0,0,0.12);
    background: transparent; cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem; font-weight: 500;
    transition: all 0.2s; color: var(--grey);
  }
  .cat-tab.active, .cat-tab:hover {
    background: var(--black); color: var(--white);
    border-color: var(--black);
  }

  .items-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 16px;
  }
  .item-card {
    background: var(--white); border-radius: 20px;
    padding: 24px; border: 1.5px solid rgba(0,0,0,0.08);
    display: flex; align-items: flex-start; gap: 16px;
    transition: all 0.25s; cursor: pointer;
  }
  .item-card:hover { transform: translateY(-4px); box-shadow: 0 12px 40px rgba(0,0,0,0.1); border-color: transparent; }
  .item-color-strip {
    width: 5px; height: 100%; border-radius: 4px;
    flex-shrink: 0; min-height: 60px;
  }
  .item-card .item-info { flex: 1; }
  .item-name { font-weight: 600; font-size: 0.95rem; margin-bottom: 6px; }
  .item-bin {
    font-size: 0.75rem; font-weight: 700;
    text-transform: uppercase; letter-spacing: 0.8px;
    padding: 3px 10px; border-radius: 20px;
    display: inline-block;
  }
  .item-desc { font-size: 0.8rem; color: var(--grey); margin-top: 8px; line-height: 1.4; }

  /* Result highlight */
  .search-result-highlight {
    display: none; margin-bottom: 32px;
    padding: 28px 32px; border-radius: 24px;
    border: 2px solid transparent;
    animation: slideIn 0.4s ease;
  }
  @keyframes slideIn {
    from { opacity:0; transform: translateY(10px); }
    to { opacity:1; transform: translateY(0); }
  }
  .search-result-highlight.show { display: flex; gap: 24px; align-items: center; }
  .result-bin-visual {
    width: 100px; height: 120px; border-radius: 16px;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center; gap: 8px;
    flex-shrink: 0;
  }
  .result-bin-visual .bin-emoji { font-size: 3rem; }
  .result-bin-name {
    font-family: 'Syne', sans-serif;
    font-weight: 800; font-size: 0.75rem;
    text-transform: uppercase; letter-spacing: 1px;
  }
  .result-info h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.4rem; font-weight: 800;
    letter-spacing: -0.5px; margin-bottom: 8px;
  }
  .result-info p { color: var(--grey); font-size: 0.9rem; line-height: 1.5; }

  /* ===== PAGE 4: RULES ===== */
  .rules-hero {
    padding: 80px 48px 60px;
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
    color: var(--white);
  }
  .rules-hero h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.2rem, 4vw, 3.5rem);
    font-weight: 800; letter-spacing: -1.5px;
    margin-bottom: 16px;
  }
  .rules-hero p { color: rgba(255,255,255,0.6); font-size: 1rem; max-width: 500px; line-height: 1.6; }
  
  .rules-grid {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 24px; padding: 60px 48px;
  }
  .rule-card {
    background: var(--white); border-radius: 24px;
    padding: 36px 32px; border: 1.5px solid rgba(0,0,0,0.07);
    position: relative; overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .rule-card:hover { transform: translateY(-6px); box-shadow: 0 20px 60px rgba(0,0,0,0.1); }
  .rule-number {
    font-family: 'Syne', sans-serif;
    font-size: 4rem; font-weight: 800;
    color: rgba(0,0,0,0.05); line-height: 1;
    margin-bottom: 16px; letter-spacing: -2px;
  }
  .rule-icon { font-size: 2rem; margin-bottom: 16px; display: block; }
  .rule-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700; font-size: 1.1rem;
    margin-bottom: 12px; letter-spacing: -0.3px;
  }
  .rule-desc { font-size: 0.88rem; color: var(--grey); line-height: 1.6; }
  .rule-card.featured {
    background: var(--black); color: var(--white);
    grid-column: span 1;
  }
  .rule-card.featured .rule-number { color: rgba(255,255,255,0.06); }
  .rule-card.featured .rule-desc { color: rgba(255,255,255,0.6); }

  /* Penalty Section */
  .do-dont-section { padding: 0 48px 60px; }
  .do-dont-section h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.8rem; font-weight: 800; letter-spacing: -1px;
    margin-bottom: 32px;
  }
  .do-dont-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
  .do-card, .dont-card {
    border-radius: 20px; padding: 32px;
  }
  .do-card { background: #E8F5E9; border: 1.5px solid #2DC653; }
  .dont-card { background: #FFEBEE; border: 1.5px solid #E63946; }
  .do-dont-header {
    display: flex; align-items: center; gap: 12px;
    margin-bottom: 24px;
  }
  .do-dont-header h4 {
    font-family: 'Syne', sans-serif;
    font-weight: 800; font-size: 1.2rem;
  }
  .do-card .do-dont-header h4 { color: #1a7a35; }
  .dont-card .do-dont-header h4 { color: var(--red); }
  .check-list, .x-list { list-style: none; }
  .check-list li, .x-list li {
    padding: 10px 0; font-size: 0.9rem;
    display: flex; align-items: flex-start; gap: 10px;
    border-bottom: 1px solid rgba(0,0,0,0.06);
  }
  .check-list li:last-child, .x-list li:last-child { border-bottom: none; }
  .check-list li::before { content: '✓'; color: #2DC653; font-weight: 700; flex-shrink: 0; }
  .x-list li::before { content: '✗'; color: var(--red); font-weight: 700; flex-shrink: 0; }

  /* ===== PAGE 5: QUIZ ===== */
  .quiz-section { padding: 80px 48px; max-width: 800px; margin: 0 auto; }
  .quiz-section h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800; letter-spacing: -1.5px;
    margin-bottom: 12px; text-align: center;
  }
  .quiz-section > p { color: var(--grey); text-align: center; margin-bottom: 48px; }

  .quiz-progress { margin-bottom: 40px; }
  .quiz-progress-bar {
    height: 6px; background: var(--light); border-radius: 6px; overflow: hidden;
  }
  .quiz-progress-fill {
    height: 100%; background: var(--black); border-radius: 6px;
    transition: width 0.5s ease;
  }
  .quiz-progress-text {
    font-size: 0.8rem; color: var(--grey); margin-top: 8px;
    font-weight: 500;
  }

  .quiz-card {
    background: var(--white); border-radius: 28px;
    padding: 48px; border: 1.5px solid rgba(0,0,0,0.08);
    box-shadow: 0 8px 40px rgba(0,0,0,0.06);
  }
  .quiz-question {
    font-family: 'Syne', sans-serif;
    font-size: 1.3rem; font-weight: 700;
    margin-bottom: 32px; line-height: 1.3;
    letter-spacing: -0.3px;
  }
  .quiz-item-name {
    font-size: 1.6rem; margin-bottom: 8px;
    text-align: center; display: block;
  }
  .quiz-options {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  .quiz-option {
    padding: 20px 24px; border-radius: 16px;
    border: 2px solid rgba(0,0,0,0.1);
    cursor: pointer; transition: all 0.25s;
    display: flex; align-items: center; gap: 14px;
    font-weight: 500; font-size: 0.95rem;
    background: var(--white);
    font-family: 'DM Sans', sans-serif;
  }
  .quiz-option:hover { border-color: var(--black); transform: translateY(-2px); }
  .quiz-option.correct { background: #E8F5E9; border-color: #2DC653; color: #1a7a35; }
  .quiz-option.wrong { background: #FFEBEE; border-color: var(--red); color: var(--red); }
  .quiz-option .opt-color {
    width: 28px; height: 28px; border-radius: 50%;
    flex-shrink: 0;
  }

  .quiz-feedback {
    margin-top: 24px; padding: 20px 24px;
    border-radius: 16px; font-size: 0.9rem;
    line-height: 1.5; display: none;
    animation: slideIn 0.3s ease;
  }
  .quiz-feedback.show { display: block; }
  .quiz-feedback.correct-fb { background: #E8F5E9; border: 1.5px solid #2DC653; color: #1a7a35; }
  .quiz-feedback.wrong-fb { background: #FFEBEE; border: 1.5px solid var(--red); color: var(--red); }

  .quiz-next {
    margin-top: 24px; width: 100%;
    background: var(--black); color: var(--white);
    border: none; border-radius: 50px;
    padding: 18px; cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem; font-weight: 500;
    transition: background 0.2s; display: none;
  }
  .quiz-next.show { display: block; }
  .quiz-next:hover { background: var(--red); }

  .quiz-result {
    text-align: center; display: none;
  }
  .quiz-result.show { display: block; }
  .quiz-score {
    font-family: 'Syne', sans-serif;
    font-size: 5rem; font-weight: 800;
    letter-spacing: -3px;
  }
  .quiz-score-label { color: var(--grey); margin-bottom: 24px; }
  .quiz-retake {
    background: var(--black); color: var(--white);
    border: none; border-radius: 50px;
    padding: 16px 40px; cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem; font-weight: 500;
    margin-top: 24px; transition: background 0.2s;
  }
  .quiz-retake:hover { background: var(--red); }

  /* ===== FOOTER ===== */
  footer {
    background: var(--black); color: rgba(255,255,255,0.5);
    padding: 48px; text-align: center;
    font-size: 0.85rem;
  }
  footer strong { color: var(--white); }

  /* ===== PAGE 6: AI FEATURES ===== */
  .ai-hero {
    padding: 72px 48px 52px;
    background: linear-gradient(135deg, #0a0a0f 0%, #0f1729 50%, #1a0f2e 100%);
    color: var(--white); position: relative; overflow: hidden;
  }
  .ai-hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 70% 60% at 70% 50%, rgba(99,52,235,0.18), transparent);
    pointer-events: none;
  }
  .ai-hero-grid {
    display: grid; grid-template-columns: 1fr auto; gap: 40px; align-items: center;
  }
  .ai-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(139,92,246,0.2); color: #c4b5fd;
    border: 1px solid rgba(139,92,246,0.35);
    padding: 6px 16px; border-radius: 50px;
    font-size: 0.78rem; font-weight: 600; letter-spacing: 0.8px;
    text-transform: uppercase; margin-bottom: 20px;
  }
  .ai-hero h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3.2rem);
    font-weight: 800; letter-spacing: -1.5px; line-height: 1.08;
    margin-bottom: 14px;
  }
  .ai-hero h2 .ai-glow { color: #a78bfa; }
  .ai-hero p { color: rgba(255,255,255,0.55); font-size: 1rem; max-width: 500px; line-height: 1.65; }

  .ai-features-tabs {
    display: flex; gap: 0; padding: 0 48px;
    border-bottom: 1.5px solid rgba(0,0,0,0.08);
    background: var(--white); position: sticky; top: 80px; z-index: 50;
  }
  .ai-tab {
    padding: 18px 28px; border: none; background: transparent;
    font-family: 'DM Sans', sans-serif; font-size: 0.88rem; font-weight: 500;
    color: var(--grey); cursor: pointer; border-bottom: 2.5px solid transparent;
    margin-bottom: -1.5px; transition: all 0.2s; display: flex; align-items: center; gap: 8px;
  }
  .ai-tab:hover { color: var(--black); }
  .ai-tab.active { color: var(--black); border-bottom-color: var(--black); font-weight: 600; }
  .ai-tab-dot { width: 8px; height: 8px; border-radius: 50%; }

  .ai-panel { display: none; padding: 48px; }
  .ai-panel.active { display: block; }

  /* ===== CLASSIFIER ===== */
  .classifier-layout {
    display: grid; grid-template-columns: 1fr 1fr; gap: 40px; align-items: start;
  }
  .classifier-input-wrap { }
  .classifier-label {
    font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1.2rem;
    margin-bottom: 8px; letter-spacing: -0.3px;
  }
  .classifier-sub { color: var(--grey); font-size: 0.88rem; margin-bottom: 24px; line-height: 1.5; }
  .classifier-textarea {
    width: 100%; padding: 20px; border-radius: 20px;
    border: 2px solid rgba(0,0,0,0.1);
    font-size: 0.95rem; font-family: 'DM Sans', sans-serif;
    background: var(--white); color: var(--black);
    outline: none; resize: vertical; min-height: 140px;
    transition: border 0.2s, box-shadow 0.2s; line-height: 1.5;
  }
  .classifier-textarea:focus { border-color: #8b5cf6; box-shadow: 0 0 0 4px rgba(139,92,246,0.08); }
  .classifier-examples { margin: 14px 0; }
  .example-chip {
    display: inline-block; padding: 6px 14px; border-radius: 50px;
    background: var(--light); border: 1px solid rgba(0,0,0,0.08);
    font-size: 0.78rem; color: var(--grey); margin: 4px 4px 4px 0;
    cursor: pointer; transition: all 0.2s;
  }
  .example-chip:hover { background: var(--black); color: var(--white); border-color: var(--black); }
  .classify-btn {
    width: 100%; padding: 18px; border-radius: 50px;
    background: linear-gradient(135deg, #7c3aed, #4f46e5);
    color: var(--white); border: none; cursor: pointer;
    font-family: 'DM Sans', sans-serif; font-size: 1rem; font-weight: 600;
    transition: all 0.25s; margin-top: 8px;
    display: flex; align-items: center; justify-content: center; gap: 10px;
  }
  .classify-btn:hover { transform: translateY(-2px); box-shadow: 0 12px 32px rgba(124,58,237,0.3); }
  .classify-btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }

  .classifier-result {
    border-radius: 24px; padding: 36px;
    background: var(--light); border: 2px solid rgba(0,0,0,0.06);
    min-height: 200px; display: flex; align-items: center; justify-content: center;
    transition: all 0.4s;
  }
  .classifier-result.loaded {
    background: var(--white); border-color: rgba(0,0,0,0.1);
    align-items: flex-start;
  }
  .result-placeholder {
    text-align: center; color: var(--grey);
  }
  .result-placeholder .placeholder-icon { font-size: 3rem; margin-bottom: 12px; opacity: 0.4; }
  .result-placeholder p { font-size: 0.9rem; }

  .result-bin-card {
    width: 100%;
  }
  .result-bin-header {
    display: flex; align-items: center; gap: 20px; margin-bottom: 24px;
  }
  .result-bin-circle {
    width: 80px; height: 80px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 2.2rem; flex-shrink: 0;
  }
  .result-bin-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.5rem; font-weight: 800; letter-spacing: -0.5px;
  }
  .result-bin-subtitle { font-size: 0.85rem; color: var(--grey); margin-top: 4px; }
  .result-reason {
    font-size: 0.9rem; line-height: 1.6; color: var(--black);
    padding: 16px; background: rgba(0,0,0,0.03);
    border-radius: 14px; border-left: 3px solid;
  }
  .result-steps { margin-top: 20px; }
  .result-steps-title {
    font-size: 0.78rem; font-weight: 700; text-transform: uppercase;
    letter-spacing: 1px; color: var(--grey); margin-bottom: 12px;
  }
  .result-step {
    display: flex; align-items: flex-start; gap: 12px;
    padding: 10px 0; border-bottom: 1px solid rgba(0,0,0,0.05);
    font-size: 0.88rem;
  }
  .result-step:last-child { border-bottom: none; }
  .step-num {
    width: 22px; height: 22px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 0.7rem; font-weight: 700; flex-shrink: 0;
    color: white;
  }

  /* AI Loader */
  .ai-loader {
    display: flex; flex-direction: column; align-items: center; gap: 16px;
    color: var(--grey); font-size: 0.9rem;
  }
  .ai-loader-dots {
    display: flex; gap: 8px;
  }
  .ai-loader-dots span {
    width: 10px; height: 10px; border-radius: 50%;
    background: #8b5cf6; animation: dotBounce 1.2s infinite;
  }
  .ai-loader-dots span:nth-child(2) { animation-delay: 0.2s; }
  .ai-loader-dots span:nth-child(3) { animation-delay: 0.4s; }
  @keyframes dotBounce {
    0%,80%,100% { transform: scale(0.6); opacity: 0.4; }
    40% { transform: scale(1); opacity: 1; }
  }

  /* ===== CHAT ASSISTANT ===== */
  .chat-layout { display: grid; grid-template-columns: 280px 1fr; gap: 32px; align-items: start; }
  .chat-sidebar { }
  .chat-sidebar-title {
    font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem;
    margin-bottom: 16px; letter-spacing: -0.3px;
  }
  .quick-question {
    padding: 12px 16px; border-radius: 14px;
    background: var(--white); border: 1.5px solid rgba(0,0,0,0.08);
    font-size: 0.82rem; color: var(--black); cursor: pointer;
    margin-bottom: 8px; transition: all 0.2s; text-align: left;
    width: 100%; font-family: 'DM Sans', sans-serif;
  }
  .quick-question:hover { border-color: #8b5cf6; color: #7c3aed; transform: translateX(4px); }
  .chat-role-toggle {
    margin-top: 24px;
  }
  .chat-role-title { font-size: 0.78rem; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; color: var(--grey); margin-bottom: 10px; }
  .role-btn {
    width: 100%; padding: 10px 16px; border-radius: 12px;
    border: 1.5px solid rgba(0,0,0,0.1); background: transparent;
    font-family: 'DM Sans', sans-serif; font-size: 0.82rem;
    cursor: pointer; margin-bottom: 6px; text-align: left;
    transition: all 0.2s; color: var(--grey);
  }
  .role-btn.selected { background: var(--black); color: var(--white); border-color: var(--black); }

  .chat-main { }
  .chat-window {
    height: 400px; overflow-y: auto; border: 1.5px solid rgba(0,0,0,0.08);
    border-radius: 24px; padding: 24px; margin-bottom: 16px;
    display: flex; flex-direction: column; gap: 16px;
    background: var(--white);
    scroll-behavior: smooth;
  }
  .chat-window::-webkit-scrollbar { width: 4px; }
  .chat-window::-webkit-scrollbar-thumb { background: rgba(0,0,0,0.1); border-radius: 4px; }
  .chat-msg {
    max-width: 80%; animation: msgIn 0.3s ease;
  }
  @keyframes msgIn {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .chat-msg.user { align-self: flex-end; }
  .chat-msg.ai { align-self: flex-start; }
  .msg-bubble {
    padding: 14px 18px; border-radius: 18px;
    font-size: 0.88rem; line-height: 1.6;
  }
  .chat-msg.user .msg-bubble {
    background: var(--black); color: var(--white);
    border-bottom-right-radius: 4px;
  }
  .chat-msg.ai .msg-bubble {
    background: var(--light); color: var(--black);
    border-bottom-left-radius: 4px;
  }
  .msg-sender {
    font-size: 0.72rem; font-weight: 700; text-transform: uppercase;
    letter-spacing: 0.8px; margin-bottom: 6px; opacity: 0.5;
  }

  .chat-input-row {
    display: flex; gap: 12px; align-items: center;
  }
  .chat-input {
    flex: 1; padding: 16px 22px; border-radius: 50px;
    border: 2px solid rgba(0,0,0,0.1);
    font-size: 0.9rem; font-family: 'DM Sans', sans-serif;
    background: var(--white); color: var(--black);
    outline: none; transition: border 0.2s;
  }
  .chat-input:focus { border-color: #8b5cf6; }
  .chat-send-btn {
    width: 52px; height: 52px; border-radius: 50%;
    background: linear-gradient(135deg, #7c3aed, #4f46e5);
    color: white; border: none; cursor: pointer;
    font-size: 1.1rem; transition: all 0.2s; flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
  }
  .chat-send-btn:hover { transform: scale(1.08); box-shadow: 0 8px 20px rgba(124,58,237,0.3); }
  .chat-send-btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

  /* ===== AI QUIZ GEN ===== */
  .aiquiz-layout { max-width: 720px; margin: 0 auto; }
  .aiquiz-controls {
    display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; margin-bottom: 32px;
  }
  .aiquiz-ctrl-label {
    font-size: 0.78rem; font-weight: 700; text-transform: uppercase;
    letter-spacing: 1px; color: var(--grey); margin-bottom: 8px;
  }
  .aiquiz-select {
    width: 100%; padding: 12px 16px; border-radius: 14px;
    border: 1.5px solid rgba(0,0,0,0.1);
    font-family: 'DM Sans', sans-serif; font-size: 0.88rem;
    background: var(--white); color: var(--black);
    outline: none; cursor: pointer;
    appearance: none;
  }
  .gen-quiz-btn {
    grid-column: span 3;
    padding: 18px; border-radius: 50px;
    background: linear-gradient(135deg, #7c3aed, #4f46e5);
    color: var(--white); border: none; cursor: pointer;
    font-family: 'DM Sans', sans-serif; font-size: 1rem; font-weight: 600;
    transition: all 0.25s; display: flex; align-items: center; justify-content: center; gap: 10px;
  }
  .gen-quiz-btn:hover { transform: translateY(-2px); box-shadow: 0 12px 32px rgba(124,58,237,0.3); }
  .gen-quiz-btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }

  .ai-quiz-area {
    background: var(--white); border-radius: 28px;
    padding: 40px; border: 1.5px solid rgba(0,0,0,0.08);
    min-height: 200px; box-shadow: 0 4px 20px rgba(0,0,0,0.04);
  }
  .ai-quiz-status {
    text-align: center; padding: 40px; color: var(--grey);
  }
  .ai-q-card { animation: slideIn 0.4s ease; }
  .ai-q-text {
    font-family: 'Syne', sans-serif;
    font-size: 1.2rem; font-weight: 700; margin-bottom: 28px;
    letter-spacing: -0.3px; line-height: 1.4;
  }
  .ai-q-options { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .ai-q-option {
    padding: 16px 20px; border-radius: 14px;
    border: 2px solid rgba(0,0,0,0.1);
    background: var(--white); cursor: pointer;
    font-family: 'DM Sans', sans-serif; font-size: 0.9rem; font-weight: 500;
    transition: all 0.2s; display: flex; align-items: center; gap: 12px; text-align: left;
  }
  .ai-q-option:hover { border-color: #8b5cf6; transform: translateY(-2px); }
  .ai-q-option.correct { background: #E8F5E9; border-color: #2DC653; color: #1a7a35; pointer-events: none; }
  .ai-q-option.wrong { background: #FFEBEE; border-color: #E63946; color: #E63946; pointer-events: none; }
  .ai-q-option.disabled { pointer-events: none; opacity: 0.7; }
  .ai-q-feedback {
    margin-top: 20px; padding: 16px 20px; border-radius: 14px;
    font-size: 0.88rem; line-height: 1.5; display: none; animation: slideIn 0.3s ease;
  }
  .ai-q-feedback.show { display: block; }
  .ai-q-nav {
    display: flex; align-items: center; justify-content: space-between;
    margin-top: 24px;
  }
  .ai-q-counter { font-size: 0.8rem; color: var(--grey); font-weight: 500; }
  .ai-q-next-btn {
    background: var(--black); color: var(--white);
    border: none; border-radius: 50px; padding: 12px 28px;
    cursor: pointer; font-family: 'DM Sans', sans-serif; font-size: 0.88rem;
    font-weight: 500; transition: background 0.2s; display: none;
  }
  .ai-q-next-btn.show { display: block; }
  .ai-q-next-btn:hover { background: #7c3aed; }

  /* Typing indicator */
  .typing-indicator {
    display: flex; gap: 5px; padding: 14px 18px;
    background: var(--light); border-radius: 18px; border-bottom-left-radius: 4px;
    width: fit-content;
  }
  .typing-dot {
    width: 7px; height: 7px; border-radius: 50%;
    background: #9ca3af; animation: typingBounce 1.2s infinite;
  }
  .typing-dot:nth-child(2) { animation-delay: 0.2s; }
  .typing-dot:nth-child(3) { animation-delay: 0.4s; }
  @keyframes typingBounce {
    0%,60%,100% { transform: translateY(0); }
    30% { transform: translateY(-6px); }
  }

  /* ===== RESPONSIVE ===== */
  @media (max-width: 900px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    .hero { grid-template-columns: 1fr; padding: 40px 24px; gap: 48px; }
    .bins-showcase { transform: none; }
    .bins-grid { grid-template-columns: 1fr; }
    .rules-grid { grid-template-columns: 1fr; }
    .do-dont-grid { grid-template-columns: 1fr; }
    .quiz-options { grid-template-columns: 1fr; }
    .guide-header, .finder-section, .rules-hero, .rules-grid, .do-dont-section { padding-left: 24px; padding-right: 24px; }
    .quiz-section { padding: 40px 24px; }
    .quiz-card { padding: 28px; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a class="nav-logo" href="#" onclick="showPage('home')">
    <span class="logo-dot"></span>
    Medi<span>Waste</span>
  </a>
  <ul class="nav-links">
    <li><a href="#" class="active" onclick="showPage('home');setActive(this)">Home</a></li>
    <li><a href="#" onclick="showPage('guide');setActive(this)">Colour Guide</a></li>
    <li><a href="#" onclick="showPage('finder');setActive(this)">Waste Finder</a></li>
    <li><a href="#" onclick="showPage('rules');setActive(this)">Rules & Safety</a></li>
    <li><a href="#" onclick="showPage('quiz');setActive(this)">Take Quiz</a></li>
    <li><a href="#" class="nav-cta" onclick="showPage('ai');setActive(this)">✨ AI Assistant</a></li>
  </ul>
</nav>

<!-- PAGE 1: HOME -->
<div class="page active" id="page-home">
  <div class="hero">
    <div class="hero-left">
      <div class="hero-badge">Healthcare Waste Management</div>
      <h1>Know Your <span class="accent">Waste,</span><br>Protect Lives.</h1>
      <p>A complete guide for healthcare staff and patients on proper biomedical waste segregation. The right waste in the right bin — every time.</p>
      <div class="hero-actions">
        <button class="btn-primary" onclick="showPage('guide')">View Colour Guide →</button>
        <button class="btn-secondary" onclick="showPage('finder')">🔍 Find a Waste Item</button>
      </div>
      <div class="hero-stats">
        <div class="stat-item">
          <div class="stat-number" style="color: var(--red)">4</div>
          <div class="stat-label">Bin Colour Categories</div>
        </div>
        <div class="stat-item">
          <div class="stat-number" style="color: var(--blue)">50+</div>
          <div class="stat-label">Waste Items Covered</div>
        </div>
        <div class="stat-item">
          <div class="stat-number" style="color: var(--green)">100%</div>
          <div class="stat-label">Based on BMW Rules 2016</div>
        </div>
      </div>
    </div>
    <div class="hero-right">
      <div class="bins-showcase">
        <div class="bin-card yellow">
          <span class="bin-icon">🟡</span>
          <div class="bin-label">Yellow Bin</div>
        </div>
        <div class="bin-card red">
          <span class="bin-icon">🔴</span>
          <div class="bin-label">Red Bin</div>
        </div>
        <div class="bin-card blue">
          <span class="bin-icon">🔵</span>
          <div class="bin-label">Blue Bin</div>
        </div>
        <div class="bin-card green">
          <span class="bin-icon">🟢</span>
          <div class="bin-label">Green Bin</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- PAGE 2: GUIDE -->
<div class="page" id="page-guide">
  <div class="guide-header">
    <h2>Biomedical Waste Colour Code Guide</h2>
    <p>As per BMW Management & Handling Rules 2016, India. Colour-coded bins ensure safe handling, transport and disposal of all healthcare waste.</p>
  </div>
  <div class="bins-grid">
    <!-- YELLOW -->
    <div class="bin-section yellow-sec" data-color-label="YELLOW">
      <div class="bin-section-header">
        <div class="bin-icon-large">🗑️</div>
        <div>
          <div class="bin-section-title">Yellow Bin</div>
          <span class="bin-color-tag">Infectious / Hazardous</span>
        </div>
      </div>
      <ul class="waste-list">
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Human anatomical waste<small>Body parts, tissues, organs from surgeries</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Animal anatomical waste<small>Body parts from animal research/testing</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Soiled bandages, dressings<small>Blood-soaked, pus-stained cotton, gauze</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Expired or discarded medicines<small>Including cytotoxic drugs and chemicals</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Microbiology & lab waste<small>Cultures, specimens, blood bags, pathological waste</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Urine bags, drainage bags<small>Used intravenous bags if contaminated</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Placenta, body fluids<small>Blood, secretions and other bodily fluids</small></div></li>
      </ul>
    </div>

    <!-- RED -->
    <div class="bin-section red-sec" data-color-label="RED">
      <div class="bin-section-header">
        <div class="bin-icon-large">🗑️</div>
        <div>
          <div class="bin-section-title">Red Bin</div>
          <span class="bin-color-tag">Recyclable Contaminated</span>
        </div>
      </div>
      <ul class="waste-list">
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Syringes without needles<small>Plastic syringes after use — needle removed</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">IV tubing and sets<small>Contaminated IV lines, blood transfusion sets</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Catheters<small>Urinary catheters, cardiac catheters</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Urine bags (uncontaminated)<small>Drainage bags without pathological waste</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Gloves<small>Used disposable examination gloves</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Contaminated plastic items<small>Any recyclable plastic contaminated with blood/body fluids</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Oxygen masks & tubing<small>Disposable oxygen delivery devices</small></div></li>
      </ul>
    </div>

    <!-- BLUE / WHITE TRANSLUCENT -->
    <div class="bin-section blue-sec" data-color-label="BLUE">
      <div class="bin-section-header">
        <div class="bin-icon-large">📦</div>
        <div>
          <div class="bin-section-title">Blue / White Puncture-Proof Bin</div>
          <span class="bin-color-tag">Sharps & Metallic</span>
        </div>
      </div>
      <ul class="waste-list">
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Needles and syringes with needles<small>Used injection needles, lancets</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Scalpels and blades<small>Surgical blades, disposable scalpels</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Scissors, forceps (disposable)<small>Single-use sharp surgical instruments</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Glass ampoules and vials<small>Broken or unbroken glass medication containers</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Metals from implants<small>Wires, pins from surgical procedures</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Broken glass items<small>Slides, coverslips, glass capillary tubes</small></div></li>
      </ul>
    </div>

    <!-- GREEN / BLACK -->
    <div class="bin-section green-sec" data-color-label="GREEN">
      <div class="bin-section-header">
        <div class="bin-icon-large">♻️</div>
        <div>
          <div class="bin-section-title">Green Bin (Black Bag)</div>
          <span class="bin-color-tag">General / Non-hazardous</span>
        </div>
      </div>
      <ul class="waste-list">
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Food waste<small>Leftover food from patient wards, canteen</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Flowers and plant waste<small>Wilted flowers, leaves from hospital premises</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">General packaging<small>Cardboard boxes, wrappers not contaminated</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Paper waste<small>Administrative paper, newspapers, books</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Disposable dishes<small>Non-contaminated plates, cups from cafeteria</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Dust and sweepings<small>General floor sweepings from non-clinical areas</small></div></li>
        <li class="waste-item"><span class="waste-dot"></span><div class="waste-text">Outer packaging of sterile items<small>Outer covers of gloves, syringes that weren't opened near patient</small></div></li>
      </ul>
    </div>
  </div>
</div>

<!-- PAGE 3: FINDER -->
<div class="page" id="page-finder">
  <div class="finder-section">
    <h2>Waste Item Finder</h2>
    <p>Search for any medical waste item to instantly find which bin it belongs to.</p>

    <div class="search-box">
      <input type="text" class="search-input" id="wasteSearch" placeholder="e.g. needle, bandage, glove, ampoule…" oninput="liveSearch(this.value)" />
      <button class="search-btn" onclick="doSearch()">Search</button>
    </div>

    <div class="search-result-highlight" id="searchResult"></div>

    <div class="categories-tabs">
      <button class="cat-tab active" onclick="filterItems('all', this)">All Items</button>
      <button class="cat-tab" onclick="filterItems('yellow', this)">🟡 Yellow</button>
      <button class="cat-tab" onclick="filterItems('red', this)">🔴 Red</button>
      <button class="cat-tab" onclick="filterItems('blue', this)">🔵 Blue</button>
      <button class="cat-tab" onclick="filterItems('green', this)">🟢 Green</button>
    </div>

    <div class="items-grid" id="itemsGrid"></div>
  </div>
</div>

<!-- PAGE 4: RULES -->
<div class="page" id="page-rules">
  <div class="rules-hero">
    <h2>Safety Rules & Regulations</h2>
    <p>Following these rules protects healthcare workers, patients, and the environment. Non-compliance can lead to serious legal consequences.</p>
  </div>

  <div class="rules-grid">
    <div class="rule-card">
      <div class="rule-number">01</div>
      <span class="rule-icon">🏷️</span>
      <div class="rule-title">Segregate at Source</div>
      <div class="rule-desc">Waste must be segregated at the point of generation. Never mix different categories of waste. Segregation after collection is prohibited and dangerous.</div>
    </div>
    <div class="rule-card featured">
      <div class="rule-number">02</div>
      <span class="rule-icon">🚫</span>
      <div class="rule-title">Never Recap Needles</div>
      <div class="rule-desc">Never recap used needles by hand. Use a one-handed scoop method or a needle remover device. Place immediately in blue puncture-proof container.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">03</div>
      <span class="rule-icon">🧤</span>
      <div class="rule-title">Wear PPE Always</div>
      <div class="rule-desc">Always wear gloves, mask, and appropriate PPE when handling biomedical waste. Change gloves between patients and waste handling tasks.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">04</div>
      <span class="rule-icon">📦</span>
      <div class="rule-title">Fill Bins to 3/4 Only</div>
      <div class="rule-desc">Never overfill waste containers. Bins should be sealed and replaced when 3/4 full to prevent spillage, injuries, and contamination.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">05</div>
      <span class="rule-icon">🏷️</span>
      <div class="rule-title">Label All Containers</div>
      <div class="rule-desc">Every waste bag/container must be labeled with the biohazard symbol, waste category, date, and generating department before dispatch.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">06</div>
      <span class="rule-icon">⏰</span>
      <div class="rule-title">Timely Collection</div>
      <div class="rule-desc">Biomedical waste must be collected within 48 hours. Anatomical and microbiological waste must be disposed of within 24 hours.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">07</div>
      <span class="rule-icon">📋</span>
      <div class="rule-title">Maintain Records</div>
      <div class="rule-desc">Every healthcare facility must maintain a log of waste generated, collected, and disposed. Records must be kept for a minimum of 5 years.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">08</div>
      <span class="rule-icon">🚑</span>
      <div class="rule-title">Report Spills Immediately</div>
      <div class="rule-desc">Any spillage of biomedical waste must be reported immediately to the infection control officer. Follow the spill management protocol at all times.</div>
    </div>
    <div class="rule-card">
      <div class="rule-number">09</div>
      <span class="rule-icon">💉</span>
      <div class="rule-title">Vaccination for Staff</div>
      <div class="rule-desc">All waste handlers must be vaccinated against Hepatitis B and Tetanus. Annual health check-ups are mandatory for all waste management personnel.</div>
    </div>
  </div>

  <div class="do-dont-section">
    <h3>Do's & Don'ts</h3>
    <div class="do-dont-grid">
      <div class="do-card">
        <div class="do-dont-header">
          <span style="font-size:1.5rem">✅</span>
          <h4>Do's</h4>
        </div>
        <ul class="check-list">
          <li>Always wash hands after handling any waste</li>
          <li>Use colour-coded bags as per guidelines</li>
          <li>Wear appropriate PPE before handling waste</li>
          <li>Report needlestick injuries immediately</li>
          <li>Attend regular training on BMW management</li>
          <li>Ensure bins are properly closed after use</li>
          <li>Follow the chain of custody for waste transport</li>
          <li>Keep waste storage area clean and disinfected</li>
        </ul>
      </div>
      <div class="dont-card">
        <div class="do-dont-header">
          <span style="font-size:1.5rem">❌</span>
          <h4>Don'ts</h4>
        </div>
        <ul class="x-list">
          <li>Never mix biomedical waste with general waste</li>
          <li>Don't use hands to press down waste in bins</li>
          <li>Never leave waste bags open or untied</li>
          <li>Don't carry waste bags close to your body</li>
          <li>Never recap needles with both hands</li>
          <li>Don't allow waste to accumulate for over 48 hours</li>
          <li>Never discard sharps in yellow or red bags</li>
          <li>Don't ignore any personal protective equipment</li>
        </ul>
      </div>
    </div>
  </div>
</div>

<!-- PAGE 5: QUIZ -->
<div class="page" id="page-quiz">
  <div class="quiz-section">
    <h2>Test Your Knowledge</h2>
    <p>Select the correct bin colour for each waste item. See how well you know healthcare waste segregation!</p>

    <div class="quiz-progress">
      <div class="quiz-progress-bar">
        <div class="quiz-progress-fill" id="quizProgressFill" style="width:0%"></div>
      </div>
      <div class="quiz-progress-text" id="quizProgressText">Question 0 of 10</div>
    </div>

    <div class="quiz-card" id="quizCard">
      <div id="quizContent"></div>
      <div class="quiz-feedback" id="quizFeedback"></div>
      <button class="quiz-next" id="quizNext" onclick="nextQuestion()">Next Question →</button>
    </div>

    <div class="quiz-result" id="quizResult">
      <div class="quiz-score" id="quizScoreNum"></div>
      <div class="quiz-score-label">out of 10</div>
      <div id="quizScoreMsg" style="font-size:1.1rem; margin:16px 0"></div>
      <button class="quiz-retake" onclick="startQuiz()">Retake Quiz</button>
    </div>
  </div>
</div>

<!-- PAGE 6: AI FEATURES -->
<div class="page" id="page-ai">

  <div class="ai-hero">
    <div class="ai-hero-grid">
      <div>
        <div class="ai-badge">✨ AI-Powered Features</div>
        <h2>Your <span class="ai-glow">AI-Powered</span><br>Waste Assistant</h2>
        <p>Ask anything, classify any waste item, or get a fresh AI-generated quiz — all powered by real intelligence, not just static data.</p>
      </div>
    </div>
  </div>

  <!-- API KEY CARD -->
  <div id="apiKeyBanner" style="padding: 40px 48px; background: #fafaf8; border-bottom: 2px solid #e5e7eb;">
    <div style="max-width: 680px; margin: 0 auto; background: white; border-radius: 24px; border: 2px solid #f59e0b; padding: 36px 40px; box-shadow: 0 4px 24px rgba(245,158,11,0.1);">
      <div style="display:flex; align-items:center; gap:12px; margin-bottom:8px;">
        <span style="font-size:2rem;">🔑</span>
        <div>
          <div style="font-family:'Syne',sans-serif; font-weight:800; font-size:1.2rem; color:#111827; letter-spacing:-0.3px;">Gemini API Key Required</div>
          <div style="font-weight:600;font-size:0.82rem;color:#92400e">Needed to activate all AI features on this page</div>
        </div>
      </div>

      <div style="height:1px; background:#f3f4f6; margin:20px 0;"></div>

      <label style="display:block; font-size:0.78rem; font-weight:700; text-transform:uppercase; letter-spacing:1px; color:#6b7280; margin-bottom:8px;">Your Google Gemini API Key</label>
      <div style="display:flex; gap:10px; align-items:stretch;">
        <input
          type="password"
          id="apiKeyInput"
          placeholder="Paste your Gemini API key here…"
          onkeydown="if(event.key==='Enter') saveApiKey()"
          style="flex:1; padding:14px 20px; border-radius:14px; border:2px solid #e5e7eb; font-family:monospace; font-size:0.88rem; color:#111827; background:#f9fafb; outline:none; transition:border 0.2s;"
          onfocus="this.style.borderColor='#7c3aed'; this.style.background='white';"
          onblur="this.style.borderColor='#e5e7eb'; this.style.background='#f9fafb';"
        />
        <button
          onclick="saveApiKey()"
          style="background: linear-gradient(135deg,#7c3aed,#4f46e5); color:white; border:none; border-radius:14px; padding:14px 28px; cursor:pointer; font-family:'DM Sans',sans-serif; font-size:0.92rem; font-weight:700; white-space:nowrap; transition: all 0.2s;"
          onmouseover="this.style.opacity='0.88'"
          onmouseout="this.style.opacity='1'"
        >Save &amp; Activate ✓</button>
      </div>

      <div id="apiKeyStatus" style="display:none; margin-top:12px; font-size:0.85rem; font-weight:600; padding:10px 16px; border-radius:10px;"></div>

      <div style="margin-top:16px; font-size:0.8rem; color:#9ca3af; line-height:1.6;">
        🔒 Key is stored only in memory — never saved or shared. &nbsp;|&nbsp;
        Get your free key at <a href="https://aistudio.google.com/app/apikey" target="_blank" style="color:#7c3aed; font-weight:600; text-decoration:none;">aistudio.google.com</a>
      </div>
    </div>
  </div>

  <!-- SUCCESS TOAST -->
  <div id="apiKeyToast" style="display:none; position:fixed; bottom:32px; right:32px; z-index:9999; background:#111827; color:white; padding:14px 24px; border-radius:50px; gap:10px; align-items:center; font-family:'DM Sans',sans-serif; font-size:0.9rem; font-weight:500; box-shadow:0 8px 32px rgba(0,0,0,0.2); transition:opacity 0.5s;">
    <span>✅</span> API key saved — AI features are ready!
  </div>

  <!-- TABS -->
  <div class="ai-features-tabs">
    <button class="ai-tab active" onclick="switchAITab('classifier', this)">
      <span class="ai-tab-dot" style="background:#8b5cf6"></span> Smart Classifier
    </button>
    <button class="ai-tab" onclick="switchAITab('chat', this)">
      <span class="ai-tab-dot" style="background:#3b82f6"></span> AI Chat Assistant
    </button>
    <button class="ai-tab" onclick="switchAITab('quizgen', this)">
      <span class="ai-tab-dot" style="background:#10b981"></span> AI Quiz Generator
    </button>
  </div>

  <!-- PANEL 1: CLASSIFIER -->
  <div class="ai-panel active" id="panel-classifier">
    <div class="classifier-layout">
      <div class="classifier-input-wrap">
        <div class="classifier-label">Describe Your Waste Item</div>
        <div class="classifier-sub">Type a description in plain language — the AI will classify it and tell you exactly which bin to use and why.</div>
        <textarea class="classifier-textarea" id="classifierInput" placeholder="e.g. A used cotton swab with blood on it from taking a sample…"></textarea>
        <div class="classifier-examples">
          <div style="font-size:0.75rem; color:var(--grey); margin-bottom:6px; font-weight:600">Quick examples:</div>
          <span class="example-chip" onclick="fillExample(this)">Used needle after injection</span>
          <span class="example-chip" onclick="fillExample(this)">Empty medicine packaging</span>
          <span class="example-chip" onclick="fillExample(this)">Blood-stained gloves</span>
          <span class="example-chip" onclick="fillExample(this)">Leftover food from patient room</span>
          <span class="example-chip" onclick="fillExample(this)">Broken glass slide from lab</span>
          <span class="example-chip" onclick="fillExample(this)">Used IV drip bag and tube</span>
        </div>
        <button class="classify-btn" id="classifyBtn" onclick="classifyWaste()">
          <span id="classifyBtnText">✨ Classify with AI</span>
        </button>
      </div>
      <div class="classifier-result" id="classifierResult">
        <div class="result-placeholder">
          <div class="placeholder-icon">🤖</div>
          <p>Describe a waste item on the left<br>and AI will classify it for you.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- PANEL 2: CHAT -->
  <div class="ai-panel" id="panel-chat">
    <div class="chat-layout">
      <div class="chat-sidebar">
        <div class="chat-sidebar-title">Quick Questions</div>
        <button class="quick-question" onclick="askQuick(this)">What happens to yellow bin waste?</button>
        <button class="quick-question" onclick="askQuick(this)">How should I handle a needlestick injury?</button>
        <button class="quick-question" onclick="askQuick(this)">Can I put gloves in the yellow bin?</button>
        <button class="quick-question" onclick="askQuick(this)">What does BMW Rules 2016 say?</button>
        <button class="quick-question" onclick="askQuick(this)">Which waste requires incineration?</button>
        <button class="quick-question" onclick="askQuick(this)">How often should bins be replaced?</button>
        <button class="quick-question" onclick="askQuick(this)">What is a puncture-proof container?</button>

        <div class="chat-role-toggle">
          <div class="chat-role-title">I am a...</div>
          <button class="role-btn selected" id="role-staff" onclick="setRole('staff', this)">🏥 Healthcare Staff</button>
          <button class="role-btn" id="role-patient" onclick="setRole('patient', this)">🧑 Patient / Visitor</button>
        </div>
      </div>
      <div class="chat-main">
        <div class="chat-window" id="chatWindow">
          <div class="chat-msg ai">
            <div class="msg-sender">MediWaste AI</div>
            <div class="msg-bubble">👋 Hi! I'm your healthcare waste management assistant. Ask me anything about biomedical waste segregation — which bin to use, safety rules, handling procedures, or regulations. How can I help you today?</div>
          </div>
        </div>
        <div class="chat-input-row">
          <input type="text" class="chat-input" id="chatInput" placeholder="Ask about waste segregation…" onkeydown="if(event.key==='Enter') sendChat()" />
          <button class="chat-send-btn" id="chatSendBtn" onclick="sendChat()">➤</button>
        </div>
      </div>
    </div>
  </div>

  <!-- PANEL 3: AI QUIZ GENERATOR -->
  <div class="ai-panel" id="panel-quizgen">
    <div class="aiquiz-layout">
      <div class="aiquiz-controls">
        <div>
          <div class="aiquiz-ctrl-label">Difficulty</div>
          <select class="aiquiz-select" id="qDifficulty">
            <option value="easy">Easy (Basic)</option>
            <option value="medium" selected>Medium</option>
            <option value="hard">Hard (Advanced)</option>
          </select>
        </div>
        <div>
          <div class="aiquiz-ctrl-label">Topic Focus</div>
          <select class="aiquiz-select" id="qTopic">
            <option value="general">All Categories</option>
            <option value="sharps">Sharps & Needles</option>
            <option value="infectious">Infectious Waste</option>
            <option value="plastic">Plastics & Recyclables</option>
            <option value="general waste">General / Green Bin</option>
          </select>
        </div>
        <div>
          <div class="aiquiz-ctrl-label">Role</div>
          <select class="aiquiz-select" id="qRole">
            <option value="healthcare staff">Healthcare Staff</option>
            <option value="nursing student">Nursing Student</option>
            <option value="patient">Patient / Public</option>
          </select>
        </div>
        <button class="gen-quiz-btn" id="genQuizBtn" onclick="generateAIQuiz()">
          <span id="genQuizBtnText">✨ Generate AI Quiz Questions</span>
        </button>
      </div>

      <div class="ai-quiz-area" id="aiQuizArea">
        <div class="ai-quiz-status">
          <div style="font-size:3rem;margin-bottom:12px">🎯</div>
          <div style="font-weight:600; margin-bottom:8px">AI-Generated Quiz</div>
          <div style="font-size:0.88rem; color:var(--grey)">Choose your settings above and click generate. The AI will create fresh, unique questions every time.</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <strong>MediWaste Guide</strong> — Based on Biomedical Waste (Management & Handling) Rules 2016, India.<br>
  <span style="margin-top: 8px; display:block;">For educational purposes. Always follow your institution's specific protocols.</span>
</footer>

<script>
// ===== NAVIGATION =====
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  window.scrollTo(0,0);
  if (id === 'finder') renderItems('all');
  if (id === 'quiz') startQuiz();
}

function setActive(el) {
  document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));
  el.classList.add('active');
}

// ===== WASTE DATA =====
const wasteData = [
  { name: 'Used Needle', bin: 'blue', emoji: '💉', desc: 'Sharps must go in puncture-proof blue container.' },
  { name: 'Surgical Blade / Scalpel', bin: 'blue', emoji: '🔪', desc: 'Sharp metallic item — blue puncture-proof bin.' },
  { name: 'Glass Ampoule', bin: 'blue', emoji: '🧪', desc: 'Broken or unbroken glass ampoules go in blue bin.' },
  { name: 'Syringe (without needle)', bin: 'red', emoji: '🪣', desc: 'Contaminated plastic — red bin for recycling.' },
  { name: 'IV Tubing', bin: 'red', emoji: '🩺', desc: 'Blood-contaminated IV lines — red bin.' },
  { name: 'Disposable Gloves', bin: 'red', emoji: '🧤', desc: 'Used examination gloves — red bin.' },
  { name: 'Blood-soaked Bandage', bin: 'yellow', emoji: '🩹', desc: 'Soiled dressings are infectious waste — yellow bin.' },
  { name: 'Placenta / Body Parts', bin: 'yellow', emoji: '🫀', desc: 'Anatomical waste — yellow bag, incineration.' },
  { name: 'Expired Medicines', bin: 'yellow', emoji: '💊', desc: 'Cytotoxic/hazardous drugs — yellow bin only.' },
  { name: 'Pathological Specimens', bin: 'yellow', emoji: '🧫', desc: 'Lab cultures, blood samples — yellow bin.' },
  { name: 'Urine Collection Bag', bin: 'red', emoji: '🫙', desc: 'If uncontaminated — red bin (contaminated → yellow).' },
  { name: 'Oxygen Mask (disposable)', bin: 'red', emoji: '😷', desc: 'Used disposable masks — red bin.' },
  { name: 'Food Waste', bin: 'green', emoji: '🍱', desc: 'General non-hazardous waste — green bin.' },
  { name: 'Paper / Cardboard', bin: 'green', emoji: '📄', desc: 'Non-contaminated paper/packaging — green bin.' },
  { name: 'Flowers from ward', bin: 'green', emoji: '🌸', desc: 'Plant waste — green bin, general disposal.' },
  { name: 'Catheter', bin: 'red', emoji: '🩻', desc: 'Contaminated plastic device — red bin.' },
  { name: 'Broken Glass Slides', bin: 'blue', emoji: '🔬', desc: 'Sharp glass — blue puncture-proof container.' },
  { name: 'Surgical Suture (used)', bin: 'yellow', emoji: '🧵', desc: 'Contaminated material — yellow bag.' },
  { name: 'Vaccine Vials (used)', bin: 'blue', emoji: '💊', desc: 'Glass vials with needle — blue/puncture-proof bin.' },
  { name: 'Packaging of Sterile Items', bin: 'green', emoji: '📦', desc: 'Outer covers not near patient — green bin.' },
];

const binColors = {
  yellow: { label: 'Yellow Bin', color: '#F5C518', bg: '#FFF8E1', textColor: '#B8860B', emoji: '🗑️' },
  red:    { label: 'Red Bin',    color: '#E63946', bg: '#FFEBEE', textColor: '#E63946', emoji: '🗑️' },
  blue:   { label: 'Blue Bin',   color: '#1D7FDB', bg: '#E3F2FD', textColor: '#1D7FDB', emoji: '📦' },
  green:  { label: 'Green Bin',  color: '#2DC653', bg: '#E8F5E9', textColor: '#1a7a35', emoji: '♻️' },
};

function renderItems(filter) {
  const grid = document.getElementById('itemsGrid');
  const items = filter === 'all' ? wasteData : wasteData.filter(w => w.bin === filter);
  grid.innerHTML = items.map(w => {
    const b = binColors[w.bin];
    return `<div class="item-card">
      <div class="item-color-strip" style="background:${b.color}"></div>
      <div class="item-info">
        <div class="item-name">${w.emoji} ${w.name}</div>
        <span class="item-bin" style="background:${b.bg};color:${b.textColor};border:1px solid ${b.color}">${b.label}</span>
        <div class="item-desc">${w.desc}</div>
      </div>
    </div>`;
  }).join('');
}

function filterItems(color, btn) {
  document.querySelectorAll('.cat-tab').forEach(t => t.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('searchResult').classList.remove('show');
  renderItems(color);
}

function liveSearch(val) {
  if (!val.trim()) {
    document.getElementById('searchResult').classList.remove('show');
    return;
  }
  const found = wasteData.find(w => w.name.toLowerCase().includes(val.toLowerCase()));
  showSearchResult(found, val);
}

function doSearch() {
  const val = document.getElementById('wasteSearch').value;
  const found = wasteData.find(w => w.name.toLowerCase().includes(val.toLowerCase()));
  showSearchResult(found, val);
}

function showSearchResult(found, val) {
  const el = document.getElementById('searchResult');
  if (found) {
    const b = binColors[found.bin];
    el.className = 'search-result-highlight show';
    el.style.background = b.bg;
    el.style.borderColor = b.color;
    el.innerHTML = `
      <div class="result-bin-visual" style="background:${b.color}">
        <span class="bin-emoji">${b.emoji}</span>
        <span class="result-bin-name" style="color:white">${b.label}</span>
      </div>
      <div class="result-info">
        <h3>${found.emoji} ${found.name}</h3>
        <p style="color:${b.textColor}"><strong>→ ${b.label}</strong></p>
        <p style="margin-top:8px">${found.desc}</p>
      </div>`;
  } else if (val.trim()) {
    el.className = 'search-result-highlight show';
    el.style.background = '#F3F4F6'; el.style.borderColor = '#d1d5db';
    el.innerHTML = `<div class="result-info"><h3>❓ Item not found</h3><p>Try searching: needle, bandage, glove, ampoule, catheter...</p></div>`;
  }
}

// ===== QUIZ =====
const quizQuestions = [
  { item: 'Used syringe needle', emoji: '💉', correct: 'blue', explain: 'Needles are sharps and must go in the blue puncture-proof container.' },
  { item: 'Blood-soaked cotton', emoji: '🩹', correct: 'yellow', explain: 'Soiled, contaminated dressings are infectious waste — yellow bin.' },
  { item: 'Syringe without needle', emoji: '🪣', correct: 'red', explain: 'Contaminated plastic items go in the red bin for treatment and recycling.' },
  { item: 'Leftover food from ward', emoji: '🍱', correct: 'green', explain: 'Food waste is general non-hazardous waste — green bin.' },
  { item: 'Expired medicines', emoji: '💊', correct: 'yellow', explain: 'Expired/cytotoxic drugs are hazardous — yellow bin.' },
  { item: 'Surgical scalpel blade', emoji: '🔪', correct: 'blue', explain: 'All sharps go in the puncture-proof blue container.' },
  { item: 'Used gloves (examination)', emoji: '🧤', correct: 'red', explain: 'Contaminated plastic gloves — red bin for recycling after treatment.' },
  { item: 'Glass ampoule', emoji: '🧪', correct: 'blue', explain: 'Glass is a sharp/fragile — blue puncture-proof bin.' },
  { item: 'Placenta from delivery', emoji: '🫀', correct: 'yellow', explain: 'Anatomical waste must go in yellow bag for incineration.' },
  { item: 'Outer packaging of gloves', emoji: '📦', correct: 'green', explain: 'Uncontaminated outer packaging is general waste — green bin.' },
];

let currentQ = 0, score = 0, answered = false;

function startQuiz() {
  currentQ = 0; score = 0; answered = false;
  document.getElementById('quizResult').classList.remove('show');
  document.getElementById('quizCard').style.display = 'block';
  renderQuestion();
}

function renderQuestion() {
  answered = false;
  const q = quizQuestions[currentQ];
  const pct = (currentQ / quizQuestions.length) * 100;
  document.getElementById('quizProgressFill').style.width = pct + '%';
  document.getElementById('quizProgressText').textContent = `Question ${currentQ + 1} of ${quizQuestions.length}`;
  document.getElementById('quizFeedback').className = 'quiz-feedback';
  document.getElementById('quizNext').className = 'quiz-next';

  const opts = ['yellow','red','blue','green'];
  document.getElementById('quizContent').innerHTML = `
    <div class="quiz-question">
      <span class="quiz-item-name">${q.emoji}</span>
      Which bin does <strong>"${q.item}"</strong> go into?
    </div>
    <div class="quiz-options">
      ${opts.map(c => {
        const b = binColors[c];
        return `<button class="quiz-option" onclick="selectAnswer('${c}', this)" data-bin="${c}">
          <span class="opt-color" style="background:${b.color}"></span>
          ${b.emoji} ${b.label}
        </button>`;
      }).join('')}
    </div>`;
}

function selectAnswer(chosen, btn) {
  if (answered) return;
  answered = true;
  const q = quizQuestions[currentQ];
  const isCorrect = chosen === q.correct;
  if (isCorrect) score++;

  document.querySelectorAll('.quiz-option').forEach(opt => {
    if (opt.dataset.bin === q.correct) opt.classList.add('correct');
    else if (opt.dataset.bin === chosen && !isCorrect) opt.classList.add('wrong');
    opt.style.pointerEvents = 'none';
  });

  const fb = document.getElementById('quizFeedback');
  fb.className = `quiz-feedback show ${isCorrect ? 'correct-fb' : 'wrong-fb'}`;
  fb.innerHTML = `<strong>${isCorrect ? '✅ Correct!' : '❌ Incorrect.'}</strong> ${q.explain}`;

  const nxt = document.getElementById('quizNext');
  nxt.className = 'quiz-next show';
  nxt.textContent = currentQ < quizQuestions.length - 1 ? 'Next Question →' : 'See Results';
}

function nextQuestion() {
  currentQ++;
  if (currentQ >= quizQuestions.length) {
    showResult();
  } else {
    renderQuestion();
  }
}

function showResult() {
  document.getElementById('quizCard').style.display = 'none';
  document.getElementById('quizProgressFill').style.width = '100%';
  document.getElementById('quizProgressText').textContent = 'Quiz Complete!';
  const res = document.getElementById('quizResult');
  res.classList.add('show');
  document.getElementById('quizScoreNum').textContent = score;
  const msg = score >= 9 ? '🏆 Excellent! You\'re a waste management expert!' :
               score >= 7 ? '👍 Great job! A little more practice and you\'ll ace it!' :
               score >= 5 ? '📚 Good effort! Review the colour guide and try again.' :
               '💡 Keep learning! Check the Colour Guide and try the quiz again.';
  document.getElementById('quizScoreMsg').textContent = msg;
  document.getElementById('quizScoreNum').style.color =
    score >= 8 ? '#2DC653' : score >= 5 ? '#F5C518' : '#E63946';
}

// Init
renderItems('all');

// ===== AI TAB SWITCHING =====
function switchAITab(tab, btn) {
  document.querySelectorAll('.ai-tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.ai-panel').forEach(p => p.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('panel-' + tab).classList.add('active');
}

// ===== API KEY MANAGEMENT =====
let geminiApiKey = '';

function saveApiKey() {
  const val = document.getElementById('apiKeyInput').value.trim();
  const status = document.getElementById('apiKeyStatus');
  if (val.length < 20) {
    status.style.display = 'block';
    status.style.background = '#FFEBEE';
    status.style.color = '#E63946';
    status.textContent = '❌ Invalid key — paste your full Gemini API key.';
    return;
  }
  geminiApiKey = val;
  // Hide the entire banner — no trace of the key visible
  document.getElementById('apiKeyBanner').style.display = 'none';
  // Show a small success toast
  const toast = document.getElementById('apiKeyToast');
  toast.style.display = 'flex';
  setTimeout(() => { toast.style.opacity = '0'; setTimeout(() => toast.style.display = 'none', 500); }, 3000);
}

// ===== GEMINI API CALL =====
async function callClaude(systemPrompt, userMessage) {
  if (!geminiApiKey) {
    throw new Error('Please enter your Gemini API key in the banner above to use AI features.');
  }
  const response = await fetch(
    `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${geminiApiKey}`,
    {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        contents: [{ parts: [{ text: userMessage }] }],
        systemInstruction: { parts: [{ text: systemPrompt }] },
        generationConfig: { maxOutputTokens: 1000, temperature: 0.7 }
      })
    }
  );
  const data = await response.json();
  if (data.error) throw new Error(data.error.message);
  return data.candidates[0].content.parts[0].text;
}

// ===== CLASSIFIER =====
const binMeta = {
  yellow: { color: '#F5C518', bg: '#FFF8E1', textColor: '#B8860B', label: 'Yellow Bin', type: 'Infectious / Hazardous', emoji: '🗑️' },
  red:    { color: '#E63946', bg: '#FFEBEE', textColor: '#E63946', label: 'Red Bin',    type: 'Contaminated Recyclable', emoji: '🗑️' },
  blue:   { color: '#1D7FDB', bg: '#E3F2FD', textColor: '#1D7FDB', label: 'Blue Bin',   type: 'Sharps & Metallic', emoji: '📦' },
  green:  { color: '#2DC653', bg: '#E8F5E9', textColor: '#1a7a35', label: 'Green Bin',  type: 'General / Non-hazardous', emoji: '♻️' },
};

function fillExample(chip) {
  document.getElementById('classifierInput').value = chip.textContent;
}

async function classifyWaste() {
  const input = document.getElementById('classifierInput').value.trim();
  if (!input) return;

  const btn = document.getElementById('classifyBtn');
  const btnText = document.getElementById('classifyBtnText');
  btn.disabled = true;
  btnText.innerHTML = '<span style="display:flex;align-items:center;gap:8px"><span style="width:16px;height:16px;border:2px solid rgba(255,255,255,0.4);border-top-color:white;border-radius:50%;animation:spin 0.8s linear infinite;display:inline-block"></span> Classifying…</span>';

  const result = document.getElementById('classifierResult');
  result.className = 'classifier-result';
  result.innerHTML = `<div class="ai-loader"><div class="ai-loader-dots"><span></span><span></span><span></span></div><div>AI is analysing your waste item…</div></div>`;

  const systemPrompt = `You are a biomedical waste classification expert based on India's BMW Management & Handling Rules 2016. 
Classify waste items into exactly one of these four bins:
- YELLOW: Infectious/hazardous waste (anatomical, soiled dressings, expired medicines, lab waste, body fluids)
- RED: Contaminated recyclable plastic (syringes without needles, IV tubes, gloves, catheters, oxygen masks)
- BLUE: Sharps and glass (needles, scalpels, blades, glass ampoules, broken glass)
- GREEN: General non-hazardous waste (food, paper, uncontaminated packaging, flowers)

Respond ONLY with valid JSON in this exact format:
{
  "bin": "yellow|red|blue|green",
  "itemName": "short name for the item",
  "reason": "2-3 sentence explanation of why this bin",
  "steps": ["Step 1 action", "Step 2 action", "Step 3 action"],
  "warning": "any safety warning or null"
}`;

  try {
    const raw = await callClaude(systemPrompt, input);
    const clean = raw.replace(/```json|```/g, '').trim();
    const parsed = JSON.parse(clean);
    const b = binMeta[parsed.bin] || binMeta['green'];

    result.className = 'classifier-result loaded';
    result.style.borderColor = b.color;
    result.innerHTML = `
      <div class="result-bin-card">
        <div class="result-bin-header">
          <div class="result-bin-circle" style="background:${b.bg};border:2px solid ${b.color}">
            <span style="font-size:2rem">${b.emoji}</span>
          </div>
          <div>
            <div class="result-bin-title" style="color:${b.textColor}">${b.label}</div>
            <div class="result-bin-subtitle">${b.type}</div>
            <div style="margin-top:6px;font-weight:600;font-size:0.95rem">${parsed.itemName}</div>
          </div>
        </div>
        <div class="result-reason" style="border-left-color:${b.color};background:${b.bg}">${parsed.reason}</div>
        <div class="result-steps">
          <div class="result-steps-title">Disposal Steps</div>
          ${parsed.steps.map((s,i) => `<div class="result-step">
            <span class="step-num" style="background:${b.color}">${i+1}</span>
            <span>${s}</span>
          </div>`).join('')}
        </div>
        ${parsed.warning ? `<div style="margin-top:16px;padding:12px 16px;background:#FFF8E1;border:1px solid #F5C518;border-radius:12px;font-size:0.85rem;color:#92400e">⚠️ ${parsed.warning}</div>` : ''}
      </div>`;
  } catch (e) {
    result.className = 'classifier-result loaded';
    result.innerHTML = `<div style="color:var(--red);text-align:center;padding:20px"><div style="font-size:2rem;margin-bottom:8px">⚠️</div><div>${e.message || 'Classification failed. Please try again.'}</div></div>`;
  }

  btn.disabled = false;
  btnText.textContent = '✨ Classify with AI';
}

// ===== CHAT ASSISTANT =====
let chatRole = 'healthcare staff';
let chatHistory = [];

function setRole(role, btn) {
  chatRole = role === 'staff' ? 'healthcare staff' : 'patient or visitor';
  document.querySelectorAll('.role-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
}

function askQuick(btn) {
  document.getElementById('chatInput').value = btn.textContent;
  sendChat();
}

function appendMessage(role, text) {
  const win = document.getElementById('chatWindow');
  const msgDiv = document.createElement('div');
  msgDiv.className = `chat-msg ${role}`;
  msgDiv.innerHTML = `
    <div class="msg-sender">${role === 'user' ? 'You' : 'MediWaste AI'}</div>
    <div class="msg-bubble">${text.replace(/\n/g, '<br>')}</div>`;
  win.appendChild(msgDiv);
  win.scrollTop = win.scrollHeight;
  return msgDiv;
}

function showTyping() {
  const win = document.getElementById('chatWindow');
  const div = document.createElement('div');
  div.className = 'chat-msg ai'; div.id = 'typingIndicator';
  div.innerHTML = `<div class="msg-sender">MediWaste AI</div><div class="typing-indicator"><span class="typing-dot"></span><span class="typing-dot"></span><span class="typing-dot"></span></div>`;
  win.appendChild(div);
  win.scrollTop = win.scrollHeight;
}

function hideTyping() {
  const t = document.getElementById('typingIndicator');
  if (t) t.remove();
}

async function sendChat() {
  const input = document.getElementById('chatInput');
  const msg = input.value.trim();
  if (!msg) return;
  if (!geminiApiKey) {
    appendMessage('ai', '⚠️ Please enter your Gemini API key in the banner at the top to use the chat.');
    return;
  }
  input.value = '';

  const sendBtn = document.getElementById('chatSendBtn');
  sendBtn.disabled = true;

  chatHistory.push({ role: 'user', content: msg });
  appendMessage('user', msg);
  showTyping();

  const systemPrompt = `You are MediWaste AI, a friendly and expert healthcare waste management assistant. 
You are helping a ${chatRole} understand biomedical waste segregation based on India's BMW Management & Handling Rules 2016.
Be concise, clear, and practical. Use simple language for patients, more technical for staff.
Key bins: Yellow (infectious/hazardous), Red (contaminated recyclable plastic), Blue (sharps/glass), Green (general waste).
Keep responses under 150 words. Use bullet points only when listing items. Be helpful and reassuring.`;

  try {
    const history = chatHistory.slice(-8);
    // Build Gemini contents array (alternating user/model)
    const contents = history.map(m => ({
      role: m.role === 'assistant' ? 'model' : 'user',
      parts: [{ text: m.content }]
    }));
    const response = await fetch(
      `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${geminiApiKey}`,
      {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          contents: contents,
          systemInstruction: { parts: [{ text: systemPrompt }] },
          generationConfig: { maxOutputTokens: 1000, temperature: 0.7 }
        })
      }
    );
    const data = await response.json();
    if (data.error) throw new Error(data.error.message);
    const reply = data.candidates[0].content.parts[0].text;
    chatHistory.push({ role: 'assistant', content: reply });
    hideTyping();
    appendMessage('ai', reply);
  } catch (e) {
    hideTyping();
    appendMessage('ai', '⚠️ Connection error. Please check your internet and try again.');
  }

  sendBtn.disabled = false;
  input.focus();
}

// ===== AI QUIZ GENERATOR =====
let aiQuizData = null;
let aiQuizIndex = 0;
let aiQuizScore = 0;
let aiQuizAnswered = false;

async function generateAIQuiz() {
  const difficulty = document.getElementById('qDifficulty').value;
  const topic = document.getElementById('qTopic').value;
  const role = document.getElementById('qRole').value;
  const btn = document.getElementById('genQuizBtn');
  const btnText = document.getElementById('genQuizBtnText');

  btn.disabled = true;
  btnText.innerHTML = '<span style="display:flex;align-items:center;gap:8px"><span style="width:16px;height:16px;border:2px solid rgba(255,255,255,0.4);border-top-color:white;border-radius:50%;animation:spin 0.8s linear infinite;display:inline-block"></span> AI is generating your quiz…</span>';

  const area = document.getElementById('aiQuizArea');
  area.innerHTML = `<div class="ai-quiz-status"><div class="ai-loader"><div class="ai-loader-dots"><span></span><span></span><span></span></div><div>Creating ${difficulty} questions about ${topic}…</div></div></div>`;

  const systemPrompt = `You are a biomedical waste management quiz creator. Generate exactly 5 multiple-choice quiz questions about healthcare waste segregation (India BMW Rules 2016).
Difficulty: ${difficulty}. Topic focus: ${topic}. Target audience: ${role}.
Respond ONLY with a valid JSON array. No markdown, no explanation. Format:
[
  {
    "question": "Question text here?",
    "options": ["Option A", "Option B", "Option C", "Option D"],
    "correct": 0,
    "explanation": "Why this answer is correct (1-2 sentences)"
  }
]
The "correct" field is the 0-based index of the correct option. Make questions practical and relevant. Vary question types (which bin, what to do, regulations, safety).`;

  try {
    const raw = await callClaude(systemPrompt, `Generate 5 ${difficulty} quiz questions about ${topic} for ${role}`);
    const clean = raw.replace(/```json|```/g, '').trim();
    aiQuizData = JSON.parse(clean);
    aiQuizIndex = 0;
    aiQuizScore = 0;
    aiQuizAnswered = false;
    renderAIQuestion();
  } catch (e) {
    area.innerHTML = `<div class="ai-quiz-status"><div style="color:var(--red);font-size:2rem">⚠️</div><div style="margin-top:8px">${e.message || 'Failed to generate quiz. Try again.'}</div></div>`;
  }

  btn.disabled = false;
  btnText.textContent = '✨ Generate AI Quiz Questions';
}

function renderAIQuestion() {
  const area = document.getElementById('aiQuizArea');
  if (!aiQuizData || aiQuizIndex >= aiQuizData.length) {
    const pct = Math.round((aiQuizScore / aiQuizData.length) * 100);
    const color = pct >= 80 ? '#2DC653' : pct >= 60 ? '#F5C518' : '#E63946';
    area.innerHTML = `
      <div style="text-align:center;padding:20px">
        <div style="font-size:5rem;font-family:Syne,sans-serif;font-weight:800;color:${color}">${aiQuizScore}/${aiQuizData.length}</div>
        <div style="color:var(--grey);margin-bottom:24px">${pct >= 80 ? '🏆 Outstanding!' : pct >= 60 ? '👍 Good job!' : '📚 Keep practising!'}</div>
        <button onclick="generateAIQuiz()" style="background:var(--black);color:white;border:none;border-radius:50px;padding:14px 32px;cursor:pointer;font-family:DM Sans,sans-serif;font-size:0.9rem;font-weight:500">Generate New Quiz ✨</button>
      </div>`;
    return;
  }

  aiQuizAnswered = false;
  const q = aiQuizData[aiQuizIndex];
  const optLetters = ['A', 'B', 'C', 'D'];
  area.innerHTML = `
    <div class="ai-q-card">
      <div class="ai-q-nav">
        <span class="ai-q-counter">Question ${aiQuizIndex + 1} of ${aiQuizData.length} • Score: ${aiQuizScore}</span>
      </div>
      <div class="ai-q-text" style="margin-top:16px">${q.question}</div>
      <div class="ai-q-options">
        ${q.options.map((opt, i) => `
          <button class="ai-q-option" onclick="answerAIQ(${i})" data-idx="${i}">
            <span style="width:26px;height:26px;border-radius:50%;background:var(--light);display:flex;align-items:center;justify-content:center;font-size:0.7rem;font-weight:700;flex-shrink:0">${optLetters[i]}</span>
            ${opt}
          </button>`).join('')}
      </div>
      <div class="ai-q-feedback" id="aiQFeedback"></div>
      <div class="ai-q-nav" style="margin-top:20px">
        <span></span>
        <button class="ai-q-next-btn" id="aiQNext" onclick="nextAIQ()">
          ${aiQuizIndex < aiQuizData.length - 1 ? 'Next Question →' : 'See Results'}
        </button>
      </div>
    </div>`;
}

function answerAIQ(idx) {
  if (aiQuizAnswered) return;
  aiQuizAnswered = true;
  const q = aiQuizData[aiQuizIndex];
  const isCorrect = idx === q.correct;
  if (isCorrect) aiQuizScore++;

  document.querySelectorAll('.ai-q-option').forEach((btn, i) => {
    btn.classList.add('disabled');
    if (i === q.correct) btn.classList.add('correct');
    else if (i === idx && !isCorrect) btn.classList.add('wrong');
  });

  const fb = document.getElementById('aiQFeedback');
  fb.className = `ai-q-feedback show ${isCorrect ? 'correct-fb' : 'wrong-fb'}`;
  fb.style.background = isCorrect ? '#E8F5E9' : '#FFEBEE';
  fb.style.border = `1.5px solid ${isCorrect ? '#2DC653' : '#E63946'}`;
  fb.style.color = isCorrect ? '#1a7a35' : '#E63946';
  fb.innerHTML = `<strong>${isCorrect ? '✅ Correct!' : '❌ Wrong.'}</strong> ${q.explanation}`;

  document.getElementById('aiQNext').classList.add('show');
}

function nextAIQ() {
  aiQuizIndex++;
  renderAIQuestion();
}

// Add spin animation
const style = document.createElement('style');
style.textContent = '@keyframes spin { to { transform: rotate(360deg); } }';
document.head.appendChild(style);
</script>
</body>
</html>
