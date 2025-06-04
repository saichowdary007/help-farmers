# help-farmers

Large seed/chemical companies are already productizing “crop-advice copilots.” Bayer’s new E.L.Y. assistant, built with Microsoft Azure OpenAI + AI Search, lets agronomists ask questions about crop nutrition, pests, or Bayer labels in plain language. Bayer is actively licensing these domain-tuned models through the Azure model catalog, signaling demand (and room) for open-source competitors. 

Dataset
What’s inside
Typical tasks
Licence/size
USDA NASS Quick Stats & Agricultural Yield Survey
County-level acreage, yield & production for every major US crop since 1866. API or bulk .gz files.
Yield regression, price forecasting, anomaly detection.
Public domain, >2 GB compressed. 
FAO / ISRIC Soil Profile & Harmonized World Soil DB v 2.0
Millions of horizon-level measurements (pH, texture, organic C, bulk density) + 1 km global raster maps.
Soil-aware fertiliser recommendation, carbon-stock modelling.
CC-BY-SA; profiles ≈ 30 MB, rasters ≈ 11 GB. 
PlantVillage Leaf-Images
50 k–70 k high-res images of healthy & 30+ disease classes across 9 species.
Vision models for early disease detection on-device.
CC BY 4.0; ≈3 GB. 
(plus) Sentinel-2 / Landsat-8 open satellite tiles (Copernicus/USGS) for NDVI, soil-moisture proxies.


Field-level yield prediction
1. Pull NASS yield targets + Sentinel-2 NDVI patches. 2. Tabular baseline with LightGBM or TabPFN. 3. Move to Temporal Fusion Transformer (PyTorch Forecasting) when you add multiyear weather sequences.
Vision disease scout app
Fine-tune EfficientNet-B4 or ViT-Base on PlantVillage (→ 90 %+ F1). Export to ONNX + TensorFlow Lite so it runs offline on Android for farmers with poor connectivity.
Text Q&A agronomy copilot
1. Scrap public extension bulletins + Bayer-like labels.2. Store in FAISS or Azure AI Search.3. QLoRA-fine-tune Mistral-7B on 3–5 k self-generated Q-&-A pairs; wrap with a RAG scaffold so the LLM always cites retrieved docs.
Multi-modal assistant
Couple your vision model’s embedding head with a small language model via LLaVA-style alignment. Farmers snap a leaf photo + ask “What’s wrong and how do I treat it?”


