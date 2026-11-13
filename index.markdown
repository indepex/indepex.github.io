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

### [On-Orbit Radiator Analysis]({{ '/systems/on-orbit-radiator-analysis/' | relative_url }})

低軌道衛星に搭載する放熱板の設計を対象に、軌道・姿勢・放射結合・熱収支を一連の流れとして評価する解析例。

- TLE・SGP4を用いた軌道計算と衛星姿勢の計算
- 地球赤外放射の入射方向分布の評価
- 反射型熱シールドの形状設計と遮蔽性能の比較
- 3次元光線追跡による放射結合係数の計算
- 放熱板の熱入力と正味冷却能力の概算

[計算コード・実行例（GitHub）](https://github.com/indepex/on-orbit-radiator-analysis)

### CMOS Detector Readout & Control System（公開準備中）

CMOS-ROICを持つ検出器の駆動、信号取得、データ保存を行うシステム。

- 検出器駆動・ADC電子回路
- FPGAによるクロック生成とデータ取得
- Zynq上のLinuxとFPGAの統合制御

### Cryogenic Detector Test System（公開準備中）

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

公開済みのプロジェクトには解説ページやGitHubリポジトリへのリンクを設けています。その他の項目は準備が整い次第、順次公開します。

