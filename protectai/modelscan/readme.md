# Model Scan
ModelScan is an open source project that scans models to determine if they contain unsafe code. 
Enterprise version: Guardian will implemented on huggingface for model scan (https://huggingface.co/blog/protectai)

Additional features with Guardian (https://protectai.com/guardian):
- Detects serialization embedded in model layers	
- Detects model architectural backdoors in file formats without serialization risks	
- Block access to models that don’t comply with policies	
- SDK support for easy integration in CI/CD or model pipelines	
- Policy management for all models	
- Integration into model registries