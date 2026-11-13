---
layout: page
title: Home
permalink: /
---

# Scientific & Engineering Projects
このサイトでは、研究開発の過程で作成したソフトウェア、電子回路、実験装置、機械設計などを紹介します。

衛星システムの解析、
画像検出器の制御、実験・計測技術、
CADを用いた機械設計など、さまざまな成果を扱います。

比較的大規模なシステムから、特定の作業を効率化するための小さなツールまで、
実際の開発や実験を通じて作成したものを整理し、順次公開していく予定です。

---

## Featured Systems

複数の技術要素を組み合わせた、比較的大規模な開発成果です。

### [Satellite Orbit, Attitude & Thermal Analysis]({{ '/systems/satellite-thermal/' | relative_url }})

人工衛星の軌道、姿勢、熱環境を統合的に解析するための計算ツール群。

- TLEを用いた軌道計算
- 衛星姿勢と太陽・地球方向の計算
- 光線追跡による放射形態係数（View Factor）の計算
- 衛星搭載放熱板の熱解析

### CMOS Detector Readout & Control System

CMOS-ROICを持つ検出器の駆動、信号取得、データ保存を行うシステム。

- 検出器駆動・ADC電子回路
- FPGAによるクロック生成とデータ取得
- Zynq上のLinuxとFPGAの統合制御

### Cryogenic Detector Test System

科学観測用検出器の性能評価に使用する冷却真空試験システム。

- 冷却真空装置の機械設計
- 冷却性能の改善
- 温度・真空度の監視
- 試験装置の制御とデータ記録

---

## Explore by Topic

開発成果を技術分野別に分類しています。

### Spacecraft Analysis & Simulation

衛星の軌道、姿勢、放射・熱環境に関する数値計算とシミュレーション。

- Ray Tracing
- Radiative View Factor Calculation
- Satellite Orbit Propagation from TLE
- Spacecraft Attitude Calculation
- Spacecraft Radiator Thermal Analysis

### Detector Electronics & FPGA Systems

検出器の駆動、信号処理、データ取得に関する電子回路と制御技術。

- CMOS Detector Driver & ADC Electronics
- FPGA-based Detector Control
- Zynq Linux/FPGA Control System
- Raspberry Pi Pico Clock Tester

### Experimental & Cryogenic Systems

科学観測機器の試験に使用する装置の設計と性能改善。

- Cryogenic Vacuum Test Chamber
- Cryogenic Performance Improvements
- Thermal Design for Experimental Apparatus

### Instrument Control & Measurement Software

各種計測器をコンピュータから制御し、測定データを取得・記録するためのソフトウェア。

- Digital Storage Oscilloscope Control
- PW18 Power Supply Control
- Lake Shore Temperature Controller
- Vacuum Gauge Data Acquisition

### CAD, Mechanical Design & Fabrication

CADを利用した設計支援ツールと、実験・製作に役立つ機械部品や治具。

- FreeCAD Assembly Integration Tool
- Twisted-wire Making Machine
- D-sub Connector Covers
- 3D-printed Laboratory Tools

---

## About This Collection

ここで紹介する成果は、研究開発の実務上の必要から作成されたものです。

それぞれのプロジェクトについて、開発の目的、基本的な仕組み、使用方法、設計資料、
ソースコードなどを、公開可能な範囲で提供します。

各プロジェクトの公開準備が整い次第、GitHubリポジトリへのリンクを追加します。

