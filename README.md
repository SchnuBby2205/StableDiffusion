# StableDiffusion

Not sure what errors you are getting, but here are the steps I took to get ComfyUI to run on my Radeon RX 5700 XT under Arch Linux:

    In a terminal, run git clone https://github.com/comfyanonymous/ComfyUI.git
    In a terminal, run cd ComfyUI
    Put your Stable Diffusion model files in ComfyUI/models/checkpoints
    Put your VAE model files into ComfyUI/models/vae if you have any
    In a terminal, run virtualenv -p 3.10 sdxl (This creates a Python virtual environment to prevent this from clogging up your main system Python since we need specific versions of packages to make ComfyUI work)
    In a terminal, run source sdxl/bin/activate (This activates the Python virtual environment. Must be done every time you launch ComfyUI from a new terminal window)
    In a terminal, run pip install torch==1.13.1+rocm5.2 torchvision==0.14.1+rocm5.2 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/rocm5.2. (Note that this is different from the official installation steps. ROCm 5.4.2/Torch 2.0+ doesn't run on the RX 5700 XT, we need this older version for our technically unsupported cards.)
maybe install numpy 1.26.0 (pip install numpy==1.26.0)
    In a terminal, do pip install -r requirements.txt
    In a terminal, run HSA_OVERRIDE_GFX_VERSION=10.3.0 python main.py --force-fp32. ComfyUI should launch and you should be able to access the UI in your web browser at http://127.0.0.1:8188 after it finishes loading. (look in the terminal for the message To see the GUI, go to http://127.0.0.1:8188 to know when it has finished loading)
    Enter your prompt and negative prompt, set your image size and batch settings, and hit Queue Prompt. Your GPU fan should kick on after a minute or so and the UI should start indicating progress (Look for a green outline moving around the screen and after a minute or two a progress bar should show up in the terminal and in the box titled KSampler)

After all that, ComfyUI should output an image to the ComfyUI/outputs directory. To launch ComfyUI subsequent times, follow step 6, then step 9. My RX 5700 XT can output an image in 2-6 minutes using Stable Diffusion XL, so if your image is taking 10+ minutes to generate or the progress bar never shows up, something is not working correctly.

Get ComfyUI Manager
https://github.com/ltdrdata/ComfyUI-Manager
