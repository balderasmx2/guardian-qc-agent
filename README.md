GUARDIAN — Creative Asset Intelligence

PMG AI & Tech Sandbox Global Hackathon 2026

Brief 3: Intelligence to Action


"The distance between insight and action is where competitive advantage is lost every day."



GUARDIAN is a local AI agent that monitors incoming creative assets, diagnoses brand safety risks, and triggers immediate action — without a human in the middle.

The Loop


Signal In — AI creative assets arrive via watch folder (Kling, Runway, Sora, production pipeline)
Intelligence Out — ffprobe + ffmpeg diagnose what is wrong and WHY. Not just "18fps" — "this will cause timing drift in your 24fps timeline and will be rejected at delivery"
Action Taken — PDF QC report generated automatically. Team notified with exact issue and recommended fix.
Loop Closed — From file arriving to team notified. Zero humans in the middle. Seconds, not hours.


What GUARDIAN Diagnoses

CheckMethodConfidenceResolution (4K, 2K, 1080p)ffprobeExactAsymmetric resolution (3840x1080)ffprobeExactFrame rate outliers (18fps, 39fps)ffprobeExactAudio sample rate (44.1kHz vs 48kHz)ffprobeExactMissing audio trackffprobeExactShort clip under 1 secondffprobeExactBlack framesffmpeg blackdetectConfirmedFreeze framesffmpeg freezedetectConfirmedSHA-256 provenance hashsha256sumExact

Validated Results


47 real M&E production files scanned — June 2026
5 critical issues diagnosed with evidence
49-page PDF report generated automatically
0 cloud API calls required
0 humans in the loop


Hardware

Dell GB10 Grace Blackwell — 128GB unified memory — NVIDIA GB10 GPU — Ubuntu Linux — Runs entirely offline

Stack


Hermes Agent (NousResearch) — AI agent runtime
Qwen3.6-35B-A3B-FP8 — local LLM via vLLM
ffprobe / ffmpeg — video analysis
sha256sum — provenance hashing
fpdf2 / Python — report generation


Run

Start vLLM:

HF_HUB_OFFLINE=1 TRANSFORMERS_OFFLINE=1 VLLM_USE_FLASHINFER_SAMPLER=0 vllm serve Qwen/Qwen3.6-35B-A3B-FP8 --host 0.0.0.0 --port 9494 --dtype auto --max-model-len 65536 --max-num-seqs 1 --gpu-memory-utilization 0.35 --enable-auto-tool-choice --tool-call-parser qwen3_coder --enforce-eager

Start Hermes Agent:

source ~/.bashrc && hermes

QC Prompt:

Scan [folder] for mp4 files. For each: run ffprobe to get resolution, fps, codec, audio sample rate, duration. Flag FAIL if not 4K, not 24fps, audio not 48kHz, or duration under 1 second. Generate PDF report. Helvetica font only.

Data Sovereignty

All processing runs locally on Dell GB10. No assets uploaded to any cloud. No API calls with production footage. Full NDA compliance. Works completely offline.


Gil Balderas —  M&E Filmmaker — shotlock.tech
