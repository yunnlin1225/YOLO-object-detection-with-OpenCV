<!doctype html>
<html lang="zh-Hant">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>YOLO 物件偵測（使用 OpenCV）</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-" crossorigin="anonymous">
  <style>
    body{padding-top:56px}
    pre.code{background:#f8f9fa;padding:12px;border-radius:6px}
    .hero{background:linear-gradient(90deg, #0d6efd22, #6c757d11);padding:28px;border-radius:8px}
    .img-sample{max-width:100%;height:auto;border-radius:6px;box-shadow:0 6px 18px rgba(0,0,0,0.08)}
  </style>
</head>
<body>
<nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">YOLO 物件偵測</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#nav" aria-controls="nav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="nav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="#intro">簡介</a></li>
        <li class="nav-item"><a class="nav-link" href="#run">執行</a></li>
        <li class="nav-item"><a class="nav-link" href="#limits">限制</a></li>
        <li class="nav-item"><a class="nav-link" href="#samples">範例畫面</a></li>
      </ul>
    </div>
  </div>
</nav>

<main class="container mt-4">
  <header class="hero mb-4">
    <h1>YOLO 物件偵測（使用 OpenCV 與 Python）</h1>
    <p class="lead">本範例以 <strong>YOLOv3</strong>（在 COCO 資料集上預訓練）搭配 OpenCV 示範影像、影片與即時影像的物件偵測。</p>
    <p class="small">作者建議：如果要在 GitHub 上發佈或教學，請先把模型檔與影像/影片放到專案目錄（例如 <code>yolo-coco/</code>、<code>images/</code>、<code>videos/</code>）。</p>
  </header>

  <section id="intro" class="mb-4">
    <h2>簡介</h2>
    <p>COCO（Common Objects in Context）資料集包含 <strong>80 類</strong>常見物件，例如人、腳踏車、車輛、動物（貓、狗、鳥、馬、牛、羊）、家具、餐具等。完整類別清單可參考 Darknet 的 <a href="https://github.com/pjreddie/darknet/blob/master/data/coco.names" target="_blank">coco.names</a>。</p>
    <p>此專案使用由 Darknet 團隊釋出的 YOLOv3 預訓練模型（放在 <code>yolo-coco/</code> 目錄）。</p>
    <ul>
      <li>yolo-coco：包含 <code>yolov3.weights</code>, <code>yolov3.cfg</code>, <code>coco.names</code>。</li>
      <li>參考 Darknet 官網：<a href="https://pjreddie.com/darknet/yolo/" target="_blank">pjreddie.com/darknet/yolo</a></li>
    </ul>
  </section>

  <section id="install" class="mb-4">
    <h2>安裝</h2>
    <p>請先建立 Python 虛擬環境（建議），再安裝套件：</p>
    <pre class="code"><code>pip install numpy
pip install opencv-python
pip install imutils  # 僅在即時偵測需要</code></pre>
  </section>

  <section id="run" class="mb-4">
    <h2>執行範例</h2>
    <h5>影像偵測</h5>
    <p>執行下列指令來偵測單張影像（範例檔案：<code>images/baggage_claim.jpg</code>）：</p>
    <pre class="code"><code>python yolo.py --image images/baggage_claim.jpg</code></pre>

    <h5>影片偵測</h5>
    <p>偵測影片並輸出成檔案：</p>
    <pre class="code"><code>python yolo_video.py --input videos/airport.mp4 --output output/airport_output.avi --yolo yolo-coco</code></pre>

    <h5>即時偵測（webcam）</h5>
    <p>啟動即時攝影機偵測：</p>
    <pre class="code"><code>python real_time_object_detection.py</code></pre>
  </section>

  <section id="samples" class="mb-4">
    <h2>範例畫面</h2>
    <p>下列為專案 README 中使用的範例圖片／GIF（直接連到原始 GitHub 圖檔）：</p>
    <div class="row g-3">
      <div class="col-md-6">
        <figure>
          <img class="img-sample" src="https://raw.githubusercontent.com/yash42828/YOLO-object-detection-with-OpenCV/master/Object%20dection%20using%20image/1.png" alt="範例1">
          <figcaption class="small text-muted">偵測到多名人物與行李。</figcaption>
        </figure>
      </div>
      <div class="col-md-6">
        <figure>
          <img class="img-sample" src="https://raw.githubusercontent.com/yash42828/YOLO-object-detection-with-OpenCV/master/Object%20detection%20using%20video/car.gif" alt="範例GIF">
          <figcaption class="small text-muted">影片中偵測到車輛與行人、交通號誌等。</figcaption>
        </figure>
      </div>
    </div>
  </section>

  <section id="limits" class="mb-4">
    <h2>限制</h2>
    <p>YOLO 的主要限制：</p>
    <ul>
      <li>對於 <strong>小物件</strong>較不敏感（若多個小物件在同一格子內，YOLO 可能會漏偵測）。</li>
      <li>群聚或遮擋情況下會較差。</li>
    </ul>
    <p>替代方案：</p>
    <ul>
      <li>若需要較好的小物件偵測，可考慮 <strong>Faster R-CNN</strong>（通常較慢但精準）。</li>
      <li>SSD（Single Shot Detector）在速度與精準度間常能取得不錯的折衷。</li>
    </ul>
  </section>

  <section id="notes" class="mb-5">
    <h2>備註</h2>
    <p>如果你要把這個 HTML 當作 README 的網站版，可以將它放到專案並搭配 GitHub Pages 發佈。需要我把此檔案打包成可下載的 HTML 檔嗎？或是要我幫你套成 GitHub Pages 的格式（例如使用 <code>index.html</code> 放到 <code>gh-pages</code> 分支或 <code>docs/</code> 目錄）？</p>
  </section>

  <footer class="text-center mb-5">
    <small class="text-muted">翻譯與格式化自原始 README（YOLO-object-detection-with-OpenCV）</small>
  </footer>
</main>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="" crossorigin="anonymous"></script>
</body>
</html>
