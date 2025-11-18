# Triton inference

Run code:
```
docker compose up -d
uvicorn api:app --reload --port 5000
```
After launch, API documentation is available here - http://127.0.0.1:5000/docs

---
To get to trtexec_container terminal:
```
docker exec -it trtexec_container bash
```
Command for ONNX -> TensorRT conversion:
```
trtexec --onnx=model.onnx --saveEngine=model.plan --minShapes=input:1x3x224x224 --optShapes=input:8x3x224x224 --maxShapes=input:16x3x224x224 --fp16 --useSpinWait --outputIOFormats=fp16:chw --inputIOFormats=fp16:chw
```
---
To test the performance of your API using the Locust tool:
```
locust -f test_locust.py --host=http://127.0.0.1:5000
```
Other testing files: test_async.py и test_usual.py