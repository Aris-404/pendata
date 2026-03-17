# Data Preparation

<div id="jb-print-docs-body" class="onlyprint">
    <h1>Missing Values Inputation dan normalisasi data</h1>
    <!-- Table of contents -->
    <div id="print-main-content">
        <div id="jb-print-toc">
            
            <div>
                <h2> Contents </h2>
            </div>
            <nav aria-label="Page">
                <ul class="visible nav section-nav flex-column">
<li class="toc-h2 nav-item toc-entry"><a class="reference internal nav-link" href="#missing-values-inputation-dengan-metode-wknn">1. Missing values inputation dengan metode WKNN</a><ul class="nav section-nav flex-column">
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#langkah-langkah-melakukan-metode-wknn">Langkah-langkah melakukan metode WKNN:</a><ul class="nav section-nav flex-column">
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#rumus-normalisasi-data-min-max-method">Rumus normalisasi data (min-max method)</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#rumus-similarity-pada-wknn">Rumus Similarity pada WKNN</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#rumus-perhitungan-nilai-imputasi">Rumus perhitungan nilai imputasi</a></li>
</ul>
</li>
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#dataset-yang-digunakan">Dataset yang digunakan</a><ul class="nav section-nav flex-column">
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#penjelasan-masing-masing-fitur-dan-class">Penjelasan masing-masing fitur dan class:</a></li>
</ul>
</li>
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#perhitungan-wknn-secara-manual">Perhitungan WKNN secara manual</a><ul class="nav section-nav flex-column">
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menentukan-missing-values">1. Menentukan missing values</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#melakukan-normalisasi-data">2. Melakukan normalisasi data</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menghitung-nilai-similarity">3. Menghitung nilai similarity</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menghitung-penyebut">4. Menghitung penyebut</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menghitung-pembilang">5. Menghitung pembilang</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menghitung-hasil-nilai-imputasi">6. Menghitung hasil nilai imputasi</a></li>
</ul>
</li>
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#perhitungan-wknn-menggunaka-python">Perhitungan WKNN menggunaka python</a><ul class="nav section-nav flex-column">
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#setting-library-dan-akses-file-dalam-drive">1. Setting library dan akses file dalam drive</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menentukan-path-drive-dan-melihat-beberapa-data-teratas">2. Menentukan path drive dan melihat beberapa data teratas</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#id1">3. Menentukan missing values</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#mengetahui-nilai-min-max-masing-masing-kolom">4. Mengetahui nilai Min-Max masing masing kolom</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#normalisasi-data">5. Normalisasi data</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menghitung-nilai-similaritas">6. Menghitung nilai similaritas</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#id2">7. Menghitung penyebut</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#id3">8. Menghitung pembilang</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#menghitung-nilai-imputasi">9. Menghitung nilai imputasi</a></li>
</ul>
</li>
</ul>
</li>
<li class="toc-h2 nav-item toc-entry"><a class="reference internal nav-link" href="#id4">2. Normalisasi data</a><ul class="nav section-nav flex-column">
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#materi-normalisasi-data">1. Materi normalisasi data</a></li>
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#macam-macam-normalisasi-data">2. Macam-macam normalisasi data</a><ul class="nav section-nav flex-column">
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#min-max-normalization">1. Min-Max Normalization</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#z-score-normalization">2. Z-score normalization</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#decimal-scaling-normalization">3. Decimal scaling normalization</a></li>
</ul>
</li>
<li class="toc-h3 nav-item toc-entry"><a class="reference internal nav-link" href="#normalisasi-data-menggunakan-python-dengan-library-scikit-learn">3. Normalisasi data menggunakan python dengan library Scikit-learn</a><ul class="nav section-nav flex-column">
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#id5">1. Min-max normalization</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#id6">2. Z-score normalization</a></li>
<li class="toc-h4 nav-item toc-entry"><a class="reference internal nav-link" href="#id7">3. Decimal scaling normalization</a></li>
</ul>
</li>
</ul>
</li>
</ul>
            </nav>
        </div>
    </div>
</div>

              
                
<div id="searchbox"></div>
                <article class="bd-article">
                  
  <section class="tex2jax_ignore mathjax_ignore" id="missing-values-inputation-dan-normalisasi-data">
