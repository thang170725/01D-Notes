Bài tập
Demo Fine-Tune Chatbot Hỏi-Đáp bằng transformer
from transformers import AutoTokenizer, AutoModelForCausalLM, Trainer, TrainingArguments
from datasets import load_dataset

model_name = "Qwen/Qwen2.5-7B-Instruct"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

# Load dữ liệu
dataset = load_dataset("csv", data_files={"train": "data.csv"})

# Tokenize
def preprocess(example):
    text = f"### User: {example['input']}\n### Assistant: {example['response']}"
    tokens = tokenizer(text, truncation=True, padding="max_length", max_length=512)
    tokens["labels"] = tokens["input_ids"].copy()  # labels = input_ids cho LM
    return tokens

tokenized_dataset = dataset["train"].map(preprocess, batched=False)

# Training
training_args = TrainingArguments(
    output_dir="./chatbot_model",
    per_device_train_batch_size=2,
    num_train_epochs=1,
    save_steps=100,
    logging_steps=10,
    fp16=True  # nếu GPU hỗ trợ
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_dataset
)

trainer.train()