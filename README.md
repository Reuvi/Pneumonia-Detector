# Pneumonia Detection (Website Tool)

This repository contains a small web experience that lets you upload a **chest X‑ray** and get a **model prediction** of *Pneumonia* vs *Normal*. It’s intended for learning and demos only — **not for medical use**.

## How it works
- A **Flask** server (`server.py`) serves a simple UI (Jinja templates in `templates/`) where you can upload an image.
- The uploaded file is saved to `uploads/`, preprocessed, and passed to a **CNN** model loaded from `BestModel/`.
- The server returns a predicted **class** and **confidence**, which are rendered back to the page.

> Note: The repo ships with model artifacts in `BestModel/`. Architecture/training code is not part of this repository. If you replace the model, make sure the preprocessing and input shape match.

## Quick start (local)
1. **Clone** the repo and create a virtual environment (optional but recommended).
2. **Install dependencies** (typical stack):
   ```bash
   pip install flask tensorflow pillow numpy
   ```
   If your model was exported with a different runtime (e.g., PyTorch), install that framework instead.
3. **Run the server**:
   ```bash
   python server.py
   ```
4. Open the site at **http://127.0.0.1:5000** and upload a chest X‑ray to test.

## Repository layout
```
BestModel/           # Saved model files used for inference
project_1_images/    # Sample images / assets (if present)
templates/           # Jinja2 HTML templates (web UI)
uploads/             # Uploaded images (runtime)
server.py            # Flask app (routes, preprocessing, inference)
image_tester.py      # CLI helper for testing images locally
README.md            # This file
```
> Folder and file names may differ slightly depending on your branch. See the source for the latest layout.

## API (optional)
If you want to call the model directly, you can expose/extend a JSON endpoint in `server.py` such as:
```
POST /predict
Form-Data: image=<file>
Response: { "label": "PNEUMONIA" | "NORMAL", "confidence": 0.00-1.00 }
```
Adjust names to match your actual route handlers.

## Model & data
- **Input**: single chest X‑ray image (JPG/PNG).
- **Preprocessing**: resize and normalize to match the model’s input shape (e.g., 224×224 or 299×299).
- **Output**: binary classification (Pneumonia / Normal) with a confidence score.

If you swap in your own model, ensure the same preprocessing pipeline is used.

## Important notice
This tool is for **education and demonstration**. It is **not a diagnostic device** and **not cleared for clinical use**. Do not use it to make medical decisions.

## Contributing
- Bug reports and small fixes (typos, doc updates, input validation) are welcome.
- If you add a new model, document its expected input size and preprocessing.

---

### Maintainer
Built by **Reuvi**. Feel free to open an issue if something in the README needs clarification.
