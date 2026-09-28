- [Ask](#ask)
  - [vllm với llm khác gì nhau?](#vllm-với-llm-khác-gì-nhau)
  - [So sánh vLLM và Ollama](#so-sánh-vllm-và-ollama)
---
# Ask
## vllm với llm khác gì nhau?
```bash
LLM là “mô hình AI”, còn vLLM là “hệ thống/runtime để chạy và phục vụ LLM”.

LLM (Large Language Model) là bản thân mô hình AI:
    ví dụ:
        - Llama 3
        - Qwen
        - Mistral
        - Gemma
        - GPT
-> LLM chứa các weights/parameters đã được train để dự đoán token tiếp theo.

vLLM không phải một LLM. Nó là một inference engine / serving framework giúp bạn chạy LLM hiệu quả hơn trên GPU.
    Ví dụ: Request -> vLLM -> LLM -> Response
```
## So sánh vLLM và Ollama
```bash
	                    Ollama	                        vLLM
Bản chất	            Runtime/API server	            Inference/serving engine
Mục tiêu chính	        Dễ chạy LLM local	            Serving LLM hiệu năng cao
Dễ setup	            ⭐⭐⭐⭐⭐	                ⭐⭐⭐
GPU	                    Có	                            Có, rất tập trung vào GPU
API	                    Có API	                        Có OpenAI-compatible API
Multi-user	            Có nhưng không phải trọng tâm	Rất phù hợp
Throughput	            Tốt	                            Rất cao
Production              Có thể	                        Rất phù hợp
Development/local	    Rất tiện	                    Có thể
Continuous batching	    Không phải điểm mạnh chính	    Điểm mạnh
```