<h1>Missing Values Inputation dan normalisasi data<a class="headerlink" href="#missing-values-inputation-dan-normalisasi-data" title="Link to this heading">#</a></h1>
<section id="missing-values-inputation-dengan-metode-wknn">
<h2>1. Missing values inputation dengan metode WKNN<a class="headerlink" href="#missing-values-inputation-dengan-metode-wknn" title="Link to this heading">#</a></h2>
<p>Missing values adalah suatu kondisi dimana dataset yang dimiliki memiliki nilai atribut yang tidak tersedia atau kosong. Hal itu akan memengaruhi kualitas suatu data, sehingga ada metode yang dapat digunakan untuk mengisi atau lebih tepatnya memperkirakan untuk mengisi missing values tersebut. Salah satu metode yang dapat digunakan adalah Weighted K-Nearest Neighbour (WKNN).</p>
<p>Metode WKNN merupakan pengembangan dari metode K-Nearest Neighbour (KNN) yang digunakan untuk melakukan imputasi nilai yang hilang berdasarkan kemiripan antar data. Pada metode ini nilai yang hilang diperkirakan denggan tetangga terdekat (nearest neighbours) yang memiliki kemiripan tertinggi. Perbedaan utama antara KNN dengan WKNN terletak pada pemberian bobot untuk setiap tetangga, dalam WKNN data yang jaraknya dekat akan diberikan bobot lebih besar dibandingkan jarak yang jauh.</p>
<section id="langkah-langkah-melakukan-metode-wknn">
<h3>Langkah-langkah melakukan metode WKNN:<a class="headerlink" href="#langkah-langkah-melakukan-metode-wknn" title="Link to this heading">#</a></h3>
<ol class="arabic simple">
<li><p>Mengidentifikasi missing values pada data</p></li>
<li><p>Melakukan normalisasi data</p></li>
<li><p>Menghitung similarity antar data</p></li>
<li><p>Menentukan beberapa tetangga terdekat (K tetangga)</p></li>
<li><p>Menghitung nilai imputasi</p></li>
</ol>
<section id="rumus-normalisasi-data-min-max-method">
<h4>Rumus normalisasi data (min-max method)<a class="headerlink" href="#rumus-normalisasi-data-min-max-method" title="Link to this heading">#</a></h4>
<div class="math notranslate nohighlight">
\[
x' = \frac{x - x_{min}}{x_{max} - x_{min}}
\]</div>
<p>Keterangan:</p>
<ul class="simple">
<li><p><span class="math notranslate nohighlight">\(x\)</span> : nilai data asli</p></li>
<li><p><span class="math notranslate nohighlight">\(x_{min}\)</span> : nilai minimum pada atribut</p></li>
<li><p><span class="math notranslate nohighlight">\(x_{max}\)</span> : nilai maksimum pada atribut</p></li>
<li><p><span class="math notranslate nohighlight">\(x'\)</span> : nilai hasil normalisasi</p></li>
</ul>
</section>
<section id="rumus-similarity-pada-wknn">
<h4>Rumus Similarity pada WKNN<a class="headerlink" href="#rumus-similarity-pada-wknn" title="Link to this heading">#</a></h4>
<div class="math notranslate nohighlight">
\[
S_i = \frac{1}{\sum (Y_{ih} - Y_{jh})^2}
\]</div>
<p>Keterangan:</p>
<ul class="simple">
<li><p><span class="math notranslate nohighlight">\(S_i\)</span> : nilai similarity antara data ke-<span class="math notranslate nohighlight">\(i\)</span> dan data ke-<span class="math notranslate nohighlight">\(j\)</span></p></li>
<li><p><span class="math notranslate nohighlight">\(Y_{ih}\)</span> : nilai atribut ke-<span class="math notranslate nohighlight">\(h\)</span> pada data yang memiliki missing value</p></li>
<li><p><span class="math notranslate nohighlight">\(Y_{jh}\)</span> : nilai atribut ke-<span class="math notranslate nohighlight">\(h\)</span> pada data tetangga</p></li>
</ul>
</section>
<section id="rumus-perhitungan-nilai-imputasi">
<h4>Rumus perhitungan nilai imputasi<a class="headerlink" href="#rumus-perhitungan-nilai-imputasi" title="Link to this heading">#</a></h4>
<div class="math notranslate nohighlight">
\[
\hat{y}_{ih} =
\frac{\sum_{j \in I_{kih}} s_i(y_j)\, y_{jh}}
{\sum_{j \in I_{kih}} s_i(y_j)}
\]</div>
<p>Keterangan:</p>
<ul class="simple">
<li><p><span class="math notranslate nohighlight">\(\hat{y}_{ih}\)</span> : nilai imputasi pada atribut ke-<span class="math notranslate nohighlight">\(h\)</span> dari data ke-<span class="math notranslate nohighlight">\(i\)</span></p></li>
<li><p><span class="math notranslate nohighlight">\(I_{kih}\)</span> : himpunan indeks dari <span class="math notranslate nohighlight">\(k\)</span> tetangga terdekat</p></li>
<li><p><span class="math notranslate nohighlight">\(s_i(y_j)\)</span> : nilai similarity antara data <span class="math notranslate nohighlight">\(i\)</span> dan data tetangga <span class="math notranslate nohighlight">\(j\)</span></p></li>
<li><p><span class="math notranslate nohighlight">\(y_{jh}\)</span> : nilai atribut ke-<span class="math notranslate nohighlight">\(h\)</span> dari data tetangga ke-<span class="math notranslate nohighlight">\(j\)</span></p></li>
</ul>
<p>Perlu diingat dalam metode ini, penentuan tetangga terdekat tidak ada metode pasti atau jumlah pasti yang digunakan, semuanya tergantung kebutuhan dataset tersebut.</p>
</section>
</section>