<h1>TinyLLaMA Fine-Tuning</h1>

<h2>Overview</h2>
<p>
This project fine-tunes <strong>TinyLLaMA</strong> on a custom domain-specific dataset using <strong>Google Colab</strong>. 
The model is adapted for specialized text generation and Q&A tasks while remaining lightweight and GPU-efficient with 
<strong>4-bit quantization (BitsAndBytes)</strong>.
</p>

<h2>Features</h2>
<ul>
  <li>Fine-tuning done completely on Google Colab</li>
  <li>TinyLLaMA model with 4-bit quantization</li>
  <li>Uses Hugging Face Transformers</li>
  <li>Supports custom datasets for domain-specific tasks</li>
  <li>Lightweight and resource-friendly workflow</li>
</ul>

<h2>Setup (Colab)</h2>

<h3>1. Open Google Colab</h3>
<p>No local setup is required. Open the notebook directly in Colab.</p>

<h3>2. Install Dependencies</h3>

<pre><code>!pip install transformers accelerate bitsandbytes peft
</code></pre>

<h2>Dataset Format</h2>
<p>Upload your dataset to Colab in <strong>Instruction-Response</strong> <code>.jsonl</code> format:</p>

<pre><code>{
  "instruction": "What is the market price of the 2019 Hyundai Santro?",
  "response": "The 2019 Hyundai Santro has listed price: 300000.0."
}
</code></pre>

<h2>Training Pipeline</h2>
<ul>
  <li>Load TinyLLaMA with 4-bit quantization</li>
  <li>Prepare data (upload to Colab or use Google Drive)</li>
  <li>Fine-tune the model using Hugging Face Trainer or PEFT (LoRA optional)</li>
  <li>Save the fine-tuned model to Google Drive or local storage</li>
</ul>

<h2>Usage Example</h2>

<pre><code>from transformers import AutoTokenizer, AutoModelForCausalLM

tokenizer = AutoTokenizer.from_pretrained("/content/final_model")
model = AutoModelForCausalLM.from_pretrained("/content/final_model")

prompt = "Explain transfer learning."
inputs = tokenizer(prompt, return_tensors="pt").to("cuda")
outputs = model.generate(**inputs, max_new_tokens=100)

print(tokenizer.decode(outputs[0], skip_special_tokens=True))
</code></pre>

<h2>Model Card</h2>

<table>
  <tr>
    <th>Field</th>
    <th>Details</th>
  </tr>
  <tr>
    <td>Model</td>
    <td>TinyLLaMA (fine-tuned)</td>
  </tr>
  <tr>
    <td>Task</td>
    <td>Text generation / Q&amp;A</td>
  </tr>
  <tr>
    <td>Quantization</td>
    <td>4-bit (BitsAndBytes)</td>
  </tr>
  <tr>
    <td>Environment</td>
    <td>Google Colab</td>
  </tr>
  <tr>
    <td>Dataset</td>
    <td>Custom Instruction-Response pairs</td>
  </tr>
</table>

<h2>License</h2>
<p>This project is released under the <strong>MIT License</strong>.</p>
