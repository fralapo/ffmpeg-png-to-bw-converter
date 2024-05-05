### Introduction
This repository contains a script to convert PNG images to black and white while preserving transparency using the ffmpeg tool. It provides commands for both PowerShell (Windows) and the terminal (Linux) to automate the conversion process.

### Prerequisites
Before using the script, ensure you have the following installed on your system:
- [ffmpeg](https://ffmpeg.org/): A powerful multimedia framework that can decode, encode, transcode, mux, demux, stream, filter, and play almost any type of media files.

### How it Works
The script utilizes ffmpeg's capabilities to convert PNG images to black and white while maintaining transparency. It iterates over each PNG file in the directory and applies the necessary ffmpeg command.

### Usage
1. Open PowerShell (Windows) or the terminal (Linux) and navigate to the directory containing the PNG images you want to convert.
2. Run the following command:
   - For PowerShell (Windows):
     ```powershell
     Get-ChildItem -Filter *.png | ForEach-Object {
         $newName = "bw_$($_.Name)"
         ffmpeg -i $_.FullName -vf "format=rgba,colorchannelmixer=0.299:0.587:0.114:0:0.299:0.587:0.114:0:0.299:0.587:0.114:0" $newName
     }
     ```
   - For Terminal (Linux):
     ```bash
     for file in *.png; do ffmpeg -i "$file" -vf "format=rgba,colorchannelmixer=0.299:0.587:0.114:0:0.299:0.587:0.114:0:0.299:0.587:0.114:0" "bw_${file%.*}.png"; done
     ```

### Command Explanation
Here's an explanation of the command used in the script:

- For PowerShell (Windows):
  - `Get-ChildItem -Filter *.png`: Retrieves all PNG files in the current directory.
  - `ForEach-Object { ... }`: Iterates over each PNG file.
  - `$newName = "bw_$($_.Name)"`: Generates a new filename for the converted image by prefixing "bw_" to the original filename.
  - `ffmpeg -i $_.FullName -vf "format=rgba,colorchannelmixer=0.299:0.587:0.114:0:0.299:0.587:0.114:0:0.299:0.587:0.114:0" $newName`: Executes the ffmpeg command to convert the PNG image to black and white while preserving transparency.

- For Terminal (Linux):
  - `for file in *.png; do ...; done`: Loops through each PNG file in the directory.
  - `ffmpeg -i "$file" -vf "format=rgba,colorchannelmixer=0.299:0.587:0.114:0:0.299:0.587:0.114:0:0.299:0.587:0.114:0" "bw_${file%.*}.png"`: Executes the ffmpeg command to convert the PNG image to black and white while preserving transparency, and saves it with a new filename prefixed with "bw_" using Bash parameter expansion.

### License
This project is licensed under the [MIT License](LICENSE).

### Acknowledgments
Special thanks to the developers of ffmpeg for providing such a versatile multimedia framework.

Feel free to contribute or report issues in this repository!
