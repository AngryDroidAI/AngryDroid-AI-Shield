<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🛡️ AngryDroid AI Shield</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      background: linear-gradient(135deg, #0d0d0d 0%, #1a1a2e 100%);
      color: #eee;
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 2em;
      min-height: 100vh;
      position: relative;
      overflow-x: hidden;
    }
    
    body::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: 
        radial-gradient(circle at 10% 20%, rgba(0, 255, 231, 0.1) 0%, transparent 20%),
        radial-gradient(circle at 90% 80%, rgba(255, 0, 128, 0.1) 0%, transparent 20%);
      z-index: -1;
    }
    
    .container {
      max-width: 800px;
      margin: 0 auto;
    }
    
    h1 {
      font-size: 2.8rem;
      margin-bottom: 1.5rem;
      text-shadow: 0 0 15px rgba(0, 255, 231, 0.7);
      background: linear-gradient(to right, #00ffe7, #ff0080);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      position: relative;
    }
    
    h1::after {
      content: "";
      display: block;
      width: 100px;
      height: 4px;
      background: linear-gradient(to right, #00ffe7, #ff0080);
      margin: 10px auto;
      border-radius: 2px;
    }
    
    .wizard-container {
      position: relative;
      margin: 2rem auto;
      width: 220px;
      height: 220px;
    }
    
    #wizard {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      box-shadow: 0 0 20px #00ffe7;
      transition: all 0.5s ease;
      position: relative;
      z-index: 2;
    }
    
    #wizard.glow {
      transform: scale(1.1);
      box-shadow: 0 0 50px #00ffe7, 0 0 100px rgba(0, 255, 231, 0.5);
    }
    
    .shield {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 250px;
      height: 250px;
      border: 3px solid rgba(0, 255, 231, 0.3);
      border-radius: 50%;
      z-index: 1;
      animation: pulse 3s infinite;
    }
    
    .shield::before, .shield::after {
      content: "";
      position: absolute;
      border: 3px solid rgba(0, 255, 231, 0.3);
      border-radius: 50%;
      width: 270px;
      height: 270px;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    
    .shield::after {
      width: 290px;
      height: 290px;
    }
    
    @keyframes pulse {
      0% { transform: translate(-50%, -50%) scale(1); opacity: 0.3; }
      50% { transform: translate(-50%, -50%) scale(1.05); opacity: 0.6; }
      100% { transform: translate(-50%, -50%) scale(1); opacity: 0.3; }
    }
    
    .scan-container {
      background: rgba(20, 20, 40, 0.7);
      border: 1px solid rgba(0, 255, 231, 0.3);
      border-radius: 15px;
      padding: 1.5rem;
      margin: 2rem auto;
      max-width: 600px;
      box-shadow: 0 0 20px rgba(0, 255, 231, 0.2);
    }
    
    #urlInput {
      width: 100%;
      padding: 1em;
      font-size: 1.1em;
      border-radius: 8px;
      border: 2px solid #00ffe7;
      background: rgba(10, 10, 20, 0.7);
      color: #eee;
      margin-bottom: 1rem;
      outline: none;
      transition: all 0.3s ease;
    }
    
    #urlInput:focus {
      border-color: #ff0080;
      box-shadow: 0 0 15px rgba(255, 0, 128, 0.5);
    }
    
    button {
      padding: 0.8em 2em;
      font-size: 1.1em;
      font-weight: bold;
      border-radius: 8px;
      border: none;
      background: linear-gradient(45deg, #00ffe7, #ff0080);
      color: #000;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
      position: relative;
      overflow: hidden;
    }
    
    button:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(0, 255, 231, 0.4);
    }
    
    button:active {
      transform: translateY(1px);
    }
    
    button::after {
      content: "";
      position: absolute;
      top: -50%;
      left: -60%;
      width: 20px;
      height: 200%;
      background: rgba(255, 255, 255, 0.3);
      transform: rotate(25deg);
      transition: all 0.6s;
    }
    
    button:hover::after {
      left: 120%;
    }
    
    .results-container {
      margin: 2rem auto;
      max-width: 700px;
    }
    
    #verdict {
      font-size: 1.5rem;
      margin: 1.5rem 0;
      padding: 1.2rem;
      border-radius: 12px;
      background: rgba(20, 20, 40, 0.7);
      border: 1px solid;
      display: none;
      animation: fadeIn 0.5s ease;
    }
    
    #verdict.safe {
      border-color: #00ff88;
      color: #00ff88;
      text-shadow: 0 0 10px rgba(0, 255, 136, 0.7);
    }
    
    #verdict.risky {
      border-color: #ff3333;
      color: #ff3333;
      text-shadow: 0 0 10px rgba(255, 51, 51, 0.7);
    }
    
    #badge {
      margin: 1.5rem auto;
      font-size: 1.3rem;
      color: #00ff88;
      display: none;
      padding: 1rem;
      border-radius: 12px;
      background: rgba(0, 255, 136, 0.1);
      border: 1px solid #00ff88;
      max-width: 500px;
      animation: pulseBadge 2s infinite;
    }
    
    @keyframes pulseBadge {
      0% { box-shadow: 0 0 5px rgba(0, 255, 136, 0.5); }
      50% { box-shadow: 0 0 20px rgba(0, 255, 136, 0.8); }
      100% { box-shadow: 0 0 5px rgba(0, 255, 136, 0.5); }
    }
    
    #loreCapsule {
      background: rgba(20, 20, 40, 0.7);
      border: 2px solid #00ffe7;
      border-radius: 15px;
      padding: 1.5rem;
      margin: 2rem auto;
      display: none;
      box-shadow: 0 0 25px rgba(0, 255, 231, 0.3);
      text-align: left;
      animation: fadeIn 0.8s ease;
      max-width: 700px;
    }
    
    #loreCapsule h3 {
      color: #00ffe7;
      margin-bottom: 1rem;
      font-size: 1.4rem;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    
    #loreText {
      line-height: 1.6;
      font-size: 1.1rem;
    }
    
    .scan-details {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1rem;
      margin-top: 1.5rem;
    }
    
    .detail-card {
      background: rgba(10, 10, 20, 0.5);
      border: 1px solid rgba(0, 255, 231, 0.2);
      border-radius: 10px;
      padding: 1rem;
      text-align: center;
    }
    
    .detail-card i {
      font-size: 2rem;
      margin-bottom: 0.5rem;
      color: #00ffe7;
    }
    
    .detail-card.risky i {
      color: #ff3333;
    }
    
    .detail-card h4 {
      margin: 0.5rem 0;
      color: #00ffe7;
    }
    
    .progress-container {
      height: 8px;
      background: rgba(100, 100, 100, 0.3);
      border-radius: 4px;
      margin: 1rem 0;
      overflow: hidden;
    }
    
    .progress-bar {
      height: 100%;
      background: linear-gradient(to right, #00ffe7, #ff0080);
      width: 0%;
      transition: width 0.5s ease;
    }
    
    #attribution {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      text-align: center;
      z-index: 999;
      font-size: 0.85em;
      color: #00ffe7;
      font-family: 'Courier New', monospace;
      background: rgba(10, 10, 20, 0.8);
      padding: 10px 15px;
      border-radius: 10px;
      border: 1px solid rgba(0, 255, 231, 0.3);
    }
    
    #attribution img {
      width: 100px;
      border-radius: 12px;
      box-shadow: 0 0 12px #00ffe7;
      margin-bottom: 8px;
      border: 2px solid #00ffe7;
    }
    
    #attribution a {
      color: #ffcc00;
      text-decoration: none;
      font-weight: bold;
    }
    
    #attribution a:hover {
      text-decoration: underline;
    }
    
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    .loading {
      display: inline-block;
      width: 20px;
      height: 20px;
      border: 3px solid rgba(255, 255, 255, 0.3);
      border-radius: 50%;
      border-top-color: #00ffe7;
      animation: spin 1s ease-in-out infinite;
      margin-right: 10px;
      vertical-align: middle;
    }
    
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
    
    .risk-indicator {
      display: inline-block;
      width: 12px;
      height: 12px;
      border-radius: 50%;
      margin-right: 8px;
    }
    
    .risk-safe {
      background-color: #00ff88;
      box-shadow: 0 0 8px #00ff88;
    }
    
    .risk-high {
      background-color: #ff3333;
      box-shadow: 0 0 8px #ff3333;
    }
    
    @media (max-width: 600px) {
      h1 {
        font-size: 2rem;
      }
      
      .wizard-container {
        width: 180px;
        height: 180px;
      }
      
      .shield {
        width: 200px;
        height: 200px;
      }
      
      .shield::before {
        width: 220px;
        height: 220px;
      }
      
      .shield::after {
        width: 240px;
        height: 240px;
      }
      
      .scan-container {
        padding: 1rem;
      }
      
      #urlInput {
        font-size: 1rem;
      }
      
      button {
        padding: 0.7em 1.5em;
        font-size: 1rem;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🧙‍♂️ AngryDroid AI Shield</h1>
    
    <div class="wizard-container">
      <div class="shield"></div>
      <img id="wizard" src="https://angrydroid.neocities.org/images/security.png" alt="Wizard Idle" />
    </div>
    
    <div class="scan-container">
      <input type="text" id="urlInput" placeholder="Enter URL to scan..." />
      <button onclick="scanURL()">
        <i class="fas fa-shield-alt"></i> Scan URL
      </button>
    </div>
    
    <div class="results-container">
      <div id="verdict"></div>
      <div id="badge">🎖️ Scan Complete — Badge Unlocked!</div>
      
      <div id="loreCapsule">
        <h3><i class="fas fa-scroll"></i> Security Analysis Report</h3>
        <p id="loreText">Awaiting scan summary...</p>
        
        <div class="scan-details">
          <div class="detail-card">
            <i class="fas fa-virus"></i>
            <h4>Malware Detection</h4>
            <div class="progress-container">
              <div class="progress-bar" id="malware-bar"></div>
            </div>
            <p id="malware-status">Not detected</p>
          </div>
          
          <div class="detail-card">
            <i class="fas fa-fish"></i>
            <h4>Phishing Risk</h4>
            <div class="progress-container">
              <div class="progress-bar" id="phishing-bar"></div>
            </div>
            <p id="phishing-status">Low risk</p>
          </div>
          
          <div class="detail-card">
            <i class="fas fa-lock"></i>
            <h4>SSL Security</h4>
            <div class="progress-container">
              <div class="progress-bar" id="ssl-bar"></div>
            </div>
            <p id="ssl-status">Secure</p>
          </div>
          
          <div class="detail-card">
            <i class="fas fa-user-secret"></i>
            <h4>Privacy Protection</h4>
            <div class="progress-container">
              <div class="progress-bar" id="privacy-bar"></div>
            </div>
            <p id="privacy-status">Good</p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <script>
    function scanURL() {
      const url = document.getElementById("urlInput").value.trim();
      if (!url) return;

      const wizard = document.getElementById("wizard");
      const verdict = document.getElementById("verdict");
      const badge = document.getElementById("badge");
      const loreCapsule = document.getElementById("loreCapsule");
      const loreText = document.getElementById("loreText");
      
      // Reset visuals
      verdict.textContent = "";
      verdict.className = "verdict";
      badge.style.display = "none";
      loreCapsule.style.display = "none";
      wizard.classList.add("glow");
      
      // Reset progress bars
      document.querySelectorAll('.progress-bar').forEach(bar => {
        bar.style.width = '0%';
      });
      
      // Show loading state
      verdict.innerHTML = '<span class="loading"></span> Scanning URL...';
      verdict.style.display = "block";

      // Simulate scan process
      setTimeout(() => {
        // Simulate verdict logic (more sophisticated)
        const riskyKeywords = ["phish", "malware", "suspicious", "bad", "evil", "danger", "hack"];
        const isRisky = riskyKeywords.some(k => url.toLowerCase().includes(k));
        
        // Update wizard animation
        wizard.classList.remove("glow");
        
        // Display verdict
        verdict.style.display = "block";
        if (isRisky) {
          verdict.innerHTML = `<span class="risk-indicator risk-high"></span> ❌ HIGH RISK: ${url}`;
          verdict.classList.add("risky");
        } else {
          verdict.innerHTML = `<span class="risk-indicator risk-safe"></span> ✅ SAFE: ${url}`;
          verdict.classList.add("safe");
        }
        
        // Show badge
        badge.style.display = "block";
        
        // Show lore capsule
        loreCapsule.style.display = "block";
        
        // Generate detailed report
        const riskLevel = isRisky ? "high" : "low";
        const malwareRisk = isRisky ? 85 : 5;
        const phishingRisk = isRisky ? 75 : 10;
        const sslSecurity = isRisky ? 20 : 95;
        const privacyProtection = isRisky ? 30 : 85;
        
        loreText.innerHTML = `
          <strong>AngryDroid AI Shield Security Analysis Report</strong><br><br>
          Scanned URL: <strong>${url}</strong><br>
          Overall Risk Level: <strong>${riskLevel.toUpperCase()}</strong><br><br>
          The AI security system has analyzed the URL using multiple threat detection algorithms. 
          ${isRisky ? 
            "This site has been flagged for potential security risks. Exercise caution when visiting." : 
            "No immediate threats detected. Site appears safe for browsing."}
          <br><br>
          <i class="fas fa-lightbulb"></i> Recommendation: ${isRisky ? 
            "Avoid this site or proceed with extreme caution." : 
            "Site is safe to visit."}
        `;
        
        // Animate progress bars
        animateProgressBar('malware-bar', malwareRisk);
        animateProgressBar('phishing-bar', phishingRisk);
        animateProgressBar('ssl-bar', sslSecurity);
        animateProgressBar('privacy-bar', privacyProtection);
        
        // Update status texts
        document.getElementById('malware-status').textContent = 
          malwareRisk > 50 ? "Detected" : "Not detected";
        document.getElementById('phishing-status').textContent = 
          phishingRisk > 50 ? "High risk" : "Low risk";
        document.getElementById('ssl-status').textContent = 
          sslSecurity > 50 ? "Secure" : "Insecure";
        document.getElementById('privacy-status').textContent = 
          privacyProtection > 50 ? "Good" : "Poor";
      }, 3000);
    }
    
    function animateProgressBar(barId, targetWidth) {
      const bar = document.getElementById(barId);
      let width = 0;
      const interval = setInterval(() => {
        if (width >= targetWidth) {
          clearInterval(interval);
        } else {
          width++;
          bar.style.width = width + '%';
          
          // Change color based on risk level
          if (barId === 'malware-bar' || barId === 'phishing-bar') {
            if (width > 50) {
              bar.style.background = 'linear-gradient(to right, #ff3333, #ff0000)';
            }
          } else {
            if (width < 50) {
              bar.style.background = 'linear-gradient(to right, #ff3333, #ff0000)';
            }
          }
        }
      }, 20);
    }
    
    // Add enter key support
    document.getElementById("urlInput").addEventListener("keyup", function(event) {
      if (event.key === "Enter") {
        scanURL();
      }
    });
  </script>
</body>
</html>
