# End-to-End-AI-Voice-Assistance-Pipeline

## Overview
This notebook implements an end-to-end AI-powered voice assistance pipeline. The primary goal is to convert voice inputs into actionable text commands, process these commands, and optionally generate voice responses. The pipeline is structured in multiple stages, each focusing on a critical part of the voice processing flow.

### Architecture
1. **Voice-to-Text Conversion**: Converts spoken language into text using a Speech-to-Text (STT) model.
2. **Command Processing**: Analyzes the text to determine the user's intent and generate appropriate responses or actions.
3. **Text-to-Speech (Optional)**: Converts the generated text responses back into speech to provide audio feedback to the user.

Each stage will be explained and documented thoroughly, along with the associated code implementation.


## Step 1: Voice-to-Text Conversion

### Overview:
In this step, we convert voice input (from a microphone or audio file) into text using a Speech-to-Text (STT) model. We utilize OpenAI's Whisper model, known for its low latency and high accuracy, making it ideal for real-time applications.

### Architecture Details:
1. **Model Selection**: We use OpenAI's Whisper model, particularly optimized for low-latency speech recognition.
   - **Model**: Whisper (from Whisper.cpp)
   - **Pre-trained Model**: English (en-US)

2. **Audio Preprocessing**:
   - **Sampling Rate**: 16 kHz (standard for high-quality STT)
   - **Audio Channel Count**: 1 (mono for simpler processing)
   
3. **Voice Activity Detection (VAD)**:
   - **VAD Threshold**: 0.5
   - **VAD Implementation**: Detects when the speaker is talking, ignoring silence to reduce unnecessary processing and latency.
   - **VAD Integration**: Implemented using an energy-based thresholding method that checks the energy level of the audio segments.


# Step 2: Text Input into LLM
In this step, we will input the transcribed text from Step 1 into a large language model (LLM) to generate a response. The process involves installing the necessary libraries, loading the GPT-2 model, and using it to generate text based on the provided input.Step 2: Text Input into LLM

##Load GPT-2 Model and Tokenizer

* Import Required Libraries: The GPT2LMHeadModel and GPT2Tokenizer classes are  imported from the transformers library. These classes are essential for working with the GPT-2 model.

* Load GPT-2 Model and Tokenizer:

* Model Name: The model_name variable is set to "gpt2", indicating the use of the base GPT-2 model.
* Tokenizer Initialization: The GPT2Tokenizer is loaded with the specified model_name. The tokenizer is responsible for converting text into a format that the GPT-2 model can process.
* Model Initialization: The GPT2LMHeadModel is loaded with the specified model_name. This model is used to generate text based on the input provided.
The tokenizer and model objects are now ready for use in text generation tasks.

## Generate Text Based on Input


1. Set Input Text:


* input_text is assigned the value of text_query, which contains the transcribed text from Step 1. This text will be used as the input for the GPT-2 model.
2. Encode Input Text and Generate Response:

* Tokenization: The tokenizer.encode method converts the input_text into token IDs that the GPT-2 model can process. The return_tensors="pt" argument ensures the tokens are returned as PyTorch tensors.
* Text Generation: The model.generate method takes the tokenized input and generates a response. max_length=50 limits the length of the generated response to 50 tokens, and num_return_sequences=1 specifies that only one response should be generated.
3. Decode and Print Response:

* Decoding: The tokenizer.decode method converts the generated token IDs back into human-readable text. The skip_special_tokens=True argument ensures that special tokens used by the model are not included in the final output.
Output: The generated response is printed to the console for review.


# Step 3: Text-to-Speech Conversion
In this step, we will convert the text generated by the LLaMA model (from Step 2) into speech using the Edge TTS model. The process involves installing the required library, setting up the TTS model, and generating and saving the speech audio.


