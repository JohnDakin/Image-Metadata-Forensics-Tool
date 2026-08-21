# 🔍 Image Metadata Forensics Tool

## 📖 Overview

**Image Metadata Forensics Tool** is a Python-based digital forensics utility designed to extract and analyze **EXIF (Exchangeable Image File Format) metadata** from image files.

The tool uses the **Pillow** library to inspect image metadata and can extract information such as:

* Camera information
* Image information
* Date and time metadata
* GPS coordinates
* Other available EXIF tags

When GPS information is available, the tool converts the coordinates into decimal degrees and generates a **Google Maps URL** that can be used to visualize the location associated with the image.

> ⚠️ **Educational and authorized-use disclaimer:** This project is intended for educational, forensic, and authorized security testing purposes. Only analyze images that you own or have explicit permission to examine.

---

# 🎯 Project Objectives

The main objectives of this project are to demonstrate how image metadata can be extracted and analyzed using Python.

The project provides practical experience with:

* Digital image forensics
* EXIF metadata extraction
* GPS metadata analysis
* Python file handling
* Data conversion
* CSV data storage
* Basic forensic investigation techniques

---

# ⚙️ How It Works

The tool follows this general process:

```text
                    Image Files
                        │
                        ▼
                ┌───────────────┐
                │ Pillow        │
                │ Image Reader  │
                └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │ EXIF Metadata │
                │ Extraction    │
                └───────┬───────┘
                        │
              ┌─────────┴─────────┐
              │                   │
              ▼                   ▼
        General Metadata      GPS Metadata
              │                   │
              │                   ▼
              │             Coordinate
              │              Conversion
              │                   │
              │                   ▼
              │             Google Maps
              │                  URL
              │                   │
              └─────────┬─────────┘
                        ▼
                 Output Results
```

---

# 📂 Project Structure

```text
Image-Metadata-Forensics-Tool/
│
├── exif.py
├── exif_csv.py
├── exif_data.csv
└── README.md
```

### Files

| File            | Description                                                                    |
| --------------- | ------------------------------------------------------------------------------ |
| `exif.py`       | Extracts EXIF metadata and outputs the results to the terminal or a text file. |
| `exif_csv.py`   | Extracts EXIF metadata and stores the results in CSV format.                   |
| `exif_data.csv` | CSV file used to store extracted metadata from images.                         |
| `README.md`     | Project documentation.                                                         |

---

# 🐍 `exif.py`

The main script extracts metadata from images located in the `images` directory.

The script currently supports:

* `.JPG`
* `.TIFF`

The implementation could be extended in the future to support additional image formats such as PNG and HEIC.

## Output Options

When the script starts, it asks how you want to receive the extracted information:

```text
How do you want to receive the output:

1 - File
2 - Terminal
Enter choice here:
```

### Option 1 — File

The extracted information is redirected to:

```text
exif_data.txt
```

### Option 2 — Terminal

The metadata is displayed directly in the terminal.

---

# 🌍 GPS Metadata Extraction

One of the main features of the project is the ability to identify GPS information embedded within an image.

The tool looks for:

```text
GPSLatitude
GPSLongitude
GPSLatitudeRef
GPSLongitudeRef
```

The GPS coordinates are initially stored using the **degrees/minutes/seconds (DMS)** format.

For example:

```text
Latitude: 1° 17' 0"
Longitude: 36° 49' 0"
```

The tool converts these coordinates into decimal degrees using:

```python
decimal_degrees = degree + minutes / 60 + seconds / 3600
```

South and West coordinates are converted to negative values.

---

# 🗺️ Google Maps Integration

After GPS coordinates have been extracted and converted, the tool generates a Google Maps URL.

The resulting link follows this format:

```text
https://maps.google.com/?q=LATITUDE,LONGITUDE
```

This makes it possible to quickly visualize the location associated with the image when GPS metadata is present.

---

# 📄 CSV Metadata Extraction

The `exif_csv.py` script provides an alternative output format.

Instead of displaying all extracted metadata in the terminal, it writes the information to:

```text
exif_data.csv
```

The CSV output can contain:

* Filename
* EXIF tags
* Camera information
* GPS information
* Latitude
* Longitude
* Google Maps link

This makes the extracted metadata easier to analyze using spreadsheet software or Python data-analysis tools.

---

# 🚀 Installation

## 1. Clone the Repository

```bash
git clone https://github.com/JohnDakin/Image-Metadata-Forensics-Tool.git
```

## 2. Navigate to the Project

