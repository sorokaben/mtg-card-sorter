
# MTG CardSorter

### Automated Magic: The Gathering Card Recognition and Sorting

MTG CardSorter is a computer vision and automation project designed to identify Magic: The Gathering cards and determine how they should be sorted.

The software analyzes card images, retrieves card information using the Scryfall API, and assigns each card to a sorting bin based on its properties.

The project was developed as part of a multidisciplinary effort to build a physical card-sorting system combining software, computer vision, electronics, and mechanical design.

## Project Demonstration

[**Watch CardSorter in Action on YouTube**](https://www.youtube.com/shorts/cT059USOEd8)

![CardSorter in Action](cardsorter_gif.gif)

## Features

- **Card Recognition:** Identify Magic: The Gathering cards from images.
- **Live Camera Recognition:** Capture and identify cards directly
  from a connected camera using OpenCV.
- **API Integration:** Retrieve card information using the Scryfall API.
- **Multiple Sorting Modes:** Classify cards based on type, color, or value.
- **Batch Processing:** Process multiple card images and organize them into folders.
- **Performance Measurement:** Measure processing time for individual card images.
- **Command-Line Interface:** Run recognition and sorting operations through Python scripts.

### Supported Sorting Modes

| Mode | Description |
|------|-------------|
| `type` | Sorts cards into Creatures, Spells, Permanents, or Lands |
| `color` | Sorts cards according to color |
| `value` | Sorts cards according to value |

## Technologies

- **Python** — Core application logic and automation
- **Google Cloud Vision** — Image recognition and text extraction
- **Scryfall API** — Magic: The Gathering card identification and metadata
- **Command-Line Tools** — Individual and batch image processing

The broader physical system also involved microcontrollers, servo and stepper motors, electrical wiring, and custom mechanical components.

## Getting Started

### Prerequisites

Before running the project, ensure you have:

- Python installed
- An internet connection for Scryfall API requests
- Google Cloud Vision credentials configured

The application expects a Google Vision credential file at:

`credentials/google-vision-key.json`

**Security note:** Never commit API keys, credentials, or other secrets to a public GitHub repository.

### Installation

Clone the repository:

```bash
git clone https://github.com/sorokaben/mtg-card-sorter.git
cd mtg-card-sorter
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

Configure your Google Cloud Vision credentials before running the application.

## Usage

### Live Camera Scanning

CardSorter supports real-time card recognition using a connected camera.

**To start live scanning:**

1. Connect your camera to your computer.
2. Launch the interactive application:

   ```bash
   python -m src.cli
   ```

3. Select option **5** from the menu:

   ```text
   5. Use Phone Camera To Scan
   ```

4. Position a Magic: The Gathering card in front of the camera.
5. The application will attempt to identify the card and send the result to the sorting system.
6. Press **Q** in the camera window to stop scanning.

**Camera configuration:**

The application currently uses OpenCV camera index `1`:

```python
cam = cv2.VideoCapture(1)
```

If your camera is not detected, try changing the index to `0` or another available device number in `src/cli.py`.

**Note:** Live camera scanning uses the sorting behavior defined in `main.py`. The `color`, `type`, and `value` modes are available through the software's sorting interface, but switching between these modes during live camera operation has not been verified.


### 1. Process a Single Card from Folder

To identify an individual card and determine its sorting bin:

```bash
python scripts/bin_from_path.py "data/Magic the gathering Iphone/Screenshot 2026-04-13 185409.png" --mode type
```

The script outputs:

- Identified card name
- Assigned sorting bin
- Processing time in seconds and milliseconds

This script runs with caching disabled, providing a cold-processing time measurement rather than relying on previously cached results.

Change the `--mode` argument to select a different sorting method.

### 2. Process a Folder of Card Images

To process multiple images and organize them into sorting folders:

```bash
python -m src.cli scan-inbox --in "data/Magic the gathering Iphone" --out "data/sorted_phone_dataset" --mode type
```

This command:

1. Reads images from the specified input directory.
2. Identifies each Magic: The Gathering card.
3. Determines the appropriate sorting bin.
4. Creates output directories corresponding to those bins.
5. Copies each image into its assigned directory.

## Project Structure

| Directory / File | Purpose |
|------------------|---------|
| `src/` | Core application code |
| `src/cli` | Command-line processing interface |
| `scripts/bin_from_path.py` | Single-image recognition and timing |
| `data/Magic the gathering Iphone/` | Example input images |
| `data/sorted_phone_dataset/` | Organized output images |
| `credentials/` | Local credential configuration |
| `requirements.txt` | Python dependencies |

Some directories and files may need to be configured locally before running the application.

## Troubleshooting

### Card Not Recognized

- Ensure the image is clear and properly focused.
- Check that the card name and relevant text are visible.
- Verify that Google Cloud Vision credentials are configured correctly.
- Confirm that an internet connection is available for Scryfall requests.

### Incorrect Card Printing

Scryfall may identify a different printing of the same card, resulting in a different set code.

In these cases, the selected sorting bin may still be correct for the intended sorting workflow.

## Development and Contributions

CardSorter was developed collaboratively as a multidisciplinary engineering project.

**My contributions included:**

- Leading the project team and coordinating development across technical disciplines.
- Supporting the integration of computer vision, software, microcontrollers, and mechanical components.
- Working directly on electrical wiring and hardware connections.
- Troubleshooting communication and timing issues between hardware and software.
- Helping coordinate testing and integration of the completed physical system.

The project provided hands-on experience with systems integration, technical problem-solving, software development, and collaborative engineering.

## Project Status

**Completed — May 2026**

The project was completed as an academic team project and serves as a demonstration of software integration, automation, and electromechanical system development.
