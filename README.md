# Khata AI training

Ye "training" model ko hazaron examples dikhata hai: "Ahmed ne 500 diye" -> `add_payment`, "add capital 2000" -> `add_capital`, Roman Urdu + English, edit/view mode, missing amount par sawal, delete par inkaar.

## Steps
1. PC par `python generate_dataset.py` (ya ready files use karein). Ye `train.jsonl` (7,600) aur `eval.jsonl` (400) banata hai.
2. colab.research.google.com > New notebook > T4 GPU. Pehle cell: `!pip install unsloth`
3. Upload: `train.jsonl, eval.jsonl, tools_edit.json, tools_view.json, train_colab.py`, phir cell mein `%run train_colab.py`
4. Training ke baad `khata-ai-gguf/` folder ki `.gguf` file apne PC par download karein.
5. PC par pehle apne asli model ka template nikalein:  `ollama show qwen2.5:3b --modelfile`
6. Ek `Modelfile` banayein: `FROM ./model.gguf` (apni file ka naam) aur upar wale output ki `TEMPLATE` aur `PARAMETER` lines paste karein. Phir:
   `ollama create khata-ai -f Modelfile`
7. App > Settings > Khata AI > Test connection > Model mein `khata-ai` chunein.

## Zaroori baatein
- Dataset synthetic hai. Apne **asli** customer names, products aur apne bolne ke jumle `generate_dataset.py` ki lists (NAMES, ITEMS, EXP aur phrases) mein daal kar dobara generate karein. Jitna asli data, utni behtar accuracy.
- Agar `ai.js` ke tools ya system prompt badlein (naya tool wagairah), to `generate_dataset.py` mein bhi wahi badlav karke dobara train karein, warna model purane tools yaad rakhega.
- Training ke baad bhi AI confirm card ke bagair kuch save nahi kar sakta; ye safety app ke code mein hai.
- GPU na ho aur model kamzor lage, to bina training ke `ollama pull qwen2.5:7b` (bada model) bhi try karein, 8GB+ RAM chahiye.
