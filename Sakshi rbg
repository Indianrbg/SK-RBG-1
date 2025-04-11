<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Advanced Background Remover</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    :root {
      --primary: #4361ee;
      --secondary: #3f37c9;
      --accent: #4895ef;
      --light: #f8f9fa;
      --dark: #212529;
      --success: #4cc9f0;
      --danger: #f72585;
      --warning: #f8961e;
      --border-radius: 12px;
      --box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
      min-height: 100vh;
      padding: 2rem;
      color: var(--dark);
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      background: white;
      border-radius: var(--border-radius);
      box-shadow: var(--box-shadow);
      overflow: hidden;
    }

    .header {
      background: linear-gradient(to right, var(--primary), var(--secondary));
      color: white;
      padding: 1.5rem;
      text-align: center;
    }

    .header h1 {
      font-weight: 600;
      font-size: 1.8rem;
      margin-bottom: 0.5rem;
    }

    .header p {
      opacity: 0.9;
      font-weight: 300;
    }

    .main-content {
      padding: 2rem;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2rem;
    }

    @media (max-width: 768px) {
      .main-content {
        grid-template-columns: 1fr;
      }
    }

    .upload-section {
      display: flex;
      flex-direction: column;
    }

    .upload-area {
      border: 2px dashed #ccc;
      border-radius: var(--border-radius);
      padding: 2rem;
      text-align: center;
      margin-bottom: 1.5rem;
      transition: all 0.3s;
      cursor: pointer;
      background: var(--light);
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .upload-area:hover {
      border-color: var(--accent);
      background: rgba(72, 149, 239, 0.05);
    }

    .upload-area.active {
      border-color: var(--success);
      background: rgba(76, 201, 240, 0.05);
    }

    .upload-icon {
      font-size: 3rem;
      color: var(--primary);
      margin-bottom: 1rem;
    }

    .file-input {
      display: none;
    }

    .controls {
      background: var(--light);
      padding: 1.5rem;
      border-radius: var(--border-radius);
      margin-bottom: 1.5rem;
    }

    .control-group {
      margin-bottom: 1.2rem;
    }

    .control-group h3 {
      font-size: 1rem;
      margin-bottom: 0.8rem;
      color: var(--secondary);
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .control-group h3 i {
      font-size: 1.2rem;
    }

    .colors {
      display: flex;
      flex-wrap: wrap;
      gap: 0.8rem;
      margin-bottom: 1rem;
    }

    .color-option {
      width: 32px;
      height: 32px;
      border-radius: 8px;
      cursor: pointer;
      border: 2px solid transparent;
      transition: all 0.2s;
    }

    .color-option:hover {
      transform: scale(1.1);
    }

    .color-option.selected {
      border-color: var(--dark);
      box-shadow: 0 0 0 2px white, 0 0 0 4px var(--primary);
    }

    .custom-color {
      display: flex;
      align-items: center;
      gap: 0.8rem;
      margin-top: 0.8rem;
    }

    .dimension-controls {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
    }

    .input-group {
      display: flex;
      flex-direction: column;
      gap: 0.3rem;
    }

    .input-group label {
      font-size: 0.85rem;
      color: #666;
    }

    .input-group input, 
    .input-group select {
      padding: 0.6rem;
      border: 1px solid #ddd;
      border-radius: 8px;
      font-family: inherit;
    }

    .input-group input:focus, 
    .input-group select:focus {
      outline: none;
      border-color: var(--accent);
    }

    .crop-controls {
      display: flex;
      gap: 0.8rem;
      margin-bottom: 1rem;
    }

    .crop-btn {
      padding: 0.6rem;
      border-radius: 8px;
      border: 1px solid #ddd;
      background: white;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.2s;
    }

    .crop-btn:hover {
      background: #f0f0f0;
    }

    .crop-btn i {
      font-size: 1rem;
    }

    .straighten-control {
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }

    .straighten-control input {
      flex-grow: 1;
    }

    .preview-section {
      display: flex;
      flex-direction: column;
    }

    .image-container {
      position: relative;
      border-radius: var(--border-radius);
      overflow: hidden;
      background: #f0f0f0;
      flex-grow: 1;
      min-height: 300px;
      margin-bottom: 1.5rem;
    }

    #image {
      max-width: 100%;
      display: none;
    }

    #preview {
      max-width: 100%;
      max-height: 100%;
      display: none;
    }

    .empty-state {
      text-align: center;
      color: #999;
      padding: 2rem;
    }

    .empty-state i {
      font-size: 3rem;
      margin-bottom: 1rem;
      opacity: 0.5;
    }

    .image-info {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
      margin-bottom: 1rem;
    }

    .info-card {
      background: var(--light);
      padding: 0.8rem;
      border-radius: 8px;
      text-align: center;
    }

    .info-card h4 {
      font-size: 0.8rem;
      color: #666;
      margin-bottom: 0.3rem;
    }

    .info-card p {
      font-weight: 500;
    }

    .action-buttons {
      display: flex;
      gap: 1rem;
      margin-top: auto;
    }

    .btn {
      padding: 0.8rem 1.5rem;
      border: none;
      border-radius: 8px;
      font-family: inherit;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.2s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;
      flex: 1;
    }

    .btn-primary {
      background: var(--primary);
      color: white;
    }

    .btn-primary:hover {
      background: var(--secondary);
      transform: translateY(-2px);
    }

    .btn-outline {
      background: transparent;
      color: var(--primary);
      border: 1px solid var(--primary);
    }

    .btn-outline:hover {
      background: rgba(67, 97, 238, 0.1);
    }

    .btn:disabled {
      opacity: 0.6;
      cursor: not-allowed;
      transform: none !important;
    }

    #download {
      display: none;
    }

    .loading {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(255, 255, 255, 0.8);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 10;
      display: none;
    }

    .spinner {
      width: 40px;
      height: 40px;
      border: 4px solid rgba(67, 97, 238, 0.2);
      border-radius: 50%;
      border-top-color: var(--primary);
      animation: spin 1s ease-in-out infinite;
      margin-bottom: 1rem;
    }

    @keyframes spin {
      to { transform: rotate(360deg); }
    }

    .error-message {
      color: var(--danger);
      text-align: center;
      padding: 1rem;
      background: rgba(247, 37, 133, 0.1);
      border-radius: 8px;
      margin-bottom: 1rem;
      display: none;
    }

    .cropper-container {
      max-height: 400px;
    }

    /* Live Preview Styles */
    .live-preview-container {
      position: absolute;
      right: 20px;
      bottom: 20px;
      width: 150px;
      height: 150px;
      border-radius: 8px;
      border: 2px solid var(--primary);
      background: white;
      overflow: hidden;
      z-index: 20;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      display: none;
    }

    #livePreview {
      width: 100%;
      height: 100%;
      object-fit: contain;
      background: repeating-conic-gradient(#f0f0f0 0% 25%, white 0% 50%) 50% / 20px 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>Advanced Background Remover</h1>
      <p>Remove backgrounds, crop, and edit your images with ease</p>
    </div>

    <div class="main-content">
      <div class="upload-section">
        <div class="upload-area" id="uploadArea">
          <input type="file" id="fileInput" class="file-input" accept="image/*">
          <div class="upload-icon">
            <i class="fas fa-cloud-upload-alt"></i>
          </div>
          <h3>Drag & Drop your image here</h3>
          <p>or click to browse files</p>
          <p class="drag-text">Supports JPG, PNG (Max 5MB)</p>
        </div>

        <div class="error-message" id="errorMessage"></div>

        <div class="controls">
          <div class="control-group">
            <h3><i class="fas fa-palette"></i> Background Color</h3>
            <div class="colors" id="colorPicker"></div>
            <div class="custom-color">
              <input type="color" id="customColor" value="#ffffff">
              <span>Custom color</span>
            </div>
          </div>

          <div class="control-group">
            <h3><i class="fas fa-crop-alt"></i> Crop & Rotate</h3>
            <div class="crop-controls">
              <button class="crop-btn" id="rotateLeft" title="Rotate Left">
                <i class="fas fa-undo"></i>
              </button>
              <button class="crop-btn" id="rotateRight" title="Rotate Right">
                <i class="fas fa-redo"></i>
              </button>
              <div class="straighten-control">
                <button class="crop-btn" title="Straighten">
                  <i class="fas fa-ruler-combined"></i>
                </button>
                <input type="range" id="straighten" min="-45" max="45" value="0" step="1">
              </div>
            </div>
          </div>

          <div class="control-group">
            <h3><i class="fas fa-expand"></i> Dimensions</h3>
            <div class="dimension-controls">
              <div class="input-group">
                <label>Width</label>
                <input type="number" id="customWidth" placeholder="Auto" min="1">
              </div>
              <div class="input-group">
                <label>Unit</label>
                <select id="widthUnit">
                  <option value="px">px</option>
                  <option value="cm">cm</option>
                  <option value="in">in</option>
                </select>
              </div>
              <div class="input-group">
                <label>Height</label>
                <input type="number" id="customHeight" placeholder="Auto" min="1">
              </div>
              <div class="input-group">
                <label>Unit</label>
                <select id="heightUnit">
                  <option value="px">px</option>
                  <option value="cm">cm</option>
                  <option value="in">in</option>
                </select>
              </div>
            </div>
          </div>

          <div class="control-group">
            <h3><i class="fas fa-file-image"></i> Output Settings</h3>
            <div class="dimension-controls">
              <div class="input-group">
                <label>Target Size</label>
                <input type="number" id="targetSize" placeholder="Original" min="1">
              </div>
              <div class="input-group">
                <label>Unit</label>
                <select id="sizeUnit">
                  <option value="KB">KB</option>
                  <option value="MB">MB</option>
                </select>
              </div>
            </div>
          </div>
        </div>

        <div class="image-info">
          <div class="info-card">
            <h4>Original Width</h4>
            <p id="originalWidth">-</p>
          </div>
          <div class="info-card">
            <h4>Original Height</h4>
            <p id="originalHeight">-</p>
          </div>
          <div class="info-card">
            <h4>File Size</h4>
            <p id="originalSize">-</p>
          </div>
          <div class="info-card">
            <h4>Aspect Ratio</h4>
            <p id="aspectRatio">-</p>
          </div>
        </div>

        <button id="cropBtn" class="btn btn-primary">
          <i class="fas fa-magic"></i> Process Image
        </button>
      </div>

      <div class="preview-section">
        <div class="image-container">
          <div class="empty-state">
            <i class="fas fa-image"></i>
            <h3>Your processed image will appear here</h3>
            <p>Upload an image to get started</p>
          </div>
          <img id="image" alt="Image to crop">
          <img id="preview" alt="Processed image preview">
          <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>Processing your image...</p>
          </div>
          <!-- Live Preview Container -->
          <div class="live-preview-container" id="livePreviewContainer">
            <img id="livePreview" alt="Live preview">
          </div>
        </div>

        <div class="action-buttons">
          <a id="download" class="btn btn-primary">
            <i class="fas fa-download"></i> Download
          </a>
        </div>
      </div>
    </div>
  </div>

  <canvas id="canvas" style="display:none;"></canvas>
  <canvas id="previewCanvas" style="display:none;"></canvas>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.js"></script>
  <script>
    document.addEventListener('DOMContentLoaded', function() {
      // API Key for remove.bg
      const apiKey = "poUHyHQHQuLyXWbxx5a4fErA";
      
      // DOM Elements
      const fileInput = document.getElementById("fileInput");
      const uploadArea = document.getElementById("uploadArea");
      const image = document.getElementById("image");
      const preview = document.getElementById("preview");
      const canvas = document.getElementById("canvas");
      const ctx = canvas.getContext("2d");
      const downloadLink = document.getElementById("download");
      const colorPicker = document.getElementById("colorPicker");
      const customColorInput = document.getElementById("customColor");
      const errorMessage = document.getElementById("errorMessage");
      const loadingElement = document.getElementById("loading");
      const emptyState = document.querySelector(".empty-state");
      const cropBtn = document.getElementById("cropBtn");
      const rotateLeft = document.getElementById("rotateLeft");
      const rotateRight = document.getElementById("rotateRight");
      const straighten = document.getElementById("straighten");
      const originalWidth = document.getElementById("originalWidth");
      const originalHeight = document.getElementById("originalHeight");
      const originalSize = document.getElementById("originalSize");
      const aspectRatio = document.getElementById("aspectRatio");
      const livePreviewContainer = document.getElementById("livePreviewContainer");
      const livePreview = document.getElementById("livePreview");
      const previewCanvas = document.getElementById("previewCanvas");
      const previewCtx = previewCanvas.getContext("2d");

      // Color options
      const colors = [
        "#ffffff", "#000000", "#f44336", "#2196f3", 
        "#4caf50", "#ffeb3b", "#9c27b0", "#ff9800", 
        "#00bcd4", "#e91e63"
      ];

      // App state
      let selectedColor = "#ffffff";
      let cropper;
      let previewUpdateTimeout;

      // Initialize color picker
      colors.forEach(color => {
        const box = document.createElement("div");
        box.className = "color-option";
        box.style.backgroundColor = color;
        box.onclick = () => {
          selectedColor = color;
          customColorInput.value = color;
          document.querySelectorAll(".color-option").forEach(b => b.classList.remove("selected"));
          box.classList.add("selected");
          updateLivePreview();
        };
        colorPicker.appendChild(box);
      });

      // Select white by default
      document.querySelector('.color-option').click();

      // Handle custom color selection
      customColorInput.addEventListener("input", () => {
        selectedColor = customColorInput.value;
        document.querySelectorAll(".color-option").forEach(b => b.classList.remove("selected"));
        updateLivePreview();
      });

      // Handle drag and drop
      uploadArea.addEventListener('dragover', (e) => {
        e.preventDefault();
        uploadArea.classList.add('active');
      });

      uploadArea.addEventListener('dragleave', () => {
        uploadArea.classList.remove('active');
      });

      uploadArea.addEventListener('drop', (e) => {
        e.preventDefault();
        uploadArea.classList.remove('active');
        
        if (e.dataTransfer.files.length) {
          fileInput.files = e.dataTransfer.files;
          handleFileUpload();
        }
      });

      uploadArea.addEventListener('click', () => {
        fileInput.click();
      });

      fileInput.addEventListener('change', handleFileUpload);

      // Crop functionality
      rotateLeft.addEventListener('click', () => {
        if (cropper) {
          cropper.rotate(-90);
          updateLivePreview();
        }
      });
      
      rotateRight.addEventListener('click', () => {
        if (cropper) {
          cropper.rotate(90);
          updateLivePreview();
        }
      });
      
      straighten.addEventListener('input', () => {
        if (cropper) {
          cropper.rotateTo(parseInt(straighten.value));
          updateLivePreview();
        }
      });

      cropBtn.addEventListener('click', processImage);

      async function handleFileUpload() {
        const file = fileInput.files[0];
        if (!file) return;

        // Validate file type
        if (!file.type.match('image.*')) {
          showError('Please upload an image file (JPEG, PNG)');
          return;
        }

        // Validate file size (max 5MB)
        if (file.size > 5 * 1024 * 1024) {
          showError('File size too large (max 5MB)');
          return;
        }

        hideError();
        loadingElement.style.display = "flex";
        emptyState.style.display = "none";
        image.style.display = "none";
        preview.style.display = "none";
        downloadLink.style.display = "none";
        livePreviewContainer.style.display = "none";

        try {
          // Process with remove.bg API
          const formData = new FormData();
          formData.append("image_file", file);
          formData.append("size", "auto");

          const res = await fetch("https://api.remove.bg/v1.0/removebg", {
            method: "POST",
            headers: { "X-Api-Key": apiKey },
            body: formData
          });

          if (!res.ok) {
            throw new Error(`API Error: ${res.status}`);
          }

          const blob = await res.blob();
          originalSize.textContent = (blob.size / 1024).toFixed(2) + " KB";

          const reader = new FileReader();
          reader.onload = () => {
            image.src = reader.result;
            image.style.display = "block";
            if (cropper) cropper.destroy();
            
            cropper = new Cropper(image, {
              viewMode: 1,
              autoCropArea: 1,
              responsive: true,
              movable: true,
              zoomable: true,
              rotatable: true,
              ready() {
                originalWidth.textContent = image.naturalWidth;
                originalHeight.textContent = image.naturalHeight;
                aspectRatio.textContent = (image.naturalWidth / image.naturalHeight).toFixed(2);
                loadingElement.style.display = "none";
                emptyState.style.display = "none";
                livePreviewContainer.style.display = "block";
                updateLivePreview();
              },
              crop() {
                updateLivePreview();
              },
              cropmove() {
                updateLivePreview();
              },
              zoom() {
                updateLivePreview();
              }
            });
          };
          reader.readAsDataURL(blob);
        } catch (error) {
          console.error('Error:', error);
          showError('Failed to process image. Please try again.');
          loadingElement.style.display = "none";
          emptyState.style.display = "block";
        }
      }

      function updateLivePreview() {
        if (!cropper) return;
        
        // Clear any pending updates
        clearTimeout(previewUpdateTimeout);
        
        // Debounce the preview update to improve performance
        previewUpdateTimeout = setTimeout(() => {
          try {
            const croppedCanvas = cropper.getCroppedCanvas({
              fillColor: selectedColor === 'transparent' ? 'rgba(0,0,0,0)' : selectedColor || '#ffffff'
            });
            
            if (croppedCanvas) {
              // Set preview canvas dimensions
              previewCanvas.width = 150;
              previewCanvas.height = 150;
              
              // Calculate dimensions to maintain aspect ratio
              const ratio = Math.min(
                previewCanvas.width / croppedCanvas.width,
                previewCanvas.height / croppedCanvas.height
              );
              const newWidth = croppedCanvas.width * ratio;
              const newHeight = croppedCanvas.height * ratio;
              const x = (previewCanvas.width - newWidth) / 2;
              const y = (previewCanvas.height - newHeight) / 2;
              
              // Fill with selected background color or transparent
              previewCtx.fillStyle = selectedColor === 'transparent' ? 'rgba(0,0,0,0)' : selectedColor || '#ffffff';
              previewCtx.fillRect(0, 0, previewCanvas.width, previewCanvas.height);
              
              // Draw the cropped image
              previewCtx.drawImage(croppedCanvas, x, y, newWidth, newHeight);
              
              // Update live preview image
              livePreview.src = previewCanvas.toDataURL();
            }
          } catch (error) {
            console.error('Error updating live preview:', error);
          }
        }, 100);
      }

      function processImage() {
        if (!cropper) return;
        
        loadingElement.style.display = "flex";
        
        setTimeout(() => {
          try {
            let width = parseFloat(document.getElementById("customWidth").value);
            let height = parseFloat(document.getElementById("customHeight").value);
            const widthUnit = document.getElementById("widthUnit").value;
            const heightUnit = document.getElementById("heightUnit").value;
            const sizeValue = parseFloat(document.getElementById("targetSize").value);
            const sizeUnit = document.getElementById("sizeUnit").value;

            // Convert units to pixels if needed
            if (widthUnit === "cm") width = width * 37.7952755906;
            if (widthUnit === "in") width = width * 96;
            if (heightUnit === "cm") height = height * 37.7952755906;
            if (heightUnit === "in") height = height * 96;

            // Get cropped canvas with selected dimensions
            const croppedCanvas = cropper.getCroppedCanvas({
              width: width || undefined,
              height: height || undefined,
              fillColor: selectedColor === 'transparent' ? 'rgba(0,0,0,0)' : selectedColor || '#ffffff'
            });

            if (!croppedCanvas) {
              throw new Error('Failed to crop image');
            }

            canvas.width = croppedCanvas.width;
            canvas.height = croppedCanvas.height;
            ctx.drawImage(croppedCanvas, 0, 0);

            // Handle target size if specified
            if (!isNaN(sizeValue)) {
              const targetBytes = sizeUnit === "MB" ? sizeValue * 1024 * 1024 : sizeValue * 1024;
              let quality = 0.9;
              let dataURL;
              
              // Binary search for optimal quality
              let minQuality = 0.1;
              let maxQuality = 1.0;
              let iterations = 0;
              const maxIterations = 10;
              
              while (iterations < maxIterations) {
                quality = (minQuality + maxQuality) / 2;
                dataURL = canvas.toDataURL("image/jpeg", quality);
                
                if (dataURL.length > targetBytes) {
                  maxQuality = quality;
                } else {
                  minQuality = quality;
                }
                
                iterations++;
                
                // If we're close enough, break
                if (Math.abs(dataURL.length - targetBytes) < targetBytes * 0.05) {
                  break;
                }
              }
              
              preview.src = dataURL;
              downloadLink.href = dataURL;
              downloadLink.setAttribute('download', 'background-removed.jpg');
            } else {
              const finalURL = canvas.toDataURL("image/png");
              preview.src = finalURL;
              downloadLink.href = finalURL;
              downloadLink.setAttribute('download', 'background-removed.png');
            }

            loadingElement.style.display = "none";
            preview.style.display = "block";
            downloadLink.style.display = "flex";
          } catch (error) {
            console.error('Error processing image:', error);
            showError('Failed to process image. Please try again.');
            loadingElement.style.display = "none";
          }
        }, 100);
      }

      function showError(message) {
        errorMessage.textContent = message;
        errorMessage.style.display = 'block';
      }

      function hideError() {
        errorMessage.style.display = 'none';
      }
    });
  </script>
</body>
</html>
