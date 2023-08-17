# LLM-for-HDL

Objectives :
  1. Fine tune GPT-2 125M for VHDL code generation and summarization
  2. Build a gradle webapp for inferencing of the fine tuned model
  3. Fine tune a bigger model Llama 3B for VHDL code genaration and summarization and compare its performance with that of GPT-2

VHDL stands for VHSIC Hardware Description Language (yeah VHSIC is also an acronym🙂). It is a language used by hardware designers to synthesize digital hardware. <br>
I used [AWfaw/ai-hdlcoder-dataset-clean](https://huggingface.co/datasets/AWfaw/ai-hdlcoder-dataset-clean) dataset from huggingface to get the webscrapped VHDL code. Training the code with just VHDL code would enable the model to learn the grammer of VHDL but that doesn't serve our purpose. So I took assistance from GPT-3.5 to generate the summary of a set of VHDL files which I would use as my dataset. The finetuned GPT-2 125M model and corresponding tokenizer is available [here](https://huggingface.co/myn11/gpt2_hdl) <br> <br>

LLM_for_HDL.ipynb contains the data preprocessing, dataset generation and gpt-2 model fine tuning. In Gradio_App_GPT_2_HDL.ipynb I have built a gradion webapp to interact with the finetuned model. <br>

Results :
  1. The LLM was able to learn the grammer of the VHDL language (resverved words, semicolon,..etc ) but it was not able to generate meaningful code
  2. The model performed "fine" in summarizing small codes (like simple ROM block) but failed to do so with large code
One possibel reason can be that gpt-2 125M is too small a model to summarize and generate complex VHDL code. So I went on to fine tune Llama 3B model
<br>
<br>
Llama-3B is too big a model to train in a single T100 GPU instance with 15GB RAM. So, I employed qLoRA (quantized low-rank adapters. paper - https://arxiv.org/abs/2305.14314v1) to train it.
Llama-3b.ipynb file has the code for fine tuning of llama-3b. As it can be seen in training details the Llama-3b fine tuning clearly beats the gpt-2 and reasonably so.