```bash
cd Image-Metadata-Forensics-Tool
```

## 3. Install Pillow

The project uses **Pillow** for image processing and EXIF extraction.

```bash
python3 -m pip install --upgrade pip
python3 -m pip install --upgrade Pillow
```

The repository's scripts specifically require Pillow rather than the older PIL package.

---

# 📁 Preparing Images

Create an `images` directory inside the project:

```text
Image-Metadata-Forensics-Tool/
│
├── images/
│   ├── image1.jpg
│   ├── image2.jpg
│   └── image3.jpg
│
├── exif.py
├── exif_csv.py
└── README.md
```

Place the images you are authorized to analyze inside the `images` directory.

---

# ▶️ Running the Tool

## Extract Metadata to Terminal or Text File

Run:

```bash
python3 exif.py
```

The program will ask whether you want the output saved to a file or displayed in the terminal.

If you select:

```text
1
```

the output is saved to:

```text
exif_data.txt
```

If you select:

```text
2
```

the metadata is displayed directly in the terminal.

---

# 📊 Export Metadata to CSV

To extract metadata into a CSV file, run:

```bash
python3 exif_csv.py
```

The script writes the extracted information to:

```text
exif_data.csv
```

This is useful when analyzing metadata from multiple images or when you want to process the results using spreadsheet software or another data-analysis tool.

---

# 🔎 Example Investigation Workflow

A basic forensic workflow could look like this:

```text
1. Obtain an authorized image
          ↓
2. Place the image in ./images
          ↓
3. Run exif.py
          ↓
4. Extract EXIF metadata
          ↓
5. Check for GPS information
          ↓
6. Convert GPS coordinates
          ↓
7. Generate Google Maps link
          ↓
8. Analyze the available metadata
```

---

# 🧪 Example Metadata

An image may contain metadata similar to:

```text
Make - Canon
Model - Canon EOS 80D
DateTimeOriginal - 2026:01:15 14:32:10
ExposureTime - 1/250
FNumber - 2.8
ISOSpeedRatings - 400
```

If GPS metadata is available, the output may also contain:

```text
GPSLatitude - (...)
GPSLatitudeRef - N
GPSLongitude - (...)
GPSLongitudeRef - E
Google Maps Link - https://maps.google.com/?q=...
```

The exact metadata depends on what information was embedded in the original image.

---

# ⚠️ Important Metadata Considerations

Not every image contains EXIF metadata.

For example, the script explicitly checks whether EXIF data exists and reports when an image contains no EXIF information.

Additionally, many social media platforms remove EXIF metadata when images are uploaded, meaning an image downloaded from social media may contain little or no original metadata.

Therefore:

> **The absence of EXIF data does not necessarily mean that an image never contained metadata.**

It may have been removed or stripped during processing or upload.

---

# 🛠️ Technologies Used

* **Python 3**
* **Pillow**
* **CSV**
* **EXIF**
* **GPS coordinate conversion**

---

# 🔐 Security & Privacy

EXIF metadata can contain sensitive information, especially:

* GPS location
* Date and time
* Camera/device information
* Software information
* Image creation details

Before publicly sharing photographs, consider checking whether they contain sensitive metadata.

This tool should only be used to analyze images that you own or are explicitly authorized to examine.

---

# 🔮 Future Improvements

Potential improvements include:

* Support for PNG images
* Support for HEIC images
* Recursive directory scanning
* Command-line arguments
* JSON output
* Better error handling
* Metadata filtering
* Interactive forensic reports
* Batch processing improvements
* Automatic metadata risk assessment
* Web-based interface
* EXIF metadata visualization

---

# 📚 Learning Objectives

This project demonstrates practical knowledge of:

* Python programming
* Image processing
* EXIF metadata
* Digital forensics
* GPS coordinate systems
* File handling
* CSV generation
* Data analysis
* Privacy and information security

---

# 👨‍💻 Author

**John Dakin**

GitHub: [JohnDakin](https://github.com/JohnDakin)

Repository: [Image-Metadata-Forensics-Tool](https://github.com/JohnDakin/Image-Metadata-Forensics-Tool)

---

# ⚖️ Disclaimer

This project is provided for **educational purposes and authorized forensic analysis only**.

Do not use this tool to analyze photographs or metadata belonging to other people without appropriate authorization.

The author is not responsible for misuse of this software.

---

## ⭐ Support

If you find this project useful for learning about Python, EXIF metadata, or digital forensics, consider giving the repository a ⭐ on GitHub.
