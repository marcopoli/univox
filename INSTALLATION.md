# Installation Guide

Complete installation guide for Study Buddy with GPU support.

## Prerequisites

### Required Software

1.  **Python 3.10+**

      * Download from: [https://www.python.org/downloads/](https://www.python.org/downloads/)
      * During installation, select **"Add Python to PATH"**

2.  **NVIDIA GPU Drivers** (optional, for GPU support)

      * Download from: [https://www.nvidia.com/Download/index.aspx](https://www.nvidia.com/Download/index.aspx)
      * Verify installation with: `nvidia-smi`

3.  **FFmpeg** (for audio/video processing)

      * Download from: [https://www.gyan.dev/ffmpeg/builds/](https://www.gyan.dev/ffmpeg/builds/)
      * Extract and add the `bin` folder to the system PATH

4.  **Tesseract OCR** (for image OCR)

      * Download from: [https://github.com/UB-Mannheim/tesseract/wiki](https://github.com/UB-Mannheim/tesseract/wiki)
      * Add to the system PATH

5.  **Poppler** (optional, for OCR of scanned PDFs)

      * Download from: [https://github.com/oschwartz10612/poppler-windows/releases/](https://github.com/oschwartz10612/poppler-windows/releases/)
      * Extract and add the `bin` folder to the PATH

-----

## Automatic Installation (Recommended)

### Windows

1.  Open PowerShell in the project folder.
2.  Run the setup script:
    ```powershell
    .\setup.ps1
    ```

The script:

  * Automatically creates the virtual environment.
  * Detects the presence of an NVIDIA GPU.
  * Installs the correct version of PyTorch (CPU or CUDA).
  * Installs all necessary dependencies.

-----

## Manual Installation

### 1\. Create the virtual environment

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### 2\. Install PyTorch

**With GPU (CUDA 12.8):**

```powershell
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
```

**CPU Only:**

```powershell
pip install torch torchvision torchaudio
```

### 3\. Install dependencies

```powershell
pip install -r requirements.txt
```

### 4\. Install additional packages

```powershell
pip install ffmpeg-python youtube-transcript-api wikipedia google-search-results
```

-----

## Configuration

### 1\. Create the `.env` file

Copy `.env.example` to `.env` and configure your API keys:

```bash
# LLM Providers
TOGETHER_API_KEY=your_together_api_key
GOOGLE_API_KEY=your_google_api_key

# Audio Services
ELEVEN_API_KEY=your_elevenlabs_api_key
ASSEMBLYAI_API_KEY=your_assemblyai_api_key

# Search & Tools
SERP_API_KEY=your_serpapi_key
TAVILY_API_KEY=your_tavily_api_key
GOOGLE_LENS_API_KEY=your_google_lens_key
IMGBB_API_KEY=your_imgbb_key

# Code Execution
E2B_API_KEY=your_e2b_api_key
```

### 2\. Verify installation

```powershell
python -c "import torch; print(f'PyTorch: {torch.__version__}'); print(f'CUDA: {torch.cuda.is_available()}')"
```

-----

## Running the Application

```powershell
streamlit run streamlit_frontend.py
```

The application will be available at: http://localhost:8502

-----

## Troubleshooting

### GPU not detected

If you have an NVIDIA GPU but PyTorch is using the CPU:

1.  Check NVIDIA drivers: `nvidia-smi`
2.  Reinstall PyTorch with CUDA:
    ```powershell
    pip uninstall torch torchvision torchaudio
    pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
    ```

### Import Errors

If you receive `ModuleNotFoundError` errors:

```powershell
pip install <missing_package_name>
```

Common packages that might be missing:

  * `ffmpeg-python`
  * `youtube-transcript-api`
  * `wikipedia`
  * `google-search-results`

### OCR Errors

If OCR is not working:

1.  Verify that Tesseract is installed: `tesseract --version`
2.  Verify that it is in the system PATH.
3.  For scanned PDFs, ensure Poppler is installed.

### Ctrl+C not working

Streamlit sometimes doesn't respond immediately to Ctrl+C on Windows. Solutions:

1.  Press Ctrl+C multiple times.
2.  Close the terminal window.
3.  Use Task Manager to terminate the Python process.

-----

## Updating

To update dependencies:

```powershell
pip install --upgrade -r requirements.txt
```

## Support

For issues or questions, consult:

  * The project README.md
  * Streamlit Documentation: [https://docs.streamlit.io/](https://docs.streamlit.io/)
  * PyTorch Documentation: [https://pytorch.org/docs/](https://pytorch.org/docs/)
