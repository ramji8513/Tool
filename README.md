<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Complete PDF Tools - Convert, Merge, Split, Compress</title>
    <script src="https://unpkg.com/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <script src="https://unpkg.com/downloadjs@1.4.7"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://unpkg.com/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <script src="https://unpkg.com/@pdf-lib/fontkit@0.0.4/dist/fontkit.umd.min.js"></script>
    <style>
        :root {
            --primary: #4a6bdf;
            --secondary: #6c757d;
            --success: #28a745;
            --danger: #dc3545;
            --light: #f8f9fa;
            --dark: #343a40;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            border-bottom: 1px solid #eee;
            margin-bottom: 30px;
        }
        
        .logo {
            font-size: 24px;
            font-weight: bold;
            color: var(--primary);
        }
        
        nav ul {
            display: flex;
            list-style: none;
        }
        
        nav ul li {
            margin-left: 20px;
        }
        
        nav ul li a {
            color: var(--dark);
            text-decoration: none;
            font-weight: 500;
        }
        
        .tool-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }
        
        .tool-card {
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .tool-card:hover {
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transform: translateY(-5px);
        }
        
        .tool-card i {
            font-size: 40px;
            color: var(--primary);
            margin-bottom: 15px;
        }
        
        .tool-interface {
            display: none;
            margin-top: 30px;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
        }
        
        .drop-area {
            border: 2px dashed #aaa;
            border-radius: 8px;
            padding: 40px;
            text-align: center;
            margin-bottom: 20px;
            cursor: pointer;
        }
        
        .drop-area.highlight {
            border-color: var(--primary);
            background-color: rgba(74, 107, 223, 0.05);
        }
        
        .options {
            margin: 20px 0;
        }
        
        .option-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        select, input[type="range"], input[type="number"] {
            width: 100%;
            padding: 8px;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
        
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            margin-right: 10px;
        }
        
        button:hover {
            opacity: 0.9;
        }
        
        .results {
            margin-top: 20px;
            display: none;
        }
        
        .result-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            background-color: #f9f9f9;
            border-radius: 4px;
            margin-bottom: 10px;
        }
        
        .progress-bar {
            width: 100%;
            background-color: #eee;
            border-radius: 4px;
            margin: 20px 0;
            display: none;
        }
        
        .progress {
            height: 20px;
            background-color: var(--primary);
            border-radius: 4px;
            width: 0%;
            transition: width 0.3s;
        }
        
        @media (max-width: 768px) {
            .tool-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            }
            
            header {
                flex-direction: column;
                text-align: center;
            }
            
            nav ul {
                margin-top: 20px;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="logo">PDF Tools Pro</div>
        <nav>
            <ul>
                <li><a href="#">Home</a></li>
                <li><a href="#tools">Tools</a></li>
                <li><a href="#about">About</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h1>Complete PDF Toolkit</h1>
        <p>Convert, edit, merge, split, compress and more - all your PDF needs in one place.</p>
        
        <div class="tool-grid" id="tools">
            <!-- Convert to PDF -->
            <div class="tool-card" data-tool="jpg-to-pdf">
                <i>🖼️</i>
                <h3>JPG to PDF</h3>
                <p>Convert images to PDF documents</p>
            </div>
            <div class="tool-card" data-tool="word-to-pdf">
                <i>📝</i>
                <h3>Word to PDF</h3>
                <p>Convert DOC/DOCX to PDF</p>
            </div>
            <div class="tool-card" data-tool="ppt-to-pdf">
                <i>📊</i>
                <h3>PPT to PDF</h3>
                <p>Convert PowerPoint to PDF</p>
            </div>
            <div class="tool-card" data-tool="excel-to-pdf">
                <i>📈</i>
                <h3>Excel to PDF</h3>
                <p>Convert XLS/XLSX to PDF</p>
            </div>
            
            <!-- Convert from PDF -->
            <div class="tool-card" data-tool="pdf-to-jpg">
                <i>📷</i>
                <h3>PDF to JPG</h3>
                <p>Convert PDF pages to images</p>
            </div>
            <div class="tool-card" data-tool="pdf-to-word">
                <i>📄</i>
                <h3>PDF to Word</h3>
                <p>Convert PDF to DOC/DOCX</p>
            </div>
            
            <!-- Edit & Organize -->
            <div class="tool-card" data-tool="merge-pdf">
                <i>🧩</i>
                <h3>Merge PDF</h3>
                <p>Combine multiple PDFs into one</p>
            </div>
            <div class="tool-card" data-tool="split-pdf">
                <i>✂️</i>
                <h3>Split PDF</h3>
                <p>Split PDF into multiple files</p>
            </div>
            <div class="tool-card" data-tool="remove-pages">
                <i>🗑️</i>
                <h3>Remove Pages</h3>
                <p>Delete pages from PDF</p>
            </div>
            <div class="tool-card" data-tool="extract-pages">
                <i>📑</i>
                <h3>Extract Pages</h3>
                <p>Extract specific pages</p>
            </div>
            
            <!-- Optimize & Secure -->
            <div class="tool-card" data-tool="compress-pdf">
                <i>🗜️</i>
                <h3>Compress PDF</h3>
                <p>Reduce PDF file size</p>
            </div>
            <div class="tool-card" data-tool="protect-pdf">
                <i>🔒</i>
                <h3>Protect PDF</h3>
                <p>Add password protection</p>
            </div>
            <div class="tool-card" data-tool="unlock-pdf">
                <i>🔓</i>
                <h3>Unlock PDF</h3>
                <p>Remove password protection</p>
            </div>
            <div class="tool-card" data-tool="sign-pdf">
                <i>✍️</i>
                <h3>Sign PDF</h3>
                <p>Add digital signature</p>
            </div>
        </div>
        
        <!-- Tool Interface -->
        <div class="tool-interface" id="toolInterface">
            <div class="tool-header">
                <h2 id="toolTitle">Tool Name</h2>
                <button id="closeTool">✕ Close</button>
            </div>
            
            <div class="drop-area" id="dropArea">
                <p>📁 Drag & drop files here or click to browse</p>
                <input type="file" id="fileInput" style="display: none;" multiple>
            </div>
            
            <div class="options" id="options">
                <!-- Options will be dynamically inserted here -->
            </div>
            
            <div class="progress-bar" id="progressBar">
                <div class="progress" id="progress"></div>
            </div>
            
            <button id="processBtn">Process</button>
            <button id="resetBtn">Reset</button>
            
            <div class="results" id="results">
                <!-- Results will be dynamically inserted here -->
            </div>
        </div>
    </main>

    <script>
        // DOM Elements
        const toolCards = document.querySelectorAll('.tool-card');
        const toolInterface = document.getElementById('toolInterface');
        const toolTitle = document.getElementById('toolTitle');
        const dropArea = document.getElementById('dropArea');
        const fileInput = document.getElementById('fileInput');
        const optionsDiv = document.getElementById('options');
        const processBtn = document.getElementById('processBtn');
        const resetBtn = document.getElementById('resetBtn');
        const resultsDiv = document.getElementById('results');
        const progressBar = document.getElementById('progressBar');
        const progress = document.getElementById('progress');
        const closeToolBtn = document.getElementById('closeTool');
        
        // Current tool and files
        let currentTool = null;
        let files = [];
        
        // Tool configurations
        const toolConfigs = {
            'jpg-to-pdf': {
                title: 'JPG to PDF Converter',
                options: `
                    <div class="option-group">
                        <label for="pageSize">Page Size:</label>
                        <select id="pageSize">
                            <option value="a4">A4 (210 × 297 mm)</option>
                            <option value="letter">Letter (8.5 × 11 in)</option>
                            <option value="auto">Auto (Fit to image)</option>
                        </select>
                    </div>
                    <div class="option-group">
                        <label for="orientation">Orientation:</label>
                        <select id="orientation">
                            <option value="portrait">Portrait</option>
                            <option value="landscape">Landscape</option>
                        </select>
                    </div>
                    <div class="option-group">
                        <label for="margin">Margin (mm):</label>
                        <input type="number" id="margin" min="0" max="50" value="10">
                    </div>
                    <div class="option-group">
                        <input type="checkbox" id="merge" checked>
                        <label for="merge">Merge all images into one PDF</label>
                    </div>
                `
            },
            'merge-pdf': {
                title: 'Merge PDF Files',
                options: `
                    <div class="option-group">
                        <label for="mergeOrder">Merge Order:</label>
                        <select id="mergeOrder">
                            <option value="sequence">In sequence (as uploaded)</option>
                            <option value="alphabetical">Alphabetical by filename</option>
                        </select>
                    </div>
                `
            },
            'split-pdf': {
                title: 'Split PDF',
                options: `
                    <div class="option-group">
                        <label>Split Mode:</label>
                        <select id="splitMode">
                            <option value="single">Extract single page</option>
                            <option value="range">Extract page range</option>
                            <option value="every">Split every page</option>
                        </select>
                    </div>
                    <div class="option-group" id="pageNumberGroup">
                        <label for="pageNumber">Page Number:</label>
                        <input type="number" id="pageNumber" min="1" value="1">
                    </div>
                    <div class="option-group" id="pageRangeGroup" style="display: none;">
                        <label for="startPage">Start Page:</label>
                        <input type="number" id="startPage" min="1" value="1">
                        <label for="endPage">End Page:</label>
                        <input type="number" id="endPage" min="1" value="1">
                    </div>
                `
            },
            'compress-pdf': {
                title: 'Compress PDF',
                options: `
                    <div class="option-group">
                        <label for="compressionLevel">Compression Level:</label>
                        <select id="compressionLevel">
                            <option value="low">Low (Best quality)</option>
                            <option value="medium" selected>Medium (Recommended)</option>
                            <option value="high">High (Smallest size)</option>
                        </select>
                    </div>
                    <div class="option-group">
                        <label for="quality">Quality: <span id="qualityValue">80</span>%</label>
                        <input type="range" id="quality" min="10" max="100" value="80">
                    </div>
                    <div class="option-group">
                        <input type="checkbox" id="removeImages" checked>
                        <label for="removeImages">Optimize images</label>
                    </div>
                `
            }
        };
        
        // Initialize tool cards
        toolCards.forEach(card => {
            card.addEventListener('click', () => {
                const tool = card.getAttribute('data-tool');
                currentTool = tool;
                
                // Show tool interface
                toolInterface.style.display = 'block';
                toolTitle.textContent = toolConfigs[tool]?.title || 'PDF Tool';
                
                // Set options
                optionsDiv.innerHTML = toolConfigs[tool]?.options || '<p>No additional options for this tool.</p>';
                
                // Special setup for certain tools
                if (tool === 'split-pdf') {
                    setupSplitPdfOptions();
                } else if (tool === 'compress-pdf') {
                    setupCompressOptions();
                }
                
                // Scroll to tool interface
                toolInterface.scrollIntoView({ behavior: 'smooth' });
            });
        });
        
        // Close tool interface
        closeToolBtn.addEventListener('click', () => {
            toolInterface.style.display = 'none';
            resetTool();
        });
        
        // Drag and drop functionality
        ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
            dropArea.addEventListener(eventName, preventDefaults, false);
            document.body.addEventListener(eventName, preventDefaults, false);
        });
        
        ['dragenter', 'dragover'].forEach(eventName => {
            dropArea.addEventListener(eventName, highlight, false);
        });
        
        ['dragleave', 'drop'].forEach(eventName => {
            dropArea.addEventListener(eventName, unhighlight, false);
        });
        
        dropArea.addEventListener('drop', handleDrop, false);
        dropArea.addEventListener('click', () => fileInput.click());
        fileInput.addEventListener('change', handleFileSelect);
        
        function preventDefaults(e) {
            e.preventDefault();
            e.stopPropagation();
        }
        
        function highlight() {
            dropArea.classList.add('highlight');
        }
        
        function unhighlight() {
            dropArea.classList.remove('highlight');
        }
        
        function handleDrop(e) {
            const dt = e.dataTransfer;
            files = Array.from(dt.files);
            updateFileDisplay();
        }
        
        function handleFileSelect(e) {
            files = Array.from(e.target.files);
            updateFileDisplay();
        }
        
        function updateFileDisplay() {
            if (files.length > 0) {
                dropArea.innerHTML = `<p>✅ ${files.length} file(s) selected</p>`;
                dropArea.style.borderStyle = 'solid';
            }
        }
        
        // Process button
        processBtn.addEventListener('click', async () => {
            if (files.length === 0) {
                alert('Please select files first');
                return;
            }
            
            try {
                progressBar.style.display = 'block';
                progress.style.width = '0%';
                
                // Simulate progress
                for (let i = 0; i <= 100; i += 10) {
                    await new Promise(resolve => setTimeout(resolve, 100));
                    progress.style.width = `${i}%`;
                }
                
                // Process based on current tool
                let result;
                switch(currentTool) {
                    case 'jpg-to-pdf':
                        result = await convertJpgToPdf();
                        break;
                    case 'merge-pdf':
                        result = await mergePdfs();
                        break;
                    case 'split-pdf':
                        result = await splitPdf();
                        break;
                    case 'compress-pdf':
                        result = await compressPdf();
                        break;
                    default:
                        result = { name: 'output.pdf', blob: new Blob() };
                }
                
                // Show result
                showResult(result);
                
            } catch (error) {
                console.error('Error:', error);
                alert('An error occurred while processing the file');
            } finally {
                progressBar.style.display = 'none';
            }
        });
        
        // Reset button
        resetBtn.addEventListener('click', resetTool);
        
        function resetTool() {
            files = [];
            fileInput.value = '';
            dropArea.innerHTML = '<p>📁 Drag & drop files here or click to browse</p>';
            dropArea.style.borderStyle = 'dashed';
            resultsDiv.style.display = 'none';
            resultsDiv.innerHTML = '';
            progressBar.style.display = 'none';
        }
        
        // Tool-specific functions
        async function convertJpgToPdf() {
            const { PDFDocument, rgb } = PDFLib;
            
            // Create a new PDF document
            const pdfDoc = await PDFDocument.create();
            
            // Process each image
            for (const file of files) {
                if (!file.type.startsWith('image/')) continue;
                
                // Add a new page
                const page = pdfDoc.addPage();
                
                // Get image dimensions
                const img = await createImageBitmap(file);
                const { width, height } = img;
                
                // Set page size based on options
                const pageSize = document.getElementById('pageSize').value;
                const orientation = document.getElementById('orientation').value;
                const margin = parseInt(document.getElementById('margin').value);
                
                let pageWidth, pageHeight;
                
                if (pageSize === 'auto') {
                    pageWidth = width;
                    pageHeight = height;
                } else if (pageSize === 'a4') {
                    pageWidth = 595; // A4 width in points (1mm = 2.83465 points)
                    pageHeight = 842; // A4 height
                } else { // letter
                    pageWidth = 612;
                    pageHeight = 792;
                }
                
                if (orientation === 'landscape' && pageSize !== 'auto') {
                    [pageWidth, pageHeight] = [pageHeight, pageWidth];
                }
                
                page.setSize(pageWidth, pageHeight);
                
                // Embed the image
                const imageBytes = await file.arrayBuffer();
                let image;
                
                if (file.type === 'image/jpeg') {
                    image = await pdfDoc.embedJpg(imageBytes);
                } else {
                    image = await pdfDoc.embedPng(imageBytes);
                }
                
                // Draw image on page with margin
                const marginPoints = margin * 2.83465; // Convert mm to points
                const imgWidth = pageWidth - (marginPoints * 2);
                const imgHeight = (imgWidth / image.width) * image.height;
                
                page.drawImage(image, {
                    x: marginPoints,
                    y: (pageHeight - imgHeight) / 2,
                    width: imgWidth,
                    height: imgHeight,
                });
            }
            
            // Save the PDF
            const pdfBytes = await pdfDoc.save();
            return {
                name: 'converted.pdf',
                blob: new Blob([pdfBytes], { type: 'application/pdf' })
            };
        }
        
        async function mergePdfs() {
            const { PDFDocument } = PDFLib;
            
            const mergedPdf = await PDFDocument.create();
            
            for (const file of files) {
                if (file.type !== 'application/pdf') continue;
                
                const pdfBytes = await file.arrayBuffer();
                const pdfDoc = await PDFDocument.load(pdfBytes);
                
                const pages = await mergedPdf.copyPages(pdfDoc, pdfDoc.getPageIndices());
                pages.forEach(page => mergedPdf.addPage(page));
            }
            
            const mergedPdfBytes = await mergedPdf.save();
            return {
                name: 'merged.pdf',
                blob: new Blob([mergedPdfBytes], { type: 'application/pdf' })
            };
        }
        
        async function splitPdf() {
            const { PDFDocument } = PDFLib;
            
            if (files.length !== 1 || files[0].type !== 'application/pdf') {
                throw new Error('Please select exactly one PDF file');
            }
            
            const pdfBytes = await files[0].arrayBuffer();
            const pdfDoc = await PDFDocument.load(pdfBytes);
            const pageCount = pdfDoc.getPageCount();
            
            const splitMode = document.getElementById('splitMode').value;
            const results = [];
            
            if (splitMode === 'single') {
                const pageNumber = parseInt(document.getElementById('pageNumber').value) - 1;
                if (pageNumber < 0 || pageNumber >= pageCount) {
                    throw new Error('Invalid page number');
                }
                
                const newPdf = await PDFDocument.create();
                const [page] = await newPdf.copyPages(pdfDoc, [pageNumber]);
                newPdf.addPage(page);
                
                const pdfBytes = await newPdf.save();
                results.push({
                    name: `page_${pageNumber + 1}.pdf`,
                    blob: new Blob([pdfBytes], { type: 'application/pdf' })
                });
                
            } else if (splitMode === 'range') {
                const startPage = parseInt(document.getElementById('startPage').value) - 1;
                const endPage = parseInt(document.getElementById('endPage').value) - 1;
                
                if (startPage < 0 || endPage >= pageCount || startPage > endPage) {
                    throw new Error('Invalid page range');
                }
                
                const newPdf = await PDFDocument.create();
                const pageIndices = Array.from({ length: endPage - startPage + 1 }, (_, i) => startPage + i);
                const pages = await newPdf.copyPages(pdfDoc, pageIndices);
                pages.forEach(page => newPdf.addPage(page));
                
                const pdfBytes = await newPdf.save();
                results.push({
                    name: `pages_${startPage + 1}-${endPage + 1}.pdf`,
                    blob: new Blob([pdfBytes], { type: 'application/pdf' })
                });
                
            } else { // split every page
                for (let i = 0; i < pageCount; i++) {
                    const newPdf = await PDFDocument.create();
                    const [page] = await newPdf.copyPages(pdfDoc, [i]);
                    newPdf.addPage(page);
                    
                    const pdfBytes = await newPdf.save();
                    results.push({
                        name: `page_${i + 1}.pdf`,
                        blob: new Blob([pdfBytes], { type: 'application/pdf' })
                    });
                }
            }
            
            return results;
        }
        
        async function compressPdf() {
            // In a real implementation, this would use a PDF compression library
            // This is a simplified version that just returns the original
            // since client-side PDF compression is limited
            
            if (files.length !== 1 || files[0].type !== 'application/pdf') {
                throw new Error('Please select exactly one PDF file');
            }
            
            // Simulate compression by just returning the original for demo purposes
            return {
                name: 'compressed_' + files[0].name,
                blob: files[0]
            };
        }
        
        // Helper functions for tool options
        function setupSplitPdfOptions() {
            const splitMode = document.getElementById('splitMode');
            const pageNumberGroup = document.getElementById('pageNumberGroup');
            const pageRangeGroup = document.getElementById('pageRangeGroup');
            
            splitMode.addEventListener('change', () => {
                if (splitMode.value === 'single') {
                    pageNumberGroup.style.display = 'block';
                    pageRangeGroup.style.display = 'none';
                } else if (splitMode.value === 'range') {
                    pageNumberGroup.style.display = 'none';
                    pageRangeGroup.style.display = 'block';
                } else {
                    pageNumberGroup.style.display = 'none';
                    pageRangeGroup.style.display = 'none';
                }
            });
        }
        
        function setupCompressOptions() {
            const qualityInput = document.getElementById('quality');
            const qualityValue = document.getElementById('qualityValue');
            
            qualityInput.addEventListener('input', () => {
                qualityValue.textContent = qualityInput.value;
            });
        }
        
        // Show results
        function showResult(result) {
            resultsDiv.innerHTML = '';
            
            if (Array.isArray(result)) {
                result.forEach((res, index) => {
                    const resultItem = document.createElement('div');
                    resultItem.className = 'result-item';
                    resultItem.innerHTML = `
                        <span>${res.name}</span>
                        <div>
                            <a href="#" class="download-btn" data-index="${index}">Download</a>
                        </div>
                    `;
                    resultsDiv.appendChild(resultItem);
                });
            } else {
                const resultItem = document.createElement('div');
                resultItem.className = 'result-item';
                resultItem.innerHTML = `
                    <span>${result.name}</span>
                    <div>
                        <a href="#" class="download-btn">Download</a>
                    </div>
                `;
                resultsDiv.appendChild(resultItem);
            }
            
            // Add download handlers
            document.querySelectorAll('.download-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.preventDefault();
                    const index = btn.getAttribute('data-index');
                    
                    if (Array.isArray(result)) {
                        downloadFile(result[index].name, result[index].blob);
                    } else {
                        downloadFile(result.name, result.blob);
                    }
                });
            });
            
            resultsDiv.style.display = 'block';
        }
        
        function downloadFile(filename, blob) {
            // Using downloadjs library for cross-browser download support
            download(blob, filename, blob.type);
        }
    </script>
</body>
</html>
