## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:

### DESIGN STEPS:

#### STEP 1:
Load the Hugging Face API and create a Client to connect to the FalconLM text-generation model.

#### STEP 2:
Create the generate() function to take the user’s prompt and maximum token value and return the generated text.


#### STEP 3:
Build the Gradio interface with a prompt box, token slider, and completion output, then launch the app.

### PROGRAM:
```
import os
import io
import IPython.display
from PIL import Image
import base64 
import requests 
requests.adapters.DEFAULT_TIMEOUT = 60

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
hf_api_key = os.environ['HF_API_KEY']

# Helper function
import requests, json
from text_generation import Client

#FalcomLM-instruct endpoint on the text_generation library
client = Client(os.environ['HF_API_FALCOM_BASE'], headers={"Authorization": f"Basic {hf_api_key}"}, timeout=120)

#Back to Lesson 2, time flies!
import gradio as gr
def generate(input, slider):
    output = client.generate(input, max_new_tokens=slider).generated_text
    return output

demo = gr.Interface(fn=generate, 
                    inputs=[gr.Textbox(label="Prompt"), 
                            gr.Slider(label="Max new tokens", 
                                      value=20,  
                                      maximum=1024, 
                                      minimum=1)], 
                    outputs=[gr.Textbox(label="Completion")])

gr.close_all()
demo.launch(share=True, server_port=int(os.environ['PORT1']))
```

### OUTPUT:
<img width="1707" height="921" alt="image" src="https://github.com/user-attachments/assets/12456415-fec0-4362-9273-5db3cc1894b6" />


### RESULT:
Therefore,the program for Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework is executed successfully and the output is verified.
