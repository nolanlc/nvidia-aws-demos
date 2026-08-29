# nvidia-aws-demos
Demo Nvidia AI Enterprise Stack on AWS

NVIDIA Enterprise Stack on AWS EKS — Single-Node Demo Guide
A complete, step-by-step guide for running inference (NVIDIA NIM) and fine-tuning (NVIDIA NeMo) on a single-node Amazon EKS cluster with GPU — using fractional GPU sharing via KAI Scheduler.

Every NVIDIA component in this demo is free. Your only costs are AWS infrastructure (~$27 for a 1-day demo).

🏗️ Architecture
┌─────────────────────────────────────────────────┐
│          AWS EKS Control Plane (managed)        │
└────────────────────────┬────────────────────────┘
           ┌─────────────▼─────────────┐
           │   g5.xlarge Worker Node   │
           │   1× NVIDIA A10G (24 GB)  │
           │                           │
           │   ┌─────────────────────┐ │
           │   │    KAI Scheduler    │ │
           │   │ (GPU Orchestration) │ │
           │   └────────┬────────────┘ │
           │   ┌────────▼────────────┐ │
           │   │   NVIDIA A10G GPU   │ │
           │   │  ┌───────┬───────┐  │ │
           │   │  │  NIM  │ NeMo  │  │ │
           │   │  │  50%  │  50%  │  │ │
           │   │  └───────┴───────┘  │ │
           │   └─────────────────────┘ │
           └───────────────────────────┘

🧩 Components
Component

Role

Cost

KAI Scheduler

Open-source GPU workload scheduling (Apache 2.0)

Free

NVIDIA NIM

Optimized inference microservices (Llama 3.1 8B)

Free (Developer Program)

NVIDIA NeMo

Model fine-tuning framework (LoRA)

Free (open source)

Amazon EKS

Managed Kubernetes control plane

~$0.10/hr

g5.xlarge

1× NVIDIA A10G GPU, 4 vCPUs, 16 GiB RAM

~$1.01/hr

🔑 Key Highlights
Fractional GPU sharing — NIM inference and NeMo fine-tuning run simultaneously on a single GPU via KAI Scheduler

LoRA fine-tuning — Parameter-efficient fine-tuning on a single GPU with as little as 16 GB VRAM

OpenAI-compatible API — NIM exposes a standard /v1/chat/completions endpoint

~$27 total cost for a full 1-day demo (tear down after use)

📋 Prerequisites
AWS CLI (configured with credentials)

kubectl v1.28+

eksctl (latest)

Helm 3.x

Git

NVIDIA Developer Program account (free)

NGC API Key

AWS service quota: ≥ 4 vCPUs for G and VT instances in your target region

🚀 Quick Start
The guide walks through 7 steps:

Create the EKS Cluster — Single-node GPU cluster with eksctl (~15–20 min)

Install GPU Operator — Automatic NVIDIA driver and toolkit setup (~5–10 min)

Install KAI Scheduler — Fractional GPU scheduling (~5 min)

Set Up NGC Credentials — Kubernetes secrets for NVIDIA container registry (~2 min)

Deploy NVIDIA NIM — Inference with Llama 3.1 8B Instruct (~10–15 min)

Fine-Tune with NeMo — LoRA fine-tuning on Dolly-15k dataset (~15–30 min)

Demonstrate GPU Sharing — Both workloads sharing a single GPU (~5 min)

📄 See the full guide: NVIDIA Enterprise Stack Demo Guide (PDF)

💰 Cost Summary
Scenario

Estimated Cost

1-day demo

~$27

1-week dev (24/7)

~$190

⚠️ Remember to tear down resources after your demo to avoid ongoing charges. Cleanup instructions are included in the guide.

📚 Resources
KAI Scheduler (GitHub)

NVIDIA NIM Documentation

NVIDIA NeMo Framework

NeMo User Guide

AWS EKS Documentation

AWS Blog: NIM on EKS

AWS Blog: Run:ai on EKS

📄 License
This demo guide is provided as-is for educational and demonstration purposes.
