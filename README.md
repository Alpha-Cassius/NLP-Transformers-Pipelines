<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NLP Pipelines with Transformers</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-glow: #8a2be2;
            --secondary-glow: #00d2ff;
            --text-main: #ffffff;
            --text-muted: #b3b3b3;
            --glass-bg: rgba(255, 255, 255, 0.05);
            --glass-border: rgba(255, 255, 255, 0.1);
            --accent-color: #a8c0ff;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
            background: radial-gradient(circle at bottom, #0f0c29, #302b63, #24243e);
            color: var(--text-main);
            min-height: 100vh;
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* Animated Background Orbs */
        .orb {
            position: fixed;
            border-radius: 50%;
            filter: blur(80px);
            z-index: -1;
            animation: float 20s infinite alternate ease-in-out;
        }
        
        .orb-1 { width: 300px; height: 300px; background: var(--primary-glow); top: 10%; left: 20%; }
        .orb-2 { width: 400px; height: 400px; background: var(--secondary-glow); bottom: 10%; right: 15%; animation-delay: -5s; }

        @keyframes float {
            0% { transform: translate(0, 0) scale(1); }
            50% { transform: translate(50px, 50px) scale(1.2); }
            100% { transform: translate(-50px, 100px) scale(0.9); }
        }

        /* Layout & Glassmorphism */
        .container {
            max-width: 900px;
            margin: 50px auto;
            padding: 20px;
        }

        .glass-panel {
            background: var(--glass-bg);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            padding: 40px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
            animation: slideUp 1s ease-out forwards;
            opacity: 0;
            transform: translateY(30px);
        }

        @keyframes slideUp {
            to { opacity: 1; transform: translateY(0); }
        }

        /* Header Alignment */
        .header-content {
            text-align: center;
        }

        .hero-img {
            max-width: 100%;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            margin-bottom: 20px;
            transition: transform 0.3s ease;
        }
        
        .hero-img:hover {
            transform: scale(1.02);
        }

        /* Typography */
        h1 {
            font-size: 2.8rem;
            background: linear-gradient(to right, #e0c3fc, #8ec5fc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 5px;
            animation: pulseText 3s infinite alternate;
        }

        h3 {
            color: var(--text-muted);
            font-weight: 400;
            margin-top: 0;
            margin-bottom: 20px;
        }

        @keyframes pulseText {
            0% { text-shadow: 0 0 10px rgba(224, 195, 252, 0.2); }
            100% { text-shadow: 0 0 20px rgba(142, 197, 252, 0.6); }
        }

        h2 {
            font-size: 1.8rem;
            border-bottom: 2px solid var(--glass-border);
            padding-bottom: 10px;
            margin-bottom: 20px;
            color: var(--accent-color);
        }

        /* Badges */
        .badges {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
            margin: 20px 0;
        }
        
        .badges img {
            border-radius: 6px;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        .badges img:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(138, 43, 226, 0.4);
        }

        /* Lists */
        ul, ol { padding-left: 20px; }
        
        li {
            margin-bottom: 15px;
            padding: 10px;
            border-radius: 8px;
            transition: background 0.3s ease, transform 0.3s ease;
        }

        .feature-list li {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid transparent;
        }

        .feature-list li:hover {
            background: rgba(255, 255, 255, 0.08);
            border-color: rgba(255, 255, 255, 0.2);
            transform: translateX(10px);
        }

        strong { color: var(--accent-color); }

        /* Grid for 'What I'm Building' */
        .grid-2x2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 20px;
        }

        .grid-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid var(--glass-border);
            border-radius: 12px;
            padding: 20px;
            transition: transform 0.3s ease, background 0.3s ease;
        }

        .grid-card:hover {
            transform: translateY(-5px);
            background: rgba(255, 255, 255, 0.08);
            border-color: var(--accent-color);
        }
        
        .grid-card h3 {
            color: #fff;
            margin-top: 0;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* Table Styling for Tech Stack */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid var(--glass-border);
        }
        
        th { color: var(--accent-color); }
        tr:last-child td { border-bottom: none; }
        
        /* Code styling */
        code {
            background: rgba(0, 0, 0, 0.5);
            padding: 2px 6px;
            border-radius: 4px;
            color: #00ffcc;
            font-family: 'Courier New', Courier, monospace;
        }

        /* Links */
        a {
            color: var(--accent-color);
            text-decoration: none;
            transition: text-shadow 0.3s ease;
        }
        
        a:hover {
            text-shadow: 0 0 8px var(--accent-color);
            text-decoration: underline;
        }

        /* Footer */
        .footer {
            text-align: center;
            margin-top: 40px;
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        /* Animations Staggering */
        .delay-1 { animation-delay: 0.2s; }
        .delay-2 { animation-delay: 0.4s; }
        .delay-3 { animation-delay: 0.6s; }

        @media (max-width: 768px) {
            .grid-2x2 { grid-template-columns: 1fr; }
            h1 { font-size: 2.2rem; }
        }
    </style>
</head>
<body>

    <!-- Background Orbs -->
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>

    <div class="container">
        
        <!-- Header Section -->
        <div class="glass-panel header-content">
            <img src="https://substackcdn.com/image/fetch/$s_!OHaK!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F7485933d-06de-47d1-a3f1-734b0d379df4_1200x630.jpeg" alt="NLP using transformers animated graduation portrait" class="hero-img">
            <h1>NLP Pipelines with Transformers</h1>
            <h3>From Scratch to Advanced Colab Implementations</h3>
            
            <div class="badges">
                <a href="https://github.com/alpha-cassius"><img src="https://img.shields.io/badge/AUTHOR-Vaibhav_Pandey-22d3ee?style=for-the-badge&labelColor=0d1117" alt="AUTHOR"></a>
                <a href="https://github.com/alpha-cassius?tab=repositories"><img src="https://img.shields.io/badge/OPEN_SOURCE-7c3aed?style=for-the-badge&labelColor=0d1117" alt="OPEN SOURCE"></a>
                <img src="https://img.shields.io/badge/BUILDING-34d399?style=for-the-badge&labelColor=0d1117" alt="BUILDING">
            </div>
            
            <p style="font-weight: 600; letter-spacing: 1px;">AI & ML | Python Developer | Robotics Enthusiast</p>
        </div>

        <!-- The Mission Section -->
        <div class="glass-panel delay-1">
            <h2>🚀 The Mission: NLP with Transformers</h2>
            <p>Natural Language Processing (NLP) is how machines understand, generate, and manipulate human language. Before 2017, this was done using slow, sequential models like RNNs. Then, Google introduced the <strong>Transformer</strong> architecture in the landmark paper <em>"Attention Is All You Need."</em></p>
            <p>Transformers changed the field entirely by relying on <strong>Self-Attention mechanisms</strong>. Instead of reading a sentence word-by-word, a Transformer processes all tokens in parallel, calculating how strongly each word relates to every other word in the sequence. This architecture enables:</p>
            
            <ul class="feature-list">
                <li><strong>Massive Parallelization:</strong> Training on modern GPUs is exceptionally fast.</li>
                <li><strong>Long-range Context:</strong> It retains connections across lengthy documents without information degradation.</li>
                <li><strong>The Foundation for LLMs:</strong> This exact architecture powers modern giants like GPT, BERT, LLaMA, and Qwen.</li>
            </ul>
            <p>I built this repository to demonstrate how to implement production-ready NLP pipelines from scratch using <strong>Google Colab</strong>, <strong>PyTorch</strong>, and <strong>Hugging Face</strong>.</p>
        </div>

        <!-- What I'm Building Section -->
        <div class="glass-panel delay-2">
            <h2>🏗️ What I’m Building</h2>
            
            <div class="grid-2x2">
                <div class="grid-card">
                    <h3>⚡ Text Generation</h3>
                    <p>Using foundational models like <b>GPT-2</b> to predict and generate sequential text autonomously.</p>
                    <p><strong>Why it matters:</strong> The core mechanism behind AI chatbots and automated coding assistants.</p>
                </div>
                <div class="grid-card">
                    <h3>⚡ Sentiment Analysis</h3>
                    <p>Deploying fine-tuned classification models to instantly grade text as positive, negative, or neutral.</p>
                    <p><strong>Why it matters:</strong> Essential for analyzing user feedback, reviews, and social media trends at scale.</p>
                </div>
                <div class="grid-card">
                    <h3>⚡ Summarization & Translation</h3>
                    <p>Leveraging lightweight chat models (<b>Qwen1.5</b>) to condense massive documents and translate English to French.</p>
                    <p><strong>Why it matters:</strong> Solves information overload by extracting core insights across language barriers.</p>
                </div>
                <div class="grid-card">
                    <h3>⚡ Named Entity Recognition (NER)</h3>
                    <p>Using a <b>BERT-based pipeline</b> to scan unstructured text and extract Locations, Organizations, and People.</p>
                    <p><strong>Why it matters:</strong> Converts chaotic raw text data into structured, queryable databases.</p>
                </div>
            </div>

            <p style="text-align: center; margin-top: 30px;">
                <a href="https://github.com/alpha-cassius?tab=repositories"><b>Explore my repositories →</b></a> &nbsp;·&nbsp;
                <a href="https://github.com/alpha-cassius?tab=stars"><b>See open-source signal →</b></a>
            </p>
        </div>

        <!-- Technology Arsenal Section -->
        <div class="glass-panel delay-3">
            <h2>⚙️ Technology Arsenal</h2>
            <div style="text-align: center; margin-bottom: 20px;">
                <img src="https://www.gitskins.com/api/readme-reference/technology-stack?username=alpha-cassius&theme=github-dark&logos=Jupyter%20Notebook%2CPython%2CGitHub&v=signature-cap-tip-languages-3" alt="Technology stack" style="max-width: 100%; filter: drop-shadow(0 0 10px rgba(255,255,255,0.1));">
            </div>

            <table>
                <tr>
                    <th>Category</th>
                    <th>Technologies</th>
                </tr>
                <tr>
                    <td><strong>Languages & Tools</strong></td>
                    <td>Jupyter Notebook (Google Colab) · Python 3 · Hugging Face Transformers</td>
                </tr>
                <tr>
                    <td><strong>Model Ecosystem</strong></td>
                    <td>GPT-2 <em>(Generation)</em> · Qwen Chat <em>(QA/Summarization)</em> · BERT <em>(NER)</em></td>
                </tr>
                <tr>
